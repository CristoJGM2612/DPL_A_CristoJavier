- Inicia sesión con un usuario con privilegios de administrador en servidor_nombre.
- Abre un terminal y accede al directorio /etc/apache2.
- Haz un listado del directorio y observa los ficheros de configuración.
![Captura1](\Captura1.PNG)

- Abre el fichero /etc/apache2/apache2.conf y analiza su configuración. Observa que incluye con la directiva include a otros ficheros y directorios.
![Captura2](\Captura2.PNG)

>*Servidor virtual por defecto.*

- Accede al directorio /etc/apache2/sites-available y comprueba que está creado archivo 000-default.conf que contiene la configuración del servidor virtual por defecto. 
![Captura3](\Captura3.PNG)
- Accede a /etc/apache2/sites-enabled y comprueba que existe el fichero 000-default.conf que es un enlace simbólico a000-default.conf pero de /etc/apache2/sites-available.
![Captura4](\Captura4.PNG)

- Cosulta el fichero /etc/apache2/apache2.conf y comprueba cuál es el valor de las siguientes directivas, explicando que función tiene cada una de ellas.

- - ServerRoot 

- - Timeout   
    El numero de segundos antes de desconectarte
- - KeepAlive
    Esta directiva se utiliza para indicar si se activarán las conexiones persistentes; es decir. el poder hacer más de una petición por conexión.
- - MaxKeepAliveRequests
    Esta directiva establece el máximo número de peticiones que se pueden realizar en una conexión persistente.
- - KeepAliveTimeout
    La directiva KeepAliveTimeout establece el número de segundos que el servidor esperará tras haber dado servicio a una petición, antes de cerrar la conexión.
- - User y Group
    User establece el nombre de usuario para el proceso del servidor y determina qué archivos puede acceder el servidor
- - ErrorLog
    Especifica el archivo donde se guardan los errores del servido.
![Captura5](\Captura5.PNG)
![Captura6](\Captura6.PNG)
- ¿Se permiten conexiones persistentes? ¿Qué directiva define este comportamiento?
    Si está activada la opción KeepAlive, puesto que esta opción es la que regula si se permite más de una petición por conexión  (Conexiones Persistentes)
- ¿Cuál es el fichero de errores?. ¿Qué directiva lo define?.
    La directiva que define el fichero de errores es ErrorDocument, y por defecto no tiene ningún fichero relacionado como se puede observar en la captura anterior
    
- Consulta el fichero /etc/apache2/ports.conf, y comprueba cuál es el puerto en el que escucha las peticiones Apache. ¿En qué puerto escuchará también si se habilita el módulo modssl?.
El puerto por defecto es el 80, y si se habilita el módulo modssl sería el puerto 443
![Captura7](\Captura7.PNG)
- Consulta el fichero /etc/apache2/sites-avalaible/000-default.conf observa y comenta la función de cada uno de los siguientes puntos:
- - Dentro de la directiva <VirtualHost>... </VirtualHost> se define el comportamiento del servidor virtual por defecto.
- - El valor de la directiva DocumentRoot es /var/www/html.
    El valor de la directiva DocumentRoot es /var/www/html.
- - El valor de la directiva ErrorLog.
    ${APACHE_LOG_DIR}/error.log
    ![Captura8](\Captura8.PNG)

- Consulta el fichero /etc/apache2/apache2.conf observa y comenta la función de cada uno de los siguientes puntos:

- - La directiva contenedora <Directory> .... </Directory> que se utiliza para determinar cómo Apache sirve el contenido del directorio/var/www.
- - Realiza una captura de ese fichero y señala en él la directiva que se sigue. 
---
#CONFIGURACIÓN BÁSICA DE APACHE 
- Para ello vamos a crear dos archivos de configuración fp.conf que hará referencia a la web alojada en la ruta /var/www/fp/.
Copiamos la configuracion predeterminad en /etc/apache/sites-avaliable a (000-default.conf)
![Captura11](\Captura11.PNG)
![Captura12](\Captura12.PNG)
- Hacemos lo mismo en la localización /etc/apache/sites-enabled, y reiniciamos el servicio de apache
![Captura11](\Captura13.PNG)
![Captura14](\Captura14.PNG)
Cambiamos la direccion de nuestro DocumentRoot a /var/www/fp
![Captura15](\Captura15.PNG)
Configuramos nuestro nuevo dominio en FreeNom

- Ficheros a servir por defecto (Directory Index).
    Desde cliente_nombre abre un navegador y establece una conexión a http://10.70.XX.11
    ![Captura16](\Captura16.PNG)
- No se ha solicitado ningún recurso en concreto por lo que el servidor ha enviado el index.html (valor en la directiva DirectoryIndex por defecto).

- Renombra el fichero /var/www/fp/index.html a /var/www/fp/indice.html
![Captura17](\Captura17.PNG)
- Desde cliente_nombre abre un navegador y establece una conexión a http://10.70.XX.11. ¿Qué ocurre ahora? ¿Ha cambiado lo que envía el servidor?.
- Edita el fichero /etc/apache2/apache2.conf y añade la siguiente directiva: DirectoryIndex listado.html en la la sección<Directory /var/www>. Explica que conseguimos al hacer esta modificación
![Captura18](\Captura18.PNG)
- Desde cliente_nombre abre un navegador y establece una conexión al servidor de nuevo. ¿Ha cambiado el fichero de carga?.
![Captura19](\Captura19.PNG)
- Páginas de error personalizadas.

- - Configura el servidor para que cuando retorne el código de error 404 (página no encontrada) envíe el texto Página no encontrada en el servidor.
    ![Captura20](\Captura20.PNG)
- Reinicia el servidor. Desde el cliente_nombre establece una conexión a http://www.fpdaw.org/noexiste.html y muestra qué te aparece en la pantalla.
    ![Captura21](\Captura21.PNG)

- *Redirecciones.*
- Configura el servidor para que al entrar a http://www.fpdaw.org/ciclos haga una redirección automática hacia http://www.fpdaw.org/dam mostrando la página web correspondiente a DAM.
    ![Captura22](\Captura22.PNG)
- *Alias*
- Crea un aliasde forma que forma que al entrar en http://www.fpdaw.org/logosmuestre el contenido de los logotipos alojados en la ruta/home/usuarios/Documentos
    ![Captura21](\Captura23.PNG)
    
- *Autenticación*
- Configura el servidor creando dos grupos de usuarios suiguientes: + 
- - alumnos :formado por alumno1 y alumno2 
- - profesores. formado por profesor1 y profesor2
    ![Captura24](\Captura24.PNG)
    ![Captura25](\Captura25.PNG)
    ![Captura26](\Captura26.PNG)
    ![Captura27](\Captura27.PNG)
    ![Captura28](\Captura28.PNG)

- *Configuración de HTTPS*

- Configura el uso de HTTPS en el servidor web. Explica detalladamente todo el proceso aportando capturas de pantalla.
- Redirecciona todo el tráfico HTTP hacia HTTPS, de forma que al conectar con http://www.fpdaw.org nos redireccione haciahttps://www.fpdaw.org.
    ![Captura24](\Captura29.PNG)
    
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
    
    
    Proyecto - Recuperación TRIM1 Revisión y configuración básica de un servidor Apache en Linux

Partiremos de la configuración de red que sigue. Si no la tienes así, realiza los cambios pertinentes para que se cumpla, o indica en tu informe de prácticas la configuración de red con la que realizaste la práctica. Aconsejo la primera opción.

    Máquina cliente_nombre (ejemplo: cliente_antonio) : Red interna con ip 10.70.XX.10
    Máquina servidor_Nombre (ejemplo: servidor_antonio): Red interna con ip10.70.XX.11 - Red puente con DHCP

Debes ir creando la estructura de carpetas y los archivos que se pidan en cada uno de los apartados.

Debes subir a tu repositorio de GitHub un documento escrito en sintaxis MarkDown en el que expliques detalladamente los pasos que se dan para resolver cada uno de los apartados, aportando capturas de pantalla. En estas capturas de pantalla debe verse claramente en la línea de comandos el nombre de usuario de la máquina para certificar su autenticidad.

1. CREACIÓN DE UN SITIO VIRTUAL.

    Crea dos sitios virtuales: www.sitio1.com y www.sitio2.com. 
    cd var/www
    
    tree
    captura

2. PUERTOS DE ESCUCHA.

    Configura tu servidor para que cada sitio funcione en un puerto distinto.
    
    cat /var/apache2/sites-avaliable/sitio1.conf
    cat /var/apache2/sites-avaliable/sitio2.conf

3. DIRECTIVA DIRECTORY.

    Haz los cambios necesarios para tener un domino www.sitio2.com cuya carpeta de publicación con ficheros sea /www/sitio2. Crea en esta carpeta un archivo html con el mensaje BIENVENIDO AL SITIO 2, de forma que al entrar nos muestre la mencionada página.
    
    cat /var/www/sitio2/index.html

4. DIRECTIVA ALIAS.

    Utiliza un nuevo alias para publicar ficheros que se encuentren dentro de /www/publico. Crea en esta carpeta un archivo html con el mensaje BIENVENIDO AL SITIO PÚBLICO, de forma que al entrar nos muestre la mencionada página.
   

5. OPTION INDEXES.

    Crea una carpeta llamada compartida con varios ficheros llamados compartida1.txt, compartida2.txt y compartida3.txt. Haz que se muestre el listado de los mismos al entrar en la url www.sitio2.com/compartida.

6. REDIRECT.

    Prueba y explica la diferencia entre el Alias y el Redirect. Utiliza las dos directivas para hacer que cuando entramos en http://www.sitio1.com/mas_info se acceda a los ficheros de la carpeta mas_informacion. Para ello tendrás que hacer primero algo parecido a Alias /mas_info /www/sitio1/mas_informacion y luego prueba a poner un Redirect /mas_info http://www.sitio1.com/mas_informacion.

7. ERRORES PERSONALIZADOS.

    Configura el servidor para que cuando se solicite una página que no existe nos devuelva la página de error 404.html que se adjunta.

8. AUTENTICACION BASIC.

Configura el servidor creando dos grupos de usuarios suiguientes:

    grupo1: formado por usuario1 y usuario2
    grupo2: formado por usuario3 y usuario4

El grupo2 debe poder acceder a todo el site, mientras que el grupo1 tienen el acceso restringido a la carpeta /sitio_grupo2/. Coloca un archivo html en esta carpeta.

9. AUTENTICACION DIGEST.

Crea dos subdirectorios en el host virtual sitio1 que se llamen users1 y users2. Crea varios usuarios con la utilidad htdigest, asignando a cada uno un dominio distinto (domusers1 y domusers2). Configura los directorios para que al primero (users1) sólo puedan acceder los usuarios del dominio domusers1, y el directorio users2 solo accedan los usuarios del dominio domusers2.

10.HTTPS.

Configura el protocolo de conexión HTTPSen el servidor así como la redirección de todas las conexiones desde HTTP a HTTPS.
