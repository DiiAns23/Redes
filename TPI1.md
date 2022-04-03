# ***TAREA PREPARATORIA 1***

## HOSTNAME

- ### NUCLEO

```shell
enable
configure terminal
hostname NUCLEO
exit
```

 - ### DST

```shell
enable
configure terminal
hostname DST
exit
```

- ### SW1

```shell
enable
configure terminal
hostname SW1
exit
```

- ### SW2

```shell
enable
configure terminal
hostname SW2
exit
```

- ### SW3

```shell
enable
configure terminal
hostname SW2
exit
```

## MODO DUPLEX

Aqui se debe de tener cuidado con cada puerto.

- ### NUCLEO

```shell
sh ip interface brief
configure terminal
interface ethernet 0/0
duplex full
no shutdown
exit
exit
```

 - ### DST

```shell
sh interface status
configure terminal
interface range ethernet 0/0 - 3
duplex full
exit
exit
```

- ### SW1, SW2, SW3

```shell
sh interface status
configure terminal
interface range ethernet 0/0 - 3
duplex full
exit
exit
```

## CREACION DE VTP

 - ### DST

```shell
configure terminal
vtp domain REDES1
vtp password REDES1
vtp version 2
vtp mode server
exit
```

- ### SW1, SW2, SW3

```shell
configure terminal
vtp domain REDES1
vtp password REDES1
vtp version 2
vtp mode client
exit
```

## CONFIGURACION DE PUERTOS

 - ### DST

```shell
configure terminal
interface range ethernet 0/0 - 3
switchport trunk encapsulation dot1q
switchport mode trunk
exit
exit
```

- ### SW1

```shell
configure terminal
interface ethernet 0/1
switchport trunk encapsulation dot1q
switchport mode trunk
exit

interface ethernet 0/0
switchport mode access
switchport access vlan 10
shutdown
no shutdown 
exit

interface ethernet 0/2
switchport mode access
switchport access vlan 20
shutdown
no shutdown 
exit

exit
sh interface status
```

- ### SW2

```shell
configure terminal
interface ethernet 0/2
switchport trunk encapsulation dot1q
switchport mode trunk
exit

interface ethernet 0/0
switchport mode access
switchport access vlan 10
shutdown
no shutdown 
exit

interface ethernet 0/1
switchport mode access
switchport access vlan 20
shutdown
no shutdown 
exit

exit
sh interface status
```

- ### SW3

```shell
configure terminal
interface ethernet 0/3
switchport trunk encapsulation dot1q
switchport mode trunk
exit

interface ethernet 0/1
switchport mode access
switchport access vlan 10
shutdown
no shutdown 
exit

interface ethernet 0/2
switchport mode access
switchport access vlan 30
shutdown
no shutdown 
exit

exit
sh interface status
```

## CREACION DE VLAN'S

 - ### DST

```shell
configure terminal

vlan 10 
name ESTUDIANTES
exit

vlan 20
name DOCENTES
exit

vlan 30 
name AUXILIARES 
exit

exit
```

## CREACION DE SUB INTERFACES
- ### NUCLEO
```shell
configure terminal

interface ethernet 0/0.10
encapsulation dot1q 10
ip address 192.168.10.254 255.255.255.0
exit

interface ethernet 0/0.20
encapsulation dot1q 20
ip address 192.168.20.254 255.255.255.0
exit

interface ethernet 0/0.30
encapsulation dot1q 30
ip address 192.168.30.254 255.255.255.0
exit

exit

sh ip interface brief 
```

## SETEO DE IP'S

- ### VLAN10-VPC1

```shell
ip 192.168.10.10/24 192.168.10.254
```

- ### VLAN20-VPC1

```shell
ip 192.168.20.10/24 192.168.20.254
```

- ### VLAN10-VPC2

```shell
ip 192.168.10.20/24 192.168.10.254
```

- ### VLAN20-VPC2

```shell
ip 192.168.20.20/24 192.168.20.254
```

- ### VLAN10-VPC3

```shell
ip 192.168.10.30/24 192.168.10.254
```

- ### VLAN30-VPC1

```shell
ip 192.168.30.10/24 192.168.20.254
```

## PRUEBA DE FUNCIONAMIENTO

- ### VLAN10-VPC1 a VLAN10-VPC2

```shell
ping 192.168.10.20
```