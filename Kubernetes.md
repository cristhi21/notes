# Kubernetes
## Docs
- [Kubernetes tutorial](https://www.golinuxcloud.com/kubernetes-tutorial/)
- [kubernetes learning path](https://github.com/techiescamp/kubernetes-learning-path)

## Instalación de Kubectl

- Windows
https://kubernetes.io/es/docs/tasks/tools/included/install-kubectl-windows/
- Linux
https://kubernetes.io/es/docs/tasks/tools/included/install-kubectl-linux/
- MacOS
https://kubernetes.io/es/docs/tasks/tools/included/install-kubectl-macos/


**Instalar Kubectl**

**Minukube** 

crea un cluster de un solo nodo para probar en local Kubernetes

Funciona en un entorno de virtualización o de contenedores

Soporta distintos tipos de container runtimes

Instalar kubectl, para trabajar con el cluster de kubernetes

Tener un hypervisor o container runtime: Docker, Podman, HyperV, VirtualBox, VMWare, etc

**Comandos de Minikube**

```sh
minikube
minikube start
minikube status
minikube logs
```

**Ficheros** 

.kube, es un directorio típico para kubernetes
.minikube, directorio de minikube

**Crear un cluster con 2 nodes**

```sh
minikube profile list
minikube start --driver=docker -p cluster-dev --nodes=2
```

**Cambiar la configuracion del cluster**

Un perfil es un cluster nuevo

<https://minikube.sigs.k8s.io/docs/commands/config/>

> minikube config set memory 4G -p minikube

Para hacer estos cambios en la configuración se debe borrar y luego iniciar el cluster

```sh
cd .minikube/config
minikube config set memory 4G -p minikube
cat config.json
```

**Cambiar de cluster**

```sh
cd ~/.kube
# Mostrar perfiles
minikube profile

# Cambiar de cluster
minikube profile cluster-dev

# Minukube dashboard
minikube dashboard

# Trabajar con otro runtime

minikube profile list
minikube start --container-runtime=cri-o -p cluster2

# Borrar un cluster

minikube profile list
minikube delete -p cluster2
minikube delete -p cluster-dev
```


**Visual studio code y Kubernetes**

Instalar extensiones de Docker y kubernetes

Si trabajas con WSL conéctate a la extensión

[Work in Windows Subsystem for Linux with Visual Studio Code](https://code.visualstudio.com/docs/remote/wsl-tutorial)

[Developing in the Windows Subsystem for Linux with Visual Studio Code](https://code.visualstudio.com/docs/remote/wsl)

Recordar el directorio **.kube** y el fichero config, allí están los clúster y conexiones locales, sus contextos y demás.

**PODS**

Son el objeto más básico en kubernetes, es un envoltorio de contenedores que agrega una funcionalidad

El pod tiene una ip, direcciones, puertos, hostmnames, sockets, memoria, volumentes, etc.

El pod se despliega en un nodo del cluster, puntualmente en los nodos workers.

Los pods son stateless(no tienen estado) igual que los contenedores.

**Múltiples contenedores en PODS**

Los contendores y kubernetes están basados en el modelo de microservicios, cuando en un pod ponemos varios componentes que se supone debo tener aislados, rompo con ese modelo.

¿De veras queremos poner todo en un mismo sitio?

Lo que queremos es que todo sea independiente.

El ciclo de vida de un componente front alojado en un servidor apache web por ejemplo, es diferente al ciclo de vida de una DB mysql.

Si quiero hacer una actualización y no esta independiente debo parar todo, lo mismo pasa con los backups, rebotes, etc.

El pod tiene una sola dirección IP proporcionada por el cluster, a donde debo apuntar si tengo 3 contenedores en un pod.

¿Cuando debo tener dos contenedores en un pod? Cuando las aplicaciones están intrínsecamente unidas es un ejemplo.

**Primer POD**

Método imperativo: Trabajar con los objetos pasando parámetros

Método declarativo: Se usa fichero manifest con características del objeto y estado que queremos tener.

```sh 
kubectl run nginx1 –image=nginx
kubectl get pods -o wide
kubectl describe <resource>/<name\_resource>

# Logs y modificacion del contenido de un pod**

kubectl run apache1 --image=httpd --port=8080
kubectl run apache1 --image=httpd --port=8080
kubelctl logs apache

# ver logs y esperar en consola los siguientes

kubectl logs -f apache
kubectl logs -f apache --tail=30

# Entrar de manera interactive al pod y actualizar e instalar cosas**

kubectl exec apache -it bash
wget localhost
apt-get update
apt-get install wget
wget localhost

# Probar el POD con proxy
# Los pods se pueden probar con el proxy a través del navegador web

kubectl proxy
[127.0.0.1:8001](http://127.0.0.1:8001/)
[127.0.0.1:8001/api/v1/namespaces/default/pods](http://127.0.0.1:8001/api/v1/namespaces/default/pods)
[127.0.0.1:8001/api/v1/namespaces/default/pods/apache/proxy/](http://127.0.0.1:8001/api/v1/namespaces/default/pods/apache/proxy/)
<http://127.0.0.1:8001/api/v1/namespaces/default/pods/nginx1/proxy/>

# Pod con servicio
# El Puerto 80 es del conedor

kubectl expose pod nginx1 --port=80 --name=nginx-service --type=LoadBalancer
kubectl get services

# Port forwarding
# Me sirve para probar el pod sin crear servicios, con eso por medio del navegador dirijo el trafico hacia el pod del cluster por medio del localhost y algún puerto que escoja

kubectl port-forward nginx1 9999:80
<http://localhost:9999/>

# Ver los pods desde un nodo del cluster

minikube ssh
docker ps
```

## LABELS

```sh
kubectl apply -f tomcat.yml
kubectl get pods -o wide
kubectl get pods --show-labels
kubectl get pods --show-labels -L estado
kubectl get pods --show-labels -L estado,responsible
kubectl describe pod/tomcat

# Agregar label a un pod

kubectl label pods/apache estado=producción
kubectl label pods/apache responsable=pedro


# SELECTORES
# Son condiciones que uso para localizar determinadas etiquetas. Sirve para buscar componentes a lo largo de nuestro cluster
# Buscar por selector

kubectl get pods --show-labels -l estado=desarrollo
kubectl get pods --show-labels -l estado=test
kubectl get pods --show-labels -l estado!=test
kubectl get pods --show-labels -l 'estado in(produccion,test)'
kubectl get pods --show-labels -l 'estado notin(produccion,test)'

# Anotaciones
# Las anotaciones son similares a las label, pero a manera de documentación para nuestros componentes.
kubectl get pod tomcat2 -o jsonpath={.metadata.annotations}
```


## Workloads y controllers

Workload: algo que uso para desplegar contenedores, el mas básico es el pod.

Los deployment envuelve los pod y le dan características de update y rollback, también comprobar que todo funcione correctamente.

Los replica set hacen el escalado de los pods de acuerdo a lo que indica el cluster, los replication controller han reemplazado el replica set.

Stateful set, es un objeto que gestiona el despliegue y escalado de los pod

Daemon set

Jobs, componente que crear uno o varios pods y se aseguran que ellos se terminen satisfactoriamente.

Cron job, hace lo mismo que el job, pero de forma planificada

## Deployment

Lo más básico que podemos tener es un contenedor, pero este no puede estar solo para interactuar con kubernetes, debe estar envuelto en un pod. 

Hay cosas que los pods no pueden hacer por si mismos, por ej ellos no escalan solitos, tampoco se recuperan ante caídas, no son buenos para hacer updates, rollbacks complicados.

Por eso los pods se ponen dentro de los deployments, este permite hacer updates y rollbacks, tiene recuperación ante caidas y permite escalar.

Cuando creo un deployment automáticamente se crear un replicaset, que este es el que tiene la funcionalidad de recuperación ante caidas y el escalamiento de los pods

Cuando crearmos un deploy y lo consultamos tiene ready y available, la diferencia es que ready es cuando el pod se ha creado y available es que esta funcionando.

```sh
# Create deployment

kubectl create deployment apache --image=httpd

# ver deployment
kubectl get deploy

# ver replica set

kubectl get rs
kubectl get pods

# Informacion del deployment

kubectl describe deploy apache
kubectl get deploy apache -o yaml
kubectl apply -f deploy_nginx.yaml
kubectl describe pod/nginx-d-7bddc944f7-jnn2p
kubectl get rs -o wide
kubectl get deploy -o wide
kubectl get pods
kubectl get pods -l app=nginx
kubectl get pods -l app=nginx -L app

kubectl apply -f deply\_nginx.yaml

kubectl get deploy,pods,rs -l app=nginx

# Editar comportamiento de los deployment de manera dinamica

kubectl edit deploy nginx-d -o yaml

# Escalar manualmente un deployment

kubectl scale deploy nginx-d --replicas=5
kubectl get deploy
```

## Services

Permite que los despliegues convivan con el mundo exterior.

A los pod se les pone una ip para acceder dentro del contenedor

Imaginar que tengo un deploy con cuatro pods, además tengo una aplicación web cliente que quiere conectarse a nuestros pods, problemas en este caso:

- No hay Ip fija
- No hay un nombre fijo (DNS)
- No hay un puerto fijo

El servicio es un componente intermedio que actúa entre el cliente y el pod, el lo que hace es un mapeo de los pods de un deployment y los ofrece a un cliente, por medio de un loadBalancer simple.

Con el service tenemos IP fija, nombre fijo y puerto fijo.


Hay varios tipos de servicio

- ClusterIp: accesible solo desde dentro del cluster
- NodePort: Accesible desde fuera del cluster
- LoadBalancer: Accesible desde fuera del cluster, esta integrado con loadbalancer de terceros como AWS, GCP o Azure

¿Como el servicio detecta los pods que se van creando?

El servicio usa los labels, el servicio usa un selector (el selector es como un query)

```sh
kubectl create deployment apache1 --image=httpd

kubectl get all

kubectl expose deploy apache1 --port=80 --type=NodePort --name=apache-service

kubectl get svc

minikube ip

minikube service list

kubectl describe svc/apache-service

kubectl edit svc/apache-service -o yaml

KUBE\_EDITOR="nano" kubectl edit svc/apache-service -o yaml
```
Minkikube tiene un problema y a veces no escucha por el puerto que expone minikube entonces tenemos que probar con el localhost y consultar la lista de servicios de minikube



## Configuración

```sh
# Asignar ambiente

aws eks update-kubeconfig --name <cluster_name>-dev --region us-east-1
aws eks update-kubeconfig --name <cluster_name>-qa --region us-east-1
aws eks update-kubeconfig --name <cluster_name>-pdn --region us-east-1

# Logs
## Todos los pods al mismo tiempo
kubectl logs -n name_namespace-pdn -f -l pod=ss-ms-device-control-pod --max-log-requests=20

## Descargar logs
kubectl logs -n name_namespace-pdn {nombre-pod} > {nombre del log}.log

# Pods

# listar pods 
kubectl get pod -n name_namespace-qa`

# listar pods con autoescalamiento y ips
kubectl get pod -n name_namespace-qa -o wide -w`

# listar pods filtrando por un label
kubectl get pod -n name_namespace-qa -l pod=fa-ms-functional-adapter-pod`

#listar pods filtrando por un label con consumo de memoria y CPU
kubectl top pod -n name_namespace-qa -l pod=fa-ms-functional-adapter-pod`

#borrar pods de un microservicio
kubectl delete pod -n name_namespace-qa -l pod=ms-authentication-pod`

# Obtener información del pod
kubectl describe pod -n name_namespace-qa -l pod=ms-authentication-pod`

# Obtener los logs de todos los pods
kubectl logs -n name_namespace-qa -f -l app=ms-vinculation-pod --max-log-requests=20`

# Obtener la información del configmap de un microservicio
kubectl get configmap -n name_namespace-pdn -o json ss-ms-device-control-configmap`
``
