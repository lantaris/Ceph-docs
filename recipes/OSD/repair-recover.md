# Проверка и восстановление 

## Процесс полной проверки рекомендуется запускать в ненагруженное время
	ceph osd scrub osd.<OSD Num>		# Запуск процесса проверки данных OSD или PG или "all" (Статус процесса "ceph health detail")
	ceph osd deep-scrub osd.<OSD Num>	# Запуск процесса глубокой проверки данных OSD или PG или "all" (Статус процесса "ceph health detail")
	ceph osd repair osd.<OSD Num>|PG_id	# Запуск процесса восстановления данных OSD или PG или "all" (Статус процесса "ceph health detail")

