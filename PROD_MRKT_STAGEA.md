Just as with the core software application, building a high-converting product marketing website requires a strict sequence of planning before any code is written (or before any site-builder like Webflow or Framer is opened). 

For a marketing website, the focus shifts away from complex database architecture and instead focuses on **psychology, SEO (Search Engine Optimization), copywriting, and Conversion Rate Optimization (CRO).**

Here are the 6 stages of planning and development for the CivicVoice Product Marketing Website before coding begins:

---

### **Stage 1: Strategy, Positioning & SEO Planning**
*Goal: Define exactly how people will find the website and what psychological triggers will make them sign up.*

*   **SEO Keyword Strategy:** Before deciding what pages to build, you must research what your target audience is Googling. 
    *   *Informational Keywords:* "Is 5kHz noise illegal?", "Landlord ignoring mold Ireland".
    *   *High-Intent Keywords:* "How to report noise complaint Dublin City Council", "HSA whistleblower form".
*   **Conversion Funnel Definition:** What is the primary goal of the site? (e.g., "Sign up for a Free Account"). What is the secondary goal if they aren't ready to sign up? (e.g., "Read our free guide on Tenant Rights").
*   **Competitor Analysis:** Look at how legal aid sites, tenant unions (like Threshold in Ireland), or local council websites present themselves, and note how CivicVoice can look much more modern, approachable, and actionable.

### **Stage 2: Information Architecture (IA) & Sitemapping**
*Goal: Create the blueprint of all the pages on the website and how they link together.*

*   **The Sitemap:** Create a visual tree (using tools like Miro or a spreadsheet) of the website structure:
    *   **Main Nav:** Home | Solutions (Dropdown: Tenants, Consumers, Communities, Workers) | Pricing | FAQs.
    *   **Utility/Footer Nav:** Privacy Policy | Terms of Service | Contact Us | GDPR Information.
*   **URL Structuring:** Plan clean, SEO-friendly URLs (e.g., `civicvoice.io/solutions/tenant-disputes` rather than `civicvoice.io/page-2`).

### **Stage 3: Content-First Copywriting**
*Goal: Write every single word that will appear on the website. Design should wrap around the content, not the other way around.*

*   **The "Hook" Matrix:** Draft different H1 Headers and Sub-headers for testing. (e.g., *“Stop Waiting. Start Resolving.”* vs *“Turn Frustration into Action.”*)
*   **Drafting the Core Pages:** Write the text for the 3-step "How it Works" section, the Pricing tiers, and the Use Cases.
*   **Micro-copy & CTAs:** Plan the text for buttons. Instead of boring "Submit" or "Learn More," use action-oriented copy like "Start Your Free Case" or "See How It Works."
*   **Legal Scrutiny:** Have legal counsel approve the disclaimers (e.g., "We are not a law firm") before the text is locked in.

### **Stage 4: Low-Fidelity Wireframing & CRO**
*Goal: Map out the structural layout of the pages to maximize user flow and sign-ups (Conversion Rate Optimization).*

*   **Block-Level Wireframing:** Using Figma or Balsamiq, create greyscale boxes representing where content will go. 
    *   *Standard SaaS Layout:* Hero Section -> Social Proof (Logos/Testimonials) -> Problem Statement -> The Solution (Features) -> 3-Step Process -> Final Call to Action.
*   **Mobile-First Layout:** Map out how the blocks will stack on a mobile screen, as 60-70% of users experiencing an immediate issue (like being kept awake by a store alarm) will be searching on their phones.

### **Stage 5: High-Fidelity UI/Visual Design**
*Goal: Apply the brand identity to make the website look highly professional, trustworthy, and visually engaging.*

*   **Apply Brand Guidelines:** Inject the chosen color palette (Navy Blue and Sage Green) and typography (Outfit/Inter). 
*   **Create Custom Assets:** 
    *   Design clean, abstract "UI mockups" to show what the app looks like inside (e.g., a graphic showing the Evidence Vault link generating).
    *   Source or design high-quality, relatable imagery (e.g., a stressed person looking at an extractor fan, contrasted with someone looking relieved at their laptop).
*   **Clickable Prototype:** Link the high-fidelity Figma screens together so stakeholders can click through the marketing site as if it were live. 

### **Stage 6: Tech Stack Selection & MarTech Setup**
*Goal: Choose the software that will host the site and the marketing tools that will track its success.*

*   **Choose the CMS / Builder:** Decide if the marketing site will be hard-coded (e.g., Next.js, matching the main app) or built on a marketing-friendly CMS (like **Webflow** or **Framer**). *Recommendation: Webflow or Framer allows the marketing team to publish blogs and update copy without waiting for software developers.*
*   **MarTech (Marketing Technology) Integration Plan:** Plan what tracking scripts need to be installed in the code:
    *   **Analytics:** Google Analytics 4 (GA4) or privacy-friendly alternatives like Plausible/Fathom.
    *   **Cookie Consent:** A GDPR-compliant banner (e.g., CookieYes or OneTrust) to legally manage tracking cookies.
    *   **CRM (Customer Relationship Management):** How will support tickets from the "Contact Us" form be handled? (e.g., routing forms to HubSpot or Zendesk).
*   **App Domain Linking:** Plan the DNS strategy. (e.g., The marketing site lives on `www.civicvoice.io`, but clicking "Log In" redirects the user to the web app hosted at `app.civicvoice.io`).

Once Stage 6 is complete, the UI/UX designs and MarTech requirements are handed over to the web developer (or Webflow expert) to officially begin building the live website.
