---
name: seo-aeo-content-generation
description: >-
  Generates SEO and AEO/GEO optimized content that ranks on Google, Bing, ChatGPT, Perplexity, Claude, and all AI search engines. Supports landing pages, blog posts, listicles, product pages, directory listings, and programmatic SEO pages. Routes each request to load only the needed reference files and workflow steps, keeping context focused. Outputs in any format: Markdown, HTML, JSX/React (Next.js), raw text, or framework-specific code (Astro, Svelte, WordPress, etc.). Produces human-written content with no em dashes, matched to the site's regional English dialect. Best results with 1-2 content pieces per session.
metadata:
  version: 1.0.0
---

# SEO & AEO Content Generation

Generate publish-ready content optimized for traditional search engines (Google, Bing) and AI search engines (ChatGPT, Perplexity, Claude, Gemini, Google AI Overviews, Copilot). Every piece of content produced by this skill is built to **rank** on Google and **get cited** by LLMs.

This skill generates content. It does not audit existing pages. For auditing, use the `seo-and-llm-rankings` skill instead.

---

## Phase 0: Task Identification and Routing

**Run this before anything else.** Identify what the user needs, then load only the reference files and workflow steps required for that task. Do not read all reference files upfront.

### Step 0: Detect Environment and Mode

Before classifying the task, determine the execution environment:

1. **Check if running inside an IDE (Cursor, VS Code, etc.):** If the user's request is in the context of a codebase (file tree visible, terminal available, workspace open), the skill is running inside an IDE.
2. **Check if the project is Next.js:** Look for `package.json` with `next` as a dependency, or `next.config.*` files in the workspace root.
3. **If Next.js is detected and the output format is JSX/React:** Load [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) as an additional reference file for all content routes. This file is loaded alongside the route-specific references listed in the table below.
4. **If the request is ambiguous or complex** (multiple content types needed, unclear target keyword, conflicting requirements, significant architectural decisions): Switch to Plan mode, ask clarifying questions, confirm the plan with the user, then switch back to normal mode for execution.
5. **If the request is clear** (single content type, clear keyword, straightforward requirements): Stay in normal mode and use `AskQuestion` for context gathering.

### Step 1: Classify the Task

Read the user's request and match it to one route from the table below. If the request is ambiguous, ask one clarifying question to determine the route before proceeding.

| Route                      | Trigger Keywords / Patterns                                                              | Reference Files to Read                                                                                                                                          | Workflow Steps                                        |
| -------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `blog-article`             | Blog post, article, how-to, tutorial, explainer, guide                                   | content-types.md (Template 1 only), writing-rules.md, geo-optimization-rules.md, schema-by-content-type.md (sections 1, 2, 12), content-quality-checklist.md     | Steps 1-7                                             |
| `listicle`                 | "Best X", "Top X", ranked list, "X tools for Y"                                          | content-types.md (Template 2 only), writing-rules.md, geo-optimization-rules.md, schema-by-content-type.md (sections 1, 2, 9, 12), content-quality-checklist.md  | Steps 1-7                                             |
| `landing-page`             | Landing page, conversion page, feature page, sales page                                  | content-types.md (Template 3 only), writing-rules.md, geo-optimization-rules.md, schema-by-content-type.md (sections 2, 3, 4, 12), content-quality-checklist.md  | Steps 1-7                                             |
| `product-page`             | Product page, SaaS page, feature page for a specific product                             | content-types.md (Template 4 only), writing-rules.md, geo-optimization-rules.md, schema-by-content-type.md (sections 2, 5, 10, 12), content-quality-checklist.md | Steps 1-7                                             |
| `directory-listing`        | Directory listing, entity page, business profile                                         | content-types.md (Template 5 only), writing-rules.md, geo-optimization-rules.md, schema-by-content-type.md (sections 2, 4, 10), content-quality-checklist.md     | Steps 1-7                                             |
| `programmatic-seo`         | Pages at scale, batch generation, template pages, pSEO, "generate X pages"               | content-types.md (Template 6 only), writing-rules.md, geo-optimization-rules.md, schema-by-content-type.md (varies by playbook), content-quality-checklist.md    | Steps 1-7, batch generation rules                     |
| `competitor-analysis-only` | "Analyze these competitors", "scrape these URLs", compare pages without drafting content | competitor-analysis-rules.md only                                                                                                                                | Competitor analysis section only, no content drafting |
| `schema-only`              | "Generate schema", "add structured data", "JSON-LD for this page"                        | schema-by-content-type.md (relevant sections only)                                                                                                               | Step 5 only                                           |
| `meta-tags-only`           | "Write meta tags", "title and description", "OG tags"                                    | None (instructions are inline in this file)                                                                                                                      | Step 6 only                                           |

**Conditional reference:** If Step 0 detected a Next.js project and the output format is JSX/React, also read [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) for every content route (`blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`) and for `schema-only`. This file is not needed for `meta-tags-only` or `competitor-analysis-only`.

### Step 2: Check for Competitor URLs

Only read [references/competitor-analysis-rules.md](references/competitor-analysis-rules.md) if the user provides competitor URLs to outrank. If no URLs are mentioned during context gathering and the user does not provide any when asked, skip the competitor analysis file and the "Competitor Content Analysis" section entirely.

### Step 3: Read Only What You Need

- **Content types:** Read only the template matching the classified route (e.g., Template 1 for `blog-article`), not the entire file.
- **Schema:** Read only the schema sections listed in the route table above, not all 12 templates.
- **Competitor analysis:** Only if competitor URLs are provided.
- **Writing rules and GEO rules:** Always read for content routes. Skip for `schema-only` and `meta-tags-only`.
- **Quality checklist:** Always read for content routes. For `schema-only`, use only section 5 (Schema Checks). For `meta-tags-only`, use only section 1 items 1.4, 1.5, 1.10, 1.11.

### Step 4: Confirm the Route

Before proceeding, state the classified route and the output format to the user in one sentence. Example: "I'll generate a blog post in markdown format." This gives the user a chance to correct course before any reference files are loaded.

---

## Content Volume

**Generate 1-2 pieces of content per session** (programmatic SEO: 2-3 pages after defining the template). Utility routes have no strict limit.

If the user asks for 3+ pieces, explain the quality trade-off and recommend splitting: "Each piece gets deeper research and more thorough validation when I focus on 1-2 at a time. Want me to start with the highest-priority piece?"

Never silently reduce research depth, skip validation steps, or shorten content to fit more pieces into a single session.

---

## Before You Start

These pre-work steps apply to all content routes (`blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`). For utility routes (`schema-only`, `meta-tags-only`, `competitor-analysis-only`), skip to the relevant workflow step directly.

**1. Check for product marketing context:**
If `.agents/product-marketing-context.md` exists (or `.claude/product-marketing-context.md` in older setups), read it first. Use that context and only ask the user for information not already covered.

**1.5. Smart codebase scan (Next.js projects only):**
If Step 0 detected a Next.js project, run the Smart Scan Procedure from [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) before generating any content. This scan identifies:
- Project structure and conventions (App Router vs Pages Router, TypeScript, Tailwind, import aliases)
- Existing SEO components and utilities to reuse (schema renderers, FAQ components, meta tag helpers)
- Layout files and metadata patterns already in use
- Pages in the same route area for consistency in structure and style
- Data fetching patterns (fetch, Prisma, Supabase, CMS SDK) to match in generated code

All generated code must match the patterns found during this scan. Do not generate code that contradicts detected conventions (e.g., do not use CSS Modules if the project uses Tailwind, do not use Pages Router patterns if the project uses App Router).

**2. Read existing site content for voice matching:**
If the user provides a URL, fetch 2-3 pages from their site. Analyze:
- Regional English dialect (American, British, Australian, Canadian, etc.)
- Tone (formal, casual, technical, conversational)
- Vocabulary patterns (industry jargon level, reading level)
- Sentence structure preferences

Match all generated content to these patterns. The detailed regional English detection rules are in [references/writing-rules.md](references/writing-rules.md), which is loaded for all content routes.

**3. Research the topic online before writing:**
Use `WebSearch` and `WebFetch` to pull the latest data, statistics, news, and developments on the topic before drafting. Do not rely solely on training data. Search for:
- Latest statistics and research (`"[topic] statistics 2026"`, `"[topic] research 2025 2026"`)
- Recent industry developments and news (`"[topic] latest news"`, `"[topic] updates [current year]"`)
- Current pricing, market data, and benchmarks (`"[topic] benchmarks [current year]"`)
- Recently published expert opinions and quotes

Incorporate what you find directly into the content with proper citations. If a search returns no useful results, note it and proceed with the best available data, but always attempt the search first. Fresh, accurate data is a top ranking signal for both Google and AI search engines.

**Factual accuracy is absolute.** Never fabricate any statistic, quote, or data point. Every number must trace to a real source found via live research. Use `[NEEDS DATA]` placeholders for unverifiable claims. Full rules in [references/writing-rules.md](references/writing-rules.md).

**4. Never generate without context:**
You must gather enough information to write content that fits the specific site, audience, and business goal. Do not guess. Ask.

---

## Context Gathering

Before generating any content, gather the following. Use `AskQuestion` if available, otherwise ask conversationally. Skip questions already answered by product-marketing-context or prior conversation. For ambiguous requests, switch to Plan mode first (see Step 0).

### Required Information

| #   | Question                                                                                                                                                   | Why It Matters                                                                                                               |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Content type** -- blog post, landing page, listicle, product page, directory listing, or programmatic SEO page?                                          | Determines structure, schema, and tone. Also used by the task router (Phase 0) to load only the relevant reference files.    |
| 2   | **Output format** -- Markdown (default), HTML, JSX/React (Next.js, etc.), raw text, or code for a specific framework (Astro, Svelte, WordPress PHP, etc.)? | Determines how content, meta tags, and schema are delivered. See the Output Format section below for details on each format. |
| 3   | **Site URL** -- what is the live site URL?                                                                                                                 | Needed for voice/dialect matching, internal linking, competitive context                                                     |
| 4   | **Target keyword(s)** -- what primary keyword should this page rank for? Any secondary keywords?                                                           | Drives H1, H2s, meta tags, and content structure                                                                             |
| 5   | **Search intent** -- informational, commercial investigation, transactional, or navigational?                                                              | Shapes the content angle and CTA strategy                                                                                    |
| 6   | **Target audience** -- who is reading this? Be specific: role, experience level, pain point                                                                | Determines depth, vocabulary, and examples                                                                                   |
| 7   | **Business goal** -- traffic, leads, signups, sales, brand awareness?                                                                                      | Shapes CTAs and conversion elements                                                                                          |

### Optional but Valuable

| #   | Question                                                                                                                                                                                      | Why It Matters                                                                                                                                                                                                                                                                                                                                        |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 8   | **Content to outrank** -- URLs of any pages you want this content to beat. Could be competitor pages, pages currently ranking for the target keyword, or any content you consider a benchmark | Deep scraping and analysis: extracts their heading structure, statistics, quotes, schema, FAQ, word count, and gaps. Your content is then built to exceed them on every dimension. If URLs are provided, the competitor-analysis-rules.md reference is loaded. See [references/competitor-analysis-rules.md](references/competitor-analysis-rules.md) |
| 9   | **Existing content on this topic** -- does the site already have related pages?                                                                                                               | Avoid keyword cannibalization, plan internal links                                                                                                                                                                                                                                                                                                    |
| 10  | **Word count preference** -- any target range?                                                                                                                                                | Default ranges vary by content type (see table below)                                                                                                                                                                                                                                                                                                 |
| 11  | **Specific data/stats to include** -- any proprietary data, case studies, or numbers?                                                                                                         | Proprietary data is the strongest differentiator for both SEO and GEO                                                                                                                                                                                                                                                                                 |
| 12  | **Author information** -- name, title, credentials for the byline                                                                                                                             | E-E-A-T signals, schema markup                                                                                                                                                                                                                                                                                                                        |
| 13  | **Tone/voice preferences** -- any specific style beyond what the site already uses?                                                                                                           | Overrides for this specific piece                                                                                                                                                                                                                                                                                                                     |
| 14  | **Direct competitors to avoid citing** -- which companies or sites are direct competitors? List names or URLs.                                                                                | Citations must NEVER link to or reference direct competitors. Identifying them upfront prevents accidentally sending link equity or reader attention to a rival. If not provided, infer from the site's product/service and ask to confirm.                                                                                                            |

### Default Word Counts by Content Type

| Content Type          | Default Word Count |
| --------------------- | ------------------ |
| Blog post / article   | 1,500-2,500        |
| Listicle              | 1,200-2,000        |
| Landing page          | 800-1,500          |
| Product page          | 1,000-2,000        |
| Directory listing     | 600-1,200          |
| Programmatic SEO page | 600-1,500          |

---

## Competitor Content Analysis

**Conditional section.** Only read [references/competitor-analysis-rules.md](references/competitor-analysis-rules.md) and execute this section if the user provides competitor URLs to outrank. If no URLs are provided during context gathering (question 8) and the user declines when asked, skip this entire section and proceed with standard SERP research in Step 1.

When competitor URLs are provided, follow this procedure:

1. **Ask** if not already answered during context gathering: "Do you have any existing pages or competitor URLs you want this content to outrank?"
2. **Scrape** each URL using `WebFetch`. Extract data points per the checklist in [references/competitor-analysis-rules.md](references/competitor-analysis-rules.md).
3. **Build the analysis report** using the templates in the reference file (per-URL report + Combined Analysis for multiple URLs).
4. **Present before drafting.** Get user confirmation before writing. Do not start drafting until the user approves the strategy.
5. **Apply all outranking rules** from [references/competitor-analysis-rules.md](references/competitor-analysis-rules.md) during drafting. Every rule is mandatory when competitor URLs were provided.

---

## Content Generation Workflow

Follow these steps in order. The task router (Phase 0) determines which steps apply. Skip steps not listed for your route.

### Step 1: Pre-Writing Analysis

**Routes:** `blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`. **Skip for:** `schema-only`, `meta-tags-only`, `competitor-analysis-only`.

Before writing a single word, complete this analysis:

**Intent mapping:** Write one sentence describing the searcher's specific problem or goal. What decision are they making? What do they need to learn?

**SERP research:** Use `WebSearch` to check the current top-ranking pages for the target keyword:
```
WebSearch: "[primary keyword]"
WebSearch: "[primary keyword] [current year]"
```

Analyze the competing pages:
- What format dominates? (listicle, tutorial, comparison, definition)
- What word count are they using?
- What questions do they answer?
- What do they miss?

**Gap analysis:** Identify 3-5 things the competing pages do not cover well. Your content must fill those gaps. If competitor URLs were provided and the Competitor Content Analysis (see above) is complete, merge those findings here: every gap from the competitor analysis becomes a required content element. Combine the SERP-based gaps with the competitor-specific gaps into a single prioritized list.

**Live topic research:** Use `WebSearch` and `WebFetch` to gather the latest real-world data on the topic. Run at least 3-5 searches:
```
WebSearch: "[topic] statistics [current year]"
WebSearch: "[topic] latest research [current year]"
WebSearch: "[topic] trends [current year]"
WebSearch: "[topic] expert opinion [current year]"
WebSearch: "[topic] case study [current year]"
```
For each useful result, use `WebFetch` to pull the full page and extract specific data points, quotes, and statistics. Record: the exact claim, the source name, the publication year, and the URL. These become your inline citations. Content built on live-researched data outranks content built on stale training data in every AI search engine.

**Citation plan:** List 5-8 authoritative sources you will reference. Prioritize sources found during live topic research above:
- Research papers, official documentation, government data
- Industry reports with named authors and dates
- Product documentation for technical claims
- Named experts you can quote

**NEVER cite direct competitors.** Never link to, cite, or reference any direct competitor's website or content. Use neutral third-party sources instead. Full rules in [references/geo-optimization-rules.md](references/geo-optimization-rules.md).

If competitor URLs were analyzed, review the statistics they cite and find newer or more authoritative versions of the same data. Your citation list must be fresher and more authoritative than any competitor's. Go to original research, not blog posts.

### Step 2: Select Content Structure

**Routes:** `blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`. **Skip for:** `schema-only`, `meta-tags-only`, `competitor-analysis-only`.

Read only the matching template from [references/content-types.md](references/content-types.md). The route table in Phase 0 tells you which template number to read. Do not read the entire file.

| Route               | Template to Read | Key Structural Feature                                   |
| ------------------- | ---------------- | -------------------------------------------------------- |
| `blog-article`      | Template 1 only  | H2s as questions, answer capsules, FAQ section           |
| `listicle`          | Template 2 only  | Numbered items, comparison table, verdict                |
| `landing-page`      | Template 3 only  | Hero, features table, social proof, comparison           |
| `product-page`      | Template 4 only  | Product definition, features, pricing, vs competitors    |
| `directory-listing` | Template 5 only  | Entity definition, key details table, related listings   |
| `programmatic-seo`  | Template 6 only  | Template variables, unique data per page, batch patterns |

### Step 3: Draft with GEO Rules

**Routes:** `blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`. **Skip for:** `schema-only`, `meta-tags-only`, `competitor-analysis-only`.

Apply all GEO optimization rules during drafting. Read [references/geo-optimization-rules.md](references/geo-optimization-rules.md) for the full specification.

**Mandatory GEO elements in every piece of content:**

1. **Answer capsules** -- After every question-style H2, write a 40-60 word self-contained paragraph that answers the question completely. AI systems will quote this verbatim.

2. **Citation density** -- Include 2-3 sourced statistics per major section. Format: "Claim (Source, Year)." Every number must have a named source.

3. **Quote slots** -- Include at least 1 expert quote with full attribution (name, title, organization) per 500 words.

4. **Extractability** -- Every key claim must stand alone. An AI system should be able to quote any single paragraph without needing the paragraph before or after it.

5. **Definition format** -- When defining terms, use the "X is Y that Z" structure: entity, category, differentiator.

6. **Tables and lists** -- Use tables for comparisons, numbered lists for processes, bullet lists for features. AI systems extract structured data more reliably than prose.

7. **First 150 words** -- Must contain a direct answer to the page's primary query. No preamble. No background. Answer first, then expand.

### Step 4: Apply Writing Rules

**Routes:** `blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`. **Skip for:** `schema-only`, `meta-tags-only`, `competitor-analysis-only`.

Read [references/writing-rules.md](references/writing-rules.md) for the complete specification. Key non-negotiable rules:

- **No em dashes.** Use commas, colons, semicolons, or parentheses instead.
- **No AI-tell words or phrases.** See banned lists in writing-rules.md.
- **ZERO fabricated facts.** Use `[NEEDS DATA]` placeholders for unverifiable claims.
- **Paragraphs: 2-3 sentences max.**
- **Vary sentence length.** No more than 2 consecutive sentences of similar word count.
- **Match regional English dialect.** See detection and application rules in writing-rules.md.

### Step 5: Add Schema Markup

**Routes:** `blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`, `schema-only`. **Skip for:** `meta-tags-only`, `competitor-analysis-only`.

Read only the relevant sections from [references/schema-by-content-type.md](references/schema-by-content-type.md) as specified in the route table (Phase 0). Do not read all 12 schema templates.

Every page must include:
- The primary schema type for the content type
- FAQPage schema for the FAQ section (present in all content types)
- SpeakableSpecification targeting H1, answer capsules, and FAQ answers
- `datePublished` and `dateModified` in all schemas that support them

### Step 6: Add Meta Tags

**Routes:** `blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`, `meta-tags-only`. **Skip for:** `schema-only`, `competitor-analysis-only`.

Generate meta tags in the output format selected by the user (see Output Format section). For markdown, output as an HTML code block. For HTML, embed in `<head>`. For JSX/Next.js, use the `metadata` export. For other frameworks, follow their conventions.

Generate for every page:

```html
<title>[Primary Keyword] - [Benefit or Angle] | [Brand]</title>
<!-- STRICTLY 50-60 characters. Must be at least 50 and NEVER 60 or more. Count every character including spaces, pipes, and brand name. Primary keyword near the beginning. -->

<meta name="description" content="[Compelling description with keyword, value prop, and implied CTA]">
<!-- STRICTLY 140-160 characters. Must be at least 140 and NEVER exceed 160. Count every character including spaces and punctuation. -->

<meta property="og:title" content="[Title]">
<meta property="og:description" content="[Description]">
<meta property="og:image" content="[Image URL 1200x630]">
<meta property="og:url" content="[Canonical URL]">
<meta property="og:type" content="[website|article]">

<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="[Title]">
<meta name="twitter:description" content="[Description]">
<meta name="twitter:image" content="[Image URL]">
```

### Step 7: Validate

**Routes:** All routes run validation, but the scope varies:
- **Content routes** (`blog-article`, `listicle`, `landing-page`, `product-page`, `directory-listing`, `programmatic-seo`): Run the full checklist from [references/content-quality-checklist.md](references/content-quality-checklist.md). If competitor URLs were provided and analyzed, also run the Competitor Outranking Checks (Section 7 of the checklist).
- **`schema-only`**: Run only Section 5 (Schema Checks) from the checklist.
- **`meta-tags-only`**: Run only checks 1.4, 1.5, 1.10, and 1.11 from Section 1 (SEO Checks).
- **`competitor-analysis-only`**: No validation checklist needed (the analysis report itself is the output).

Present the validation results to the user as a scored checklist:

```markdown
## Content Validation

### SEO Checks
- [x] H1 contains primary keyword
- [x] Meta title: strictly 50-60 chars (must be >=50 and <60)
- [x] Meta description: strictly 140-160 chars (must be >=140 and <=160)
- ...

### GEO Checks
- [x] Answer capsule after every question-style H2
- [x] 2-3 sourced stats per section
- [x] Zero citations to direct competitors
- ...

### Writing Quality
- [x] Zero em dashes
- [x] Zero AI-tell words
- [x] Zero fabricated facts
- [x] Regional English consistent (American/British/Australian/Canadian)
- ...

### Competitor Outranking (if competitor URLs provided)
- [x] Covers every topic competitors cover
- [x] More sourced statistics than best competitor
- [x] More expert quotes than best competitor
- [x] Stronger first 150 words
- [x] More FAQ questions
- [x] Better schema markup
- [x] Fresher data
- [x] More structured data elements
- [x] All identified gaps filled

### AI Citation Score Estimate: X/10
```

---

## Output Format

Deliver content in the format the user selected during context gathering (question 2). If no format was specified, default to **Markdown**. In every format, meta tags and schema markup are embedded natively rather than appended as separate blocks.

### Markdown (default)

Standard markdown with heading hierarchy, tables, and code blocks for schema.

```markdown
# Content Output: [Page Title]

## Meta Tags
[Title, description, OG tags, Twitter cards as HTML code block]

## Content
[Full page content with H1/H2/H3 hierarchy, markdown tables, lists]

## Schema Markup
[JSON-LD in a json code block]

## Internal Linking Suggestions
[3-5 pages on the site this content should link to]
[3-5 pages on the site that should link back to this content]

## Validation Report
[Scored checklist from Step 7]
```

### HTML

Full semantic HTML document. Meta tags go in `<head>`, schema goes in `<script type="application/ld+json">`, content uses `<article>`, `<section>`, `<table>`, and semantic heading tags.

```html
<!DOCTYPE html>
<html lang="[detected dialect]">
<head>
  <title>[Meta title]</title>
  <meta name="description" content="[Meta description]">
  <!-- OG tags, Twitter cards -->
  <script type="application/ld+json">[Schema JSON-LD]</script>
</head>
<body>
  <article>
    <h1>[Title]</h1>
    <!-- Full content with semantic HTML -->
  </article>
</body>
</html>
```

Append internal linking suggestions and the validation report as HTML comments or as a separate markdown section after the HTML block.

### JSX / React (Next.js)

Export a React component with Next.js `metadata` or `generateMetadata` for meta tags. Use the shared SEO components (`SchemaJsonLd`, `FAQSection`, `AnswerCapsule`) from [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) section B instead of inline boilerplate. Use TypeScript if the project uses TypeScript. Follow all conventions detected during the Smart Scan (Step 1.5).

**Before generating:** Check if these components already exist in the project. If not, create them in the project's component directory (default: `src/components/seo/`).

**Static content pages:** Use `metadata` export + default page component with `SchemaJsonLd`, `AnswerCapsule`, and `FAQSection`. See [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) section D for the full pattern.

**Programmatic SEO pages:** Use `generateMetadata` + `generateStaticParams` + data layer. See [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) section E for the full pattern.

Append internal linking suggestions and the validation report as a separate markdown section after the code.

### Raw Text

Plain text with headings indicated by formatting conventions (ALL CAPS for H1, Title Case with underlines for H2). No markup of any kind. Schema and meta tags are provided in a separate section after the content body since they cannot be embedded in plain text.

### Framework-Specific Code

For other frameworks (Astro, Svelte, WordPress PHP, Hugo, etc.), adapt the output to that framework's conventions:

- **Astro:** `.astro` component with frontmatter for meta, `<script type="application/ld+json">` for schema
- **Svelte:** `.svelte` component with `<svelte:head>` for meta tags and schema
- **WordPress:** PHP template with `wp_head` action for meta, `wp_footer` for schema
- **Hugo / Jekyll:** Markdown with frontmatter for meta, partial/include for schema

If the framework is not listed here, ask the user for a sample component or page file from their project, then match that structure.

In all formats, always include internal linking suggestions and the validation report after the main content output.

---

## Programmatic SEO: Batch Generation

**Route:** `programmatic-seo` only. Skip this section for all other routes.

When generating pages at scale (e.g., `/glossary/[term]/`, `/for/[audience]/`, `/compare/[x]-vs-[y]/`):

1. Define the **template structure** once using Template 6 from [references/content-types.md](references/content-types.md)
2. Define the **variable list** (terms, cities, audiences, products)
3. For each variable, specify **3+ unique data points** that differentiate that page from all others
4. Generate pages one at a time, varying:
   - Examples and case studies
   - Local/audience-specific statistics
   - Comparison targets
   - FAQ questions
5. Validate that no two pages share more than 40% of their content

**Batch generation must never produce thin content.** If unique data cannot be sourced for a variable, skip that page and flag it rather than generating a low-quality version.

### Next.js Programmatic SEO

For Next.js projects, programmatic SEO pages should use dynamic route segments (`[slug]`, `[term]`, `[city]`) with `generateStaticParams` for static generation at build time. Create a single page component with a data-fetching layer, not separate files per page.

**File structure:**

```
app/
  glossary/
    [term]/
      page.tsx              # Template component with generateStaticParams + generateMetadata
      _data/
        index.ts            # Data source providing unique content per term
        types.ts            # TypeScript interfaces (if TS project)
```

**Key rules for Next.js pSEO:**

1. Use `generateStaticParams` to export all known parameter values for build-time static generation
2. Use `generateMetadata` (not static `metadata`) since meta tags vary per page
3. Separate content data from the page component: keep unique-per-page data in a data layer (`_data/` directory, CMS, database), keep the template in `page.tsx`
4. Reuse the shared SEO components (`SchemaJsonLd`, `FAQSection`, `AnswerCapsule`) across all generated pages
5. Match the project's existing data fetching pattern detected during the Smart Scan
6. See [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) section E for full implementation patterns

---

## Platform-Specific Optimization Tips

Apply these during drafting based on which platforms matter most to the user:

| Platform             | Key Optimization                            | Content Implication                                                |
| -------------------- | ------------------------------------------- | ------------------------------------------------------------------ |
| Google (traditional) | Backlinks + E-E-A-T + Core Web Vitals       | Strong author bios, external links to primary sources              |
| Google AI Overviews  | E-E-A-T + Schema + Knowledge Graph          | Structured data, clear entity definitions, tables                  |
| ChatGPT              | Domain authority + content-answer fit       | Self-contained answer paragraphs, branded definitions              |
| Perplexity           | Semantic relevance + freshness + FAQ Schema | FAQ sections, dated content, high factual density                  |
| Claude               | Factual density + structural clarity        | Data-rich paragraphs, clear hierarchies, authoritative definitions |
| Copilot              | Bing index + MS ecosystem                   | Bing-indexable content, LinkedIn/GitHub presence mentions          |

---

## Related Skills

- **seo-and-llm-rankings** -- Audit existing content for SEO and AI visibility issues
- **seo-audit** -- Technical SEO audit (crawl errors, indexing, page speed)
- **programmatic-seo** -- Strategy and planning for pages at scale
- **optimize-for-ai** -- Deep dive into AI citation architecture and entity building
- **product-marketing-context** -- Create the foundational context document for all marketing skills

## References

- [references/content-types.md](references/content-types.md) -- Detailed templates for each content type
- [references/writing-rules.md](references/writing-rules.md) -- Human writing rules, anti-AI detection, regional English
- [references/geo-optimization-rules.md](references/geo-optimization-rules.md) -- GEO methods for content generation
- [references/schema-by-content-type.md](references/schema-by-content-type.md) -- JSON-LD schema per page type
- [references/content-quality-checklist.md](references/content-quality-checklist.md) -- Post-generation validation checklist
- [references/competitor-analysis-rules.md](references/competitor-analysis-rules.md) -- Competitor scraping, analysis, and outranking methodology
- [references/nextjs-integration-rules.md](references/nextjs-integration-rules.md) -- Next.js codebase scanning, shared SEO components, code quality rules, and DRY patterns (loaded conditionally for JSX/Next.js output)
