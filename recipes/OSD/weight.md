# ���������� ������ �������� Ceph

## ���������� ���� ����� � OSD
	ceph osd df
	ceph osd tree
	
## �������������� ��������� "����" OSD 
	# <OSD Num> - ����� OSD
	# <weight> - ����� ���
	ceph osd crush reweight osd.<OSD Num> <weight>

## ��������� ����� OSD � ������� �� ������ � ������� ��������� 
## (� ������ ������ �������� ��������  ���������� ����������� REWEIGHT, � �� WEIGHT)
	# �������� �������������� ��� ���������.
	ceph osd test-reweight-by-utilization    
	
	# �������������� (��������� ���������� ���������� �����������)
	ceph osd reweight-by-utilization	 

## ��������������  � �������������� MGR/balancer
## (������������� ������ � ������������� �����)
	# (������ 7%) ��������� ������, ��� ������� ������������� ����� ������������ ������
	ceph config-key set mgr/balancer/max_misplaced .07   	

	# ��������� ������� MGR/balancer (�� ��������� �������� ������������)
	ceph mgr module enable balancer				

	# ��� ������������ ��������� � CRUSHMAP�
	ceph balancer mode crush-compat				

	# ������ �������� ������������ ������
	ceph balancer on					# ������ �������� ������������ ������

## ���������� MGR/balancer ����� ����� �������
	ceph balancer off
