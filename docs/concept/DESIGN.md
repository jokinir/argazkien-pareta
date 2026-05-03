# Design Specification: Argazkien Pareta

## 1. Core Concept & Identity
Argazkien Pareta is a premium marketing and delivery hub for professional real estate photographers. It replaces generic file-sharing (Dropbox/WeTransfer) with a branded, secure, and automated delivery experience [3, 4].

- **Primary Goal:** Secure high-resolution assets until payment is confirmed [4, 5].
- **Visual Style:** Minimalist, high-end agency feel. Dark mode support, typography-heavy, and mobile-responsive [6, 7].
- **Key Differentiator:** Integrated payment-to-unlock workflow (Stripe/Bizum) [5, 8].

## 2. Main UI/UX Workflow
1. **Onboarding:** Photographer logs in/signs up [9].
2. **Creation:** Create a Listing (Address, Agent Name, Price) and upload high-res photos [9, 10].
3. **Processing (Internal):** System generates watermarked, low-res previews [9, 11].
4. **Distribution:** Photographer copies a unique URL and sends it to the Agent via WhatsApp [9, 12].
5. **Collection:** Agent views the page. To get high-res files, they pay via Stripe or Bizum [5, 8].
6. **Delivery:** Once paid, the page automatically unlocks the high-res "Download All" package [13, 14].

## 3. Page Breakdown

### Page A: Photographer Dashboard (The "Command Center")
The main view where the user manages their business at a glance [10, 15].
- **Top Bar:** Profile, Subscription status (Basic/Pro), "New Listing" button.
- **Listing Grid:** Cards for each property showing:
    - Thumbnail, Address, and Date created.
    - **Status Badges:** `Draft`, `Awaiting Payment` (Yellow), `Paid` (Green), `Delivered` (Blue) [9, 16].
    - **Quick Actions:** Copy Link, Edit, Delete (Kill-switch), Download Invoice [10, 15, 17].

### Page B: Listing Editor & Uploader
A functional workspace to prepare the delivery [9, 10].
- **Metadata Form:** Input fields for Title, Description, Agent details, and Price.
- **Uploader:** Drag-and-drop zone for high-res images. 
- **Preview Gallery:** A grid of uploaded images where photographers can toggle watermarking or reorder shots [10].
- **Settings Toggle:** Enable/Disable "Pay-to-Unlock", Choose Template (Slider vs. Grid), Dark/Light theme [6, 18].

### Page C: Public Delivery Page (The "Product")
This is the page the Agent sees. It must look like a high-end property website [18, 19].
- **Header:** Branded with the Photographer's (and optionally the Agent's) logo [6, 10].
- **Hero Section:** Large property title and address over the primary photo.
- **Image Gallery:**
    - **Unpaid State:** Low-res, watermarked images in a sleek slider or grid. Images have a "Locked" overlay [9, 18].
    - **Paid State:** High-res, crisp images. "Download All" button appears prominently [9].
- **Call to Action (CTA) Section:**
    - "Unlock High-Resolution Photos" button.
    - Payment options: **Credit Card (Stripe)** or **Bizum/Bank Transfer** instructions [8, 18].
- **Footer:** "Powered by Argazkien Pareta" (Viral referral link) [1, 20].

### Page D: Payment Confirmation Dialog
- **Stripe:** Standard checkout overlay.
- **Bizum:** A modal showing the photographer's phone number and a "Notify Photographer" button to speed up manual verification [8, 21].

## 4. Mobile UX Requirements
- **WhatsApp Optimization:** Public pages must load in <2 seconds. Buttons must be thumb-friendly. OpenGraph tags should ensure the property photo appears in WhatsApp link previews [6, 19].
