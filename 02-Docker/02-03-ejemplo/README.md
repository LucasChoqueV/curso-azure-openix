# Usar docker con un proyecto de prueba
1. Crear un archivo llamado `dockerfile` en la raiz del proyecto con el siguiente contenido.
```docker
# Usamos la imagen oficial de node y le ponemos el alias nodeBuild
FROM  node:18  as  nodeBuild

# Creamos la carpeta app como directorio de trabajo
WORKDIR  /app

# Copiamos todos los archivos al directorio de trabajo
COPY  .  .

# Instalamos las dependencias
RUN  npm  install

# Generamos la carpeta /dist con el proyecto buildeado
RUN  npm  run  build

# Usamos la imagen oficial de nginx
FROM  nginx:alpine

# Copiamos la carpeta /dist a la carpeta html
COPY  --from=nodeBuild  /app/dist  /usr/share/nginx/html

# Exponemos el puerto 80 para el servidor de nginx
EXPOSE  80

# Iniciamos nginx
CMD  ["nginx",  "-g",  "daemon  off;"]
```
2. Abrir CMD y moverse a la raiz del proyecto
3. Ejecutar `docker build -t my-app-image .`
4. Ejecutar `docker images` para validar, deberia aparecer una imagen llamada `my-app`
5. Ejecutar `docker run --name my-app-container -p 5000:80 -d my-app-image:latest` 
6. Validar con `docker ps`
7. En un navegador acceder a `http://localhost:5000`
8. Ingresar al container con `docker exec -it my-app-container sh`
9. Modificar el `index.html`
10. Detener el container con `docker stop my-app-container`
11. Borrar el contenedor con `docker rm my-app-container`
12. Borrar la imagen con `docker rmi my-app-image:latest` 