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
| [aws_iam_role.iam_role_lambda](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta | `string` | n/a | yes |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | nombre corto del Bucket s3 | `string` | n/a | yes |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta del proyecto en AWS | `string` | n/a | yes |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto (por ejemplo, dev, qa y prod) | `string` | n/a | yes |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto | `string` | n/a | yes |
| <a name="input_iam_role_lambda_name"></a> [iam\_role\_lambda\_name](#input\_iam\_role\_lambda\_name) | Nombre del rol de la lambda | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Arn del rol de la lambda |
| <a name="output_id"></a> [id](#output\_id) | Id del rol de lambda |
| <a name="output_name"></a> [name](#output\_name) | Nombre del rol de la lambda |
<!-- END_TF_DOCS -->