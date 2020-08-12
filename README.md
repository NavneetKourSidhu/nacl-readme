# terraform-AWS-NACL

Network ACL for the VPC

##Usage

```
resource "aws_network_acl" "main" {
  vpc_id = aws_vpc.main.id

  egress {
    protocol   = "tcp"
    rule_no    = 200
    action     = "allow"
    cidr_block = "10.3.0.0/18"
    from_port  = 443
    to_port    = 443
  }

  ingress {
    protocol   = "tcp"
    rule_no    = 100
    action     = "allow"
    cidr_block = "10.3.0.0/18"
    from_port  = 80
    to_port    = 80
  }

  tags = {
    Name = "main"
  }
}
```

##Variables

* vpc_id - (Required) The ID of the associated VPC.
* subnet_ids - (Optional) A list of Subnet IDs to apply the ACL to
* ingress - (Optional) Specifies an ingress rule. Parameters defined below. This argument is processed in attribute-as-blocks mode.
* egress - (Optional) Specifies an egress rule. Parameters defined below. This argument is processed in attribute-as-blocks mode.
* tags - (Optional) A map of tags to assign to the resource.

Both egress and ingress support the following keys:

* from_port - (Required) The from port to match.
* to_port - (Required) The to port to match.
* rule_no - (Required) The rule number. Used for ordering.
* action - (Required) The action to take.
* protocol - (Required) The protocol to match. If using the -1 'all' protocol, you must specify a from and to port of 0.
* cidr_block - (Optional) The CIDR block to match. This must be a valid network mask.

##Outputs

* id - The ID of the network ACL
* arn - The ARN of the network ACL
* owner_id - The ID of the AWS account that owns the network ACL.


 
