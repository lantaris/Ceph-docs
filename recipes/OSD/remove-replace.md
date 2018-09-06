#  �������� ��� ������ �������� OSD

##  �������� �������� OSD
	#
	# ���� OSD ��� ���� ��� - �� ���, ����� ��������� Ceph ������������ � ���� ������
	# 
	#  <OSD Num>  - ����� OSD (����� OSD ����� ���������� ��������� "ceph osd tree", "ceph osd df", "ceph osd status"
	# 
	# �� ������ ���������� � OUT OSD ����� ������� � ���������� (IN) ��������� �������� "ceph osd in <OSD Num>"
	#  
	ceph osd out osd.<OSD Num>  


### ����� ��������� ������, ���� ��� �����������, ��������� ��� ������ �������������� "ceph osd safe-to-destroy <OSD Num>".
### ������������� �� ������ ����� ������� OSD.
### ��������� "ceph osd status", ��� ���������� ������ ��� OSD
	systemctl stop ceph-osd@<OSD Num>.service

### ������� OSD �� ��������
	ceph osd purge osd.<OSD Num>


### ������� ������� OSD
	# ���� ����� OSD � ��������� ��������� ������ ������� ����� ������������ ��������� �������:
	#
	#  readlink -f /var/lib/ceph/osd/ceph-<OSD Num>/* 	# ���������� ������ 
	#  lsblk -f 						# ������ �������� ���������
	#  dmsetup ls						# ������������ �������� ��� LVM �� /dev/dm<�����>
	#  lvs							# �� ����� -o- ����� ������ ������������ � ������ ������ ��� ��� ���.
	#
	umount /var/lib/ceph/osd/ceph-<OSD Num>
	rmdir /var/lib/ceph/osd/ceph-<OSD Num>

### ��������� ������� ����. ����� ���� �������� �������
	echo 1 > /sys/block/<data-disk>/device/delete

##  ���������� ������ OSD


### ����� ���������� ������ �����. ������� ����� ������ ���������� 
### ����� ������������ ��� OSD. �� ����������� ������� ������� ����
	lsblk -f

###  ������ ��� ��� ��� ���� ��� 0.
	wipefs -af /dev/<����������>

### ��������� ����� OSD c ������� ceph-deploy � admin �����
	ceph-deploy osd create --data /dev/<����������> <����>

### ���������� ��������� �������� ��������� ������ � �������� HEALTH_OK
### ��������� ��������� ��� ��� �������������� � ��� ��� � ������� ���������:
	ceph status
	ceph osd status
	ceph osd tree
	ceph osd df
