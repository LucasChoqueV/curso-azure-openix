# Crear cuenta en azure devops
1. Ir al link https://azure.microsoft.com/es-es/products/devops
2. Ingresar con la cuenta de microsoft
3. Crear nueva organizacion
4. Crear un nuevo proyecto
5. Proyecto privado
6. Work item process: Scrum
## Subir proyecto a Azure Repo
1. Vamos a "Repos"
2. Clonamos el proyecto con SSH
3. Copias el proyecto de ejemplo en el repo
4. Creamos un manifest con el depoyment y el service de kubernetes
5. Validar que la imagen de docker se cree bien
6. Validar que el manifiesto de kubernetes se levante bien
7. Validar en Repos que el proyecto se haya subido.
## Crear un build pipeline
1. Ir a "Pipelines"
2. Click en "Create Pipeline"
3. Click en "Use the classic editor"
4. Elegir "Azure Repo"
5. Click en "Empty Job"
6. Le damos un nombre al pipeline
7. En "Pipeline" elegimos "ubuntu-latest"
8. Le damos nombre al agent
9. Click en "+" y agregamos una tarea de docker
10. Task version: 1.* para usar la conexion con subscription 
11. Display name: build image
12. Command: build
13. Dockerfile: buscamos en el explorador de archivos
14. Image name: openixtestingacr/dev/app:latest
15. Solo guardamos y vamos a **Crear una conexion con Azure Portal**
16. Luego volver al pipeline y agregar la conexion, guardamos y encolamos.
17. Duplicamos la tarea pero ahora haciendo push
18. Activar el continouse integration.
## Crear un build deployment
1. Primero modificamos el manifest 
	- Eliminar imagePullPolicy
	- El puerto del service ponerlo en 80
	- Modificar la imagen para que apunte al ACR
2. Ir a "Releases" y click en "New pipeline"
3. Le damos un nombre Stage name: DEV
4. Agregamos un artifact de tipo Azure Repo
5. Click en "1 Job, 0 task"
6. En el agent job le ponemos nombre y seleccionamos "Azure pipelines" y "ubuntu-latest"
7. Agreamos una task de kubernetes y completamos los campos y le damos a guardar
8. Volvemos a release y creamos un release
9. habilitamos el continouse deployment y hacemos un cambio para testear todo
### Crear una conexion con Azure Portal
1. Click en "Project settings", "Service connections", "Create service connection"
2. Elegimos "Azure Resource Manager" y "Service principal (manual)
3. Vamos a Azure portal y buscamos "Active Directory"
4. Vamos a "App registrations" y agregamos una nueva
5. Vamos a la subscription y creamos un rol en IAM, "Add Role Assigment"
6. Damos rol de "Owner" no recomendando para todos los grupos
7. Buscamos el service principal creado y guardamos el rol
8. Volvemos al pipeline