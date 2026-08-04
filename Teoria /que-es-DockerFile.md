# ¿Que es dockerfile?
Un Dockerfile es un archivo de texto con instrucciones para contruir una imagen en Docker. Es como "una receta de comida" que le dice como crear tu aplicación empaquetada.
---
# Estructura básica de un Dockerfile
```bash
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
