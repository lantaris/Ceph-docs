# ����ன�� CephFS (MDS).

## �������뢠��� MDS �������

	ceph-deploy mds create <Server1> <Server2> <Server3>

## �������� �㫮� ��� �࠭���� CephFS.

	# PGs ����뢠���� �� ��㫥
	#
	#         (OSDs * 100)
	# <PGs> = ------------
	#          pool size
	#
	# (������� ������ ���� ���㣫�� �� ������襩 �⥯��� 2)
	#
	ceph osd pool create cephfs_data <PGs> [<PGP>]
	ceph osd pool application enable cephfs_data cephfs
	ceph osd pool create cephfs_metadata <PGs> [<PGP>]
	ceph osd pool application enable cephfs_metadata cephfs

## �������� �㫮�, ����� �ॡ����� ⮫쪮 �� �ᯮ�짮����� NFS-Ganesha
	ceph osd pool create nfs-ganesha 8                         
	ceph osd pool application enable nfs-ganesha cephfs

## ��᢮���� CephFS (MDS) �㫮� �࠭���� ������/��⠤�����

	ceph fs new cephfs cephfs_metadata cephfs_data

## �������� ���짮��⥫� cephpf � �ࠢ��� ��� ࠡ��� � ⮬�� � ���㧪� ���� ����㯠

ceph auth get-or-create client.cephfs mon 'allow r' mds 'allow rw' osd 'allow rw pool=cephfs_data allow rw pool=nfs-ganesha' -o /etc/ceph/ceph.client.cephfs.keyring
ceph auth get-key client.cephfs | tee /etc/ceph/client.cephfs.key

##  ��ਠ��� ����஢���� CephFS

	mount -t ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs
	mount -t ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=admin,secret=<secret key>
	mount -t ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=admin,secretfile=/etc/ceph/client.cephfs.key
	#
	# ���������� �������
	#
	mount.ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs
	mount.ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=admin,secret=<secret key>
	mount.ceph <SrvMON1>,<SrvMON2>,<SrvMON3>:/ /mnt/mycephfs -o name=admin,secretfile=/etc/ceph/client.cephfs.key

