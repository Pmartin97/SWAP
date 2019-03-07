# Práctica 1 : Preparación de las herramientas

En esta práctica vamos a preparar dos máquinas virtuales para que proporcionen servicios ssh, html, etc.
Para comprobar su funcionamiento vamos a utilizar ssh y curl.

## Preparación de las máquinas

Primero debemos realizar la instalación de las dos máquinas virtuales, en nuestro caso VirtualBox.
En la propia instalación tenemos la posiubilidad de instalar todos los paquetes necesarios para la práctica,
si no lo hacemos en la instalación, podemos usar el comando "**tasksel**" para realizar una instalación más automática.

Cuando tenemos las dos máquinas virtuales preparadas debemos añadir un adaptador a VirtualBox y a las dos máquinas
para que puedan comunicarse entre ellas. Finalmente configuramos los adaptadores accediendo al archivo */etc/network/interfaces*.

## Prueba de funcionamiento

Una vez está todo bien configurado(podemos comprobarlo con **systemctl status *servicio***) procedemos a utilizar
ssh y curl.
Las dos máquinas virtuales están configuradas de la siguiente forma:

|        swap1 | swap2        |
|:------------ | ------------:|
|192.168.10.10 | 192.168.10.11|

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)

Priemro realizamos ssh desde swap1 a swap2:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ssh.png)

Por último realizamos la prueba de curl desde swap2 a swap1:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/curl.png)
