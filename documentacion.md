### Paso 1: Conectarse al servidor

Para conectarse al servidor usaremos  `ssh`. Si introduces el siguiente comando pasaremos la clave publica que hemos creado al servidor y nos conectaremos a el.

    ssh -i "gotzon.pem" ubuntu@ec2-3-82-194-142.compute-1.amazonaws.com

![](images/ServerConnect.png)

### Paso 2: Instalar Apache
Una vez dentro del servidor instalaremos apache para eso introduce el siguiente codigo en el terminal.

    sudo apt-get update

![](images/Update.png)
Con ese comando actualizaremos todo el servidor una vez hecho eso meteremos el siguiente comando

    sudo apt-get install apache2
![](images/InstallApache.png)

### Paso 3: Instalar MySQL

Ahora que tienes tu servidor web activo y funcional, es el momento de instalar MySQL. MySQL es un sistema de administración de bases de datos. Basicamente, él organizará y proveerá acceso a las bases de datos donde tu sitio podrá guardar información.

Tenemos que meter el siguiente comando para instalar `MySQL` en el servidor.

    sudo apt install mysql-server

![](images/InstallMySQL.png)

Cuando la instalación esté completa, debes ejecutar un archivo de comandos de seguridad que viene preinstalado con MySQL, éste removerá algunos parámetros peligrosos, así como asegurará el acceso a tu base de datos. Ejecuta el archivo interactivo de comandos mediante:

    sudo mysql_secure_installation

Lo primero qu nos va ha preguntar sera si queremos cambiar la contraseña y poner el nivel de contraseña. Ponemos el nivel 2 e introducimos la contraseña que queramos con los requisitos que hemos puesto.

![](images/MySQLPassword.png)

Luego nos preguntara más cosas pon si siquieres insertarlos a MySQL.

![](images/MySQLPreguntas.png)

### Paso 4: Instalar PHP

El siguiente paso es instalar `PHP`.Una vez más usaremos el sistema apt para instalar PHP. Adicionalmente lo podemos configurar para que se ejecute sobre el servidor Apache y para que se comunique con la base de datos MySQL:

    sudo apt install php libapache2-mod-php php-mysql

![](images/InstallPHP.png)

Ahora meteremos el siguiente comando para cambiar el orden del `index.php`.

    sudo nano /etc/apache2/mods-enabled/dir.conf

Nos saldra lo siguiente:

    <IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
    </IfModule>

Ahora pon el index.php el primero.

    <IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>