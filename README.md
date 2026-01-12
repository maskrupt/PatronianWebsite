# Patronian Website

A futuristic portfolio for a Streamer and Software Developer, built with Vue 3, Vite, Tailwind CSS, and Vue Router.

## Theme & Style
The website features a high-contrast futuristic theme inspired by the Patronian character concept:
- **Colors**: Deep Black (`#0a0a0a`), Clean White (`#f5f5f5`), and Golden Brass (`#d4af37`).
- **Typography**: Space Grotesk (Futuristic font).
- **Accents**: Subtle purple glows and geometric patterns.

## Features
- **Responsive Landing Page**: Hero section with futuristic animations.
- **Routing**: Client-side navigation between Home and About pages.
- **Tailwind CSS 4**: Modern styling with custom color palette.

## Getting Started

### Prerequisites
- Node.js (v20.19+ or v22.12+)
- npm

### Installation
```bash
npm install
```

### Development
```bash
npm run dev
```

### Build
```bash
npm run build
```

## Deployment

### Cloudflare Pages
This project is ready for deployment on **Cloudflare Pages**. 

1. **Connect Repository**: Connect your GitHub repository to Cloudflare Pages.
2. **Build Settings**:
   - **Framework Preset**: `Vite`
   - **Build Command**: `npm run build`
   - **Build Output Directory**: `dist`
3. **Environment Variables**: Ensure you are using Node.js 20 or higher (Set `NODE_VERSION` to `20` if necessary).

The project includes a `_redirects` file in the `public` folder to ensure smooth navigation for the Vue Router SPA.

## Structure
- `src/views/Home.vue`: Main landing page with interactive hero section.
- `src/views/About.vue`: Detailed information about the persona.
- `src/router/index.js`: Routing configuration.
- `src/style.css`: Global styles and Tailwind directives.
