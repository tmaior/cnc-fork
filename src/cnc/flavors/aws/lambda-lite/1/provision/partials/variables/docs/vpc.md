###########################
# VPC
###########################

#### `create_vpc`

- **Description**: Controls if VPC should be created (affects almost all resources).
- **Type**: `bool`
- **Default**: `true`
  - Determines whether to create the VPC or not.

#### `cidr`

- **Description**: (Optional) The IPv4 CIDR block for the VPC.
- **Type**: `string`
- **Default**: `"10.0.0.0/16"`
  - Specifies the CIDR block for the VPC. Can be explicitly set or derived from IPAM using `ipv4_netmask_length` & `ipv4_ipam_pool_id`.

#### `azs`

- **Description**: A list of availability zones names or ids in the region.
- **Type**: `list(string)`
- **Default**: `["{{ env_collection.region | default('us-east-1') }}a", "{{ env_collection.region | default('us-east-1') }}b", "{{ env_collection.region | default('us-east-1') }}c"]`
  - Lists the availability zones to use for subnet creation within the specified region.

#### `enable_dns_hostnames`

- **Description**: Should be true to enable DNS hostnames in the VPC.
- **Type**: `bool`
- **Default**: `true`
  - Controls whether DNS hostnames are enabled for the VPC.

#### `enable_dns_support`

- **Description**: Should be true to enable DNS support in the VPC.
- **Type**: `bool`
- **Default**: `true`
  - Controls whether DNS support is enabled for the VPC.

#### `vpc_tags`

- **Description**: Additional tags for the VPC.
- **Type**: `map(string)`
- **Default**: `{}`
  - Provides additional tags to apply to the VPC resources.

#### `tags`

- **Description**: A map of tags to add to all resources.
- **Type**: `map(string)`
- **Default**: `{}`
  - Specifies common tags to apply across all resources within the VPC.

###########################
# Public Subnets
###########################

#### `public_subnets`

- **Description**: A list of public subnets inside the VPC.
- **Type**: `list(string)`
- **Default**: `["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]`
  - Lists the CIDR blocks for the public subnets.

#### `create_multiple_public_route_tables`

- **Description**: Indicates whether to create a separate route table for each public subnet.
- **Type**: `bool`
- **Default**: `false`
  - Determines if separate route tables should be created for each public subnet.

#### `public_subnet_names`

- **Description**: Explicit values to use in the Name tag on public subnets. If empty, Name tags are generated.
- **Type**: `list(string)`
- **Default**: `[]`
  - Specifies names for public subnets; autogenerated if empty.

#### `public_subnet_suffix`

- **Description**: Suffix to append to public subnets names.
- **Type**: `string`
- **Default**: `"public"`
  - Specifies the suffix to append to public subnet names.

#### `public_subnet_tags`

- **Description**: Additional tags for the public subnets.
- **Type**: `map(string)`
- **Default**: `{ Tier = "public" }`
  - Provides additional tags to apply to the public subnets.

#### `public_subnet_tags_per_az`

- **Description**: Additional tags for the public subnets where the primary key is the AZ.
- **Type**: `map(map(string))`
- **Default**: `{}`
  - Provides additional tags to apply to public subnets, categorized by availability zone.

#### `public_route_table_tags`

- **Description**: Additional tags for the public route tables.
- **Type**: `map(string)`
- **Default**: `{}`
  - Provides additional tags to apply to the public route tables.

###########################
# Private Subnets
###########################

#### `private_subnets`

- **Description**: A list of private subnets inside the VPC.
- **Type**: `list(string)`
- **Default**: `["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]`
  - Lists the CIDR blocks for the private subnets.

#### `private_subnet_names`

- **Description**: Explicit values to use in the Name tag on private subnets. If empty, Name tags are generated.
- **Type**: `list(string)`
- **Default**: `[]`
  - Specifies names for private subnets; autogenerated if empty.

#### `private_subnet_suffix`

- **Description**: Suffix to append to private subnets names.
- **Type**: `string`
- **Default**: `"private"`
  - Specifies the suffix to append to private subnet names.

#### `private_subnet_tags`

- **Description**: Additional tags for the private subnets.
- **Type**: `map(string)`
- **Default**: `{ Tier = "private" }`
  - Provides additional tags to apply to the private subnets.

#### `var.{{ environment.name }}_{{environment.collection.instance_name}}_private_subnet_tags_per_az`

- **Description**: Additional tags for the private subnets where the primary key is the AZ.
- **Type**: `map(map(string))`
- **Default**: `{}`
  - Provides additional tags to apply to private subnets, categorized by availability zone.

#### `private_route_table_tags`

- **Description**: Additional tags for the private route tables.
- **Type**: `map(string)`
- **Default**: `{}`
  - Provides additional tags to apply to the private route tables.

###########################
# Internet Gateway
###########################

#### `create_igw`

- **Description**: Controls if an Internet Gateway is created for public subnets and the related routes that connect them.
- **Type**: `bool`
- **Default**: `true`
  - Determines whether to create an Internet Gateway for public subnets.

#### `create_egress_only_igw`

- **Description**: Controls if an Egress Only Internet Gateway is created and its related routes.
- **Type**: `bool`
- **Default**: `true`
  - Determines whether to create an Egress Only Internet Gateway.

#### `igw_tags`

- **Description**: Additional tags for the internet gateway.
- **Type**: `map(string)`
- **Default**: `{}`
  - Provides additional tags to apply to the internet gateway.

###########################
# NAT Gateway
###########################

#### `enable_nat_gateway`

- **Description**: Should be true if you want to provision NAT Gateways for each of your private networks.
- **Type**: `bool`
- **Default**: `true`
  - Controls whether NAT Gateways are provisioned for private networks.

#### `nat_gateway_destination_cidr_block`

- **Description**: Used to pass a custom destination route for private NAT Gateway.
- **Type**: `string`
- **Default**: `"0.0.0.0/0"`
  - Specifies the destination route for the NAT Gateway.

#### `single_nat_gateway`

- **Description**: Should be true if you want to provision a single shared NAT Gateway across all of your private networks.
- **Type**: `bool`
- **Default**: `true`
  - Controls whether a single shared NAT Gateway is provisioned.

#### `one_nat_gateway_per_az`

- **Description**: Should be true if you want only one NAT Gateway per availability zone.
- **Type**: `bool`
- **Default**: `false`
  - Controls whether one NAT Gateway is provisioned per availability zone.

#### `reuse_nat_ips`

- **Description**: Should be true if you don't want EIPs to be created for your NAT Gateways and will instead pass them in via the 'external_nat_ip_ids' variable.
- **Type**: `bool`
- **Default**: `false`
  - Controls whether existing EIPs are used for NAT Gateways.

#### `external_nat_ip_ids`

- **Description**: List of EIP IDs to be assigned to the NAT Gateways (used in combination with `reuse_nat_ips`).
- **Type**: `list(string)`
- **Default**: `[]`
  - Specifies EIP IDs for NAT Gateways if `reuse_nat_ips` is true.

#### `external_nat_ips`

- **Description**: List of EIPs to be used for `nat_public_ips` output (used in combination with `reuse_nat_ips` and `external_nat_ip_ids`).
- **Type**: `list(string)`
- **Default**: `[]`
  - Specifies EIPs for NAT Gateways if `reuse_nat_ips` is true.

#### `nat_gateway_tags`

- **Description**: Additional tags for the NAT gateways.
- **Type**: `map(string)`
- **Default**: `{}`
  - Provides additional tags to apply to the NAT gateways.

#### `nat_eip_tags`

- **Description**: Additional tags for the NAT EIP.
- **Type**: `map(string)`
- **Default**: `{}`
  - Provides additional tags to apply to the NAT EIP.

#### `add_security_groups`

- **Description**: List of security groups to create.
- **Type**: `list(object({ name = string, ingress = list(object({ from_port = number, to_port = number, protocol = string, cidr_blocks = list(string) })) }))`
- **Default**: `[]`
  - Specifies the security groups and their ingress rules to create.
