
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