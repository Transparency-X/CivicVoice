Here is the **Stage 5: Technical System Design & Architecture** document. 

This document serves as the master blueprint for the Lead Developer or Chief Technology Officer (CTO). It translates the user requirements, legal constraints, and UI designs into concrete technical choices—outlining the exact software, databases, and cloud infrastructure required to build and scale CivicVoice securely.

---

# **Stage 5 Technical System Design Document: CivicVoice**

## **1. Technology Stack Selection**
To ensure the platform is fast, scalable, and maintainable by a small initial development team, we will use a modern, JavaScript/TypeScript-based stack. This allows developers to use the same language for both the user interface and the server logic.

### **A. Frontend (User Interface)**
*   **Framework:** **Next.js (React)** with TypeScript.
    *   *Why:* Next.js provides Server-Side Rendering (SSR), which is crucial for SEO (so users Googling "how to report noise in Dublin" find the platform) and ensures rapid page loads on mobile devices.
*   **Styling:** **Tailwind CSS**.
    *   *Why:* Allows for rapid translation of the Figma UI designs into responsive, accessible code.
*   **State Management:** **Zustand** or **React Context API**.

### **B. Backend (Server Logic & APIs)**
*   **Framework:** **Node.js** with **Express.js** (or NestJS for stricter architecture).
    *   *Why:* Highly scalable, handles asynchronous requests (like heavy file uploads) exceptionally well.
*   **Database ORM:** **Prisma**.
    *   *Why:* Prisma makes querying the database extremely secure, preventing SQL injection attacks, and provides excellent TypeScript autocompletion for developers.

### **C. Database & Caching**
*   **Primary Database:** **PostgreSQL** (Relational Database).
    *   *Why:* The platform relies heavily on structured relationships (User -> Cases -> Evidence -> Authorities). PostgreSQL handles this perfectly and enforces strict data integrity.
*   **Caching (Optional MVP, Required for V2):** **Redis**.
    *   *Why:* To temporarily store user session data and cache the "Authority Directory" so the database isn't queried every time someone searches for "Dublin City Council."

---

## **2. Cloud Infrastructure & Hosting Architecture**
The system will be hosted on a distributed cloud architecture to ensure high availability (99.9% uptime) and secure data separation.

*   **Frontend Hosting:** **Vercel**. Provides automatic global CDN distribution so the web app loads instantly anywhere in Ireland/EU.
*   **Backend Hosting:** **AWS (Amazon Web Services) - EC2 or App Runner**. Encapsulated in a Virtual Private Cloud (VPC) so it is not directly exposed to the public internet.
*   **Database Hosting:** **AWS RDS (Relational Database Service)**. Automated daily backups and point-in-time recovery.
*   **The Evidence Vault (Storage):** **AWS S3 (Simple Storage Service)**. 
    *   *Crucial Security Feature:* Files uploaded here will be set to "Private." The backend will generate **Pre-Signed URLs** (temporary access links that expire after e.g., 24 hours) for the "Evidence Link" shared with authorities.

---

## **3. Database Schema Design (Core Entity Relationship)**
This is the technical map of how data is stored. To comply with GDPR (Stage 2), User PII is kept cleanly severable from Case Data.

### **Table 1: `Users`**
*   `id` (UUID, Primary Key)
*   `email` (String, Unique, Encrypted)
*   `password_hash` (String, Bcrypt hashed)
*   `created_at` (Timestamp)
*   `is_active` (Boolean - allows soft bans for vexatious users)

### **Table 2: `Cases`**
*   `id` (UUID, Primary Key)
*   `user_id` (Foreign Key -> Users.id) *[Set to CASCADE DELETE so if a user deletes their account, their cases vanish]*
*   `status` (Enum: 'DRAFT', 'SENT', 'ESCALATED', 'RESOLVED')
*   `issue_category_id` (Foreign Key -> Issue_Categories.id)
*   `target_entity_name` (String - e.g., "Dunnes Stores")
*   `target_eircode` (String)

### **Table 3: `Evidence_Files`**
*   `id` (UUID, Primary Key)
*   `case_id` (Foreign Key -> Cases.id)
*   `file_name` (String)
*   `s3_bucket_key` (String - The internal path to the AWS file)
*   `file_type` (String - e.g., "video/mp4", "text/csv")
*   `external_link` (String, Nullable - If user pastes a Google Drive link instead)

### **Table 4: `Authorities` (The Directory)**
*   `id` (UUID, Primary Key)
*   `name` (String - e.g., "Health & Safety Authority")
*   `jurisdiction` (String - e.g., "National" or "Dublin")
*   `contact_email` (String)

---

## **4. Third-Party API Integrations**
To avoid reinventing the wheel, the backend will communicate with specific external services:

*   **Authentication:** **NextAuth.js** or **Auth0**. Handles secure login, password resets, and JWT (JSON Web Token) session management securely out-of-the-box.
*   **Transactional Email:** **SendGrid** or **Postmark**. 
    *   *Usage:* To send password resets, platform alerts, and "Follow-up Reminders" to the user. (Note: Initial complaints are sent *by the user* from their own email client, not the platform's email server, to avoid spam blacklisting).
*   **Geolocation & Mapping:** **Google Maps API** or **Autoaddress (Irish standard)**. 
    *   *Usage:* When a user enters "Ilac Centre, D1", the API automatically converts this to precise coordinates and an Eircode to ping the exact correct Local Authority tier.
*   **AI Text Generation (Future-Proofing for Phase 5):** **OpenAI API (GPT-4o)**.
    *   *Usage:* Later, this will be integrated so the backend can accept an angry, unformatted user rant and return a perfectly formatted, legally sound letter.

---

## **5. Security & DevSecOps Implementation**
Given the sensitive nature of disputes (e.g., whistleblowers reporting unsafe work conditions, tenants reporting landlords), security protocols must be rigorous.

### **A. Encryption Standards**
*   **In Transit:** All API traffic forced over **HTTPS/TLS 1.3**.
*   **At Rest:** Database fields containing PII (like Emails and personal addresses) encrypted using **AES-256-GCM** before being saved to the database. 

### **B. File Upload Security (Malware Protection)**
*   Users uploading CSVs and MP4s could accidentally (or maliciously) upload malware.
*   *Protocol:* Files are uploaded to an isolated "Quarantine S3 Bucket" first. An AWS Lambda function scans the file for viruses using an open-source scanner (like ClamAV). If clean, it moves to the main "Evidence Vault" bucket.
*   *Rate Limiting:* Limit file uploads to e.g., 5 files / 50MB per user per hour to prevent server DDoS attacks.

### **C. CI/CD (Continuous Integration / Continuous Deployment)**
*   **GitHub Actions:** Every time a developer writes a new feature, GitHub Actions will automatically run automated tests.
*   **Environments:** Code must pass through three stages:
    1.  *Development (Local)* -> Where devs build.
    2.  *Staging (Cloud)* -> A private clone of the site where the founders/QA test the exact flow of the "Dunnes Store Complaint" with fake data.
    3.  *Production (Live)* -> The public-facing site.

---

### **Next Steps for the Dev/Design Team based on Stage 5:**
1.  **DevOps Setup (Sprint 0):** The Lead Developer sets up the GitHub repositories, creates the AWS/Vercel accounts, and provisions the initial PostgreSQL database.
2.  **Environment Variables:** Create secure `.env` files to store all API keys (SendGrid, AWS, Maps) securely away from the main codebase.
3.  **Transition to Stage 6:** With the architecture approved, the Project Manager will take all previous documents and break them down into actionable Jira/Trello tickets to officially begin **Coding Sprints**.
