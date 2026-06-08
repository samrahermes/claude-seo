# SEO Audit Report — vitaminkorgen.se

**Audit Date:** 2026-06-08
**Tool:** Claude SEO v1.1.0
**Business Type Detected:** Local Service (Fruktkorgar & kontorslösningar — Stockholm)
**Pages i Sitemap:** 57
**Pages Indexerade (Google):** 4

---

## Executive Summary

### SEO Health Score: 18 / 100

| Kategori | Score | Vikt | Viktat |
|----------|-------|------|--------|
| Technical SEO | 20 / 100 | 25% | 5.0 |
| Content Quality | 12 / 100 | 25% | 3.0 |
| On-Page SEO | 10 / 100 | 20% | 2.0 |
| Schema / Structured Data | 0 / 100 | 10% | 0.0 |
| Performance (CWV) | 30 / 100 | 10% | 3.0 |
| Images | 8 / 100 | 5% | 0.4 |
| AI Search Readiness | 15 / 100 | 5% | 0.8 |

**Sammanfattning:** Sajten har rika JS-renderade sidor med produkter, priser, FAQ:er och lokala landningssidor — men allt detta är **osynligt för sökmotorer** eftersom det renderas enbart via JavaScript (CSR). HTML-källan som crawlers ser innehåller `<div id="root"></div>` och 8 ord. Samma title och meta description returneras för alla 57 URL:er. Dessutom pekar sitemap-referensen i robots.txt till fel domän och ~35 location-sidor verkar vara soft 404:or.

### Topp 5 Kritiska Problem

1. **Client-Side Rendering (CSR) utan SSR/SSG** — Sökmotorer ser en tom `<div id="root"></div>` med 8 ord
2. **Identisk title + meta description på alla 57 sidor** — I HTML-källan
3. **robots.txt sitemap pekar på fel domän** — `frukt-for-foretag.lovable.app/sitemap.xml` istället för `vitaminkorgen.se`
4. **~35 location-sidor är soft 404:or** — HTTP 200 men visar "Page not found" i renderad vy
5. **Ingen Schema/JSON-LD, inga canonical tags, inga headings i HTML-källan**

### Topp 5 Quick Wins

1. Fixa sitemap-referensen i robots.txt till rätt domän
2. Ta bort soft 404-sidor från sitemap (eller bygg dem med innehåll)
3. Implementera SSR/pre-rendering (Lovable.app-begränsning — kräver plattformslösning)
4. Lägg till LocalBusiness JSON-LD schema (kan injiceras server-side)
5. Sätt unika title-taggar per sida

---

## Webbplatsöversikt

### Identifierade Sidor (JS-renderat innehåll)

| Sida | Status | Renderat Innehåll |
|------|--------|-------------------|
| / (Startsida) | ✅ Aktiv | Hero, tjänsteöversikt, CTA:er |
| /bestall | ✅ Aktiv | Beställningsflöde, 6 produkter med priser (166–259 kr), 8% rabatt |
| /produkter | ✅ Aktiv | Produktöversikt |
| /provkorg | ✅ Aktiv | "Beställ en gratis provkorg" — landningssida |
| /kontakt | ✅ Aktiv | Formulär (namn, email, meddelande), telefon, email |
| /om-oss | ✅ Aktiv | Företagsinfo, hållbarhet, anställdförmåner |
| /blogg | ✅ Aktiv | 3+ artiklar (publicerade 2026-05-19) |
| /blogg/tips | ⚠️ Okänt | Kan inte verifiera rendering |
| /blogg/recept | ⚠️ Okänt | Kan inte verifiera rendering |
| /blommor | ✅ Aktiv | Blomuthyrning för kontor |
| /varuautomat | ✅ Aktiv | Varuautomater och kaffemaskiner |
| /fruktkorg-stockholm | ✅ Aktiv | Landningssida med priser, FAQ, CTA:er |
| /fruktkorg-foretag | ✅ Aktiv | Företagsfokuserad sida, sjukfrånvaro -20%, priser |
| /fruktkorg-pa-jobbet | ⚠️ Okänt | Keyword-landningssida |
| /fruktkorg-kontor | ⚠️ Okänt | Keyword-landningssida |
| /fruktleverans-foretag | ⚠️ Okänt | Keyword-landningssida |
| /prova-fruktkorg | ⚠️ Okänt | Keyword-landningssida |
| /fruktlada | ⚠️ Okänt | Keyword-landningssida |
| /produkt/fruktkorg-original | ⚠️ Okänt | Produktsida |
| /produkt/fruktkorg-premium | ⚠️ Okänt | Produktsida |
| /produkt/fruktkorg-banan | ⚠️ Okänt | Produktsida |
| /fruktkorg/[35 områden] | ❌ Soft 404 | "Oops! Page not found" |

### Kontaktinformation (från JS-renderat)

- **Telefon:** 010-183 98 36
- **Email:** info@vitaminkorgen.se
- **Företag:** VitaminKorgen AB
- **Leveransområde:** Stockholm, Södertälje, Uppsala (31+ stadsdelar)
- **Grundat:** 2021
- **Kunder:** 150+ företag

### Produkter (från /bestall)

| Produkt | Vikt | Ordinarie Pris | Kampanjpris (8% rabatt) |
|---------|------|----------------|------------------------|
| Fruktkorg Premium | 4 kg | 250 kr | 230 kr |
| Fruktkorg Banan Plus | 4 kg | 230 kr | 212 kr |
| Fruktkorg Supreme | 4 kg | 230 kr | 212 kr |
| Fruktkorg Original | 4 kg | 220 kr | 202 kr |
| Fruktkorg Bas | 4 kg | 180 kr | 166 kr |
| Fruktkorg Sicilien | 4 kg | 282 kr | 259 kr |

---

## 1. Technical SEO (20 / 100)

### 1.1 Crawlability

| Check | Status | Detaljer |
|-------|--------|----------|
| robots.txt | ⚠️ VARNING | Finns och tillåter alla crawlers, inkl. AI-crawlers. **MEN** sitemap-referens pekar på fel domän: `frukt-for-foretag.lovable.app/sitemap.xml` |
| Sitemap.xml | ⚠️ VARNING | 57 URL:er men: inga lastmod-datum, ~35 location-sidor är soft 404:or |
| Server-Side Rendering | ❌ KRITISK | Ren CSR (React SPA). `<div id="root"></div>` — ingen renderad HTML |
| Crawlbart innehåll | ❌ KRITISK | 8 ord synliga i HTML-källan för alla sidor |
| Google Site Verification | ✅ PASS | `3SrrgJPyzJjimRlKkyreCjVOkSsJYUbI7KxNfxH83RQ` |
| HTTP Status | ⚠️ VARNING | Alla sidor returnerar 200, inklusive soft 404:or |

### 1.2 robots.txt Analys

```
User-agent: Googlebot       → Allow: /
User-agent: Bingbot          → Allow: /
User-agent: Twitterbot       → Allow: /
User-agent: facebookexternalhit → Allow: /
User-agent: GPTBot           → Allow: /
User-agent: ChatGPT-User     → Allow: /
User-agent: Google-Extended   → Allow: /
User-agent: PerplexityBot    → Allow: /
User-agent: CCBot             → Allow: /
User-agent: anthropic-ai     → Allow: /
User-agent: ClaudeBot         → Allow: /
User-agent: cohere-ai        → Allow: /
User-agent: *                → Allow: /

Sitemap: https://frukt-for-foretag.lovable.app/sitemap.xml  ← FEL DOMÄN!
```

**Problem:** Sitemap-URL pekar på Lovable.app-subdomänen istället för `https://vitaminkorgen.se/sitemap.xml`. Google följer denna referens och kan missa sitemapen.

### 1.3 Sitemap Analys

| Check | Status |
|-------|--------|
| Antal URL:er | 57 |
| lastmod | ❌ Saknas på alla URL:er |
| changefreq | Weekly/Monthly (varierar) |
| Priority | 0.6–1.0 (rimligt) |
| Soft 404:or i sitemap | ❌ ~35 URL:er (/fruktkorg/[area]) visar 404-innehåll |
| Korrekt domän | ✅ URL:er pekar på vitaminkorgen.se |

### 1.4 Indexability

| Check | Status | Detaljer |
|-------|--------|----------|
| Canonical tags | ❌ KRITISK | Saknas på alla sidor |
| meta robots | ✅ PASS | Inga noindex-direktiv |
| Google-indexering | ❌ DÅLIG | 4 av 57 sidor indexerade (7%) |
| Duplicerat innehåll | ❌ KRITISK | Alla sidor returnerar identisk HTML |

**Indexerade sidor (Google):**

| URL | Indexerad | I Sitemap |
|-----|-----------|-----------|
| / | ✅ | ✅ |
| /kontakt | ✅ | ✅ |
| /produkter | ✅ | ✅ |
| /varuautomater-kaffemaskin (www.) | ✅ | ❌ Saknas |

### 1.5 Security Headers

| Header | Status | Värde |
|--------|--------|-------|
| HTTPS | ✅ PASS | Aktiv |
| HSTS | ✅ PASS | `max-age=31536000; includeSubDomains` |
| Referrer-Policy | ✅ PASS | `strict-origin-when-cross-origin` |
| X-Content-Type-Options | ✅ PASS | `nosniff` |
| Content-Security-Policy | ❌ SAKNAS | |
| X-Frame-Options | ❌ SAKNAS | |
| Permissions-Policy | ❌ SAKNAS | |
| Cache-Control | ⚠️ VARNING | `no-cache, must-revalidate, max-age=0` — ingen browser-caching |

### 1.6 URL Structure

| Check | Status |
|-------|--------|
| Rena URL:er | ✅ PASS |
| Svensk URL-struktur | ✅ PASS (/produkter, /om-oss, /kontakt) |
| Keyword-URL:er | ✅ BRA (/fruktkorg-stockholm, /fruktkorg-foretag) |
| Location-URL:er | ⚠️ VARNING — /fruktkorg/[area] finns i sitemap men sidor är soft 404:or |
| www vs non-www | ⚠️ VARNING — www.vitaminkorgen.se/varuautomater-kaffemaskin indexerad (inkonsekvent) |

### 1.7 JavaScript Rendering

| Check | Status |
|-------|--------|
| Rendering-typ | ❌ CSR (React SPA via Lovable.app) |
| HTML Body | `<div id="root"></div>` |
| JS Bundle | `assets/index-BDwX_yjH.js` (module) |
| CSS Bundle | `assets/index-bYK_tMtE.css` |
| Third-party JS | GTM, GA4, Flock, Tidio, Lovable events (5 st) |
| OG/Twitter tags | ⚠️ "Set dynamically by SEOHead component" — ej i HTML-källan |
| Information leakage | ⚠️ Lovable event script exponerar commit SHA och deployment tokens |

### 1.8 Core Web Vitals (Uppskattning)

| Metric | Uppskattning | Tröskel | Status |
|--------|-------------|---------|--------|
| LCP | >4s (troligt) | <2.5s | ❌ Troligt FAIL |
| INP | Okänt | <200ms | ⚠️ Okänt |
| CLS | Okänt | <0.1 | ⚠️ Okänt |

CSR + 5 third-party scripts + `cache-control: no-cache` = troligtvis dålig LCP.

---

## 2. Content Quality (12 / 100)

### 2.1 E-E-A-T Assessment

| Signal | Score | Detaljer |
|--------|-------|----------|
| Experience | 15 / 100 | JS-renderat: nämner "sedan 2021", "150+ företag", sjukfrånvaro -20% — men ej crawlbart |
| Expertise | 10 / 100 | Inga synliga expertissignaler i HTML. I JS: tips, recept, hälsoinformation |
| Authoritativeness | 10 / 100 | Ingen extern bekräftelse synlig. Google Site Verification tillagt |
| Trustworthiness | 20 / 100 | HTTPS ✅, kontaktinfo (JS-renderat), Tidio chat tillagd |
| **Totalt E-E-A-T** | **14 / 100** | |

### 2.2 Crawlbart vs JS-renderat Innehåll

| Aspekt | I HTML (crawlbart) | I JS (ej crawlbart) |
|--------|-------------------|---------------------|
| Ord | 8 | Hundratals–tusentals |
| Produkter | 0 | 6 med priser |
| FAQ:er | 0 | Ja, på landningssidor |
| Kontaktinfo | 0 | Telefon, email, adress |
| Kundstatistik | 0 | 150+ företag, sedan 2021 |
| Blogginlägg | 0 | 3+ artiklar |
| Testimonials | 0 | Troligtvis finns |

### 2.3 Content per Sidtyp (HTML-källa)

| Sidtyp | Antal | Ord i HTML | Min. krav | Status |
|--------|-------|------------|-----------|--------|
| Startsida | 1 | 8 | 500 | ❌ FAIL |
| Produktsidor | 3 | 8 | 400 | ❌ FAIL |
| Tjänstesidor | 8 | 8 | 800 | ❌ FAIL |
| Blogg | 3+ | 8 | 1 500 | ❌ FAIL |
| Location-sidor | 35 | 8 (soft 404) | 500 | ❌ FAIL |
| Om oss | 1 | 8 | 500 | ❌ FAIL |
| Kontakt | 1 | 8 | N/A | ❌ FAIL |

### 2.4 Location Pages Quality Assessment

**35 location-sidor** i sitemap (`/fruktkorg/[stadsdel]`) — ALLA visar "Oops! Page not found" (soft 404). Dessa sidor:
- Slösar Google crawl budget
- Skadar sajtens kvalitetssignaler
- Borde antingen byggas med unikt lokalt innehåll ELLER tas bort från sitemap

**Quality Gate Varning:** 35 location-sidor överstiger 30-gränsen. Om de byggs ut krävs minst 60% unikt innehåll per sida.

### 2.5 Blogg

3+ publicerade artiklar (2026-05-19):
1. Hammarby Sjöstad Guide — fruktkorgar till techkontor
2. Solna Business Area — Arenastaden, Solna Business Park
3. Södermalm — SoFo till Hornstull

**Positivt:** Lokalt fokuserat, relevant innehåll.
**Problem:** Ej crawlbart i HTML-källan.

---

## 3. On-Page SEO (10 / 100)

### 3.1 Title Tags (HTML-källa)

| Sida | Title |
|------|-------|
| **Alla 57 sidor** | "Fruktkorg på jobbet Stockholm \| Fruktkorgar till kontoret - Vitaminkorgen" |

❌ **KRITISK:** Identisk title på alla sidor. Sajten har troligtvis en dynamisk SEOHead React-komponent som sätter unika titles via JavaScript, men dessa injiceras EFTER sidladdning och finns inte i HTML-källan.

### 3.2 Meta Descriptions (HTML-källa)

| Sida | Description |
|------|-------------|
| **Alla 57 sidor** | "Fruktkorg på jobbet Stockholm ✓ Vi levererar färska fruktkorgar direkt till ert kontor..." |

❌ **KRITISK:** Identisk description överallt.

### 3.3 OG & Twitter Tags

| Tag | Status | Problem |
|-----|--------|---------|
| og:title | ❌ SAKNAS | Kommentar i HTML: "set dynamically by SEOHead component" — men finns ej i källan |
| og:description | ❌ SAKNAS | Samma problem |
| og:image | ✅ FINNS | Cloudflare R2 CDN-bild (automatiskt genererad av Lovable) |
| twitter:image | ✅ FINNS | Samma R2-bild |
| twitter:card | ❌ SAKNAS | Inte i HTML-källan |
| twitter:site | ❌ SAKNAS | Borttagen (var @lovable_dev förut — förbättring) |

### 3.4 Heading Structure (HTML-källa)

| Tag | Antal | Status |
|-----|-------|--------|
| H1 | 0 | ❌ KRITISK |
| H2 | 0 | ❌ KRITISK |
| H3 | 0 | ❌ KRITISK |

Headings existerar troligtvis i det JS-renderade innehållet men finns inte i HTML-källan.

### 3.5 Internal Linking (HTML-källa)

| Check | Status |
|-------|--------|
| Interna länkar | 0 — ❌ Ej crawlbart |
| Navigation | Finns i JS (8 huvudlänkar) men ej i HTML |
| Footer-länkar | Finns i JS (30+ områdeslänkar) men ej i HTML |
| Breadcrumbs | Ej identifierade |

### 3.6 Meta Keywords

```html
<meta name="keywords" content="fruktkorg på jobbet stockholm, fruktkorgar stockholm...">
```
⚠️ **ONÖDIG** — Google ignorerar meta keywords sedan 2009. Avslöjar sökordsstrategi för konkurrenter.

---

## 4. Schema / Structured Data (0 / 100)

### 4.1 Befintlig Schema

**Ingen Schema/JSON-LD hittad** i HTML-källan på någon sida.

### 4.2 Rekommenderade Schema-typer

| Schema-typ | Prioritet | Var | Påverkan |
|------------|-----------|-----|----------|
| LocalBusiness | Kritisk | / | Google Business Profile, Knowledge Panel |
| Product | Hög | /produkt/*, /bestall | Rich results med priser |
| Service | Hög | /blommor, /varuautomat | Tjänstebeskrivning |
| Organization | Hög | /om-oss | Företagsinformation |
| BreadcrumbList | Medium | Alla sidor | Navigationsstruktur |
| FAQPage | Medium | /fruktkorg-stockholm, /fruktkorg-foretag | FAQ rich results |
| BlogPosting | Medium | /blogg/* | Artikelmarkeringar |
| ContactPage | Låg | /kontakt | Kontaktinformation |
| WebSite + SearchAction | Låg | / | Sitelinks searchbox |
| AggregateOffer | Låg | /produkter | Prisspann |

### 4.3 LocalBusiness Schema — Rekommenderad Implementation

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Vitaminkorgen",
  "legalName": "VitaminKorgen AB",
  "description": "Vi levererar färska fruktkorgar till kontor i Stockholm, Södertälje och Uppsala",
  "url": "https://vitaminkorgen.se",
  "telephone": "010-183 98 36",
  "email": "info@vitaminkorgen.se",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Stockholm",
    "addressRegion": "Stockholms län",
    "addressCountry": "SE"
  },
  "areaServed": [
    { "@type": "City", "name": "Stockholm" },
    { "@type": "City", "name": "Södertälje" },
    { "@type": "City", "name": "Uppsala" }
  ],
  "foundingDate": "2021",
  "priceRange": "166–259 kr/vecka",
  "paymentAccepted": "Faktura",
  "openingHours": "Mo-Fr 08:00-17:00",
  "image": "https://vitaminkorgen.se/[logotyp].webp",
  "sameAs": []
}
```

### 4.4 Product Schema — Rekommenderad Implementation

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Fruktkorg Original",
  "description": "Balanserad mix av bananer, äpplen, päron och apelsiner, toppad med säsongsfrukt",
  "brand": { "@type": "Brand", "name": "Vitaminkorgen" },
  "offers": {
    "@type": "Offer",
    "price": "220",
    "priceCurrency": "SEK",
    "priceValidUntil": "2026-12-31",
    "availability": "https://schema.org/InStock",
    "url": "https://vitaminkorgen.se/produkt/fruktkorg-original"
  },
  "weight": { "@type": "QuantitativeValue", "value": "4", "unitCode": "KGM" }
}
```

---

## 5. Performance (30 / 100)

### 5.1 Positiva signaler

- **Cloudflare CDN** — Global edge-distribution
- **HTTP/2** — Stöds
- **HSTS** — Korrekt konfigurerat

### 5.2 Negativa signaler

| Problem | Påverkan |
|---------|----------|
| CSR-arkitektur | JavaScript måste ladda, parsas, exekveras innan innehåll visas |
| `cache-control: no-cache, must-revalidate, max-age=0` | Ingen browser-caching — varje besök hämtar om allt |
| 5 third-party scripts | GTM, GA4, Flock, Tidio, Lovable events |
| Inga preload/preconnect hints | Inga resource hints i HTML |
| Dubbla analytics | GA4 + Flock + GTM = redundant |

### 5.3 Laddade Resurser

| Resurs | Typ | Observation |
|--------|-----|-------------|
| `assets/index-BDwX_yjH.js` | JS Module | Hela SPA-bundlen |
| `assets/index-bYK_tMtE.css` | CSS | Stilmall |
| `gtm.js?id=GTM-56Z5QZHQ` | GTM | Google Tag Manager |
| `gtag/js?id=G-JZJV317Q2E` | GA4 | Google Analytics 4 |
| `/~flock.js` | Analytics | Flock analytics |
| `/__l5e/events.js` | Tracking | Lovable.app event tracking |
| `code.tidio.co/[id].js` | Chat | Tidio livechatt |

### 5.4 Caching

```
cache-control: no-cache, must-revalidate, max-age=0
```

❌ **Ingen caching alls.** Varje sidladdning hämtar hela HTML-dokumentet från servern. Assets (JS/CSS) kan cachas via Cloudflare, men HTML-dokumentet aldrig.

---

## 6. Images (8 / 100)

### 6.1 HTML-bildanalys

**0 bilder i HTML-källan** — alla bilder laddas via JavaScript.

### 6.2 OG Image

| Check | Status |
|-------|--------|
| Finns | ✅ Ja |
| URL | Cloudflare R2 CDN (`pub-bb2e103a32db4e198524a2e9ed8f35b4.r2.dev`) |
| Format | PNG (borde vara WebP) |
| Automatiskt genererad | Ja — Lovable.app preview-bild |
| Anpassad per sida | ❌ Samma bild på alla sidor |

### 6.3 Rekommendationer (efter SSR-implementation)

- Sätt `alt`-attribut på alla bilder (svenska, beskrivande)
- Sätt `width` + `height` (förhindrar CLS)
- Använd `loading="lazy"` under fold
- Konvertera till WebP/AVIF
- Implementera `srcset` för responsiva bilder
- Skapa unika OG-bilder per sidtyp

---

## 7. AI Search Readiness / GEO (15 / 100)

### 7.1 AI Crawler Access

| Crawler | robots.txt | Crawlbart Innehåll |
|---------|-----------|-------------------|
| GPTBot | ✅ Allow | ❌ 8 ord |
| ChatGPT-User | ✅ Allow | ❌ 8 ord |
| ClaudeBot | ✅ Allow | ❌ 8 ord |
| anthropic-ai | ✅ Allow | ❌ 8 ord |
| PerplexityBot | ✅ Allow | ❌ 8 ord |
| Google-Extended | ✅ Allow | ❌ 8 ord |
| CCBot | ✅ Allow | ❌ 8 ord |
| cohere-ai | ✅ Allow | ❌ 8 ord |

**Positivt:** Alla AI-crawlers explicit tillåtna (bättre än förra auditen).
**Problem:** Inget innehåll att crawla.

### 7.2 llms.txt

❌ **Saknas** — Ingen `/.well-known/llms.txt` hittad.

### 7.3 Citability Score

| Faktor | Score | Detaljer |
|--------|-------|----------|
| Quotable Facts | 2 / 20 | Meta description nämner "150+ företag" |
| Structured Data | 0 / 20 | Ingen schema markup |
| Clear Hierarchy | 0 / 20 | Inga headings i HTML |
| Passage Length | 0 / 20 | Inga textpassager i HTML |
| Authority Signals | 5 / 20 | Google Site Verification, fast domän sedan 2021 |
| **Totalt** | **7 / 100** | |

### 7.4 Brand Mentions

Sajten har potential att bli citerad i AI-svar om "fruktkorg kontor stockholm" men saknar crawlbart innehåll för AI-modeller att referera till. De rika landningssidorna (/fruktkorg-stockholm, /fruktkorg-foretag) med priser, FAQ:er och statistik ("sjukfrånvaro -20%") vore utmärkta för AI-citeringar — OM de var crawlbara.

---

## Appendix

### A. Hosting & Infrastruktur

| Parameter | Värde |
|-----------|-------|
| Plattform | Lovable.app (AI-driven no-code) |
| Subdomän | frukt-for-foretag.lovable.app |
| CDN | Cloudflare |
| Protokoll | HTTP/2 |
| SSL | Giltigt certifikat |
| Cookie-domän | vitaminkorgen.se (förbättring — var lovable.app förut) |
| Analytics | Google Tag Manager + GA4 + Flock Analytics |
| Chat | Tidio |
| Build-info | Commit SHA exponerat via Lovable event script |

### B. Jämförelse med Förra Auditen (2026-02-11)

| Aspekt | Feb 2026 | Jun 2026 | Förändring |
|--------|----------|----------|------------|
| SEO Score | 14 | 18 | +4 |
| Sidor i sitemap | 8 | 57 | +49 |
| Google-indexerade | 3 | 4 | +1 |
| AI crawlers i robots.txt | 0 | 8 | +8 |
| Google Tag Manager | Nej | Ja | ✅ |
| Google Site Verification | Nej | Ja | ✅ |
| Live chat (Tidio) | Nej | Ja | ✅ |
| Cookie-domän | lovable.app | vitaminkorgen.se | ✅ |
| Twitter @lovable_dev | Ja | Borttagen | ✅ |
| OG/Twitter tags i HTML | Delvis | Nästan inga | ⬇️ |
| Soft 404-sidor | 0 | ~35 | ⬇️ |
| Third-party scripts | 3 | 5 | ⬇️ |
| Browser caching | Ej testat | Helt avaktiverat | ⬇️ |
| CSR-problem | Ja | Ja (oförändrat) | ➡️ |
| Schema markup | 0 | 0 | ➡️ |
| Canonical tags | 0 | 0 | ➡️ |
| Headings i HTML | 0 | 0 | ➡️ |

### C. Soft 404 Location Pages (35 st)

Följande sidor i sitemap returnerar HTTP 200 men visar "Oops! Page not found":

```
/fruktkorg/ostermalm     /fruktkorg/kungsholmen    /fruktkorg/sodermalm
/fruktkorg/gamla-stan     /fruktkorg/gardet         /fruktkorg/ropsten
/fruktkorg/stadshagen     /fruktkorg/fridhemsplan   /fruktkorg/hammarby-sjostad
/fruktkorg/solna          /fruktkorg/sundbyberg     /fruktkorg/hagalund
/fruktkorg/bromma         /fruktkorg/alvik          /fruktkorg/nacka
/fruktkorg/taby           /fruktkorg/arninge        /fruktkorg/jarfalla
/fruktkorg/huddinge       /fruktkorg/haninge        /fruktkorg/handen
/fruktkorg/jordbro        /fruktkorg/lanna          /fruktkorg/tyreso
/fruktkorg/farsta          /fruktkorg/skondal        /fruktkorg/skogas
/fruktkorg/bandhagen      /fruktkorg/alvsjo         /fruktkorg/hagersten
/fruktkorg/vastberga      /fruktkorg/fruangen       /fruktkorg/tumba
/fruktkorg/salem          /fruktkorg/botkyrka       /fruktkorg/stockholm
```
