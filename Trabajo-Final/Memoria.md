#Montar un servidor en nuestra maquina

Para usar nuestro terminar a modo de servidor en primer lugar toda la información y debería de estar duplicada en un lugar seguro ya que lo que vamos a realizar es la creación de un servidor en una maquina local para servir peticiones mientras se realiza el rearme del servidor principal.
Existen varias formas de realizar el montaje de un servidor la más rápida para algo temporal podría ser desde una maquina virtual.

Para ello necesitamos la previa instalación de un entorno de virtualización para cargar la imagen de alguno de los sistemas operativos que utilizaremos para el servidor, en mi caso he utilizado la imagen de Ubuntu 12.04 server  que previamente había instalado con las herramientas básicas que tengo preparada y exportada para cualquier función necesaria. Una vez realizado el paso anterior lo que he realizado es la carga y puesta en marcha de dicho sistema operativo exportado y he instalado las herramientas necesarias para  la puesta en marcha. Una vez importada la maquina con el sistema procedemos a iniciarla y a introducir el login que establecimos en la anterior instalación o incluso en la maquina del servidor principal.
Ahora el siguiente paso será loguearnos como superusuario y acceder al fichero interfaces en la ruta de /etc/network/interfaces
Ahí será donde cambiaremos la dirección ip la máscara subred y el puerto de enlace para poder conectarnos desde otra máquina externa pondremos la ip fija y asi poder acceder desde otro sistema, fuera el virtualbox. Después de realizar esta configuración tendremos que reiniciar la máquina para que los cambios se hagan efectivos.
Una vez iniciada y logueda de nuevo la maquina realizamos un update y seguidamente instalaremos apache.

```sh
apt-get install apache2
```

Una vez instalado apache vamos a la ruta /etc/apache2/ y a la carpeta  mods available ahí vemos los mods que se puede aplicar en apache y lo que hacemos es copiar userdir.conf y userdir.log a la carpeta /etc/apache2/mods-enable.Cada mods le da cosas nuevas a apache.
Y reiniciamos apache con : /etc/init.d/apache2 restart
También instalaremos php5 
```sh
apt-get install php5 libapache2-mod-php5
```
Ahora par aver si todo esto funciona accedemos a : /etc/apache2/mods-available y hacemos nano php5.conf
