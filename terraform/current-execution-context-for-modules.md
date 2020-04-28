# Get current execution context for modules

It's typical to build a module which requires the module caller's `region` or `account_id` as these are typically needed for ARNs or for certain regional services (like S3 buckets). It's possible (and sometimes smart) to accept those in via variables, but it is also possible to fetch them using the following:

```hcl
data "aws_region" "current" {}
data "aws_caller_identity" "current" {}

locals {
  region     = coalesce(var.region, data.aws_region.current.name)
  account_id = data.aws_caller_identity.current.account_id
}
```
