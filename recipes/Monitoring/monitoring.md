# ������� ����������� �������� Ceph

## ���������� ��������
	ceph -s				# ����� ������ �������� Ceph
	ceph status			# ����� ������ �������� Ceph
	ceph -w				# ���������� �������� � �������� �������
	ceph health detail		# ��������� ������ ��������

## ������ ��������
ceph auth list			

## ���������� OSD � ���������
ceph osd tree			# ��������� ��������
ceph osd df  			# ������� ��������� OSD (����, ���������, PGS)
ceph osd dump			# ��������� ���������� � OSD
ceph tell osd.<OSD Num> bench	# �������� �������� ������������� OSD

## ����
ceph osd pool get <pool> all	# ��������� ����
ceph pg dump pgs		# ���� ���� PGs
ceph pg dump			# ���������� ��� ����� ���� ����������
rbd du <pool>/<volume>		# ���������� ������/���������� ������ ���� � RBD ����
rbd ls -l <pool>		# ���������� ����
ceph osd lspools		# ������ �����
rados df 			# ������� ���������� � �������� � ��������� ����� � �����

## CephFS (MDS)
ceph mds stat
ceph mds dump
