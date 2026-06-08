# SEO Action Plan — vitaminkorgen.se

**Genererad:** 2026-06-08
**Nuvarande SEO Health Score:** 18 / 100
**Uppskattat Score efter alla åtgärder:** 70–80 / 100

---

## Prioritet: KRITISK (Fixas omedelbart)

Dessa problem blockerar indexering och förhindrar all organisk synlighet.

### 1. Implementera Server-Side Rendering (SSR) eller Pre-rendering

**Problem:** Sajten är en React SPA med client-side rendering. HTML-källan innehåller `<div id="root"></div>` och 8 ord. Sökmotorer och AI-crawlers ser i princip en tom sida, trots att JS-renderat innehåll inkluderar produkter, priser, FAQ:er, blogg och 31+ stadsdelar.

**Åtgärd:**
- **Alternativ A (Bäst):** Migrera till Next.js eller Remix med SSR/SSG
- **Alternativ B:** Implementera pre-rendering via Prerender.io eller Rendertron som serverar statisk HTML till crawlers
- **Alternativ C:** Kontakta Lovable.app support för SSR-stöd
- **Alternativ D (Snabbast):** Använd Cloudflare Workers + HTMLRewriter för att injicera grundläggande SEO-element (title, description, canonical, schema) per URL

**Påverkan:** ALLA andra SEO-åtgärder är verkningslösa utan denna fix. Sajten har rika sidor med produkter (166–259 kr), FAQ:er och statistik ("sjukfrånvaro -20%") som Google inte kan se.

---

### 2. Fixa robots.txt Sitemap-referens

**Problem:** robots.txt pekar på `Sitemap: https://frukt-for-foretag.lovable.app/sitemap.xml` — fel domän.

**Åtgärd:** Ändra till `Sitemap: https://vitaminkorgen.se/sitemap.xml`

**Svårighet:** Låg. Kräver bara en textändring.

---

### 3. Ta bort Soft 404-sidor från Sitemap

**Problem:** 35 location-sidor (`/fruktkorg/[stadsdel]`) i sitemap returnerar HTTP 200 men visar "Oops! Page not found". Dessa:
- Slösar Googles crawl budget
- Signalerar låg kvalitet
- Kan leda till att hela sajten nedvärderas

**Åtgärd (välj en):**
- **A:** Ta bort alla 35 URL:er från sitemap.xml tills sidorna är byggda med riktigt innehåll
- **B:** Bygg ut sidorna med unikt lokalt innehåll (minst 500 ord, 60%+ unikt per sida)
- **C:** Sätt 410 Gone-status eller noindex om sidorna ska avvecklas

**⚠️ Quality Gate:** 35 sidor > 30-gränsen. Om ni bygger dem krävs minst 60% unikt innehåll per sida.

---

### 4. Unika Title Tags och Meta Descriptions per Sida

**Problem:** Alla 57 sidor returnerar identisk title och meta description i HTML-källan. Sajten har troligtvis en React SEOHead-komponent som sätter dessa dynamiskt, men de injiceras INTE i server-renderad HTML.

**Åtgärd:** Unika title + description måste finnas i HTML-källan (kräver SSR eller Cloudflare Workers):

| Sida | Föreslagen Title | Föreslagen Description |
|------|------------------|----------------------|
| / | Fruktkorg på jobbet Stockholm \| Vitaminkorgen | Vitaminkorgen levererar färska fruktkorgar till kontor i Stockholm. Gratis leverans, 150+ nöjda företag sedan 2021. Prova gratis! |
| /bestall | Beställ fruktkorg – 6 korgar från 166 kr \| Vitaminkorgen | Välj bland 6 fruktkorgar från 166 kr/vecka. Gratis leverans i Stockholm. 8% rabatt just nu. Beställ idag! |
| /produkter | Fruktkorgar & priser – Fruktkorg till kontoret \| Vitaminkorgen | Se vårt sortiment av fruktkorgar – från Bas (166 kr) till Sicilien (259 kr). Handplockad frukt, leverans varje vecka. |
| /provkorg | Gratis provkorg – Testa utan bindningstid \| Vitaminkorgen | Beställ en kostnadsfri provkorg till kontoret. Ingen bindningstid, inga dolda kostnader. Upplev kvaliteten själv! |
| /kontakt | Kontakta oss – Vitaminkorgen Stockholm | Kontakta Vitaminkorgen: 010-183 98 36 eller info@vitaminkorgen.se. Fruktkorgar till kontor i Stockholm. |
| /om-oss | Om Vitaminkorgen – Fruktleveranser sedan 2021 | Lär känna Vitaminkorgen – Stockholmsföretaget som levererat fruktkorgar till 150+ kontor sedan 2021. Hållbart och lokalt. |
| /blogg | Blogg – Tips om frukt & hälsa på jobbet \| Vitaminkorgen | Läs tips, recept och guider om frukt på jobbet. Öka välmåendet och produktiviteten på kontoret. |
| /blommor | Blommor till kontoret Stockholm \| Vitaminkorgen | Fräscha snittblommor och växter till kontoret. Automatiska byten, inget underhåll. Gratis leverans i Stockholm. |
| /varuautomat | Varuautomater för kontoret \| Vitaminkorgen | Moderna varuautomater med snacks, dryck och frukt. Kontaktlös betalning, Swish, kort. Installation & service ingår. |
| /fruktkorg-stockholm | Fruktkorg Stockholm – Leverans från 166 kr/v \| Vitaminkorgen | Fruktkorgar till kontor i Stockholm. Handplockad frukt, gratis leverans, 3 korgtyper. Prova gratis! |
| /fruktkorg-foretag | Fruktkorg för företag – Minska sjukfrånvaron \| Vitaminkorgen | Fruktkorgar som sänker sjukfrånvaron med 20%. Flexibla korgar för 5–500+ anställda. Faktura. |

---

### 5. Lägg till Canonical Tags

**Problem:** Inga canonical tags på någon sida.

**Åtgärd:** `<link rel="canonical" href="https://vitaminkorgen.se/[sida]">` på varje sida. Måste finnas i HTML-källan.

---

## Prioritet: HÖG (Fixas inom 1 vecka)

### 6. Implementera LocalBusiness + Product Schema (JSON-LD)

**Problem:** Noll schema markup. Sajten missar rich results för priser, produkter, FAQ, och lokalt företag.

**Åtgärd:** Injicera JSON-LD i HTML `<head>` (se FULL-AUDIT-REPORT.md för fullständig kod):
- **LocalBusiness** på startsidan (namn, telefon, email, leveransområde)
- **Product** på varje produktsida (namn, pris, tillgänglighet)
- **FAQPage** på /fruktkorg-stockholm och /fruktkorg-foretag

**Möjlighet med Cloudflare Workers:** Schema kan injiceras server-side via Cloudflare Workers utan att ändra React-appen.

---

### 7. Implementera Heading Structure (H1–H3)

**Problem:** Inga headings i HTML-källan.

**Åtgärd:** Varje sida måste ha minst 1 H1 och 2–5 H2 i HTML. Kräver SSR.

---

### 8. Bygg Ut eller Ta Bort Location-sidor

**Problem:** 35 location-sidor (soft 404:or) i sitemap.

**Åtgärd om ni bygger dem:**
- Minst 500 ord per sida
- 60%+ unikt innehåll (ej bara stad-namn utbytt)
- Lokala referenser (företagsområden, pendelmöjligheter)
- Unik H1: "Fruktkorg till kontor i [Stadsdel]"
- Produkter tillgängliga i området
- Leveransinformation specifik för stadsdelen
- LocalBusiness + Service schema per sida

**Bra exempel att bygga vidare på:** Bloggartiklarna om Hammarby Sjöstad, Solna och Södermalm har redan lokalt fokuserat innehåll — använd den modellen.

---

### 9. Fixa www vs non-www Inkonsistens

**Problem:** `www.vitaminkorgen.se/varuautomater-kaffemaskin` är indexerad av Google men vitaminkorgen.se (utan www) är huvuddomänen. En URL som inte finns i sitemap.

**Åtgärd:**
- Sätt 301-redirect från www → non-www (eller tvärtom, konsekvent)
- Omdirigera `/varuautomater-kaffemaskin` till `/varuautomat` om det är samma sida
- Verifiera i Google Search Console

---

### 10. Aktivera Browser Caching

**Problem:** `cache-control: no-cache, must-revalidate, max-age=0` — helt avaktiverad caching.

**Åtgärd:** Via Cloudflare Page Rules eller Cache Rules:
- HTML: `max-age=300, stale-while-revalidate=86400` (5 min cache, 1 dag stale)
- JS/CSS assets: `max-age=31536000, immutable` (1 år — filnamn har hash)
- Bilder: `max-age=604800` (1 vecka)

---

## Prioritet: MEDIUM (Fixas inom 1 månad)

### 11. Unika OG Tags per Sida

**Problem:** OG title + description saknas helt i HTML. OG image är samma auto-genererade Lovable.app preview på alla sidor.

**Åtgärd:**
- Injicera `og:title`, `og:description`, `og:url` per sida
- Skapa unika OG-bilder per sidtyp (åtminstone: startsida, produkter, blogg, kontakt)
- Byt bild till eget varumärke istället för Lovable-genererad preview

---

### 12. Lägg till lastmod i Sitemap

**Problem:** Inga lastmod-datum i sitemap.xml.

**Åtgärd:** Lägg till `<lastmod>` med korrekt datum per URL. Hjälper Google att prioritera crawling.

---

### 13. Minska Third-Party Scripts

**Problem:** 5 scripts: GTM, GA4, Flock, Tidio, Lovable events.

**Åtgärd:**
- Ta bort Flock Analytics (redundant med GA4/GTM)
- Undersök om Lovable events-scriptet kan tas bort (exponerar commit SHA)
- Ladda Tidio med `defer` och villkora på user interaction
- Flytta GA4 till GTM (konsolidering)

**Resultat:** 5 → 2 scripts (GTM + Tidio on-demand)

---

### 14. Skapa llms.txt

**Problem:** Saknas — AI-crawlers har ingen maskinläsbar sammanfattning av sajten.

**Åtgärd:** Skapa `/.well-known/llms.txt`:

```
# Vitaminkorgen
> Vitaminkorgen AB levererar färska fruktkorgar, blommor och varuautomater
> till kontor i Stockholm, Södertälje och Uppsala sedan 2021.

## Fruktkorgar
- Fruktkorg Bas: 180 kr/vecka (4 kg)
- Fruktkorg Original: 220 kr/vecka (4 kg)
- Fruktkorg Premium: 250 kr/vecka (4 kg)
- Fruktkorg Banan Plus: 230 kr/vecka (4 kg)
- Fruktkorg Supreme: 230 kr/vecka (4 kg)
- Fruktkorg Sicilien: 282 kr/vecka (4 kg)

## Övriga tjänster
- Blommor och växter till kontoret
- Varuautomater med snacks och dryck
- Gratis provkorg utan bindningstid

## Leveransområde
Gratis leverans i Stockholm (31+ stadsdelar), Södertälje och Uppsala.

## Kontakt
- Telefon: 010-183 98 36
- E-post: info@vitaminkorgen.se
- Webb: https://vitaminkorgen.se
- Offertförfrågan: https://vitaminkorgen.se/offertforfragan
```

---

### 15. Säkerhetsheaders

**Åtgärd (via Cloudflare):**
```
Content-Security-Policy: default-src 'self'; script-src 'self' https://www.googletagmanager.com https://code.tidio.co 'unsafe-inline'; img-src 'self' https://*.r2.dev https://storage.googleapis.com data:;
X-Frame-Options: SAMEORIGIN
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

---

### 16. Förbättra Intern Länkning (efter SSR)

**Åtgärd:**
- Navigering + footer-länkar måste renderas i HTML
- Breadcrumbs med BreadcrumbList-schema
- Blogg → produktsidor korslänkning
- Fruktkorgar ↔ Blommor ↔ Varuautomat korslänkning
- Location-sidor (om de byggs) → produktsidor

---

## Prioritet: LÅG (Backlog)

### 17. Ta bort meta keywords

**Problem:** Ignoreras av Google sedan 2009, avslöjar sökordsstrategi.

**Åtgärd:** Ta bort `<meta name="keywords">`.

---

### 18. Preconnect & Resource Hints

**Åtgärd:**
```html
<link rel="preconnect" href="https://www.googletagmanager.com">
<link rel="preconnect" href="https://code.tidio.co">
<link rel="dns-prefetch" href="https://www.googletagmanager.com">
```

---

### 19. Ta bort Lovable Information Leakage

**Problem:** Lovable events-script exponerar commit SHA och deployment tokens i HTML.

**Åtgärd:** Ta bort eller konfigureras bort i Lovable-inställningar.

---

### 20. Hreflang (om flerspråkig planeras)

Om sajten förblir enbart svensk behövs ingen hreflang. Om engelska planeras, implementera `<link rel="alternate" hreflang="sv" href="...">` etc.

---

## Prioriterad Tidslinje

### Vecka 1 (Omedelbart)
- [ ] Fixa robots.txt sitemap-referens (#2)
- [ ] Ta bort soft 404-sidor från sitemap (#3)
- [ ] Ta bort meta keywords (#17)

### Vecka 2–4 (SSR/Pre-rendering)
- [ ] Implementera SSR eller Cloudflare Workers-lösning (#1)
- [ ] Unika title/description per sida (#4)
- [ ] Canonical tags (#5)
- [ ] Heading structure (#7)
- [ ] Fixa www-inkonsistens (#9)

### Månad 2 (Schema & Optimering)
- [ ] LocalBusiness + Product schema (#6)
- [ ] Bygg ut eller ta bort location-sidor (#8)
- [ ] Aktivera browser caching (#10)
- [ ] Unika OG tags (#11)
- [ ] Lastmod i sitemap (#12)

### Månad 3 (Finjustering)
- [ ] Minska scripts (#13)
- [ ] Skapa llms.txt (#14)
- [ ] Säkerhetsheaders (#15)
- [ ] Intern länkning (#16)
- [ ] Preconnect hints (#18)

---

## Sammanfattning

| Prioritet | Antal | Huvudfokus |
|-----------|-------|------------|
| Kritisk | 5 | SSR, sitemap-fix, soft 404:or, unika meta-taggar, canonicals |
| Hög | 5 | Schema, headings, location-sidor, www-redirect, caching |
| Medium | 6 | OG tags, lastmod, scripts, llms.txt, säkerhet, intern länkning |
| Låg | 4 | Meta keywords, preconnect, info leakage, hreflang |

**Enskilt viktigaste åtgärden:** Implementera SSR eller pre-rendering. Sajten har redan rikt innehåll (produkter med priser, FAQ:er, bloggartiklar, 31+ leveransområden) — men allt är osynligt för sökmotorer och AI-crawlers. Med SSR stiger SEO-scoren troligtvis från 18 till 55+ direkt.
