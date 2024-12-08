<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | 5.65.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_domain5_dms"></a> [domain5\_dms](#module\_domain5\_dms) | git::https://bitbucket.org/losandespe/aws-dms-module.git//dms-mongodb | n/a |
| <a name="module_domain5_docDB"></a> [domain5\_docDB](#module\_domain5\_docDB) | git::https://bitbucket.org/losandespe/aws-documentdb-module.git//documentdb-dms-mongodb | n/a |
| <a name="module_domain5_ec2_kafka_cluster"></a> [domain5\_ec2\_kafka\_cluster](#module\_domain5\_ec2\_kafka\_cluster) | git::https://bitbucket.org/losandespe/aws-ec2-module.git//ec2-kafka | n/a |
| <a name="module_domain5_ec2_repl_mongodb_docdb"></a> [domain5\_ec2\_repl\_mongodb\_docdb](#module\_domain5\_ec2\_repl\_mongodb\_docdb) | git::https://bitbucket.org/losandespe/aws-ec2-module.git//ec2-repl-mongodb-docdb | n/a |
| <a name="module_domain5_lambda_clean_replication"></a> [domain5\_lambda\_clean\_replication](#module\_domain5\_lambda\_clean\_replication) | git::https://bitbucket.org/losandespe/aws-lambda-module.git//lambda-clean-repl-docdb-s3-mongodb | n/a |
| <a name="module_domain5_lambda_config_docdb"></a> [domain5\_lambda\_config\_docdb](#module\_domain5\_lambda\_config\_docdb) | git::https://bitbucket.org/losandespe/aws-lambda-module.git//lambda-docdb-create-user-db | n/a |
| <a name="module_domain5_lambda_restore_replication"></a> [domain5\_lambda\_restore\_replication](#module\_domain5\_lambda\_restore\_replication) | git::https://bitbucket.org/losandespe/aws-lambda-module.git//lambda-restore-repl-s3-mongodb | n/a |
| <a name="module_domain5_lambda_setup_kafka"></a> [domain5\_lambda\_setup\_kafka](#module\_domain5\_lambda\_setup\_kafka) | git::https://bitbucket.org/losandespe/aws-lambda-module.git//lambda-setup-kafka | n/a |
| <a name="module_domain5_lambda_start_replication"></a> [domain5\_lambda\_start\_replication](#module\_domain5\_lambda\_start\_replication) | git::https://bitbucket.org/losandespe/aws-lambda-module.git//lambda-start-repl-docdb-s3 | n/a |
| <a name="module_domain5_policy_lambda_access_s3"></a> [domain5\_policy\_lambda\_access\_s3](#module\_domain5\_policy\_lambda\_access\_s3) | git::https://bitbucket.org/losandespe/aws-iam-module.git//iam-policy-lambda/access-s3 | n/a |
| <a name="module_domain5_policy_lambda_get_secret"></a> [domain5\_policy\_lambda\_get\_secret](#module\_domain5\_policy\_lambda\_get\_secret) | git::https://bitbucket.org/losandespe/aws-iam-module.git//iam-policy-lambda/secret-manager | n/a |
| <a name="module_domain5_policy_lambda_repl_access_ec2"></a> [domain5\_policy\_lambda\_repl\_access\_ec2](#module\_domain5\_policy\_lambda\_repl\_access\_ec2) | git::https://bitbucket.org/losandespe/aws-iam-module.git//iam-policy-lambda/access-ec2 | n/a |
| <a name="module_domain5_role_lambda_config_docdb"></a> [domain5\_role\_lambda\_config\_docdb](#module\_domain5\_role\_lambda\_config\_docdb) | git::https://bitbucket.org/losandespe/aws-iam-module.git//iam-role-lambda/replication | n/a |
| <a name="module_domain5_role_lambda_replication"></a> [domain5\_role\_lambda\_replication](#module\_domain5\_role\_lambda\_replication) | git::https://bitbucket.org/losandespe/aws-iam-module.git//iam-role-lambda/replication | n/a |
| <a name="module_domain5_secret_docdb"></a> [domain5\_secret\_docdb](#module\_domain5\_secret\_docdb) | git::https://bitbucket.org/losandespe/aws-secretsmanager-module.git//secret-docdb | n/a |
| <a name="module_domain5_security_group_dms"></a> [domain5\_security\_group\_dms](#module\_domain5\_security\_group\_dms) | git::https://bitbucket.org/losandespe/aws-ec2-sg-module.git//minimal | n/a |
| <a name="module_domain5_security_group_docdb"></a> [domain5\_security\_group\_docdb](#module\_domain5\_security\_group\_docdb) | git::https://bitbucket.org/losandespe/aws-ec2-sg-module.git//minimal | n/a |
| <a name="module_domain5_security_group_ec2"></a> [domain5\_security\_group\_ec2](#module\_domain5\_security\_group\_ec2) | git::https://bitbucket.org/losandespe/aws-ec2-sg-module.git//minimal | n/a |
| <a name="module_domain5_security_group_ec2_kafka"></a> [domain5\_security\_group\_ec2\_kafka](#module\_domain5\_security\_group\_ec2\_kafka) | git::https://bitbucket.org/losandespe/aws-ec2-sg-module.git//minimal | n/a |
| <a name="module_domain5_security_group_lambda"></a> [domain5\_security\_group\_lambda](#module\_domain5\_security\_group\_lambda) | git::https://bitbucket.org/losandespe/aws-ec2-sg-module.git//minimal | n/a |

## Resources

| Name | Type |
|------|------|
| [aws_iam_role_policy_attachment.lambda_access_ec2](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.lambda_access_s3](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.lambda_create_user_get_s3](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.lambda_create_user_get_secret_value](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.lambda_create_user_vpc_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.lambda_replication_vpc_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.role_lambda_replication_get_secret_value](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_lambda_invocation.invoke_create_user_replication](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_invocation) | resource |
| [aws_s3_bucket.backups](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) | resource |
| [aws_s3_bucket_object.dms_tasks_json](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_object) | resource |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region) | data source |
| [aws_secretsmanager_secret.dms_replication_user_secret](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/secretsmanager_secret) | data source |
| [aws_secretsmanager_secret.docdb_master_user_secret](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/secretsmanager_secret) | data source |
| [aws_secretsmanager_secret_version.dms_replication_user_secret_version](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/secretsmanager_secret_version) | data source |
| [aws_secretsmanager_secret_version.docdb_master_user_secret_version](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/secretsmanager_secret_version) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta de origen en AWS | `string` | n/a | yes |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | Nombre de la cuenta de destino en AWS | `string` | n/a | yes |
| <a name="input_aws_account_vpc_id"></a> [aws\_account\_vpc\_id](#input\_aws\_account\_vpc\_id) | vp del proyecto | `string` | n/a | yes |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_aws_project_devops_cdir"></a> [aws\_project\_devops\_cdir](#input\_aws\_project\_devops\_cdir) | CIDR de la cuenta de origen (devops) | `string` | n/a | yes |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto (por ejemplo, dev, qa y prod) | `string` | n/a | yes |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_dms_cloudwatch_role_name"></a> [dms\_cloudwatch\_role\_name](#input\_dms\_cloudwatch\_role\_name) | Nombre del rol para acceder a cloudwatch | `string` | n/a | yes |
| <a name="input_dms_egress_rules"></a> [dms\_egress\_rules](#input\_dms\_egress\_rules) | Reglas de egreso del grupo de seguridad de la instancia de replicación | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_dms_endpoint_mongodb"></a> [dms\_endpoint\_mongodb](#input\_dms\_endpoint\_mongodb) | Endpoint de la base de datos destino (mongodb onpremise) | <pre>list(object({<br>    endpoint_id   = string<br>    server_name   = string<br>    database_name = string<br>    port          = number<br>  }))</pre> | <pre>[<br>  {<br>    "database_name": "",<br>    "endpoint_id": "test-mongodb",<br>    "port": 27017,<br>    "server_name": "testqa-mongodb01.losandes.pe"<br>  }<br>]</pre> | no |
| <a name="input_dms_endpoints_docdb"></a> [dms\_endpoints\_docdb](#input\_dms\_endpoints\_docdb) | Lista de endpoints DocDB para DMS | <pre>list(object({<br>    endpoint_id   = string<br>    database_name = string<br>  }))</pre> | <pre>[<br>  {<br>    "database_name": "Si_DbClaCobranza",<br>    "endpoint_id": "test-docdb-cobranza"<br>  },<br>  {<br>    "database_name": "Si_DbClaCuentaDigital",<br>    "endpoint_id": "test-docdb-cuenta-digital"<br>  },<br>  {<br>    "database_name": "Si_DbClaFirmas",<br>    "endpoint_id": "test-docdb-cuenta-firmas"<br>  },<br>  {<br>    "database_name": "claModelosCreticiosLog",<br>    "endpoint_id": "test-docdb-modelo-crediticio"<br>  },<br>  {<br>    "database_name": "Si_DbClaPagos",<br>    "endpoint_id": "test-docdb-pagos"<br>  }<br>]</pre> | no |
| <a name="input_dms_ingress_rules"></a> [dms\_ingress\_rules](#input\_dms\_ingress\_rules) | Reglas de ingreso del grupo de seguridad de la instancia de replicación | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_dms_replication_task_migration_type"></a> [dms\_replication\_task\_migration\_type](#input\_dms\_replication\_task\_migration\_type) | Tipo de migración de las tareas | `string` | `"full-load-and-cdc"` | no |
| <a name="input_dms_ri_mongodb_docdb"></a> [dms\_ri\_mongodb\_docdb](#input\_dms\_ri\_mongodb\_docdb) | Configuración de la instancia de replicación del DMS | <pre>list(object({<br>    replication_instance_id      = string<br>    allocated_storage            = number<br>    allow_major_version_upgrade  = bool<br>    apply_immediately            = bool<br>    auto_minor_version_upgrade   = bool<br>    availability_zone            = string<br>    engine_version               = string<br>    multi_az                     = bool<br>    publicly_accessible          = bool<br>    replication_instance_class   = string<br>    preferred_maintenance_window = string<br>  }))</pre> | n/a | yes |
| <a name="input_dms_secret_user_replication_name"></a> [dms\_secret\_user\_replication\_name](#input\_dms\_secret\_user\_replication\_name) | Nombre del secreto que guardará las credenciales del usuario dms para la replicacion | `string` | n/a | yes |
| <a name="input_dms_sg_description"></a> [dms\_sg\_description](#input\_dms\_sg\_description) | Descripción del grupo de seguirdad de la isntancia de replicación | `string` | n/a | yes |
| <a name="input_dms_sg_name"></a> [dms\_sg\_name](#input\_dms\_sg\_name) | Nombre del grupo de seguridad de la instancia de replicación | `string` | n/a | yes |
| <a name="input_dms_start_replication_task"></a> [dms\_start\_replication\_task](#input\_dms\_start\_replication\_task) | Inicia o pausa las tareas de replicación | `bool` | n/a | yes |
| <a name="input_dms_subnet_group_mongodb_docdb"></a> [dms\_subnet\_group\_mongodb\_docdb](#input\_dms\_subnet\_group\_mongodb\_docdb) | Subnets donde se desplegará la instancia de replicación | <pre>list(object({<br>    replication_subnet_group_id          = string<br>    subnet_ids                           = list(string)<br>    replication_subnet_group_description = string<br>  }))</pre> | <pre>[<br>  {<br>    "replication_subnet_group_description": "descripcion",<br>    "replication_subnet_group_id": "replication-mongodb-docdb",<br>    "subnet_ids": [<br>      "subnet-0c0c3ea6aed670172",<br>      "subnet-0df38652588ba4da5"<br>    ]<br>  }<br>]</pre> | no |
| <a name="input_dms_target_endpoint_engine_name"></a> [dms\_target\_endpoint\_engine\_name](#input\_dms\_target\_endpoint\_engine\_name) | Motor de la base de datos destino | `string` | `"docdb"` | no |
| <a name="input_dms_user_replication_username"></a> [dms\_user\_replication\_username](#input\_dms\_user\_replication\_username) | Username del usuario de replicacion para dms | `string` | n/a | yes |
| <a name="input_dms_vpc_role_name"></a> [dms\_vpc\_role\_name](#input\_dms\_vpc\_role\_name) | Nombre del rol para acceder a la VPC | `string` | n/a | yes |
| <a name="input_docdb_cluster_instance_class"></a> [docdb\_cluster\_instance\_class](#input\_docdb\_cluster\_instance\_class) | Clase de instancia para la replicación de DocDB | `string` | `"db.t3.medium"` | no |
| <a name="input_docdb_cluster_instance_count"></a> [docdb\_cluster\_instance\_count](#input\_docdb\_cluster\_instance\_count) | Cantidad de nodos del cluster de docdb | `number` | n/a | yes |
| <a name="input_docdb_cluster_parameter_group_family"></a> [docdb\_cluster\_parameter\_group\_family](#input\_docdb\_cluster\_parameter\_group\_family) | Familia de versiones del DocDB | `string` | `"docdb4.0"` | no |
| <a name="input_docdb_cluster_parameter_group_name"></a> [docdb\_cluster\_parameter\_group\_name](#input\_docdb\_cluster\_parameter\_group\_name) | Nombre del grupo de parámetros de DocDB | `string` | n/a | yes |
| <a name="input_docdb_cluster_replication"></a> [docdb\_cluster\_replication](#input\_docdb\_cluster\_replication) | Configuración del clúster de replicación de DocDB | <pre>list(object({<br>    cluster_identifier           = string<br>    engine_version               = string<br>    preferred_backup_window      = string<br>    backup_retention_period      = number<br>    availability_zones           = list(string)<br>    apply_immediately            = bool<br>    preferred_maintenance_window = string<br>    deletion_protection          = bool<br>    skip_final_snapshot          = bool<br>    port                         = number<br>  }))</pre> | n/a | yes |
| <a name="input_docdb_egress_rules"></a> [docdb\_egress\_rules](#input\_docdb\_egress\_rules) | Reglas de egreso del grupo de seguridad del docdb | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_docdb_ingress_rules"></a> [docdb\_ingress\_rules](#input\_docdb\_ingress\_rules) | Reglas de ingreso del grupo de seguridad del docdb | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_docdb_master_user_secret_name"></a> [docdb\_master\_user\_secret\_name](#input\_docdb\_master\_user\_secret\_name) | Nombre del secreto donde se guardan las credeciales del usuario root del documentDB | `string` | n/a | yes |
| <a name="input_docdb_sg_description"></a> [docdb\_sg\_description](#input\_docdb\_sg\_description) | Descripción del grupo de seguridad del docdb | `string` | n/a | yes |
| <a name="input_docdb_sg_name"></a> [docdb\_sg\_name](#input\_docdb\_sg\_name) | Nombre del grupo de seguridad del docdb | `string` | n/a | yes |
| <a name="input_docdb_subnet_group_name"></a> [docdb\_subnet\_group\_name](#input\_docdb\_subnet\_group\_name) | Nombre del grupo de subredes de DocDB | `string` | n/a | yes |
| <a name="input_docdb_subnets_ids"></a> [docdb\_subnets\_ids](#input\_docdb\_subnets\_ids) | Lista de IDs de subredes para DocDB | `list(string)` | n/a | yes |
| <a name="input_ec2_egress_rules"></a> [ec2\_egress\_rules](#input\_ec2\_egress\_rules) | Reglas de egreso del grupo de seguridad del ec2 de replicaicón de docdb a mongodb | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_ec2_ingress_rules"></a> [ec2\_ingress\_rules](#input\_ec2\_ingress\_rules) | Reglas de ingreso del grupo de seguridad del ec2 de replicaicón de docdb a mongodb | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_ec2_instance_type"></a> [ec2\_instance\_type](#input\_ec2\_instance\_type) | Tipo de instancia del ec2 de replicaicón de docdb a mongodb | `string` | n/a | yes |
| <a name="input_ec2_kafka_instance_type"></a> [ec2\_kafka\_instance\_type](#input\_ec2\_kafka\_instance\_type) | Nombre del cluster de kafka | `string` | n/a | yes |
| <a name="input_ec2_kafka_key_pair_name"></a> [ec2\_kafka\_key\_pair\_name](#input\_ec2\_kafka\_key\_pair\_name) | Nombre del kay pair de las intancias del cluster de kafka | `string` | n/a | yes |
| <a name="input_ec2_kafka_name_1"></a> [ec2\_kafka\_name\_1](#input\_ec2\_kafka\_name\_1) | Nombre del ec2 1 del cluster ed kafka | `string` | n/a | yes |
| <a name="input_ec2_kafka_name_2"></a> [ec2\_kafka\_name\_2](#input\_ec2\_kafka\_name\_2) | Nombre del ec2 1 del cluster ed kafka | `string` | n/a | yes |
| <a name="input_ec2_kafka_sg_description"></a> [ec2\_kafka\_sg\_description](#input\_ec2\_kafka\_sg\_description) | Descripción del grupo de seguridad del EC2 | `string` | n/a | yes |
| <a name="input_ec2_kafka_sg_name"></a> [ec2\_kafka\_sg\_name](#input\_ec2\_kafka\_sg\_name) | Nombre del grupo de seguridad del EC2 | `string` | n/a | yes |
| <a name="input_ec2_kafka_subnet_id"></a> [ec2\_kafka\_subnet\_id](#input\_ec2\_kafka\_subnet\_id) | Nombre del cluster de kafka | `string` | n/a | yes |
| <a name="input_ec2_kafka_volume_size"></a> [ec2\_kafka\_volume\_size](#input\_ec2\_kafka\_volume\_size) | Nombre del cluster de kafka | `number` | n/a | yes |
| <a name="input_ec2_key_pair_name"></a> [ec2\_key\_pair\_name](#input\_ec2\_key\_pair\_name) | Nombre del key pair del ec2 de replicaicón de docdb a mongodb | `string` | n/a | yes |
| <a name="input_ec2_name"></a> [ec2\_name](#input\_ec2\_name) | id del ec2 de replicación de docdb a mongodb | `string` | n/a | yes |
| <a name="input_ec2_sg_description"></a> [ec2\_sg\_description](#input\_ec2\_sg\_description) | Descripción del grupo de seguridad del ec2 de replicaicón de docdb a mongodb | `string` | n/a | yes |
| <a name="input_ec2_sg_name"></a> [ec2\_sg\_name](#input\_ec2\_sg\_name) | Nombre del grupo de seguridad del ec2 de replicación de docdb a mongodb | `string` | n/a | yes |
| <a name="input_ec2_subnet_id"></a> [ec2\_subnet\_id](#input\_ec2\_subnet\_id) | id de la subnet donde se va a desplegar el ec2 de replicaicón de docdb a mongodb | `string` | n/a | yes |
| <a name="input_ec2_volume_size"></a> [ec2\_volume\_size](#input\_ec2\_volume\_size) | Volumen del ec2 de replicaicón de docdb a mongodb | `string` | n/a | yes |
| <a name="input_iac_aws_account_target_role"></a> [iac\_aws\_account\_target\_role](#input\_iac\_aws\_account\_target\_role) | ARN del ROL de la cuenta TARGET | `string` | n/a | yes |
| <a name="input_iac_aws_region"></a> [iac\_aws\_region](#input\_iac\_aws\_region) | Region donde se desplegará la infra | `string` | n/a | yes |
| <a name="input_iam_ec2_kafka_role_name"></a> [iam\_ec2\_kafka\_role\_name](#input\_iam\_ec2\_kafka\_role\_name) | Nombre del cluster de kafka | `string` | n/a | yes |
| <a name="input_iam_policy_ec2_name"></a> [iam\_policy\_ec2\_name](#input\_iam\_policy\_ec2\_name) | Nombre de la política del ec2 de replicación de docdb a mongodb | `string` | n/a | yes |
| <a name="input_iam_policy_lambda_access_docdb_name"></a> [iam\_policy\_lambda\_access\_docdb\_name](#input\_iam\_policy\_lambda\_access\_docdb\_name) | Nombre de la política que usarán las lambdas crear usuario y crear bd para acceder al documentDB | `string` | n/a | yes |
| <a name="input_iam_policy_lambda_access_ec2_name"></a> [iam\_policy\_lambda\_access\_ec2\_name](#input\_iam\_policy\_lambda\_access\_ec2\_name) | Nombre de la política de la lambda para acceder a ec2 | `string` | n/a | yes |
| <a name="input_iam_policy_lambda_access_s3_name"></a> [iam\_policy\_lambda\_access\_s3\_name](#input\_iam\_policy\_lambda\_access\_s3\_name) | Nombre de la política de la lambda para acceder a S3 | `any` | n/a | yes |
| <a name="input_iam_role_ec2_name"></a> [iam\_role\_ec2\_name](#input\_iam\_role\_ec2\_name) | Nombre del rol del ec2 de replicación de docdb a mongodb | `string` | n/a | yes |
| <a name="input_iam_role_lambda_access_docdb_name"></a> [iam\_role\_lambda\_access\_docdb\_name](#input\_iam\_role\_lambda\_access\_docdb\_name) | Nombre del rol que usarán las lambdas crear usuario y crear db para acceder al documentDB | `string` | n/a | yes |
| <a name="input_iam_role_lambda_repl_name"></a> [iam\_role\_lambda\_repl\_name](#input\_iam\_role\_lambda\_repl\_name) | Nombre del rol de la lambda de replicacion (rol que usarán las lambdas: start-replication, restore-replication y clean-replication) | `string` | n/a | yes |
| <a name="input_kafka_egress_rules"></a> [kafka\_egress\_rules](#input\_kafka\_egress\_rules) | n/a | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_kafka_ingress_rules"></a> [kafka\_ingress\_rules](#input\_kafka\_ingress\_rules) | n/a | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_kms_key_arn"></a> [kms\_key\_arn](#input\_kms\_key\_arn) | Arn del kms gestionado por aws | `string` | `"arn:aws:kms:us-east-1:546007436944:key/146d6403-63e2-4125-ba42-5ee85db9136b"` | no |
| <a name="input_lambda_clean_replication_function_name"></a> [lambda\_clean\_replication\_function\_name](#input\_lambda\_clean\_replication\_function\_name) | Nombre de la función de la lambda de limpieza | `string` | n/a | yes |
| <a name="input_lambda_create_user_db_function_name"></a> [lambda\_create\_user\_db\_function\_name](#input\_lambda\_create\_user\_db\_function\_name) | Nombre de la lambda crear usuario | `string` | n/a | yes |
| <a name="input_lambda_egress_rules"></a> [lambda\_egress\_rules](#input\_lambda\_egress\_rules) | Reglas de egreso del grupo de seguridad de las lambdas | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_lambda_ingress_rules"></a> [lambda\_ingress\_rules](#input\_lambda\_ingress\_rules) | Reglas de ingreso del grupo de seguridad de las lambdas | <pre>list(object({<br>    from_port   = number<br>    to_port     = number<br>    protocol    = string<br>    cidr_blocks = list(string)<br>  }))</pre> | n/a | yes |
| <a name="input_lambda_restore_replication_function_name"></a> [lambda\_restore\_replication\_function\_name](#input\_lambda\_restore\_replication\_function\_name) | Nombre de la función de la lambda de restauración | `string` | n/a | yes |
| <a name="input_lambda_setup_kafka_name"></a> [lambda\_setup\_kafka\_name](#input\_lambda\_setup\_kafka\_name) | Nombre de la función de la lmabda de setup kafka | `string` | n/a | yes |
| <a name="input_lambda_sg_description"></a> [lambda\_sg\_description](#input\_lambda\_sg\_description) | Descripción del grupo de seguridad de las lambdas | `string` | n/a | yes |
| <a name="input_lambda_sg_name"></a> [lambda\_sg\_name](#input\_lambda\_sg\_name) | Nombre del grupo de seguridad que de las lambdas | `string` | n/a | yes |
| <a name="input_lambda_start_replication_function_name"></a> [lambda\_start\_replication\_function\_name](#input\_lambda\_start\_replication\_function\_name) | Nombre de la función de la lambda de replicacion | `string` | n/a | yes |
| <a name="input_lambda_subnet_ids"></a> [lambda\_subnet\_ids](#input\_lambda\_subnet\_ids) | Lista de IDs de subredes para las lambdas | `list(string)` | n/a | yes |
| <a name="input_mongodb_onpremise_password"></a> [mongodb\_onpremise\_password](#input\_mongodb\_onpremise\_password) | Password del usuario para acceder a mongodb on premise | `string` | `"Cl4MKmJz1$TqBaUq$-Pr0t3cs0"` | no |
| <a name="input_mongodb_onpremise_username"></a> [mongodb\_onpremise\_username](#input\_mongodb\_onpremise\_username) | Username del usuario para acceder a mongodb onpremise | `string` | `"usrprotecso"` | no |
| <a name="input_private_ip_kafka1"></a> [private\_ip\_kafka1](#input\_private\_ip\_kafka1) | IP privada del kafka 1 | `any` | n/a | yes |
| <a name="input_private_ip_kafka2"></a> [private\_ip\_kafka2](#input\_private\_ip\_kafka2) | IP privada del kafka 2 | `any` | n/a | yes |
| <a name="input_s3_bucket_name"></a> [s3\_bucket\_name](#input\_s3\_bucket\_name) | Nombre del bucket de S3 | `string` | n/a | yes |

## Outputs

No outputs.
<!-- END_TF_DOCS -->