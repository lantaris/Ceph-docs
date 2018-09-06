# Развесовка данных кластера Ceph

## Посмотреть веса узлов и OSD
	ceph osd df
	ceph osd tree
	
## Принудительное изменение "веса" OSD 
	# <OSD Num> - номер OSD
	# <weight> - новый вес
	ceph osd crush reweight osd.<OSD Num> <weight>

## Изменение весов OSD с расчета их объема и текущей занятости 
## (В данном случае меняется параметр  вторичного взвешивания REWEIGHT, а не WEIGHT)
	# Проверка ребалансировки без изменения.
	ceph osd test-reweight-by-utilization    
	
	# Ребалансировка (изменение параметров вторичного взвешивания)
	ceph osd reweight-by-utilization	 

## Ребалансировка  с использованием MGR/balancer
## (рекомендуется запуск в ненагруженное время)
	# (пример 7%) Настройка порога, при котором балансировшик будет распределять данные
	ceph config-key set mgr/balancer/max_misplaced .07   	

	# Активация плагина MGR/balancer (не запускает процесса балансировки)
	ceph mgr module enable balancer				

	# Тип балансировки приближен к CRUSHMAPу
	ceph balancer mode crush-compat				

	# Запуск процесса балансировки данных
	ceph balancer on					# Запуск процесса балансировки данных

## Остановить MGR/balancer можно таким образом
	ceph balancer off
