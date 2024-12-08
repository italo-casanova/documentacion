# **Despliegue de la solución**

## **Pre-requisitos:**

### **1. Configuración de la VPC**
- **Crear una VPC** con las siguientes características:
  - **Subnets privadas**: Crear **3 subnets privadas** en diferentes zonas de disponibilidad.
  - **Subnets públicas**: Crear **3 subnets públicas** en diferentes zonas de disponibilidad.
  - Configurar rutas y tablas necesarias para permitir comunicación entre subnets públicas y privadas.
  - **Conexión al MongoDB on-premise**:  
    La VPC debe incluir un **túnel VPN** o **Direct Connect** para establecer una conexión privada con el MongoDB on-premise.

### **2. Configuración de Secret Manager**

- **Crear un secreto en AWS Secret Manager** que almacene las credenciales del usuario maestro del **DocumentDB**.
- La estructura del secreto debe ser:

```json
{
  "username": "<username>",
  "password": "<password>"
}
```
- Este secreto será utilizado para la configuración del clúster de DocumentDB y la integración con AWS DMS.

### **3. Configuración del MongoDB On-Premise**

#### **Creación de Usuario con Permisos Requeridos**
Crear un usuario en el **MongoDB on-premise** que cuente con los siguientes permisos sobre las bases de datos y colecciones que se van a replicar:

1. Operaciones:  
   - `"write"`, `"find"`, `"changeStream"`.

2. Rol:  
   - `"read"`.

- Para más información sobre los permisos, revisar la sección:  
  [Permissions needed when using MongoDB as a source for AWS DMS](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Source.MongoDB.html).

---

#### **Configurar el Replica Set del MongoDB On-Premise**
1. Asegurarse de que el **MongoDB on-premise** esté configurado como un **replica set**.
2. Verificar y habilitar las configuraciones necesarias para el **Change Data Capture (CDC)**.
3. Para más detalles, revisar la sección:  
   [Configuring a MongoDB replica set for CDC](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Source.MongoDB.html#CHAP_Source.MongoDB.CDC).


## **Configuración del archivo `env.yml` para desplegar la solución con Jenkins**

- **Link del archivo en develop**:  
  [env.yml en Bitbucket](https://bitbucket.org/losandespe/jenkins-pipelines/src/main/Develop/Domain5/apibus-always/env.yml)

---

### **Configuración de DocumentDB**

#### **Parameter Group**
- **`docdb_cluster_parameter_group_family`** (`String`):  
  Ingresar familia del grupo de parámetros, dejar valor por defecto `"docdb4.0"`.
- **`docdb_cluster_parameter_group_name`** (`String`):  
  Ingresar el nombre deseado del grupo de parámetros.

---

#### **DocumentDB**
- **`docdb_master_user_secret_name`** (`String`):  
  Ingresar el nombre del secreto que almacena las credenciales (usuario y contraseña) del **DocumentDB** (debe existir previamente).
- **`docdb_subnet_group_name`** (`String`):  
  Ingresar el nombre deseado para el grupo de subredes.
- **`docdb_subnets_ids`** (`List[String]`):  
  Ingresar los **IDs** de las subredes privadas deseadas.
#### **Cluster Replication**

- **`cluster_identifier`** (`String`):  
  Ingresar el identificador deseado para el clúster.

- **`engine_version`** (`String`):  
  Dejar valor por defecto `"4.0.0"`.

- **`preferred_backup_window`** (`String`):  
  Ingresar ventana de tiempo en la que el DocumentDB esté en menor uso, ejemplo: `"02:00-03:00"`.

- **`backup_retention_period`** (`Integer`):  
  Ingresar el periodo de retención deseado en días.

- **`availability_zones`** (`List[String]`):  
  Ingresar las zonas de disponibilidad que coincidan con las subredes privadas.

- **`apply_immediately`** (`Boolean`):  
  Dejar valor por defecto `true` para el primer despliegue.

- **`preferred_maintenance_window`** (`String`):  
  Ingresar ventana de tiempo en la que el DocumentDB esté en menor uso, ejemplo: `"sun:04:00-sun:05:00"`.

---

- **`deletion_protections`** (`Boolean`):  
  Configurar como `true` en producción para evitar eliminación accidental.

- **`skip_final_snapshot`** (`Boolean`):  
  Ingresar `true` para omitir el snapshot final o `false` si desea crearlo.

- **`port`** (`Integer`):  
  Ingresar el puerto deseado, el valor por defecto para MongoDB es `27017`.


#### **Cluster Instance**

- **`docdb_cluster_instance_class`** (`String`):  
  Ingresar el tipo de instancia adecuada según el uso del **DocumentDB**.

- **`docdb_cluster_instance_count`** (`Integer`):  
  Ingresar la cantidad deseada de instancias del clúster, recomendación: `3`.

### **Grupos de Seguridad**

#### **DocumentDB Security Group**
- **`docdb_sg_name`** (`String`):  
  Ingresar el nombre deseado para el grupo de seguridad.

- **`docdb_sg_description`** (`String`):  
  Ingresar la descripción deseada para el grupo de seguridad.

- **`docdb_ingress_rules`** (`List[Object]`):  
  Configurar las reglas para permitir conexión TCP al puerto del **DocumentDB** desde **DMS**, **Lambdas** y **EC2**.
  - **`from_port`** (`Integer`): Ingresar el puerto de inicio.
  - **`to_port`** (`Integer`): Ingresar el puerto final.
  - **`protocol`** (`String`): Ingresar el protocolo, generalmente `"TCP"`.
  - **`cidr_blocks`** (`List[String]`): Ingresar los rangos CIDR permitidos.

- **`docdb_egress_rules`** (`List[Object]`):  
  Dejar valor por defecto `[]`.

---

#### **Lambda Security Group**
- **`lambda_sg_name`** (`String`):  
  Ingresar el nombre deseado para el grupo de seguridad.

- **`lambda_sg_description`** (`String`):  
  Ingresar la descripción deseada para el grupo de seguridad.

- **`lambda_ingress_rules`** (`List[Object]`):  
  Dejar valor por defecto `[]`.

- **`lambda_egress_rules`** (`List[Object]`):  
  Configurar las reglas de salida para conectar **Lambdas** a **DocumentDB** (puerto configurado) y **EC2** (puerto 22).
---
### **Secrets**
- **`dms_secret_user_replication_name`** (`String`):  
  Ingresar el nombre deseado para el secreto de replicación.

- **`dms_user_replication_username`** (`String`):  
  Ingresar el nombre de usuario deseado para replicación.

---

### **Roles y Políticas**

#### **Lambda para crear usuario**
- **`iam_policy_lambda_access_docdb_name`** (`String`):  
  Ingresar el nombre deseado de la política IAM.

- **`iam_role_lambda_access_docdb_name`** (`String`):  
  Ingresar el nombre deseado del rol IAM.

- **`lambda_subnet_ids`** (`List[String]`):  
  Ingresar los **IDs** de las subredes privadas.

- **`lambda_create_user_db_function_name`** (`String`):  
  Ingresar el nombre deseado para la función Lambda.
---
### **Configuración de DMS**

#### **General**
- **`dms_cloudwatch_role_name`** (`String`):  
  Ingresar el nombre deseado para el rol de **CloudWatch**.

- **`dms_vpc_role_name`** (`String`):  
  Ingresar el nombre deseado para el rol de la VPC.

---

#### **Endpoints**
- **`mongodb_onpremise_username`** (`String`):  
  Ingresar el nombre de usuario de **MongoDB on-premise**.

- **`mongodb_onpremise_password`** (`String`):  
  Ingresar la contraseña del usuario de **MongoDB on-premise**.

- **`kms_key_arn`** (`String`):  
  Ingresar el ARN de la clave **KMS** gestionada por AWS para **DMS**.

- **`dms_target_endpoint_engine_name`** (`String`):  
  Dejar valor por defecto `"docdb"`.

- **`dms_endpoint_mongodb`** (`Object`):  
  Configurar el endpoint para **MongoDB on-premise**.
  - **`endpoint_id`** (`String`): Ingresar el nombre deseado para el endpoint.
  - **`server_name`** (`String`): Ingresar la IP o dominio del MongoDB.
  - **`database_name`** (`String`): Dejar valor por defecto `""` para conectar con todas las bases de datos.
  - **`port`** (`Integer`): Ingresar el puerto del MongoDB on-premise.

- **`dms_endpoints_docdb`** (`List[Object]`):  
  Ingresar lista de endpoints para **DocumentDB**.
  - **`endpoint_id`** (`String`): Ingresar el nombre deseado, debe coincidir con `dmsReplicationTasks.json`.
  - **`database_name`** (`String`): Ingresar el nombre de la base de datos de MongoDB que se desea migrar.


### **Subnet Group**

- **`replication_subnet_group_id`** (`String`):  
  Ingresar el nombre deseado para el grupo de subredes de replicación.

- **`subnet_ids`** (`List[String]`):  
  Ingresar **IDs** de las subredes privadas.

- **`replication_subnet_group_description`** (`String`):  
  Ingresar la descripción deseada para el grupo.

---

### **Instancia de Replicación**

- **`replication_instance_id`** (`String`):  
  Ingresar el nombre deseado para la instancia de replicación.

- **`allocated_storage`** (`Integer`):  
  Ingresar el tamaño de almacenamiento deseado en GB (mínimo 50).

- **`allow_major_version_upgrade`** (`Boolean`):  
  Ingresar `true` o `false` según sea necesario.

- **`apply_immediately`** (`Boolean`):  
  Ingresar `true` o `false` según sea necesario.

- **`auto_minor_version_upgrade`** (`Boolean`):  
  Ingresar `true` para activar actualizaciones automáticas menores.

- **`availability_zone`** (`String`):  
  Ingresar una zona de disponibilidad que coincida con las subredes privadas.

- **`engine_version`** (`String`):  
  Dejar valor por defecto `"3.5.2"`.

- **`multi_az`** (`Boolean`):  
  Ingresar `true` para habilitar Multi-AZ o `false` para desactivarlo.

- **`publicly_accessible`** (`Boolean`):  
  Dejar valor por defecto `false`.

- **`replication_instance_class`** (`String`):  
  Ingresar el tipo de instancia adecuada según los datos de **MongoDB**.

- **`preferred_maintenance_window`** (`String`):  
  Ingresar ventana de mantenimiento, ejemplo: `"Mon:03:00-Mon:05:00"`.

---

### **Tareas de Replicación**

- **`dms_replication_task_migration_type`** (`String`):  
  Dejar valor por defecto `"full-load-and-cdc"`.

- **`dms_start_replication_task`** (`String`):  
  Ingresar el nombre deseado para iniciar replicación.


### **Security Group del DMS**
- **`dms_sg_name`** (`String`):  
  Ingresar el nombre deseado para el grupo de seguridad.

- **`dms_sg_description`** (`String`):  
  Ingresar la descripción deseada para el grupo.

- **`dms_ingress_rules`** (`List[Object]`):  
  Dejar valor por defecto `[]`.

- **`dms_egress_rules`** (`List[Object]`):  
  Configurar reglas para conexión TCP con **MongoDB** y **DocumentDB**.

---

### **S3**
- **`s3_bucket_name`** (`String`):  
  Ingresar el nombre deseado para el bucket.

---

### **Instancia EC2 de Replicación**

#### **Configuración de la Instancia**
- **`iam_policy_ec2_name`** (`String`):  
  Ingresar el nombre deseado para la política IAM.

- **`iam_role_ec2_name`** (`String`):  
  Ingresar el nombre deseado para el rol IAM.

- **`ec2_name`** (`String`):  
  Ingresar el nombre deseado para la instancia EC2.

- **`ec2_key_pair_name`** (`String`):  
  Ingresar el nombre deseado para el par de claves.

- **`ec2_instance_type`** (`String`):  
  Ingresar el tipo de instancia deseada, recomendado: `"t3.large"`.

- **`ec2_subnet_id`** (`String`):  
  Ingresar el ID de la subred privada.

- **`ec2_volume_size`** (`Integer`):  
  Ingresar el tamaño de almacenamiento en GB, recomendado: `50GB`.

---

#### **Security Group del EC2**
- **`ec2_sg_name`** (`String`):  
  Ingresar el nombre deseado para el grupo de seguridad.

- **`ec2_sg_description`** (`String`):  
  Ingresar la descripción deseada.

- **`ec2_ingress_rules`** (`List[Object]`):  
  Configurar reglas para abrir el puerto 22 si es necesario.

- **`ec2_egress_rules`** (`List[Object]`):  
  Configurar reglas de salida, valor predeterminado:  
  - `from_port = 0`, `to_port = 0`, `protocol = "-1"`, `cidr_blocks = ["0.0.0.0/0"]`.


### **Lambdas para Replicación**

- **`iam_role_lambda_repl_name`** (`String`):  
  Ingresar el nombre deseado para el rol IAM.

- **`iam_policy_lambda_access_ec2_name`** (`String`):  
  Ingresar el nombre deseado para la política IAM con acceso a EC2.

- **`iam_policy_lambda_access_s3_name`** (`String`):  
  Ingresar el nombre deseado para la política IAM con acceso a S3.

- **`lambda_start_replication_function_name`** (`String`):  
  Ingresar el nombre deseado para la función Lambda de inicio de replicación.

- **`lambda_restore_replication_function_name`** (`String`):  
  Ingresar el nombre deseado para la función Lambda de restauración de replicación.

- **`lambda_clean_replication_function_name`** (`String`):  
  Ingresar el nombre deseado para la función Lambda de limpieza de replicación.


## **Configuración del archivo `dmsReplicationTask.json`**

El archivo `dmsReplicationTask.json` configura las tareas de replicación, especificando qué colecciones y bases de datos se van a replicar.

---

### **Estructura de una tarea de replicación**

```json
{
  "task_id": "cobranza-1",
  "table-mappings": {
    "rules": [
      {
        "rule-type": "selection",
        "rule-id": "1",
        "rule-name": "cobranza-1",
        "object-locator": {
          "schema-name": "Si_DbClaCobranza",
          "table-name": "OfertaAsignada"
        },
        "rule-action": "include",
        "filters": []
      }
    ]
  },
  "target_endpoint_key": "pagos"
}
```


**Explicación de cada campo**

- **`task_id`**:  
  Identificador único de la tarea de migración o replicación.

- **`table-mappings`**:  
  Contiene las reglas que definen cómo se deben seleccionar las tablas de la base de datos de origen y cómo se deben mapear a la base de datos de destino durante el proceso de migración.
  - **`rules`**:  
    Un conjunto de reglas que determinan qué tablas de la base de datos de origen se deben incluir o excluir en la migración, así como otros aspectos relacionados con la transformación y selección de los datos.
    - **`rule-type`**:  
      Especifica el tipo de la regla, como la selección de tablas para incluir o excluir, o transformaciones de los datos.
    - **`rule-id`**:  
      Identificador único para cada regla dentro del conjunto de reglas.
    - **`rule-name`**:  
      Nombre descriptivo de la regla.
    - **`object-locator`**:  
      Define la ubicación del objeto (en este caso, la colección) dentro de la base de datos de origen, indicando el esquema y el nombre de la tabla que se está seleccionando o excluyendo.
      - **`schema-name`**:  
        El nombre del esquema dentro de la base de datos de origen donde se encuentra la tabla que se selecciona o se excluye.
      - **`table-name`**:  
        El nombre de la tabla dentro del esquema que se selecciona o se excluye en la regla de migración.
    - **`rule-action`**:  
      Especifica la acción que debe realizarse con la tabla seleccionada, como incluirla en la migración o excluirla.
    - **`filters`**:  
      Lista de filtros que se pueden aplicar a las filas de las tablas seleccionadas, para limitar los datos migrados según ciertos criterios. Si está vacío, no se aplica ningún filtro.

- **`target_endpoint_key`**:  
  Identificador del endpoint de destino donde se migrarán los datos desde la base de datos de origen.

**Valores**

- **`task_id`**:  
  Ingresar nombre deseado.

- **`table-mappings`**:
  - **`rules`**:
    - **`rule-type`**:  
      Ingresar valor: `"selection"`.
    - **`rule-id`**:  
      Ingresar ID deseado.
    - **`rule-name`**:  
      Ingresar nombre deseado.
    - **`object-locator`**:
      - **`schema-name`**:  
        Ingresar nombre de la base de datos de las colecciones que desea migrar en esta tarea de replicación.
      - **`table-name`**:  
        Ingresar nombre de la colección que desea replicar.
    - **`rule-action`**:  
      Ingresar valor: `"include"`.
    - **`filters`**:  
      Ingresar valor: `[]`.

- **`target_endpoint_key`**:  
  Ingresar el identificador del endpoint.

Ejemplo de configuración:
```json
[
    {
    "task_id": "task_id",
    "table-mappings": {
      "rules": [
        {
          "rule-type": "selection",
          "rule-id": "rule_id_1",
          "rule-name": "rule_name_1",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_1"
          },
          "rule-action": "include",
          "filters": []
        },
        {
          "rule-type": "selection",
          "rule-id": "rule_id_2",
          "rule-name": "rule_name_2",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_2"
          },
          "rule-action": "include",
          "filters": []
        }
      ]
    },
    "target_endpoint_key": "nuevoEndpointId"
    },
  ...
  ...
  ...
]
```
### **Recomendaciones**

- Aegurarse de que las subnets tienen comunicación entre sí
- En el documentDB verificar que las subnets ids coincidan con las AZ elegidas.




#  Casos de Uso

### Iniciar las tareas de replicacion


### 1. Actualizar el usuario de docdb que usan los target endpoints para la replicacion
Los target endpoint usan el usuario replicacion que fue creado por la lambda crear usuario, las credenciales de este usuario son almacenadas en un secreto de secret manager, un secreto que es una estructura: llave-valor con llaves: username y password, los target endpoints usan el arn del secreto internamente para acceder al secreto por lo tanto siempre habrá que usar ese secreto, pero aún así se puede actualizar el usuario y la contraseña:
>  #### Actualizar el usuario y contraseña

Pre condiciones:
- Las tareas deben estar detenidas, puede pausarlas cambiando el valor de la variable dms_start_replicacion_tasks a false y correrlo


Procedimientos para actualizar este usuario:
- Cambiar el valor del username del usuario de replicación en la variable dms_user_replication_username, esto hará que el componente secret-docdb detecte el cambio y al momento de correr el código generará una nueva contraseña mediante el componente random_password de terraform.
- Una vez hayan corrido el paso anterior, ahora deben cambiar el valor de dms_start_replication_tasks a true para reanudar las tareas y correrlo de nuevo

Post condiciones:
- Username y password actualizado
- Tareas replicando
- El usuario anterior sigue existiendo en el docdb (eliminarlo mediante una conexion ssh o rpd mediante el usuario master del docdb)
> #### Solo actualizar la contraseña:
  Para cambiar la contraseña debería crear una lambda que tenga permisos de ejecutarse dentro de esa VPC, acceder al secreto del usuario de replicación y al docdb de destino y ejecutar el código necesario para actualizaro, las pre condiciones son iguales que para el primer caso, deben pausar las tareas,





### 2. Creación de una nueva base de datos y colecciones

Las tareas de replicación, de ahora en adelante solo tareas, y las bases de datos junto a sus colecciones están estrechamente relacionadas mediante el archivo dmsReplicationTask.json, la creación y destrucción de estas es bidireccional, si un conjunto de colecciones se crea/destruye su tarea asociada también, la creación/destrucción de estas se realiza configurando el archivo dmsReplicationTask.json.
Entonces al momento de que se quiere agregar una nueva base de datos, se deberá crear la tarea asociada a la replicación de esa base de datos y ese conjunto de colecciones.

Pre condiciones:
- La base de datos y sus colecciones deben existir en el mongodb on-premise.
- Las tareas deben estar pausadas, puede pausarla cambiando el valor de la variable dms_start_replication_task a false y correrlo.
- Asegurarse que el usuario del MongoDB on-premise que usa el DMS tenga los mismos permisos sobre las nuevas bases de datos y colecciones.
Procedimiento:



- Agregar el nuevo target endpoint de la nueva base de datos en la variable  dms_endpoints_docdb
- Los campos que debería llenar son:
> - endpoint_id = "nuevoEnpointId"
> - database_name = "nuevaBaseDatos"

Ejemplo:
```json
 [
    #Nuevo endpoint:
    {
      endpoint_id   = "nuevoEndpointId"
      database_name = "nuevaBaseDatos"
    },
    #Bases de datos ya existentes:
    {
      endpoint_id   = "test-docdb-cuenta-digital"
      database_name = "Si_DbClaCuentaDigital"
    },
    {
      endpoint_id   = "test-docdb-firmas"
      database_name = "Si_DbClaFirmas"
    }.
    ...
    ...
    ...
  ]
```

- Luego modificar el archivo dmsReplicationTask.json  agregando una nueva tarea.

Ejemplo:

> - nombre de la nueva base de datos: nuevaBaseDatos <br>
> - nombre de coleccion 1: coleccion_1 <br>
> - nombre de coleccion 2: coleccion_2 <br>

Leer sección "Inputs > Files" del componente DMS para entender mejor que colocar en los campos task_id, rule-id, rule-name, schema-name, target_endpoint_key, etc.

Debería agregar la siguiente tarea al json con este formato:
```json
[
    {
    "task_id": "task_id",
    "table-mappings": {
      "rules": [
        {
          "rule-type": "selection",
          "rule-id": "rule_id_1",
          "rule-name": "rule_name_1",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_1"
          },
          "rule-action": "include",
          "filters": []
        },
        {
          "rule-type": "selection",
          "rule-id": "rule_id_2",
          "rule-name": "rule_name_2",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_2"
          },
          "rule-action": "include",
          "filters": []
        }
      ]
    },
    "target_endpoint_key": "nuevoEndpointId"
    },
  ...
  ...
  ...
]
```


- Una vez modificado el dmsReplicationTasks.json y cambiar el dms_start_replication_task a true y correrlo


Post-condiciones:
- Base de datos y colecciones creadas en el docdb.
- Tarea de replicación replicando las colecciones establecidas.

### 3. Eliminación de una base de datos
Pre condiciones:
- Las tareas deben estar pausadas, puede pausarla cambiando el valor de la variable dms_start_replication_task a false y correrlo

Procedimiento:

- Ir al archivo dmsReplicationTask.json y eliminar todas las tareas asociadas a esa base de datos, es decir todas las tareas que tengan su campo schema_name: "Nombre de la base de datos que quiere borrar"
- Borrar en la variable dms_endpoints_docdb el endpoint cuyo campo database_name coincida con el nombre de la base de datos que se quiere borrar y correrlo
- Cambiar el campo dms_start_replication_task a true y correrlo

Nota:El lambda solo borrará la base de datos si se encuentra en el entorno de qa y dev, en entorno de prod no borra la bases de datos del docdb, solo se borraría la tarea de replicación y la base de datos seguirá existiendo en el docdb.



### 4. Eliminación de colecciones
Pre condiciones:
- Las tareas deben estar pausadas, puede pausarla cambiando el valor de la variable dms_start_replication_task a false y correrlo.

Procedimiento:

- Ir al archivo dmsReplicationTask.json y eliminar todas la regla de la tarea asociada a esa colección, es decir todas las reglas de la tarea que tengan su campo table_name: "Nombre de la colección que quieren borrar".

Ejemplo:

Supongamos que quiere borrar la coleccion_2, este sería el dmsTaskSetting.json al inicio
```json
[
    {
    "task_id": "task_id",
    "table-mappings": {
      "rules": [
        {
          "rule-type": "selection",
          "rule-id": "rule_id_1 ",
          "rule-name": "rule_name_1",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_1"
          },
          "rule-action": "include",
          "filters": []
        },
        {
          "rule-type": "selection",
          "rule-id": "rule_id_2",
          "rule-name": "rule_name_2",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_2"
          },
          "rule-action": "include",
          "filters": []
        }
      ]
    },
    "target_endpoint_key": "endpoint_id"
  },
  ...
  ...
  ...
]
```
Y este sería el dmsTaskSetting.json al final:
```json
[
    {
    "task_id": "task_id",
    "table-mappings": {
      "rules": [
        {
          "rule-type": "selection",
          "rule-id": "rule_id_1 ",
          "rule-name": "rule_name_1",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_1"
          },
          "rule-action": "include",
          "filters": []
        },
      ]
    },
    "target_endpoint_key": "endpoint_id"
  },
  ...
  ...
  ...
]
```

- Una vez borrado del dmsReplicationTask.json corremos el código
- Luego para activar las tareas, cambiamos la variable dms_start_replication_task a true y lo corremos
Post condiciones:

La tarea asociada a ese task_id solo repliclará las colecciones que no fueron eliminadas, en este ejemplo solo coleccion_1 y ya no coleccion_2.

Nota: El lambda solo borrará las colecciones si se encuentra en el entorno de "qa" o "dev", en entorno de "prod" no borra las colecciones solo dejaría de replicar, la variable que determina el entorno es aws_project_env.

### 5. Agregar otra coleccion a una tarea de replicacion
Pre condiciones:
- La colección debe existir en la base de datos fuente
- Las tareas deben estar pausadas, puede pausarla cambiando el valor de la variable dms_start_replication_task a false y correrlo

Procedimiento:

- Ir al archivo dmsReplicationTask.json e identificar la tarea de replicación donde quieres colocar la nueva colección

Ejemplo: Supongamos que quiere añadir la coleccion_3 en la tarea que replica la coleccion_1 y coleccion_2

Nota: para que funcione las colecciones ya existentes y la nueva coleccion deben estar en la misma base de datos fuente y destino (la creación de la colección en el docdb será función de la lambda-create-user)

dmsReplicationTask.json al inicio:
```js
[
    {
    "task_id": "task_id",
    "table-mappings": {
      "rules": [
        {
          "rule-type": "selection",
          "rule-id": "rule_id_1 ",
          "rule-name": "rule_name_1",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_1"
          },
          "rule-action": "include",
          "filters": []
        },
        {
          "rule-type": "selection",
          "rule-id": "rule_id_2",
          "rule-name": "rule_name_2",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_2"
          },
          "rule-action": "include",
          "filters": []
        }
      ]
    },
    "target_endpoint_key": "endpoint_id"
  },
]
```

dmsReplicationTask.json después de agregar la nueva colección:

```json
[
    {
    "task_id": "task_id",
    "table-mappings": {
      "rules": [
        {
          "rule-type": "selection",
          "rule-id": "rule_id_1 ",
          "rule-name": "rule_name_1",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_1"
          },
          "rule-action": "include",
          "filters": []
        },
        {
          "rule-type": "selection",
          "rule-id": "rule_id_2",
          "rule-name": "rule_name_2",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_2"
          },
          "rule-action": "include",
          "filters": []
        },
        {
          "rule-type": "selection",
          "rule-id": "rule_id_3",
          "rule-name": "rule_name_3",
          "object-locator": {
            "schema-name": "nuevaBaseDatos",
            "table-name": "coleccion_3"
          },
          "rule-action": "include",
          "filters": []
        }
      ]
    },
    "target_endpoint_key": "endpoint_id"
  },
  ...
  ...
  ...
]
```
- Una vez agregada la nueva regla a la tarea, cambiamos la variable dms_start_replication_task a true y correrlo

Post-condiciones:
- La nueva colección estará creada en el docdb.
- La tarea replicará también la nueva colección establecida.





---------------------------
