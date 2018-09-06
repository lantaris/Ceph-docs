# Команды  управления демонами Ceph

** Запуск/Остановка/Перезапуск монитора MON

	systemctl [start|stop|restart] ceph-mon.target

** Запуск/Остановка/Перезапуск всех OSD хоста

	systemctl [start|stop|restart] ceph-osd.target

** Запуск/Остановка/Перезапуск менеджера MGR

	systemctl [start|stop|restart] ceph-mgr.target

** Запуск/Остановка/Перезапуск OSD на хосте <OSD Num> - номер OSD

	systemctl [start|stop|restart] ceph-osd@<OSD Num>.service
