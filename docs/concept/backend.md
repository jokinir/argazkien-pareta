# Backend Plan for Argazkien Pareta

This document outlines the backend architecture, backend-specific technology choices, and implementation plan for the Argazkien Pareta SaaS platform. 

## Tech Stack

### Framework: Django
Django has been chosen as the backend framework. It is well-suited for this platform due to its:
- Batteries-included approach with pre-built tools for user authentication, ORM, forms, and security features.
- Scalability and maintainability for a small team.
- Seamless integration with image processing libraries and payment systems like Stripe.
- Excellent compatibility with Docker for containerization.

### Database: PostgreSQL
- **Reasoning:** A relational database is essential for managing structured data (e.g., users, properties, payments). PostgreSQL offers strong consistency, excellent performance, and support for JSONB for semi-structured data.
- **Deployment:** The database will be containerized within Docker Compose for local development and production alignment.

### File Storage: S3-Compatible Storage
- **Initial Service:** Cloudflare R2 for storing images (both high-resolution and watermarked previews). 
- **Why:** It offers cost-effective storage with no egress fees and compatibility with Django’s `django-storages` package for direct integration.

### Caching and Background Tasks
- **Redis**: Used for caching frequently-accessed data and as a message broker for asynchronous tasks like image watermarking and thumbnail generation.
- **Celery**: Task management with Redis will allow for offloading intensive workflows.

---

## System Architecture Design

### Key Backend Modules
The backend is divided into the following modules:

1. **Authentication and Authorization**
   - Django’s built-in `auth` system will handle user registration, authentication, and permissions.
   - Extend the base user model to differentiate photographers (primary users) and agents (secondary users).

2. **Listings Management**
   - Enable CRUD operations for property listings.
   - Integrate foreign key relationships between properties, photographers, and agents.
   - Add support for uploading and validating photos.

3. **Image Processing**
   - Generate watermarked previews, thumbnails, and high-resolution photos.
   - Use Django signals to process image uploads.
   - Optimize images for Idealista/Fotocasa metadata requirements.

4. **Payment Integration**
   - Use `dj-stripe` for Stripe payment processing.
   - Add manual toggling for Bizum payments.
   - Lock/unlock high-res downloads based on payment status.
   - Automate invoice generation for payment confirmations.

5. **Language and Localization**
   - Use Django’s i18n and l10n tools to support Spanish, English, and Basque for multilingual pages.
   - Support currency and date formatting for Spanish-specific requirements.

6. **GDPR Compliance**
   - Store user data securely (encrypted, access-controlled).
   - Add explicit consent logging for WhatsApp/SMS usage.
   - Auto-delete expired data/images after retention windows.

---

## Django Models

### Core Models
#### **User**
Extends Django’s `AbstractUser`:
- **Fields:** `email`, `password`, `is_photographer`, `is_agent`.
- **Custom Permissions:** Role-based access for managing properties and handling payments.

#### **PropertyListing**
Represents a real estate listing:
- **Fields:** `title`, `address`, `description`, `agent` (FK to User), `photographer` (FK to User), `status` (Enum: Draft/Preview/Paid/Delivered).
- **Relations:** Linked to uploaded photos and payments.

#### **Photo**
Handles image uploads:
- **Fields:** `property_listing` (FK), `image_file` (original), `watermarked_file` (processed), `thumbnail_file`, `metadata` (JSONB).
- **Signals:** Automatically generate watermarked/optimized versions when uploaded.

#### **Payment**
Tracks payment status:
- **Fields:** `property_listing` (FK), `stripe_payment_id`, `manual_payment_note`, `status` (Unpaid/Paid).
- **Logic:** Trigger image unlock when payment status is updated.

---

## API Design

### RESTful Endpoints
Built with Django REST Framework (DRF). Core endpoints include:
1. **User Authentication**
   - `/api/auth/register/` (POST): Create an account.
   - `/api/auth/login/` (POST): Log in to the system.

2. **Listings Management**
   - `/api/listings/` (GET/POST): View and create property listings.
   - `/api/listings/<id>/` (GET/PUT/DELETE): Retrieve, update, or delete a listing.

3. **Photo Uploads**
   - `/api/photos/upload/` (POST): Upload new images.
   - `/api/photos/<id>/` (DELETE): Delete specific photos from a listing.

4. **Payment Management**
   - `/api/payments/stripe/` (POST): Initiate Stripe checkout.
   - `/api/payments/manual/` (POST): Manually confirm Bizum payments.

5. **Public Delivery Pages**
   - `/api/public/listings/<slug>/`: Render listing pages with shareable URLs.

---

## Containerized Development Environment

### Docker Setup
Develop the entire system using Docker Compose:
- **Containers:**
  - **Backend App:** Runs Django and Celery workers.
  - **Database:** Runs PostgreSQL.
  - **File Storage Proxy:** Cloudflare R2-compatible S3 proxy in development, e.g., MinIO.
  - **Redis:** Message broker for Celery tasks.
  - **Frontend Proxy (Optional for API Development):** React or simple static file server.

### Docker Compose Example
```yaml
version: '3.8'

services:
  app:
    build:
      context: .
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis

  db:
    image: postgres:14
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: securepassword
      POSTGRES_DB: app_db
    volumes:
      - db_data:/var/lib/postgresql/data

  redis:
    image: redis:latest

volumes:
  db_data:
```

---

## Image Processing Pipeline

### Watermark Implementation
Use Pillow (Python Imaging Library):
- On image upload, generate:
  - **Low-Res Watermarked Previews**
  - **High-Resolution (Locked) Photos**
- Example Django Signal:
```python
from PIL import Image
from django.db.models.signals import post_save

def apply_watermark(sender, instance, **kwargs):
    if not instance.watermarked_file:
        with Image.open(instance.image_file) as img:
            # Add watermark logic here
            instance.watermarked_file.save(...)
post_save.connect(apply_watermark, sender=Photo)
```

### Future Extension with C++ gRPC
- Replace Pillow-based scripts with a high-performance C++ image processing microservice.
- Connect via gRPC for parallelized watermarking and EXIF processing.

---

## Deployment Plan

### Hosting Environment
Start cost-effectively:
- Use a small VPS or platform-as-a-service like Heroku or Render.
- Switch to containerized platforms like AWS ECS or DigitalOcean once usage scales.

### Security
- Secure Django with `SECURE_SSL_REDIRECT`, `HttpOnly` cookies, and `django.middleware.security`.
- Use environment variables for secrets (`django-environ`).

### CI/CD Pipeline
Automate deployment:
- Use GitHub Actions:
  - **Test Steps:** Run Django unit tests, lint code.
  - **Build Steps:** Build Docker containers.
  - **Deploy Steps:** Deploy to staging/production with health checks.

---

## Implementation Phases

### Phase 1: Build Core MVP Backend
- Set up Django + REST Framework + PostgreSQL.
- Create `User`, `PropertyListing`, `Photo`, and `Payment` models.
- Develop CRUD endpoints for listings and photos.
- Add Stripe integration for basic payment workflows.
- Implement watermarked images and secure file hosting.

### Phase 2: Pilot Integration and Testing
- Deploy on staging environment.
- Test workflows with 3–5 photographers.
- Optimize payment flows and feedback loop.

### Phase 3: Scale and Improve
- Add Redis and Celery for background tasks like photo processing.
- Implement localization and multi-language support.
- Deploy full CI/CD pipeline.

---

## Conclusion
Django provides the stability, security, and extendibility necessary to deliver Argazkien Pareta's goals. With a structured, containerized setup using Docker, Redis, Celery, and PostgreSQL, the platform is positioned for rapid MVP development and eventual scaling.
