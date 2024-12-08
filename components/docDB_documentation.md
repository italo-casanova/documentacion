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
| [aws_docdb_cluster.docdb_cluster](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_cluster) | resource |
| [aws_docdb_cluster_instance.docdb_cluster_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_cluster_instance) | resource |
| [aws_docdb_cluster_parameter_group.docdb_cluster_parameter_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_cluster_parameter_group) | resource |
| [aws_docdb_subnet_group.docdb_subnet_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_subnet_group) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta de origen en AWS | `string` | `"devops"` | no |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | Nombre de la cuenta de destino en AWS | `string` | `"integration-qa"` | no |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta del proyecto en AWS | `string` | `"devops"` | no |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto (por ejemplo, dev, qa y prod) | `string` | `"develop"` | no |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto en AWS | `string` | `"dca"` | no |
| <a name="input_docdb_cluster"></a> [docdb\_cluster](#input\_docdb\_cluster) | Configuración del clúster de replicación de DocDB.<br>  estructura:<br>    cluster\_identifier           = id del cluster<br>    master\_username              = usuario root del cluster<br>    master\_password              = contraseña root del cluster<br>    engine\_version               = version del motro documentdb, debe ser compatible con la version de mongodb<br>                                    (actualmente 4.4.14)<br>    preferred\_backup\_window      = horario para la creación de backups<br>    backup\_retention\_period      = tiempo de retención del backup<br>    availability\_zones           = zonas de disponibilidad para el despliegue de los nodos<br>    apply\_immediately            = define si los cambios se aplicarán de manera inmediata o en la siguiente etapa de mantenimiento<br>    preferred\_maintenance\_window = tiempo de inicio y fin del mantenimiento<br>    deletion\_protection          = evita que un usuario borre el cluster, para borrarlo primero colocar<br>                                    el valor en false<br>    skip\_final\_snapshot          = true -> crea un snapshot al borrar el cluster<br>    port                         = puerto de conexión | <pre>list(object({<br>    cluster_identifier           = string<br>    engine_version               = string<br>    preferred_backup_window      = string<br>    backup_retention_period      = number<br>    availability_zones           = list(string)<br>    apply_immediately            = bool<br>    preferred_maintenance_window = string<br>    deletion_protection          = bool<br>    skip_final_snapshot          = bool<br>    port                         = number<br>  }))</pre> | n/a | yes |
| <a name="input_docdb_cluster_instance_class"></a> [docdb\_cluster\_instance\_class](#input\_docdb\_cluster\_instance\_class) | Clase de instancia para la replicación de DocDB | `string` | `"db.t3.medium"` | no |
| <a name="input_docdb_cluster_instance_count"></a> [docdb\_cluster\_instance\_count](#input\_docdb\_cluster\_instance\_count) | Cantidad de nodos del cluster de docdb | `number` | n/a | yes |
| <a name="input_docdb_cluster_master_password"></a> [docdb\_cluster\_master\_password](#input\_docdb\_cluster\_master\_password) | Password del usuario maestro de DocDB | `string` | n/a | yes |
| <a name="input_docdb_cluster_master_username"></a> [docdb\_cluster\_master\_username](#input\_docdb\_cluster\_master\_username) | Username del usuario maestro de DOCDB | `string` | n/a | yes |
| <a name="input_docdb_cluster_parameter_group_family"></a> [docdb\_cluster\_parameter\_group\_family](#input\_docdb\_cluster\_parameter\_group\_family) | Familia de la version del DocDb | `string` | n/a | yes |
| <a name="input_docdb_cluster_parameter_group_name"></a> [docdb\_cluster\_parameter\_group\_name](#input\_docdb\_cluster\_parameter\_group\_name) | Nombre del grupo de parámetros de DocDB | `string` | `"replication-mongodb-docdb"` | no |
| <a name="input_docdb_cluster_vpc_security_group_ids"></a> [docdb\_cluster\_vpc\_security\_group\_ids](#input\_docdb\_cluster\_vpc\_security\_group\_ids) | Descripción de los grupos de seguridad del cluster de docdb | `list(string)` | n/a | yes |
| <a name="input_docdb_subnet_group_name"></a> [docdb\_subnet\_group\_name](#input\_docdb\_subnet\_group\_name) | Nombre del grupo de subredes de DocDB | `string` | `"docdb-subnet-group"` | no |
| <a name="input_docdb_subnets_ids"></a> [docdb\_subnets\_ids](#input\_docdb\_subnets\_ids) | Lista de IDs de subredes para DocDB | `list(string)` | <pre>[<br>  "subnet-0c0c3ea6aed670172",<br>  "subnet-0df38652588ba4da5",<br>  "subnet-0dc5efbdaa7d5b864"<br>]</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_docdb_cluster_arn"></a> [docdb\_cluster\_arn](#output\_docdb\_cluster\_arn) | Arn del cluster |
| <a name="output_docdb_cluster_endpoint"></a> [docdb\_cluster\_endpoint](#output\_docdb\_cluster\_endpoint) | Endpoint, server name, ip o dominio del cluster |
| <a name="output_docdb_cluster_port"></a> [docdb\_cluster\_port](#output\_docdb\_cluster\_port) | Puerto para conectarse al cluster de docdb |
<!-- END_TF_DOCS -->