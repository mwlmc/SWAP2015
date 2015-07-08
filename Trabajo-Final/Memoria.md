#Montar un servidor en nuestra maquina

Para usar nuestro terminar a modo de servidor,en primer lugar toda la información y debería de estar duplicada en un lugar seguro ya que lo que vamos a realizar es la creación de un servidor en una maquina local para servir peticiones mientras se realiza el rearme del servidor principal.

Existen varias formas de realizar el montaje de un servidor la más rápida para algo temporal podría ser desde una maquina virtual. Para ello necesitamos la previa instalación de un entorno de virtualización para cargar la imagen de alguno de los sistemas operativos que utilizaremos para el servidor, en mi caso he utilizado la imagen de Ubuntu 12.04 server  que previamente había instalado con las herramientas básicas que tengo preparada y exportada para cualquier función necesaria. 

Una vez realizado el paso anterior lo que he realizado es la carga y puesta en marcha de dicho sistema operativo exportado y he instalado las herramientas necesarias para  la puesta en marcha. Después de importar la maquina con el sistema procedemos a iniciarla y a introducir el login que establecimos en la anterior instalación o incluso en la maquina del servidor principal.

Ahora el siguiente paso será loguearnos como superusuario y acceder al fichero interfaces en la ruta de /etc/network/interfaces
Ahí será donde cambiaremos la dirección ip(192.168.1.10) la máscara subred(255.255.255.0) y el puerto de enlace(192.168.1.1) para poder conectarnos desde otra máquina externa pondremos la ip fija (static)y asi poder acceder desde otro sistema, fuera el virtualbox. Después de realizar esta configuración tendremos que reiniciar la máquina para que los cambios se hagan efectivos.

Una vez iniciada y logueda de nuevo la maquina realizamos un update y seguidamente instalaremos apache.

```sh
apt-get install apache2
```

Una vez instalado apache vamos a la ruta /etc/apache2/ y a la carpeta  mods available ahí vemos los mods que se puede aplicar en apache y lo que hacemos es copiar userdir.conf y userdir.log a la carpeta /etc/apache2/mods-enable.Cada mods le da cosas nuevas a apache.

Y reiniciamos apache con : 
```sh
/etc/init.d/apache2 restart
```

También instalaremos php5 

```sh
apt-get install php5 libapache2-mod-php5
```
Creamos una maquina nueva en el virtualizador para usarla de balanceador. Dicho balanceador deberá de repartir la señal siempre al primer servidor pero en caso de no responder quien responderá a dichas peticiones será el servidor de respaldo creado en nuestro terminal.
 Como software para realizar el balanceo he elegido nginx ya que lo hemos trabajado en las prácticas. 
Este balanceador estará físicamente fuera de mi maquina principal puesto que mi maquina será de uso personal hasta el momento de que yo descubra que el servidor principal esta caído. Pero debido a que esto se trata de una simulación será una maquina virtual en mi equipo.
```sh
La direcciones de los diferentes equipos serán:
Balanceador: 192.168.1.10
Servidor principal: 192.168.1.11
Servidor temporal en mi equipo: 192.168.1.12
```
Las configuraciones de red de las maquinas serán doble en los servidores para que se vean y la otra para que se vean entre ellas pero eso no es necesario puesto que son maquina que nunca tendrán que comunicarse.
Ahora voy a crear el archivo de configuración de nginx para servir las peticiones con la restricción de que si el servidor principal se cae o no esta disponible pueda servirla mi maquina personal.
![](http://i.imgur.com/Dkwwr2N.jpg)
he añadido que solo pueda tener 3 errores máximo y que el tiempo de fallo sea como máximo 10s.

La opción backup junto a la dirección de mi servidor principal es la que me da lugar a servirle la petición en caso de que no responda el servidor principal.
Una vez realizada la configuración de nginx reiniciamos la maquina ya que a esta también hemos tenido que acceder a su fichero interfaces para asignarle una dirección estática.
Ya hemos reiniciado ,ahora iniciamos nginx con 
```sh service nginx start ```.

Imágenes de la realización:
#Peticion al balanceador estando el servidor principal disponible
![](http://i.imgur.com/AhkBeR1.jpg)

#Peticion al balanceador estando el servidor principal fuera de servicio.
![](http://i.imgur.com/oOJmHzD.jpg)

