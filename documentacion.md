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


### Paso 5: IP Elastica

Para asignar una dirección IP elástica desde un grupo de direcciones IPv4 públicas de Amazon utilizando la consola:

* Abra la consola de Amazon EC2 en https:// console.aws.amazon.com/ec2/.

* En el panel de navegación, elija Elastic IPs (Direcciones IP elásticas).

    

* Elija Allocate new address (Asignar nueva dirección).

    ![](images/NewElasticIp.png)

* En IPv4 address pool (Grupo de direcciones IPv4), elija Amazon pool (Grupo de Amazon).

    ![](images/AmazonPoolGroup.png)

* Elija Allocate (Asignar) y cierre la pantalla de confirmación.

    ![](images/AssociateElasticIp.png)

### Paso 6: Gestión de DNS

* A = Dirección (address). Este registro se usa para traducir nombres de servidores de alojamiento a direcciones IPv4.

* AAAA = Dirección (address). Este registro se usa en IPv6 para traducir nombres de hosts a direcciones IPv6.

* CNAME = Nombre canónico (canonical Name). Se usa para crear nombres de servidores de alojamiento adicionales, o alias, para los servidores de alojamiento de un dominio. Es usado cuando se están corriendo múltiples servicios (como FTP y servidor web) en un servidor con una sola dirección IP. Cada servicio tiene su propia entrada de DNS (como ftp.ejemplo.com. y www.ejemplo.com.). Esto también es usado cuando corres múltiples servidores HTTP, con diferentes nombres, sobre el mismo host. Se escribe primero el alias y luego el nombre real. Ej. Ejemplo1 IN CNAME ejemplo2

* SRV = Service record (SRV record).

* TXT = Un registro TXT es un tipo de registro DNS que proporciona información de texto a fuentes externas a tu dominio.El texto puede ser lenguaje legible por máquina o por el ser humano, y se puede utilizar para diversos fines.

![](images/CrearDNS.png)