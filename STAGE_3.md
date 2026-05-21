Here is the **Stage 3: Data Architecture & Content Strategy** document. 

Before the database is coded, the core content—which authorities to contact, which laws to quote, and how the templates will look—must be mapped out. This document defines the data structures and statutory logic required for CivicVoice, using the Irish legal framework as the launch market.

---

# **Stage 3 Data Architecture & Content Strategy: CivicVoice**

## **1. The Authority & Jurisdiction Database Schema**
The platform’s "Smart Authority Mapping" relies on a relational database. Before coding, this data must be gathered into a master spreadsheet. Every issue selected by a user must map to a specific authority based on the **Issue Category** and the **Geolocation (County/Eircode)**.

### **A. Required Database Columns (The Master Spreadsheet)**
*   `Authority_ID` (Unique Identifier)
*   `Authority_Name` (e.g., Health and Safety Authority)
*   `Department_Name` (e.g., Workplace Inspections)
*   `Issue_Category` (e.g., Health & Safety)
*   `Issue_Subcategory` (e.g., Noise Hazard, Chemical Spill)
*   `Jurisdiction_Zone` (e.g., National, or Specific County like "Dublin City Council")
*   `Tier_Level` (Tier 3 = State Regulator)
*   `Contact_Email` (e.g., contactus@hsa.ie)
*   `Contact_Phone` (e.g., 0818 289 389)
*   `Web_Form_URL` (Link to their specific complaint portal)

### **B. Sample Data Mapping (Irish Launch Market)**
| Issue Subcategory | Jurisdiction | Tier | Target Authority | Target Department | Statutory Law to Quote |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Commercial Noise Hazard | Dublin City | Tier 3 | Dublin City Council | Air Quality & Noise Control Unit | Environmental Protection Agency Act 1992 (Sec 108) |
| Workplace Noise/Safety | National | Tier 3 | Health & Safety Authority (HSA) | Workplace Inspections Unit | Safety, Health & Welfare at Work Regs 2007 (Part 5) |
| Black Mold / Broken Heating | National | Tier 3 | Residential Tenancies Board (RTB) | Dispute Resolution | Housing (Standards for Rented Houses) Regs 2019 |
| Faulty Goods / Consumer Rights | National | Tier 3 | Competition & Consumer Protection (CCPC) | Consumer Enforcement | Consumer Rights Act 2022 |

---

## **2. Dynamic Template Architecture (The "Mad-Libs" Framework)**
The platform will generate communications dynamically. To do this, templates must be written with standardized **Variables** that the backend system can replace with user inputs.

### **A. Standardized System Variables**
When drafting templates, content strategists will use the following standard tags:
*   `[User_Name]` / `[User_Address]` / `[User_Phone]`
*   `[Target_Entity]` (e.g., Dunnes Stores, Acme Property Management)
*   `[Entity_Location]` (e.g., Ilac Centre, D1)
*   `[Issue_Type]` (e.g., high-frequency acoustic hazard)
*   `[Specific_Details]` (User's free-text description)
*   `[Evidence_URL]` (The generated CivicVoice secure vault link)
*   `[Statutory_Reference]` (Pulled from the Authority Database above)
*   `[Action_Deadline]` (Calculated date: e.g., Current Date + 7/14 days)

### **B. Example: Tier 3 Authority Complaint Template (JSON / Logic Structure)**
*This is how a template is drafted for the database before it becomes code.*

**Condition:** IF `Issue_Category` = "Workplace Safety" AND `Tier` = "3"
**Recipient:** `[Authority_Email]`
**Subject:** Formal Hazard Notification: `[Target_Entity]` at `[Entity_Location]`

**Body:**
> Dear Inspectorate at the `[Authority_Name]`,
> 
> I am submitting a formal notification regarding a severe `[Issue_Type]` at `[Target_Entity]`, located at `[Entity_Location]`. 
>
> **Details of the Hazard:**
> `[Specific_Details]`
>
> I believe this constitutes a direct breach of the `[Statutory_Reference]`. 
> 
> I have securely logged objective evidence (including media and data logs) verifying this issue. The complete evidence file can be reviewed securely here: 
> **`[Evidence_URL]`**
>
> Management at `[Target_Entity]` has been notified as of `[Date_of_Tier1_Contact]`, but the hazard persists. I request that your department investigate this matter under your statutory powers.
>
> Yours sincerely,
> `[User_Name]`
> `[User_Phone]`

---

## **3. The "In-Person / Call Script" Architecture**
Writing a formal email is easy; confronting a manager or making a phone call is stressful. The platform will generate highly structured "Scripts" for the user to read from.

### **Script Structure Design:**
*   **The Opener (De-escalation & Clarity):** "Hi, I need to speak to the duty manager regarding an urgent health and safety issue."
*   **The Hook (Data-Driven Fact):** "There is a `[Issue_Type]` happening right now at `[Entity_Location]`. I have measured it at `[Specific_Details - e.g., 85 decibels peaking at 5kHz]`, which is an acoustic hazard."
*   **The Request:** "I need you to contact facilities management to isolate the equipment immediately."
*   **If/Then Rebuttals (The "Shield" strategy):**
    *   *If the manager says "We can't do anything right now":* 
        "I understand you are restricted locally, but this is an occupational hazard for your staff under the `[Statutory_Reference]`. Can you please provide me with the email for your corporate facilities team?"
    *   *If the manager says "You can't record in here":*
        "I am solely documenting a health and safety hazard for my complaint to the `[Authority_Name]`. I am not recording customers or staff faces."

---

## **4. Data Gathering & Content Execution Plan**
To populate this database, the content team must execute the following steps during the final weeks before development.

### **Step 1: The Government Scraping Phase**
*   Manually review the websites of all Irish local authorities (31 City/County Councils). 
*   Extract the exact email addresses for: Environmental Health, Housing Inspections, Waste Management, and Road Maintenance. *Note: Many councils hide these behind web forms; FOI (Freedom of Information) requests may be required to get the direct department emails.*

### **Step 2: The Corporate Directory Phase**
*   Create a "Tier 2" database of the top 50 retail, property management, and utility companies in the country (e.g., Dunnes Stores, Tesco, Ires Reit, ESB).
*   Log their legal Registered Office addresses, Customer Service emails, and Facilities Management contacts.

### **Step 3: Legal Review**
*   Have a qualified legal professional review the `[Statutory_Reference]` text strings to ensure they are accurate and up-to-date (e.g., ensuring references to the *Residential Tenancies Act* include recent amendments). 
*   Ensure that the tone of the "Final Warning" templates complies with pre-action protocol guidelines in Irish law.

---

### **Next Steps for the Dev/Design Team based on Stage 3:**
1.  **Frontend Requirement:** The UI must feature a dynamic questionnaire that accurately filters down to the `Issue_Subcategory` so the database knows exactly which template and law to pull.
2.  **Backend Requirement:** The server must feature a text-parser that can instantly swap out `[Variables]` with the user's JSON data without breaking formatting. 
3.  **Content Requirement:** Assign a team member to complete the "Master Spreadsheet" of all 31 Irish local authorities and their department contacts.
