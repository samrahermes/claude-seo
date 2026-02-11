# SEO Action Plan — vitaminkorgen.se

**Genererad:** 2026-02-11
**Nuvarande SEO Health Score:** 14 / 100
**Uppskattat Score efter åtgärder:** 65–75 / 100

---

## Prioritet: KRITISK (Fixas omedelbart)

Dessa problem blockerar indexering och förhindrar all SEO-prestanda.

### 1. Implementera Server-Side Rendering (SSR) eller Pre-rendering

**Problem:** Sajten är en ren React SPA med client-side rendering. Sökmotorer ser en tom `<div id="root"></div>` med bara 8 ord.

**Åtgärd:**
- **Alternativ A (Rekommenderat):** Migrera till Next.js med SSR/SSG. Detta ger server-renderad HTML för sökmotorer och snabb interaktivitet för användare.
- **Alternativ B:** Implementera pre-rendering via tjänster som Prerender.io eller Rendertron som serverar statisk HTML till crawlers.
- **Alternativ C:** Kontakta Lovable.app support för att aktivera SSR om plattformen stödjer det.

**Påverkan:** Alla andra SEO-åtgärder är i princip verkningslösa utan denna fix. Detta är den #1 viktigaste åtgärden.

**Påverkade sidor:** Alla 8 sidor.

---

### 2. Unika Title Tags per Sida

**Problem:** Alla 8 sidor har identisk title: "Fruktkorg på jobbet Stockholm | Fruktkorgar till kontoret - Vitaminkorgen"

**Åtgärd:** Skapa unika, beskrivande titles per sida:

| Sida | Föreslagen Title |
|------|------------------|
| / | Fruktkorg på jobbet Stockholm \| Vitaminkorgen |
| /produkter | Fruktkorgar & priser – Beställ fruktkorg till kontoret \| Vitaminkorgen |
| /blogg | Blogg – Tips om frukt & hälsa på jobbet \| Vitaminkorgen |
| /om-oss | Om Vitaminkorgen – Fruktleveranser sedan 2021 |
| /kontakt | Kontakta oss – Vitaminkorgen Stockholm |
| /offertforfragan | Begär offert – Fruktkorg till företaget \| Vitaminkorgen |
| /blommor | Blommor till kontoret Stockholm \| Vitaminkorgen |
| /varuautomat | Varuautomater & kaffemaskin – Kontorslösningar \| Vitaminkorgen |

**Riktlinjer:** 50–60 tecken, huvudsökord först, varumärke sist.

---

### 3. Unika Meta Descriptions per Sida

**Problem:** Alla sidor delar samma meta description.

**Åtgärd:** Skriv unika, handlingsorienterade descriptions per sida (120–155 tecken):

| Sida | Föreslagen Description |
|------|----------------------|
| / | Vitaminkorgen levererar färska fruktkorgar till kontor i Stockholm. Gratis leverans, flexibla abonnemang. 150+ nöjda företag sedan 2021. |
| /produkter | Se våra fruktkorgar – från lilla kontoret till storföretag. Handplockad frukt, leverans varje vecka i Stockholm. Beställ idag. |
| /blogg | Läs våra artiklar om frukt på jobbet, hälsa & välmående. Tips för att öka produktiviteten med rätt kost på kontoret. |
| /om-oss | Lär känna Vitaminkorgen – Stockholmsföretaget som levererat färska fruktkorgar till 150+ kontor sedan 2021. |
| /kontakt | Kontakta Vitaminkorgen för fruktkorgar till ert kontor i Stockholm. Ring, maila eller fyll i formuläret. |
| /offertforfragan | Begär en kostnadsfri offert på fruktkorgar till ert företag. Skräddarsydda lösningar för kontor i Stockholm. |
| /blommor | Fräscha snittblommor till kontoret i Stockholm. Veckoleverans av blommor som lyfter arbetsmiljön. |
| /varuautomat | Varuautomater och kaffemaskin för kontoret. Komplett servicelösning med frukt, snacks och dryck i Stockholm. |

---

### 4. Lägg till Canonical Tags

**Problem:** Inga canonical tags på någon sida — risk för duplicerat innehåll.

**Åtgärd:** Lägg till `<link rel="canonical" href="https://vitaminkorgen.se/[sida]">` på varje sida med sin egen URL.

---

### 5. Implementera Heading Structure (H1–H3)

**Problem:** Inga headings i HTML-källan.

**Åtgärd:** Varje sida behöver minst:
- **1 st H1** (sidans huvudrubrik, unik per sida)
- **2–5 st H2** (underrubriker för sektioner)
- **H3** vid behov (detaljer under H2)

**Exempel för startsidan:**
```html
<h1>Fruktkorg på jobbet i Stockholm</h1>
<h2>Varför välja Vitaminkorgen?</h2>
<h2>Våra populäraste fruktkorgar</h2>
<h2>Så fungerar det</h2>
<h2>Vad våra kunder säger</h2>
<h2>Vanliga frågor</h2>
```

---

## Prioritet: HÖG (Fixas inom 1 vecka)

### 6. Implementera LocalBusiness Schema (JSON-LD)

**Problem:** Ingen schema markup alls.

**Åtgärd:** Lägg till LocalBusiness-schema på startsidan:

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Vitaminkorgen",
  "description": "Vi levererar färska fruktkorgar till kontor i Stockholm",
  "url": "https://vitaminkorgen.se",
  "telephone": "[TELEFONNUMMER]",
  "email": "[E-POST]",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Stockholm",
    "addressRegion": "Stockholms län",
    "addressCountry": "SE"
  },
  "areaServed": {
    "@type": "City",
    "name": "Stockholm"
  },
  "foundingDate": "2021",
  "priceRange": "$$",
  "image": "https://vitaminkorgen.se/[optimerad-bild].webp",
  "sameAs": []
}
```

Lägg även till Service-schema på /produkter, /blommor och /varuautomat.

---

### 7. Fixa Sitemap-inkonsistenser

**Problem:**
- /varuautomater-kaffemaskin indexerad av Google men saknas i sitemap.
- /varuautomat finns i sitemap men verkar vara en annan URL.

**Åtgärd:**
- Verifiera vilken URL som är korrekt.
- Uppdatera sitemap.xml att inkludera alla giltiga URL:er.
- Sätt upp redirect (301) om en URL-variant ska avvecklas.

---

### 8. Fixa OG Image URL

**Problem:** OG-bildens URL innehåller mellanslag: `...VitaminKorgen 2.jpg`

**Åtgärd:**
- Byt namn på bildfilen (ta bort mellanslag): `vitaminkorgen-social.jpg`
- Konvertera till WebP-format för bättre prestanda.
- Optimera till rekommenderad storlek: 1200×630 px.
- Uppdatera alla OG- och Twitter-taggar med ny URL.

---

### 9. Fixa Twitter Card

**Problem:** Twitter site pekar på `@lovable_dev` istället för företagets eget konto.

**Åtgärd:**
- Skapa ett Twitter/X-konto för Vitaminkorgen.
- Uppdatera `twitter:site` till `@vitaminkorgen` (eller företagets konto).
- Alternativt: ta bort `twitter:site` om inget eget konto finns.

---

### 10. Unika OG Tags per Sida

**Problem:** Samma OG title, description och bild på alla sidor.

**Åtgärd:** Sätt sidspecifika OG-taggar som matchar sidans unika title och description. Skapa unika delbilder för nyckelsidor (startsida, produkter, blogg).

---

## Prioritet: MEDIUM (Fixas inom 1 månad)

### 11. Lägg till Content Security Policy (CSP) Header

**Problem:** Saknas — ökar risken för XSS-attacker.

**Åtgärd:** Konfigurera CSP-header via Cloudflare eller hosting:
```
Content-Security-Policy: default-src 'self'; script-src 'self' https://www.googletagmanager.com; img-src 'self' https://storage.googleapis.com; style-src 'self' 'unsafe-inline';
```

---

### 12. Lägg till X-Frame-Options Header

**Åtgärd:** `X-Frame-Options: DENY` eller `SAMEORIGIN`

---

### 13. Lägg till Permissions-Policy Header

**Åtgärd:**
```
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

---

### 14. Optimera Bilder

**Åtgärd (efter SSR-implementation):**
- Lägg till `alt`-attribut på alla bilder (beskrivande, på svenska).
- Sätt `width` och `height` på alla `<img>`-element (förhindrar CLS).
- Använd `loading="lazy"` på bilder under fold.
- Konvertera till WebP/AVIF-format.
- Implementera responsive images med `srcset`.

---

### 15. Förbättra Intern Länkning

**Åtgärd (efter SSR-implementation):**
- Se till att navigationen renderas i HTML (ej bara via JS).
- Lägg till breadcrumbs med BreadcrumbList-schema.
- Länka från bloggartiklar till produktsidor.
- Länka relaterade tjänster sinsemellan (fruktkorgar ↔ blommor ↔ varuautomat).

---

### 16. Skapa llms.txt

**Åtgärd:** Skapa `/.well-known/llms.txt` med företagsinfo:
```
# Vitaminkorgen
> Vitaminkorgen levererar färska fruktkorgar och blommor till kontor i Stockholm sedan 2021.

## Tjänster
- Fruktkorgar till kontoret
- Snittblommor till kontoret
- Varuautomater och kaffemaskin

## Kontakt
- Webb: https://vitaminkorgen.se
- Offertförfrågan: https://vitaminkorgen.se/offertforfragan
```

---

## Prioritet: LÅG (Backlog)

### 17. Ta bort meta keywords

**Problem:** `<meta name="keywords">` ignoreras av Google sedan 2009.

**Åtgärd:** Ta bort taggen — den gör ingen nytta och kan avslöja sökordsstrategi för konkurrenter.

---

### 18. Överväg Hreflang (om flerspråkig)

**Åtgärd:** Om sajten enbart är på svenska behövs ingen hreflang. Om fler språk planeras, implementera hreflang-taggar.

---

### 19. Konsolidera Analytics

**Problem:** Två analytics-script (GA4 + Flock) kan påverka prestanda.

**Åtgärd:** Utvärdera om båda behövs. Överväg att konsolidera till ett.

---

### 20. Preconnect & Resource Hints

**Åtgärd:** Lägg till i `<head>`:
```html
<link rel="preconnect" href="https://www.googletagmanager.com">
<link rel="preconnect" href="https://storage.googleapis.com">
<link rel="dns-prefetch" href="https://www.googletagmanager.com">
```

---

## Sammanfattning

| Prioritet | Antal åtgärder | Huvudfokus |
|-----------|---------------|------------|
| Kritisk | 5 | SSR, unika meta-taggar, canonicals, headings |
| Hög | 5 | Schema, sitemap, OG-bilder, Twitter card |
| Medium | 6 | Security headers, bildoptimering, intern länkning, llms.txt |
| Låg | 4 | Meta keywords, hreflang, analytics, resource hints |

**Det absolut viktigaste:** Implementera SSR/SSG. Utan det är sajten i princip osynlig för sökmotorer trots att all content finns — den renderas bara inte i HTML-källan.
