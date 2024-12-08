# Arquitectura física:
Componentes:

## VPC
- 2 subnets privadas
- 2 subnets pública
- Nat gateway
- Internet Gateway


Nota: La configuración de la VPC y los recursos de red asociados, como subnets, tablas de enrutamiento, gateways, y otros, se realiza de forma manual según las necesidades específicas de la solución. Se recomienda, como mínimo, configurar al menos dos subnets privadas y dos subnets públicas distribuidas en diferentes zonas de disponibilidad (AZ) para garantizar alta disponibilidad, redundancia y una separación lógica de los recursos según sus niveles de acceso y seguridad.

## DocumentDB
Base de datos compatible con MongoDB gestionada por AWS.
## DMS
Servicio de AWS encargado de replicar datos entre MongoDB y DocumentDB
## EC2
Instancia de cómputo donde se ejecutan servicios de replicación y procesamiento relacionados con la arquitectura.
## AWS Lambda Functions:
- Lambda Start Replication: Inicia el proceso de replicación entre DocumentDB y S3, gestionando permisos y configuraciones necesarias.
- Lambda Restore Replication: Orquesta la restauración de datos, configurando permisos de solo lectura y aprovisionando servicios en EC2 para procesar operaciones.
- Lambda Clean Replication: Gestiona la limpieza de datos obsoletos, cerrando los ChangeStreams en DocumentDB, eliminando archivos BSON en S3 y apagando EC2 tras completar las tareas.
S3

## Secret Manager
Almacena y gestiona las credenciales del usuario maestro de DocumentDB


# Arquitecutra física
![arquitectura-física](./archi.png)