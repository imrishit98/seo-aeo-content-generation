# Next.js Integration Rules

Rules for generating SEO/AEO content as production-ready Next.js code. Load this file only when the output format is JSX/React (Next.js). These rules ensure generated code fits the existing codebase, follows Next.js best practices, and stays DRY.

---

## A. Smart Scan Procedure

Run this scan before generating any Next.js output. The scan discovers the project's structure, conventions, and existing components so generated code fits seamlessly.

### Step 1: List the Project Structure

Use `Glob` or directory listing to map the project tree. Identify the top-level structure:

```
Glob: "src/**/*" or "app/**/*"
```

Record:
- Whether the project uses `src/` directory or root-level `app/`
- Existing route segments and page files
- Component directories (`components/`, `src/components/`, `ui/`, etc.)
- Utility directories (`lib/`, `utils/`, `helpers/`, etc.)

### Step 2: Read `package.json`

Read `package.json` and extract:

| Field | What to Record |
|-------|----------------|
| `dependencies.next` | Next.js version (determines API availability: 13 = App Router stable, 14 = Server Actions stable, 15+ = async params/searchParams) |
| `dependencies.react` | React version (19+ = use hooks, async components natively) |
| `devDependencies.typescript` | Whether TypeScript is used (controls file extensions and type annotations) |
| `dependencies.tailwindcss` or `devDependencies.tailwindcss` | Whether Tailwind CSS is available (controls styling approach) |
| SEO libraries | Check for `next-seo`, `next-sitemap`, `@next/third-parties`, or custom SEO packages |
| CSS libraries | Check for `styled-components`, `@emotion/react`, `css-modules`, or other CSS-in-JS solutions |

### Step 3: Read Path Configuration

Read `tsconfig.json` (TypeScript projects) or `jsconfig.json` (JavaScript projects). Extract:

- `compilerOptions.paths` to detect import aliases (e.g., `"@/*": ["./src/*"]`)
- `compilerOptions.baseUrl` for module resolution

Use the detected alias pattern in all generated imports. If `@/` maps to `src/`, import as `@/components/seo/SchemaJsonLd` rather than `../../components/seo/SchemaJsonLd`.

### Step 4: Read the Root Layout

Read the root layout file to understand existing patterns:

- **App Router:** `app/layout.tsx` or `src/app/layout.tsx`
- **Pages Router:** `pages/_app.tsx` or `src/pages/_app.tsx`

Record:
- How metadata is currently handled (static `metadata` export, `generateMetadata`, `next-seo`, or manual `<Head>`)
- Shared wrappers, providers, or context in use
- Font setup (`next/font` imports and application)
- Global CSS imports
- Analytics or script integrations

### Step 5: Deep-Read Relevant Files

Based on the content being generated, read files in the target area:

| What to Read | Why |
|--------------|-----|
| Existing pages in the same route segment (e.g., other pages under `app/blog/`) | Match page structure, data fetching patterns, and component usage |
| Shared component directory (`components/`, `src/components/`) | Find existing reusable components to use instead of creating new ones |
| SEO/schema utilities (`lib/schema.ts`, `utils/seo.ts`, `components/seo/`) | Reuse existing schema generation, meta tag helpers, or structured data utilities |
| Layout files in the target route segment (`app/blog/layout.tsx`) | Understand shared layouts that wrap the generated page |
| Data fetching utilities (`lib/data.ts`, `lib/api.ts`, `services/`) | Match existing data fetching patterns (fetch, Prisma, Supabase, CMS SDK, etc.) |

### Step 6: Record Detected Patterns

After scanning, record these patterns for use during code generation:

| Pattern | Detection Method | Impact on Generated Code |
|---------|-----------------|-------------------------|
| **Router type** | Presence of `app/` directory = App Router; `pages/` directory = Pages Router | Determines metadata API, file conventions, and data fetching approach |
| **Language** | `typescript` in devDependencies, `.tsx` files present | Controls file extensions (`.tsx` vs `.jsx`), type annotations, and interface definitions |
| **Styling** | Tailwind classes in existing components, CSS Module imports, styled-components usage | Controls how components are styled |
| **Client boundaries** | `'use client'` directives in existing components | Determines where to place client boundaries in generated code |
| **Data fetching** | `fetch()`, Prisma client, Supabase client, CMS SDK calls in existing pages | Match data fetching patterns in generated pages |
| **Component naming** | PascalCase files vs kebab-case, barrel exports vs direct imports | Match naming conventions in generated components |
| **Import style** | `@/` alias vs relative paths, named vs default exports | Match import conventions in generated code |

---

## B. Shared SEO Component Library

When generating Next.js output, check if these components already exist in the project. If they do, reuse them. If they don't, create them in the appropriate directory (default: `src/components/seo/` or match the project's component directory structure).

### Component Placement Rules

1. Check if a `components/seo/` directory already exists. Use it if found.
2. If not, check the project's primary component directory (`components/`, `src/components/`, `app/components/`). Create an `seo/` subdirectory inside it.
3. If the project has no component directory convention, create `src/components/seo/`.
4. Add a barrel export file (`index.ts` or `index.tsx`) if the project uses barrel exports elsewhere.

### SchemaJsonLd Component

Renders JSON-LD structured data in a `<script>` tag. Replaces the repeated `dangerouslySetInnerHTML` pattern.

**TypeScript version:**

```tsx
interface SchemaJsonLdProps {
  schema: Record<string, unknown> | Record<string, unknown>[];
}

export function SchemaJsonLd({ schema }: SchemaJsonLdProps) {
  const jsonLd = Array.isArray(schema)
    ? { "@context": "https://schema.org", "@graph": schema }
    : { "@context": "https://schema.org", ...schema };

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
    />
  );
}
```

**JavaScript version:**

```jsx
export function SchemaJsonLd({ schema }) {
  const jsonLd = Array.isArray(schema)
    ? { "@context": "https://schema.org", "@graph": schema }
    : { "@context": "https://schema.org", ...schema };

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
    />
  );
}
```

**Usage:** Pass a single schema object or an array for `@graph` combination:

```tsx
<SchemaJsonLd schema={[articleSchema, faqSchema, breadcrumbSchema]} />
```

### FAQSection Component

Renders the FAQ section with proper heading hierarchy and semantic HTML. Pairs with FAQPage schema.

**TypeScript version:**

```tsx
interface FAQItem {
  question: string;
  answer: string;
}

interface FAQSectionProps {
  items: FAQItem[];
  headingLevel?: "h2" | "h3";
}

export function FAQSection({ items, headingLevel = "h3" }: FAQSectionProps) {
  const HeadingTag = headingLevel;

  return (
    <section>
      <h2>Frequently Asked Questions</h2>
      <dl>
        {items.map((item) => (
          <div key={item.question}>
            <dt>
              <HeadingTag>{item.question}</HeadingTag>
            </dt>
            <dd className="faq-answer">{item.answer}</dd>
          </div>
        ))}
      </dl>
    </section>
  );
}
```

**Usage:**

```tsx
const faqItems = [
  { question: "What is RAG?", answer: "RAG is an AI architecture..." },
  { question: "How does RAG work?", answer: "RAG works by first..." },
];

<FAQSection items={faqItems} />
```

The `faq-answer` class on `<dd>` elements enables SpeakableSpecification targeting via the CSS selector `.faq-answer`.

### AnswerCapsule Component

A semantic paragraph component with the `.answer-capsule` class for SpeakableSpecification targeting.

**TypeScript version:**

```tsx
interface AnswerCapsuleProps {
  children: React.ReactNode;
}

export function AnswerCapsule({ children }: AnswerCapsuleProps) {
  return <p className="answer-capsule">{children}</p>;
}
```

**Usage:**

```tsx
<h2>What Is Retrieval-Augmented Generation?</h2>
<AnswerCapsule>
  Retrieval-Augmented Generation (RAG) is an AI architecture that combines
  information retrieval with text generation to produce answers grounded in
  external data. Instead of relying only on training data, RAG systems search
  a knowledge base first, then generate responses using the retrieved documents
  as context (Lewis et al., 2020).
</AnswerCapsule>
```

### MetaTags Helper

A utility function that builds the Next.js `Metadata` object from structured input. Only create this if the project does not already have a metadata helper or pattern.

**TypeScript version (App Router):**

```tsx
import type { Metadata } from "next";

interface MetaTagsInput {
  title: string;
  description: string;
  canonicalUrl: string;
  ogImage?: string;
  ogType?: "website" | "article";
  twitterCard?: "summary" | "summary_large_image";
  keywords?: string[];
  author?: string;
}

export function buildMetadata(input: MetaTagsInput): Metadata {
  return {
    title: input.title,
    description: input.description,
    keywords: input.keywords,
    authors: input.author ? [{ name: input.author }] : undefined,
    openGraph: {
      title: input.title,
      description: input.description,
      url: input.canonicalUrl,
      images: input.ogImage ? [{ url: input.ogImage, width: 1200, height: 630 }] : undefined,
      type: input.ogType ?? "website",
    },
    twitter: {
      card: input.twitterCard ?? "summary_large_image",
      title: input.title,
      description: input.description,
      images: input.ogImage ? [input.ogImage] : undefined,
    },
    alternates: {
      canonical: input.canonicalUrl,
    },
  };
}
```

**Usage in a page file:**

```tsx
import { buildMetadata } from "@/components/seo";

export const metadata = buildMetadata({
  title: "Best CI/CD Tools for Startups in 2026",
  description: "Compare the top 8 CI/CD tools...",
  canonicalUrl: "https://example.com/blog/best-cicd-tools",
  ogImage: "https://example.com/images/cicd-tools-og.jpg",
  ogType: "article",
});
```

---

## C. Next.js Code Quality Rules

Apply these rules to all generated Next.js code. They ensure the output follows current Next.js best practices and integrates cleanly with the project.

### Metadata API

- **App Router (Next.js 13.2+):** Use the static `metadata` export or `generateMetadata` async function. Never use manual `<meta>` tags in `<head>`.
- **Pages Router:** Use `next/head` with `<Head>` component. Never use `document.title` or manual DOM manipulation.
- **Dynamic metadata** (content depends on params, e.g., programmatic SEO pages): Use `generateMetadata` with `async` and `await params`.

```tsx
// App Router: static metadata
export const metadata: Metadata = {
  title: "Page Title",
  description: "Page description",
};

// App Router: dynamic metadata (Next.js 15+)
export async function generateMetadata(
  { params }: { params: Promise<{ slug: string }> }
): Promise<Metadata> {
  const { slug } = await params;
  // ... fetch data based on slug
  return { title: "...", description: "..." };
}
```

### Server Components by Default

- All generated page components are Server Components unless they require interactivity.
- Only add `'use client'` when the component uses: `useState`, `useEffect`, `useRef`, event handlers (`onClick`, `onChange`, etc.), browser APIs (`window`, `document`, `localStorage`).
- Content pages (blog posts, landing pages, product pages) are almost always Server Components. They have no interactive state.
- If a small interactive element is needed (e.g., a copy button, accordion FAQ), extract only that element into a separate client component. Keep the page itself as a Server Component.

### Async APIs (Next.js 15+)

In Next.js 15 and later, `params`, `searchParams`, `cookies()`, and `headers()` are async. Generated code must handle this:

```tsx
// Correct for Next.js 15+
export default async function Page(
  { params }: { params: Promise<{ slug: string }> }
) {
  const { slug } = await params;
  // ...
}

// Correct for Next.js 13-14
export default function Page(
  { params }: { params: { slug: string } }
) {
  const { slug } = params;
  // ...
}
```

Check the Next.js version detected in Step 2 of the Smart Scan to determine which pattern to use.

### Image Handling

- Use `next/image` for all image references. Never use a plain `<img>` tag.
- Always include `alt`, `width`, and `height` attributes.
- Add `sizes` for responsive images.
- Use `priority` for above-the-fold images (hero images, LCP candidates).
- Configure `remotePatterns` in `next.config.js` if referencing external image domains.

```tsx
import Image from "next/image";

<Image
  src="/images/hero.jpg"
  alt="Descriptive alt text for SEO"
  width={1200}
  height={630}
  sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
  priority
/>
```

### TypeScript

When the project uses TypeScript (detected in Step 2):

- Use `.tsx` file extensions for components, `.ts` for utilities
- Define interfaces for all component props
- Type schema data objects explicitly
- Type the `Metadata` import from `next`
- Type `generateStaticParams` return values
- Use `React.ReactNode` for children props

When the project uses JavaScript:

- Use `.jsx` file extensions for components, `.js` for utilities
- Use JSDoc comments for complex prop shapes if the project uses JSDoc elsewhere
- Skip type annotations entirely (do not use TypeScript syntax in `.js` files)

### Import Conventions

- Match the project's detected import alias (from Step 3 of Smart Scan)
- If `@/` alias is configured, use it: `import { SchemaJsonLd } from "@/components/seo"`
- If no alias is detected, use relative imports: `import { SchemaJsonLd } from "../../components/seo"`
- Match the project's export style: if the project uses named exports, use named exports. If it uses default exports for pages, use default exports for pages.
- Match barrel export patterns: if `components/index.ts` re-exports, add new components to it.

### Styling

Match the project's detected styling approach:

| Detected Pattern | How to Style Generated Components |
|------------------|----------------------------------|
| Tailwind CSS | Use Tailwind utility classes directly. No separate CSS files. Use `className` strings. |
| CSS Modules | Create `.module.css` files alongside components. Import as `styles`. |
| styled-components / Emotion | Use the same CSS-in-JS library. Mark component as `'use client'` if needed. |
| Plain CSS | Use `className` strings referencing classes from global CSS. |
| No clear pattern | Default to Tailwind if installed, otherwise use CSS Modules. |

---

## D. DRY Code Patterns

### Before Creating Any Component

1. **Search the codebase first.** Before generating a new component, search for existing equivalents:
   - `Grep` for `application/ld+json` to find existing schema rendering
   - `Grep` for `FAQPage` or `faq` to find existing FAQ components
   - `Grep` for `generateMetadata` or `metadata` exports to find existing meta patterns
   - `Glob` for `**/seo/**`, `**/schema/**`, `**/meta/**` to find SEO utility directories

2. **Reuse if found.** If an existing component handles the same concern, use it directly. Do not create a duplicate.

3. **Extend if close.** If an existing component handles a similar concern but is missing a feature (e.g., a schema component that doesn't support `@graph`), extend it by adding the missing capability rather than creating a parallel component.

4. **Create only if absent.** Only create new shared components when no equivalent exists in the project.

### Page Generation Patterns

**Single content page (blog post, landing page, product page):**

Generate a single `page.tsx` file in the appropriate route segment. Include:
- `metadata` or `generateMetadata` export at the top
- Default-exported page component
- `SchemaJsonLd` component call with all required schemas
- Content sections using `AnswerCapsule` and `FAQSection` components
- No inline schema `<script>` tags (delegate to `SchemaJsonLd`)

**Programmatic SEO pages:**

Generate a dynamic route with:
- `page.tsx` with `generateMetadata` (dynamic, based on params)
- `generateStaticParams` exporting all known param values
- A data layer (function or file) providing unique content per param value
- Shared template structure reusing the same SEO components

```
app/
  glossary/
    [term]/
      page.tsx          # Template with generateStaticParams + generateMetadata
  blog/
    [slug]/
      page.tsx          # Dynamic blog post page
```

### Component Reuse Across Content Types

The shared SEO components (`SchemaJsonLd`, `FAQSection`, `AnswerCapsule`) work across all content types. When the skill generates multiple content pages in a project, these components are created once and reused everywhere. Never duplicate their logic into individual page files.

### Data Separation

Separate content data from presentation:

- **Schema data:** Define as a plain object or function, pass to `SchemaJsonLd`
- **FAQ data:** Define as an array of `{question, answer}` objects, pass to `FAQSection`
- **Metadata:** Define using `buildMetadata` helper or direct `metadata` export
- **Page content:** Render in the page component's JSX

This separation makes content updates easier without touching component logic, and keeps page files focused on structure rather than data wiring.

---

## E. Programmatic SEO with Next.js

When the route is `programmatic-seo` and the output format is Next.js, use dynamic route segments with static generation.

### File Structure

```
app/
  [routePattern]/
    page.tsx              # Page component with generateStaticParams
    _data/
      index.ts            # Data source: array of items with unique content per variable
      types.ts            # TypeScript interfaces for the data (if TS project)
```

### generateStaticParams Pattern

```tsx
import { getAllItems } from "./_data";

export async function generateStaticParams() {
  const items = await getAllItems();
  return items.map((item) => ({ slug: item.slug }));
}
```

### generateMetadata Pattern

```tsx
import type { Metadata } from "next";
import { getItemBySlug } from "./_data";

export async function generateMetadata(
  { params }: { params: Promise<{ slug: string }> }
): Promise<Metadata> {
  const { slug } = await params;
  const item = await getItemBySlug(slug);

  return buildMetadata({
    title: item.metaTitle,
    description: item.metaDescription,
    canonicalUrl: `https://example.com/${item.slug}`,
    ogType: "article",
  });
}
```

### Data Layer

The data layer provides unique content per variable. Each item must include at minimum:

- `slug`: URL parameter value
- `metaTitle`: Unique meta title (50-59 characters)
- `metaDescription`: Unique meta description (140-160 characters)
- `content`: Unique body content data (not shared across items)
- `faqItems`: Unique FAQ questions and answers
- `schemaData`: Pre-built schema objects for this specific item

The data layer can source from:
- A static TypeScript/JavaScript file with hardcoded data (simplest)
- A CMS API call
- A database query (Prisma, Supabase, etc.)
- A JSON/YAML data file
- A combination of static template + dynamic data

Match the project's existing data fetching pattern detected during the Smart Scan.
