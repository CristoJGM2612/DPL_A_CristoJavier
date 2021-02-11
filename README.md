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
    CAPTURA

2. PUERTOS DE ESCUCHA.

    Configura tu servidor para que cada sitio funcione en un puerto distinto.
    
    cat /var/apache2/sites-avaliable/sitio1.conf
    cat /var/apache2/sites-avaliable/sitio2.conf
    
    - Traté de congigurarlo, pero no reconocía la configuración y adquiría la conf del otro dominio, así que opté por no configurarlo
    
3. DIRECTIVA DIRECTORY.

    Haz los cambios necesarios para tener un domino www.sitio2.com cuya carpeta de publicación con ficheros sea /www/sitio2. Crea en esta carpeta un archivo html con el mensaje BIENVENIDO AL SITIO 2, de forma que al entrar nos muestre la mencionada página.
    
    cat /var/www/sitio2/index.html
    CAPTURA 

4. DIRECTIVA ALIAS.

    Utiliza un nuevo alias para publicar ficheros que se encuentren dentro de /www/publico. Crea en esta carpeta un archivo html con el mensaje BIENVENIDO AL SITIO PÚBLICO, de forma que al entrar nos muestre la mencionada página.
    - Debemos de editar el archivo que se encuentra en /etc/apache2/sites-avaliable/sitio1.conf, como se muestra en la imagen
   CAPTURA

5. OPTION INDEXES.

    Crea una carpeta llamada compartida con varios ficheros llamados compartida1.txt, compartida2.txt y compartida3.txt. Haz que se muestre el listado de los mismos al entrar en la url www.sitio2.com/compartida.
    -Al igual que en en anterior apartado, debemos de configuar el archivo que se encuentra en /etc/apache2/sites-avaliable/sitio2.conf, como se muestra en la imagen
    CAPTURA

6. REDIRECT.

    Prueba y explica la diferencia entre el Alias y el Redirect. Utiliza las dos directivas para hacer que cuando entramos en http://www.sitio1.com/mas_info se acceda a los ficheros de la carpeta mas_informacion. Para ello tendrás que hacer primero algo parecido a Alias /mas_info /www/sitio1/mas_informacion y luego prueba a poner un Redirect /mas_info http://www.sitio1.com/mas_informacion.
    
    - Traté de realizar la dirección, pero no entiendo que es lo que pide exactamente

7. ERRORES PERSONALIZADOS.

    Configura el servidor para que cuando se solicite una página que no existe nos devuelva la página de error 404.html que se adjunta.
    - Por alguna razón no muestra la página, aunque si muestra un mensaje de que recibe la petición de mostrarla
    CAPTURA

8. AUTENTICACION BASIC.

Configura el servidor creando dos grupos de usuarios suiguientes:

    grupo1: formado por usuario1 y usuario2
    grupo2: formado por usuario3 y usuario4

El grupo2 debe poder acceder a todo el site, mientras que el grupo1 tienen el acceso restringido a la carpeta /sitio_grupo2/. Coloca un archivo html en esta carpeta.

    - Debemos de configurar cada usuario con httpasswd (-c solo la primera vez, para crear el documento txt con las contraseñas) nombrearchivo.txt nombreusuario
    - También debemos de crear los grupos pertinentes, con un simple nano bastará
    - Los archivos resultantes: 
    CAPTURA
    - Para finalizar debemos de activar el modulo: authz_groupfile y añadir las restricciones en el archivo de configuración pertinente
    -CAPTURA
9. AUTENTICACION DIGEST.

Crea dos subdirectorios en el host virtual sitio1 que se llamen users1 y users2. Crea varios usuarios con la utilidad htdigest, asignando a cada uno un dominio distinto (domusers1 y domusers2). Configura los directorios para que al primero (users1) sólo puedan acceder los usuarios del dominio domusers1, y el directorio users2 solo accedan los usuarios del dominio domusers2.
    CAPTURA

10.HTTPS.

Configura el protocolo de conexión HTTPSen el servidor así como la redirección de todas las conexiones desde HTTP a HTTPS.

    - Primero activamos el flujo de datos, con ufw enable
    - Luego instalamos cerbot y elegimos en que "dominios" queremos aplicar el certificado
    - Esperamos y listo
    
