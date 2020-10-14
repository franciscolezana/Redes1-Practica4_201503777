<img src="https://portal.ingenieria.usac.edu.gt/images/2019/logo/logo-fiusac.png"/>



**NOMBRE**: FRANCISCO HUMBERTO LEZANA RAMOS  
**CARNET**: 201503777  
**CURSO**: REDES DE COMPUTADORAS 1

# MANUAL DE CONFIGURACIÓN

## HERRAMIENTAS A UTILIZAR 

- GNS3
- Software de virtualización (VMWare o Virtual Box) instalados y configurado para uso con GNS3.
- Software para captura de datos 

## TOPOLOGIA DE RED DEL PROYECTO 

La siguiente topología cuenta con 4 host de los cuales 3 son VPCS y 1 es una máquina virtual con un sistema tiny-linux para ahorrar recursos, podemos observar que los host se conectan a 2 switches distintos y estos se conectan a 3 EtherSwitch routers y estos a su vez se conectan a un router el cuál será centro principal de comunicación.  
<img src="/xdxd/topologia.PNG" alt="drawing" width="600"/>

## CONFIGURACIÓN DE LA TOPOLOGÍA DE RED EN GNS3

### DIRECCIONES IP DE LOS HOST

Las direcciones de red son las siguientes 192.168.1X.0/24 y 192.168.2X.0/24. Donde X es el último dígito del carné, en este caso el número 7.

Las direcciones ips de los hosts están dados en la siguiente tabla:  

| NO.  | VIRTUALIZADA | IP ASIGNADA    | MASCARA DE RED  | VLAN  |
| ---- | -------- | -------------- | --------------- | ----- |
| 1    | SI     | 192.168.17.10  | 255.255.255.0   | 10 |
| 2    | NO     | 192.168.27.10  | 255.255.255.0   | 20 |
| 3    | NO     | 192.168.17.15  | 255.255.255.0   | 10 |
| 4    | NO     | 192.168.27.15  | 255.255.255.0   | 20 |



### CONFIGURACIÓN DE MODO ACCESO Y MODO TRONCAL

Para la configuración dentro de cada switch, debemos seleccionar 2 puertos en modo trunk(dot1q) y 2 en modo acceso con las vlan 10 y 20 respectivamente como lo vemos en la siguiente imagen:  
<img src="/xdxd/1.PNG" alt="drawing" width="600"/>


### CONFIGURACIÓN DE VTP (servidor y cliente)

Dentro de la consola para el ESW1 escribiremos los siguientes comandos para configurar correctamente la vtp y utilizaremos este ESW1 como servidor  

`conf t`  

`vtp domain redes1_201503777`  

`vtp password  redes1_201503777`  

`vtp mode server`  

`end`  


<img src="/xdxd/Captura.PNG" alt="drawing" width="600"/>


Dentro de la consola para el ESW2 y ESW3 escribiremos los siguientes comandos para configurar correctamente la vtp y utilizaremos estos como clientes  

`conf t`  

`vtp domain redes1_201503777`  

`vtp password  redes1_201503777`  

`vtp mode client`  

`end`  


<img src="/xdxd/Captura2.PNG" alt="drawing" width="600"/>  
<img src="/xdxd/Captura3.PNG" alt="drawing" width="600"/>


### CREACION DE VLAN 10 Y 20 

Dentro de la consola para el ESW1 escribiremos los siguientes comandos para configurar correctamente la  VLAN 10

`conf t`  

`vlan 10`  

`name VENTAS`  

`end`  

`wr`  


<img src="/xdxd/Captura4.PNG" alt="drawing" width="600"/>  

Para mostrar las vlans creadas utilizamos el comando  


`sh vlan-switch`  

<img src="/xdxd/Captura5.PNG" alt="drawing" width="600"/>


Dentro de la misma consola para el ESW1 escribiremos los siguientes comandos para configurar correctamente la  VLAN 20

`conf t`  

`vlan 20`  

`name CONTABILIDAD`  

`end`  

`wr`  


<img src="/xdxd/Captura6.PNG" alt="drawing" width="600"/>  

Para mostrar las vlans creadas utilizamos el comando  


`sh vlan-switch`  

<img src="/xdxd/Captura7.PNG" alt="drawing" width="600"/>



### CONFIGURACION IPS PARA LOS HOST

Se configuran las direcciones ips para los host bajo el formato de la tabla establecida

<img src="/xdxd/Captura9.PNG" alt="drawing" width="600"/>

<img src="/xdxd/Captura10.PNG" alt="drawing" width="600"/>

<img src="/xdxd/Captura11.PNG" alt="drawing" width="600"/>



### ENCAPSULACIÓN EN ROUTER 

Para encapsular las vlans utilizaremos los siguientes comandos en la consola del router:
`conf t`  
`int f0/0.10`
`encapsulation dot1q 10`
`ip address 192.168.17.254 255.255.255.0`
`end`
`wr`
`conf t`  
`int f0/0.20`
`encapsulation dot1q 20`
`ip address 192.168.27.254 255.255.255.0`
`end`
`wr`  

<img src="/xdxd/Captura12.PNG" alt="drawing" width="600"/>


### CONFIGURACION Y CREACIÓN DE PORT-CHANNEL

o Po1: entre ESW1 y ESW2  
Para la configuración del port-channel 1 utilizaremos los siguientes comandos en la consola del ESW1:
`conf t`
`interfaces range f1/0-1`
`channel-group 1 mode on`
`end`

Y los siguientes comandos en la consola del ESW2:
`conf t`
`interfaces range f1/0-1`
`channel-group 1 mode on`
`end`  

<img src="/xdxd/poo.PNG" alt="drawing" width="600"/>

o Po2: entre ESW1 y ESW3  
Para la configuración del port-channel 2 utilizaremos los siguientes comandos en la consola del ESW1:
`conf t`
`interfaces range f1/2-3`
`channel-group 2 mode on`
`end`

Y los siguientes comandos en la consola del ESW3:
`conf t`
`interfaces range f1/2-3`
`channel-group 2 mode on`
`end`
  
  
<img src="/xdxd/poo2.PNG" alt="drawing" width="600"/>

o Po3: entre ESW2 y ESW3  
Para la configuración del port-channel 2 utilizaremos los siguientes comandos en la consola del ESW2:
`conf t`
`interfaces range f1/4-5`
`channel-group 3 mode on`
`end`

Y los siguientes comandos en la consola del ESW3:
`conf t`
`interfaces range f1/4-5`
`channel-group 3 mode on`
`end`  

<img src="/xdxd/poo3.PNG" alt="drawing" width="600"/>







