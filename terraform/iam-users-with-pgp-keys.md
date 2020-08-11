# Encrypt IAM user creds using PGP Keys -- Commands + HCL

Here are the relevent commands for creating, outputting, and using a PGP for IAM User Secret encryption:

1. gpg --generate-key
1. gpg --output ./pub_keys/public-key-binary.gpg --export $KEYS_EMAIL
1. Terraform Code:
    ```hcl
    data "local_file" "pgp_key" {
        filename = "./pub_keys/public-key-binary.gpg"
    }

    module "user" {
        source  = "terraform-aws-modules/iam/aws//modules/iam-user"
        version = "~> 2.0"

        name    = "$USERNAME"
        pgp_key = data.local_file.pgp_key.content_base64

        force_destroy                 = true
        create_user                   = true
        create_iam_access_key         = true
        create_iam_user_login_profile = false
        upload_iam_user_ssh_key       = false
    }

    output "user_decrypt_secret_key_command" {
        value = <<EOF
    echo "${module.user.this_iam_access_key_encrypted_secret}" | base64 --decode | gpg --decrypt
    EOF
    }

    output "user_access_key" {
        value = module.user.this_iam_access_key_id
    }
    ```

More Info: https://menendezjaume.com/post/gpg-encrypt-terraform-secrets/