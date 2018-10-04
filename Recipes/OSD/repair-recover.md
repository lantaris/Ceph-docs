## Проверка и восстановление 

### Процесс полной проверки рекомендуется запускать в ненагруженное время

**Запуск процесса проверки данных OSD или PG или "all"**

	ceph osd scrub <osd.(OSD Num)|PG Num|all> 

**Запуск процесса глубокой проверки данных OSD или PG или "all")**

	ceph osd deep-scrub <osd.(OSD Num)|PG Num|all>

**Детальный статус ошибок можно посмотреть**
	
	ceph health detail

**Запуск процесса восстановления данных**

	ceph osd repair <osd.(OSD Num)|PG Num|all>

