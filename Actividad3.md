## Opción 1: Creación y uso de volúmenes
1. Crear volúmenes
Crea dos volúmenes con docker volume:

    ```html
    docker volume create volumen_datos
    docker volume create volumen_web
    ```

![](imagenes/Actividad3/Imagen1.png)

2. Arrancar contenedor c1
Arranca un contenedor llamado c1 con la imagen php:7.4-apache y monta el volumen volumen_web:

    ```html
    docker run -d --name c1 -p 8080:80 -v volumen_web:/var/www/html php:7.4-apache
    ```

![](imagenes/Actividad3/Imagen2.png)

3. Arrancar contenedor c2
Arranca un contenedor llamado c2 con la imagen mariadb y monta el volumen volumen_datos. La contraseña del root será admin:

    ```html
    docker run -d --name c2 -e MYSQL_ROOT_PASSWORD=admin -v volumen_datos:/var/lib/mysql mariadb
    ```

![](imagenes/Actividad3/Imagen3.png)

4. Borrar el volumen volumen_datos
Primero, detén y elimina el contenedor c2:

    ```html
    docker rm -f c2
    ```

![](imagenes/Actividad3/Imagen4.png)

Luego, borra el volumen:

    ```html
    docker volume rm volumen_datos
    ```

![](imagenes/Actividad3/Imagen5.png)

5. Copiar archivo index.html a c1
Crea el archivo index.html en tu sistema local:

    ```html
    <h1>HOLA SOY Alberto Vicente Garcia</h1>
    ```

![](imagenes/Actividad3/Imagen6.png)

Copia el archivo al contenedor c1:

    ```html
    docker cp index.html c1:/var/www/html/index.html
    ```

![](imagenes/Actividad3/Imagen7.png)

Verifica que se puede acceder en el navegador a:
http://localhost:8080/index.html

![](imagenes/Actividad3/Imagen8.png)

6. Crear contenedor c3
Borra el contenedor c1 y crea c3 usando el mismo volumen volumen_web pero sirviendo en el puerto 8081:

    ```html
    docker rm -f c1
    ```

![](imagenes/Actividad3/Imagen9.png)

    ```html
    docker run -d --name c3 -p 8081:80 -v volumen_web:/var/www/html php:7.4-apache
    ```

![](imagenes/Actividad3/Imagen10.png)

Accede en el navegador a:
http://localhost:8081/index.html

![](imagenes/Actividad3/Imagen11.png)

## Opción 2: Bind mount para compartir datos
1. Crear carpeta y archivo index.html
En tu sistema local, crea la carpeta saludo y el archivo index.html con:

    ```html
    mkdir saludo
    echo "<h1>HOLA SOY Alberto Vicente Garcia</h1>" > saludo/index.html
    ```

![](imagenes/Actividad3/Imagen12.png)

2. Arrancar contenedor c1
Arranca el contenedor c1 con bind mount en el puerto 8181:

    ```html
    docker run -d --name c1 -p 8181:80 -v $(pwd)/saludo:/var/www/html php:7.4-apache
    ```

![](imagenes/Actividad3/Imagen13.png)

3. Arrancar contenedor c2
Arranca el contenedor c2 con bind mount en el puerto 8282:

    ```html
    docker run -d --name c2 -p 8282:80 -v $(pwd)/saludo:/var/www/html php:7.4-apache
    ```

![](imagenes/Actividad3/Imagen14.png)

4. Verificar acceso a c1 y c2
Accede a:

http://localhost:8181/index.html (para c1)

![](imagenes/Actividad3/Imagen15.png)

http://localhost:8282/index.html (para c2)

![](imagenes/Actividad3/Imagen16.png)

5. Modificar el archivo index.html
Modifica el archivo local:

    ```html
    echo "<h1>Hola, este es el nuevo contenido</h1>" > saludo/index.html
    ```

![](imagenes/Actividad3/Imagen17.png)

6. Comprobar acceso después de la modificación
Accede nuevamente a:

http://localhost:8181/index.html (para c1)

![](imagenes/Actividad3/Imagen18.png)

http://localhost:8282/index.html (para c2)

![](imagenes/Actividad3/Imagen19.png)
