# Schema Markup by Content Type

JSON-LD structured data templates mapped to each content type. Include the appropriate schemas in every piece of generated content.

---

## Schema Requirements by Content Type

| Content Type | Required Schemas | Optional Schemas |
|-------------|-----------------|-----------------|
| Blog post / article | Article + FAQPage + SpeakableSpecification | HowTo (if tutorial), BreadcrumbList |
| Listicle | Article + ItemList + FAQPage + SpeakableSpecification | BreadcrumbList |
| Landing page | WebPage + Organization + FAQPage + SpeakableSpecification | Product or SoftwareApplication |
| Product page | Product + FAQPage + WebPage + SpeakableSpecification | BreadcrumbList, AggregateRating |
| Directory listing | Organization + FAQPage + BreadcrumbList | LocalBusiness, Person |
| pSEO: Glossary | DefinedTerm + FAQPage + BreadcrumbList | WebPage |
| pSEO: Location | LocalBusiness + FAQPage + BreadcrumbList | Service |
| pSEO: Persona | Service + FAQPage + BreadcrumbList | WebPage |
| pSEO: Integration | SoftwareApplication + FAQPage + BreadcrumbList | WebPage |
| pSEO: Comparison | Article + FAQPage + SpeakableSpecification | BreadcrumbList |

---

## 1. Article Schema

**Use for:** Blog posts, articles, listicles, comparison pages, tutorials.

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[Article Title, max 110 characters]",
  "description": "[Meta description]",
  "image": [
    "https://example.com/image-16x9.jpg",
    "https://example.com/image-4x3.jpg",
    "https://example.com/image-1x1.jpg"
  ],
  "datePublished": "[YYYY-MM-DD]T[HH:MM:SS]+00:00",
  "dateModified": "[YYYY-MM-DD]T[HH:MM:SS]+00:00",
  "author": {
    "@type": "Person",
    "name": "[Author Name]",
    "url": "[Author Page URL]",
    "jobTitle": "[Author Title]",
    "worksFor": {
      "@type": "Organization",
      "name": "[Company Name]"
    }
  },
  "publisher": {
    "@type": "Organization",
    "name": "[Publisher Name]",
    "logo": {
      "@type": "ImageObject",
      "url": "[Logo URL]",
      "width": 600,
      "height": 60
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "[Canonical URL]"
  },
  "keywords": ["[keyword1]", "[keyword2]", "[keyword3]"],
  "articleSection": "[Category]",
  "wordCount": "[word count]",
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": ["h1", ".answer-capsule", ".faq-answer"]
  }
}
```

**Placeholder notes:**
- `headline`: Use the H1. Keep under 110 characters.
- `datePublished` / `dateModified`: Use today's date for new content.
- `author`: Use the author information gathered during context collection. If none provided, leave a placeholder for the user to fill.
- `keywords`: Primary keyword + 2-3 secondary keywords.
- `wordCount`: Actual word count of the generated content.

---

## 2. FAQPage Schema

**Use for:** Every content type. Pair with the FAQ section that appears on all pages.

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "[Question text exactly as it appears in the content]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Full answer text exactly as it appears in the content]"
      }
    },
    {
      "@type": "Question",
      "name": "[Question 2]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Answer 2]"
      }
    }
  ]
}
```

**Rules:**
- Include ALL FAQ questions from the content, not a subset
- Question `name` must match the H3 heading text exactly
- Answer `text` must match the answer content exactly
- Do not include HTML tags in the `text` field (plain text only)

---

## 3. WebPage Schema

**Use for:** Landing pages, product pages, any page that needs SpeakableSpecification.

```json
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "name": "[Page Title]",
  "description": "[Meta description, STRICTLY 140-160 characters]",
  "url": "[Canonical URL]",
  "datePublished": "[YYYY-MM-DD]",
  "dateModified": "[YYYY-MM-DD]",
  "inLanguage": "[en-US / en-GB / en-AU / en-CA]",
  "isPartOf": {
    "@type": "WebSite",
    "name": "[Site Name]",
    "url": "[Site Root URL]"
  },
  "author": {
    "@type": "Organization",
    "name": "[Organization Name]",
    "url": "[Organization URL]"
  },
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": ["h1", ".hero-description", ".answer-capsule", ".faq-answer"]
  }
}
```

**Notes:**
- Set `inLanguage` to match the detected regional English dialect
- `speakable` CSS selectors should target the most quotable elements on the page

---

## 4. Organization Schema

**Use for:** Landing pages, about pages, any page representing a company or brand.

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "[Organization Name]",
  "url": "[Site URL]",
  "logo": "[Logo URL]",
  "description": "[One-sentence organization description]",
  "foundingDate": "[YYYY]",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "[City]",
    "addressRegion": "[State/Province]",
    "addressCountry": "[Country Code]"
  },
  "contactPoint": {
    "@type": "ContactPoint",
    "contactType": "customer service",
    "email": "[Email]"
  },
  "sameAs": [
    "[Twitter URL]",
    "[LinkedIn URL]",
    "[GitHub URL]",
    "[Other profile URLs]"
  ]
}
```

**Notes:**
- `sameAs` links are critical for entity clarity. Include every official profile.
- `description` should use the "X is Y that Z" definition format.

---

## 5. Product Schema

**Use for:** Product pages, SaaS product pages, e-commerce pages.

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "[Product Name]",
  "description": "[Product description]",
  "image": ["[Product image URL]"],
  "brand": {
    "@type": "Brand",
    "name": "[Brand Name]"
  },
  "offers": {
    "@type": "Offer",
    "url": "[Product page URL]",
    "priceCurrency": "[USD / GBP / AUD / CAD]",
    "price": "[Price]",
    "priceValidUntil": "[YYYY-MM-DD]",
    "availability": "https://schema.org/InStock"
  }
}
```

**For SaaS products, use SoftwareApplication instead:**

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "[App Name]",
  "description": "[App description]",
  "applicationCategory": "[Category]",
  "operatingSystem": "[Cross-platform / Web / iOS / Android]",
  "url": "[App URL]",
  "featureList": [
    "[Feature 1]",
    "[Feature 2]",
    "[Feature 3]"
  ],
  "offers": {
    "@type": "Offer",
    "price": "[Price or 0 for free]",
    "priceCurrency": "[Currency]"
  },
  "author": {
    "@type": "Organization",
    "name": "[Company Name]",
    "url": "[Company URL]"
  }
}
```

---

## 6. DefinedTerm Schema

**Use for:** Glossary pages, definition pages, "What is X?" pages.

```json
{
  "@context": "https://schema.org",
  "@type": "DefinedTerm",
  "name": "[Term]",
  "description": "[Definition capsule text, 40-60 words]",
  "inDefinedTermSet": {
    "@type": "DefinedTermSet",
    "name": "[Site Name] Glossary",
    "url": "[Glossary index URL]"
  }
}
```

---

## 7. LocalBusiness Schema

**Use for:** Location pages, local business directory listings.

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "[Business Name] - [Location]",
  "description": "[Business description]",
  "url": "[Page URL]",
  "telephone": "[Phone]",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "[Street]",
    "addressLocality": "[City]",
    "addressRegion": "[State/Province]",
    "postalCode": "[Postal Code]",
    "addressCountry": "[Country Code]"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "[Latitude]",
    "longitude": "[Longitude]"
  },
  "areaServed": {
    "@type": "City",
    "name": "[City Name]"
  },
  "priceRange": "[Price Range, e.g., $$]"
}
```

---

## 8. Service Schema

**Use for:** Persona pages ("/for/[audience]/"), service-specific pages.

```json
{
  "@context": "https://schema.org",
  "@type": "Service",
  "name": "[Service] for [Audience]",
  "description": "[Service description for this audience]",
  "provider": {
    "@type": "Organization",
    "name": "[Company Name]",
    "url": "[Company URL]"
  },
  "audience": {
    "@type": "Audience",
    "audienceType": "[Audience type]"
  },
  "areaServed": "[Geographic area if applicable]"
}
```

---

## 9. ItemList Schema

**Use for:** Listicles, ranked lists, "Best X" pages.

```json
{
  "@context": "https://schema.org",
  "@type": "ItemList",
  "name": "[List title, e.g., Best Project Management Tools in 2026]",
  "description": "[List description]",
  "numberOfItems": "[Number of items]",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "[Item 1 Name]",
      "url": "[Item 1 URL if applicable]",
      "description": "[One-sentence description]"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "[Item 2 Name]",
      "url": "[Item 2 URL]",
      "description": "[One-sentence description]"
    }
  ]
}
```

---

## 10. BreadcrumbList Schema

**Use for:** Any page with navigation hierarchy (directory listings, glossary pages, location pages, persona pages).

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "[Site Root URL]"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "[Parent Category]",
      "item": "[Category URL]"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "[Current Page]"
    }
  ]
}
```

**Note:** The last item in the breadcrumb should not include an `item` URL (it represents the current page).

---

## 11. HowTo Schema

**Use for:** Tutorial articles, how-to guides, step-by-step content.

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "How to [Do Something]",
  "description": "[Brief description of the process]",
  "totalTime": "PT[X]M",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Step 1: [Step Name]",
      "text": "[Detailed step instructions]",
      "url": "[Page URL]#step1"
    },
    {
      "@type": "HowToStep",
      "name": "Step 2: [Step Name]",
      "text": "[Detailed step instructions]",
      "url": "[Page URL]#step2"
    }
  ]
}
```

---

## 12. SpeakableSpecification

**Use for:** Any page that should be extractable by voice assistants and AI systems. Add to WebPage or Article schema.

```json
{
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [
      "h1",
      ".answer-capsule",
      ".summary",
      ".key-takeaways",
      ".faq-answer",
      ".hero-description",
      ".tldr"
    ]
  }
}
```

Target the CSS selectors at the most quotable, extractable sections of the page. At minimum, always include `h1` and `.faq-answer`.

---

## Combining Schemas with @graph

When a page needs multiple schemas, combine them using `@graph` in a single `<script>` tag:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Article",
      "headline": "[Title]",
      "author": { ... },
      "datePublished": "[Date]",
      "speakable": { ... }
    },
    {
      "@type": "FAQPage",
      "mainEntity": [ ... ]
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [ ... ]
    },
    {
      "@type": "Organization",
      "name": "[Company]",
      "sameAs": [ ... ]
    }
  ]
}
```

### Rules for @graph

- Use a single `<script type="application/ld+json">` tag per page
- Include all schemas in one `@graph` array
- Each schema in the array is a separate object with its own `@type`
- Do not duplicate `@context` inside individual schemas (only at the top level)

---

## Validation

After generating schema, remind the user to validate:

1. **Google Rich Results Test:** `https://search.google.com/test/rich-results?url=[encoded-url]`
2. **Schema.org Validator:** `https://validator.schema.org/?url=[encoded-url]`
3. **Google Search Console:** Check "Enhancements" tab for schema errors after deployment
