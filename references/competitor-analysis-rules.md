# Competitor Content Analysis Rules

When a user provides URLs of pages they want to outrank, follow this procedure to scrape, analyze, and build a content strategy that beats every provided reference on SEO, AEO/GEO, and content quality dimensions.

This process applies to any URL the user wants to surpass: direct competitors, pages currently ranking for the target keyword, or any content the user considers a benchmark.

---

## When to Trigger

Run when the user provides URLs to outrank (competitor pages, currently-ranking pages, benchmarks, or their own existing content). If no URLs are provided, skip and proceed with standard SERP research.

---

## Scraping Procedure

For each URL the user provides:

### 1. Fetch the Page

```
WebFetch: "[competitor URL]"
```

If `WebFetch` fails (paywall, bot block, 404), note the failure and ask the user to paste the content manually. Do not skip the URL silently.

### 2. Extract These Data Points

Work through the fetched content and record each of the following. If a data point is not present on the page, record "Not found" (this becomes a gap you can exploit).

| Data Point | What to Record |
|------------|---------------|
| **Title tag** | Exact title text, character count |
| **Meta description** | Exact description text, character count |
| **H1** | Exact H1 text, whether it contains the target keyword |
| **Heading structure** | All H2s and H3s listed in order |
| **Word count** | Estimated word count of body content |
| **Topics covered** | One-sentence summary per H2 section |
| **Statistics cited** | Each stat with its source and year (e.g., "42% -- Forrester, 2024") |
| **Total statistic count** | Number of sourced statistics in the piece |
| **Expert quotes** | Each quote with attribution (name, title, org) |
| **Total quote count** | Number of attributed expert quotes |
| **Tables present** | Count of data tables, brief description of each |
| **Lists present** | Count of numbered and bullet lists |
| **FAQ section** | Whether present, number of questions, list each question |
| **Answer capsules** | Whether self-contained answer paragraphs appear after headings |
| **Schema markup** | Types of schema detected (if visible in the fetched content) |
| **Internal links** | Approximate count of links to other pages on the same domain |
| **External links** | Approximate count of outbound links to other domains |
| **Publication date** | Date published or last modified (if visible) |
| **Author information** | Author name, title, credentials (if present) |
| **Regional English** | Dialect detected (American, British, Australian, Canadian) |
| **CTA type** | What action the page tries to drive (signup, purchase, download, none) |
| **Unique strengths** | 2-3 things this page does notably well |
| **Obvious weaknesses** | 2-3 things this page does poorly or omits entirely |

---

## Competitor Analysis Report

After scraping, build a structured report for each competitor URL. Present this to the user before drafting.

### Per-URL Report Template

```markdown
## Competitor Analysis: [Page Title]
**URL:** [url]
**Target keyword match:** [How well the page targets the same keyword]

### Content Profile
| Metric | Competitor | Our Target |
|--------|-----------|------------|
| Word count | [X] | [X + 20-30% or matched] |
| H2 sections | [X] | [X + 2-3 additional] |
| Sourced statistics | [X] | [X + 3-5 more] |
| Expert quotes | [X] | [X + 1-2 more] |
| Data tables | [X] | [X + 1-2 more] |
| FAQ questions | [X] | [X + 2-3 more] |
| Answer capsules | [Yes/No] | Yes (mandatory) |
| Schema types | [types] | [same + additional types] |

### Topics Covered
[Numbered list of every topic/section the competitor covers]

### Statistics They Cite
[List every sourced statistic with its source and year]

### Gaps Found
1. [Gap 1: topic not covered, data missing, outdated info, etc.]
2. [Gap 2]
3. [Gap 3]
...

### Strengths to Match or Beat
1. [Strength 1: what they do well that we must equal or exceed]
2. [Strength 2]
...
```

---

## Multiple Competitor Handling

When the user provides 2 or more URLs, analyze each one individually using the report template above, then produce a **Combined Analysis** that synthesizes findings across all competitors.

### Combined Analysis Template

```markdown
## Combined Competitor Analysis

### Competitors Analyzed
1. [URL 1] -- [Title]
2. [URL 2] -- [Title]
3. [URL 3] -- [Title] (if applicable)

### Topic Coverage Matrix
| Topic | Comp 1 | Comp 2 | Comp 3 | Our Content |
|-------|--------|--------|--------|-------------|
| [Topic A] | Yes | Yes | No | Must cover |
| [Topic B] | Yes | No | Yes | Must cover |
| [Topic C] | No | No | No | Opportunity |
| [Topic D] | Weak | Yes | Weak | Cover in depth |

### Best-in-Class Benchmarks
| Dimension | Best Competitor | Their Score | Our Target |
|-----------|----------------|-------------|------------|
| Word count | [Comp X] | [X words] | [X + 20%] |
| Statistics | [Comp X] | [X stats] | [X + 5] |
| Expert quotes | [Comp X] | [X quotes] | [X + 2] |
| FAQ questions | [Comp X] | [X questions] | [X + 3] |
| Tables | [Comp X] | [X tables] | [X + 2] |

### Universal Gaps (No Competitor Covers)
[Topics, data points, or structural elements that NONE of the competitors include. 
These are the highest-value opportunities for differentiation.]

### Shared Weaknesses
[Common problems across all competitors: outdated data, missing schema, no FAQ, 
prose comparisons instead of tables, no answer capsules, etc.]
```

---

## Outranking Rules

After completing the analysis, apply these rules during content drafting. Every rule is mandatory when competitor URLs were provided.

### Content Depth

1. **Cover every topic the competitor covers.** List the competitor's H2s. Your content must address every one of those topics, either as its own H2 or within a broader section.
2. **Fill every gap.** Every gap identified in the analysis becomes a required section or data point in your content.
3. **Match or exceed word count.** Target 20-30% more words than the longest competitor, unless the competitor is clearly padding with filler. In that case, match word count but with higher information density.
4. **Add 2-3 topics no competitor covers.** Use the "Universal Gaps" from the combined analysis, or research additional subtopics via `WebSearch`.

### Data and Evidence

5. **Include more sourced statistics.** Count the competitor's sourced statistics. Your content must include at least 3-5 more, each with named source and year.
6. **Cite fresher data.** If the competitor cites data from 2023 or earlier, search for 2025-2026 data on the same claims. Use `WebSearch` to find updates: `"[claim topic] statistics 2025 2026"`.
7. **Include more expert quotes.** Count the competitor's attributed quotes. Your content must include at least 1-2 more, each with full attribution (name, title, organization).
8. **Find better sources.** If the competitor cites blog posts or secondary sources, find the original research, official documentation, or primary data instead.

### Structure and GEO

9. **Add answer capsules where competitors lack them.** If the competitor does not use self-contained answer paragraphs after headings, adding 40-60 word answer capsules gives your content an immediate GEO advantage.
10. **Convert prose comparisons to tables.** If the competitor describes comparisons in paragraph form, present the same data in a structured table.
11. **Add more structured data.** For every comparison, process, or feature list the competitor writes in prose, use a table, numbered list, or bullet list instead.
12. **Build a stronger FAQ section.** Include every FAQ question the competitor uses, plus 2-3 additional questions sourced from Google's "People Also Ask" for the target keyword.

### Opening and Extractability

13. **Write a stronger first 150 words.** Your opening must deliver a more direct, data-backed answer than the competitor's opening. Include a sourced statistic in the first 150 words that the competitor does not have.
14. **Make every paragraph self-contained.** Each paragraph should be quotable on its own. If the competitor's paragraphs depend on surrounding context, this is a structural advantage for your content.

### Technical SEO

15. **Use superior schema markup.** Include every schema type the competitor uses, plus any additional types appropriate for the content type (see [schema-by-content-type.md](schema-by-content-type.md)). If the competitor has no visible schema, adding it gives your content a significant advantage.
16. **Write better meta tags.** Your title tag must be STRICTLY 50-59 characters (>=50 and <60) with the keyword near the front. Your meta description must be STRICTLY 140-160 characters (>=140 and <=160) and more compelling than the competitor's, with a clearer value proposition.

### Freshness

17. **Use more recent data.** If the competitor's content is older than 6 months, make freshness a primary differentiator. Date all statistics. Include `datePublished` and `dateModified` in schema.
18. **Reference current developments.** Use `WebSearch` to find any recent news, product updates, or industry changes the competitor's content predates.

---

## Presenting the Analysis

Present the competitor analysis to the user **before** starting the draft. Include per-URL reports, combined analysis (if multiple URLs), and a Content Strategy Summary listing how your content will exceed competitors on each dimension (topics, statistics, quotes, tables, FAQ questions, answer capsules, schema). Ask: "Shall I proceed with drafting, or would you like to adjust the strategy?"

---

## Edge Cases

### Competitor page cannot be fetched
If `WebFetch` fails on a URL, inform the user and offer two options:
1. The user pastes the page content directly
2. Skip that URL and proceed with the others

### Competitor content is very short (under 300 words)
Note that the competitor has thin content. This is an advantage: producing a thorough, data-rich page on the same topic will outrank thin content on almost every dimension. Set minimum word count to 800 words regardless of the thin competitor benchmark.

### Competitor content is very long (over 5,000 words)
Do not try to exceed word count for the sake of it. Instead, focus on information density: cover the same topics in fewer words with more data points, better structure, and stronger extractability. Aim for 70-80% of the competitor's word count with higher data density.

### Competitor targets a different keyword
If the competitor page targets a related but different keyword, note the keyword mismatch. Still analyze the content for structural and topical insights, but do not force keyword alignment where it does not fit.

### User provides their own existing page
If the URL is the user's own site, treat it as a "current state" baseline rather than a competitor. Frame the analysis as "improvements over your current version" rather than "beating the competitor."
