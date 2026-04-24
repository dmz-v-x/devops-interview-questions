### Question  
Suppose I have one running server in AWS on which my internet-facing e-commerce application is running. The application needs to show product pictures on the portal and all these pictures are stored in an S3 bucket. Now on the portal product pictures are not reflecting. What will be your basic approach to troubleshoot this?

---

### 1. Check S3 Bucket Permissions

The first thing to verify is that your S3 bucket and objects have the correct permissions for public access or that your EC2 instance has the necessary permissions to access the S3 bucket.

#### Check Object Permissions:

- Go to the AWS S3 Console.  
- Select the S3 bucket where the images are stored.  
- Check the permissions of the individual product image files. If they are set to private, they may not be accessible publicly.  

You can make images publicly accessible by modifying their ACL (Access Control List) to allow public read access or by ensuring the S3 bucket policy allows public access to the object.

#### Example Bucket Policy:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<your-bucket-name>/*"
        }
    ]
}
```

---

#### Check Bucket Policy:

Ensure your S3 bucket policy allows the EC2 instance or your application to read from the bucket.

If you’re using IAM roles, ensure that the EC2 instance has the correct IAM policy allowing `s3:GetObject` access to the S3 bucket.

#### Example IAM Policy for EC2 Role:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<your-bucket-name>/*"
        }
    ]
}
```

---

### 2. Verify the Image URLs in the Application

#### Check Image URLs:

Ensure that the URLs used in the application to display the product pictures are correct and point to the right location in the S3 bucket.

Format:
```
https://<bucket-name>.s3.amazonaws.com/<image-path>
```

Make sure the product pictures are being served with the correct path and filename.

---

#### Test URLs Directly:

- Copy the image URL and paste it into a browser.  
- If the image loads → issue is in application  
- If it doesn't load → issue is with permissions or URL  

---

### 3. Check CloudFront (if used)

If your application uses Amazon CloudFront:

#### Check Cache:

CloudFront might cache:
- Old images  
- 404 errors  

Invalidate cache:
```bash
aws cloudfront create-invalidation --distribution-id <your-cloudfront-id> --paths "/path/to/image.jpg"
```

---

#### Check Permissions:

Ensure CloudFront has access to S3 via:
- Origin Access Identity (OAI)

---

### 4. Check for Application Bugs

Possible issues:

- Incorrect file paths  
- Wrong S3 URL generation  
- Application-level caching issues  

#### Actions:

- Check database paths  
- Verify dynamic URL generation  
- Check logs for errors  

---

### 5. Check Security Group and Network Configuration

#### Verify:

- EC2 security group allows outbound traffic  
- No firewall blocking S3 access  

---

#### IAM Role:

Ensure EC2 has correct IAM role with S3 permissions  

#### Test from EC2:

```bash
aws s3 ls s3://<your-bucket-name>/
```

---

### 6. Check for DNS / Configuration Issues

#### DNS:

- Ensure domain (e.g., images.domain.com) points correctly  

---

#### CORS Configuration:

If frontend and S3 are on different domains:

```xml
<CORSRule>
  <AllowedOrigin>*</AllowedOrigin>
  <AllowedMethod>GET</AllowedMethod>
  <AllowedHeader>*</AllowedHeader>
</CORSRule>
```

---

### 7. Monitor with CloudWatch Logs (Optional)

- Check logs for:
  - 403 errors  
  - 404 errors  
  - Timeouts  

---

### 8. Check for S3 Versioning (If Enabled)

- Ensure correct version of image is being accessed  
- CloudFront/app may cache old version  

---

### 9. Test Image Upload

- Upload a new image manually  
- Test access  

#### Outcome:
- Works → issue with old images  
- Fails → issue with permissions or setup  

---

### Summary

- Check S3 permissions and policies  
- Verify URLs  
- Check CloudFront caching  
- Debug application code  
- Validate IAM roles and networking  
- Test and monitor logs  

---

By following this approach, you can systematically identify whether the issue lies in S3 permissions, application logic, networking, or caching layers.

---

---

### Question  
How do you automate the creation of an EC2 instance and install Apache on it using a user data script?

---

### Answer

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = "ami-08c40ec9ead489470" # Amazon Linux 2 AMI (region-specific)
  instance_type = "t2.micro"
  key_name      = "my-keypair"

  # Security group to allow HTTP
  vpc_security_group_ids = [aws_security_group.web_sg.id]

  # User data script to install Apache
  user_data = <<-EOF
              #!/bin/bash
              yum update -y
              yum install -y httpd
              systemctl start httpd
              systemctl enable httpd
              echo "<h1>Hello from Terraform + Apache</h1>" > /var/www/html/index.html
              EOF

  tags = {
    Name = "Terraform-Apache-Server"
  }
}

resource "aws_security_group" "web_sg" {
  name        = "web-sg"
  description = "Allow HTTP and SSH"

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
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
```

---

### Key Points

- `user_data` runs at instance startup  
- Installs Apache (`httpd`)  
- Starts and enables the service  
- Creates a sample HTML page  
- Security group allows HTTP (port 80) and SSH (port 22)  

---

### Interview-Ready Summary

“To automate EC2 creation with Apache installation, I use Terraform with a user_data script. The script runs during instance startup, installs Apache, starts the service, and deploys a sample web page. I also configure a security group to allow HTTP and SSH access.”
