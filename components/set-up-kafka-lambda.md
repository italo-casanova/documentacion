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
| <a name="input_iam_role_lambda_arn"></a> [iam\_role\_lambda\_arn](#input\_iam\_role\_lambda\_arn) | ARN del role para que una lambda se ejecute en uan VPC | `string` | n/a | yes |
| <a name="input_instance_id_kafka1"></a> [instance\_id\_kafka1](#input\_instance\_id\_kafka1) | id de la priemra instancia del cluster kafka | `any` | n/a | yes |
| <a name="input_instance_id_kafka2"></a> [instance\_id\_kafka2](#input\_instance\_id\_kafka2) | id de la segunda instancia del cluster kafka | `any` | n/a | yes |
| <a name="input_lambda_function_name"></a> [lambda\_function\_name](#input\_lambda\_function\_name) | Nombre del la función lambda | `string` | `"kafka_setup"` | no |
| <a name="input_lambda_sg_ids"></a> [lambda\_sg\_ids](#input\_lambda\_sg\_ids) | Ids de los grupo de seguridad de la lambda | `list(string)` | n/a | yes |
| <a name="input_lambda_subnets_id"></a> [lambda\_subnets\_id](#input\_lambda\_subnets\_id) | Subnets donde se puede ejecutar la lambda | `list(string)` | <pre>[<br/>  "subnet-0df38652588ba4da5",<br/>  "subnet-0dc5efbdaa7d5b864"<br/>]</pre> | no |
| <a name="input_private_ip_kafka1"></a> [private\_ip\_kafka1](#input\_private\_ip\_kafka1) | private ip de la instancia de kafka | `any` | n/a | yes |
| <a name="input_private_ip_kafka2"></a> [private\_ip\_kafka2](#input\_private\_ip\_kafka2) | ip privada de la instancia de kafka | `any` | n/a | yes |

## Outputs

No outputs.
