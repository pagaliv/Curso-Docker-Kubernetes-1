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

```bash
# Añade la clave GPG oficial de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
La clave GPG es la clave publico-privada que te garantiza que te estas instalando la información de docker y no de un tercero. 
- curl -fsSL: Descarga silenciosamente la clave
- gpg --dearmor: Convierte la clave en formato binario
- -o: Guarda el archivo en la ruta especficiada

```bash
# Añade el repositorio de Docker
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- deb: indica que es un repo de paquetes
- arch=$(dpkg --print-architecture): Detecta automáticamente tu arquitectura
- signed-by=...: Especifica qué clave GPG usar para verificar paquetes
- $(lsb_release -cs): Obtiene el nombre de tu versión de Ubuntu
- tee: Escribe la línea en el archivo /etc/apt/sources.list.d/docker.list
- > /dev/null: Suprime la salida para no mostrar el contenido en pantalla

```bash
#actualiza la lista de paquetes disponibles en Ubuntu
sudo apt update
```
Actualiza los repositorios nuevamente para incluir el nuevo repositorio de Docker que acabas de añadir.

```bash
# Instala Docker
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```bash
# Añade tu usuario al grupo docker para no usar sudo siempre
sudo usermod -aG docker $USER
```
- -Ag: Añade(append) al Grupo
- docker: Nombre del grupo
- $USER: variable que contiene tu nombre de usuario
Se podra usar docker sin sudo, ahorrando escribirlo cada vez.

```bash
# Añade tu usuario al grupo docker para no usar sudo siempre
sudo usermod -aG docker $USER
```

Verifica que funciona:
```bash
docker --version
docker run hello-word
```

Si todo ha salido bien debería aparecer un mensaje similar al siguiente 
```bash
Docker version [tu-version], build [cod]
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
[cod2]: Pull complete 
[cod3]: Download complete 
Digest: sha256:[cod4]
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
---
### Paso 2: Instalación de Kubernetes (Minikube) en Linux
```bash
# Descarga el binario de Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Descarga kubectl (el cliente de Kubernetes)
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Verifica
minikube version
kubectl version --client
```
Para verificar que todo ha ido correctamente deberán aparecer las versiones correspondientes de ambos comandos.

---
### Paso 3: verificación de correcto funcionamiento

```bash
minikube start --driver=docker
kubectl get nodes
# Deberías ver un nodo con estado "Ready"
```
