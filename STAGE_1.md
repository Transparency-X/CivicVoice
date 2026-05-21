Here is the **Stage 1: Requirements Definition & User Stories** document. This serves as the foundational blueprint for the CivicVoice platform, outlining exactly who the users are, what the software must do, and the technical standards it must meet.

---

# **Stage 1 Requirements Document: CivicVoice**

## **1. User Personas**
Understanding *who* will use the platform helps the design and development teams empathize with the user and prioritize the right features.

### **Persona A: The Frustrated Citizen/Consumer (e.g., Sarah)**
*   **Profile:** A 34-year-old professional who shops locally.
*   **The Problem:** She has identified a severe issue (e.g., a dangerously loud, high-frequency noise at a local supermarket). She has raw evidence (videos, acoustic data) but doesn't know the legal terminology or exactly which state body enforces noise regulations. Store managers are ignoring her.
*   **Platform Needs:** Needs a quick way to upload large video/CSV files, instantly find out who holds jurisdiction (e.g., Dublin City Council Noise Unit, HSA), and generate a formal email that forces corporate facilities management to act.
*   **Tech Literacy:** High. Uses smartphones for everything, comfortable with cloud storage.

### **Persona B: The Vulnerable Tenant (e.g., Liam)**
*   **Profile:** A 25-year-old renter living in an apartment with black mold and a broken fire alarm.
*   **The Problem:** His landlord ignores WhatsApp messages. Liam is anxious about confrontation and fears eviction if he says the wrong thing.
*   **Platform Needs:** Needs the platform to act as a "shield." He needs formal, legally sound letters referencing the *Housing (Standards for Rented Houses) Regulations*, and conversational scripts so he knows exactly what to say on the phone without losing his temper.
*   **Tech Literacy:** Moderate. Uses social media but finds formal/legal processes overwhelming.

### **Persona C: The Community Advocate (e.g., Elena)**
*   **Profile:** A 50-year-old neighborhood watch coordinator.
*   **The Problem:** Constantly dealing with systemic local issues (illegal dumping, unsafe road crossings). She sends dozens of emails to the local council but loses track of who replied and when.
*   **Platform Needs:** Needs a robust Case Management Dashboard to track multiple ongoing issues, log follow-up dates, and easily share the status of complaints with her community group.
*   **Tech Literacy:** Moderate. Primarily uses desktop/laptop for administrative work.

---

## **2. User Stories**
User stories are written from the perspective of the end-user. They define the required features for the development team. 

### **Epic 1: Account Management & Security**
*   **US 1.1:** As a user, I want to create an account using my email and a password so that my case history and evidence are securely saved.
*   **US 1.2:** As a user, I want to request a password reset via email so that I can regain access to my account if I forget my login.
*   **US 1.3:** As a user, I want the option to permanently delete my account and all associated data so that my privacy is protected (GDPR compliance).

### **Epic 2: The Issue Builder & Authority Mapping**
*   **US 2.1:** As a user, I want to select my issue from a categorized list (e.g., Commercial Noise, Workplace Hazard, Tenancy Dispute) so that the platform understands the context of my complaint.
*   **US 2.2:** As a user, I want to enter the location/Eircode of the issue so that the platform can identify the correct local authority or regulatory body.
*   **US 2.3:** As a user, I want the platform to recommend a "Tiered Escalation" path (e.g., 1. Branch Manager -> 2. Head Office -> 3. Health & Safety Authority) so that I know the correct order of operations.

### **Epic 3: The Evidence Vault**
*   **US 3.1:** As a user, I want to upload files (images, audio, videos, CSV data logs) to my case profile so that all my evidence is stored in one place.
*   **US 3.2:** As a user, I want to paste external links (e.g., Google Drive, Dropbox) into my case profile if my files are too large to upload directly.
*   **US 3.3:** As a user, I want the platform to generate a secure, public "Evidence Link" so that I can easily include it in my emails to authorities without dealing with email attachment limits.

### **Epic 4: Communication Engine (Letters & Scripts)**
*   **US 4.1:** As a user, I want the platform to automatically generate a formal email draft populated with my case details, location, and evidence link so that I don't have to write it from scratch.
*   **US 4.2:** As a user, I want to select the "Tone" of my letter (e.g., Friendly Inquiry, Firm Complaint, Final Legal Warning) so that the communication matches the current stage of my dispute.
*   **US 4.3:** As a user, I want the platform to generate a "Phone Call Script" with opening statements and rebuttal points so that I feel confident speaking to a manager or council worker.
*   **US 4.4:** As a user, I want to copy the generated text to my clipboard with one click so I can easily paste it into my personal email client.

### **Epic 5: Case Management Dashboard**
*   **US 5.1:** As a user, I want to view all my active and closed cases on a single dashboard so that I can quickly check their statuses.
*   **US 5.2:** As a user, I want to change the status of a case (e.g., "Drafting," "Sent," "Escalated," "Resolved") so that I can track its progress.
*   **US 5.3:** As a user, I want to log a "Follow-up Date" and receive an email reminder when it is time to escalate the issue if no one has replied.

---

## **3. Non-Functional Requirements (NFRs)**
These are the technical standards the system must meet regarding performance, security, and usability. 

### **A. Security & Data Privacy (Crucial)**
*   **GDPR Compliance:** The system must adhere strictly to EU GDPR. All user data (names, addresses, evidence) must be exportable and deletable upon user request.
*   **Encryption:** All Personally Identifiable Information (PII) must be encrypted at rest in the database (e.g., using AES-256). All web traffic must be encrypted in transit via HTTPS/TLS 1.2+.
*   **Vault Security:** Evidence links generated by the platform must be read-only. Users should have the option to set an expiration date (e.g., link expires in 30 days) on their evidence vaults.

### **B. Performance & Scalability**
*   **Mobile-First Responsiveness:** Because users will likely log issues on their phones while looking at the hazard, the web app must be fully responsive and perform flawlessly on mobile browsers (Safari, Chrome for Android).
*   **Page Load Speed:** Core pages must load in under 2.5 seconds on a standard 4G mobile connection to prevent user drop-off.
*   **File Upload Handling:** The platform must support asynchronous uploads so the UI does not freeze when uploading large HQ videos. Maximum file size for initial MVP uploads should be capped (e.g., 50MB per file), with a prompt to use external links (like Google Drive) for larger files.

### **C. Accessibility & Usability**
*   **WCAG 2.1 AA Compliance:** The platform must be accessible to people with disabilities. This includes high-contrast text, proper header structures for screen readers, and full keyboard navigability.
*   **Plain English UI:** While the *generated templates* will use legal/statutory language, the *user interface* (instructions, buttons, menus) must be written in Plain English (reading level of a 12-year-old) to ensure accessibility for all citizens.

### **D. Availability**
*   **Uptime:** The platform must be hosted on a reliable cloud infrastructure (e.g., AWS, Vercel, or Azure) aiming for a 99.9% uptime, as citizens may need to report hazardous issues outside of standard business hours.
