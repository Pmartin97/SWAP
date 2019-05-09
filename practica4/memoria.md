# Practica 4 Asegurar la granja web

## 1- Instalar un certificado SSL autofirmado para configurar el acceso por HTTPS

Primero vamos a instalar el certificado:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/certificado_autofirmado.PNG)

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/instalacion_crt.PNG)

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/conf_crt.PNG)

Por último cambiamos la configuración de los certificados a utilizar en el sistema:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/conf_default-sites.PNG)

Con el certificado instalado vamos a realizar una prueba:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/prueba_https.PNG)

Para que funcione en nuestra granja debemos configurar nginx para que redireccione el tráfico correctamente:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/crt_nginx.PNG)

Ahora que tenemos configurado el certificado en la máquina 1 y en el balanceador, podemos copiar el crt en la máquina 2 y probar su funcionamiento desde el cliente:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/prueba_final_crt.PNG)
### Nota: debemos recordar que el balanceador tiene la ip 192.168.10.20 y las máquinas terminan en 10 y 11

## 2- Configuración del cortafuegos

Para la configuracion del cortafuegos se han utilizado 3 scripts. El primero reinicia la ip table por defecto, el segundo deniega todo el tráfico y el tercero utiliza la configuración pedida, solo acepta tráfico del balanceador.

Una prueba de denegación de todo el tráfico es la siguiente:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/conf_denegar_iptables.PNG)
### Nota: se puede ver que se recibió un curl de la máquina 2, en este ejemplo no se configuró dicha máquina, así que solo debería denegar servicio la ip 192.168.10.10 que pertenece a la máquina 1. De hecho es la continuación de la imagen anterior.

Después de comprobar que lo anterior funciona, pasamos a configurar el cortafuegos para que solo acepte tráfico de nginx:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/conf_final_tablas.PNG)
### Nota: se repiten las líneas de puerto 80 de forma idéntica para el puerto 443. También se aceptan peticiones en local por si en el futuro es necesario realizar una comprobación, evitar malgastar tiempo buscando el error.

Una vez configurado todo vamos a comprobar que realmente funciona. Primero, como solo se ha configurado la máquina 1 y nginx, entonces el cliente debe ser capaz de realizar peticiones https a máquina 2 pero no a máquina 1.

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/prueba_final_tablas_cliente.PNG)

Como podemos comprobar en la imagen ocurre lo que se esperaba.

Ahora hay que comprobar que nginx puede acceder a máquina 1:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica4/prueba_final_tablas_nginx.PNG)

Como podemos ver en la imagen, nginx es capaz de obtener tráfico de la máquina 1 por el puerto 80(http) y el 433(https)
Como paso final podemos incluir la dirección del script de la configuración del cortafuegos en el archivo /etc/rc.local

De hecho las imágenes obtenidas se realizaron después de un reinicio de todas las máquinas para asegurar que los servicios se reiniciaban correctamente y que el cortafuegos funcionaba.


