#  Quickinstall �� ������������� Ceph ��������


## ��������� ����������� ��������� � ����������� Ceph
	yum -y install python-setuptools
	yum -y install https://download.ceph.com/rpm-luminous/el7/noarch/ceph-deploy-2.0.1-0.noarch.rpm 

## ����������� ! ��������� � ������ ����� ������� �������
	yum -y install chrony && service chronyd restart

## ���������� �������� ��� �������� ������������ � ������, ��� ����������� ������������� � ���������� ���������
	mkdir -p /opt/ceph-admin
	cd /opt/ceph-admin

## �������� ������� ������������
	ceph-deploy new <Server1> <Server2> <Server3>

## ��������� ������� Ceph �� �����, ������� ����� ����������� �������� Ceph
	ceph-deploy install --release luminous <Server1> <Server2> <Server3>

## ��������� � ������ ��������� MON (����������� ������ ���� �������� ������. ������� 3 ��������)
	ceph-deploy mon create-initial

## ����������� ������������������ ����� �� �� ����, � ������� ����� ������������ ���������� � ����������
	ceph-deploy admin <Server1> <Server2> <Server3>

## ������������� � ��������� ������ ��������� MGR
	ceph-deploy mgr create <Server1>
	ceph config-key set mgr/dashboard/server_addr ::
	ceph mgr module enable dashboard

## ������������� ������� ��������� OSD
	ceph-deploy osd create --data /dev/vdb <Server1>
	ceph-deploy osd create --data /dev/vdb <Server2>
	ceph-deploy osd create --data /dev/vdb <Server3>


## ����� ������� ���� � �.�.
