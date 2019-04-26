# Práctica 3: Balanceo de carga

## El servidor web nginx

### Instalar nginx

Para la instalación de nginx se ha generado una nueva máquina virtual idéntica a las 2 anteriores, se ha instalado nginx y se 
ha deshabilitado apache.

### Configuración nginx

Una vez instalado, pasamos a configurar el balanceador, para ello vamos a utilizar la siguiente configuración:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)

### Prueba nginx

Para comprobar que el balanceador funciona vamos a pedir el archivo hola.html de cada una de las máquinas:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)

### Prueba final nginx

Para terminar vamos a ver cómo se comporta el balanceador cambiando el peso de la máquina 1 al doble de trabajo de la máquina 2:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)


##El balanceador haproxy

### Instalación haproxy

Primero creamos una copia de la máquina de nginx y cambiamos las configuraciones requeridas(como ip, host,...). 
Configuramos el archivo del balanceador:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)


### Prueba inicial haproxy

Vamos a comprobar que el balanceador funciona correctamente:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)


### Prueba final haproxy

Por último comprobaremos el funcionamiento de haproxy con apache benchmark, con la misma configuración para su posterior comentario:


![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)




## Análisis de resultados

### Resultado de nginx

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)


### Resultado de haproxy

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica1/ip%20addr.png)






