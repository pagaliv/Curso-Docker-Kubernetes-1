# Curso-Docker-Kubernetes-1
Breve curso sobre docker con los conocimientos que he ido adquieriendo por si le resultan útiles a alguién 

## Instalaciones y preparación del curso (Linux)

### Paso 1: Instalación de Docker en Linux
Para instalar Docker procederemos de forma estandar
```bash
#actualiza la lista de paquetes disponibles en Ubuntu
sudo apt update
```
```bash
#Instalamos las dependencias necesarias 
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```
- apt-trasport-https: Permite a apt usar repositorios HTTPS
- ca-certificates: Certificados SSL para conexiones seguras
- curl: Herramienta para trasferir datos
- software-propierties-common: Añade comandos como add-apt-repository que es un atajo para añadir repositorios facilmente
- -y: Responde automaticamente "Si" a las preguntas de isntalación
