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

