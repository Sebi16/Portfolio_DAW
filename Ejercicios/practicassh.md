# Practica SSH

## PC Servidor
### Crear un usuario nuevo
Para crear un usuario nuevo usaremos los siguientes comandos:

```
 sudo adduser olaya
```
Para crear el usuario olaya.
```
sudo usermod -aG sudo olaya
```
Para dar permisos de superusuario.

### Activar servidor SSH
Para activar el servidor SSH usaremos los siguientes comandos:
```
 sudo systemctl start ssh
```
Para iniciar el servidor SHH.

### Buscar la ip del ordenador
Para buscar la ip del ordenador usaremos el siguiente comando:
```
ifconfig
```

