# Saikiran Pattipaka | Personal Website & Resume

Welcome to my personal website repository! This site showcases my professional resume, skills, projects, and contact information, built with HTML, CSS, and JavaScript.

---

## Table of Contents

- [About](#about)  
- [Features](#features)  
- [Technologies](#technologies)  
- [Project Structure](#project-structure)  
- [Hosting on AWS](#hosting-on-aws)  
  - [Using S3 Static Website Hosting](#using-s3-static-website-hosting)  
  - [Using EC2](#using-ec2)  
- [Usage](#usage)  
- [Contact](#contact)  

---

## About

This repository contains the full source code for my personal website that includes:

- A hero section with animated typing text  
- Professional summary and detailed skills  
- Work experience and project highlights  
- Education background  
- Contact info with links to LinkedIn and GitHub  
- Downloadable resume PDF  
- Responsive design and smooth animations  

---

## Features

- Clean and modern UI with gradient background animation  
- Animated typing effect showcasing multiple roles and skills  
- Downloadable resume button  
- Responsive layout for mobile and desktop  
- Hosted images and assets for professional appearance  

---

## Technologies

- **HTML5** for markup  
- **CSS3** (Flexbox, animations) for styling  
- **JavaScript** for dynamic typing animation  
- Google Fonts for typography  
- SVG icons for LinkedIn and GitHub  

---

## Project Structure
```
/ (root)
├── index.html # Main HTML page
├── style.css # Stylesheet
├── script.js # JavaScript typing animation
├── profile.jpg # Profile photo
├── resume.pdf # Resume file
└── README.md # This documentation
```
---

## Hosting on AWS

You can deploy this website easily on AWS using either **S3** or **EC2** depending on your requirements.

### Using S3 Static Website Hosting (Recommended for Static Sites)

1. **Create an S3 Bucket**  
   - Go to AWS S3 console.  
   - Create a new bucket (e.g., `saikiran-website`) with a unique name.  
   - Disable **Block all public access** so the bucket can serve public files.

2. **Upload Files**  
   - Upload all your website files: `index.html`, `style.css`, `script.js`, `profile.jpg`, `resume.pdf` to the bucket.

3. **Enable Static Website Hosting**  
   - Go to the bucket properties.  
   - Enable **Static website hosting**.  
   - Set the **Index document** to `index.html`.

4. **Set Bucket Policy for Public Read Access**  
   - Add a bucket policy to allow public read of objects:

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::your-bucket-name/*"
           }
       ]
   }


5. **Using CloudFront CDN**
   - To make your website faster and enable HTTPS, set up Amazon CloudFront:
   - Go to CloudFront Console > Create Distribution
   - Set Origin Domain to your S3 static website endpoint (e.g., saikiran.dev.s3-website.ap-south-1.amazonaws.com)
   - Set Viewer Protocol Policy: Redirect HTTP to HTTPS
   - Cache Policy: Use “CachingOptimized” (for fast resume/photo loads)
   - Alternate Domain Names (CNAMEs): Add your domain (e.g., www.saikiran.dev)
   - Add SSL Certificate:
   - Use AWS Certificate Manager (ACM) to request a free SSL cert
   - Validate via DNS or Email
   - Deploy
   - ✅ Bonus: CloudFront caches resume/photo/script content at edge locations = fast global delivery!


6. **Using Route 53 for Custom Domain**
   - To connect your domain (e.g., saikiran.dev or saikiran.in):
   - Register a Domain (via Route 53 or external registrar like GoDaddy)
   - Create a Hosted Zone in Route 53
   - Add a Record Set (A or CNAME)
   - Type: A Record (Alias)
   - Alias: Yes
   - Alias Target: Your CloudFront Distribution DNS
If using external registrar:
   - Update NS records in domain settings to match Route 53’s hosted zone
   - Wait for DNS to propagate (may take 5–30 mins)
     
7. **Access your website**
   - Enter your domain name to access your website.

### Using EC2 (More Control, Suitable for Dynamic Backends)

1. **Launch an EC2 instance**
   - Choose Amazon Linux 2 or Ubuntu Server AMI.
   - Configure security group to allow HTTP (port 80) inbound traffic.
   - Connect to your EC2 instance
   - SSH into the instance using your key pair.

2. **Install a web server**
   - For example, install Apache or Nginx:
```
sudo yum update -y            # Amazon Linux
sudo yum install httpd -y     # Install Apache
sudo systemctl start httpd
sudo systemctl enable httpd
```

3. **Upload website files**
   - You can use scp or SFTP to transfer files to /var/www/html (default Apache root).
   - Example using scp:

```
scp -i your-key.pem -r * ec2-user@your-ec2-public-ip:/var/www/html/
```

   - Set proper permissions
```
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html
```

4. **Access your website**
   - Open your EC2 instance's public IP or public DNS in a browser.
```
git clone https://github.com/saikiranpattipaka/your-repo.git
cd your-repo
python3 -m http.server
```
---
### Usage
```
git clone https://github.com/saikiranpattipaka/your-repo.git
cd your-repo
python3 -m http.server
```
 - Then open http://localhost:8000 in your browser

---
### contact
   - 📬 Contact
   - 📧 Email: saikiranpattipaka@outlook.com
   - 🔗 LinkedIn: linkedin.com/in/saikiranpattipaka
   - 🐙 GitHub: github.com/saikiranpattipaka
