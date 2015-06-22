#Comprobar el rendimiento de servidores web

##En esta práctica se deben usar las dos herramientas para medir, primero el rendimiento de una sola máquina servidora (haciendo peticiones a la IP de la máquina 1 , p.ej.), y a continuación el rendimiento de la granja web cuando usamos balanceo de carga tanto con nginx como con haproxy (haciendo las peticiones a la dirección IP del balanceador). 

##Tres configuraciones a evaluar: (1) servidor solo, (2) granja web con nginx, (3) granja web con haproxy.

Existen diversas herramientas para comprobar el rendimiento de servidores web. Las hay basadas en interfaz de línea de comandos y de interfaz gráfica.Yo personalmente utilizare apache Benchmark ,siege y openload.

En todas las pruebas para la obtencion de datos he tenido que realizar una carga especial en cada caso por que mi equipo no era capaz de disipar el calor de mi terminal y no llegaba a terminar las ejecuciones por lo que he decidido realizar cargas menos y en los datos no se aprecian diferencias muy significativas.

- ##Apache
![](http://i.imgur.com/6IsC9dn.png)

- Graficas
- Time taken for tests,Filed requests,Requests per second
![](http://i.imgur.com/qRLfLAa.png)

- ##Siege
![](http://i.imgur.com/vYzOkls.png)

- Graficas
- Response time (s),Transaction rate (p/s),Longest transaction
![](http://i.imgur.com/jwbH2vz.png)

- ##Openload
![](http://i.imgur.com/vTfgVlg.png)

- Graficas
- Avg. Response time(s),Max. Response time(s),Total Resquests
![](http://i.imgur.com/z6g3QKg.png)
