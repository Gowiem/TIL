# Create NAT Gateway for allowing AWS Lambda Function to connect to outside world

AWS Lambda functions by default don't have access to the outside web, which means your outside API calls will fail. Usually these failures are silent, which can be a bit of a head scratcher. The answer to this issue is to introduce a VPC NAT Gateway giving the Lambda Function access to the outside world by running on a VPC Subnet that funnels traffic through the NAT. This can be accomplished with the following:

1. Create new private Subnet in your desired availability zone (AZ). Give this a useful name like `$VPC_NAME.subnet.1a.priv`.
2. If this is your default VPC, you should already have a subnet for each AZ in that region, but just in case double check that you have another Subnet in the same AZ as your new private Subnet. If not then create one.
3. Create a new NAT Gateway via [NAT Gateways](https://console.aws.amazon.com/vpc/home?#NatGateways:):
  - You'll use one of your VPC's public Subnets for the NAT's Subnet. It should be in the same AZ as your new private Subnet.
  - You can choose to create a new Elastic IP address for the NAT's Allocation ID
  - Choose to go onto Editing Route Tables
4. Update route tables for the following scenario:
  - Main Route Table for the VPC should have the new private Subnet associated with it and should have one route with destination `0.0.0.0/0` and target the new NAT Gateway ID (`nat-*`).
  - Create a new route table for your VPC with name `$VPC_NAME.customtable.public`. This route table should have all existing public Subnets associated with it and have one route with destination `0.0.0.0/0` and target your existing VPC's Internet Gateway (`igw-*`).
5. Our NAT is now all setup and we just need to update our Lambda Function to run within our new private Subnet. Go to your Lambda Advanced configuration and do the following:
  - Update the VPC to the VPC you added the NAT Gateway to.
  - Your Subnet should be the new private Subnet that you created.
  - You should select a Security Group that has Outbound Rules which don't restrict internet access.

Your Lambda Function should now have access to the outside world. More info can be found [here](https://docs.aws.amazon.com/lambda/latest/dg/vpc.html).
