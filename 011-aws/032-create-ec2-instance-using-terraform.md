### Question  
Create an EC2 instance using Terraform

---

### Answer  

#### main.tf

```hcl
# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

# Create a Security Group to allow SSH
resource "aws_security_group" "ec2_sg" {
  name        = "ec2_sg"
  description = "Allow SSH inbound traffic"

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Create an EC2 Instance
resource "aws_instance" "my_ec2" {
  ami           = "ami-08c40ec9ead489470" # Example Amazon Linux 2 AMI ID for us-east-1
  instance_type = "t2.micro"
  key_name      = "my-keypair"           # Pre-created SSH key in AWS

  vpc_security_group_ids = [aws_security_group.ec2_sg.id]

  tags = {
    Name = "Terraform-EC2"
  }
}
```

---

### Commands to Apply

```bash
terraform init     # Initialize provider plugins
terraform plan     # Preview changes
terraform apply    # Create resources
```

---

### Best Practices

- Store state in a remote backend (e.g., S3 with DynamoDB locking)  
- Use variables for AMI, instance type, and key pair instead of hardcoding  
- Add outputs (e.g., public IP) for easy access after provisioning  

---

### Interview-Ready Summary

“To create an EC2 instance using Terraform, I define the AWS provider, create a security group to allow SSH access, and then define an aws_instance resource with AMI, instance type, key pair, and security group. After writing the configuration, I run terraform init, plan, and apply to provision the infrastructure. I also follow best practices like using remote state and variables for flexibility.”
