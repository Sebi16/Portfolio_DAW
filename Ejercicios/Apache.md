# Apache

## Introducción

Apache HTTP Server es el servidor web por excelencia. Es una herramienta libre que ha acompañado el desarrollo de la web prácticamente desde sus inicios y durante mucho tiempo ha sido el servidor web más utilizado en Internet aunque recientemente ha cedido el podio a otro servidor libre: nginx.

El servidor web Apache HTTP Server se desarrolla de manera abierta bajo el amparo de la Fundación Apache que también desarrolla muchos otros proyectos libres e interesantes.

## Configuración Apache

### 1.Instalar Apache:  
A continuación,instale el paquete apache2:
```
sudo apt install apache2
```
### 2.Ajustar el firewall:  
Antes de probar Apache, es necesario modificar los ajustes de firewall para permitir el acceso externo a los puertos web predeterminados. Suponiendo que siguió las instrucciones de los requisitos previos, debería tener un firewall UFW configurado para que restrinja el acceso a su servidor.

Durante la instalación, Apache se registra con UFW para proporcionar algunos perfiles de aplicación que pueden utilizarse para habilitar o deshabilitar el acceso a Apache a través del firewall.

Enumere los perfiles de aplicación ufw escribiendo lo siguiente:
```
sudo apt install apache2
```
Obtendrá una lista de los perfiles de aplicación:
```
Output
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
```
Como lo indica el resultado, hay tres perfiles disponibles para Apache:
1. Apache: este perfil abre solo el puerto 80 (tráfico web normal no cifrado)
2. Apache Full: este perfil abre el puerto 80 (tráfico web normal no cifrado) y el puerto 443 (tráfico TLS/SSL cifrado)
3. Apache Secure: este perfil abre solo el puerto 443 (tráfico TLS/SSL cifrado)
A continuacion vamos a habilitar Apache:
```
sudo ufw allow 'Apache'
```
Puede verificar el cambio escribiendo lo siguiente:
```
sudo ufw status
```
El resultado proporcionará una lista del tráfico de HTTP que se permite:
```
Estado: activo

Hasta                      Acción      Desde
-----                      ------      -----
Apache                     ALLOW       Anywhere                  
Apache (v6)                ALLOW       Anywhere (v6)
```
Como lo indica el resultado, el perfil se activó para permitir el acceso al servidor web Apache.
### 3.Comprobar su servidor web:
Para comprobar si el servidor web esta ya activo escribimos los siguiente.
```
sudo systemctl status apache2
```
```
Output
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2020-04-23 22:36:30 UTC; 20h ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 29435 (apache2)
      Tasks: 55 (limit: 1137)
     Memory: 8.0M
     CGroup: /system.slice/apache2.service
             ├─29435 /usr/sbin/apache2 -k start
             ├─29437 /usr/sbin/apache2 -k start
             └─29438 /usr/sbin/apache2 -k start
```
Puede acceder a la página de destino predeterminada de Apache para confirmar que el software funcione correctamente mediante su dirección IP: Si no conoce la dirección IP de su servidor, puede obtenerla de varias formas desde la línea de comandos.

```
hostname -I
```
Cuando tenga la dirección IP de su servidor, introdúzcala en la barra de direcciones de su navegador:
```
http://192.168.0.134
```
Debería ver la página web predeterminada de Apache en Ubuntu 20.04:
![](https://assets.digitalocean.com/articles/how-to-install-lamp-ubuntu-16/small_apache_default.png)
### 4.Administrar el proceso de Apache:
Ahora que el servidor web está listo y en funcionamiento, repasemos algunos comandos de administración básicos con systemctl.
Para detener su servidor web, escriba lo siguiente:
```
sudo systemctl stop apache2
```
Para iniciar el servidor web cuando no esté activo, escriba lo siguiente:
```
sudo systemctl start apache2
```
Para detener y luego iniciar el servicio de nuevo, escriba lo siguiente:
```
sudo systemctl restart apache2
```
Si solo realiza cambios de configuración, Apache a menudo puede recargarse sin cerrar conexiones. Para hacerlo, utilice este comando:

```
sudo systemctl reload apache2
```
Por defecto, Apache está configurado para iniciarse automáticamente cuando el servidor lo hace. Si no es lo que quiere, deshabilite este comportamiento escribiendo lo siguiente:

```
sudo systemctl disable apache2
```
Para volver a habilitar el servicio de modo que se cargue en el inicio, escriba lo siguiente:
```
sudo systemctl enable apache2
```
Ahora, Apache debería iniciarse de forma automática cuando el servidor lo haga de nuevo.

### 5. Configuración del archivo de configuración de VirtualHost

Comenzamos este paso yendo al directorio de archivos de configuración:
```
cd /etc/apache2/sites-available/
```
Dado que Apache vino con un archivo VirtualHost predeterminado, usémoslo como base. (gci.conf se usa aquí para que coincida con nuestro nombre de subdominio):
```
sudo cp 000-default.conf gci.conf
```
Editamos el archivo:
```
sudo nano gci.conf
```
Una vez dentro del archivo escribimos lo siguiente:
```
ServerAdmin yourname@example.com
```
```
DocumentRoot /var/www/gci/
```
```
ServerName gci.example.com
```

### 6. Activating VirtualHost file
Después de configurar nuestro sitio web, debemos activar el archivo de configuración de hosts virtuales para habilitarlo.
Para habilitarlo usaremos lo siguiente comando:
```
sudo a2ensite gci.conf
```
Deberías ver el siguiente resultado:
```
Enabling site gci.
To activate the new configuration, you need to run:
  service apache2 reload
root@ubuntu-server:/etc/apache2/sites-available#
```
Para cargar el nuevo sitio, reiniciamos Apache escribiendo:
```
service apache2 reload
```
Una vez realizado todo nos tendría que salir el siguiente resultado:  
![](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/2X/7/7d6944922296826f70f27ec9b5eff67bd7f46158.png)

En el caso de que nos saliera el siguiente problema:  
![](https://www.desarrollolibre.net/public/images/example/apache/sitio-caido.png?ezimgfmt=rs:300x225/rscb1/ng:webp/ngcb1)

Deberemos ir al siguiente directorio y modificar el archivo hosts.
```
cd /etc/hosts
```
Una vez dentro ejecutaremos el siguiente comando
```
sudo nano hosts
```
Dentro del archivo hosts deberemos agrgar nuestro dominio.
```
127.0.0.1 desarrollolibre2.net
```
Ahora si navegamos a nuestro dominio podremos visulizar nuestra pagina.  
![](https://www.desarrollolibre.net/public/images/example/apache/sitio-activo.png?ezimgfmt=rs:300x286/rscb1/ng:webp/ngcb1)

## Conclusión
Apache es el servidor web con el que trabajan miles de hosting a nivel mundial.  
Es ideal para pequeñas y medianas empresas que desean tener presencia en el mundo digital. Muy compatible con WordPress, lo que permite poder trabajar de manera sencilla y ordenada.

## Bibliografía
[Link 1](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-es)  
[Link 2](https://ubuntu.com/tutorials/install-and-configure-apache#1-overview)  
[Link 3](https://www.desarrollolibre.net/blog/apache/que-son-y-como-emplear-los-virtualhost-en-apache)  
[Link 4](https://www.neolo.com/blog/que-es-apache-y-como-funciona-este-servidor.php)  
[Link 5](https://elpuig.xeill.net/Members/vcarceler/articulos/introduccion-a-apache-http-server)  


