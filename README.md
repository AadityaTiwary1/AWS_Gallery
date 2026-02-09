# 📸 EC2 + S3 Photo Gallery App 

A simple cloud-based photo gallery built using **Amazon EC2 and Amazon S3 only**, with a **single `index.html` frontend file** written in HTML, CSS, and JavaScript.

Users can upload photos directly from the browser, store them in S3, and view them in a public gallery hosted via an EC2 instance.

---

## 🚀 Project Overview

This project demonstrates how to build a cloud-hosted web application using only:

* **Amazon EC2** → hosts the website
* **Amazon S3** → stores uploaded photos
* **HTML + CSS + JavaScript** → frontend (single file)
* **Public bucket access (no IAM used)**

No backend server and no frameworks were used.

---

## 🧱 Architecture

```
User Browser
     ↓
EC2 Public IP (Apache Web Server)
     ↓
index.html (HTML + CSS + JS)
     ↓
Uploads via Fetch API
     ↓
Amazon S3 Bucket (Public storage)
     ↓
Images displayed in gallery
```

---

## ✨ Features

* Upload images directly from browser
* Store photos in S3 bucket
* Public gallery view
* Works using EC2 public URL
* Single frontend file
* No backend code
* No IAM configuration required
* Fully cloud-based deployment

---

## 🛠️ Technologies Used

* Amazon EC2 (Amazon Linux)
* Amazon S3
* Apache Web Server
* HTML5
* CSS3
* JavaScript (Fetch API)

---

## ⚙️ Setup Instructions

### 1) Launch EC2 Instance

* AMI: Amazon Linux
* Instance type: t2.micro
* Allow HTTP (port 80) and SSH
* Connect using SSH:

```bash
ssh -i your-key.pem ec2-user@<EC2-PUBLIC-IP>
```

---

### 2) Install Apache Web Server

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

### 3) Create S3 Bucket

* Create a new bucket
* Disable block public access
* Add bucket policy for public read & upload

Bucket policy:

```json
{
 "Version":"2012-10-17",
 "Statement":[
  {
   "Effect":"Allow",
   "Principal":"*",
   "Action":["s3:GetObject"],
   "Resource":["arn:aws:s3:::YOUR-BUCKET-NAME/*"]
  },
  {
   "Effect":"Allow",
   "Principal":"*",
   "Action":["s3:PutObject"],
   "Resource":["arn:aws:s3:::YOUR-BUCKET-NAME/*"]
  }
 ]
}
```

---

### 4) Configure CORS

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET","PUT"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": []
  }
]
```

---

### 5) Deploy Frontend to EC2

```bash
cd /var/www/html
sudo nano index.html
```

Paste the full frontend code and save.

Restart Apache:

```bash
sudo systemctl restart httpd
```

---

### 6) Access Website

Open in browser:

```
http://<EC2-PUBLIC-IP>
```

The gallery is now live.

---

## 📂 How It Works

### Upload Flow

1. User selects an image
2. JavaScript sends a PUT request to S3
3. Image stored publicly in bucket

### Gallery Flow

1. Page loads
2. JS fetches bucket objects
3. Displays images dynamically

---

## ⚠️ Security Note

This project uses **public bucket access** for simplicity and demonstration.

Anyone can:

* Upload images
* View images

Recommended only for:

* College projects
* Learning AWS
* Demo apps

Not recommended for production environments.

---

## 🎯 Use Cases

* Cloud computing academic project
* AWS hands-on practice
* Beginner DevOps deployment

---

## 👨‍💻 Author

Built as a cloud project using:

* EC2
* S3
* HTML
* CSS
* JavaScript
