# Content Type Templates

Detailed structural templates for each content type. When generating content, read the template matching the content type, then follow it precisely.

All templates share these universal rules (do not skip any):
- GEO optimization rules from [geo-optimization-rules.md](geo-optimization-rules.md)
- Writing rules from [writing-rules.md](writing-rules.md)
- Schema requirements from [schema-by-content-type.md](schema-by-content-type.md)
- Validation checklist from [content-quality-checklist.md](content-quality-checklist.md)

---

## Template 1: Blog Post / Article

**Use when:** Creating informational content targeting a search query. How-to guides, explainers, industry analysis, tutorials, opinion pieces backed by data.

**Word count:** 1,500-2,500 words

### Structure

```
H1: [Article Title with Primary Keyword]

Opening paragraph (first 150 words):
  - Directly answer the target query in 2-3 sentences
  - No preamble, no background setup
  - Include one sourced statistic

H2: [Question people search for]
  Answer capsule (40-60 words, self-contained)
  2-3 paragraphs expanding with data, examples, specifics
  1 sourced statistic minimum
  
H2: [Question people search for]
  Answer capsule (40-60 words, self-contained)
  2-3 paragraphs expanding
  Table or list if comparison/process data exists
  1 expert quote with attribution

H2: [Question people search for]
  Answer capsule
  Detailed expansion
  ...

(Repeat for 5-8 H2 sections total)

H2: Frequently Asked Questions
  H3: [Question]?
    2-4 sentence answer, starts with direct statement, includes one data point
  H3: [Question]?
    ...
  (5-8 FAQ items)
```

### H2 Heading Rules

- Phrase H2s as questions real people search for
- Use "People Also Ask" queries from Google as inspiration
- Each H2 must have a 40-60 word answer capsule immediately after it
- The answer capsule must make sense without any surrounding text

### Data Requirements

- 2-3 sourced statistics per major section: "Claim (Source, Year)"
- At least 1 expert quote with full attribution per 500 words
- Tables for any comparison data (never describe comparisons in prose)
- Numbered lists for any process or sequence

### FAQ Section Rules

- 5-8 questions
- Each answer starts with a direct statement (never "It depends..." or "Well...")
- Each answer is 2-4 sentences
- Each answer contains at least one specific data point or named reference
- Each answer stands alone without context

### Schema Required

Article + FAQPage + SpeakableSpecification

---

## Template 2: Listicle

**Use when:** Creating "Best X", "Top X", "X Tools for Y" content. Ranked or curated lists where each item gets a mini-review.

**Word count:** 1,200-2,000 words

### Structure

```
H1: [Number] Best [Category] [for Audience] in [Year]

Opening paragraph (first 150 words):
  - State the winner/top pick immediately
  - Why this list exists and who it helps
  - How items were evaluated (criteria)

H2: Quick Comparison
  Summary table:
  | Rank | [Item] | Best For | Key Strength | Price |
  (One row per item in the list)

H2: 1. [Item Name] -- Best for [Specific Use Case]
  Answer capsule (40-60 words defining the item and why it tops this category)
  
  H3: Key Features
    Bullet list of 4-6 features with specific details
  
  H3: Pros
    Bullet list (3-5 items, each with a specific claim)
  
  H3: Cons
    Bullet list (2-3 items, honest and specific)
  
  H3: Pricing
    Specific pricing with date: "(as of [Month Year])"
  
  H3: Who Should Use [Item]
    1-2 sentences describing the ideal user scenario

H2: 2. [Item Name] -- Best for [Specific Use Case]
  (Same structure as above)

(Repeat for all items, typically 5-15)

H2: How We Evaluated
  Numbered criteria list explaining the methodology
  Specific weights or scoring if applicable

H2: Frequently Asked Questions
  5-8 questions with self-contained answers

H2: The Verdict
  2-3 sentences restating the top pick with the key reason
  Brief mention of runner-up for a different use case
```

### Item Entry Rules

- Each item needs unique, specific analysis (not generic descriptions from the product's marketing page)
- Include at least one data point per item (user count, benchmark, rating, pricing)
- Pros must be specific: "Processes 10,000 records per second" not "Very fast"
- Cons must be honest and specific: "No free tier; starts at $49/month" not "Can be expensive"
- All pricing must include "(as of [Month Year])"

### Schema Required

Article + ItemList + FAQPage + SpeakableSpecification

---

## Template 3: Landing Page

**Use when:** Creating a conversion-focused page for a product, feature, or service. Commercial-intent queries. Pages where the goal is signups, demos, or purchases.

**Word count:** 800-1,500 words

### Structure

```
H1: [Product/Service] -- [Primary Benefit for Target Audience]

Hero section (first 150 words):
  - One sentence: what the product is and who it helps
  - One sentence: specific, quantified benefit
  - One sentence: social proof (user count, rating, named customer)
  - CTA button indication

H2: What Is [Product]?
  Answer capsule (40-60 words, self-contained definition)
  2-3 short paragraphs expanding with specifics

H2: How Does [Product] Work?
  Answer capsule
  Numbered list: 3-5 steps showing the user workflow
  Each step: one sentence of action, one sentence of outcome

H2: Key Features
  Table format:
  | Feature | What It Does | Benefit |
  5-8 features, one row each

H2: Who Is [Product] For?
  Answer capsule listing 3-4 audience segments
  Short paragraph per segment with specific use case

H2: [Product] vs [Top Competitor]
  Comparison table:
  | Capability | [Product] | [Competitor] |
  Include pricing, 5-8 feature rows, limitations
  Be factual, not salesy

H2: Pricing
  Clear pricing table if multiple tiers
  State free/trial tier details
  All pricing dated "(as of [Month Year])"

H2: What Customers Say
  2-3 specific testimonials with name, role, company
  Each testimonial includes a measurable result

H2: Frequently Asked Questions
  5-8 questions with self-contained answers

CTA section:
  Restate the core value proposition
  Clear call to action
```

### Landing Page Rules

- No superlatives without data: "fastest" needs a benchmark, "#1" needs a source
- Every benefit claim must have a specific number or comparison
- Social proof must name real companies or cite real metrics
- No pressure tactics or false urgency ("Limited time!" "Only 3 left!")
- Comparison section must be factual and verifiable

### Schema Required

WebPage + Organization + FAQPage + SpeakableSpecification

---

## Template 4: Product Page

**Use when:** Creating a page for a specific product (SaaS feature, e-commerce item, physical product). The page must define the product clearly enough for AI systems to cite it when users ask "What is [product]?"

**Word count:** 1,000-2,000 words

### Structure

```
H1: [Product Name]: [What It Does in One Phrase]

Opening paragraph (first 150 words):
  - "[Product] is [category] that [core function]." (X is Y that Z format)
  - One quantified benefit
  - One social proof element

H2: What Is [Product]?
  Answer capsule (40-60 words, definitional, self-contained)
  2-3 paragraphs expanding: what problem it solves, who uses it, key differentiator

H2: How Does [Product] Work?
  Answer capsule
  Numbered process (3-6 steps)
  Each step: action + outcome

H2: Key Features
  Table:
  | Feature | Description | Benefit |
  5-10 rows

H2: [Product] Pricing
  Pricing table:
  | Plan | Price | Includes | Best For |
  All pricing dated
  Free tier / trial details if applicable

H2: [Product] vs [Alternative 1]
  Comparison table with specific data points
  One-sentence verdict: when to choose each

H2: [Product] vs [Alternative 2]
  Same structure
  (Include 2-3 competitor comparisons for products in competitive markets)

H2: Use Cases
  H3: [Use Case 1]
    Specific scenario, named example if possible, measurable outcome
  H3: [Use Case 2]
    ...
  (3-5 use cases)

H2: What Users Say About [Product]
  2-3 testimonials or review excerpts with attribution
  Include specific results or metrics

H2: Frequently Asked Questions
  5-8 questions covering: what it is, how it works, pricing, alternatives, compatibility

H2: Getting Started with [Product]
  3-5 step quick start
  Link to documentation or signup
```

### Product Page Rules

- The definition in the first 150 words is the most important element: AI systems will quote it when asked "What is [Product]?"
- Use "X is Y that Z" format for the definition
- All pricing must be dated
- Competitor comparisons must be factual and verifiable
- Use cases must be specific scenarios, not abstract benefits

### Schema Required

Product (or SoftwareApplication) + FAQPage + WebPage + SpeakableSpecification + BreadcrumbList

---

## Template 5: Directory Listing Page

**Use when:** Creating a page for an entity in a directory (business, tool, person, organization). Common in aggregator sites, review platforms, and curated directories.

**Word count:** 600-1,200 words

### Structure

```
H1: [Entity Name] -- [Brief Descriptor]

Opening paragraph (first 150 words):
  - "[Entity] is [category] that [core function/purpose]." (X is Y that Z)
  - Founded/established date, location
  - Key distinguishing fact with source

H2: Quick Facts
  Table:
  | Detail | Value |
  | Founded | [Year] |
  | Headquarters | [Location] |
  | Employees | [Count or range] |
  | Pricing | [Starting price or range] |
  | Website | [URL] |
  | Category | [Category/Industry] |

H2: What Does [Entity] Do?
  Answer capsule (40-60 words)
  2-3 paragraphs with specific details about services/products
  Include one sourced statistic about the entity

H2: Key Features / Services
  Bullet list with 5-8 items
  Each item: feature name + one sentence of specific detail

H2: Pros and Cons
  Two-column table or separate bullet lists:
  | Pros | Cons |
  3-5 items each, all specific and verifiable

H2: Pricing
  Pricing details with date
  Table if multiple tiers
  Note free tier/trial if applicable

H2: [Entity] vs [Similar Entity]
  Brief comparison table (5-6 rows)
  One-sentence verdict

H2: User Reviews Summary
  Aggregate rating if available
  2-3 key themes from reviews
  Source of reviews (G2, Capterra, Trustpilot, etc.)

H2: Frequently Asked Questions
  3-5 questions specific to this entity
  Self-contained answers

H2: Related [Category] Listings
  Bullet list of 3-5 related entities with one-line descriptions
  Internal links to their directory pages
```

### Directory Listing Rules

- Every fact must be verifiable and sourced
- Do not fabricate reviews or ratings
- Include the "last verified" date for factual claims
- Related listings must link to actual pages on the site
- If data is unavailable for a section, note it rather than leaving the section out

### Schema Required

Organization (or LocalBusiness or Person) + FAQPage + BreadcrumbList

---

## Template 6: Programmatic SEO Page

**Use when:** Creating pages at scale using a template with variable data. Glossary terms, location pages, persona pages, integration pages, comparison pages generated from a data set.

**Word count:** 600-1,500 words

### Playbook Selection

Choose the right playbook based on the page pattern:

| Playbook | URL Pattern | Variable |
|----------|-------------|----------|
| Glossary | `/glossary/[term]/` | Term/concept |
| Location | `/[service]/[city]/` | City/region |
| Persona | `/for/[audience]/` | Audience segment |
| Integration | `/integrations/[tool]/` | Partner tool |
| Comparison | `/compare/[x]-vs-[y]/` | Product pair |
| Templates | `/templates/[type]/` | Template category |

### Universal pSEO Structure

```
H1: [Variable-specific title with primary keyword]

Opening paragraph (first 150 words):
  - Define the variable-specific topic immediately
  - Include one data point unique to this variable
  - State who this page helps and why

H2: [What/Why question about the variable]
  Answer capsule (40-60 words)
  2-3 paragraphs with variable-specific information
  At least 1 statistic unique to this page

H2: [How question about the variable]
  Answer capsule
  Numbered steps or process specific to this variable
  Concrete example relevant to this specific variable

H2: [Comparison or context section]
  Table comparing the variable to a related alternative
  Variable-specific data in every row

H2: Key [Details/Features/Facts]
  Table or list with variable-specific data
  No generic content that could apply to any page in the set

H2: Frequently Asked Questions
  3-5 questions specific to THIS variable (not the category)
  Each answer includes variable-specific data

Related pages:
  Links to 3-5 other pages in the same programmatic set
  Links to the hub/category page
```

### Batch Generation Rules

When generating multiple pages from this template:

1. **Unique data requirement:** Each page must have at least 3 data points that appear on no other page in the set
2. **Content uniqueness threshold:** No two pages may share more than 40% of their body content
3. **Variable-specific examples:** Examples, case studies, and scenarios must be specific to the variable (not generic)
4. **Skip rather than fake:** If unique data cannot be sourced for a variable, skip that page and flag it. Never generate thin content to fill a gap
5. **Vary FAQ questions:** No two pages in the set should have identical FAQ questions
6. **Internal linking:** Every page links to 3-5 related pages in the set and to the hub page

### Schema Required (varies by playbook)

| Playbook | Primary Schema |
|----------|---------------|
| Glossary | DefinedTerm + FAQPage + BreadcrumbList |
| Location | LocalBusiness + FAQPage + BreadcrumbList |
| Persona | Service + FAQPage + BreadcrumbList |
| Integration | SoftwareApplication + FAQPage + BreadcrumbList |
| Comparison | Article + FAQPage + SpeakableSpecification |
| Templates | CreativeWork + FAQPage + BreadcrumbList |

---

## Cross-Template Rules

These apply to every template above:

1. **H1:** One per page, contains the primary keyword
2. **Heading hierarchy:** H1 > H2 > H3 only. No skipped levels (never H1 > H3)
3. **Answer capsules:** Required after every question-style H2, 40-60 words, self-contained
4. **First 150 words:** Must directly answer the primary query
5. **Paragraphs:** 2-3 sentences maximum
6. **Tables:** Required for any comparison or multi-attribute data
7. **FAQ section:** Required on every page, minimum 3 questions
8. **Internal links:** Suggest 3-5 internal links to other pages on the site
9. **Meta tags:** Title (STRICTLY 50-59 chars, must be >=50 and <60), description (STRICTLY 140-160 chars, must be >=140 and <=160), OG tags, Twitter cards
10. **Schema:** Appropriate JSON-LD for the content type, always including FAQPage
11. **Zero fabricated facts:** Never invent statistics, quotes, expert names, study results, or any factual claim. Every data point must come from a real, verifiable source found via live research. Use `[NEEDS DATA]` placeholders when data cannot be found.
12. **Zero competitor citations:** Never cite, link to, or reference any direct competitor of the site you are writing for. Use neutral third-party sources instead.
