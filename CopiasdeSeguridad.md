###
**1º. Realiza una copia de seguridad lógica de tu base de datos completa, teniendo en cuenta los siguientes requisitos:
- La copia debe estar encriptada y comprimida.
- Debe realizarse en un conjunto de ficheros con un tamaño máximo de 100 MB.
- Programa la operación para que se repita cada día a una hora determinada.**

Creamos un directorio en el cuál vamos a guardar todas las copias
![Captura](imagenes/captura.png)

Hacemos la copia encriptada y comprimida con un tamaño máximo de 100MB
![Captura2](imagenes/captura2.png)

![Captura3](imagenes/captura3.png)

Para programar la operación, he creado una tarea de cron usando un script con el mismo comando utlizado anteriormente
![Captura4](imagenes/captura4.png)

###
**2º. Restaura la copia de seguridad lógica creada en el punto anterior.**
Para la restauración, vamos a usarla en una máquina limpia 

###
**3º. Realiza un script de sistema operativo que automatice las operaciones necesarias para realizar una copia de seguridad física offline de tu base de datos, copiando todos los ficheros requeridos y borrando los archivos existentes si se habían realizado otras copias de seguridad previamente.**
*El script tenemos que ejecutarlo con superusuario*
~~~
#!/bin/bash
ruta=/home/oracle

if [-e $ruta/copiasseguridad]
then
        rm -rf $ruta/copiasseguridad
        mkdir $ruta/copiasseguridad
        cp -r /opt/oracle/oradata/orcl/* $ruta/copiasseguridad
        cp -r /opt/oracle/product/12.1.0.2/dbhome_1/* $ruta/copiasseguridad
        cp -r /opt/oracle/fast_recovery_area/* $ruta/copiasseguridad
else
         mkdir $ruta/copiasseguridad
        cp -r /opt/oracle/oradata/orcl/* $ruta/copiasseguridad
        cp -r /opt/oracle/product/12.1.0.2/dbhome_1/* $ruta/copiasseguridad
        cp -r /opt/oracle/fast_recovery_area/* $ruta/copiasseguridad
fi
~~~

###
**4º. Programa el script del ejercicio anterior para que se ejecute automáticamente todos los días a una hora determinada.**
He creado una tarea en cron para que es ejecute todos los días
![Captura5](imagenes/captura5.png)

###
**5º. Pon tu base de datos en modo ArchiveLog y realiza con RMAN una copia de seguridad física en caliente. Realiza después la misma operación empleando Enterprise Manager.**
Antes de activar el archivelog, vamos a comprobar que está desactivado
![Captura6](imagenes/captura6.png)

Vamos a crear una carpeta para guardar los logs
![Captura7](imagenes/captura7.png)

Tras ésto cambiamos nuestra base de datos a archivelog
![Captura8](imagenes/captura8.png)

Apagamos la base de datos y la montamos y la cambiamos en archive log
![Captura9](imagenes/captura9.png)

Para hacer la copia de seguridad en caliente usaremos rman aunque no he sido capaz de hacerla, adjunto cómo pienso que es
![Captura10](imagenes/captura10.png)

###
**8º. Documenta el empleo de herramientas de copia de seguridad y restauración en Postgres.**
Para la copia de seguridad de postgres la realizaremos a partir del usuario postgres
![Captura11](imagenes/captura11.png)

Para importar la copia realizada anteriormente
![Captura12](imagenes/captura12.png)

###
**9º. Documenta el empleo de herramientas de copia de seguridad y restauración en MySQL.**
Para realizar la copia ejecutaremos
![Captura13](imagenes/captura13.png)

Para importarla
![Captura14](imagenes/captura14.png)

![Captura15](imagenes/captura15.png)

###
**10º. Documenta el empleo de herramientas de copia de seguridad y restauración en MongoDB.**
Para hacer la copia la haremos así
![Captura16](imagenes/captura16.png)
Usa por defecto el puerto de mongo 27017

Para restaurar la copia usaremos 
![Captura17](imagenes/captura17.png)
