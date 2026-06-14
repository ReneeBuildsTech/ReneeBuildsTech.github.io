# Portfolio Site Architecture & AWS Deployment Guide

This document outlines the strategic blueprint for building, securing, and deploying a multi-site portfolio infrastructure. The architecture utilizes a hybrid model: local visual design transitioning into a hardened, zero-trust static frontend served via AWS.

---

## 🌐 Component Architecture Roles

* **Design Engine:** WordPress + Elementor Pro (Executed strictly in a local sandbox via LocalWP).
* **Compilation Layer:** Static export compilation (Scraping dynamic PHP/MySQL into flat HTML/CSS/JS).
* **Storage Layer:** Amazon S3 (Configured with private access vectors only).
* **Edge Delivery & Security:** Amazon CloudFront + Origin Access Control (OAC) + AWS Certificate Manager (ACM).
* **DNS Management:** Amazon Route 53.

---

## 🏗️ Secure Static Site AWS Checklist

### 1. The Build Phase (Local sandbox)
- [ ] **Local Environment:** Initialize LocalWP and establish a local site instance.
- [ ] **Core Activation:** Install core Elementor followed by the Elementor Pro zip package via plugin upload.
- [ ] **Design Execution:** Apply the "Compliance Blue" template kit (Deep Navy `#0A1A3C`, Slate Grey, Digital Cyan `#00D2FF`).
- [ ] **Static Compilation:** Run an export plugin to compile the flat web asset directory.

### 2. The Storage Phase (Amazon S3)
- [ ] **Bucket Provisioning:** Create an S3 bucket matching the target canonical domain (e.g., `www.yourname.com`).
- [ ] **Public Blockade:** Keep "Block all public access" explicitly enabled on the bucket to enforce zero-trust bounds.
- [ ] **Asset Ingestion:** Upload the flat exported directory directly to the root of the S3 bucket.

### 3. The Delivery Phase (CloudFront & ACM)
- [ ] **TLS/SSL Encryption:** Provision a public SSL certificate via AWS Certificate Manager (ACM) within the `us-east-1` region.
- [ ] **Distribution Creation:** Create an Amazon CloudFront distribution mapping the S3 bucket as the origin.
- [ ] **Origin Access Control (OAC):** Restrict S3 bucket access explicitly to the CloudFront distribution identity, preventing origin-bypass traffic.
- [ ] **Root Object Resolution:** Explicitly declare `index.html` as the default root object.

### 4. The Edge Routing Phase (Route 53)
- [ ] **Hosted Zone Allocation:** Initialize a public hosted zone for the domain namespace.
- [ ] **Alias Record Mapping:** Inject an authoritative 'A' Alias record mapping the apex and subdomains directly to the CloudFront edge distribution CNAME.

---

## 📊 Site Structure Map