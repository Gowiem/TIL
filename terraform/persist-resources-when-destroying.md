# Persist certain resources during a `terraform destroy`

Using some smart `tf state` usage, you can enable keeping around certain resources during a `terraform destroy`. This is useful for keeping around KMS keys and other important resources that you want to survive a complete or partial deletion of an environment.

To do so:

1. `terraform state rm $RESOURCE_TO_KEEP`
1. `terraform plan -destroy -out=run.plan`
1. `terraform apply run.plan`
1. `terraform import $RESOURCE_TO_KEEP`


[Source](https://stackoverflow.com/a/44478759/1159410)

