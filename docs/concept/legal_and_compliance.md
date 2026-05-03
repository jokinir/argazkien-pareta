# Legal and Compliance Plan for Spain

## Introduction
Operating a SaaS business in Spain requires compliance with Spanish and EU laws, especially for data handling, taxes, and business registration. As a personal side-project targeting photographers and agents, focus on minimal viable compliance to avoid penalties. This plan assumes a solo operation; consult a lawyer or tax advisor for personalized advice.

## Business Structure: Should You Be an "Autónomo"?
- **Yes, as an Autónomo (Self-Employed Freelancer):** Ideal for a solo side-project. Registration is straightforward via the Spanish Social Security (Seguridad Social) and Tax Agency (Hacienda). Threshold: If annual income > €1,000 (2023 figure; check current), you must register. Benefits: Simple setup, low costs (€50–€100/month in social security contributions). Drawbacks: Personal liability for business debts.
- **Alternatives:** If scaling up, consider Sociedad Limitada (SL) for limited liability, but it's more complex and costly (€1,000+ setup). For now, Autónomo is sufficient and common for freelancers.
- **Registration Steps:** Register as Autónomo at the Seguridad Social office or online (via Cl@ve). Get a NIF (tax ID) if not already. Declare activity code (e.g., 6201 for software development).

## Taxes: Handling VAT (IVA) and Other Taxes
- **VAT (IVA):** As a SaaS provider, you're subject to IVA on sales. Threshold: Register for IVA if annual turnover > €0 (no minimum for digital services under EU rules). Rate: 21% standard for software/services. Collect IVA from customers and remit to Hacienda quarterly. Use tools like Stripe for automated collection.
- **Income Tax (IRPF):** As Autónomo, pay personal income tax on profits. Quarterly estimates (model 130) and annual declaration (model 100). Deduct expenses (infrastructure, tools). Tax rate: Progressive, up to 47% on high income.
- **Other Taxes:** Social Security contributions (~30% of income, but deductible). No corporate tax as Autónomo. If expanding, consider withholding tax (IRPF) on payments to freelancers.
- **Invoicing:** Issue electronic invoices with IVA, NIF, and details. Use software like Facturae or Stripe for compliance. Keep records for 4–6 years.
- **Tips:** Track all income/expenses meticulously. Use accounting software (e.g., Conta Azul). File taxes online via Hacienda's portal.

## GDPR: Data Protection Compliance
GDPR is critical as your SaaS handles personal data (photographer/agent details, photos). You're a data controller; photos may involve data subjects (property owners).

- **Key Requirements:**
  - **Privacy Policy:** Create and display a clear policy on your website explaining data collection, use, and rights. Include consent for processing.
  - **Data Processing:** Only collect necessary data (e.g., emails for invoices). Secure storage (encrypted, Cloudflare R2). Limit retention (e.g., delete after 1–2 years max). For photos, add opt-in consent for property owner data.
  - **Consent and Rights:** Obtain explicit consent for data use. Honor rights: access, rectification, erasure (right to be forgotten).
  - **Data Breaches:** Report breaches to AEPD within 72 hours if affecting EU residents.
  - **International Transfers:** If data leaves EU (e.g., to US servers), ensure adequacy (e.g., Privacy Shield) or standard clauses.

- **How to Handle GDPR:**
  - **Minimal Setup:** Use templates from AEPD or GDPR tools. For photos, watermark to anonymize; avoid storing sensitive data.
  - **Risk Assessment:** Low risk for initial MVP (few users). Conduct a basic DPIA for the MVP to assess risks.
  - **Penalties:** Up to €20M or 4% global turnover for violations. Comply early to avoid issues.
  - **Tools:** Integrate cookie consent banners and audit logs. Consult free AEPD resources.

## Other Compliance Considerations
- **Contracts:** Use standard terms for photographers (e.g., data processing agreements). Include liability limits. Draft standard terms limiting liability for photo theft/loss.
- **Intellectual Property:** Protect your code/software via copyright; consider trademarks for branding.
- **Consumer Protection:** Ensure fair terms; no misleading claims.
- **Insurance:** Optional but recommended (cyber liability for data breaches). Add cyber liability insurance early.
- **International Aspects:** For EU/US expansion, comply with local laws (e.g., CCPA in US). For EU expansion, ensure EU adequacy for data transfers. Budget for legal reviews (€500–€1,000 initially).

## Recommendations
- Start as Autónomo for simplicity.
- Automate taxes/invoicing with tools to minimize hassle.
- Prioritize GDPR with a basic privacy policy, cookie consent banners, audit logs, and a DPIA for the MVP.
- Budget €200–€500/month for legal/compliance initially, plus €500–€1,000 for legal reviews.
- Seek free advice from Cámara de Comercio or AEPD. Scale compliance as you grow.