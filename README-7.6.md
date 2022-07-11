# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - 7.6. Написание собственных провайдеров для Terraform.**


**1**

[data_source](https://github.com/hashicorp/terraform-provider-aws/blob/f79cc524cdaa2581c1a96cabdafc8eb04d582aa4/internal/provider/provider.go#L426) 

[resource](https://github.com/hashicorp/terraform-provider-aws/blob/f79cc524cdaa2581c1a96cabdafc8eb04d582aa4/internal/provider/provider.go#L920)



**2**

[ConflictWith](https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/resource_aws_sqs_queue.go#L51)


[если имя больше 80 символов будет ошибка](https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/validators.go#L1037)


ответ на третий пункт я так и не нашел.