# Quickinstall �� ࠧ����뢠��� NFS-Ganesha

## ��⠭���� NFS Ganesha, ����� �������� �ᯮ��஢��� CephFS
## ��� ����஢����, ������� �१ libcephfs. � ������� ������� 
## ������ ����� �������� �⪠����⮩稢�� �奬�, ��⥬ ��⠭���� ��� 
## �� �㦭� ���� � ���쭥�訬 ����஢����� NFS ⮬� �१ "localhost"


## ��⠭���� ceph �� �㦭� ����

	yum -y install https://download.ceph.com/rpm-luminous/el7/noarch/ceph-release-1-1.el7.noarch.rpm
	yum -y install ceph

## ��⠭���� nfs-ganesha

	yum -y install nfs-ganesha nfs-ganesha-ceph nfs-ganesha-utils

## �ࠢ�� ���䨣��樮��� 䠩�
## ( ��ࠧ�� ./cfg/ganesha.conf )

## ��⨢��㥬 � ����᪠�� �ࢨ�

	systemctl enable nfs-ganesha.service
	systemctl start nfs-ganesha.service

## ����஢���� � �஢�ઠ ࠡ��ᯮᮡ����

	mkdir -p /mnt/ganesha
	mount.nfs localhost:/ceph /mnt/ganesha
	df -h /mnt/ganesha

## ��� ࠡ��� � oVirt ��⠭�������� �ࠢ�

	chown -R 36.36 /mnt/ganesha

## ��������㥬, �᫨ �ॡ����

	umount /mnt/ganesha
