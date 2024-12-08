<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_archive"></a> [archive](#provider\_archive) | n/a |
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_lambda_function.lambda_function](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_function) | resource |
| [archive_file.lambda_docdb_zip](https://registry.terraform.io/providers/hashicorp/archive/latest/docs/data-sources/file) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta | `string` | n/a | yes |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | nombre corto del Bucket s3 | `string` | n/a | yes |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta | `string` | n/a | yes |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto | `string` | n/a | yes |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto | `string` | n/a | yes |
| <a name="input_docdb_cluster_endpoint"></a> [docdb\_cluster\_endpoint](#input\_docdb\_cluster\_endpoint) | Endpoint del cluster de DocumentDB | `string` | n/a | yes |
| <a name="input_docdb_cluster_port"></a> [docdb\_cluster\_port](#input\_docdb\_cluster\_port) | Puerto del cluster de DocumentDB | `string` | n/a | yes |
| <a name="input_docdb_master_user_secret_arn"></a> [docdb\_master\_user\_secret\_arn](#input\_docdb\_master\_user\_secret\_arn) | Arn del secreto que guarda las credenciales dl usuario maestro del DocumentDB | `string` | n/a | yes |
| <a name="input_ec2_instance_id"></a> [ec2\_instance\_id](#input\_ec2\_instance\_id) | Id de la instancia de ec2 que ejecuta los servicios para la restauración del MongoDB on-premise | `string` | n/a | yes |
| <a name="input_iam_role_lambda_arn"></a> [iam\_role\_lambda\_arn](#input\_iam\_role\_lambda\_arn) | ARN del role para que una lambda se ejecute en uan VPC | `string` | n/a | yes |
| <a name="input_lambda_function_name"></a> [lambda\_function\_name](#input\_lambda\_function\_name) | Nombre del la función lambda | `string` | `"docdb_management"` | no |
| <a name="input_lambda_sg_ids"></a> [lambda\_sg\_ids](#input\_lambda\_sg\_ids) | Ids de los grupo de seguridad de la lambda | `list(string)` | n/a | yes |
| <a name="input_lambda_subnet_ids"></a> [lambda\_subnet\_ids](#input\_lambda\_subnet\_ids) | Subnets donde se puede ejecutar la lambda | `list(string)` | <pre>[<br>  "subnet-0df38652588ba4da5",<br>  "subnet-0dc5efbdaa7d5b864"<br>]</pre> | no |
| <a name="input_s3_bucket_name"></a> [s3\_bucket\_name](#input\_s3\_bucket\_name) | Nombre del s3 que guarda los dumps y las operaciones para la restauración del MongoDB on-premise | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_function_name"></a> [function\_name](#output\_function\_name) | Nombre de la funcion lambda |
<!-- END_TF_DOCS -->