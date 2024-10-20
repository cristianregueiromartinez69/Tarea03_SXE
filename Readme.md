## Tarea_03 Comandos Docker

***Apartados***
1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.
2. Crea un contenedor con el nombre 'dam_web1'.
3. Si quieres poder acceder desde el navegador de tu equipo, ¿que debes hacer?
   Utiliza bind mount para que el directorio del apache2 'htdocs' esté montado un directorio que tu elijas.
4. Realiza un 'hola mundo' en html y comprueba que accedes desde el navegador.
5. Crea otro contenedor 'dam_web2' con el mismo bind mount y a otro puerto, por ejemplo 9080.
6. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:
   http://localhost:9080

   http://localhost:8000
7. Realiza modificaciones de la página y comprueba que los dos servidores 'sirven' la misma página



### 1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.
```bash
#comando para descargar la imagen
sudo docker pull httpd:2.4

#comprobamos que existe
sudo docker images
```
Si la imagen está, es que hemos tenido éxito.

### 2. Crea un contenedor con el nombre 'dam_web1'.
```bash
#comando para crear el contenedor
sudo docker container create -i -t --name dam-web1 httpd

#comprobamos que ha sido creado
sudo docker ps -a
```

### 3. Si quieres poder acceder desde el navegador de tu equipo, ¿que debes hacer? Utiliza bind mount para que el directorio del apache2 'htdocs' esté montado un directorio que tu elijas.

```bash
#instalamos ssh y lo configuramos para establecer conexión con la máquina anfitriona
sudo apt install openssh-server

#mapeamos el puerto del contenedor al puerto del equipo con el siguiente comando
sudo docker run -d --name dam_web1 -p 8000:80 httpd:2.4

#una vez hechos los pasos anteriores, creamos un directorio nuevo
mkdir /home/cristian/mi_apache_host

#ahora ejecutamos esto para crear el contenedor con el directorio mapeado
sudo docker run -d --name dam_web1 -p 8000:80 -v /home/cristian/mi_apache_host:/usr/local/apache2/htdocs httpd:2.4
```
Con esto hicimos lo siguiente:
- corremos el contenedor
- le damos el nombre
- usamos -v para hacer el bind mount
- configuramos el directorio origen y el directorio destino
- abrimos http://http://10.0.9.151:8000/
- deberíamos ver la pagina de apache

### 4. Realiza un 'hola mundo' en html y comprueba que accedes desde el navegador.
```bash
#creamos un archivo html tal que así. podemos hacerlo con nano mismamente
 <html>
     <head>
         <title>Hola Mundo</title>
     </head>
     <body>
         <h1>Hola Mundo</h1>
     </body>
 </html>
#lo metemos en la carpeta /home/cristian/mi_apache_host y vamos a un navegador.
http://10.0.9.151:8000
```
Debería de aparecer el hola mundo del html

### 5. Crea otro contenedor 'dam_web2' con el mismo bind mount y a otro puerto, por ejemplo 9080.
```bash
#mismo procedimiento que en el contenedor anterior, pero cambiando puertos
sudo docker run -d --name dam_web2 -p 9080:80 -v /home/cristian/mi_apache_host:/usr/local/apache2/htdocs httpd:2.4

#comprobamos que corre
sudo docker ps
```

### 6. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador: http://localhost:9080 http://localhost:8000
```bash
#accedemos a un navegador e introducimos
 http://10.0.9.151:9080 
 http://10.0.9.151:8000
```
Deberíamos de poder ver un hola mundo en ambos servicios

### 7. Realiza modificaciones de la página y comprueba que los dos servidores 'sirven' la misma página
```bash
#abrimos el html de hola mundo e introducimos algunos cambios como estos
<html>
     <head>
         <title>Hola Diego</title>
     </head>
     <body>
         <h2><strong>Ambos servicios han sido cambiados<strong></h2>
         <p style="color: red;">Hala madrid</p>
     </body>
 </html>

#abrimos un navegador e introducimos
 http://10.0.9.151:9080 
 http://10.0.9.151:8000
```
Deberíamos de ver los cambios reflejados en los 2 si hemos seguido la guía.
