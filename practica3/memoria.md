# Práctica 3: Balanceo de carga

## El servidor web nginx

### Instalar nginx

Para la instalación de nginx se ha generado una nueva máquina virtual idéntica a las 2 anteriores, se ha instalado nginx y se 
ha deshabilitado apache.

IMPORTANTE: IP

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/nginx_ip.PNG)

Más adelante se le otorgará la misma ip a haproxy sumando 1(es decir 21 en lugar de 20).

### Configuración nginx

Una vez instalado, pasamos a configurar el balanceador, para ello vamos a utilizar la siguiente configuración:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/confnginx.PNG)


### Prueba nginx

Para comprobar que el balanceador funciona vamos a pedir el archivo hola.html de cada una de las máquinas:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/prueba_nginx.PNG)

### Prueba final nginx

Para terminar vamos a ver cómo se comporta el balanceador cambiando el peso de la máquina 1 al doble de trabajo de la máquina 2:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/ab_nginx.png)


##El balanceador haproxy

### Instalación haproxy

Primero creamos una copia de la máquina de nginx y cambiamos las configuraciones requeridas(como ip, host,...). 
Configuramos el archivo del balanceador:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/conf_haproxy1.PNG)

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/conf_haproxy2.PNG)


### Prueba inicial haproxy

Vamos a comprobar que el balanceador funciona correctamente:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/prueba_haproxy.PNG)


### Prueba final haproxy

Por último comprobaremos el funcionamiento de haproxy con apache benchmark, con la misma configuración para su posterior comentario:


![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/pruebafinal_haproxy.png)




## Análisis de resultados

### Resultado de nginx

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/tiempo_nginx.PNG)


### Resultado de haproxy

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica3/tiempo_haproxy.PNG)






