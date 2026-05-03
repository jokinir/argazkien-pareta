# MVP Plan for Argazkien Pareta

## Goal
Build a focused, launchable MVP for a real estate photographer delivery and marketing hub that can be developed in evenings and weekends alongside a full-time job.

The primary objective is to validate demand from Spanish professional real estate photographers by delivering a small, high-value workflow: secure photo delivery, payment-linked unlock, and a branded mobile-first listing page.

## MVP Scope

### Core Value Proposition
- Enable photographers to send a premium delivery page instead of a Dropbox/WeTransfer link.
- Protect high-resolution photos with low-res, watermarked previews.
- Unlock high-res downloads only after payment is confirmed.
- Make the shared page mobile-friendly for WhatsApp and agent workflows.

### Must-have features
1. Photographer onboarding and listing creation
   - Simple signup with email/password.
   - Create a new property listing with basic metadata: title, address, description, agent name, photographer name.
   - Upload a small set of photos (initially 6–12 images).

2. Delivery page generation
   - Generate a unique, shareable public URL for each listing.
   - Use one or two polished responsive templates only.
   - Display listing name, location, photographer contact, agent contact, photo gallery, and payment status.
   - Show low-resolution watermarked previews initially.

3. Payment unlock flow
   - Offer a Stripe payment link for agents or clients.
   - Add a manual “Bizum / bank transfer” payment toggle for Spanish habits.
   - After payment is confirmed, automatically unlock high-resolution downloads.
   - Support manual payment confirmation by the photographer for Bizum.

4. Photo protection and asset generation
   - Generate web-optimized preview images with visible watermark.
   - Generate a high-resolution download package for paid users.
   - Keep original uploads secure behind authenticated storage.

5. Minimal dashboard and workflow
   - Photographer view: list of active listings, status (preview / paid / delivered), and quick access to share links.
   - Listing management: edit metadata, upload additional photos, mark payment received.

6. GDPR and compliance fundamentals
   - Collect explicit consent for communications if WhatsApp or SMS is added later.
   - Store only required user and listing data.
   - Provide a basic privacy policy placeholder and cookie notice for the MVP.

## Nice-to-have but deferred
- Multi-language UI (English/Spanish/Basque). Keep MVP in Spanish + English copy where needed.
- Agency whitelabel branding and theme selection.
- A/B theme testing dashboard.
- Full invoice generation with PDF + Spanish IVA/IRPF fields.
- WhatsApp bot automation for payment confirmation.
- Analytics beyond simple view/download counts.
- Direct portal metadata export for Idealista/Fotocasa.

## MVP success criteria
- A photographer can onboard, create a listing, upload photos, share a secure page, and unlock downloads after payment.
- The delivery page is mobile-first and suitable for WhatsApp sharing.
- The workflow is clear with no more than 4 screens for the photographer.
- The first pilot users report that the experience feels more premium than Dropbox and that payment unlock is a compelling improvement.

## Implementation strategy

### Phase 1: Minimal product architecture
- Backend: lightweight server with authenticated user/listing management.
- Storage: object storage for photos (Cloudflare R2, AWS S3, or similar).
- Frontend: simple responsive web app with a photographer dashboard + listing page.
- Payments: Stripe Checkout or Payment Link for the initial flow.
- Deploy on a serverless-friendly environment or a small VPS to keep costs low.

### Phase 2: MVP feature build
- Build user registration and login.
- Build listing CRUD and photo upload flow.
- Build public listing page renderer and shareable URL generator.
- Build payment status workflow and high-res unlock logic.
- Add watermark generation and low-res preview generation.
- Add a photographer dashboard with listing statuses.

### Phase 3: Pilot and feedback loop
- Invite 3–5 photographers to test the workflow quickly.
- Validate that they prefer the shared page over a simple file link.
- Watch for friction in upload, sharing, and payment confirmation.
- Iterate on wording, payment flow, and preview quality.

## Timebox and schedule
Because this is a side-project, keep the MVP timeline realistic and timeboxed.

### 6-week side-project sprint
- Week 1: Define data model, choose stack, wireframe the dashboard and page.
- Week 2: Implement authentication, user onboarding, and listing creation.
- Week 3: Add photo upload, preview generation, and public page rendering.
- Week 4: Integrate Stripe payment unlock and manual payment confirmation.
- Week 5: Polish mobile UX, add share links, and secure storage/workflow.
- Week 6: Pilot with real users and collect improvement feedback.

### Ongoing weekly rhythm
- Limit work to 6–10 hours per week.
- Reserve one evening for code and one weekend session for integration.
- Keep scope small: one template, one payment flow, one sharing channel.

## Technical constraints and choices

### Keep complexity low
- Avoid building a full CMS or marketplace.
- Use existing payment infrastructure rather than custom billing.
- Prefer simple, reliable storage and CDNs.
- Do not build multi-tenant agency dashboards in MVP.

### Use off-the-shelf tools where possible
- Stripe for payments and invoices initially.
- Prebuilt UI components for forms and responsive layout.
- A managed database or SaaS backend to reduce ops burden.

### Focus on what proves value first
- Photo protection and payment unlock are the key differentiators.
- The page should feel premium and mobile-ready.
- The workflow should require minimal training for photographers and agents.

## Risks and mitigation

### Risk: Too much scope for a side-project
- Mitigation: Freeze scope early. Build only one share page template and one payment gateway.

### Risk: Payment flow is too complex for Spanish users
- Mitigation: Start with Stripe plus a clear manual Bizum confirmation path. Keep instructions concise and localized.

### Risk: GDPR or legal exposure
- Mitigation: Limit data collected, store the minimum required, and add a simple privacy notice. Add full legal pages after MVP validation.

### Risk: No interest in the product
- Mitigation: Talk to 3–5 photographers before coding. Use quick mockups or manual demos to validate the core idea.

## First pilot metrics to watch
- Number of listings created per user.
- Share link clicks / public page views.
- High-res download unlock rate after payment.
- Time taken from upload to payment confirmation.
- Qualitative feedback: ease of use, perceived professionalism, and whether they would pay for it.

## Next steps after MVP
If the MVP proves value, the next prioritized enhancements should be:
1. Invoice PDF generation with Spanish IVA/IRPF fields.
2. WhatsApp/SMS sharing automation and consent-tracked communication.
3. Agency partner/whitelabel page support.
4. Multi-language UI and portal-expo metadata exports.
5. Basic analytics dashboard for views, downloads, and engagement.

## Notes for a side-project owner
- Accept that the first version will be deliberately imperfect.
- Aim for clarity over feature count.
- Track progress in small weekly slices, and ship a working workflow fast.
- Use the MVP to validate the business idea before investing in larger automation.

