# Portfolio Site Strategy & Recommendations

## 1. Architectural Strategy
* **Framework:** Standardize on **Genesis (StudioPress)** for its lightweight, hook-based architecture. Avoid "Page Builders" (e.g., Elementor) to prevent DOM bloat, rendering lag, and unnecessary security attack surfaces.
* **Hosting:** Deploy on **AWS Lightsail or EC2** using a "Code-First" approach. This allows for manual SSH access for hardening while leveraging AWS’s robust ecosystem for backups and CDN (CloudFront) integration.
* **Hardening:** Implement basic security measures at the server level:
    * **Disable XML-RPC:** In `.htaccess` to mitigate common attack vectors.
    * **Remove WP version headers:** In `functions.php` for security through obscurity.
* **Static Site Alternative:** For maximum security and speed, consider converting your content to a static site (using **Hugo/Jekyll**) and hosting on **S3 + CloudFront** to eliminate database exploits entirely.

## 2. UI & Interaction Design
* **Layout:** Adopt a clean, grid-based aesthetic. Use this hierarchy to present projects for quick recruiter scanning.
* **Performance-First Modals:** For e-commerce needs, avoid heavy pop-up plugins. Use the native HTML5 `<dialog>` element combined with `IntersectionObserver` for lightweight, hardware-accelerated trigger logic.
* **Content Mapping:** Structure project pages to lead with **Architecture Diagrams (Mermaid/Excalidraw)**, followed by **Compliance Tables** (derived from your Asset Generator), and finish with a direct **GitHub repository link** to your `README.md`.

## 3. GRC & Compliance Dashboard
* **Structure:** Dedicate a specific section of your site to GRC. Organize this not just by project, but by **Regulatory Mapping** (e.g., NIST CSF, PCI-DSS).
* **Policy-as-Code:** Treat your GRC section as a "Knowledge Base" rather than a document repository. Create a dynamic table that maps your technical IAM implementations (P3/P4) directly to regulatory controls.
* **Evidence Repository:** Feature a "Compliance Evidence" page containing logs, snippets of remediation scripts, and structured compliance data to prove you understand auditor requirements.

## 4. Implementation Roadmap
* **Automation:** Use **Terraform** for infrastructure-as-code (S3/IAM/SNS) and **Ansible** for environment configuration (RHEL/Python runtime).
* **Metadata Strategy:** Incorporate `CONTROLS_MAPPING` objects directly into your Python automation code. This enables the site to automatically generate its own `COMPLIANCE.md` or dashboard view by crawling your own repositories.
