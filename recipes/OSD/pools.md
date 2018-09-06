# ������� ���������� ������

## ������ �����
	ceph osd lspools

## �������� ���� ��������. PGs ������������� �� ������� :
	#
	#         (OSDs * 100)
	# <PGs> = ------------
	#          pool size
	#
	# ��������� ���������� ������ ���� �������� �� ��������� ������� 2
	#
	#  <pool name> - ��� ����
	#  <application> - ��� (����������) [cephfs,rbd,rgw]
	#
	ceph osd pool create <pool name> <PG> [<PGP>]
	ceph osd pool application enable <pool name> <application> 

## �������� ������������ ��� ������� � ���� � �������� �����
	# <username> - 	��� ������������
	# <pool name> - ��� (�������� �������� ���������� �����:
	#   "profile rbd pool=<pool name1>,profile rbd pool=<pool name2>"
	#
	ceph auth get-or-create client.<username> mon 'profile rbd' osd 'profile rbd pool=<pool name>'
	ceph auth get-or-create client.<username>  | tee /etc/ceph/ceph.client.<username>.keyring
	ceph auth get-key client.<username> | tee /etc/ceph/client.<username>.key
