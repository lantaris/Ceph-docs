#  Удаление или замена сбойного OSD

##Удаление сбойного OSD

**Эвакуация данных**

	# Если OSD еще хоть как - то жив, можно заставить Ceph эвакуировать с него данные
	# 
	# <OSD Num>  - номер OSD (Номер OSD можно посмотреть командами "ceph osd tree", "ceph osd df", "ceph osd status"
	# 
	# По ошибке выведенный в OUT OSD можно вернуть в нормальное (IN) состояние комендой "ceph osd in <OSD Num>"
	#  
	ceph osd out osd.<OSD Num>  


**После эвакуации данных, если это требовалось, проверяем что данные эвакуировались и можно безопасно удалять OSD**
 
	ceph osd safe-to-destroy <OSD Num>

**Останавливаем на нужном хосте сбойный OSD**
	
	# Останавливаем демон OSD
	systemctl stop ceph-osd@<OSD Num>.service
	
	# Проверяем, что остановлен именно тот OSD
	ceph osd status
	

**Удаляем OSD из кластера**

	ceph osd purge osd.<OSD Num>

**Удаление OSD из CRUSHMAP(не обязательно, предыдущая команда удаляет OSD из CRUSHMAP)**

        ceph osd crush remove osd.<OSD Num>

**Удаляем остатки OSD**

	# Если много OSD и требуется детальный разбор полетов можно использовать следующие команды:
	#
	#  readlink -f /var/lib/ceph/osd/ceph-<OSD Num>/* 	# Паказывает ссылки 
	#  lsblk -f 										# Список дисковых устройств
	#  dmsetup ls										# соответствие разделов или LVM их /dev/dm<номер>
	#  lvs												# По флагу -o- можно понять используется в данный момент том или нет.
	#
	umount /var/lib/ceph/osd/ceph-<OSD Num>
	rmdir /var/lib/ceph/osd/ceph-<OSD Num>

**Извлекаем сбойный диск. Перед этим выполнив команду**

	echo 1 > /sys/block/<data-disk>/device/delete

##Добавление нового OSD


**После физической замены диска. Смотрим какое именно устройство будет использовано под OSD. По результатам команды находим диск**

	lsblk -f

**Чистим все что там есть под 0**

	wipefs -af /dev/<устройство>

**Поднимаем новый OSD c помощью ceph-deploy с admin хоста**

	ceph-deploy osd create --data /dev/<Устройство> <хост>

**Дожидаемся окончания процесса ребаланса данных и получаем HEALTH_OK**

**Проверяем состояние как все распределилось и что все в рабочем состоянии**

	ceph status
	ceph osd status
	ceph osd tree
	ceph osd df
