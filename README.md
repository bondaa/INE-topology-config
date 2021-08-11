# INE-topology-config
Проект используется для быстрого разворачивания лабораторной для отрабатывания навыков работы с сетевым оборудованием. 
Схема сети с IP адресацией в файле INE Topology.pdf.

Описание стенда:
Для эмуляции сетевых устройств используется EVE-NG с образами:
•	L2-15.1.bin 
•	L3-15.5.2.bin
Устройства подключены согласно схеме в файле Physical topology.PNG. 
Ansible развернут на отдельной Linux машине в среде VMware и подключен к лабораторной в EVE-NG через встроенный интерфейс pnet1(Cloud1\Network adapter 2; подбробнее про подключение на сайте EVE-NG в файле EVE-NG Community Cookbook). 

Версия Ansible и Python:
mint@mint-virtual-machine:~$  ansible --version
ansible 2.9.6
…
  python version = 3.8.5 (default, Jan 27 2021, 15:41:15) [GCC 9.3.0]
Виртуальная машина имеет адрес в той же сети, что и MGMT итерфейсы устройств, т.е. 160.1.0.0/24

Работа с проектом:
В проекте представлены файлы:
•	INE Topology.pdf – топология разворачиваемого проекта.
•	INE Topology default config.txt – файлы первоначальной настройки устройств для возможности подключения по SSH. 
•	Файлы Ansible:
  o	Файлы конфигурации
    - ansible.cfg
    - hosts.ini
  o	Playbooks
    - playbook_lab_basic_ip.yml – Плейбук для настройки первоначальных параметров устройств.
    - playbook_lab_dmvpn.yml – Плейбук для настройки DMVPN на роутерах R1-5.
  o	Templays
    - basic.j2 – Настройка основных параметров устройств.
    - ip_addr.j2 – Настройка IP адресации устройств.
    - dmvpn_without_ipsec.j2 – Настройка DMVPN для роутеров R1-5 без IPSEC для возможности просмотра обмениваемыми сообщениями через WIRESHARK. 
    - dmvpn_with_ipsec.j2 – Настройка DMVPN для роутеров R1-5 с IPSEC.
  o	Файлы переменных
    - group_vars – общие переменные для устройств.
    - host_vars – переменные для конкретных устройств.
