<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |
| <a name="provider_tls"></a> [tls](#provider\_tls) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_iam_instance_profile.iam_instance_profile](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_instance_profile) | resource |
| [aws_iam_policy.ec2_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_role.ec2_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy_attachment.ec2_repl_mongodb_docdb](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.ssm_instance_core_attach](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.ssm_patch_association_attach](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_instance.ec2](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance) | resource |
| [aws_key_pair.key_pair](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/key_pair) | resource |
| [tls_private_key.tls_private_key](https://registry.terraform.io/providers/hashicorp/tls/latest/docs/resources/private_key) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta de origen en AWS | `string` | n/a | yes |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | Nombre de la cuenta de destino en AWS | `string` | n/a | yes |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto (por ejemplo, dev, qa y prod) | `string` | n/a | yes |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_docdb_cluster_endpoint"></a> [docdb\_cluster\_endpoint](#input\_docdb\_cluster\_endpoint) | Endpoint del cluster de DocumentDB | `string` | n/a | yes |
| <a name="input_docdb_cluster_port"></a> [docdb\_cluster\_port](#input\_docdb\_cluster\_port) | Puerto del cluster de DocumentDB | `string` | n/a | yes |
| <a name="input_docdb_master_user_secret_arn"></a> [docdb\_master\_user\_secret\_arn](#input\_docdb\_master\_user\_secret\_arn) | Arn del secreto que guarda las credenciales del usuario maestro del DocumentDB | `string` | n/a | yes |
| <a name="input_ec2_name"></a> [ec2\_name](#input\_ec2\_name) | Nombre del ec2 | `string` | n/a | yes |
| <a name="input_file_replication_go"></a> [file\_replication\_go](#input\_file\_replication\_go) | Ruta al servicio de replicación qué está hecho en golang | `string` | n/a | yes |
| <a name="input_iam_ec2_policy_name"></a> [iam\_ec2\_policy\_name](#input\_iam\_ec2\_policy\_name) | Nombre de la política | `string` | n/a | yes |
| <a name="input_iam_ec2_role_name"></a> [iam\_ec2\_role\_name](#input\_iam\_ec2\_role\_name) | Nombre del rol del ec2 | `string` | n/a | yes |
| <a name="input_instance_type"></a> [instance\_type](#input\_instance\_type) | Nombre del tipo de instancia | `string` | n/a | yes |
| <a name="input_key_pair_name"></a> [key\_pair\_name](#input\_key\_pair\_name) | Nombre del key\_pair del ec2 | `string` | n/a | yes |
| <a name="input_path_user_data_sh"></a> [path\_user\_data\_sh](#input\_path\_user\_data\_sh) | Ruta hacia el script de bash que configura el ec2 | `string` | n/a | yes |
| <a name="input_s3_arn"></a> [s3\_arn](#input\_s3\_arn) | Arn del s3 donde se van a guardar los dumps del MongoDB, DocumentDB y las operaciones para la restauración a MongoDB on premise | `string` | n/a | yes |
| <a name="input_s3_bucket_name"></a> [s3\_bucket\_name](#input\_s3\_bucket\_name) | Nombre del s3 donde se guardan las dumps y las operaciones de restauración del MongoDB on premise | `string` | n/a | yes |
| <a name="input_secret_arn"></a> [secret\_arn](#input\_secret\_arn) | Arn del secreto donde están las credenciales del usuario maestro del DocumentDB | `string` | n/a | yes |
| <a name="input_subnet_id"></a> [subnet\_id](#input\_subnet\_id) | Id de la subnet donde va a estar el ec2 | `string` | n/a | yes |
| <a name="input_volume_size"></a> [volume\_size](#input\_volume\_size) | Volumen del ec2 | `string` | n/a | yes |
| <a name="input_vpc_security_group_ids"></a> [vpc\_security\_group\_ids](#input\_vpc\_security\_group\_ids) | Ids del sg del ec2 | `list(string)` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Arn del ec2 |
| <a name="output_id"></a> [id](#output\_id) | Id del ec2 |
<!-- END_TF_DOCS -->