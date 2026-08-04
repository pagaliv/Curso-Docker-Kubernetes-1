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
d
