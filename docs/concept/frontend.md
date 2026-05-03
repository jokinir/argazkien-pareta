# Frontend Plan for Argazkien Pareta

This document outlines the frontend architecture, frontend-specific technology choices, and the implementation plan for the Argazkien Pareta SaaS platform.

---

## Tech Stack

### Framework: React with Next.js
Next.js has been chosen to build the frontend for the following reasons:
- Full support for **hybrid rendering** modes:
  - **Static Generation (SSG):** Ideal for public property listing pages to ensure fast loading and SEO optimization.
  - **Server-Side Rendering (SSR):** Will be used for personalized sections like agency-branded pages or pages with CNAMEs.
- Built-in **Image Optimization API** to handle watermarked previews, thumbnails, and responsive image loading.
- Excellent **SEO capabilities** for public listings shared via WhatsApp or idealista.
- Great developer experience with a strong ecosystem of third-party libraries.

### Styling: Tailwind CSS
- Tailwind CSS will be used for rapid development of mobile-first, responsive designs. 
- Benefits include:
  - Utility-first class approach for consistent and clean styling.
  - Ease of customization for branding (colors, fonts, themes).
  - Pre-built support for dark/light mode.

### Component Library: Headless UI or Chakra-UI
- **Headless UI**: Lightweight, unstyled components to ensure total control over appearance.
- **Chakra-UI (optional)**: Prebuilt, accessible components for faster dashboard development.

### State Management: Context API + Zustand
- Global state will be managed using Next.js’ built-in Context API. Zustand may be introduced later for lightweight, modular state management.

### Hosting: Vercel
- Vercel is the ideal hosting platform for Next.js due to:
  - Seamless integration.
  - Global edge caching for fast public property pages.
  - Free tier suitable for side project MVP.

---

## Key Frontend Modules

### 1. **Photographer Dashboard**
The core tool for photographers to manage listings, payments, and delivery pages.

**Key Features:**
- **Listings Management CRUD:**
  - Add/edit/delete properties.
  - Upload and preview watermarked images.
  - View payment statuses (e.g., unpaid, paid, delivered).
- **Theme Customization:**
  - Select branding (logo, colors).
  - Enable/disable delivery page features (e.g., A/B testing, dark mode).
- **Invoice Downloads:**
  - Access PDF invoice history.

---

### 2. **Public Listing Pages**
The consumer-facing interface: a mobile-first delivery experience optimized for WhatsApp sharing.

**Key Features:**
- **Responsive Design:** Previews must load instantly and adapt to varied screen sizes (WhatsApp-heavy audience).
- **OpenGraph Metadata:** Ensure perfect rendering in WhatsApp, Facebook, and Instagram previews.
- **Generate Two Layouts:**
  - Basic image slider gallery with description/contact fields.
  - A paginated grid for larger photo collections.
- **SEO & Performance:**
  - Use Next.js static site generation (SSG) where possible.
  - Optimize images to reduce load size, without sacrificing quality.

---

### 3. **Authentication and Onboarding**
- **Authentication**: Photographer login will be token-based (JWT) using API endpoints provided by the Django backend.
- **Onboarding Flows:**
  - Walk photographers through first listing creation.
  - Showcase dashboard features succinctly.

---

### 4. **Payment Confirmation Flow**
- After a payment is marked as complete:
  - The delivery page will automatically update to enable downloads for high-res, non-watermarked files.
  - Notifications will inform the photographer of the completed process.

---

## API Integration

### Integration with Django REST Framework
- All frontend data will be fetched from the backend’s APIs using Axios or Fetch.
- API Endpoints:
  - **Listings:** `/api/listings`
  - **Photos:** `/api/photos/upload`
  - **Payments:** `/api/payments/confirm`
  - **Public Pages:** `/api/public/listings/:id`

### Authentication:
- Use JWT stored in cookies (HttpOnly + secure).
- Authentication headers attached to Axios requests.

---

## Component Design and File Structure

### Directory Structure
Below is a simplified directory structure for the Next.js app:
```
src/
│
├── components/
│   ├── Dashboard/
│   ├── Listings/
│   ├── Modals/
│   └── Shared/
│
├── hooks/
│   └── useAuth.js
│
├── layouts/
│   ├── MainLayout.js
│   ├── DashboardLayout.js
│   └── PublicLayout.js
│
├── pages/
│   ├── _app.js
│   ├── index.js
│   ├── dashboard/
│   │   ├── index.js
│   │   └── listings/
│   │       └── [id].js
│   ├── public/
│   │   └── [slug].js
│   └── api/
│
├── styles/
│   └── globals.css
│
└── util/
    └── api.js
```

### Component Breakdown
1. **Reusable Components**: 
   - `ImageGallery.js`: Displays photos in a responsive grid or slider.
   - `PaymentStatus.js`: Shows whether the listing is paid/unlocked.
   - `ThemeSwitcher.js`: Toggles between light/dark modes.
2. **Layouts**:
   - Different layouts for dashboard vs public pages.
3. **Hooks**:
   - `useAuth`: Frontend authentication management (log in/out, tokens).
   - `useAPI`: Wrapper around Axios for DRF communication.

---

## Implementation Roadmap

### **Phase 1: Core Dashboard and Listing CRUD**
1. **Week 1–2**:
   - Set up Next.js project.
   - Design photographer dashboard with mock data.
   - Implement authentication workflows.
2. **Week 3**:
   - Add API calls for listing CRUD.
   - Integrate photo upload flow to Cloudflare R2 via backend endpoints.
   - Generate low-res previews for gallery.

### **Phase 2: Public Delivery Page**
1. **Week 4**:
   - Develop listing page layout.
   - Add OpenGraph metadata for sharing.
   - Optimize mobile responsiveness.

### **Phase 3: Payment and Deployment**
1. **Week 5**:
   - Implement payment status integration.
   - Update delivery page upon Stripe webhook.
2. **Week 6**:
   - Finalize theming and branding toggles.
   - Deploy MVP to Vercel.

---

## Risks and Mitigation

### **Risk: Limited Time**
- Mitigation: Leverage component libraries and utility-based styling (Tailwind) to reduce frontend design time.

### **Risk: CNAME and Agency Branding**
- Mitigation: Use placeholders for branding in MVP. Add dynamic CNAME logic for Phase 2+.

### **Risk: Multi-language Complexity**
- Mitigation: Default to Spanish and English in the MVP with i18n structure ready for future expansion.

---

## Conclusion

React with Next.js is the optimal stack for both the frontend dashboard and public listing pages. The hybrid rendering capabilities, SEO features, prebuilt image optimization, and excellent hosting with Vercel align perfectly with the project’s requirements. The outlined implementation strategy focuses on shipping an MVP rapidly while ensuring scalability for future features.