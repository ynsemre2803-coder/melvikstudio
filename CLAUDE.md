# CLAUDE.md — Frontend Website Rules

## Project Brief — Melvikstudio

- **Site name:** Melvikstudio
- **Purpose:** Bir web sitesi tasarım/geliştirme hizmetinin tek sayfalık tanıtım sitesi. Ziyaretçiye "bu kişi/stüdyo internet sitesi yapıyor" mesajını net şekilde vermek.
- **Sections (bu sırayla):** Hero → Hizmetler (Services) → Hakkımda/Hakkımızda (About) → Portfolyo (Portfolio) → İletişim (Contact) → Footer
- **Portfolio content:** Şu an canlıda örnek proje yok. Mockup/görsel taslaklar kullan, her kartın üzerine "Yakında" / "Coming Soon" etiketi ekle. Gerçek proje geldikçe kolayca değiştirilebilecek şekilde (tek bir yerde tanımlı, tekrar kullanılabilir kart yapısı) kodla.
- **Contact methods:** Sadece **WhatsApp linki** (`https://wa.me/90XXXXXXXXXX`) ve **mailto: linki** (`mailto:info@melvikstudio.com`). İletişim formu YOK — backend/3. parti servis gerektirmesin.
- **Target audience / local SEO:** İstanbul merkezli. Local SEO önceliği var — içerik ve schema İstanbul'u hedeflemeli (ör. "İstanbul'da web sitesi tasarımı" gibi doğal, spam olmayan ifadeler).
- **Language:** Türkçe (birincil).
- **Tone:** Profesyonel ama samimi, jenerik ajans diliyle konuşma ("kaliteli hizmet", "vizyonumuz" gibi boş ifadelerden kaçın), somut ve net.

## Hosting Constraint — CRITICAL

- Kullanıcı **hosting satın almıyor**, sadece **domain** satın alacak.
- Site, ücretsiz statik hosting üzerinde çalışacak şekilde tasarlanmalı: Cloudflare Pages, GitHub Pages veya Vercel/Netlify free tier (custom domain destekli).
- **Hiçbir backend, sunucu kodu, veritabanı veya form-processing servisi kullanma.** Sadece statik HTML/CSS/JS.
- İletişim formu ekleme — yukarıda belirtildiği gibi sadece WhatsApp + mailto linkleri kullanılacak.

## SEO & GEO Requirements — CRITICAL

Site hem klasik arama motorları (Google) hem de AI cevap motorları (ChatGPT, Perplexity, Gemini vb. — "Generative Engine Optimization") için optimize edilmeli:

- **Semantic HTML:** Doğru `<h1>` (sadece bir tane), mantıklı `<h2>`/`<h3>` hiyerarşisi, `<header>`, `<main>`, `<footer>`, `<nav>`, `<section>` etiketleri.
- **Meta etiketleri:** `<title>`, `<meta name="description">`, Open Graph (`og:title`, `og:description`, `og:image`, `og:url`) ve Twitter Card etiketleri eksiksiz olmalı.
- **Structured data (JSON-LD):** `LocalBusiness` veya `ProfessionalService` schema.org işaretlemesi ekle — isim, İstanbul konumu, sunulan hizmetler, iletişim (WhatsApp/mail) bilgileriyle. Bu, AI motorlarının siteyi doğru şekilde okuyup özetlemesi için kritik.
- **`sitemap.xml` ve `robots.txt`** dosyalarını da oluştur (tek sayfalık site için basit halleri yeterli).
- **Net, özgün ve somut metin yaz:** GEO için AI motorlarının kolayca alıntılayabileceği, iddialı değil açıklayıcı cümleler kullan (ör. "İstanbul'da küçük işletmeler için tek sayfalık, hızlı yüklenen web siteleri tasarlıyorum" gibi — belirsiz pazarlama dilinden kaçın).
- **Hız:** Tek dosya + CDN yapısı zaten hızlı yüklenmeye yardımcı olur; gereksiz büyük görsel/script ekleme.
- **Erişilebilirlik de SEO'yu destekler:** Görsellerde anlamlı `alt` metni, doğru kontrast oranları.

## Always Do First

- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.

## Reference Images

- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content (images via `https://placehold.co/`, generic copy). Do not improve or add to the design.
- If no reference image: design from scratch with high craft (see guardrails below).
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Local Server

- **Always serve on localhost** — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves the project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking any screenshots.
- If the server is already running, do not start a second instance.

## Screenshot Workflow

- Puppeteer is installed at `C:/Users/nateh/AppData/Local/Temp/puppeteer-test/`. Chrome cache is at `C:/Users/nateh/.cache/puppeteer/`.
- **Always screenshot from localhost:** `node screenshot.mjs http://localhost:3000`
- Screenshots are saved automatically to `./temporary screenshots/screenshot-N.png` (auto-incremented, never overwritten).
- Optional label suffix: `node screenshot.mjs http://localhost:3000 label` → saves as `screenshot-N-label.png`
- `screenshot.mjs` lives in the project root. Use it as-is.
- After screenshotting, read the PNG from `temporary screenshots/` with the Read tool — Claude can see and analyze the image directly.
- When comparing, be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Output Defaults

- Single `index.html` file, all styles inline, unless user says otherwise
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- Mobile-first responsive

## Brand Assets

- Always check the `brand_assets/` folder before designing. It may contain logos, color guides, style guides, or images.
- If assets exist there, use them. Do not use placeholders where real assets are available.
- If a logo is present, use it. If a color palette is defined, use those exact values — do not invent brand colors.
- **Melvikstudio logosu bu klasöre henüz eklenmedi — kullanıcı ekleyene kadar isim tabanlı bir metin-logo (wordmark) kullan, gerçek logo eklendiğinde onunla değiştir.**

## Anti-Generic Guardrails

- **Colors:** Never use default Tailwind palette (indigo-500, blue-600, etc.). Pick a custom brand color and derive from it.
- **Shadows:** Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Never use the same font for headings and body. Pair a display/serif with a clean sans. Apply tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Images:** Add a gradient overlay (`bg-gradient-to-t from-black/60`) and a color treatment layer with `mix-blend-multiply`.
- **Spacing:** Use intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Surfaces should have a layering system (base → elevated → floating), not all sit at the same z-plane.

## Hard Rules

- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
- Do not add any backend, server, database, or form-processing dependency — this site must run on free static hosting only
