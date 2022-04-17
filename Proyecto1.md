## **PREPARANDO GNS3**
Dejar descargando las imagenes una noche antes :3

[Ubuntu Server](https://drive.google.com/file/d/1Rqstwstuq-iVICmclHeVu5voB_D74FYL/view)

[Ubuntu Desktop](https://releases.ubuntu.com/18.04/ubuntu-18.04.6-desktop-amd64.iso)


## **SERVER (SW1)**

- ### **CONFIGURACION DE VLAN'S**
```shell
configure terminal
vlan 411
name Diego201903865
exit
vlan 419
name Obin201903865
exit

spanning-tree vlan 411 root primary
spanning-tree vlan 419 root primary

do sh vlan-sw
```
- ### **CONFIGURACION DE PUERTOS**
  
```shell
hostname SERVER
vtp domain GRUPO4
vtp password grupo4
vtp version 2
vtp mode server
exit

sh vtp status
configure terminal
int f1/10
switchport mode access
switchport access vlan 411
exit

int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit

int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit

int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit
exit

copy running-config startup-config
```

## **CLIENT (SW2)**

- ## **CONFIGURACION DE PUERTOS**
```shell
configure terminal
hostname CLIENT
vtp domain GRUPO4
vtp password grupo4
vtp version 2
vtp mode client
exit
sh vtp status
configure terminal
int f1/10
switchport mode access
switchport access vlan 411
exit
int f1/5
switchport mode access
switchport access vlan 419
exit
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit
int f1/4
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit
exit

copy running-config startup-config
```

- ## **CONFIGURACION DE RADIUS**
```shell
configure terminal

username admin_201903865 privilege 15 secret cisco_4

aaa new-model

radius-server host 192.168.0.8 auth-port 1812 acct-port 1813

radius-server key UTCJ

aaa authentication login default group radius local

aaa authorization exec default group radius if-authenticated

enable secret cisco_4

```

## **TRANSPARENT (SW3)**
```shell
configure terminal
hostname TRANSPARENT
vtp domain GRUPO4
vtp password grupo4
vtp version 2
vtp mode transparent
exit

sh vtp status
configure terminal
int f1/10
switchport mode access
switchport access vlan 419
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit

int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit

int f1/4
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
exit
exit

copy running-config startup-config
```

## **PORTCHANNEL**

- ### **ESW1, ESW2**
```shell
configure terminal
interface range f1/0 - 1
channel-group 1 mode on
exit
```

- ### **ESW1, ESW3**
```shell
configure terminal
interface range f1/2 - 3
channel-group 2 mode on
exit
```

- ### **MODE TRUNK**
  - ### **CHANNEL 1**
```shell
int port-channel 1
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
```
  - ### **CHANNEL 2**
```shell
int port-channel 2
switchport mode trunk
switchport trunk allowed vlan 1,411,419,1002-1005
```

## **VPC'S**
- ### **VPC1**
```shell
ip 192.168.0.30/24 192.168.0.1
save
```

- ### **VPC2**
```shell
ip 192.168.0.40/24 192.168.0.1
save
```

- ### **VPC3**
```shell
ip 192.168.0.50/24 192.168.0.1
save
```