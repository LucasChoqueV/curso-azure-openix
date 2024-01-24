
# Usar el Cluster de kubernetes con Docker Desktop
Al tener Docker Desktop tambien tenemos un Cluster de Kubernetes en donde podemos hacer pruebas locales, para habilitar el cluster vamos a **Settings** -> **Kubernetes** y habilitamos "Enable Kubernetes"
## Descargar kubectl
kubectl es el cliente de kubernetes que necesitamos para interactuar con la API.
https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
1. Verificamos la instalacion `kubectl version --short`
2. Listar los comandos de configuracion `kubectl config`
3. Listar los context `kubectl config get-contexts`
4. Setear el context de docker `kubectl config set-context docker-desktop`
5. Listar los clusters `kubectl config get-clusters`
6. Setear el cluster de docker destop `kubectl config set-cluster docker-desktop`
7. Ver el namespace `kubectl get namespace`
8. Ver los nodos `kubectl get nodes`
## Practica
### Pods
1. Creamos un archivo `01-simple-pod.yml` con este contenido
```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-label
spec:
  containers:
  - name: my-container
    image: example-project
    imagePullPolicy: Never
```
2. Nos movemos a la carpeta del archivo y ejecutamos `kubectl apply -f 01-simple-pod.yml`
3. Validamos con `kubectl get pods`
4. Ver mas contenido del pod `kubectl describe pod my-pod`
5. Ver logs `kubectl logs my-pod`
6. Entrar al container `kubectl exec -it my-pod sh`
7. Eliminar el pod `kubectl delete pod my-pod`
#### Referencias.
- https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.29/#pod-v1-core
- https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.29/#pod-v1-core
### Deployments
1. Creamos un archivo `02-simple-deployment.yml` con este contenido
```yaml
apiVersion: apps/v1
kind: Deployment 
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:  
    metadata:
      name: my-pod
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: example-project
          imagePullPolicy: Never
```
2. Nos movemos a la carpeta del archivo y ejecutamos `kubectl apply -f 2-simple-deployment.yml`
3. Validamos con `kubectl get deployments`
4. Validamos con `kubectl get replicaset`
5. Validamos con `kubectl get pods`
6. Entramos a un pod con `kubectl exec -it <pod> sh`
7. Eliminamos un pod con `kubectl delete pod <pod>`
8. Eliminamos el deployment `kubectl delete deploy my-deployment`
#### Referencias.
- https://kubernetes.io/es/docs/concepts/workloads/controllers/deployment/
- https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.29/#deployment-v1-apps
### Services
1. Creamos un archivo `03-simple-service.yml` con este contenido
```yaml
apiVersion: v1
kind: Service 
metadata:
  name: my-lb-service
spec:
  type: LoadBalancer # ClusterIp, # NodePort
  selector:
    app: my-app
  ports: 
    - name: http
      port: 8001 # Service Port
      targetPort: 80 # Container Port
```
2. Nos movemos a la carpeta del archivo y ejecutamos `kubectl apply -f 03-simple-service.yml`
3. Validamos con `kubectl get service`
4. Entramos a la aplicacion con `http://localhost:8001`
#### Referencias.
- https://kubernetes.io/es/docs/concepts/services-networking/service/