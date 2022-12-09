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




### 4º Activar el módulo “wsgi” para permitir la ejecución de aplicaciones Python<br><br>



### 5º Crea y despliega una pequeña aplicación python para comprobar que funciona correctamente.<br><br>



### 6º Adicionalmente protegeremos el acceso a la aplicación python mediante autenticación<br><br>


### 7º Instala y configura awstat.<br><br>


### 8º Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio “servidor2.centro.intranet”. Debes configurarlo para que sirva en el puerto 8080 y haz los cambios necesarios para ejecutar php. Instala phpmyadmin.<br><br>


