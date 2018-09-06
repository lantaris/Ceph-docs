# Команды управления пулами

**Список пулов**

	ceph osd lspools

**Создание пула хранения. PGs расчитываются по формуле**

	#
	#         (OSDs * 100)
	# <PGs> = ------------
	#          pool size
	#
	# Результат вычислений должен быть округлен до ближайшей степени 2
	#    32,64,127.....
	#
	#  <pool name> - имя пула
	#  <application> - тип (приложение) [cephfs,rbd,rgw]
	#
	ceph osd pool create <pool name> <PG> [<PGP>]
	ceph osd pool application enable <pool name> <application> 

**Создание пользователя для доступа к пулу и выгрузка ключа**

	# <username> - 	имя пользователя
	# <pool name> - пул (возможно указание нескольких пулов:
	#   "profile rbd pool=<pool name1>,profile rbd pool=<pool name2>"
	#
	ceph auth get-or-create client.<username> mon 'profile rbd' osd 'profile rbd pool=<pool name>'
	ceph auth get-or-create client.<username>  | tee /etc/ceph/ceph.client.<username>.keyring
	ceph auth get-key client.<username> | tee /etc/ceph/client.<username>.key
