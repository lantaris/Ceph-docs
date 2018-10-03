## Анализ поведения трафика  кластера Ceph при его работе с использованием кластерной и публичной сети ##


### Исходные данные ###

Все тесты производились на виртуальных машинах в ОС Centos 7 + libivirt + virt-manager. 


**Виртуальные машины:**

	h201: vda(50Gb)-система vdb(100Gb)-OSD
		  eth0:10.0.2.201/24(публичная) eth1:10.0.3.201/24(кластерная)
	h201: vda(50Gb)-система vdb(100Gb)-OSD
		  eth0:10.0.2.202/24(публичная) eth1:10.0.3.202/24(кластерная)
	h201: vda(50Gb)-система vdb(100Gb)-OSD
		  eth0:10.0.2.203/24(публичная) eth1:10.0.3.203/24(кластерная)
	h201: vda(50Gb)-система vdb(100Gb)-OSD
		  eth0:10.0.2.204/24(публичная) eth1:10.0.3.204/24(кластерная)

**Конфигурационный файл сeph.conf**
	
	[global]
	fsid = 5231a9c6-2a1f-4c49-bb1f-4946f35fd408
	public_network = 10.0.2.0/24
	cluster_network = 10.0.3.0/24
	mon_initial_members = h201, h202, h203
	mon_host = 10.0.2.201,10.0.2.202,10.0.2.203
	auth_cluster_required = cephx
	auth_service_required = cephx
	auth_client_required = cephx


**Пулы и MDSы**

	Пулы:

	1 cephfs_data size=3 PG=64
	2 cephfs_metadata size=3 PG=64

	MDS:

	0=h202=up:active
	1=h203=up:active
	2=h203=up:standby

**Точка монтирования:**

	mount -t ceph h201,h202,h203:/ /mnt/ceph -o name=cephfs,secret=<KEY>	

###Цель тестов:###

**Работа Ceph кластера с использованием кластерной и публичной сети:** 

1. Мониторинг и построение графиков при заполнении кластера.
   (test-clu.md, test-clu-graph.pdf)
2. Мониторинг и построение графиков при добавлении OSD и ребалансе данных.
   (test-rebalance-clu.md, test-rebalance-clu-graph.pdf)

**Работа Ceph кластера с использованием только публичной сети:** 

1. Мониторинг и построение графиков при заполнении кластера.
   (test-pub.txt, test-pub-graph.pdf)
2. Мониторинг и построение графиков при добавлении OSD и ребалансе данных.
   (test-rebalance-pub.txt, test-rebalance-pub-graph.pdf)

    