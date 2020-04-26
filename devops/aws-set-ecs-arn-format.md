# Update AWS ECS Account Settings to Support Long ARN Formats

AWS is a pain and they have a long window for updating this no-brainer setting. Without the below commands, AWS throws some odd errors back at Terraform when trying to do ECS deployments. The should be run on all accounts within an organization immediately after creation to fix the issue:

```bash
aws ecs put-account-setting-default --name serviceLongArnFormat --value enabled
aws ecs put-account-setting-default --name taskLongArnFormat --value enabled
aws ecs put-account-setting-default --name containerInstanceLongArnFormat --value enabled
```
