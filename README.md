# AWS VPC Terraform Module

A simple, reusable Terraform module for creating AWS VPCs with public and private subnets.

## Features

- VPC with configurable CIDR block
- Public subnets with Internet Gateway
- Private subnets with dedicated route tables
- Configurable DNS settings
- Flexible tagging support

## Usage

```hcl
module "vpc" {
  source = "github.com/[your-username]/module-terraform-vpc?ref=v1.0.1"

  vpc_name           = "my-vpc"
  vpc_cidr           = "10.0.0.0/16"
  availability_zones = ["us-east-1a", "us-east-1b"]

  public_subnet_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnet_cidrs = ["10.0.10.0/24", "10.0.20.0/24"]

  module_version = "v1.0.1"

  tags = {
    Environment = "production"
    ManagedBy   = "terraform"
  }
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| vpc_name | Name of the VPC | `string` | n/a | yes |
| vpc_cidr | CIDR block for the VPC | `string` | `"10.0.0.0/16"` | no |
| availability_zones | List of availability zones | `list(string)` | n/a | yes |
| public_subnet_cidrs | CIDR blocks for public subnets | `list(string)` | `[]` | no |
| private_subnet_cidrs | CIDR blocks for private subnets | `list(string)` | `[]` | no |
| enable_dns_hostnames | Enable DNS hostnames in the VPC | `bool` | `true` | no |
| enable_dns_support | Enable DNS support in the VPC | `bool` | `true` | no |
| module_version | Version tag for the module (e.g., v1.0.1) | `string` | `"v1.0.1"` | no |
| tags | Additional tags for all resources | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| vpc_id | ID of the VPC |
| vpc_cidr | CIDR block of the VPC |
| public_subnet_ids | IDs of public subnets |
| private_subnet_ids | IDs of private subnets |
| internet_gateway_id | ID of the Internet Gateway |
| public_route_table_id | ID of the public route table |
| private_route_table_ids | IDs of private route tables |

## Examples

See the [examples/basic](examples/basic) directory for a complete example.

## Versioning

This module follows semantic versioning. Use Git tags to reference specific versions:

```hcl
source = "github.com/[your-username]/module-terraform-vpc?ref=v1.0.1"
```

## Requirements

- Terraform >= 1.0
- AWS Provider >= 4.0

## License

See LICENSE file for details.
