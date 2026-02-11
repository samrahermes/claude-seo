# SEO Audit Report — vitaminkorgen.se

**Audit Date:** 2026-02-11
**Tool:** Claude SEO v1.1.0
**Business Type Detected:** Local Service (Fruktkorgar / Kontorsfrukt — Stockholm)
**Pages Analyzed:** 8 (full sitemap)

---

## Executive Summary

### SEO Health Score: 14 / 100

| Category | Score | Weight | Weighted |
|----------|-------|--------|----------|
| Technical SEO | 15 / 100 | 25% | 3.8 |
| Content Quality | 10 / 100 | 25% | 2.5 |
| On-Page SEO | 15 / 100 | 20% | 3.0 |
| Schema / Structured Data | 0 / 100 | 10% | 0.0 |
| Performance (CWV) | 40 / 100 | 10% | 4.0 |
| Images | 10 / 100 | 5% | 0.5 |
| AI Search Readiness | 5 / 100 | 5% | 0.3 |

**Verdict:** Webbplatsen har allvarliga, grundläggande SEO-problem som hindrar sökmotorer från att indexera och ranka sidan. Huvudproblemet är att hela sajten är en React SPA (Single Page Application) med ren klient-rendering (CSR) — ingen server-side rendering (SSR) eller static site generation (SSG). Sökmotorer ser i princip en tom sida.

### Topp 5 Kritiska Problem

1. **Klient-rendering utan SSR/SSG** — All content renderas via JavaScript. HTML-källan innehåller `<div id="root"></div>` och 8 ord.
2. **Identiska meta-taggar på alla sidor** — Samma title och description på alla 8 sidor.
3. **Noll crawlbart innehåll** — Sökmotorer ser 8 ord istället för faktiskt sidinnehåll.
4. **Ingen heading-struktur (H1/H2/H3)** — Inga headings i HTML-källan.
5. **Ingen Schema/Structured Data** — Noll JSON-LD markup.

### Topp 5 Quick Wins

1. Implementera SSR eller pre-rendering för alla sidor.
2. Unika title-taggar och meta-descriptions per sida.
3. Lägg till LocalBusiness JSON-LD schema.
4. Lägg till kanoniska URL:er (canonical tags) på varje sida.
5. Fixa OG-bild URL (ta bort mellanslag).

---

## 1. Technical SEO (15 / 100)

### 1.1 Crawlability

| Check | Status | Detaljer |
|-------|--------|----------|
| robots.txt | ✅ PASS | Finns och tillåter alla crawlers. Sitemap refererad. |
| Sitemap.xml | ⚠️ VARNING | Finns med 8 URL:er. Men /varuautomater-kaffemaskin saknas i sitemap trots att den är indexerad av Google. |
| Server-Side Rendering | ❌ FAIL | Ren CSR (React SPA). `<div id="root"></div>` — ingen renderad HTML. |
| Crawlbart innehåll | ❌ FAIL | Bara 8 ord synliga i HTML-källan för alla sidor. |
| Redirect-kedjor | ✅ PASS | Inga onödiga redirects detekterade. |
| HTTP Status | ✅ PASS | Alla sidor returnerar 200. |

### 1.2 Indexability

| Check | Status | Detaljer |
|-------|--------|----------|
| Canonical tags | ❌ FAIL | Saknas på alla sidor. |
| meta robots | ✅ PASS | Inga noindex-direktiv (men utan crawlbart innehåll spelar det liten roll). |
| Google-indexering | ❌ FAIL | Bara 3 av 8+ sidor indexerade (/, /produkter, /varuautomater-kaffemaskin). |
| Duplicerat innehåll | ❌ FAIL | Alla sidor returnerar identisk HTML till sökmotorer. |
| Hreflang | ❌ FAIL | Saknas. Sajten har `lang="sv"` men inga hreflang-taggar. |

### 1.3 Security

| Check | Status | Detaljer |
|-------|--------|----------|
| HTTPS | ✅ PASS | Aktiv med giltigt certifikat. |
| HSTS | ✅ PASS | `strict-transport-security: max-age=31536000; includeSubDomains` |
| Referrer-Policy | ✅ PASS | `strict-origin-when-cross-origin` |
| X-Content-Type-Options | ✅ PASS | `nosniff` |
| Content-Security-Policy | ❌ FAIL | Saknas. |
| X-Frame-Options | ❌ FAIL | Saknas. |
| Permissions-Policy | ❌ FAIL | Saknas. |

### 1.4 URL Structure

| Check | Status | Detaljer |
|-------|--------|----------|
| Rena URL:er | ✅ PASS | Bra URL-struktur (/produkter, /blogg, /om-oss, /kontakt). |
| URL-konsistens | ⚠️ VARNING | Sitemap har /varuautomat men Google har indexerat /varuautomater-kaffemaskin — inkonsekvent. |
| Trailing slashes | ✅ PASS | Konsekvent utan trailing slashes. |

### 1.5 Mobile Optimization

| Check | Status | Detaljer |
|-------|--------|----------|
| Viewport meta | ✅ PASS | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` |
| Responsiv | ⚠️ OKÄNT | Kan ej verifieras utan JS-rendering. |

### 1.6 Core Web Vitals (Uppskattning baserad på källkod)

| Metric | Uppskattning | Tröskel | Status |
|--------|-------------|---------|--------|
| LCP | >4s (troligt) | <2.5s | ❌ FAIL |
| INP | Okänt | <200ms | ⚠️ OKÄNT |
| CLS | Okänt | <0.1 | ⚠️ OKÄNT |

**Orsak:** En ren CSR-applikation kräver att hela JavaScript-bundlen laddas, parsas och exekveras innan första meningsfulla innehåll visas. Detta ger typiskt dåliga LCP-värden.

### 1.7 JavaScript Rendering

| Check | Status | Detaljer |
|-------|--------|----------|
| Rendering-typ | ❌ CSR | Ren klient-rendering via React. |
| JS Bundle | ⚠️ VARNING | `assets/index-BsmIKI_A.js` (modul) — storleken okänd men SPA-bundles tenderar att vara stora. |
| Hosting | ℹ️ INFO | Lovable.app (no-code plattform) via Cloudflare CDN. |

---

## 2. Content Quality (10 / 100)

### 2.1 E-E-A-T Assessment

| Signal | Score | Detaljer |
|--------|-------|----------|
| Experience | 5 / 100 | Ingen synlig förstahandsupplevelse i HTML-källan. |
| Expertise | 5 / 100 | Inga synliga expertissignaler. |
| Authoritativeness | 10 / 100 | Meta-beskrivning nämner "Sedan 2021" och "150+ företag" — men ej crawlbart. |
| Trustworthiness | 15 / 100 | HTTPS OK, men ingen kontaktinfo i crawlbar HTML. |
| **Totalt E-E-A-T** | **9 / 100** | |

### 2.2 Content per sida (HTML-källa)

| Sida | Ord | Min. krav | Status |
|------|-----|-----------|--------|
| / (Startsida) | 8 | 500 | ❌ FAIL (98% under minimum) |
| /produkter | 8 | 800 (Tjänstesida) | ❌ FAIL |
| /blogg | 8 | N/A (listning) | ❌ FAIL |
| /om-oss | 8 | 500 | ❌ FAIL |
| /kontakt | 8 | N/A | ❌ FAIL |
| /offertforfragan | 8 | N/A | ❌ FAIL |
| /blommor | 8 | 800 (Tjänstesida) | ❌ FAIL |
| /varuautomat | 8 | 800 (Tjänstesida) | ❌ FAIL |

**Alla sidor visar bara 8 ord för sökmotorer** på grund av CSR-problemet.

### 2.3 Duplicerat Innehåll

**100% duplicerat** — alla sidor returnerar exakt samma HTML till sökmotorer. Detta innebär att Google behandlar hela sajten som en enda sida med samma innehåll.

### 2.4 AI-genererat Innehåll

Sajten är byggd med Lovable.app (en AI-driven no-code plattform). Twitter-kortet refererar till `@lovable_dev`. Det innebär i sig inget negativt, men E-E-A-T-signaler och unikt innehåll är extra viktigt att säkerställa.

---

## 3. On-Page SEO (15 / 100)

### 3.1 Title Tags

| Sida | Title | Status |
|------|-------|--------|
| Alla 8 sidor | "Fruktkorg på jobbet Stockholm \| Fruktkorgar till kontoret - Vitaminkorgen" | ❌ FAIL — Identisk title på alla sidor |

**Problem:**
- Samma title överallt — Google kan inte särskilja sidorna.
- Title-längd: 72 tecken (OK men kunde optimeras per sida).

### 3.2 Meta Descriptions

| Sida | Description | Status |
|------|-------------|--------|
| Alla 8 sidor | "Fruktkorg på jobbet Stockholm ✓ Vi levererar färska fruktkorgar..." | ❌ FAIL — Identisk description |

**Problem:** Samma meta description på alla sidor. Varje sida behöver en unik, sidspecifik description.

### 3.3 OG & Twitter Tags

| Check | Status | Problem |
|-------|--------|---------|
| OG Title | ⚠️ VARNING | Skiljer sig från page title (inkonsekvent). |
| OG Description | ⚠️ VARNING | Samma på alla sidor. |
| OG Image | ❌ FAIL | URL innehåller mellanslag: `...VitaminKorgen 2.jpg` — kan orsaka problem vid delning. |
| Twitter Site | ❌ FAIL | Pekar på `@lovable_dev` istället för företagets eget konto. |
| Twitter Card | ✅ PASS | `summary_large_image` — korrekt typ. |

### 3.4 Heading Structure

| Check | Status |
|-------|--------|
| H1 | ❌ FAIL — Finns ej i HTML-källan (0 st) |
| H2 | ❌ FAIL — Finns ej i HTML-källan (0 st) |
| H3 | ❌ FAIL — Finns ej i HTML-källan (0 st) |

### 3.5 Internal Linking

| Check | Status |
|-------|--------|
| Interna länkar i HTML | ❌ FAIL — 0 interna länkar synliga i källkoden |
| Navigation | ❌ FAIL — Ej crawlbar (renderas av JS) |

### 3.6 Övriga meta-taggar

| Tag | Värde | Status |
|-----|-------|--------|
| `meta keywords` | "fruktkorg på jobbet stockholm, fruktkorgar stockholm..." | ⚠️ ONÖDIG — Google ignorerar meta keywords sedan 2009. |
| `meta author` | "Vitaminkorgen AB" | ✅ OK |
| `lang` attribut | `sv` | ✅ PASS |

---

## 4. Schema / Structured Data (0 / 100)

### 4.1 Befintlig Schema

**Ingen Schema/JSON-LD hittad** på någon sida.

### 4.2 Rekommenderade Schema-typer

| Schema-typ | Prioritet | Var |
|------------|-----------|-----|
| LocalBusiness | Kritisk | Startsidan |
| Service | Hög | /produkter, /blommor, /varuautomat |
| Organization | Hög | /om-oss |
| BreadcrumbList | Medium | Alla sidor |
| Product | Medium | /produkter (individuella produkter) |
| ContactPage | Medium | /kontakt |
| WebSite (med SearchAction) | Low | Startsidan |

### 4.3 Exempel: LocalBusiness Schema

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Vitaminkorgen",
  "description": "Vi levererar färska fruktkorgar på jobbet i Stockholm",
  "url": "https://vitaminkorgen.se",
  "telephone": "[TELEFONNUMMER]",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Stockholm",
    "addressCountry": "SE"
  },
  "areaServed": {
    "@type": "City",
    "name": "Stockholm"
  },
  "foundingDate": "2021",
  "priceRange": "$$"
}
```

---

## 5. Performance (40 / 100)

### 5.1 Positiva signaler

- **Cloudflare CDN** — Bra geografisk distribution och caching.
- **HTTP/2** — Stöds.
- **Gzip/Deflate** — Accept-Encoding finns.
- **ETag** — Korrekt caching-header.

### 5.2 Negativa signaler

- **CSR-arkitektur** — JavaScript måste laddas, parsas och exekveras innan innehåll visas.
- **Inga preload/prefetch hints** i HTML-källan.
- **Google Analytics + Flock Analytics** — Två analytics-script som potentiellt blockerar rendering.
- **Ingen preconnect** till externa domäner (googleapis.com, googletagmanager.com).

### 5.3 Resursanalys

| Resurs | Typ | Observation |
|--------|-----|-------------|
| `assets/index-BsmIKI_A.js` | JS Module | Hela applikationsbundlen — ej code-split synligt i HTML. |
| `assets/index-DbWCcWDi.css` | CSS | Stilmall. |
| `gtag/js?id=G-JZJV317Q2E` | Analytics | Externt script, asynkront. |
| `~flock.js` | Analytics | Ytterligare analytics — deferred. |

---

## 6. Images (10 / 100)

### 6.1 HTML-bildanalys

**0 bilder i HTML-källan** — alla bilder laddas via JavaScript.

### 6.2 OG/Twitter-bild

| Check | Status | Detaljer |
|-------|--------|----------|
| OG Image | ⚠️ VARNING | URL har mellanslag: `...VitaminKorgen 2.jpg` |
| Hosting | ℹ️ INFO | Hostad på `storage.googleapis.com` (Google Cloud Storage) |
| Alt-text | ❌ FAIL | Ingen alt-text möjlig att verifiera i källkod. |
| Bildformat | ⚠️ OKÄNT | JPG (borde använda WebP/AVIF för modern optimering). |
| Lazy loading | ❌ FAIL | Inga `loading="lazy"` attribut i HTML. |
| Dimensioner | ❌ FAIL | Inga width/height-attribut i HTML. |

---

## 7. AI Search Readiness / GEO (5 / 100)

### 7.1 AI Crawler Access

| Crawler | Åtkomst | Problem |
|---------|---------|---------|
| Googlebot | ✅ Tillåten | Ser bara 8 ord (CSR-problem) |
| GPTBot | ✅ Tillåten | Ser bara 8 ord |
| ClaudeBot | ✅ Tillåten | Ser bara 8 ord |
| PerplexityBot | ✅ Tillåten | Ser bara 8 ord |
| Bingbot | ✅ Tillåten | Ser bara 8 ord |

**Alla crawlers tillåts i robots.txt, men det finns inget crawlbart innehåll.**

### 7.2 llms.txt

❌ **Saknas** — Ingen `/.well-known/llms.txt` finns. Returnerar 404.

### 7.3 Citability Score

| Faktor | Score | Detaljer |
|--------|-------|----------|
| Quotable Facts | 0 / 20 | Inga citeringsbara fakta i HTML |
| Structured Data | 0 / 20 | Ingen schema markup |
| Clear Hierarchy | 0 / 20 | Inga headings |
| Passage Length | 0 / 20 | Inga textpassager |
| Authority Signals | 5 / 20 | Meta-taggar nämner "150+ företag" och "Sedan 2021" |
| **Totalt** | **5 / 100** | |

### 7.4 Brand Mention Signals

Svagt varumärkesrykte online — begränsad synlighet i AI-sökresultat. Utan crawlbart innehåll kan AI-modeller inte referera till sajten som källa.

---

## Appendix

### A. Indexeringsstatus (Google)

| URL | Indexerad | I Sitemap |
|-----|-----------|-----------|
| / | ✅ Ja | ✅ Ja |
| /produkter | ✅ Ja | ✅ Ja |
| /varuautomater-kaffemaskin | ✅ Ja | ❌ Nej |
| /blogg | ❌ Nej | ✅ Ja |
| /om-oss | ❌ Nej | ✅ Ja |
| /kontakt | ❌ Nej | ✅ Ja |
| /offertforfragan | ❌ Nej | ✅ Ja |
| /blommor | ❌ Nej | ✅ Ja |
| /varuautomat | ❌ Nej | ✅ Ja |

### B. Sitemap.xml Analys

- **Antal URL:er:** 8
- **Lastmod:** 2026-01-22 (alla sidor)
- **Changefreq:** Weekly (de flesta), Monthly (om-oss, kontakt)
- **URL som saknas:** /varuautomater-kaffemaskin (indexerad men ej i sitemap)
- **URL-inkonsistens:** /varuautomat i sitemap vs /varuautomater-kaffemaskin indexerad

### C. robots.txt Analys

```
User-agent: Googlebot → Allow: /
User-agent: Bingbot → Allow: /
User-agent: Twitterbot → Allow: /
User-agent: facebookexternalhit → Allow: /
User-agent: * → Allow: /
Sitemap: https://vitaminkorgen.se/sitemap.xml
```

**Status:** ✅ Korrekt konfigurerad men saknar specifika regler för AI-crawlers (GPTBot, ClaudeBot, PerplexityBot).

### D. Hosting & Infrastruktur

| Parameter | Värde |
|-----------|-------|
| Plattform | Lovable.app (AI-driven no-code) |
| CDN | Cloudflare |
| Server | Envoy (proxy) |
| Protokoll | HTTP/2 |
| SSL | Giltigt certifikat |
| Analytics | Google Analytics 4 (G-JZJV317Q2E) + Flock Analytics |
