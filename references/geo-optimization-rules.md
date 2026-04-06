# GEO Optimization Rules for Content Generation

Rules for making generated content citable by AI search engines (ChatGPT, Perplexity, Claude, Gemini, Google AI Overviews, Copilot). Based on the Princeton GEO research (2023, KDD 2024) with 2026 field data updates.

Apply every rule in this file during content drafting. These are not post-production tweaks. They shape how content is structured from the first word.

---

## The 9 GEO Methods (Ranked by Impact)

| Rank | Method | Visibility Boost | Application |
|------|--------|-----------------|-------------|
| 1 | Cite Sources | +27-40% | Add authoritative citations with author, publication, year |
| 2 | Statistics Addition | +33-37% | Include specific numbers with named sources |
| 3 | Quotation Addition | +30-43% | Add expert quotes with full attribution |
| 4 | Authoritative Tone | +25% | Write with confidence, back claims with data |
| 5 | Easy-to-Understand | +20% | Explain complex concepts accessibly |
| 6 | Technical Terms | +18% | Include domain-specific terminology correctly |
| 7 | Unique Words | +15% | Diversify vocabulary, avoid repetition |
| 8 | Fluency Optimization | +15-30% | Improve readability and logical flow |
| 9 | Keyword Stuffing | **-9 to -10%** | **NEVER DO THIS. Actively decreases visibility** |

### Best Method Combinations

| Combination | When to Use |
|-------------|-------------|
| Fluency + Statistics | Maximum overall boost. Use for every content type |
| Citations + Authoritative Tone | Professional content, B2B, financial, legal |
| Easy Language + Statistics | Consumer content, health, education |
| Technical Terms + Citations | Academic, scientific, developer documentation |

---

## Answer Capsules

The single strongest citation trigger across all AI platforms. Required after every question-style H2 heading.

### Format

A self-contained paragraph of 40-60 words placed immediately after a question-style H2. The paragraph must answer the H2's question completely without needing any surrounding text.

### Requirements

1. **40-60 words** (count carefully)
2. **Self-contained:** Must make sense if quoted alone, without the heading or surrounding paragraphs
3. **Direct answer:** First sentence answers the question. No lead-in, no context-setting
4. **Placed immediately after the H2:** No other content between the heading and the capsule
5. **One per question-style H2:** Every H2 phrased as a question gets an answer capsule

### Example

**Good:**
```
## What Is Retrieval-Augmented Generation?

Retrieval-Augmented Generation (RAG) is an AI architecture that combines 
information retrieval with text generation to produce answers grounded in 
external data. Instead of relying only on training data, RAG systems search 
a knowledge base first, then generate responses using the retrieved 
documents as context. This reduces hallucinations by 30-50% compared to 
standalone LLMs (Lewis et al., 2020).
```

**Bad (not self-contained):**
```
## What Is Retrieval-Augmented Generation?

As mentioned earlier, this technique was introduced to solve a critical 
problem. It works by combining two approaches that we discussed in the 
previous section.
```

**Bad (too long, not a capsule):**
```
## What Is Retrieval-Augmented Generation?

[250-word paragraph that covers everything about RAG]
```

---

## Citation Density

### Target

2-3 sourced statistics per major section (H2 block). At minimum, every piece of content must include 5 sourced statistics total.

### Citation Format

Use inline citation format: "Claim (Source, Year)."

**Good examples:**
- "Email marketing generates $42 in revenue for every $1 spent (Litmus, 2023)."
- "53% of all website traffic comes from organic search (BrightEdge, 2024)."
- "RAG reduces LLM hallucinations by 30-50% (Lewis et al., 2020)."

**Bad examples:**
- "Studies show that email marketing is effective." (no source, no number)
- "Email marketing ROI is $42." (no source)
- "According to studies, most traffic comes from search." (vague, no number)
- "73% of marketers agree that..." (made-up statistic with no real source)

**CRITICAL: Never fabricate statistics.** Every number must come from a real source found via `WebSearch` or `WebFetch`. If you cannot find a real statistic to support a claim, use `[NEEDS DATA]` instead of inventing one. A paragraph without a statistic is always better than a paragraph with a fabricated one.

### Source Quality Hierarchy

Prefer sources in this order:
1. Peer-reviewed research papers
2. Official documentation and first-party data
3. Government and institutional data
4. Named industry reports (Gartner, Forrester, McKinsey, etc.)
5. Named expert statements from recognized authorities
6. Third-party review aggregators (G2, Capterra, etc.)

Avoid citing other blog posts as primary sources. Go to the original research.

### NEVER Cite Direct Competitors

**Absolute rule: Never cite, link to, quote from, or reference any direct competitor of the site you are generating content for.**

A direct competitor is any company or website that offers the same or a substantially similar product, service, or content to the same target audience. Citing a competitor sends link equity to a rival, signals to search engines that the competitor is an authority, and risks sending readers to a competing product.

**What to do instead:**
- Cite neutral third-party sources: research firms, analyst reports, academic papers, government data, trade publications
- Cite industry experts who are not affiliated with a competing product
- If a data point is only available from a competitor's site, search for the original research the competitor cited, or use a `[NEEDS DATA]` placeholder
- When comparing products (e.g., "[Product] vs [Competitor]" sections), state factual capabilities without linking to the competitor's site. Use neutral review platforms (G2, Capterra, Trustpilot) as sources for competitor data instead.

**How to identify competitors:** Before selecting citations, ask yourself: "Does this source offer a product or service that directly competes with the site I am writing for?" If yes, do not cite it. When in doubt, ask the user.

### Freshness

- **Always search the internet first.** Use `WebSearch` and `WebFetch` to find the most current data before writing. Never rely on training data alone when live search is available.
- Prefer data from the last 2 years
- If older data is the best available, note the year and add: "the most recent available data"
- Date all pricing and market data: "(as of March 2026)"
- When live research yields newer data than what you already know, always use the live data and cite the source URL

---

## Expert Quote Slots

### Target

At least 1 expert quote with full attribution per 500 words of content.

### Quote Format

Include the quote with: name, title/role, and organization.

**Good:**
```
"The companies seeing the biggest gains from AI are those that treat it 
as a tool for augmenting human expertise, not replacing it," says Sarah 
Chen, VP of Engineering at Anthropic.
```

**Bad:**
```
"AI is very useful for businesses." - Industry expert
```

### Quote Rules

1. Name the expert with their title and organization
2. The quote must add information, not just restate what the text already says
3. **NEVER fabricate quotes.** Every quote must come from a real, published source (interview, conference talk, blog post, press release, or official statement). Use `WebSearch` to find real quotes on the topic before writing.
4. **Verify the person is real.** The expert you quote must be a real person with a verifiable role at the named organization. Do not invent expert names or titles.
5. If real expert quotes are unavailable after searching, use direct statements from official sources (company blog posts, conference talks, published interviews). If no quotes can be found at all, omit the quote slot and flag it with `[NEEDS EXPERT QUOTE: topic]` for the user to fill.
6. Position quotes after a relevant data point or claim they support

---

## Extractability Rules

Every paragraph in the content should be extractable by AI systems. This means:

### Self-Contained Paragraphs

Each paragraph should make sense on its own. An AI system should be able to quote any single paragraph from your content without needing the paragraph before or after it.

**Test:** Cover up the paragraphs above and below. Does the paragraph still communicate a complete idea? If not, rewrite it.

### "X is Y that Z" Definitions

When defining any term, product, or concept, use this structure:

- **X** = the entity being defined (named in full)
- **Y** = the category or class it belongs to
- **Z** = its distinguishing characteristic or function

**Example:** "Perplexity is an AI search engine that combines real-time web search with large language model reasoning to generate cited answers."

### First 150 Words

The opening 150 words of every page are the most extracted, most quoted section. They must:

1. Directly answer the page's primary query
2. Include the primary keyword
3. Name the subject entity in full (never pronouns or abbreviations)
4. Include one sourced statistic
5. Be completely self-contained

### Structured Data Preference

AI systems extract structured data more reliably than prose. Use:

| Data Type | Use This | Not This |
|-----------|----------|----------|
| Comparisons | Tables | "X is better than Y because..." paragraphs |
| Processes | Numbered lists | "First you do X, then you do Y..." prose |
| Features | Bullet lists | Run-on feature paragraphs |
| Statistics | Tables or inline with source | Vague adjectives ("many", "most") |

---

## FAQ Section Optimization

FAQ sections have the highest AI citation rate of any content format when structured correctly.

### Rules

1. **Every page gets a FAQ section.** No exceptions.
2. **Minimum 3 questions, target 5-8** for articles and landing pages
3. **Each answer starts with a direct statement.** Never "It depends..." or "Great question!" or "Well..."
4. **Each answer is 2-4 sentences.** Self-contained.
5. **Each answer includes at least one specific data point** or named reference
6. **Questions must be real queries people search for.** Use Google "People Also Ask" as a source.
7. **Answers must stand alone.** They should make sense without reading the rest of the page.

### FAQPage Schema

Always pair the FAQ section with FAQPage JSON-LD schema. Include ALL questions from the section in the schema, not a subset.

---

## Platform-Specific Optimization

Different AI systems extract and cite content differently. Apply these tips during drafting:

### Google AI Overviews

- **Strongest signal:** E-E-A-T (Experience, Expertise, Authority, Trust)
- **Content format:** Short paragraphs, bullet points, tables. Prefers content that can be displayed directly in the overview.
- **Schema:** Structured data (FAQ, Article, HowTo) increases inclusion rates
- **Citation style:** Cites 3-8 sources per overview. Favors .edu, .gov, and recognized brands.
- **Action:** Include clear, quotable answer capsules. Use tables. Add author bios with credentials.

### ChatGPT (with browsing)

- **Strongest signal:** Domain authority and content-answer fit
- **Content format:** Uses inline citations [1], [2]. Pulls exact quotes when information is distinctive.
- **Freshness:** Content updated within 30 days gets 3.2x more citations
- **Domain preference:** Favors .edu/.gov/.org and sites with >350K referring domains
- **Action:** Make content uniquely quotable. Brand your definitions. Update content dates frequently.

### Perplexity

- **Strongest signal:** Semantic relevance and factual density
- **Content format:** Shows domain and publish date alongside citations. Cites 5-10 sources per answer.
- **Freshness:** Strongest freshness bias of any AI platform. Prioritizes recent content.
- **Schema preference:** FAQ Schema increases citation rates. PDF documents prioritized.
- **Action:** Use FAQ Schema. Date all content. Include high factual density (numbers, sources, specifics in every paragraph). Keep content updated.

### Claude

- **Strongest signal:** Factual density and structural clarity
- **Indexing:** Uses Brave Search, not Google. Ensure the site is indexed by Brave.
- **Content preference:** Data-rich content, clear hierarchies, authoritative definitions. Prefers well-established methodologies and consensus information.
- **Action:** Write data-dense paragraphs. Use clear heading hierarchies. Include authoritative, verifiable definitions.

### Microsoft Copilot

- **Strongest signal:** Bing index position
- **Indexing:** Requires Bing indexing (uses Bing as its search layer)
- **Ecosystem bonus:** LinkedIn, GitHub, and Microsoft ecosystem mentions help
- **Action:** Submit site to Bing Webmaster Tools. Mention relevant LinkedIn/GitHub profiles. Keep page speed under 2 seconds.

---

## Content Structure for Maximum AI Extraction

### Heading Hierarchy

```
H1: [Primary keyword in clear title]
  H2: [Question people search for]
    H3: [Subtopic if needed]
  H2: [Question people search for]
    H3: [Subtopic]
    H3: [Subtopic]
  H2: Frequently Asked Questions
    H3: [Question]
    H3: [Question]
```

Rules:
- One H1 per page
- H2s phrased as questions when possible
- No heading level skips (H1 > H3 is not allowed)
- Answer capsule immediately after each question-style H2

### Paragraph Structure

- 2-3 sentences per paragraph
- First sentence makes the key claim
- Second sentence provides evidence or data
- Third sentence (optional) adds context or implication

### List and Table Placement

- Place a comparison table near the top of the content (within the first 30% of the page)
- Use numbered lists for any sequential process
- Use bullet lists for non-sequential items (features, benefits, requirements)
- Never describe comparison data in prose when a table would work

---

## Common Mistakes to Avoid

1. **Writing the answer capsule as a teaser.** Bad: "There are many benefits to consider." Good: "RAG reduces hallucinations by 30-50% and grounds LLM responses in verified data (Lewis et al., 2020)."

2. **Burying the answer.** The answer to the page's primary query must appear in the first 150 words, not after 3 paragraphs of background.

3. **Unsourced statistics.** Every number needs a source. "67% of companies..." needs "(Source, Year)."

4. **Prose comparisons instead of tables.** "Product A is faster than Product B and cheaper than Product C" should be a table with specific numbers.

5. **Generic FAQ answers.** Each FAQ answer needs at least one specific data point or named reference.

6. **Keyword stuffing.** Using the primary keyword more than 3 times per 300 words actively decreases AI visibility (-9 to -10%). Write naturally.

7. **Missing FAQPage schema.** The FAQ section without JSON-LD schema loses 40% of its potential AI visibility boost.
