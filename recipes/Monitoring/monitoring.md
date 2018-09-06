# Команды мониторинга кластера Ceph

**Мониторинг кластера**

	ceph -s					# Общий статус кластера Ceph
	ceph status				# Общий статус кластера Ceph
	ceph -w					# Мониторинг кластера в реальном времени
	ceph health detail		# Детальный статус здоровья

**Список доступов(пользователей)**

	ceph auth list			

**Мониторинг OSD и структуры**

	ceph osd tree					# Структура кластера
	ceph osd df  					# Текущее состояние OSD (веса, занятость, PGS)
	ceph osd dump					# Детальная информация о OSD
	ceph tell osd.<OSD Num> bench	# Проверка скорости определенного OSD

**Пулы**

	ceph osd pool get <pool> all	# Настройки пула
	ceph pg dump pgs				# Дамп всех PGs
	ceph pg dump					# Статистика для групп мест размещения
	rbd du <pool>/<volume>			# Информация размер/занимаемый размер тома в RBD пуле
	rbd ls -l <pool>				# Содержимое пула
	ceph osd lspools				# Список пулов
	rados df 						# Сводная информация о размерах и свободном месте в пулах

**CephFS (MDS)**

	ceph mds stat
	ceph mds dump
