# Practica 2 : Clonar la informacion de un sitio web

En esta práctica vamos a compartir información de datos entre las dos máquinas previamente configuradas.
# 1- Copia de archivos por ssh
Primero vamos a probar a pasar un archivo de una máquina a otra mediante ssh:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/tar_sin_llave.PNG)

# 2- Clonado de una carpeta entre las dos máquinas(rsync)

Antes de usar rsync debemos instalarlo ya que no viene instalado por defecto:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/Instalacion_rsync.PNG)

Para probar su funcionamiento vamos a utilizar una carpeta de html para ver que se sincronice correctamente.
Si queremos que una máquina acceda a la ruta /var/www/html debemos de darle permisos a dicha carpeta:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/cambio_permisos_html.PNG)

Para su uso se han seguido las opciones básicas del guión, ya que no manejamos datos sensibles ni
una cantidad de datos complejos que necesiten una preparación previa:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/rsync_con_contrase%C3%B1a.PNG)

Su uso sin contraseña se podrá observar en el archivo cron.

# 3- Configurar llaves para acceder en ssh sin contraseña

Para configurar el acceso de ssh sin contraseña es necesario crear una llave publica y privada y cederla(la pública) 
a la máquina destino, de este modo al acceder, la máquina origen le mandará un mensaje cifrado con su llave privada
y la máquina destino obtendrá correctamente el mensaje con la correspondiente llave pública:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/ssh-keygen-swap1.PNG)

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/ssh_con_llave_publica.PNG)

En la imagen solo se aprecia que solamente una máquina es capaz de acceder a la otra sin contraseña
pero se añadieron las dos llaves a ambas máquinas para poder realizar las pruebas en ambas máquinas.


# 4- Tarea de cron

Para realizar la tarea de cron se ha utilizado la siguiente configuración del archivo:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/cron.PNG)

En este punto se produjo un problema, no se realizaba ninguna acción. Para su solución se reinició el
servicio de cron para que los cambios del archivo de configuración tuvieran efecto.
El resultado es el siguiente:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica2/prueba%20cron.PNG)

Se puede apreciar que solo después del tiempo impuesto en el archivo de configuración es cuando se genera el mensaje
y se sincroniza el archivo el cual no se encontraba en la máquina.
