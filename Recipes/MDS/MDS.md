## Настройка CephFS (MDS).

**Развертывание MDS демонов**

	ceph-deploy mds create <Server1> <Server2> <Server3>

**Создание пулов для хранения CephFS.**

	# PGs расчитываются по формуле
	#
	#         (OSDs * 100)
	# <PGs> = ------------
	#          pool size
	#
	# (Результат должен быть округлен до ближайшей степени 2)
	#
	ceph osd pool create cephfs_data <PGs> [<PGP>]
	ceph osd pool application enable cephfs_data cephfs
	ceph osd pool create cephfs_metadata <PGs> [<PGP>]
	ceph osd pool application enable cephfs_metadata cephfs

**Создание пулов, которые требуются только при использовании NFS-Ganesha**

	ceph osd pool create nfs-ganesha 8                         
	ceph osd pool application enable nfs-ganesha cephfs

**Присвоение CephFS (MDS) пулов хранения данных/метаданных**

	ceph fs new cephfs cephfs_metadata cephfs_data

**Активируем два MDS демона. По итогу получится не 1 активный и два в standby, а 2 - active, 1 - standby

	ceph fs set cephfs max_mds 2

**Создание пользователя cephpf с правами для работы с томом и выгрузка ключа доступа**

	ceph auth get-or-create client.cephfs mon 'allow r' mds 'allow rw' osd 'allow rw pool=cephfs_data, allow rw pool=nfs-ganesha' -o /etc/ceph/ceph.client.cephfs.keyring
	ceph auth get-key client.cephfs | tee /etc/ceph/client.cephfs.key

**Варианты монтирование CephFS**

	mount -t ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs
	mount -t ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=cephfs,secret=<secret key>
	mount -t ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=cephfs,secretfile=/etc/ceph/client.cephfs.key
	#
	# Равнозначные команды
	#
	mount.ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs
	mount.ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=cephfs,secret=<secret key>
	mount.ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=cephfs,secretfile=/etc/ceph/client.cephfs.key

