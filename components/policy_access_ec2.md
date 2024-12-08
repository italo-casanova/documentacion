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
| [aws_iam_policy.lambda_access_ec2](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_account_origin"></a> [aws\_account\_origin](#input\_aws\_account\_origin) | Nombre de la cuenta de origen en AWS | `string` | `"devops"` | no |
| <a name="input_aws_account_target"></a> [aws\_account\_target](#input\_aws\_account\_target) | Nombre de la cuenta de destino en AWS | `string` | `"integration-qa"` | no |
| <a name="input_aws_project_account"></a> [aws\_project\_account](#input\_aws\_project\_account) | Nombre de la cuenta del proyecto en AWS | `string` | `"devops"` | no |
| <a name="input_aws_project_env"></a> [aws\_project\_env](#input\_aws\_project\_env) | Ambiente del proyecto (por ejemplo, dev, qa y prod) | `string` | `"develop"` | no |
| <a name="input_aws_project_id"></a> [aws\_project\_id](#input\_aws\_project\_id) | Etiqueta del proyecto en AWS | `string` | `"dca"` | no |
| <a name="input_iam_policy_lambda_access_ec2_arns"></a> [iam\_policy\_lambda\_access\_ec2\_arns](#input\_iam\_policy\_lambda\_access\_ec2\_arns) | Arn de los ec2s a los cuales la lambda se va a conectar | `list(string)` | n/a | yes |
| <a name="input_iam_policy_lambda_access_ec2_name"></a> [iam\_policy\_lambda\_access\_ec2\_name](#input\_iam\_policy\_lambda\_access\_ec2\_name) | Nombre de la política de la lambda para acceder a ec2 y ejecutar comando medioante ssm | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Arn de la política |
<!-- END_TF_DOCS -->