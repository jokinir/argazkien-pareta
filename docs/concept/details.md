# Fine Details to Add Value


- Allow 3 languages (English, Spanish, Basque)
- 

## WhatsApp Bot for Photographer

Send a pre-written message such as this (words with $ are variables to be replaced):

"""
Hello $Agent,

Hereby I send you the preview for the listing $listing-name ($listing-desc): $url.

To confirm payment faster, you can send a WhatsApp message to number $MY-SAAS-BOT-NUMBER indicating payment for $listing-id.

Once paid, all photos will be replaced by high-quality watermark-free versions, and you will receive:

- .zip with Idealista-ready material
- Short video with highlights
- A3 and A4 posters
- (Other ideas TBD)

Thank you!
$Photographer
"""

This message will be sent to the photographer, who can later forward it to the agent.

### Implementation Notes
- Start with **Twilio WhatsApp API** for easier setup and lower approval friction than the official WhatsApp Business API.
- Budget for message costs: **€0.05–€0.10 per WhatsApp message**.
- Use Twilio's webhook flow to receive incoming messages and route payment confirmations.
- Display WhatsApp opt-in consent on the photographer and agent signup flow so message data is GDPR compliant. Store consent metadata, and allow users to withdraw consent at any time.

### Fallback Channels
- If the recipient is not on WhatsApp, fall back to **SMS** or **email** with the same payment confirmation link and instructions.
- Ensure the message content is consistent across WhatsApp/SMS/email and includes a clear privacy notice.

## Payment WhatsApp Bot

Agents can start a conversation with the payment bot, sending the $listing-id to confirm payment.

After receiving this message, the system sends a notification to the photographer chat and requests confirmation. If the photographer confirms, payment is marked as processed and the delivery page updates.

### Implementation Notes
- Use Twilio's programmable WhatsApp API for message delivery and inbound replies.
- Track message status and delivery receipts via Twilio.
- For non-WhatsApp users, offer **SMS/email** fallback automatically.
- Store and respect GDPR consent for all message-based communication. Keep logs minimal and only for the duration needed to support delivery/payment workflows.

Generate new message and new links for each piece of extra material.

## Customization

- Limit the initial product to **1–2 polished page templates** to keep the UX simple and reduce development scope.
- Offer **1–2 theme variants** per template and enable **A/B testing** for themes so photographers can compare which style drives more engagement.
- Photographer shall have option to enable/disable features per listing.
- Photographer shall have option to customize one/all features:
  - Add (or not) their logo
  - Add (or not) agent logo
  - Add (or not) agency logo/branding for whitelabel pages
  - Select main color
  - Select dark/light theme
- Keep all customizations within a single preset template structure, not a fully free-form editor.
- Ensure full mobile responsiveness and validate on **iOS and Android WhatsApp previews**, since the page will be shared via mobile messaging.
- Add metadata tagging for portal uploads, including **EXIF/metadata for Idealista** and other Spanish portals, so generated assets require less manual rework.

## Analytics and Engagement Tracking

- Integrate basic listing analytics so photographers can see:
  - Views per listing
  - Downloads per listing
  - Clicks on payment/booking buttons
- Surface this data in the photographer dashboard to help them understand which listings attract the most engagement and which delivery page style performs better during A/B tests.
- Keep analytics lightweight and privacy-friendly: no unnecessary personal tracking, only listing-level events.

## Agency Whitelabel

- Allow agencies to use whitelabel pages with their logo, colors, and footer copy.
- Support shared branding between photographer and agency when requested.
- Keep the page workflow the same, while letting agencies appear as the recommending partner.

A clean, mobile-first webpage, with Listing Name, location, contact info, photos. Optional logo(s) and background/title colors.

## Photographer Workflow

### Agents View

- Add Agent details
- Add Agent logo etc.
- Manage all previous and pending work with agent
- Manage payments and invoices
- Support agency-branded delivery pages and partner-managed photographer seats
- Etc.

### Listings View

- Manage each listing
- Customize looks, logos, name, description...
- Upload photos
- Remove/Modify photos
- Unlock HD photos and extra features
- Enable/disable features
- Language(s) in which to generate material
- Etc.

## Invoicing

- Integrate **Stripe** for subscription billing, invoice generation, and recurring payments.
- Build an invoicing engine with an official Spanish invoice format, including NIF/CIF, IVA, and IRPF fields.
- Automate PDF invoice generation using a headless rendering library such as **Puppeteer** or similar, producing ready-to-download PDFs.
- Embed **QR codes** in invoices for easy payment scanning (Bizum, bank transfer, or payment links).
- Store invoices securely and allow photographers to download historic invoices from their dashboard.

## Payment to platform

- Use **Stripe** as the primary payment platform for subscriptions and online payments.
- Support **Bizum** as a manual payment option with a toggle on each listing or invoice page.
- For Bizum, allow photographers to mark payments as received and trigger the high-res delivery workflow manually.
- Keep the payment flow simple: Stripe for automated card/SEPA subscriptions, Bizum for local Spanish payment habits with manual confirmation.
- Include clear payment instructions and QR codes both on the delivery page and the invoice/PDF.
