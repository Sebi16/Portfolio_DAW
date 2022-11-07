# Practica SSH

## PC Servidor
### Crear un usuario nuevo
Para crear un usuario nuevo usaremos los siguientes comandos:

Para crear el usuario olaya.
```
 sudo adduser olaya
```
Para dar permisos de superusuario.
```
sudo usermod -aG sudo olaya
```

### Activar servidor SSH
Para activar el servidor SSH usaremos los siguientes comandos:

Para iniciar el servidor SHH.
```
 sudo systemctl start ssh
```

### Buscar la ip del ordenador
Para buscar la ip del ordenador usaremos el siguiente comando:
```
ifconfig
```

## PC Cliente

### Entrar en el otro pc mediante SSH
Para entrar en un pc mediante ssh usaremos los siguientes comandos:

Para conectar con el otro pc.
```
 ssh olaya@192.168.0.135
```

Ejemplo del resultado:  
![](https://lh4.googleusercontent.com/TNsVTUC0cZELaz4gkRVRkzdJ1steWeVl0OZgFnN9ImzW6cQ8fzxVSbBUbao7YH0JxEY=w2400)

### Instalar Apache en el servidor
Para instalar apache en el sevidor usaremos los siguientes comandos:

Para instalar apache.
```
sudo apt install apache2
```

Para seguir con la parte de configuracion visitar los siguientes links:  
[Link 1](https://github.com/Sebi16/Portfolio_DAW/edit/main/Ejercicios/Apache.md)  
[Link 2]()  
[Link 3]()  

Una vez realizada la configuracion el resultado final debe ser similar al siguiente:  
![](https://lh6.googleusercontent.com/EkLnHS4MUgv2FCAyIICw4MH-9dhSr0GIaDu1nGuanYg3rEACEn9CHF2qdNxh34zxyXo=w2400)

### Pasa una web a algún lugar del servidor
Para pasar una pagina web lo primero deberemos cnfigurar el archivo de configuración de VirtualHost.

### Creacion y configuracion del virtualhost
Para crear y configurar el virtualhost, usaremos los siguientes comandos:

Comenzamos este paso yendo al directorio de archivos de configuración:
```
cd /etc/apache2/sites-available/
```

Dado que Apache vino con un archivo VirtualHost predeterminado, usémoslo como base. (gci.conf se usa aquí para que coincida con nuestro nombre de subdominio).
```
cd /etc/apache2/sites-available/
```

Editamos el archivo.
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

Después de configurar nuestro sitio web, debemos activar el archivo de configuración de hosts virtuales para habilitarlo. Para habilitarlo usaremos lo siguiente comando:
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

En el caso de que nos saliera el siguiente problema:  
![](https://www.desarrollolibre.net/public/images/example/apache/sitio-caido.png?ezimgfmt=rs:300x225/rscb1/ng:webp/ngcb1)

Pasaremos al siguiente paso que es Modificar los hosts.

### Modifica los host del local para que con la dirección elegida vaya a la ip del servidor
Para modificar los hosts deberiamos ir al siguiente directorio y modificar el archivo hosts.
```
cd /etc/hosts
```

Una vez dentro ejecutaremos el siguiente comando:
```
sudo nano hosts
```

Dentro del archivo hosts deberemos agrgar nuestro dominio.
```
127.0.0.1 desarrollolibre2.net
```
```
192.168.0.135 desarrollolibre2.net
```
Ahora si navegamos a nuestro dominio podremos visulizar nuestra pagina.
![](https://lh4.googleusercontent.com/ySvXjjaQJqoquzbNBg5hu7l_w5Yw8L7BIWXcx7RqLimRBo5DZXWZqcU3OKkSbY9iwb8=w2400)
