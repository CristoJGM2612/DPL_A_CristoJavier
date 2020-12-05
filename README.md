- Inicia sesión con un usuario con privilegios de administrador en servidor_nombre.
- Abre un terminal y accede al directorio /etc/apache2.
- Haz un listado del directorio y observa los ficheros de configuración.
![Captura1](\Captura1.PNG)

- Abre el fichero /etc/apache2/apache2.conf y analiza su configuración. Observa que incluye con la directiva include a otros ficheros y directorios.
![Captura2](\Captura2.PNG)

>*Servidor virtual por defecto.*

- Accede al directorio /etc/apache2/sites-available y comprueba que está creado archivo 000-default.conf que contiene la configuración del servidor virtual por defecto. 
![Captura3](\Captura3.PNG)
![Captura4](\Captura4.PNG)