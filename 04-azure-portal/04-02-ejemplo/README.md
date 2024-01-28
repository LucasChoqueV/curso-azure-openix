# Crear cuenta
1. Seguir el tutorial de aqui: https://www.youtube.com/watch?v=ZNTdN2FO0bs
# Crear subscripcion
1. Buscar "Subscriptions"
2. Click en "Add"
3. Crear "Billing Profile" si es que no existe uno por defecto
4. Agregar nombre a la subscription: ca-dev-01-ss
# Crear resource group
1. Buscar "Resource group"
2. Click en "Add"
3. Seleccionar la subscription previamente creada
4. Agregar nombre al resource group: ca-dev-01-rg 
# Crear Azure Container Registry
1. Buscar "Container Registry"
2. Click en "Create"
3. Seleccionar la subscription y el resource group
4. Agregar nombre al container: cadev01acr
5. Pricing plan: Basic
6. Click en "Create"
# Crear Azure Kubernetes Service
Antes de crear el cluster es mejor esperar a ver la seccion **Azure DevOps** y luego volver aqui para crear el cluster, ya que Kubernetes Service en Azure no entra en la capa gratuita y la idea es levantar el cluster el menor tiempo posible para evitar gastos.
1. Buscar "Kubernetes Service"
2. Click en "Create" y "Create a Kubernetes cluster"
- Basics Tab
	- Seleccionar la subscription y resource group
	- Cluster preset configuration: Dev/Test
	- Kubernetes cluster name: ca-dev-01-cluster
	- Region: East US
	- Availability zones: None
	- AKS pricing tier: Free
	- Kubernetes version: 1.27.7
	- Automatic upgrade: Enabled with patch
	- Authentication and Authorization: Local Accounts with kubernetes RBAC
- Node Pools
	- Editar el nodepool creado automaticamente
	- Node size: elegir el standard b2s
	- Scale method: manual
	- node count: 1
	- Max pods per node: 50
- Networking no modificar
- Integrations
	- Azure Container Registry: Seleccionar el ACR nuestro
3. Click en "Review + create"