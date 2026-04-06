# Content Quality Checklist

Run every piece of generated content through this checklist before delivering it. Present the results to the user as a scored validation report.

---

## How to Use

1. Complete all content generation steps first
2. Go through each section below, marking each item as Pass, Partial, or Fail
3. Calculate scores per section and overall
4. Fix any Fail items before delivering
5. Present the validation report to the user

---

## 1. SEO Checks

| # | Check | Pass | Fail |
|---|-------|------|------|
| 1.1 | H1 contains the primary keyword | Keyword present naturally | Keyword missing or forced |
| 1.2 | Only one H1 per page | Single H1 | Multiple H1s or no H1 |
| 1.3 | Heading hierarchy: H1 > H2 > H3, no skipped levels | Correct hierarchy | H1 > H3 skip or other violations |
| 1.4 | Meta title is STRICTLY 50-60 characters (must be >=50 and <60) | 50-59 characters, keyword near start. Count every character including spaces, pipes, and brand name. | Under 50, 60 or more, or keyword missing |
| 1.5 | Meta description is STRICTLY 140-160 characters (must be >=140 and <=160) | 140-160 characters, includes keyword and CTA. Count every character including spaces and punctuation. | Under 140, over 160, or generic |
| 1.6 | Primary keyword appears in first 150 words | Present naturally | Missing or forced |
| 1.7 | Primary keyword density is 0.5-2.5% | Within range | Under 0.5% or over 2.5% |
| 1.8 | Secondary keywords appear in H2 headings | 2-3 secondary keywords in H2s | No secondary keywords in headings |
| 1.9 | Internal linking suggestions provided | 3-5 outbound + 3-5 inbound suggestions | No linking suggestions |
| 1.10 | Open Graph tags generated | Title, description, image, URL, type | Missing or incomplete |
| 1.11 | Twitter Card tags generated | Card type, title, description, image | Missing or incomplete |
| 1.12 | Image alt text suggestions included | Descriptive alt text for key images | No alt text guidance |

---

## 2. GEO Checks (AI Visibility)

| # | Check | Pass | Fail |
|---|-------|------|------|
| 2.1 | Answer capsule after every question-style H2 | 40-60 words, self-contained, immediate | Missing, too long/short, or not self-contained |
| 2.2 | First 150 words directly answer the primary query | Answer is immediate, no preamble | Answer buried after background text |
| 2.3 | Citation density: 2-3 sourced stats per major section | Format: "Claim (Source, Year)" | Unsourced numbers or no statistics |
| 2.4 | Total sourced statistics: minimum 5 in the piece | 5+ stats with named sources and dates | Fewer than 5, or sources unnamed |
| 2.5 | Expert quotes: 1 per 500 words minimum | Named expert, title, organization | No quotes, or quotes without attribution |
| 2.6 | Tables used for comparison data | Structured tables, not prose comparisons | Comparisons described in paragraphs |
| 2.7 | Numbered lists for processes/sequences | Ordered lists for step-by-step content | Steps described in prose |
| 2.8 | Definitions use "X is Y that Z" format | Entity named, categorized, differentiated | Vague or roundabout definitions |
| 2.9 | FAQ section present | 3-8 questions with self-contained answers | Missing or fewer than 3 questions |
| 2.10 | FAQ answers start with direct statements | No "It depends" or "Great question" | Evasive or preamble-heavy answers |
| 2.11 | FAQ answers include specific data points | Each answer has a number or named reference | Generic answers without data |
| 2.12 | Every paragraph is self-contained | Can be quoted without surrounding context | Paragraphs depend on previous text |
| 2.13 | Live internet research was performed | WebSearch/WebFetch used to gather latest data, stats, and developments on the topic before writing | Content written from training data alone without live research |
| 2.14 | Zero citations to direct competitors | No links, citations, quotes, or references to any site that directly competes with the site being written for | Any citation or link pointing to a direct competitor's website or content |

---

## 3. Writing Quality Checks

| # | Check | Pass | Fail |
|---|-------|------|------|
| 3.1 | Zero em dashes in the entire output | No `--` or `—` anywhere | Any em dash present |
| 3.2 | Zero AI-tell verbs | None of: delve, leverage, utilize, foster, bolster, streamline, enhance, endeavour, ascertain, elucidate | Any banned verb present |
| 3.3 | Zero AI-tell adjectives | None of: robust, comprehensive, pivotal, seamless, holistic, cutting-edge, groundbreaking, transformative, innovative, intricate, nuanced, multifaceted | Any banned adjective present |
| 3.4 | No banned opening phrases | Does not start with "In today's...", "In an era of...", "In the ever-evolving..." | Opens with a banned phrase |
| 3.5 | No banned transitional phrases | None of: "That being said", "It's worth noting", "At its core", "Let's delve into" | Any banned transition present |
| 3.6 | No banned closing phrases | Does not end with "In conclusion...", "To sum up...", "All things considered..." | Ends with a banned closing |
| 3.7 | All paragraphs are 2-3 sentences | No paragraph exceeds 3 sentences | Any 4+ sentence paragraph |
| 3.8 | Sentence length varies | No 3+ consecutive sentences of similar word count | Monotonous sentence rhythm |
| 3.9 | No filler words without purpose | Filler words (basically, essentially, actually, obviously, etc.) removed or justified | Multiple purposeless filler words |
| 3.10 | Content reads like human writing | Passes the "read aloud" test, sounds natural | Sounds robotic or corporate |
| 3.11 | No banned structural patterns | No "Whether you're a [X], [Y], or [Z]..." or "By [gerund], you can..." | Banned patterns present |
| 3.12 | ZERO fabricated facts | Every statistic has a real, named source found via live research. Every expert quote is from a real person who actually said it. Every data point is verifiable. No invented numbers, names, studies, or claims. | Any statistic without a real source, any invented quote or expert name, any made-up data point |

---

## 4. Regional English Checks

| # | Check | Pass | Fail |
|---|-------|------|------|
| 4.1 | Dialect identified and stated | Dialect declared (American/British/Australian/Canadian) | No dialect identified |
| 4.2 | Spelling consistency | All regional spellings match (-ise/-ize, -our/-or, -re/-er) | Mixed spelling dialects |
| 4.3 | Vocabulary consistency | Regional vocabulary used (holiday/vacation, mobile/cell phone, etc.) | Vocabulary mismatch |
| 4.4 | Date format matches dialect | MM/DD/YYYY (US), DD/MM/YYYY (UK/AU), YYYY-MM-DD (CA/technical) | Wrong date format |
| 4.5 | Currency format matches | Correct currency symbol and format | Wrong currency or format |
| 4.6 | Measurement units match | Imperial (US) or metric (UK/AU/CA) as appropriate | Wrong measurement system |

---

## 5. Schema Checks

| # | Check | Pass | Fail |
|---|-------|------|------|
| 5.1 | Primary schema type matches content type | Correct @type for the page (Article, Product, etc.) | Wrong or missing schema type |
| 5.2 | FAQPage schema includes ALL FAQ questions | Every FAQ question from the content is in the schema | Subset or missing FAQPage schema |
| 5.3 | SpeakableSpecification included | Targets H1, answer capsules, FAQ answers | Missing or targets wrong elements |
| 5.4 | datePublished present | Valid date in ISO format | Missing |
| 5.5 | dateModified present | Valid date in ISO format | Missing |
| 5.6 | Author information present | Name, title, organization included | Anonymous or missing |
| 5.7 | Schemas combined with @graph | Single script tag with @graph array | Multiple separate script tags |
| 5.8 | JSON-LD is syntactically valid | Valid JSON, no trailing commas or syntax errors | Invalid JSON |

---

## 6. AI Citation Score Estimate

Quick estimate of how likely AI systems are to cite this content. Score each dimension 0-10.

| Dimension | What to Check | Score |
|-----------|--------------|-------|
| **Extractability** | Can AI pull a useful answer from the first 150 words? Are paragraphs self-contained? Are tables/lists used for data? | /10 |
| **Quotability** | Do claims have specific numbers with sources? Are definitions clear ("X is Y that Z")? Are comparisons in tables? | /10 |
| **Authority** | Is an author identified with credentials? Are expert quotes included? Are primary sources cited (not blogs)? | /10 |
| **Freshness** | Is datePublished set? Are statistics from the last 2 years? Is pricing dated? | /10 |
| **Entity Clarity** | Is the subject entity named in full in the opening? Is Organization schema present with sameAs? Is the brand name consistent? | /10 |

**AI Citation Score: [average of all 5 dimensions]/10**

| Score | Rating | Interpretation |
|-------|--------|---------------|
| 8-10 | Strong | Content is well-positioned for AI citations |
| 5-7 | Moderate | Address weak dimensions before publishing |
| 3-4 | Weak | Major structural improvements needed |
| 0-2 | Critical | Fundamental issues, likely will not be cited |

---

## 7. Competitor Outranking Checks

Only score this section when competitor URLs were provided and analyzed. If no competitor analysis was performed, skip this section entirely.

| # | Check | Pass | Fail |
|---|-------|------|------|
| 7.1 | Covers every topic the competitor covers | All competitor H2 topics addressed in your content | One or more competitor topics missing |
| 7.2 | Includes more sourced statistics | Your stat count exceeds the best competitor's by 3+ | Fewer or equal sourced statistics |
| 7.3 | Includes more expert quotes | Your quote count exceeds the best competitor's by 1+ | Fewer or equal attributed quotes |
| 7.4 | Stronger first 150 words | Opening delivers a more direct, data-backed answer than competitor's opening | Opening is weaker, vaguer, or lacks data |
| 7.5 | More FAQ questions | FAQ covers all competitor FAQ questions plus 2-3 additional | Fewer FAQ questions than the best competitor |
| 7.6 | Better schema markup | Includes all competitor schema types plus additional appropriate types | Missing schema types the competitor uses |
| 7.7 | Fresher data | Statistics are from more recent sources than competitor's | Older or same-age data as competitor |
| 7.8 | More structured data elements | More tables, numbered lists, and bullet lists than competitor | Fewer structured elements; data left in prose |
| 7.9 | Content gaps filled | Every gap identified in the competitor analysis is addressed | One or more identified gaps remain unfilled |

---

## Validation Report Template

Present the validation results in this format:

```markdown
## Content Validation Report

### SEO Checks: [X/12 passed]
- [x] H1 contains primary keyword
- [x] Single H1 per page
- [x] Heading hierarchy correct
- [x] Meta title: [XX] chars (STRICT: must be >=50 and <60)
- [x] Meta description: [XX] chars (STRICT: must be >=140 and <=160)
- [x] Primary keyword in first 150 words
- [x] Keyword density: [X.X]%
- [x] Secondary keywords in H2s
- [x] Internal linking suggestions provided
- [x] Open Graph tags complete
- [x] Twitter Card tags complete
- [x] Image alt text guidance included

### GEO Checks: [X/14 passed]
- [x] Answer capsule after every question-style H2
- [x] First 150 words answer the primary query directly
- [x] Citation density: [X] sourced stats per section
- [x] Total sourced statistics: [X] (minimum 5)
- [x] Expert quotes: [X] (1 per 500 words target)
- [x] Tables used for comparisons
- [x] Numbered lists for processes
- [x] "X is Y that Z" definitions
- [x] FAQ section: [X] questions
- [x] FAQ answers start with direct statements
- [x] FAQ answers include data points
- [x] All paragraphs self-contained
- [x] Live internet research performed for latest data
- [x] Zero citations to direct competitors

### Writing Quality: [X/12 passed]
- [x] Zero em dashes
- [x] Zero AI-tell verbs
- [x] Zero AI-tell adjectives
- [x] No banned opening phrases
- [x] No banned transitional phrases
- [x] No banned closing phrases
- [x] All paragraphs 2-3 sentences
- [x] Sentence length varied
- [x] No purposeless filler words
- [x] Reads as human-written
- [x] No banned structural patterns
- [x] Zero fabricated facts: every stat, quote, and data point verified from real sources

### Regional English: [X/6 passed]
- [x] Dialect: [American/British/Australian/Canadian]
- [x] Spelling consistent
- [x] Vocabulary consistent
- [x] Date format matches
- [x] Currency format matches
- [x] Measurement units match

### Schema: [X/8 passed]
- [x] Primary schema type correct
- [x] FAQPage schema complete
- [x] SpeakableSpecification included
- [x] datePublished present
- [x] dateModified present
- [x] Author information present
- [x] @graph structure used
- [x] JSON-LD syntax valid

### AI Citation Score Estimate: [X]/10
| Dimension | Score |
|-----------|-------|
| Extractability | [X]/10 |
| Quotability | [X]/10 |
| Authority | [X]/10 |
| Freshness | [X]/10 |
| Entity Clarity | [X]/10 |

### Competitor Outranking: [X/9 passed] (if competitor URLs provided)
- [x] All competitor topics covered
- [x] More sourced statistics: [yours] vs [competitor's best]
- [x] More expert quotes: [yours] vs [competitor's best]
- [x] Stronger first 150 words
- [x] More FAQ questions: [yours] vs [competitor's best]
- [x] Better schema markup
- [x] Fresher data
- [x] More structured data elements: [yours] vs [competitor's best]
- [x] All [X] identified gaps filled

### Issues to Address
1. [Any failed items with specific fix instructions]
```

---

## Priority of Fixes

If time or effort is limited, fix items in this order:

**P0 (fix before publishing):**
- Fabricated facts present (check 3.12) -- any invented statistic, fake quote, or made-up data point must be removed or replaced with verified data before publishing
- Em dashes present (check 3.1)
- AI-tell words present (checks 3.2, 3.3)
- Missing FAQ section (check 2.9)
- No answer capsules (check 2.1)
- First 150 words do not answer the query (check 2.2)
- Schema missing or invalid (checks 5.1, 5.2, 5.8)

**P1 (fix soon):**
- Citations pointing to direct competitors (check 2.14) -- replace with neutral third-party sources
- No live internet research performed (check 2.13)
- Unsourced statistics (check 2.3)
- Missing expert quotes (check 2.5)
- Prose comparisons instead of tables (check 2.6)
- Paragraphs too long (check 3.7)
- Regional English inconsistencies (section 4)
- Competitor topics not fully covered (check 7.1, if competitor analysis was performed)
- Content gaps from competitor analysis remain unfilled (check 7.9, if competitor analysis was performed)

**P2 (improve when possible):**
- Sentence variety (check 3.8)
- Filler words (check 3.9)
- Internal linking suggestions (check 1.9)
- Image alt text (check 1.12)
