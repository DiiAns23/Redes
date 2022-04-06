## **DESCARGA E INSTALACION DE LA IMAGEN DE ROUTER**
[Imagen Router](https://drive.google.com/file/d/1Y5b1ZUQxSwvKQ-jLYcqQssTsBsLuPwkO/view)

## **VALOR DE 'X'**

Es importante tener en cuenta que el valor de 'X' debera ser sustituido por: No. de Grupo + Ultimos 2 digitos de su carne

Ejemplo: Grupo no. 4 -> 201903865 = 4 + 6 + 5 = 15

## **ROUTERS - ROUTERS**

- ### **R1 - R2**
```shell
configure terminal
int s1/0
ip address 172.X1.0.1 255.255.0.0
no shutdown
exit
exit
```

- ### **R2 - R1**
```shell
configure terminal
int s1/0
ip address 172.X1.0.2 255.255.0.0
no shutdown
exit
exit
```

- ### **R1 - R3**
```shell
configure terminal
int s1/1
ip address 172.X2.0.1 255.255.0.0
no shutdown
exit
exit
```

- ### **R3 - R1**
```shell
configure terminal
int s1/1
ip address 172.X2.0.2 255.255.0.0
no shutdown
exit
exit
```

- ### **R3 - R2**
```shell
configure terminal
int s1/2
ip address 172.X3.0.1 255.255.0.0
no shutdown
exit
exit
```

- ### **R2 - R3**
```shell
configure terminal
int s1/2
ip address 172.X3.0.2 255.255.0.0
no shutdown
exit
exit
```

## **ROUTERS - SWITCHS**

### **ROUTERS**

- ### **R1**
```shell
configure terminal
int f0/0
ip address 192.168.X3.1 255.255.0.0
no shutdown
exit
exit
```

- ### **R2**
```shell
configure terminal
int f0/0
ip address 192.168.X2.1 255.255.0.0
no shutdown
exit
exit
```

- ### **R3**
```shell
configure terminal
int f0/0
ip address 192.168.X1.1 255.255.0.0
no shutdown
exit
exit
```

### **ENRUTAMIENTO ESTATICO**

- ### **R1 - R2**
```shell
configure terminal
ip route 192.168.X2.0 255.255.255.0 172.X1.0.2
exit
```

- ### **R2 - R1**
```shell
configure terminal
ip route 192.168.X3.0 255.255.255.0 172.X1.0.1
exit
```

- ### **R1 - R3**
```shell
configure terminal
ip route 192.168.X1.0 255.255.255.0 172.X2.0.2
exit
```

- ### **R3 - R1**
```shell
configure terminal
ip route 192.168.X3.0 255.255.255.0 172.X2.0.1
exit
```


- ### **R3 - R2**
```shell
configure terminal
ip route 192.168.X2.0 255.255.255.0 172.X3.0.2
exit
```

- ### **R2 - R3**
```shell
configure terminal
ip route 192.168.X1.0 255.255.255.0 172.X3.0.1
exit
```

## **VPC'S**

- ### **VPC1**
```shell
ip 192.168.X1.10/24 192.168.X1.1
save
```

- ### **VPC2**
```shell
ip 192.168.X1.20/24 192.168.X1.1
save
```

- ### **VPC3**
```shell
ip 192.168.X2.10/24 192.168.X2.1
save
```

- ### **VPC4**
```shell
ip 192.168.X2.20/24 192.168.X2.1
save
```

- ### **VPC5**
```shell
ip 192.168.X3.10/24 192.168.X3.1
save
```

- ### **VPC6**
```shell
ip 192.168.X3.20/24 192.168.X3.1
save
```

## **PRUEBAS PING**

- ### **VPC1 - VPC6**
```shell
ping 192.168.X3.20
```