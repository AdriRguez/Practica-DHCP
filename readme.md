# Practica DHCP

## Docker-Compose
Primero crearemos las estructura y añadiremos el contenedor al docker compose con la imagen del DHCP.
~~~
version: '3.3'
services:
    dhcp:
        container_name: servidorasir2a_dhcp
        hostname: servidor_dhcp
        network_mode: host
        image: networkboot/dhcpd
        volumes:
          - /home/asir2a/Escritorio/Docker/Practica_DHCP/data:/data
~~~

Despues añadiremos el archivo dhcpd.conf
## dhcpd.conf
Configuramos el DHCP con una configuracion predeterminada sacada de internet y le asignamos el rango que le vamos a dar.
~~~
subnet 10.0.9.0 netmask 255.255.255.0 {    
    

    option domain-name "PracticaAsirDHCP.com";
    option routers 10.0.9.254;
    option subnet-mask 255.255.255.0; 
    option broadcast-address 10.0.9.255;
    option domain-name-servers 8.8.8.8, 8.8.4.4;    
    default-lease-time 86400;
  
    default-lease-time 86400;
    max-lease-time 172800;

  group {

     default-lease-time 604800;
     max-lease-time 691200;

     host apache {
         hardware ethernet 08:00:27:CE:A1:1A;
         fixed-address 10.0.9.197;
     }

  }
}
~~~

Despues para asignar la ip fija, abrimos la maquina virtual ponemos el adaptador en modo bridge y vemos la MAC, la añadimos al dhcpd.conf y le pedimos una ip al DHCP.

![Imagen IP DHCP](../Imagenes/dhcpIP.png)