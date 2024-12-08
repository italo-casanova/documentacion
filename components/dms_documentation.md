<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_dms_endpoint.source_enpoint](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dms_endpoint) | resource |
| [aws_dms_endpoint.target_endpoint](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dms_endpoint) | resource |
| [aws_dms_replication_instance.dms_replication_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dms_replication_instance) | resource |
| [aws_dms_replication_subnet_group.dms_replication_subnet_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dms_replication_subnet_group) | resource |
| [aws_dms_replication_task.replication_task](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dms_replication_task) | resource |
| [aws_iam_role.dms-cloudwatch-logs-role-replication-mongodb-docdb](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.dms-vpc-role-replication-mongodb-docdb](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy_attachment.dms-cloudwatch-logs-role-replication-mongodb-docdb-AmazonDMSCloudWatchLogsRole](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.dms-vpc-role-replication-mongodb-docdb-AmazonDMSVPCManagementRole](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_policy_document.dms_assume_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta de origen en AWS | `string` | n/a | yes |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | Nombre de la cuenta de destino en AWS | `string` | n/a | yes |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto (por ejemplo, dev, qa y prod) | `string` | n/a | yes |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_dms_cloudwatch_role_name"></a> [dms\_cloudwatch\_role\_name](#input\_dms\_cloudwatch\_role\_name) | Nombre del rol de cloudwatch logs para la replicación de mongodb a docdb | `string` | `"dms-cloudwatch-logs-role-replication-mongodb-docdb"` | no |
| <a name="input_dms_endpoint_mongodb"></a> [dms\_endpoint\_mongodb](#input\_dms\_endpoint\_mongodb) | Componente lógico que establece los campos necesario para la conexion a la base de datos fuente, endpoint\_id: identificador del endpoint, server\_name:ip o dominio de conexion de la base de datos, port = puerto de conexion a la base de datos, comentarios: se deja el valor de database\_name vacio para usar este endpoint como conexion a todas las bases de datos de la fuentes | <pre>list(object({<br>    endpoint_id   = string<br>    server_name   = string<br>    database_name = string<br>    port          = number<br>  }))</pre> | <pre>[<br>  {<br>    "database_name": "",<br>    "endpoint_id": "test-mongodb",<br>    "port": 27017,<br>    "server_name": "testqa-mongodb01.losandes.pe"<br>  }<br>]</pre> | no |
| <a name="input_dms_endpoints_target"></a> [dms\_endpoints\_target](#input\_dms\_endpoints\_target) | Lista de targets endpoints para conectarnos a las diferentes bases de datos dentro del cluster de docdb, endpoint\_id: identificador único del endpoint, database\_name: base de datos a la cuál se quiere conectar, comentarios: a diferencia del source\_endpoint aquí este valor no se puede dejar vacío porque cuando el motor es mongodb/docdb sí hay que especificar la base de datos | <pre>list(object({<br>    endpoint_id   = string<br>    database_name = string<br>  }))</pre> | <pre>[<br>  {<br>    "database_name": "Si_DbClaCobranza",<br>    "endpoint_id": "test-docdb-cobranza"<br>  },<br>  {<br>    "database_name": "Si_DbClaCuentaDigital",<br>    "endpoint_id": "test-docdb-cuenta-digital"<br>  },<br>  {<br>    "database_name": "Si_DbClaFirmas",<br>    "endpoint_id": "test-docdb-firmas"<br>  },<br>  {<br>    "database_name": "claModelosCreticiosLog",<br>    "endpoint_id": "test-docdb-modelo-crediticio"<br>  },<br>  {<br>    "database_name": "Si_DbClaPagos",<br>    "endpoint_id": "test-docdb-pagos"<br>  }<br>]</pre> | no |
| <a name="input_dms_repl_tasks_json_dir"></a> [dms\_repl\_tasks\_json\_dir](#input\_dms\_repl\_tasks\_json\_dir) | Ruta al archivo json donde se guardan los archivos el array de JSON de las tareas de replicación DMS | `string` | n/a | yes |
| <a name="input_dms_replication_subnet_group"></a> [dms\_replication\_subnet\_group](#input\_dms\_replication\_subnet\_group) | Grupo de subnets dondes se desplegará la instancia de replicación, replication\_subnet\_group\_id: identificador único del subnet group, subnets\_ids: ids de las subnets donde se quiere que se despliegue la instancia de replicación, replication\_subnet\_group\_description = descripcion asociada a la subnet | <pre>list(object({<br>    replication_subnet_group_id = string<br>    subnet_ids = list(string)<br>    replication_subnet_group_description= string<br>  }) )</pre> | <pre>[<br>  {<br>    "replication_subnet_group_description": "descripcion",<br>    "replication_subnet_group_id": "replication-mongodb-docdb",<br>    "subnet_ids": [<br>      "subnet-0c0c3ea6aed670172",<br>      "subnet-0df38652588ba4da5"<br>    ]<br>  }<br>]</pre> | no |
| <a name="input_dms_replication_task_migration_type"></a> [dms\_replication\_task\_migration\_type](#input\_dms\_replication\_task\_migration\_type) | Tipo de migratción de las tareas | `string` | n/a | yes |
| <a name="input_dms_ri_mongodb_docdb"></a> [dms\_ri\_mongodb\_docdb](#input\_dms\_ri\_mongodb\_docdb) | Instancia de replicacion, replication\_instnace\_id: idetntificador único, allocated storage: cantidad de almacenamiento en GB de la instancia, allow\_major\_version\_upgrade: permiso de actualización a una versión mayor de la instancia de replicación, apply\_inmediately: Indica si los cambios se realican de forma inmediata (true) o en la proxima ventana de mantenimiento (false), auto\_minor\_version\_upgrade: Indica si se deben realizar las actualicaiones menores, availability\_zone: zona de disponibilidad en donde se debe crear la isntancia, engine\_version: versión del motor que se usará, multi\_az: si la instancia debe estar configurada en múltiples AZ, publicly\_accessible: si la instancia debe ser accesible desde internet, replication\_instance\_class: clase de la instancia, preferred\_maintance\_window: ventana de mantenimiento preferida | <pre>list(object({<br>    replication_instance_id=string<br>    allocated_storage = number<br>    allow_major_version_upgrade = bool<br>    apply_immediately = bool<br>    auto_minor_version_upgrade=bool<br>    availability_zone= string<br>    engine_version=string<br>    multi_az=bool<br>    publicly_accessible=bool<br>    replication_instance_class=string<br>    preferred_maintenance_window = string<br>  }))</pre> | <pre>[<br>  {<br>    "allocated_storage": 50,<br>    "allow_major_version_upgrade": false,<br>    "apply_immediately": true,<br>    "auto_minor_version_upgrade": true,<br>    "availability_zone": "us-east-1a",<br>    "engine_version": "3.5.2",<br>    "multi_az": false,<br>    "preferred_maintenance_window": "",<br>    "publicly_accessible": false,<br>    "replication_instance_class": "dms.t3.medium",<br>    "replication_instance_id": "test-replication-mongodb-docdb"<br>  }<br>]</pre> | no |
| <a name="input_dms_start_replication_task"></a> [dms\_start\_replication\_task](#input\_dms\_start\_replication\_task) | Campo para activar, detener o renaudar una tarea | `bool` | `true` | no |
| <a name="input_dms_target_endpoint_engine_name"></a> [dms\_target\_endpoint\_engine\_name](#input\_dms\_target\_endpoint\_engine\_name) | Nombre del motor de la base de datos destino según AWS-DMS | `string` | n/a | yes |
| <a name="input_dms_target_endpoint_password"></a> [dms\_target\_endpoint\_password](#input\_dms\_target\_endpoint\_password) | Password del usuario para conectarse a la base de datos destino | `string` | n/a | yes |
| <a name="input_dms_target_endpoint_port"></a> [dms\_target\_endpoint\_port](#input\_dms\_target\_endpoint\_port) | Puerto por el cual los target endpoints se van a conectar | `number` | n/a | yes |
| <a name="input_dms_target_endpoint_server_name"></a> [dms\_target\_endpoint\_server\_name](#input\_dms\_target\_endpoint\_server\_name) | ip o endpoint del cluster de docdb que se usará como target endpoint, es proporcionado por el docdb que se crea en el modulo documentDB | `string` | n/a | yes |
| <a name="input_dms_target_endpoint_username"></a> [dms\_target\_endpoint\_username](#input\_dms\_target\_endpoint\_username) | Usename del usuario para conectarse a la base de datos destino | `string` | n/a | yes |
| <a name="input_dms_vpc_role_name"></a> [dms\_vpc\_role\_name](#input\_dms\_vpc\_role\_name) | Nombre del rol de VPC | `string` | `"vpc-role-test"` | no |
| <a name="input_dms_vpc_sg_ids"></a> [dms\_vpc\_sg\_ids](#input\_dms\_vpc\_sg\_ids) | Ids de los grupos de seguridad de la instancia de replicación | `list(string)` | n/a | yes |
| <a name="input_kms_key_arn"></a> [kms\_key\_arn](#input\_kms\_key\_arn) | Clave de cifrado que se usa para descifrar los datos en el docdb, si es que se activa el cifrado | `string` | `"arn:aws:kms:us-east-1:546007436944:key/146d6403-63e2-4125-ba42-5ee85db9136b"` | no |
| <a name="input_mongodb_onpremise_password"></a> [mongodb\_onpremise\_password](#input\_mongodb\_onpremise\_password) | Password del usuario de conexion a la base de datos on-premise | `string` | `"Cl4MKmJz1$TqBaUq$-Pr0t3cs0"` | no |
| <a name="input_mongodb_onpremise_username"></a> [mongodb\_onpremise\_username](#input\_mongodb\_onpremise\_username) | Username del usuario de conexion a la base de datos on-premise | `string` | `"usrprotecso"` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->