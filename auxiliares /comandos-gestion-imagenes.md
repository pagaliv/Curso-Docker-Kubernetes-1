# Comandos gestion de imagenes
## docker build - contruir una imagen desde un Dockerfile
```bash
docker build [opciones] -t <nombre>:<tag> <ruta_del_dockerfile>
```
Lee el Dokerfile, ejecuta cada instrucción y genera una imagen.
 ### Ejemplos
```bash
# Construir con nombre y versión
docker build -t mi-app:1.0 .

# Construir sin usar cache (forzar rebuild)
docker build --no-cache -t mi-app:1.0 .

# Construir usando un archivo Dockerfile con otro nombre
docker build -f Dockerfile.prod -t mi-app:prod .
```
### Flags Importantes 
- -t, --tag: Asigna nombre y versión a la imagen
- --no-cache: No usa la cache de capas anteriores
- -f, --file: Especifica un Dockerfile diferente
- --build-arg: Pasa variables en tiempo de contrucción

---

## docker images - Listar imágenes locales
```bash
docker images
docker images -a  # Muestra todas (incluyendo las intermedias)
```
### Ejemplo de salida
```bash
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
mi-app        1.0       abc123def456   5 minutes ago   1.2GB
python        3.11-slim 789ghi012jkl   2 weeks ago     125MB
```
---
## docker rmi - Elimiar imagenes
```bash
docker rmi <nombre_o_id>      # Elimina una imagen
docker rmi -f <id>            # Forzar eliminación
```

### Ejemplos
```bash
docker rmi mi-app:1.0         # Elimina la imagen v1.0
docker rmi abc123def456       # Elimina por ID
docker rmi $(docker images -q) # ¡CUIDADO! Elimina TODAS las imágenes
```
---
## docker tag - Renombrar/etiquetar una imagen
```bash
docker tag <imagen_original> <nuevo_nombre>:<tag>
```
### Ejemplo 
```bash
# Preparar para subir a Docker Hub
docker tag mi-app:1.0 usuario/mi-app:latest
docker tag mi-app:1.0 usuario/mi-app:1.0
```
----
# Comandos Gestion de contenedores
## docker run - Crear y ejecutar un contenedor
```bash
docker run [opciones] <imagen> [comando]
```
### Opciones fundamentales 
- -d, --detach: Ejecuta en segundo plano
- --name: Asigna un nombre al contenedor
- -p, -publish: Mapea puertos host:container
- -v, --volume: Monta un volumen para persistir datos
- -e, --env: Define variables de entorno
- --rm: Elimina el contenedor al deternerse

### Ejemplos practicos
```bash
# 1. Ejecutar en primer plano (ver logs)
docker run -p 8080:80 nginx

# 2. Ejecutar en segundo plano con nombre
docker run -d --name mi-web -p 8080:80 nginx

# 3. Con variables de entorno
docker run -d -e MYSQL_ROOT_PASSWORD=secreto -e MYSQL_DATABASE=mi_db mysql

# 4. Con volumen persistente
docker run -d -v /mi/datos:/app/data mi-app

# 5. Puerto mapeado y nombre
docker run -d --name mi-app -p 3000:3000 mi-app:1.0

# 6. Con recurso limitado
docker run -d --memory="512m" --cpus="1" nginx

# 7. Ejecutar y luego eliminar automáticamente
docker run --rm -it ubuntu bash

# 8. Ejecutar comando específico
docker run ubuntu ls -la
```

