# PROJECT BLUEPRINT: Multi-Property Tenant Onboarding Portal

## 1. Core Concept & Business Logic
A B2B SaaS platform built for Property Management Companies (PMCs). Each PMC manages multiple distinct properties (communities, apartment buildings, or single-family portfolios). Each property requires a tailored onboarding experience (custom hero imagery, accent colors, property title, custom welcome note, and downloadable onboarding packets), while individual units hold unit-specific hardware/access data (Wi-Fi, smart lock codes, mailbox numbers).

## 2. Three-Tier Data Inheritance Hierarchy

### Tier 1: Management Company (`companies` table)
- `company_id`: Unique ID
- `company_name`: e.g., "Summit Peak Property Management"
- `company_logo_url`: Corporate badge displayed in the footer or header
- `support_portal_url`: Link to the PMC's main resident portal (for rent/maintenance)

### Tier 2: Property / Community (`properties` table)
*Controls the custom look, feel, and onboarding packet for each specific building.*
- `property_id`: Unique ID (links to `company_id`)
- `property_name`: e.g., "Cahill Pond Apartments" vs. "The Lofts at Downtown"
- `property_tagline`: Custom welcome subtitle
- `hero_image_url`: High-res exterior or lobby photo of that specific property
- `theme_accent_color`: Hex color code tailored to the property's branding
- `welcome_message`: Custom paragraph welcoming the resident to this specific community
- `onboarding_packets`: Array of downloadable PDF/document links specific to this property (e.g., "Cahill Pond Pool & Amenity Rules.pdf", "Move-In Inspection Checklist.pdf", "Parking Pass Application.pdf")
- `utility_providers`: Array of local utility setup links required for this specific property address
- `building_rules`: Accordion items (Trash schedule, quiet hours, pet policies, emergency contacts)

### Tier 3: Unit (`units` table)
*Controls the specific door the tenant is moving into (accessed via unique QR slug).*
- `unit_id`: Unique ID (links to `property_id`)
- `slug_token`: URL identifier (e.g., `cahill-8-x9f2`)
- `unit_number`: e.g., "Unit 8"
- `wifi_ssid` & `wifi_password`: Pre-installed unit Wi-Fi credentials
- `access_notes`: Smart lock instructions, gate code, and mailbox number

## 3. Technical Stack Rules for AI Code Generation
- **Frontend:** Pure HTML5, CSS3 (CSS Custom Properties `--accent-color` for dynamic property theming), and Vanilla JavaScript Web Components. Zero frameworks (no React/Vue build steps) for instant deployment on Netlify subdomains.
- **Backend:** Python FastAPI + Supabase (PostgreSQL).
- **Design Aesthetic:** Mobile-first container (`max-width: 480px`), sleek dark-mode slate UI with dynamic property-specific hero banners and accent glows.