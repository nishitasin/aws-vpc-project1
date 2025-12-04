# aws-vpc-project1


# AWS VPC Project – Public + Private Subnets | IGW | NAT Gateway | Route Tables | S3 Static Hosting

This project demonstrates building a complete AWS network architecture manually inside AWS, including VPC, subnets, routing, NAT gateway, and S3 hosting.

---

## 🔹 VPC Configuration

| Component | Details |
|----------|---------|
| **VPC Name** | Nishita_VPC |
| **CIDR Block** | `10.0.0.0/16` |
| **Region** | ap-south-2 (Hyderabad) |

---

## 🔹 Subnets

### **Public Subnets**

| Name | CIDR |
|------|------|
| Public_Subnet_1 | `10.0.1.0/24` |
| Public_Subnet_2 | `10.0.2.0/24` |

### **Private Subnets**

| Name | CIDR |
|------|------|
| Private_Subnet_1 | `10.0.3.0/24` |
| Private_Subnet_2 | `10.0.4.0/24` |

---

## 🔹 Internet Gateway (IGW)

An Internet Gateway is attached to **Nishita_VPC** to allow public subnets to communicate with the internet.

---

## 🔹 NAT Gateway

| Attribute | Value |
|-----------|--------|
| **Subnet** | Public_Subnet_1 |
| **Connectivity** | Public |
| **Purpose** | Allows private subnets to access the internet |

---

## 🔹 Route Tables

### **Public Route Table**

| Destination | Target |
|-------------|--------|
| `0.0.0.0/0` | Internet Gateway |
| `10.0.0.0/16` | Local |

### **Private Route Table**

| Destination | Target |
|-------------|--------|
| `0.0.0.0/0` | NAT Gateway |
| `10.0.0.0/16` | Local |

✔ Both **public** subnets use the **Public Route Table**  
✔ Both **private** subnets use the **Private Route Table**

---

## 🔹 S3 Static Website Hosting

- **Bucket Name:** `nishita-website-bucket`
- Public Access → **Disabled (manually allowed via policy)**
- Static Website Hosting → **Enabled**
- Index Document → `index.html`

### **Bucket Policy Used**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::nishita-website-bucket/*"
    }
  ]
}
                 Internet
                    |
              ┌──────────────┐
              │     IGW      │
              └──────────────┘
                    |
     ┌────────────────────────────────┐
     │             VPC                │
     │          10.0.0.0/16           │
     │                                │
     │  Public Subnets                │
     │  10.0.1.0/24   10.0.2.0/24      │
     │      |              |          │
     │    EC2(Optional)   NAT-GW      │
     │                    |           │
     │  Private Subnets               │
     │  10.0.3.0/24   10.0.4.0/24      │
     │      |              |          │
     │  App Servers     Databases     │
     └────────────────────────────────┘
This repository contains the complete AWS infrastructure for:

VPC

Public & Private Subnets

Internet Gateway

NAT Gateway

Route Tables

S3 Website Hosting
==================================================

---

# 🎉 README IS READY  
You can **paste this entire block** into your GitHub `README.md`.

If you want:

✅ A folder structure  
✅ Terraform code  
✅ Architecture diagram PNG  
✅ Steps summary for your instructor  

Just say **"Give me folder structure"** or **"Give me Terraform"**.

