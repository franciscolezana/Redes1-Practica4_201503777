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

## CONFIGURACIÓN DE LA TOPOLOGÍA DE RED EN GNS3

### DIRECCIONES IP DE LOS HOST

Para esta práctica se van a utilizar las siguientes direcciones IP, la X y Y representan el último y penúltimo número del carnét del estudiante. El carnet del usuario es 201503777 , se utilizarán X:7 y Y:8 para evitar errores al momento de conectar los host.  
