# ProyectoSRI_1Trimestre

Vamos a instalar un servidor web interno para un instituto. Se Pide:<br><br>
### 1º Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python<br><br>

Actualizar repositorios  sudo apt update<br>
Instalar apache2 sudo apt install apache2<br>
Tendríamos listo apache y Comprobaremos que se ha instalado correctamente
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap1.jpg)

Crearemos los dominios centro.intranet y departamento.centro.intranet en www<br>
cd /var/www<br>
sudo mkdir centro.intranet<br>
sudo mkdir departamentos.centro.intranet<br><br>
Añadimos el dominio departamento.centro.intranet y centro.intranet en el fichero /etc/host<br>
cd /etc<br>
sudo nano hosts<br><br>
Ponemos una ip a centro.intranet y departamento.centro.intranet<br>
127.0.1.74        centro.intranet<br>
127.0.1.74        departamentos.centro.intranet<br><br>
Le daremos entorno y y archivo de configuración a cada uno de los dominios<br>
sudo chown -R $USER:$USER /var/www/centro.intranet<br>
sudo chown -R $USER:$USER /var/www/departamentos.centro.intranet<br>
sudo nano /etc/apache2/sites-available/departamentos.centro.intranet.conf<br>
sudo nano /etc/apache2/sites-available/centro.intranet.conf<br><br>
Dentro de los archivos: 1º en centro.intranet 2º en departamentos.centro.intranet<br>
<VirtualHost *:80><br>
    ServerName departamentos.centro.intranet<br>
    ServerAlias www.departamentos.centro.intranet<br>
    ServerAdmin webmaster@localhost<br>
    DocumentRoot /var/www/departamentos.centro.intranet<br>
    ErrorLog ${APACHE_LOG_DIR}/error.log<br>
    CustomLog ${APACHE_LOG_DIR}/access.log combined<br>
</VirtualHost><br>
<VirtualHost *:80><br>
    ServerName centro.intranet<br>
    ServerAlias www.centro.intranet<br>
    ServerAdmin webmaster@localhost<br>
    DocumentRoot /var/www/centro.intranet<br>
    ErrorLog ${APACHE_LOG_DIR}/error.log<br>
    CustomLog ${APACHE_LOG_DIR}/access.log combined<br>
</VirtualHost><br><br>
Habilitamos los virtualhost<br>
sudo a2ensite departamentos.centro.intranet<br>
sudo a2ensite centro.intranet<br><br>
Reiniciamos el servicio de apache<br>
sudo service apache2 restart<br><br>
Vamos a ver que funcione centro.intranet y departamentos.centro.intranet<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap2.jpg)<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap3.jpg)

### 2º Activar los módulos necesarios para ejecutar php y acceder a mysql<br><br>

Vamos a instalar php sudo apt-get install php<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap4.jpg)<br>
Instalaremos mysql server sudo apt-get install mysql-server<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap5.jpg)<br>
Comprobamos que se ha instalado php<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap6.jpg)

### 3º Instala y configura wordpress<br><br>

Descargamos y extraemos wordpress de la página oficial<br>
Nos conectaremos a mysql para crear la base de datos de wordpress<br>
create database wordpress;<br><br>
Creamos un usuario de la base de datos<br>
grant all on wordpress.* to 'brian'@'localhost' identified by 'brian';<br><br>
Reiniciamos apache<br>
sudo service apache2 restart<br><br>
Vamos al navegador y ya podremos visualizar wordpress y configurarlo<br>
Escribimos las crendenciales<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap7.jpg)<br>
Escribimos el usuario y contraseña<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap8.jpg)<br>
Ya habremos acabado la configuración, podremos iniciar sesión y ya estariamos dentro<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap9.jpg)<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap10.jpg)<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap11.jpg)<br>

### 4º Activar el módulo “wsgi” para permitir la ejecución de aplicaciones Python<br><br>

Vamos a ejecutar el siguiente comando:<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap12.jpg)

### 5º Crea y despliega una pequeña aplicación python para comprobar que funciona correctamente.<br><br>

Creamos la carpeta departamentos.centro.intranet dentro del directorio html:<br>
cd /var/www/html/
sudo mkdir departamentos.centro.intranet<br><br><br>
Cremaos 2 directorios mypythonapp y publi_html dentro de aquel directorio<br>
cd /var/www/html/departamentos.centro.intranet<br>
sudo mkdir mypythonapp<br>
sudo mkdir public_html<br><br>
Creamos un archivo python controlador dentro de la carpeta mypythonapp<br>
cd /var/www/html/departamentos.centro.intranet/mypythonapp<br>
sudo nano controller.py<br>
En ella habrá:<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap13.jpg)<br><br>
Creamos el archivo de virtual host en el directorio sites-available<br>
cd /etc/apache2/sites-available<br>
sudo nano departamentos.centro.intranet.conf<br><br>
Añadiremos a las lineas del archivo de configuracion de departamentos.centro.intranet:<br>
<VirtualHost *:80><br>
    ServerName departamentos.centro.intranet<br>
    DocumentRoot /var/www/html/departamentos.centro.intranet/public_html<br>
    WSGIScriptAlias / /var/www/html/departamentos.centro.intranet/mypythonapp/controller.py<br>
</VirtualHost><br><br>
Habilitamos el virtualhost, lo reiniciamos y podremos entrar:<br>
sudo a2ensite departamentos.centro.intranet.conf<br>
sudo service apache2 restart<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap14.jpg)


### 6º Adicionalmente protegeremos el acceso a la aplicación python mediante autenticación<br><br>

Instalamos las utilidades de apache<br>
sudo apt-get install apache2-utils<br><br>
Creamos el usuario<br>
sudo htpasswd -c /etc/apache2/.htpasswd brian<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap15.jpg)<br>
Vamos al archivo departamentos.centro.intranet.conf y le añadimos lo siguiente:<br>
sudo nano /etc/apache2/sites-enabled/departamentos.centro.intranet.conf<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap16.jpg)<br>
Reiniciamos apache2<br>
sudo systemctl restart apache2<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap17.jpg)
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap18.jpg)

### 7º Instala y configura awstat.<br><br>

Instalamos el servicio de AWstats<br>
sudo apt-get install awstats<br><br>
Luego habilitamos el modulo cgi<br>
sudo service apache2 restart<br>
sudo a2enmod cgi<br><br>
Configuramos el sitio web editando los siguientes puntos<br>
sudo cp /etc/awstats/awstats.conf /etc/awstats/awstats.departamentos.centro.intranet.conf<br>
sudo nano /etc/awstats/awstats.departamentos.centro.intranet.conf<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap19.jpg)<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap20.jpg)<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap21.jpg)<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap22.jpg)<br>
Terminaremos de configurar el apache junto con el awstats<br>
sudo /usr/lib/cgi-bin/awstats.pl -config=departamentos.centro.intranet -update<br><br>
sudo cp -r /usr/lib/cgi-bin /var/www/html/departamentos.centro.intranet<br>
sudo chown -R www-dat www-data /var/www/html/departamentos.centro.intranet/cgi-bin/<br><br>
Haremos un restart en el apache:<br>
sudo service apache2 restart<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap23.jpg)


### 8º Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio “servidor2.centro.intranet”. Debes configurarlo para que sirva en el puerto 8080 y haz los cambios necesarios para ejecutar php. Instala phpmyadmin.<br><br>

Instalamos nginx:<br>
sudo apt install nginx<br><br>
Habilitamos el servicio de nginx HTTP<br>
sudo ufw allow 'Nginx HTTP'<br><br>
Podemos visualizarlo, pero nos pide cambiar el puerto a uno deseado:<br>
sudo nano /etc/nginx/sites-available/default<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap24.jpg)<br>
Reiniciamos el servicio de nginx<br>
sudo service nginx restart<br>
![](https://github.com/brianllj03/ProyectoSRI_1Trimestre/blob/main/cap25.jpg)








