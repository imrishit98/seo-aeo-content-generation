# Next.js Integration Rules

Rules for generating SEO/AEO content as production-ready Next.js code. Load this file only when the output format is JSX/React (Next.js). These rules ensure generated code fits the existing codebase, follows Next.js best practices, and stays DRY.

**Default:** Examples use **JavaScript** and **`.jsx`** file extensions, since most integrations are JS projects. For TypeScript projects, use `.tsx`/`.ts`, add types, and mirror the same patterns.

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

Read `jsconfig.json` (JavaScript projects) or `tsconfig.json` (TypeScript projects). Extract:

- `compilerOptions.paths` to detect import aliases (e.g., `"@/*": ["./src/*"]`)
- `compilerOptions.baseUrl` for module resolution

Use the detected alias pattern in all generated imports. If `@/` maps to `src/`, import as `@/components/seo/SchemaJsonLd` rather than `../../components/seo/SchemaJsonLd`.

### Step 4: Read the Root Layout

Read the root layout file to understand existing patterns:

- **App Router:** `app/layout.jsx` or `src/app/layout.jsx` (or `.tsx` if the project uses TypeScript)
- **Pages Router:** `pages/_app.jsx` or `src/pages/_app.jsx` (or `.tsx` if the project uses TypeScript)

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
| SEO/schema utilities (`lib/schema.js`, `utils/seo.js`, `components/seo/`) | Reuse existing schema generation, meta tag helpers, or structured data utilities |
| Layout files in the target route segment (`app/blog/layout.jsx`) | Understand shared layouts that wrap the generated page |
| Data fetching utilities (`lib/data.js`, `lib/api.js`, `services/`) | Match existing data fetching patterns (fetch, Prisma, Supabase, CMS SDK, etc.) |

### Step 6: Record Detected Patterns

After scanning, record these patterns for use during code generation:

| Pattern | Detection Method | Impact on Generated Code |
|---------|-----------------|-------------------------|
| **Router type** | Presence of `app/` directory = App Router; `pages/` directory = Pages Router | Determines metadata API, file conventions, and data fetching approach |
| **Language** | `typescript` in devDependencies, `.tsx` files present | Controls file extensions (`.jsx` vs `.tsx`), JSDoc vs type annotations |
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
4. Add a barrel export file (`index.js` or `index.jsx`) if the project uses barrel exports elsewhere.

### SchemaJsonLd Component

Renders JSON-LD structured data in a `<script>` tag. Replaces repeated `dangerouslySetInnerHTML` patterns.

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

**Usage:** `<SchemaJsonLd schema={[articleSchema, faqSchema, breadcrumbSchema]} />`

### FAQSection Component

Renders the FAQ section with semantic HTML (`<dl>`). Pairs with FAQPage schema. The `faq-answer` class on `<dd>` enables SpeakableSpecification targeting.

```jsx
export function FAQSection({ items, headingLevel = "h3" }) {
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

### AnswerCapsule Component

Semantic paragraph with `.answer-capsule` class for SpeakableSpecification targeting.

```jsx
export function AnswerCapsule({ children }) {
  return <p className="answer-capsule">{children}</p>;
}
```

### MetaTags Helper

A utility function that builds the Next.js `Metadata` object from structured input. Only create this if the project does not already have a metadata helper or pattern.

**JavaScript (App Router):** use JSDoc so editors still understand the return type.

```jsx
/**
 * @param {object} input
 * @param {string} input.title
 * @param {string} input.description
 * @param {string} input.canonicalUrl
 * @param {string} [input.ogImage]
 * @param {"website"|"article"} [input.ogType]
 * @param {"summary"|"summary_large_image"} [input.twitterCard]
 * @param {string[]} [input.keywords]
 * @param {string} [input.author]
 * @returns {import("next").Metadata}
 */
export function buildMetadata(input) {
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

```jsx
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

```jsx
// App Router: static metadata (JSDoc optional)
/** @type {import("next").Metadata} */
export const metadata = {
  title: "Page Title",
  description: "Page description",
};

// App Router: dynamic metadata (Next.js 15+)
export async function generateMetadata({ params }) {
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

```jsx
// Correct for Next.js 15+
export default async function Page({ params }) {
  const { slug } = await params;
  // ...
}

// Correct for Next.js 13-14
export default function Page({ params }) {
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

```jsx
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

### JavaScript vs TypeScript

When the project uses **JavaScript** (default for this reference):

- Use `.jsx` file extensions for components, `.js` for utilities
- Use JSDoc (`/** @type {import("next").Metadata} */`, `@param`, etc.) for complex shapes when it helps tooling
- Skip TypeScript-only syntax (`interface`, `type`, generics on components) in source files

When the project uses **TypeScript**:

- Use `.tsx` for components, `.ts` for utilities
- Define interfaces for component props where the project does so elsewhere
- Type the `Metadata` import from `next` and `generateStaticParams` return values as appropriate

### Import Conventions

- Match the project's detected import alias (from Step 3 of Smart Scan)
- If `@/` alias is configured, use it: `import { SchemaJsonLd } from "@/components/seo"`
- If no alias is detected, use relative imports: `import { SchemaJsonLd } from "../../components/seo"`
- Match the project's export style: if the project uses named exports, use named exports. If it uses default exports for pages, use default exports for pages.
- Match barrel export patterns: if `components/index.js` re-exports, add new components to it.

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

1. **Search first:** `Grep` for `application/ld+json`, `FAQPage`, `generateMetadata`; `Glob` for `**/seo/**`, `**/schema/**`, `**/meta/**`
2. **Reuse** if an existing component handles the same concern
3. **Extend** if a similar component exists but is missing a feature
4. **Create only if absent**

### Page Generation Patterns

**Single content page:** Generate `page.jsx` with `metadata` export, default page component, `SchemaJsonLd`, `AnswerCapsule`, and `FAQSection`. No inline `<script>` tags.

**Programmatic SEO pages:** Generate dynamic route (`[slug]/page.jsx`) with `generateMetadata`, `generateStaticParams`, and a data layer providing unique content per param. See section E for details.

### Component Reuse Across Content Types

The shared SEO components (`SchemaJsonLd`, `FAQSection`, `AnswerCapsule`) work across all content types. When the skill generates multiple content pages in a project, these components are created once and reused everywhere. Never duplicate their logic into individual page files.

### Data Separation

Separate content data from presentation: schema data as plain objects passed to `SchemaJsonLd`, FAQ data as `{question, answer}[]` passed to `FAQSection`, metadata via `buildMetadata` or `metadata` export, and page content in JSX. This keeps page files focused on structure.

---

## E. Programmatic SEO with Next.js

When the route is `programmatic-seo` and the output format is Next.js, use dynamic route segments with static generation.

### File Structure

```
app/
  [routePattern]/
    page.jsx              # Page component with generateStaticParams
    _data/
      index.js            # Data source: array of items with unique content per variable
```

If the project uses TypeScript, use `.tsx`/`.ts` and add a `types.ts` (or inline types) only where the codebase already does.

### generateStaticParams Pattern

```jsx
import { getAllItems } from "./_data";

export async function generateStaticParams() {
  const items = await getAllItems();
  return items.map((item) => ({ slug: item.slug }));
}
```

### generateMetadata Pattern

```jsx
import { getItemBySlug } from "./_data";

export async function generateMetadata({ params }) {
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

Each item must include at minimum: `slug`, `metaTitle` (50-59 chars), `metaDescription` (140-160 chars), unique `content`, `faqItems`, and `schemaData`.

Data sources: static JS file, CMS API, database query (Prisma, Supabase), JSON/YAML file, or static template + dynamic data. Match the project's existing data fetching pattern from the Smart Scan.
