# SEO Audit Report — primeseo.se

**Audit Date:** 2026-06-08
**Tool:** Claude SEO v1.1.0
**Business Type Detected:** Agency (SEO-byrå — Stockholm, Hägersten)
**Pages i Sitemap:** 7 (exklusive startsidan)
**Faktiska Sidor:** ~16+ (tjänster, guider, legal, onboarding)
**Pages Indexerade (Google):** 1

---

## Executive Summary

### SEO Health Score: 39 / 100

| Kategori | Score | Vikt | Viktat |
|----------|-------|------|--------|
| Technical SEO | 45 / 100 | 25% | 11.3 |
| Content Quality | 40 / 100 | 25% | 10.0 |
| On-Page SEO | 25 / 100 | 20% | 5.0 |
| Schema / Structured Data | 70 / 100 | 10% | 7.0 |
| Performance (CWV) | 50 / 100 | 10% | 5.0 |
| Images | 15 / 100 | 5% | 0.8 |
| AI Search Readiness | 20 / 100 | 5% | 1.0 |

**Sammanfattning:** PrimeSEO har gjort ett imponerande jobb med SEO-workarounds för en Lovable.app-baserad React SPA. Sajten har 4 schema-block (LocalBusiness, Organization, WebSite, FAQPage), statiska crawlbara nav/footer-länkar utanför React, H1-injection per sida, canonical tag, och hreflang. Men tre kritiska problem kvarstår: (1) alla undersidor returnerar startsidans title, description, canonical och schema, (2) sitemapen täcker bara 7 av 16+ sidor, och (3) bara 1 sida är indexerad av Google.

### Topp 5 Kritiska Problem

1. **Alla sidor delar startsidans meta-taggar** — Samma title, description, canonical (`/`) och schema på alla undersidor
2. **Canonical tag pekar på `/` överallt** — Alla sidor signalerar till Google att de är startsidan
3. **Sitemapen saknar majoriteten av sidorna** — 7 URL:er vs 16+ faktiska sidor
4. **Bara 1 av 16+ sidor indexerad** — Extremt låg indexeringsgrad
5. **Ingen unik content i HTML-källan** — 163 ord (från dolda element) identiskt på alla sidor

### Topp 5 Positiva Observationer

1. 4 välstrukturerade JSON-LD schema-block (LocalBusiness, Organization, WebSite, FAQPage)
2. Statisk crawlbar navigation och footer med 57 interna länkar
3. H1-injection med per-sida mapping (fungerar med JS-rendering)
4. Preconnect, preload och delayed analytics för bättre prestanda
5. Hreflang-taggar (sv + x-default)

---

## 1. Technical SEO (45 / 100)

### 1.1 Crawlability

| Check | Status | Detaljer |
|-------|--------|----------|
| robots.txt | ✅ PASS | Tillåter alla, /admin/ blockad, dual sitemap (primeseo.se + Supabase) |
| Sitemap.xml | ⚠️ VARNING | Bara 7 URL:er — saknar /tjanster/*, /guider/*, /onboarding |
| Static Crawlable Links | ✅ BRA | 57 interna länkar utanför React (nav + footer + contextual) |
| SSR/CSR | ⚠️ Hybrid | CSR med statiska SEO-element utanför React — kreativ lösning |
| Google Site Verification | ❌ SAKNAS | Ingen verifieringstagg hittad |

### 1.2 robots.txt

```
User-agent: *
Allow: /
Disallow: /admin/
Sitemap: https://primeseo.se/sitemap.xml
Sitemap: https://kpduigpzkrhadetinpcb.supabase.co/functions/v1/sitemap
```

**Noterbart:** Dual sitemap med Supabase Edge Function som backup — bra redundans. Men exponerar Supabase-instans.

### 1.3 Sitemap Analys

**Sidor i sitemap (7):**
- / (1.0), /kontakt (0.8), /om-oss (0.8), /integritetspolicy (0.3), /privacy-policy (0.3), /villkor (0.3), /terms-of-service (0.3)

**Sidor som SAKNAS i sitemap (9+):**
- /tjanster
- /tjanster/lokal-seo
- /tjanster/on-page-seo
- /tjanster/off-page-seo
- /guider
- /guider/vad-ar-seo
- /guider/lokal-seo-for-smaforetag
- /guider/lokal-seo-hagersten-globen-guide
- /onboarding

**lastmod:** 2025-09-10 på alla (9 månader gammalt)

### 1.4 Indexability

| Check | Status | Detaljer |
|-------|--------|----------|
| Canonical tag | ❌ KRITISK | Finns men pekar på `https://primeseo.se/` på ALLA sidor — alla undersidor canonicaliseras till startsidan |
| meta robots | ✅ PASS | `index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1` |
| Google-indexering | ❌ KRITISK | Bara 1 sida indexerad (startsidan) |
| Hreflang | ✅ BRA | `sv` + `x-default` — men pekar bara till `/` på alla sidor |
| Title tags | ❌ KRITISK | Identisk title på alla sidor i HTML-källan |
| Meta descriptions | ❌ KRITISK | Identisk description på alla sidor |

**Orsak till låg indexering:** Alla sidor har `<link rel="canonical" href="https://primeseo.se/">` — Google tolkar detta som att alla sidor vill vara startsidan och ignorerar undersidorna.

### 1.5 Security Headers

| Header | Status | Värde |
|--------|--------|-------|
| HTTPS | ✅ PASS | Aktiv |
| HSTS | ✅ PASS | `max-age=31536000; includeSubDomains` |
| Referrer-Policy | ✅ PASS | `strict-origin-when-cross-origin` |
| X-Content-Type-Options | ✅ PASS | `nosniff` (server + meta) |
| Content-Security-Policy | ❌ SAKNAS | |
| X-Frame-Options | ❌ SAKNAS | |
| Permissions-Policy | ❌ SAKNAS | |
| Cache-Control | ⚠️ VARNING | `no-cache, must-revalidate, max-age=0` |

### 1.6 JavaScript Rendering & Static SEO

**Kreativ hybrid-approach:**

| Element | Implementation | Status |
|---------|---------------|--------|
| Navigation (9 länkar) | Static HTML, sr-only utanför React | ✅ Crawlbar |
| Footer (13 länkar) | Static HTML, sr-only utanför React | ✅ Crawlbar |
| Contextual links (~35 st) | Static HTML, per-sida kontext, sr-only | ✅ Crawlbar |
| H1 per sida | JS injection med URL-map + hardcoded fallback | ⚠️ Delvis — fallback är startsidans H1 |
| Title / Description / Canonical | Hardcoded i `<head>` (ej dynamiska) | ❌ Samma på alla sidor |
| Schema JSON-LD | Hardcoded i `<head>` | ⚠️ Startsidans schema på alla sidor |
| OG / Twitter tags | Hardcoded i `<head>` | ⚠️ Startsidans OG-data på alla sidor |

**Risknivå för dold text:** De statiska elementen använder CSS `clip:rect(0,0,0,0)` och `position:absolute; width:1px; height:1px` — Google accepterar generellt sr-only/screen-reader-mönster, men det finns risk att det betraktas som cloaking om innehållet inte matchar det JS-renderade.

### 1.7 Code Splitting & JS Architecture

| Resurs | Typ |
|--------|-----|
| `index-D1kgqqqc.js` | Main app bundle (module) |
| `vendor-react-CQ1qzVd1.js` | React framework (modulepreload) |
| `vendor-ui-DGQuO8Gu.js` | UI component library (modulepreload) |
| `vendor-query-BjjBBhlm.js` | React Query/data fetching (modulepreload) |
| `vendor-charts-wIbTeRgY.js` | Charts library (modulepreload) |
| `index-Doo21qNH.css` | Stylesheet |

**Positivt:** Bra code splitting med modulepreload — bättre än en monolitisk bundle.

### 1.8 Core Web Vitals (Uppskattning)

| Metric | Uppskattning | Tröskel | Status |
|--------|-------------|---------|--------|
| LCP | 2.5–4s (troligt) | <2.5s | ⚠️ Gränsfall |
| INP | Bra (troligt) | <200ms | ✅ Troligt PASS |
| CLS | Låg (troligt) | <0.1 | ✅ Troligt PASS |

**Positivt:** Font preload med `display:swap`, delayed analytics (2s), preconnect, modulär JS-laddning. Risken för dålig LCP kvarstår dock pga CSR.

---

## 2. Content Quality (40 / 100)

### 2.1 E-E-A-T Assessment

| Signal | Score | Detaljer |
|--------|-------|----------|
| Experience | 40 / 100 | Case: "+340% organisk trafik", "127 recensioner", konkreta KPI:er (JS-renderat) |
| Expertise | 45 / 100 | 3+ SEO-guider, specifik Lokal SEO-expertis, branschterminologi |
| Authoritativeness | 30 / 100 | sameAs: Facebook, Instagram, LinkedIn. Inga synliga branschcertifieringar |
| Trustworthiness | 55 / 100 | Full adress, telefon, email, öppettider, org.nr (559386-0181), "Nord Styling AB" |
| **Totalt E-E-A-T** | **43 / 100** | |

### 2.2 Crawlbar vs JS-renderat Innehåll

| Aspekt | HTML-källa (163 ord) | JS-renderat |
|--------|---------------------|-------------|
| Navigeringslänkar | ✅ 9 st | ✅ Fler |
| Footer med adress | ✅ Full adress + telefon | ✅ Utökad |
| Kontextuella länkar | ✅ ~35 st per-sida | ✅ Fler |
| H1 per sida | ⚠️ Bara startsidans (hardcoded) | ✅ Per-sida via JS |
| Tjänstebeskrivningar | ❌ | ✅ 3 tjänster |
| Priser | ❌ | ✅ "1500–5000 SEK/månad", 3 paket |
| FAQ | ❌ (men i schema) | ✅ Fler frågor |
| Guider/Artiklar | ❌ | ✅ 5+ artiklar |
| Kundstatistik | ❌ | ✅ +340%, 4.9/5, 127 reviews |
| Kontaktformulär | ❌ | ✅ Namn, företag, email, meddelande |

### 2.3 JS-renderat Innehåll per Sida

| Sida | Huvudinnehåll (JS) | Uppskattat Ord |
|------|--------------------|----|
| / | Hero, statistik, tjänster, FAQ, CTA | ~800+ |
| /tjanster | 3 tjänstekategorier, beskrivningar | ~500+ |
| /tjanster/lokal-seo | Lokal SEO-guide, 3 paket (Silver/Gold/Diamond), statistik (46%, 88%) | ~1000+ |
| /tjanster/on-page-seo | On-page optimeringsguide | ~600+ |
| /tjanster/off-page-seo | Länkbyggnadsstrategi | ~600+ |
| /guider | Artikellistning, 5+ guider med kategorier | ~400+ |
| /guider/vad-ar-seo | SEO-grundkurs | ~800+ |
| /guider/lokal-seo-for-smaforetag | Komplett lokal SEO-guide | ~1000+ |
| /guider/lokal-seo-hagersten-globen-guide | Lokal guide | ~800+ |
| /om-oss | Företagsinfo, värderingar (4 st), målmarknad | ~600+ |
| /kontakt | Kontaktformulär, karta, adress, öppettider | ~300+ |
| /onboarding | Onboarding-process | ~400+ |

**Problem:** Allt detta rika innehåll existerar bara i JS — crawlers ser 163 ord (dolda element) på varje sida.

### 2.4 Blogg/Guider

5+ guider med relevant SEO-expertis:
1. "Komplett guide till lokal SEO 2025"
2. "Så optimerar du din Google Business Profile"
3. "SEO-strategi för B2B-företag"
4. "Case: Hur vi ökade organisk trafik med 340%"
5. "Vad är SEO?" + lokala guider (Hägersten, Globen)

**Positivt:** Starkt kunskapsinnehåll som demonstrerar expertis.
**Problem:** Saknas helt i sitemapen. Inte crawlbart i HTML.

---

## 3. On-Page SEO (25 / 100)

### 3.1 Title Tags (HTML-källa)

| Sida | Title i HTML |
|------|-------------|
| **Alla sidor** | "PrimeSEO \| SEO-byrå i Stockholm - Lerkrogsvägen 21, Hägersten" |

❌ Identisk title. Title-längd: 60 tecken (bra längd men borde vara unik per sida).

React-appen sätter troligtvis per-sida titles via document.title, men dessa syns inte i den server-renderade HTML-källan.

### 3.2 Meta Descriptions (HTML-källa)

| Sida | Description i HTML |
|------|-------------------|
| **Alla sidor** | "PrimeSEO är en SEO-byrå i Hägersten, Stockholm. Vi hjälper svenska företag ranka högre på Google..." |

❌ Identisk. 137 tecken (bra längd men borde vara unik per sida).

### 3.3 OG & Twitter Tags

| Tag | Status | Värde |
|-----|--------|-------|
| og:type | ✅ | website |
| og:url | ⚠️ | `https://primeseo.se/` (samma för alla sidor) |
| og:title | ✅ | Eget värde (skiljer sig från page title — bra) |
| og:description | ✅ | Unik och handlingsorienterad |
| og:image | ✅ | Eget varumärke med 1200×630 dimensioner |
| og:site_name | ✅ | "PrimeSEO" |
| og:locale | ✅ | sv_SE |
| twitter:card | ✅ | summary_large_image |
| twitter:image | ✅ | Samma som OG |

**Bra implementation** — men statisk för alla sidor (borde vara dynamisk per sida).

### 3.4 Heading Structure

**I HTML-källan:**
- H1: 1 st — "SEO-byrå i Stockholm – PrimeSEO" (samma på alla sidor via hardcoded fallback)
- H2: 0
- H3: 0

**JS H1-mapping (per sida, via injection script):**
| Sida | H1 (JS) |
|------|---------|
| / | SEO-byrå i Stockholm – PrimeSEO |
| /tjanster | Våra SEO-tjänster |
| /tjanster/on-page-seo | On-page SEO – optimera din webbplats |
| /tjanster/off-page-seo | Off-page SEO – bygg auktoritet |
| /tjanster/lokal-seo | Lokal SEO för småföretag i Stockholm |
| /guider | SEO-guider för svenska företag |
| /guider/vad-ar-seo | Vad är SEO? |
| /om-oss | Om oss – Teamet bakom PrimeSEO |
| /kontakt | Kontakta PrimeSEO |
| /onboarding | Kom igång med PrimeSEO |

**Problem:** H1-scriptet körs client-side och fallback-H1 i HTML är startsidans. Crawlers utan JS-rendering ser alltid "SEO-byrå i Stockholm – PrimeSEO".

### 3.5 Internal Linking

| Typ | Antal | Status |
|-----|-------|--------|
| Statisk navigation | 9 länkar | ✅ Crawlbar |
| Statisk footer | 13 länkar | ✅ Crawlbar |
| Contextual (per-sida) | ~35 länkar | ✅ Crawlbar |
| **Totalt i HTML** | **57 unika** | ✅ Bra intern länkning |

**Positivt:** Rik intern länkning med kontextuell anchor text. Bra SEO-praktik.
**Problem:** Alla 57 länkar finns på ALLA sidor (inte filtrerade per sida-kontext).

### 3.6 Övriga meta-taggar

| Tag | Värde | Status |
|-----|-------|--------|
| meta keywords | "SEO Sverige, sökmotoroptimering..." | ⚠️ Onödig (ignoreras av Google) |
| meta author | "PrimeSEO" | ✅ OK |
| meta language | "Swedish" | ⚠️ Icke-standard — använd `lang="sv"` på `<html>` |
| geo.region | "SE" | ✅ OK |
| geo.placename | "Sverige" | ✅ OK |
| format-detection | "telephone=no" | ✅ OK |

---

## 4. Schema / Structured Data (70 / 100)

### 4.1 Schema-block (4 st)

| # | @type | Kvalitet | Problem |
|---|-------|----------|---------|
| 1 | LocalBusiness + ProfessionalService | ✅ Utmärkt | Komplett: namn, adress, geo, telefon, email, öppettider, priceRange, sameAs, areaServed |
| 2 | Organization | ✅ Bra | ContactPoint, adress, sameAs, service-beskrivning |
| 3 | WebSite + SearchAction | ⚠️ Varning | SearchAction pekar på `?q={search_term_string}` — fungerar sökfunktionen verkligen? |
| 4 | FAQPage | ⚠️ Varning | 3 frågor — bra men statisk för alla sidor. Borde vara sidspecifik |

### 4.2 Schema-kvalitet

**Positivt:**
- `@id` på LocalBusiness (`#localbusiness`) — bra för entity linking
- Koordinater (latitude/longitude) — förstärker lokal SEO
- GeoCircle med 50 km radie — tydligt serviceområde
- sameAs till Facebook, Instagram, LinkedIn
- OpeningHoursSpecification korrekt formaterad
- PriceRange specifikt: "1500-5000 SEK/månad"

**Problem:**
- Samma schema-block på ALLA sidor — /tjanster borde ha Service-schema, /guider borde ha Article-schema
- FAQPage med 3 generella frågor på alla sidor — ska vara sidspecifika
- Organization-schema duplicerar delvis LocalBusiness (kan konsolideras)
- SearchAction URL otestbar (`?q=` parameter)
- LinkedIn-URL i LocalBusiness.sameAs men saknas i Organization.sameAs (inkonsekvent)

### 4.3 Saknade Schema-typer

| Schema-typ | Var | Prioritet |
|------------|-----|-----------|
| Service (per tjänst) | /tjanster/lokal-seo, /on-page-seo, /off-page-seo | Hög |
| Article/BlogPosting | /guider/* | Hög |
| BreadcrumbList | Alla sidor | Medium |
| Offer (prispaket) | /tjanster/lokal-seo (Silver/Gold/Diamond) | Medium |
| ContactPage | /kontakt | Låg |
| Review/AggregateRating | / (4.9/5, 127 reviews) | Hög |

---

## 5. Performance (50 / 100)

### 5.1 Positiva Signaler

| Feature | Status |
|---------|--------|
| Cloudflare CDN | ✅ |
| HTTP/2 | ✅ |
| HSTS | ✅ |
| Code splitting (5 chunks) | ✅ Utmärkt |
| `modulepreload` på vendor-chunks | ✅ Bra |
| Font preload med `display:swap` | ✅ Bra för CLS |
| Preconnect (fonts, Supabase) | ✅ |
| DNS prefetch (GTM, fonts) | ✅ |
| Delayed GA (2s efter load) | ✅ Bra prestanda |

### 5.2 Negativa Signaler

| Problem | Påverkan |
|---------|----------|
| `cache-control: no-cache, max-age=0` | Ingen browser-caching av HTML |
| CSR — content laddas via JS | LCP beroende av JS-parsing |
| Flock analytics + Lovable events | 2 extra scripts |
| Charts vendor-chunk laddas på alla sidor | Onödig om charts bara finns på en sida |

### 5.3 Third-Party Scripts

| Script | Laddning | Påverkan |
|--------|----------|----------|
| GA4 (G-2PCJN6WEG2 + GT-WPDC88WQ) | Delayed 2s | ✅ Minimal |
| Flock analytics | defer | ⚠️ Extra script |
| Lovable events | defer | ⚠️ Extra + exponerar commit SHA |
| Google Fonts | preload → stylesheet | ✅ Optimerad |

---

## 6. Images (15 / 100)

### 6.1 HTML-bilder

**0 bilder i HTML-källan** — alla bilder laddas via React.

### 6.2 OG/Schema-bilder

| Bild | URL | Status |
|------|-----|--------|
| OG image | /lovable-uploads/d2720de1-...png | ✅ Eget varumärke, 1200×630 |
| Logo (schema) | /lovable-uploads/dad2b176-...png | ✅ Finns i schema |
| Schema image | Samma som OG | ✅ |

**Problem:**
- PNG-format (borde vara WebP)
- Filnamn är UUID:er (borde vara beskrivande: `primeseo-logo.webp`)
- Samma OG-bild på alla sidor
- Inga alt-texter verifierbara i HTML

---

## 7. AI Search Readiness / GEO (20 / 100)

### 7.1 AI Crawler Access

| Crawler | robots.txt | Status |
|---------|-----------|--------|
| GPTBot | ✅ Tillåten (`*`) | Ser 163 ord + schema |
| ClaudeBot | ✅ Tillåten | Ser 163 ord + schema |
| PerplexityBot | ✅ Tillåten | Ser 163 ord + schema |
| Googlebot | ✅ Tillåten | Kan rendera JS → full content |

### 7.2 llms.txt

❌ **Saknas** — Varken `/.well-known/llms.txt` eller `/llms.txt`.

### 7.3 Citability Score

| Faktor | Score | Detaljer |
|--------|-------|----------|
| Quotable Facts | 5 / 20 | Schema har telefon, adress, priser — men begränsat |
| Structured Data | 14 / 20 | 4 schema-block med rik data |
| Clear Hierarchy | 3 / 20 | H1 finns men inga H2/H3 i HTML |
| Passage Length | 2 / 20 | 163 ord (dolda element) — inga riktiga textpassager |
| Authority Signals | 5 / 20 | sameAs, org.nr, adress, GeoCoordinates |
| **Totalt** | **29 / 100** | |

### 7.4 AI Search Potential

Sajten nämner specifikt "ChatGPT" i sitt OG-beskrivning ("ranka högre på Google, Google Maps och ChatGPT") — visar medvetenhet om AI-sök. Schema-datan (adress, priser, tjänster, FAQ) gör sajten delvis citiérbar av AI-modeller, men det faktiska innehållet (guider, case studies, detaljerade tjänstebeskrivningar) är bara tillgängligt via JS-rendering.

---

## Appendix

### A. Hosting & Infrastruktur

| Parameter | Värde |
|-----------|-------|
| Plattform | Lovable.app |
| Backend | Supabase (kpduigpzkrhadetinpcb.supabase.co) |
| CDN | Cloudflare |
| Protokoll | HTTP/2 |
| SSL | Giltigt |
| Cookie-domän | primeseo.se |
| Fonts | Google Fonts (Manrope, Inter) |
| Analytics | GA4 (G-2PCJN6WEG2 + GT-WPDC88WQ), delayd 2s |
| Juridisk enhet | Nord Styling AB (559386-0181) |
| Varumärkesfärg | #FF5A1F (orange) |
| PWA | manifest.json finns |

### B. Alla Identifierade Sidor

| URL | I Sitemap | HTTP | Google-indexerad |
|-----|-----------|------|-----------------|
| / | ✅ | 200 | ✅ |
| /tjanster | ❌ | 200 | ❌ |
| /tjanster/lokal-seo | ❌ | 200 | ❌ |
| /tjanster/on-page-seo | ❌ | 200 | ❌ |
| /tjanster/off-page-seo | ❌ | 200 | ❌ |
| /guider | ❌ | 200 | ❌ |
| /guider/vad-ar-seo | ❌ | 200 | ❌ |
| /guider/lokal-seo-for-smaforetag | ❌ | 200 | ❌ |
| /guider/lokal-seo-hagersten-globen-guide | ❌ | 200 | ❌ |
| /om-oss | ✅ | 200 | ❌ |
| /kontakt | ✅ | 200 | ❌ |
| /onboarding | ❌ | 200 | ❌ |
| /integritetspolicy | ✅ | 200 | ❌ |
| /privacy-policy | ✅ | 200 | ❌ |
| /villkor | ✅ | 200 | ❌ |
| /terms-of-service | ✅ | 200 | ❌ |

### C. Schema Validation Summary

| Schema | Valid | Problem |
|--------|-------|---------|
| LocalBusiness + ProfessionalService | ✅ | Inga strukturella fel. LinkedIn saknas i Organization.sameAs |
| Organization | ✅ | Duplicerar delvis LocalBusiness |
| WebSite + SearchAction | ⚠️ | Sökfunktionen via `?q=` otestbar |
| FAQPage | ⚠️ | Bara 3 frågor, statiskt på alla sidor, borde vara per-sida |
