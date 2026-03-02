# Sagar Dash - Portfolio Website

A modern, visually stunning portfolio website built with Astro, featuring Aceternity UI components for enhanced animations and effects.

## ✨ Features

- **Modern Design**: Clean, professional design with Aceternity UI components
- **Dark Mode**: Full dark mode support with smooth transitions
- **Animated Effects**: Sparkles, moving borders, gradient backgrounds, and more
- **Responsive**: Fully responsive design for all screen sizes
- **Content-Driven**: Content managed through Astro's Content Collections
- **Fast**: Built with Astro for optimal performance
- **Accessible**: SEO-friendly with semantic HTML

## 🛠 Tech Stack

### Core Framework
- **Astro 5.17** - Modern static site generator
- **TypeScript** - Type-safe development

### Styling
- **Tailwind CSS 3.4** - Utility-first CSS framework
- **@astrojs/tailwind** - Astro Tailwind integration
- **CSS Variables** - Dynamic theming system

### UI Components (Aceternity UI)
- **Sparkles** - Animated particle effects
- **MovingBorder** - Animated gradient borders
- **HeroHighlight** - Floating gradient backgrounds
- **MagicButton** - Spinning gradient border buttons

### Libraries
- **framer-motion** - Animation library
- **clsx & tailwind-merge** - Utility class management
- **rss-parser** - RSS feed parsing
- **satori & resvg** - OG image generation
- **jspdf** - PDF generation

## 📁 Project Structure

```
/
├── public/              # Static assets (images, fonts, favicon)
├── src/
│   ├── components/       # Reusable components
│   │   ├── ui/        # Aceternity UI components
│   │   │   ├── Sparkles.astro
│   │   │   ├── MovingBorder.astro
│   │   │   ├── HeroHighlight.astro
│   │   │   └── MagicButton.astro
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── ThemeToggle.astro
│   │   └── SidebarTimeline.astro
│   ├── content/         # Content collections
│   │   ├── about.md
│   │   ├── config.ts
│   │   ├── articles/
│   │   ├── experience/
│   │   ├── opensource/
│   │   ├── projects/
│   │   └── skills/
│   ├── layouts/         # Page layouts
│   │   └── BaseLayout.astro
│   ├── lib/            # Utility functions
│   │   └── utils.ts
│   ├── pages/           # Route pages
│   │   ├── index.astro
│   │   ├── articles/[slug].astro
│   │   └── projects/[slug].astro
│   └── styles/         # Global styles
│       └── global.css
├── astro.config.mjs     # Astro configuration
├── tailwind.config.mjs   # Tailwind configuration
├── tsconfig.json        # TypeScript configuration
└── package.json        # Project dependencies
```

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ installed
- npm or yarn package manager

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd portfolio
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to:
```
http://localhost:4321
```

## 📝 Content Management

### Adding a New Project

Create a new markdown file in `src/content/projects/`:

```markdown
---
title: "Project Name"
description: "A brief description of the project"
date: 2024-01-01
coverImage: "/images/project-cover.jpg"
tags: ["React", "TypeScript", "Node.js"]
link: "https://github.com/username/project"
---

# Project Name

Detailed description of your project...

## Key Features

- Feature 1
- Feature 2
- Feature 3
```

### Adding Experience

Create a new markdown file in `src/content/experience/`:

```markdown
---
title: "Job Title"
company: "Company Name"
period: "Jan 2020 - Present"
order: 1
---

## Job Title at Company Name

- Achievement 1
- Achievement 2
- Achievement 3
```

### Adding Skills

Create a new markdown file in `src/content/skills/`:

```markdown
---
title: "Languages"
order: 1
skills: ["TypeScript", "JavaScript", "Python", "Go"]
---
```

### Adding Open Source Projects

Create a new markdown file in `src/content/opensource/`:

```markdown
---
title: "Project Name"
description: "Description of the open source project"
link: "https://github.com/username/project"
role: "author"  # or "contributor"
order: 1
---
```

## 🎨 Aceternity UI Components

The portfolio includes several Aceternity UI components for enhanced visual effects:

### Sparkles

Adds animated sparkle particles to any container.

```astro
<Sparkles 
  particleColor="var(--brand-color)" 
  size={8} 
  particleDensity={100}
/>
```

### MovingBorder

Creates a card with an animated moving border gradient.

```astro
<MovingBorder className="p-4">
  <div>Your content here</div>
</MovingBorder>
```

### HeroHighlight

Wrapper for hero sections with floating gradient backgrounds.

```astro
<HeroHighlight class="section hero">
  <div>Your hero content</div>
</HeroHighlight>
```

### MagicButton

A stunning button with a spinning gradient border.

```astro
<!-- As a button -->
<MagicButton>Click Me</MagicButton>

<!-- As a link -->
<MagicButton href="/path" target="_blank">Link Button</MagicButton>
```

For more details, see [ACETERNITY_UI_INTEGRATION.md](./ACETERNITY_UI_INTEGRATION.md).

## 🔧 Configuration

### Tailwind CSS

Configure Tailwind in `tailwind.config.mjs`:

```javascript
export default {
  content: [
    "./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}",
  ],
  darkMode: 'class',
  theme: {
    extend: {
      // Your custom theme
    },
  },
  plugins: [],
}
```

### Astro

Configure Astro in `astro.config.mjs`:

```javascript
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';

export default defineConfig({
  integrations: [tailwind()],
});
```

### Theme Colors

Edit CSS variables in `src/styles/global.css`:

```css
:root {
  --bg-color: #ffffff;
  --text-color: #1a1a1a;
  --brand-color: #0070f3;
  --card-bg: #f9f9f9;
  --border-color: #eaeaea;
}

:root.dark {
  --bg-color: #111111;
  --text-color: #f5f5f5;
  --brand-color: #3291ff;
  --card-bg: #1a1a1a;
  --border-color: #333333;
}
```

## 🏗️ Building for Production

Build the site for production:

```bash
npm run build
```

The optimized site will be generated in the `dist/` directory.

Preview the production build:

```bash
npm run preview
```

## 📦 Deployment

This site can be deployed to any static hosting service:

### Vercel

```bash
npm install -g vercel
vercel
```

### Netlify

```bash
npm install -g netlify-cli
netlify deploy --prod
```

### GitHub Pages

1. Build the site: `npm run build`
2. Push the `dist` folder to a GitHub repository
3. Enable GitHub Pages in repository settings

### Cloudflare Pages

1. Connect your GitHub repository
2. Set build command: `npm run build`
3. Set build output directory: `dist`

## 🧞 Available Scripts

| Command | Description |
|---------|-------------|
| `npm install` | Install dependencies |
| `npm run dev` | Start development server |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build |
| `npm run astro ...` | Run Astro CLI commands |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License.

## 🌟 Acknowledgments

- **Astro** - The amazing web framework
- **Aceternity UI** - Beautiful UI components
- **Tailwind CSS** - Utility-first CSS framework
- **Framer Motion** - Smooth animations

## 📞 Contact

- **Email**: talk@sagardash.me
- **Telegram**: [@sagardashme](https://t.me/sagardashme)
- **Medium**: [@sagar-dash290](https://medium.com/@sagar-dash290)

---

Built with ❤️ using Astro and Aceternity UI