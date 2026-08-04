# Comandos gestion de imagenes
## docker build - contruir una imagen desde un Dockerfile
```bash
docker build [opciones] -t <nombre>:<tag> <ruta_del_dockerfile>
```
Lee el Dokerfile, ejecuta cada instrucción y genera una imagen.
Ejemplos:
```bash
# Construir con nombre y versión
docker build -t mi-app:1.0 .

# Construir sin usar cache (forzar rebuild)
docker build --no-cache -t mi-app:1.0 .

# Construir usando un archivo Dockerfile con otro nombre
docker build -f Dockerfile.prod -t mi-app:prod .
```
