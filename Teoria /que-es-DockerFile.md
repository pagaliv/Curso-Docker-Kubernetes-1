# ¿Que es dockerfile?
Un Dockerfile es un archivo de texto con instrucciones para contruir una imagen en Docker. Es como "una receta de comida" que le dice como crear tu aplicación empaquetada.
---
# Estructura básica de un Dockerfile
```dockerfile
# Comentarios (empiezan con #)

# 1. Imagen base (el "punto de partida")
FROM ubuntu:22.04

# 2. Información del mantenedor (opcional)
LABEL maintainer="tu@email.com"

# 3. Ejecutar comandos durante la construcción
RUN apt-get update && apt-get install -y python3

# 4. Copiar archivos desde tu PC a la imagen
COPY app.py /app/

# 5. Establecer directorio de trabajo
WORKDIR /app

# 6. Exponer puertos
EXPOSE 8080

# 7. Comando que se ejecuta al iniciar el contenedor
CMD ["python3", "app.py"]
```
---

#  Componentes clave (instrucciones principales)
## FROM - la base 
```dockerfile
FROM ubuntu:22.04
FROM node:18-alpine
FROM python:3.11-slim
```
Define la imagen base sobre la que se contruira y siempre es la primera intrucción de un Dockerfile, se pueden usar imagenes propias como oficiales.

## RUN - ejecutar comandos 
```dockerfile
RUN apt-get update
RUN pip install flask
RUN npm install -g create-react-app
```
ejecuta comandos durante la contrucción de la imagen, cada RUN crea una nueva capa en la imagen.

## COPY y ADD - Copiar archivos
```dockerfile
COPY app.py /app/
COPY . /usr/src/app/
ADD https://ejemplo.com/archivo.tar.gz /tmp/
```
copia archivos desde tu sistema a la imagen, COPY es el simple y si solo hay que trasportarlo es el recomendado, por su parte ADD tiene funcionalidades extras como descomprimir o descargar URLs.

## WORKDIR - Directorio de trabajo
```dockerfile
WORKDIR /app
WORKDIR /usr/src/proyecto
```
Establece en el directorio donde se ejecutan los comandos, es como el cd dentro de la imagen, sirve para moverse.

## ENV - Variables de entorno
```dockerfile
ENV NODE_ENV=production
ENV PORT=3000
ENV DATABASE_URL=postgresql://...
```
Define variables de entorno dentro del contenedor

