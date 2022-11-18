# Examen Sebas DAW

## Índice

1. Introducción  
2. Ejercicio 2
3. Ejercicio 3
4. Ejercicio 4
5. Conclusion
6. Bibliografía


## Introducción
Vamos a realizar un examen en el cual explicaremos un tutorial por cada ejercicio de como usar servidor apache y servidor ssh. Para ello haremos los siguientes ejercicios que hay a continuacion en grupo.

## Ejercicio 2

Primero comprobamos que tenemos iniciado el servidor ssh.

```
sudo systemctl status ssh
```
```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-11-18 15:53:42 CET; 16min left
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 826 (sshd)
      Tasks: 1 (limit: 4561)
     Memory: 2.4M
     CGroup: /system.slice/ssh.service
             └─826 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Warning: some journal files were not opened due to insufficient permissions.

```

Si tenemos iniciado el ssh podremos conectar con el otro cliente para hacerlo usaremos el siguiente comando.
```
sudo ssh usuario@192.168.0.168
```
Una vez realizado la conexion y haber introducido la contraseña nos tendria que salir el siguiente resultado si todo ha ido correctamente.
```
[sudo] contraseña para sebastian: 
The authenticity of host '192.168.0.168 (192.168.0.168)' can't be established.
ECDSA key fingerprint is SHA256:iWkyi99XmZvsg5KHNJYRhUmMeitc3CltsPGZtX88Pfw.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.0.168' (ECDSA) to the list of known hosts.
usuario@192.168.0.168's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.13.0-30-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

Se pueden aplicar 172 actualizaciones de forma inmediata.
101 de estas son actualizaciones de seguridad estándares.
Para ver estas actualizaciones adicionales ejecute: apt list --upgradable


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
New release '22.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


2 updates could not be installed automatically. For more details,
see /var/log/unattended-upgrades/unattended-upgrades.log
Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Fri Nov 18 15:43:26 2022 from 192.168.0.128
usuario@usuario-OptiPlex-380:~$
```
Como vemos ya estamos conectados al usuario:
```
usuario@usuario-OptiPlex-380:~$
```
Ahora crearemos el directorio /var/www/sebastian para hacerlo usaremos el siguiente comando:
```
sudo mkdir var/www/sebastian
```
Una vez creado el directorio crearemos el fichero ejercicio2.txt para hacerlo usaremos el siguiente comando:
```
sudo touch ejercicio2.txt
```
Y con esto ya estaria la tarea realizada.

Opcional,Si tenemos un directorio como var/www/sebastian con varios subdirectorios, entonces el siguiente comando cambiará la propiedad de todos los directorios y subdirectorios al usuario usuario.
```
sudo chown -R usuario:usuario /var/www/sebastian/
```
Ahora podemos comprobar las propiedades de todos los directorios y subdirectorios pertenece a usuario:usuario:
```
cd /var/www/sebastian/
```
```
ls -l
```
```
total 0
-rw-r--r-- 1 usuario usuario 0 nov 18 15:59 ejercicio2.txt

```
Y si aparte queremos otorgar permisos al propietario del archivo para leer, escribir y ejecutar usaremos el siguiente comando:
```
chmod 755 ejercicio2.txt

```
Esto seria todo.

## Ejercicio 3
Para descargar una imagen usaremos el siguiente comando:
```
usuario@usuario-OptiPlex-380:/var/www/sebastian$ sudo wget https://iesalandalus.org/ciclos/semipresencial/daw-sp/daw.png
```
```
usuario@usuario-OptiPlex-380:/var/www/sebastian$ sudo wget https://iesalandalus.org/ciclos/semipresencial/daw-sp/daw.png
--2022-11-18 16:18:27--  https://iesalandalus.org/ciclos/semipresencial/daw-sp/daw.png
Resolviendo iesalandalus.org (iesalandalus.org)... 85.208.102.26
Conectando con iesalandalus.org (iesalandalus.org)[85.208.102.26]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 47546 (46K) [image/png]
Guardando como: “daw.png”

daw.png                     100%[===========================================>]  46,43K  --.-KB/s    en 0,05s   

2022-11-18 16:18:27 (931 KB/s) - “daw.png” guardado [47546/47546]

usuario@usuario-OptiPlex-380:/var/www/sebastian$ ls -l
total 48
-rw-r--r-- 1 root    root    47546 nov  7 13:35 daw.png
-rwxr-xr-x 1 usuario usuario     0 nov 18 15:59 ejercicio2.txt

```

## Ejercicio 4
Lo primero de todo comprobamos que tengamos el servidor apache en marcha,para comprobarlo usaremos el siguiente comando:
```
sebastian@usuario-OptiPlex-380:~$ sudo systemctl status apache2
[sudo] contraseña para sebastian: 
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-11-18 15:53:43 CET; 33min ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 866 (apache2)
      Tasks: 55 (limit: 4561)
     Memory: 7.8M
     CGroup: /system.slice/apache2.service
             ├─866 /usr/sbin/apache2 -k start
             ├─867 /usr/sbin/apache2 -k start
             └─868 /usr/sbin/apache2 -k start

nov 18 15:53:42 usuario-OptiPlex-380 systemd[1]: Starting The Apache HTTP Server...
nov 18 15:53:43 usuario-OptiPlex-380 apachectl[821]: AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 1>
nov 18 15:53:43 usuario-OptiPlex-380 systemd[1]: Started The Apache HTTP Server.
```
Como vemos el estado esta en active y eso indica que tenemos el servidor apache en marcha.

El siguiente paso a realizar es el de saber nuestra ip de la maquina,para saberlo usaremos el siguiente comando:
```
hostname -I
```
```
sebastian@usuario-OptiPlex-380:~$ hostname -I
192.168.0.131 

```

Cuando tenga la dirección IP de su servidor, introdúzcala en la barra de direcciones de su navegador:
```
http://192.168.0.131
```
Debería ver la página web predeterminada de Apache en Ubuntu 20.04:
![](https://github.com/Sebi16/examen/blob/main/Examen/ejer4.png?raw=true)

El siguiente paso a realizar es crear nuestro directorio:

```
sudo mkdir /var/www/html/
```
Dentro del directorio /var/www/html crearemos un fichero html,para crearlo usaremos el siguiente comando:

```
sudo touch sebas.html
```
Una vez creado vamos a modificarlos con el siguiente contenido,para modificarlos usaremos el siguiente comando:

```
sudo nano sebas.html 
```
El resultado debe quedar como en este ejemplo.
![](https://github.com/Sebi16/examen/blob/main/Examen/html.png?raw=true)

Ahora comenzamos el siguiente paso yendo al directorio de archivos de configuración:
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
ServerAdmin webmaster@localhost

```
```
DocumentRoot /var/www/html/
```
```
ServerName daw.ejercicio4.com
```

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
Despues de hacer todo estos pasos vamos a modificar el fichero hosts, para ello debemos entrar en el siguiente directorio:
```
cd /etc
```
```
sudo nano hosts

```
Una vez dentro del archivo hosts añadiremos nuestra ip local y el dominio,debera quedar de la siguiente manera.  
![](https://github.com/Sebi16/examen/blob/main/Examen/hosts.png?raw=true)

Por acabar solo faltaria comprobar nuestro dominio en la web,para hacerlo escribiremos los siguiente en la web:
```
http://daw.ejercicio4.com/sebas.html
```
Y deberiemoas ver el siguiente resultado:  
![](https://github.com/Sebi16/examen/blob/main/Examen/Resultadofinal.png?raw=true)


## Conclusión
Recomiendo este informe para aprobar la asigantura de Despliegue de Aplicaciones Web.
Mucha suerte.

## Bibliografia
[Link 1](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-es)  
[Link 2](https://ubuntu.com/tutorials/install-and-configure-apache#3-creating-your-own-website)  
[Link 3](https://jcastaneda.com/servidores/configurar-ssh-en-ubuntu-server-20-04/?cn-reloaded=1)  
[Link 4](https://www.hostinger.es/tutoriales/usar-comando-wget/)  
