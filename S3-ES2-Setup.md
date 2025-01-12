Here's a well-documented S3 and EC2 setup guide for GitHub:

---

## **AWS S3 and EC2 Setup Documentation**

### **Table of Contents**

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Setting Up S3](#setting-up-s3)
4. [Setting Up EC2](#setting-up-ec2)
5. [Connecting S3 and EC2](#connecting-s3-and-ec2)
6. [Conclusion](#conclusion)

---

### **1. Introduction**

This guide walks through the process of setting up:

- **S3 (Simple Storage Service)** for scalable storage.
- **EC2 (Elastic Compute Cloud)** for on-demand virtual servers.

By the end, you'll have a functioning EC2 instance with access to your S3 bucket.

---

### **2. Prerequisites**

- **AWS Account**: Ensure you have an AWS account. [Sign up here](https://aws.amazon.com/).
- **IAM User**: Set up an IAM user with Administrator or specific permissions for S3 and EC2.
- **AWS CLI**: Install AWS CLI on your local machine. [Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

---

### **3. Setting Up S3**

1. **Login to AWS Console**

   - Go to the **S3 Dashboard** from the AWS Management Console.

2. **Create an S3 Bucket**

   - Click on **Create Bucket**.
   - **Bucket Name**: Use a globally unique name (e.g., `my-project-bucket`).
   - **Region**: Select your preferred AWS region.
   - Enable or disable **Bucket Versioning** as needed.
   - Leave other settings default unless necessary.
   - Click **Create Bucket**.

3. **Configure Bucket Permissions**

   - Go to the **Permissions** tab.
   - Adjust public access and bucket policies:
     - For private buckets: Keep **"Block all public access"** enabled.
     - For public buckets: Configure bucket policy to allow public reads.

4. **Test the Bucket**
   - Upload a test file to verify the bucket works as expected.

---

### **4. Setting Up EC2**

1. **Login to AWS Console**

   - Go to the **EC2 Dashboard**.

2. **Launch an EC2 Instance**

   - Click **Launch Instance**.
   - **Name**: Enter a name for your instance (e.g., `my-project-ec2`).
   - **AMI**: Select Amazon Linux 2 or Ubuntu (or any preferred OS).
   - **Instance Type**: Choose an instance type (e.g., `t2.micro` for free tier).
   - **Key Pair**:
     - Create or use an existing key pair.
     - Download the `.pem` file and store it securely.
   - **Security Group**:
     - Allow SSH (port 22) and HTTP/HTTPS traffic (ports 80/443).
   - Click **Launch Instance**.

3. **Connect to the Instance**
   - Locate the instance's public IP.
   - Use SSH to connect:
     ```bash
     ssh -i path/to/your-key.pem ec2-user@your-ec2-public-ip
     ```

---

### **5. Connecting S3 and EC2**

1. **Install AWS CLI on EC2**

   - SSH into the EC2 instance.
   - Install AWS CLI:
     ```bash
     sudo yum update -y
     sudo yum install -y aws-cli
     ```
   - Verify installation:
     ```bash
     aws --version
     ```

2. **Configure AWS CLI**

   - Set up AWS CLI with credentials:
     ```bash
     aws configure
     ```
     Enter your **Access Key**, **Secret Key**, **Region**, and output format (e.g., `json`).

3. **Grant EC2 Access to S3**

   - Go to **IAM Dashboard**.
   - Create an **IAM Role**:
     - Trusted entity: EC2.
     - Permissions: Attach the **AmazonS3FullAccess** policy.
   - Attach the role to your EC2 instance.

4. **Test S3 Access**
   - Run the following on your EC2 instance:
     ```bash
     aws s3 ls
     ```
     You should see a list of your S3 buckets.

---

### **6. Conclusion**

You now have:

- An S3 bucket for storage.
- An EC2 instance with AWS CLI configured.
- EC2 instance permissions to access your S3 bucket.
