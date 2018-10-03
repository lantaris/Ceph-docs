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