# SEO Action Plan — primeseo.se

**Genererad:** 2026-06-08
**Nuvarande SEO Health Score:** 39 / 100
**Uppskattat Score efter alla åtgärder:** 75–85 / 100

---

## Prioritet: KRITISK (Fixas omedelbart)

### 1. Fixa Canonical Tags per Sida

**Problem:** ALLA sidor har `<link rel="canonical" href="https://primeseo.se/">` — varje undersida signalerar till Google att den ÄR startsidan. Detta är den troligaste orsaken till att bara 1 sida är indexerad.

**Åtgärd:** Varje sida måste ha sin egen canonical URL:

| Sida | Canonical |
|------|-----------|
| / | `https://primeseo.se/` |
| /tjanster | `https://primeseo.se/tjanster` |
| /tjanster/lokal-seo | `https://primeseo.se/tjanster/lokal-seo` |
| /tjanster/on-page-seo | `https://primeseo.se/tjanster/on-page-seo` |
| /tjanster/off-page-seo | `https://primeseo.se/tjanster/off-page-seo` |
| /guider | `https://primeseo.se/guider` |
| /guider/vad-ar-seo | `https://primeseo.se/guider/vad-ar-seo` |
| /kontakt | `https://primeseo.se/kontakt` |
| /om-oss | `https://primeseo.se/om-oss` |
| /onboarding | `https://primeseo.se/onboarding` |

**Implementation:** Samma approach som H1-scriptet — server-side injection eller Cloudflare Worker som matchar pathname → korrekt canonical.

**Påverkan:** Denna enda fix kan dramatiskt öka indexeringen från 1 → 16+ sidor.

---

### 2. Unika Title Tags per Sida

**Problem:** Alla sidor returnerar: "PrimeSEO | SEO-byrå i Stockholm - Lerkrogsvägen 21, Hägersten"

**Åtgärd:**

| Sida | Föreslagen Title |
|------|------------------|
| / | PrimeSEO \| SEO-byrå i Stockholm – Ranka högre på Google |
| /tjanster | SEO-tjänster Stockholm – Lokal, On-page & Off-page \| PrimeSEO |
| /tjanster/lokal-seo | Lokal SEO Stockholm – Syns på Google Maps \| PrimeSEO |
| /tjanster/on-page-seo | On-page SEO – Optimera din webbplats \| PrimeSEO |
| /tjanster/off-page-seo | Off-page SEO – Bygg auktoritet med backlinks \| PrimeSEO |
| /guider | SEO-guider för svenska företag \| PrimeSEO |
| /guider/vad-ar-seo | Vad är SEO? Komplett guide 2026 \| PrimeSEO |
| /guider/lokal-seo-for-smaforetag | Lokal SEO för småföretag – Steg-för-steg guide \| PrimeSEO |
| /om-oss | Om PrimeSEO – SEO-byrå i Hägersten, Stockholm |
| /kontakt | Kontakta PrimeSEO – Boka kostnadsfri SEO-analys |
| /onboarding | Kom igång med PrimeSEO – Så fungerar det |

---

### 3. Unika Meta Descriptions per Sida

**Problem:** Identisk description på alla sidor.

**Åtgärd:**

| Sida | Föreslagen Description |
|------|----------------------|
| / | PrimeSEO hjälper svenska företag ranka högre på Google & Maps. SEO-byrå i Hägersten, Stockholm. Boka kostnadsfri SEO-analys idag. |
| /tjanster | Professionella SEO-tjänster: Lokal SEO, On-page & Off-page. Paket från 1 500 kr/mån. Gratis analys och rådgivning. |
| /tjanster/lokal-seo | Lokal SEO för småföretag i Stockholm. 46% av Google-sökningar är lokala. Vi optimerar din Google Business Profile. Silver, Gold & Diamond-paket. |
| /tjanster/on-page-seo | On-page SEO: teknisk optimering, innehåll och intern länkning. Vi hjälper din webbplats ranka högre. Kostnadsfri analys. |
| /tjanster/off-page-seo | Off-page SEO: länkbyggnad, auktoritet och omnämnanden. Stärk din domäns position i Googles sökresultat. |
| /guider | Kostnadsfria SEO-guider för svenska företag. Lär dig lokal SEO, Google Business Profile-optimering och mer. |
| /kontakt | Kontakta PrimeSEO: 010-555 87 28 eller info@primeseo.se. Lerkrogsvägen 21, Hägersten. Kostnadsfri rådgivning utan förpliktelser. |
| /om-oss | Möt teamet bakom PrimeSEO. Vi brinner för kvalitet, transparens och resultat. SEO-byrå i Hägersten sedan 2025. |

---

### 4. Uppdatera Sitemap med Alla Sidor

**Problem:** Sitemapen har bara 7 URL:er — saknar alla tjänste-, guide- och onboarding-sidor.

**Åtgärd:** Lägg till alla aktiva sidor:

```xml
<!-- Tjänster -->
<url><loc>https://primeseo.se/tjanster</loc><priority>0.9</priority><changefreq>monthly</changefreq></url>
<url><loc>https://primeseo.se/tjanster/lokal-seo</loc><priority>0.9</priority><changefreq>monthly</changefreq></url>
<url><loc>https://primeseo.se/tjanster/on-page-seo</loc><priority>0.8</priority><changefreq>monthly</changefreq></url>
<url><loc>https://primeseo.se/tjanster/off-page-seo</loc><priority>0.8</priority><changefreq>monthly</changefreq></url>

<!-- Guider -->
<url><loc>https://primeseo.se/guider</loc><priority>0.8</priority><changefreq>weekly</changefreq></url>
<url><loc>https://primeseo.se/guider/vad-ar-seo</loc><priority>0.8</priority><changefreq>monthly</changefreq></url>
<url><loc>https://primeseo.se/guider/lokal-seo-for-smaforetag</loc><priority>0.8</priority><changefreq>monthly</changefreq></url>
<url><loc>https://primeseo.se/guider/lokal-seo-hagersten-globen-guide</loc><priority>0.7</priority><changefreq>monthly</changefreq></url>

<!-- Onboarding -->
<url><loc>https://primeseo.se/onboarding</loc><priority>0.7</priority><changefreq>monthly</changefreq></url>
```

**Uppdatera också:** lastmod-datum från 2025-09-10 → aktuellt datum.

---

### 5. Unika Hreflang-taggar per Sida

**Problem:** Hreflang pekar på `https://primeseo.se/` på alla sidor.

**Åtgärd:** Varje sida ska ha hreflang som pekar på sin egen URL:
```html
<!-- På /tjanster -->
<link rel="alternate" hreflang="sv" href="https://primeseo.se/tjanster" />
<link rel="alternate" hreflang="x-default" href="https://primeseo.se/tjanster" />
```

---

## Prioritet: HÖG (Fixas inom 1 vecka)

### 6. Per-sida Schema Markup

**Problem:** Alla sidor returnerar startsidans 4 schema-block. /tjanster/lokal-seo borde ha Service-schema, /guider/* borde ha Article-schema.

**Åtgärd:**

| Sida | Schema |
|------|--------|
| / | LocalBusiness + Organization + WebSite + FAQPage (nuvarande — behåll) |
| /tjanster | Service (typ-lista med 3 tjänster) |
| /tjanster/lokal-seo | Service + Offer (Silver/Gold/Diamond-paket) |
| /tjanster/on-page-seo | Service |
| /tjanster/off-page-seo | Service |
| /guider/* | Article / BlogPosting (titel, publiceringsdat., författare) |
| /kontakt | ContactPage |
| /om-oss | AboutPage |

### 7. Lägg till AggregateRating Schema

**Problem:** Startsidan visar "4.9/5 rating" och "127 reviews" — men ingen AggregateRating schema.

**Åtgärd:**
```json
{
  "@context": "https://schema.org",
  "@type": "AggregateRating",
  "itemReviewed": {"@id": "https://primeseo.se/#localbusiness"},
  "ratingValue": "4.9",
  "bestRating": "5",
  "ratingCount": "127"
}
```

### 8. Lägg till BreadcrumbList Schema

**Åtgärd:**
```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {"@type": "ListItem", "position": 1, "name": "Hem", "item": "https://primeseo.se/"},
    {"@type": "ListItem", "position": 2, "name": "Tjänster", "item": "https://primeseo.se/tjanster"},
    {"@type": "ListItem", "position": 3, "name": "Lokal SEO", "item": "https://primeseo.se/tjanster/lokal-seo"}
  ]
}
```

### 9. Per-sida OG Tags

**Problem:** Alla sidor delar startsidans OG title, description och URL.

**Åtgärd:** Dynamiska OG-taggar per sida (samma approach som title/canonical-fix):
- `og:url` → sidans faktiska URL
- `og:title` → sidans unika title
- `og:description` → sidans unika description
- Behåll `og:image` (kan vara delad) men skapa unika bilder för tjänste- och guide-sidor om möjligt

### 10. Lägg till Google Site Verification

**Problem:** Saknas — krävs för Google Search Console.

**Åtgärd:**
```html
<meta name="google-site-verification" content="[VERIFIERINGSKOD]" />
```

---

## Prioritet: MEDIUM (Fixas inom 1 månad)

### 11. Implementera SSR eller Cloudflare Workers per-sida Injection

**Problem:** Alla sidor serverar identisk HTML med startsidans metadata. Den nuvarande H1-injection-approachen (JavaScript) fungerar som proof-of-concept men täcker inte title, canonical, description, schema eller OG-taggar.

**Åtgärd (Cloudflare Worker):** Skapa en Worker som matchar `pathname` och modifierar HTML-svaret:
- Byter `<title>` per sida
- Byter `<meta name="description">` per sida
- Byter `<link rel="canonical">` per sida
- Byter `hreflang` href per sida
- Byter OG/Twitter-taggar per sida
- Injicerar sidspecifik schema JSON-LD
- Uppdaterar H1 (ta bort JS-injection, använd server-side)

**Detta eliminerar behovet av SSR** och fungerar med Lovable.app.

---

### 12. Aktivera Browser Caching

**Problem:** `cache-control: no-cache, must-revalidate, max-age=0`

**Åtgärd (Cloudflare):**
- HTML: `max-age=300, stale-while-revalidate=86400`
- JS/CSS (har hash i filnamn): `max-age=31536000, immutable`
- Bilder: `max-age=604800`

---

### 13. Skapa llms.txt

**Åtgärd:**
```
# PrimeSEO
> PrimeSEO är en SEO-byrå i Hägersten, Stockholm som hjälper svenska företag ranka högre på Google, Google Maps och i AI-sökresultat.

## Tjänster
- Lokal SEO: Google Business Profile, recensioner, lokal synlighet (1 500–5 000 SEK/mån)
- On-page SEO: Innehåll, rubriker, interna länkar, teknisk optimering
- Off-page SEO: Backlinks, auktoritet, omnämnanden

## Paket
- PS Silver (Starter)
- PS Gold (Populär)
- PS Diamond (Enterprise)

## Guider
- Komplett guide till lokal SEO
- Google Business Profile-optimering
- SEO-strategi för B2B
- Vad är SEO?

## Kontakt
- Telefon: 010-555 87 28
- E-post: info@primeseo.se
- Adress: Lerkrogsvägen 21, 126 79 Hägersten
- Öppettider: Mån–Fre 10:00–17:00
```

---

### 14. Säkerhetsheaders

**Åtgärd (via Cloudflare):**
```
Content-Security-Policy: default-src 'self'; script-src 'self' https://www.googletagmanager.com 'unsafe-inline'; img-src 'self' data: blob:; style-src 'self' https://fonts.googleapis.com 'unsafe-inline'; font-src 'self' https://fonts.gstatic.com;
X-Frame-Options: SAMEORIGIN
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

---

### 15. Konsolidera/Ta bort Duplicerad Schema

**Problem:** LocalBusiness och Organization-schemas duplicerar delvis information.

**Åtgärd:**
- Lägg till `"@id"` på Organization och koppla till LocalBusiness
- Flytta `sameAs` till en plats (inkludera LinkedIn i Organization)
- Ta bort SearchAction om sökfunktionen inte fungerar

---

## Prioritet: LÅG (Backlog)

### 16. Ta bort meta keywords

**Problem:** Ignoreras av Google, avslöjar sökordsstrategi.

### 17. Optimera Bilder

- Byt OG-bild/logo från PNG → WebP
- Ge beskrivande filnamn (ej UUID)
- Lägg till alt-attribut i React-appen

### 18. Ta bort Lovable Information Leakage

**Problem:** Lovable events-script exponerar commit SHA och deployment tokens.

### 19. Dölj Supabase-instans-URL

**Problem:** Supabase-URL exponeras i robots.txt och som preconnect. Potentiell angreppyta.

**Åtgärd:** Använd en proxy (Supabase custom domain eller Cloudflare Worker) istället för direkt Supabase-URL.

### 20. Verifiera SearchAction

**Problem:** WebSite-schema har SearchAction med `?q={search_term_string}` — kontrollera att sökfunktionen faktiskt fungerar på sajten.

---

## Prioriterad Tidslinje

### Dag 1–3 (Omedelbart)
- [ ] Fixa canonical tags per sida (#1)
- [ ] Unika title tags per sida (#2)
- [ ] Unika meta descriptions per sida (#3)
- [ ] Uppdatera sitemap med alla sidor (#4)
- [ ] Fixa hreflang per sida (#5)

### Vecka 1–2
- [ ] Per-sida schema markup (#6)
- [ ] AggregateRating schema (#7)
- [ ] BreadcrumbList schema (#8)
- [ ] Per-sida OG tags (#9)
- [ ] Google Site Verification (#10)

### Månad 1
- [ ] Cloudflare Worker för per-sida injection (#11)
- [ ] Browser caching (#12)
- [ ] Skapa llms.txt (#13)
- [ ] Säkerhetsheaders (#14)
- [ ] Konsolidera schema (#15)

### Backlog
- [ ] Ta bort meta keywords (#16)
- [ ] Bildoptimering (#17)
- [ ] Lovable info leakage (#18)
- [ ] Supabase-URL (#19)
- [ ] SearchAction-verifiering (#20)

---

## Sammanfattning

| Prioritet | Antal | Huvudfokus |
|-----------|-------|------------|
| Kritisk | 5 | Canonical, unika titles/descriptions, sitemap, hreflang |
| Hög | 5 | Per-sida schema, AggregateRating, BreadcrumbList, OG, GSC |
| Medium | 5 | Cloudflare Worker, caching, llms.txt, säkerhet, schema-cleanup |
| Låg | 5 | meta keywords, bilder, info leakage, Supabase, SearchAction |

**Enskilt viktigaste åtgärden:** Fixa canonical tags. Alla undersidor pekar canonical till `/` — detta säger till Google "alla dessa sidor är egentligen startsidan, ignorera dem". Denna enda fix kan gå från 1 → 16+ indexerade sidor.

**Styrka att bygga vidare på:** Sajten har redan en sofistikerad SEO-grund: 4 schema-block, 57 crawlbara interna länkar, H1-injection, preconnect/preload, delayed analytics. Med per-sida metadata-injection (via Cloudflare Worker) kan scoren nå 75–85 utan att lämna Lovable.app.
