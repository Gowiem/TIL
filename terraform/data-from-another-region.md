# Data From Another Region than the Default Provider
Date: 03/16/20

Typically, you use the Terraform `data` source object to obtain information about an already created object in your default provider. For AWS, you specify a region to your provider so your default provider corresponds to a particular region like `us-west-1` or `us-east-2`. This for example will read the ACM cert for the domain example.com from the `us-east-2` region:

```hcl
provider "aws" {
  region = "us-east-2"
}

data "aws_acm_certificate" "default" {
  domain = "example.com"
}

## data.aws_acm_certificate.default.arn => ARN of the example.com cert in us-east-2
```

But if you need to read in a cert to come from a different region then you need to specify a second provider which specifies that region and then use the [`data.provider`](https://www.terraform.io/docs/configuration/resources.html#provider-selecting-a-non-default-provider-configuration) attribute to inform Terraform to read that data from that second provider. Example:


```hcl
provider "aws" {
  region = "us-east-2"
}

provider "aws" {
  region = "us-west-2"
  alias  = "oregon"
}

data "aws_acm_certificate" "default" {
  domain = "example.com"
}

data "aws_acm_certificate" "oregon" {
  domain   = "example.com"
  provider = aws.oregon
}


## data.aws_acm_certificate.default.arn => ARN of the example.com cert in us-east-2
## data.aws_acm_certificate.oregon.arn => ARN of the example.com cert in us-west-2
```
