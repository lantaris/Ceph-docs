## Перевод кластера в режим обслуживания

**Перевод в режим обслуживания**

	ceph osd set noout
	ceph osd set nobackfill
	ceph osd set norecover
	ceph osd set norebalance
	ceph osd set nodown
	ceph osd set pause

**Снятие режима обслуживания**

	ceph osd unset noout
	ceph osd unset nobackfill
	ceph osd unset norecover
	ceph osd unset norebalance
	ceph osd unset nodown
	ceph osd unset pause

**При выводе одной из нод кластера в обслуживание нужно установить**

	ceph osd set noout	  - Не уносить данные с OSD
	ceph osd set norebalance  - Не производить ребаланс кластера

**После возврата ноды в кластер нужно снять ранее установленные флаги**

	ceph osd unset noout 
	ceph osd unset norebalance