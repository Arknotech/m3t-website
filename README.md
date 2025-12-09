M3T Website (Static) - Deployed in Vercel (December 09, 2025)
This is project dedicated to M3T Data Management System and creating a dedicated website for them to start with. I am planning to increase features 
to include backend web components (Admin Panel, Database, Auth, Storage, and all that). 

Tech Stacks: Vanilla HTML, CSS, Javascript
Tools: VS Code, ChatGPT/Claude (AI Coding)
Possible Backend: SupaBase - BaaS 

Static Website Link: https://m3t-website.vercel.app/

--------------------------------------------------------------


The M3T Data Management Website is a full-stack web application designed for a professional Data Management Services company.
This project includes:

✔ Fully responsive frontend (Tailwind CSS + Dark Mode UI)
✔ Contact form with secure data capture
✔ Supabase database + storage for file uploads
✔ Secure backend API (Vercel Serverless Functions)
✔ Admin login system (JWT Auth)
✔ Admin Dashboard with analytics, charts, filters & CSV export

______________________________________________________________________________________________________________________________

# M3T Web Project - AI Coding Instructions

## Project Overview
M3T Data Management is a **static HTML/CSS/JavaScript website** (no backend framework) showcasing data analytics and market research services. All pages are self-contained HTML files using **Tailwind CSS** for styling and **vanilla JavaScript** for interactivity.

## Architecture & File Organization

### Page Structure
- **`index.html`** - Homepage (landing page with chat widget)
- **`about.html`** - Company information
- **`contact.html`** - Contact form with file upload capability
- **`contact_simple.html`** - Simplified contact form variant
- **`services_main.html`** - Main services overview with dropdown navigation
- **`services_*.html`** - Individual service detail pages:
  - `services_dataprocess.html`
  - `services_qual.html` (Qualitative Research)
  - `services_quan.html` (Quantitative Research)
  - `services_marketmapping.html`
  - `services_mystshop.html`
  - `services_retailstudies.html`
  - `services_traffic_count.html`

### Key Design Pattern: Replicated Chat Widget
Every HTML page includes an identical chat launcher component (`id="chatBtn"` and `id="chatPanel"`). When modifying this widget:
- Update **all pages simultaneously** - changes must be consistent across all files
- The widget includes: launcher button, collapsible panel, message display, input area, FAQ quick-links
- Widget queries `/api/faq` endpoint for responses (backend integration point)

## Styling Conventions

### Color System (Custom Tailwind Colors)
Every page extends Tailwind with these custom colors:
```javascript
colors: {
    m3tViolet: '#A066CB',
    m3tBlue: '#1736B1',
    pageBg: '#0A1026'
}
```
- Use `from-m3tViolet to-m3tBlue` for gradient buttons
- Use `border-m3tViolet/30` for subtle borders
- Background is always dark: `bg-bgDark` or `#0A1026`

### Common CSS Classes
- `.animate-fadeIn` - Fade-in animation (defined in most pages)
- `.grid-bg` - Subtle grid background pattern
- **Gradients**: `bg-gradient-to-r from-m3tBlue/80 via-[#0A1530]` for headers

## JavaScript Patterns

### Chat Widget Functions (Cross-Page)
```javascript
sendMessage()      // Sends user input to /api/faq endpoint
sendFAQ(type)      // Sends predefined FAQ requests ('services', 'coverage', 'contact')
addUserMessage()   // Appends user message to chat panel
addBotMessage()    // Appends bot response to chat panel
```

### Form Handling (contact.html specific)
- File uploads converted to Base64 before transmission
- Form data serialized as JSON and sent to backend endpoint
- Example: `toBase64(file)` converts File object to Base64 string

### Navigation Pattern
Services pages use **dropdown menus** with click-to-open behavior (not hover):
```javascript
document.getElementById("servicesBtn").onclick = // toggle dropdown display
```

## Important Conventions

### No Build Process
- Direct Tailwind CDN usage (`<script src="https://cdn.tailwindcss.com"></script>`)
- No npm, webpack, or build tools
- All styling is inline or in `<style>` tags

### File Naming
- Service pages follow pattern: `services_[servicename].html`
- Avoid special characters except underscores in filenames
- `contact_simple.html` is a variant; maintain both if used separately

### Backend Integration Points
1. **Chat Widget**: POST to `/api/faq` with payload `{ message: string }` or `{ faq: string }`
2. **Contact Form**: POST to `/api/contact` with file upload support (Base64 encoded)

### Consistency Across Pages
When updating shared components (chat widget, navigation, color scheme):
1. Make changes to **all pages** - this is not a template-based system
2. Test navigation links between pages
3. Verify chat widget styling matches across all pages

## Development Tips

- **Modifying Chat Widget**: Use Find & Replace across all `.html` files to ensure consistency
- **Service Pages**: Each service page is independent; changes to one don't auto-propagate
- **Testing Navigation**: Check `<a href="">` links resolve correctly (all files in root directory)
- **Color Updates**: Change custom Tailwind color definitions in `<script>` tags (not in CSS)
