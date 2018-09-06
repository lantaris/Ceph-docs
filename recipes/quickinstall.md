#  Quickinstall по развертыванию Ceph кластера


## Установка необходимых библиотек и репозитария Ceph
	yum -y install python-setuptools
	yum -y install https://download.ceph.com/rpm-luminous/el7/noarch/ceph-deploy-2.0.1-0.noarch.rpm 

## Обязательно ! Установка и запуск служб точного времени
	yum -y install chrony && service chronyd restart

## Подготовка каталога для создания конфигурации и ключей, для дальнейшего развертывания и управления кластером
	mkdir -p /opt/ceph-admin
	cd /opt/ceph-admin

## Создание базовой конфигурации
	ceph-deploy new <Server1> <Server2> <Server3>

## Установка пакетов Ceph на хосты, которые будут участниками кластера Ceph
	ceph-deploy install --release luminous <Server1> <Server2> <Server3>

## Установка и запуск монитором MON (обязательно должен быть нечетный кворум. Минимум 3 монитора)
	ceph-deploy mon create-initial

## Копирование администраторского ключа на те ноды, с которых будет производится мониторинг и управление
	ceph-deploy admin <Server1> <Server2> <Server3>

## Развертывание и настройка демона менеджера MGR
	ceph-deploy mgr create <Server1>
	ceph config-key set mgr/dashboard/server_addr ::
	ceph mgr module enable dashboard

## Развертывание демонов хранилищь OSD
	ceph-deploy osd create --data /dev/vdb <Server1>
	ceph-deploy osd create --data /dev/vdb <Server2>
	ceph-deploy osd create --data /dev/vdb <Server3>


## Далее создаем пулы и т.д.
