# Quickinstall по развертыванию NFS-Ganesha

## Установка NFS Ganesha, который позволяет экспортировать CephFS
## без монтирования, напрямую через libcephfs. С помощью данного 
## демона можно добиться отказоустойчивой схемы, путем установки его 
## на нужные хосты с дальнейшим монтированием NFS тома через "localhost"


## Установка ceph на нужные хосты

	yum -y install https://download.ceph.com/rpm-luminous/el7/noarch/ceph-release-1-1.el7.noarch.rpm
	yum -y install ceph

## Установка nfs-ganesha

	yum -y install nfs-ganesha nfs-ganesha-ceph nfs-ganesha-utils

## Правим конфигурационный файл
## ( образец ./cfg/ganesha.conf )

## Активируем и запускаем сервис

	systemctl enable nfs-ganesha.service
	systemctl start nfs-ganesha.service

## Монтирование и проверка работоспособности

	mkdir -p /mnt/ganesha
	mount.nfs localhost:/ceph /mnt/ganesha
	df -h /mnt/ganesha

## Для работы с oVirt устанавливаем права

	chown -R 36.36 /mnt/ganesha

## Размонтируем, если требуется

	umount /mnt/ganesha
