# �������  ���������� �������� Ceph

## ������/���������/���������� �������� MON

	systemctl [start|stop|restart] ceph-mon.target

## ������/���������/���������� ���� OSD �����

	systemctl [start|stop|restart] ceph-osd.target

## ������/���������/���������� ��������� MGR

	systemctl [start|stop|restart] ceph-mgr.target

## ������/���������/���������� OSD �� ����� <OSD Num> - ����� OSD

	systemctl [start|stop|restart] ceph-osd@<OSD Num>.service