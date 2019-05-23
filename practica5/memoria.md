# Práctica 5: Replicación de bases de datos MySQL

## Estado de la base de datos

Se ha configurado maria db en las máquinas finales. Adicionalmente se ha generado en una de ellas
la base de datos **SWAP**. Dentro de esta base de datos se ha creado una tabla llamada prácticas,
que contiene un número entero que funciona de llave primaria y un texto descriptivo de 200 caracteres máx.

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/bd_solo_swap1.PNG)

Podemos ver que en la máquina 2 intentamos acceder a la base de datos y nos dice que no existe.

## Copia de una base de datos mediante mysqldump

Para la copia de la base de datos mediante mysqldump generamos un archivo con extensión sql. Transferimos
el archivo a la máquina en la que deseamos replicar la base de datos y utilizamos el mismo comando para
generar la base de datos a partir del arhivo.

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/replicacion_bd_swap2.PNG)


## Configuración maestro-esclavo

Para la configuración maestro-esclavo se va a utilizar la máquina 1 como maestra y la máquina 2
como esclava.
Nota: la ip de la máquina 1 era **192.168.10.10**.

Primero cambiamos los archivos de configuración:
<br/>
*SWAP1*
![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/conf1_ms.PNG)
<br/>
*SWAP2*
![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/conf2_ms.PNG)

Una vez configurado los archivos creamos el usuario que utilizará la máquina 2 para replicar
la base de datos:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/crear_usuario_esclavo.PNG)

Una vez tenemos el usuario creado, pasamos a la máquina 2 y le indicamos los datos de la máquina 1:

**mysql> change master to master_host='192.168.10.10',<br/>
          master_user='esclavo',<br/>
          master_password='esclavo',<br/>
          master_log_file='bin.000001',<br/>
          master_log_pos=980,<br/>
          master_port=3306;** <br/>
Por último ejecutamos "start slave;".
En este momento se producieron dos errores:
  1- Las tablas en la máquina 1 seguían con el bloqueo activado.
  2- Al haber clonado la máquina 2 a partir de la 1 se produjo un error sobre la UUID(arreglado por el apéndice del guión).
  
Una vez hecho lo anterior pasamos a comprobar la configuración del esclavo:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/slave_satus1.PNG)
![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/slave_satus2.PNG)
![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/slave_status3.PNG)
![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/slave_status4.PNG)

Para finalizar vamos a probar que nuestra configuración funciona:

![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/replicacion_final1.PNG)
Las dos máquinas parten de la misma base de datos, por el traspaso de la información por mysqldump.
![imagen](https://github.com/Pmartin97/SWAP/blob/master/practica5/replicacion_final2.PNG)
Insertamos un nuevo valor en la máquina 1 y podemos ver que se ha transferido también a la máquina 2.
