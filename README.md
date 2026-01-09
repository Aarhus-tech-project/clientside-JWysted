# Viewport-First Framework - Build System

## 📚 Oversigt

Dette er et **compile-time framework** der transformerer HTML attributter til optimeret CSS ved build-time. Frameworket demonstrerer alle dine læringsmål gennem en praktisk implementation.

## 🏗️ Projekt Struktur

```
projekt/
├── src/
│   └── buildHtml.ts         # Compiler der transformerer HTML
├── index.html               # Source HTML (med fw-* attributter)
├── dist/                    # Build output (genereret)
│   ├── index.html          # Transformeret HTML
│   └── framework.css       # Genereret CSS
├── package.json
└── tsconfig.json
```

## 🚀 Sådan kører du det

### 1. Installer dependencies
```bash
npm install
```

### 2. Byg projektet
```bash
npm run build:html
npm run build:ts
```

### 3. Start development server
```bash
npm start
```

Eller kør alle kommandoer på én gang:
```bash
npm run build:html && npm run build:ts && npm start
```

## 🔧 Hvordan det virker

### Step 1: Source HTML (index.html)
Du skriver HTML med framework attributter:

```html
<div fw-center>
  <h1>Hello World</h1>
</div>

<nav fw-align="top">
  <a href="#">Link</a>
</nav>
```

### Step 2: Compilation (src/buildHtml.ts)
TypeScript compiler læser HTML'en og:

1. **Scanner** efter alle `fw-*` attributter
2. **Genererer** CSS regler baseret på fundne attributter
3. **Transformerer** HTML attributter til CSS klasser
4. **Outputter** til `dist/` folder

### Step 3: Output (dist/index.html + framework.css)

**HTML output:**
```html
<div class="fw-center-viewport">
  <h1>Hello World</h1>
</div>

<nav class="fw-align-top">
  <a href="#">Link</a>
</nav>
```

**CSS output (framework.css):**
```css
.fw-center-viewport {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
}

.fw-align-top {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
}
```

## 📖 Framework Attributter

### Viewport Centering
- `fw-center` - Centrerer både X og Y akse i viewport
- `fw-center="x"` - Centrerer kun horisontalt
- `fw-center="y"` - Centrerer kun vertikalt

### Viewport Alignment
- `fw-align="top"` - Top center
- `fw-align="bottom"` - Bottom center
- `fw-align="left"` - Left center
- `fw-align="right"` - Right center
- `fw-align="top-left"` - Top left corner
- `fw-align="top-right"` - Top right corner
- `fw-align="bottom-left"` - Bottom left corner
- `fw-align="bottom-right"` - Bottom right corner

### Container Scope
- `fw-container` - Skaber en container der ændrer positionering fra viewport til relativ

## 🎯 Læringsmål Dækket

### ✅ 1. Client-Server Model & HTTP
- **Compile-time på server**: HTML transformation sker før filen sendes til klient
- **HTTP protokol**: Demonstreret i demo-sektionen med request/response eksempler
- **Build proces**: Viser server-side processing før client modtager filen

### ✅ 2. HTML Struktur & Semantik
- Korrekt DOCTYPE, html, head, body struktur
- Semantiske tags: `<nav>`, `<main>`, `<section>`
- Meta tags for viewport og charset

### ✅ 3. Lister, Links, Billeder
- Ordered lists (`<ol>`) og unordered lists (`<ul>`)
- Navigation med `<a>` links
- Billeder med `<img>` og responsive gallery
- Alt tekst for tilgængelighed

### ✅ 4. Tabeller
- Komplet tabel struktur: `<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>`
- CSS styling med zebra-striping
- Hover effekter

### ✅ 5. HTML Formularer
- Alle input typer: text, email, password, checkbox, select, textarea
- Labels og form validation
- Submit handling

### ✅ 6. CSS Selectors
- Element selectors (`table`, `form`)
- Class selectors (`.card`, `.nav-menu`)
- ID selectors (`#intro`, `#http`)
- Pseudo-classes (`:hover`, `:nth-child`)
- Attribute selectors (`[fw-center]`)

### ✅ 7. CSS Styling
- Typography (font-family, font-size, line-height)
- Colors og backgrounds
- Borders og border-radius
- Shadows (box-shadow, text-shadow)
- Transitions og hover effekter

### ✅ 8. Box Model
- `box-sizing: border-box` globalt
- Margin, padding, border demonstrations
- Width og height calculations
- Content, padding, border, margin forklaring

### ✅ 9. Responsive Design
- Mobile-first approach
- Media queries (@media)
- Flexbox for navigation
- CSS Grid for billeder
- Viewport units (vw, vh)

## 🔍 Compiler Detaljer

### buildHtml.ts Funktioner

#### `findFrameworkAttributes(html: string): Set<string>`
Scanner HTML for alle `fw-*` attributter og returnerer et unikt sæt.

#### `generateClassName(attribute: string, scope: string): string`
Konverterer framework attributter til CSS class names:
- `fw-center` → `fw-center-viewport`
- `fw-align="top"` → `fw-align-top`

#### `generateCSS(attributes: Set<string>): string`
Genererer CSS regler baseret på fundne attributter. Inkluderer:
- Viewport positioning rules
- Alignment rules
- Container scope rules
- Responsive media queries

#### `transformHTML(html: string, attributes: Set<string>): string`
Transformer HTML ved at erstatte framework attributter med CSS klasser.

## 💡 Nøgle Koncepter

### Viewport-First Philosophy
Elementer placeres fra **viewport centrum** som standard, ikke fra øverste venstre hjørne. Dette er fundamentalt anderledes end traditionelle CSS frameworks.

### Compile-Time vs Runtime
- **Runtime frameworks** (React, Vue): Kode kører i browseren
- **Compile-time frameworks** (dette): Transformation sker før deployment
  - Ingen runtime overhead
  - Optimeret CSS
  - Ren HTML output

### Container Opt-In
`fw-container` ændrer positioning kontekst fra viewport til relativ. Dette giver fleksibilitet når du har brug for traditionel layout.

## 🧪 Test Scenarioer

### Scenario 1: Centered Login
```html
<form fw-center>
  <!-- Form stays centered when window resizes -->
</form>
```

### Scenario 2: Fixed Header + Centered Content
```html
<nav fw-align="top">Navigation</nav>
<main fw-center>Content</main>
```

### Scenario 3: Container Scoped
```html
<div fw-container>
  <div fw-center>
    <!-- Centered in container, not viewport -->
  </div>
</div>
```

## 📝 Næste Skridt / Forbedringer

- [ ] TypeScript typer for framework config
- [ ] Flere alignment options (percentage based)
- [ ] Z-index management system
- [ ] Animation utilities
- [ ] Dark mode support i generated CSS
- [ ] Source maps for debugging
- [ ] Watch mode for development

## 🤝 Bidrag

Dette er et lærings-projekt. Koden er struktureret til at være læsevenlig og forståelig for studerende der lærer om:
- HTML/CSS fundamentals
- Build tools og compilation
- TypeScript
- Node.js file system operations

## 📚 Ressourcer

- TypeScript: https://www.typescriptlang.org/
- Node.js fs module: https://nodejs.org/api/fs.html
- HTML Standard: https://html.spec.whatwg.org/
- CSS Positioning: https://developer.mozilla.org/en-US/docs/Web/CSS/position

---

**🎓 Lavet til undervisning i webudvikling**
