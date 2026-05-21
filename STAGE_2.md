Here is the **Stage 2: Legal, Compliance, & Risk Assessment** document. Because CivicVoice handles sensitive disputes, personal data, and statutory complaints against corporations and government bodies, establishing a strict legal and compliance framework before writing any code is non-negotiable. 

This document outlines the required legal frameworks, disclaimers, and moderation strategies that must be built into the platform's architecture.

---

# **Stage 2 Legal & Compliance Document: CivicVoice**

## **1. GDPR & Data Privacy Strategy**
As an EU-based platform (starting in Ireland), CivicVoice must adhere strictly to the General Data Protection Regulation (GDPR) and the Data Protection Act 2018. CivicVoice acts as the **Data Controller** for user profiles and the **Data Processor** for the evidence files.

### **A. Data Classification & Minimization**
*   **Standard PII:** Name, Email, Phone Number, Home Address (only requested if the statutory form strictly requires it, e.g., an RTB tenancy dispute).
*   **Dispute Data:** The specific nature of the complaint, geolocation of the issue, and targeted entities (e.g., Dunnes Stores, a private landlord).
*   **Principle of Minimization:** The platform will *never* ask for PPS numbers, banking details, or sensitive health data unless absolutely required by a specific tier-3 statutory template (and even then, this data should ideally be inputted locally by the user *after* downloading the template, not stored on the database).

### **B. Core User Privacy Rights (Built into UI)**
*   **The Right to be Forgotten:** A one-click "Delete Account & Wipe All Data" button must exist in the settings. This must trigger a hard delete (not a soft flag) on the database and trigger a script to wipe all files from the cloud bucket (e.g., AWS S3).
*   **Subject Access Requests (SAR):** A one-click "Export My Data" button that generates a JSON file of all user activity, cases, and generated texts.
*   **Consent Checkboxes:** Explicit opt-in checkboxes are required for creating an account and for accepting that evidence files will be stored on cloud servers.

### **C. Data Retention Policy**
*   **Active Cases:** Data is held indefinitely while a case is marked "Active."
*   **Closed Cases:** Evidence files are automatically wiped 90 days after a case is marked "Resolved" to save server costs and minimize data breach risks. The text data of the case remains for the user's historical log.

---

## **2. Liability Mitigation & Terms of Service (ToS)**
If a user uses the platform to send a legally threatening letter to a corporation or landlord, the platform itself must be insulated from legal blowback. 

### **A. "Not Legal Advice" Disclaimer (Crucial)**
This disclaimer must be highly visible on the homepage, the footer, and as a required acknowledgment during sign-up.
*   **The Clause:** *"CivicVoice provides software, structural templates, and contact directories to assist users in formatting complaints. CivicVoice is not a law firm. The use of this platform does not constitute legal advice, nor does it establish an attorney-client relationship. Users are solely responsible for ensuring the accuracy and truthfulness of their claims before sending them to regulatory bodies."*

### **B. Acceptable Use Policy (AUP)**
The Terms of Service must explicitly ban the following behaviors, giving CivicVoice the right to terminate accounts immediately:
*   **Vexatious Complaints:** Spamming corporations or councils with repeated, identical, automated complaints (the platform is not a DDoS tool).
*   **Harassment:** Using the platform to personally target, threaten, or doxx individual frontline employees (e.g., naming a specific store cashier rather than targeting the "Store Manager/Head Office").
*   **Illegal Material:** Uploading explicit content, illegal material, or evidence that violates wiretapping/privacy laws.

### **C. Indemnification Clause**
*   **The Clause:** *"The user agrees to indemnify and hold harmless CivicVoice, its founders, and employees from any legal claims, defamation suits, or damages arising from communications generated and sent by the user via the platform."*

---

## **3. Defamation & Libel Risk Strategy**
Because users will be logging complaints against identifiable businesses (like Dunnes Stores) and private individuals (like landlords), the platform must mitigate the risk of being sued for defamation.

### **A. "Private by Default" Architecture**
*   **1-to-1 Communication:** CivicVoice acts as a drafting tool. The complaints are sent *by the user* (via their own email or an embedded private proxy) directly to the authority. CivicVoice does not host an open public forum where users post complaints for the world to see. Because the platform does not "publish" the claim to the public, it is significantly protected against defamation claims.

### **B. Moderating the "Public Heatmap" (Future Feature)**
In Phase 6 of the roadmap, CivicVoice plans to aggregate data to show "heatmaps" of local issues. To do this without triggering libel lawsuits:
*   **Anonymization & Generalization:** The heatmap will never show user-submitted text or evidence. It will only show categorized metadata.
    *   *Unsafe:* "John Smith claims Dunnes Stores Ilac Centre is breaking the law with deafening alarms."
    *   *Safe (Platform Standard):* "5 Commercial Noise Hazards reported in Dublin 1 this month."
*   **Verification thresholds:** A location/corporation will only "glow red" on the public heatmap if a threshold is met (e.g., 3+ unique users report the same issue in a 30-day window).

---

## **4. Evidence Vault: Privacy & Copyright Management**
When users upload photos or videos (such as the HQ video of the Dunnes Stores equipment), specific risks arise.

### **A. Third-Party Privacy Warning (CCTV/Recording rules)**
*   When a user uploads a video to the Evidence Vault, a tooltip or modal must remind them of recording laws: 
    *   *Warning: Ensure your photo/video focuses on the hazard (e.g., the equipment, the hazard, the noise) and avoid capturing the identifiable faces of private citizens or frontline staff without their consent.*
### **B. Copyright of Evidence**
*   The Terms of Service must state that the user retains full copyright of any photos/videos uploaded, but grants CivicVoice a limited license to host that data solely for the purpose of generating their case link.

---

### **Next Steps for the Dev/Design Team based on Stage 2:**
1.  **UI/UX Requirement:** Add an un-skippable "I understand this is not legal advice" checkbox to the registration screen.
2.  **Database Requirement:** Build the database schema so that "User PII" and "Case Evidence" are stored in separate, cleanly severable tables to allow for easy GDPR "Right to be Forgotten" wipes.
3.  **Content Requirement:** Draft the final Privacy Policy and Terms of Service (with a qualified legal professional based in Ireland) using this framework.
