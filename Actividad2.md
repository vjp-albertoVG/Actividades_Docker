# Ejercicio para entregar

## Servidor web

1. Ejecuta el siguiente comando para crear y ejecutar el contenedor nginx en modo demonio, mapeando el puerto 8181 del host al puerto 80 del contenedor:


    ```html
    docker run -d --name servidor_web -p 8181:80 nginx
    ```

![](imagenes/imagenesACT2/imagen1.png)

Para comprobar que el contenedor está funcionando correctamente, ejecuta:

    ```html
    docker ps
    ```

Esto mostrará una lista de contenedores activos, incluido el que acabas de crear. 

![](imagenes/imagenesACT2/imagen2.png)

2. Para entrar en la pagina tenemos que poner el el navegador de nustra maquina localhost:8181 y nos saldra la pagina de nginx.

![](imagenes/imagenesACT2/imagen3.png)  
   
3. Para ver las imágenes locales en tu registro Docker, ejecuta el siguiente comando:
 
    ```html
    docker images
    ```
    
Este comando mostrará una lista de las imágenes descargadas, incluida la de nginx.
     
    ![](imagenes/imagenesACT2/imagen4.png) 

4. Para eliminar los contenedores tenemos que poner 


    ```html
    docker rm -f servidor_web
    ```
    ![](imagenes/imagenesACT2/imagen5.png)  

5. Para demos trar que ya no esta iniciado el contenedor

    ```html
    docker ps -a
    ```

    ![](imagenes/imagenesACT2/imagen6.png)
