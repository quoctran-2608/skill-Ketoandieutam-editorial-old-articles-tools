# Kế Toán Diệu Tâm — Editorial HTML Transformation Specification v1.3.2

**Status:** Canonical  
**Applies to:** Legacy HTML → EDS v2.3.4 Inline Emphasis Hierarchy + Adaptive / Embedded Tables canonical HTML  
**Transformation mode:** FORMAT-ONLY SEMANTIC TRANSFORMATION  
**Canonical EDS reference:** `docs/21-content-editorial-design-system.md`

## 1. Objective

Convert heterogeneous legacy accounting/tax HTML into a small, stable semantic HTML vocabulary whose presentation is controlled centrally by the website's Editorial Design System.

The transformation layer must not become a writing, legal-updating or visual-design layer.

EDS v2.3.4 requires the transformer to:

- preserve meaningful title-like opening content without letting it corrupt body heading hierarchy;
- recover meaningful emphasis from legacy red/yellow/blue/green styling without preserving arbitrary colors;
- distinguish longer scan-worthy emphasis from shorter decisive highlight semantics;
- preserve source item boundaries and distinguish **peer-member lists** from genuine glossary/definition structures;
- preserve meaningful nested table row/column relationships instead of blindly flattening them.

## 2. Architectural boundary

```text
Legacy HTML + optional article metadata
    ↓
Opening-title classification / heading-tree analysis
    ↓
AI semantic transformation
    ↓
Canonical HTML
    ↓
sanitizeEditorialHtml()
    ↓
EDS v2.3.4 Inline Emphasis + Adaptive / Embedded Table CSS
    ↓
Preview
    ↓
Draft
    ↓
Human review
    ↓
Publish
```

The AI owns semantic classification and heading-tree normalization.

The sanitizer owns safety and class/tag validation.

CSS owns visual presentation, including typography, color, spacing, H2 accents, intro/emphasis/highlight paint, list rhythm, repeated-component tint rhythm and responsive behavior.

Human review owns final publication approval.

## 3. Transformation invariants

The following must remain unchanged unless the source markup itself prevents recovery:

- written facts;
- meaningful opening text;
- source item boundaries;
- label → description associations;
- meaningful table row/column associations;
- monetary values;
- account numbers;
- account names;
- Nợ/Có labels;
- legal names;
- legal document numbers;
- law/decree/circular references;
- dates;
- percentages;
- formulas;
- source URLs;
- image URLs;
- quoted text.

A title-like body block may be removed only when supplied masthead-title metadata confirms it is an **exact/no-information duplicate**. A probable title-root without metadata must be preserved as `ct-article-intro` when structurally appropriate.

Presentation-only list marker characters may be removed only when semantic list structure replaces them and they carry no lexical meaning beyond marking an item.

A nested table boundary may be removed only when its row/column placement carries no meaningful relationship.

## 4. Presentation must not leak into canonical HTML

Canonical output must not contain presentation decisions such as:

- font names, including Google Sans;
- font sizes or font weights chosen for appearance;
- Fresh Editorial color values or color utility classes;
- H2 gold accent markup;
- inline colors;
- legacy red/yellow/blue/green classes;
- pixel widths for layout;
- arbitrary left margins;
- box shadows;
- background color utilities;
- custom component IDs;
- ad hoc visual classes;
- manually encoded A/B tint variants.

The canonical HTML expresses meaning. EDS CSS renders the current visual system.

`ct-article-intro`, `ct-key-emphasis`, `ct-key-highlight`, `ct-source-note` and `ct-key-line.is-result` are semantic vocabulary, not permission to copy legacy paint.

A nested `table.ct-data-table.is-simple` may be retained when the source column relationship itself is meaningful. Its responsive side-by-side/stacked behavior remains CSS-owned.

## 5. Canonical classification matrix

| Source meaning | Canonical semantic |
|---|---|
| Normal prose | `p` |
| Meaningful title-like opening scope/context | `p.ct-article-intro` |
| Major body section | `h2` |
| Subsection | `h3` |
| Local sub-subsection | `h4` |
| Ordinary local emphasis | `strong` |
| Longer scan-worthy clause/list-like phrase | `span.ct-key-emphasis` |
| Decisive short condition/exception/threshold | `mark.ct-key-highlight` |
| Short attached legal/source attribution | `p.ct-source-note` |
| Ordinary grouped items | `ul` / `ol` |
| Declared family of sibling members with label + explanation | `ul > li > strong + text` |
| Checklist/requirements | `.ct-checklist` |
| Ordered procedure | `.ct-steps` |
| Main insight/principle | `.ct-content-box.is-note` |
| Neutral additional info | `.ct-content-box.is-info` |
| Risk/error/penalty | `.ct-content-box.is-warning` |
| Legal basis | `.ct-content-box.is-legal` |
| Practical example | `.ct-content-box.is-example` |
| Compact formula | `.ct-key-line.is-formula` |
| Final resolved answer/conclusion | `.ct-key-line.is-result` |
| Compact process | `.ct-key-line.is-process` |
| Journal entry | `.ct-accounting-entry` |
| Related journal entries | `.ct-accounting-group` |
| Genuine glossary term/concept → definition | `.ct-definition-list` |
| Key → short value | `.ct-fact-list` |
| Simple data table | `.ct-data-table.is-simple` |
| Dense data table | `.ct-data-table.is-complex` |
| Meaningful 1-row nested support relation | nested `.ct-data-table.is-simple` |
| Genuine quote | `blockquote` |
| Editorial image | `.ct-editorial-media` |
| Genuine Q&A | `.ct-faq` |
| Explicit related resource | `.ct-related-content` |

## 6. Decision precedence

When multiple components seem possible, use this order:

1. Is the first source heading an article-title root, and if so must its text be removed or preserved as intro?
2. What is the true body heading tree after separating title-root structure from opening-text preservation?
3. Does source have an established semantic structure already?
4. What is content's actual communicative function?
5. Is the block a **peer-member enumeration** that should remain a normal list before considering `dl`?
6. If a table is nested, do its row/column boundaries encode a meaningful association before any flattening decision?
7. Can normal prose/`strong`/list/table represent it without losing meaning?
8. If source uses visual emphasis, is there a meaningful emphasis role that should survive after color is stripped?
9. Use a special component only if it adds semantic clarity.
10. If still ambiguous, choose simpler structure, preserve content/item/cell relationships and report ambiguity.

## 7. Title-like first block and heading rebasing

The article masthead owns H1. Canonical body starts from H2.

Legacy content may include a title-like `h1` or `h2` as its first meaningful block even though the CMS/page stores the article title separately. This root must not cause real major sections to be emitted as H3.

**Structural title-root detection and visible-text preservation are separate decisions.**

### 7.1 Metadata comparison

When article title metadata is supplied, compare it with first meaningful body `h1`/`h2` using conservative normalization only:

- decode HTML entities;
- strip presentation-only tags;
- trim/collapse whitespace;
- ignore insignificant case/punctuation differences.

Do not rewrite words, remove substantive phrases or use semantic paraphrase to manufacture a match.

### 7.2 Metadata-confirmed exact/no-information duplicate

If first title-like body heading is fully represented by masthead title and contains no additional meaningful scope/context:

1. remove that body heading;
2. record it under **Removed**;
3. determine whether it acted as root of body heading tree;
4. rebase descendants so actual major sections start at H2.

This is the only automatic title-text deletion case.

### 7.3 Metadata available but body title adds meaning

If first title-like block overlaps masthead title but contains additional scope, objects, conditions, examples or description:

1. preserve complete source visible text as `p.ct-article-intro`;
2. do not summarize/shorten/rewrite it;
3. separately repair descendant heading levels.

### 7.4 High-confidence fallback without title metadata

A first H1/H2 may be classified as probable title-root without metadata only if pattern is strong, such as all/most of:

- first meaningful body block;
- broad title-like wording;
- followed by introductory lead/prose;
- next headings exactly one level deeper;
- multiple peer major sections at that deeper level, commonly numbered `1.`, `2.`, `3.`;
- no peer section exists at same source level as candidate root.

If high-confidence:

1. **preserve text as `p.ct-article-intro`**;
2. rebase descendants;
3. add **Needs review** because masthead metadata did not confirm classification.

Do not remove probable title-root text when metadata is absent.

### 7.5 Rebase mapping

If title-root = source H1:

```text
source H2 → canonical H2
source H3 → canonical H3
source H4 → canonical H4
```

If title-root = source H2 and owns article tree:

```text
source H3 → canonical H2
source H4 → canonical H3
```

Never emit body H1. Never promote above H2.

Do not blindly decrement every heading in malformed document. Rebase only subtree structurally nested under title-root; independent heading trees must be analyzed separately.

### 7.6 Example pattern

Legacy:

```html
<h2>Hướng dẫn cách tính nguyên giá TSCĐ hữu hình, gồm mua sắm, xây dựng, sản xuất...</h2>
<p>Phần giới thiệu...</p>
<h3>1. TSCĐ hữu hình mua sắm</h3>
<h4>Nguyên tắc xác định</h4>
<h3>2. TSCĐ tự xây dựng hoặc tự sản xuất</h3>
```

Without masthead metadata, canonical:

```html
<p class="ct-article-intro">Hướng dẫn cách tính nguyên giá TSCĐ hữu hình, gồm mua sắm, xây dựng, sản xuất...</p>
<p>Phần giới thiệu...</p>
<h2>1. TSCĐ hữu hình mua sắm</h2>
<h3>Nguyên tắc xác định</h3>
<h2>2. TSCĐ tự xây dựng hoặc tự sản xuất</h2>
```

The opening text remains. Only its heading-root role is removed.

## 8. Legacy faux headings

Common legacy patterns:

```html
<p><strong>I. PHẠM VI ÁP DỤNG</strong></p>
<p style="font-size:18px"><b>Hạch toán tài khoản 642</b></p>
<div><span style="font-weight:bold">Ví dụ</span></div>
```

Only convert to H2/H3/H4 when text clearly marks article hierarchy.

Do not promote every bold sentence to heading.

Do not add visual markup for H2 gold signature; CSS owns treatment.

Legacy blue/green text or colored backgrounds are not sufficient evidence for heading status.

## 9. Legacy indentation

Indented text does not automatically imply nested semantics.

Example:

```html
<p style="margin-left:40px">Nợ TK 642...</p>
<p style="margin-left:40px">Có TK 111...</p>
```

If content clearly represents a journal entry, transform semantically to accounting entry.

If several indented paragraphs are sibling members under a lead such as “có N tài khoản cấp 2”, classify them as a normal peer list.

Otherwise remove indentation and preserve prose.

## 10. Accounting transformation

### Single entry

```html
<div class="ct-accounting-entry">
  <p class="ct-accounting-entry__title">Định khoản</p>
  ...
</div>
```

### Line

```html
<div class="ct-accounting-entry__line is-debit">
  <strong class="ct-accounting-entry__side">Nợ</strong>
  <span>...</span>
</div>
```

```html
<div class="ct-accounting-entry__line is-credit">
  <strong class="ct-accounting-entry__side">Có</strong>
  <span>...</span>
</div>
```

### Neutral

```html
<div class="ct-accounting-entry__line">
  <strong class="ct-accounting-entry__side">...</strong>
  <span>...</span>
</div>
```

Use neutral only when debit/credit is not explicit.

### Multiple entries

Use:

```html
<section class="ct-accounting-group">
```

only when entries form a coherent accounting treatment.

## 11. Legal content

Use `.is-legal` when source primarily presents:

- statutory basis;
- quoted legal provision;
- official rule;
- circular/decree/law reference tied directly to point.

Do not automatically put every sentence containing “Thông tư”, “Nghị định” or “Luật” into legal box.

A short attached attribution such as `(Theo Khoản 1 Điều 4 Thông tư...)` is usually `p.ct-source-note`, not full legal box.

Context determines semantic function.

## 12. Warning content

Use `.is-warning` only when content warns about:

- tax/compliance risk;
- penalty exposure;
- easily misunderstood requirement;
- common accounting mistake;
- invalid treatment;
- deadline/risk condition.

Do not use Warning merely because legacy text is red.

## 13. Example content

Use `.is-example` only when content contains real example, scenario, calculation or case.

Legacy green/yellow boxes do not automatically become examples.

## 14. Key insight

Use `.is-note` for conclusions or principles that materially help reader understand section.

Do not use it for introductory decoration.

## 15. Semantic emphasis recovery from legacy colors

Legacy articles often encode hierarchy through presentation:

```html
<span style="color:red">...</span>
<span style="background:#ffff99">...</span>
<span style="background:#f0ffff">...</span>
<span style="color:#4472c4">...</span>
```

Transformation rule:

> **Color is evidence to inspect, not meaning to preserve.**

Use smallest semantic level that keeps intended importance:

1. ordinary importance → `strong`;
2. longer scan-worthy clause/list-like phrase → `span.ct-key-emphasis`;
3. short decisive condition/exception/threshold/scope → `mark.ct-key-highlight`;
4. compact calculation → `.ct-key-line.is-formula`;
5. resolved output/conclusion → `.ct-key-line.is-result`;
6. whole-block risk → `.ct-content-box.is-warning`;
7. whole-block legal basis → `.ct-content-box.is-legal`;
8. whole-block principle → `.ct-content-box.is-note`.

Never create red/yellow/blue highlight variants.

### 15.1 `ct-key-emphasis`

Use for a longer phrase/clause/list-like phrase where:

- source meaningfully emphasizes it;
- readers benefit from quick scanning;
- `strong` would flatten hierarchy;
- background highlight would be too heavy for length;
- it is not a whole formula/result/callout.

Example:

```html
<span class="ct-key-emphasis">lãi tiền vay ...; chi phí vận chuyển, bốc dỡ; chi phí nâng cấp; chi phí lắp đặt, chạy thử; lệ phí trước bạ...</span>
```

Do not map every red span here.

### 15.2 `ct-key-highlight`

Use only for short inline phrase where losing prominence could cause reader to miss decisive condition.

Good pattern:

```html
<p>Nguyên giá bao gồm các chi phí <mark class="ct-key-highlight">tính đến thời điểm tài sản ở trạng thái sẵn sàng sử dụng</mark>.</p>
```

Do not mark full paragraphs or long lists.

### 15.3 Overlap

Avoid nesting `ct-key-emphasis` and `ct-key-highlight`. Split ranges where practical so each semantic owns its own text.

### 15.4 `ct-source-note`

Use for short explicit source attribution attached to nearby content:

```html
<p class="ct-source-note">Theo Khoản 1 Điều 4 Thông tư 45/2013/TT-BTC</p>
```

Do not invent/update citation text.

### 15.5 `is-result`

Use for answer/result resolving preceding formula/example/decision path:

```html
<p class="ct-key-line is-result"><strong>Nguyên giá chính thức: 8.700.000.000 đồng</strong></p>
```

A paragraph containing amount is not automatically a result.

## 16. Peer lists vs definition/fact structures

### 16.1 Peer-member list — first check

Before creating any `dl`, ask whether the source is simply enumerating sibling members in one declared family.

Strong signals:

- lead says “có N tài khoản cấp 2”;
- “gồm các loại / nhóm / trường hợp / khoản”;
- several adjacent items share the same grammatical shape;
- each item is a member/category, not a term being taught as a concept;
- source uses repeated indented paragraphs or hyphen-prefixed paragraphs.

Canonical:

```html
<ul>
  <li><strong>Tài khoản 2141 - ...:</strong> Phản ánh...</li>
  <li><strong>Tài khoản 2142 - ...:</strong> Phản ánh...</li>
</ul>
```

Preserve item order and label-description pairing. Strip a source `-`/`•` only when it is purely a visual list marker replaced by semantic `<li>`.

### 16.2 Definition list

Use `.ct-definition-list` only when terms function as genuine concepts/definitions, for example:

```text
Khấu hao → định nghĩa...
Giá trị còn lại → định nghĩa...
```

A repeated `strong label + explanation` pattern is **not sufficient** evidence for Definition List.

Do not classify a child-account enumeration as Definition List merely because each account label is followed by a description.

### 16.3 Fact list

Use `.ct-fact-list` for concise metadata/factual attributes such as document number, date, authority, status or effective date.

If values become narrative, prefer normal prose/list or genuine Definition List depending on meaning.

If list-vs-definition is ambiguous, prefer normal `ul/li` or prose and report review.

## 17. Table classification heuristic

Prefer `is-simple` if:

- 2–3 columns;
- short headers;
- readable within normal prose width;
- no complex spanning.

Prefer `is-complex` if any are true:

- 4+ columns;
- dense numeric matrix;
- long headers;
- `rowspan` / `colspan`;
- accounting/tax comparison matrix;
- natural minimum width exceeds reading lane;
- 2–3 columns but cells contain dense multi-paragraph comparison content.

Never classify based solely on legacy pixel width.

## 18. Table integrity and nested-table preservation

Do not:

- merge cells unless source does;
- split source cells to “improve” readability;
- change data order;
- reformat values in a way that changes meaning;
- delete empty cells if they carry structural meaning;
- flatten nested tables before checking whether their cell boundaries carry meaning.

### 18.1 Nested-table decision test

For each nested table inside a `td`/`th`, ask:

> If I remove these row/column boundaries, will the reader lose a relationship between a primary block and its note/basis/value, or between two peer cell groups?

If yes, preserve the nested relationship.

### 18.2 Embedded support table

A common case is one row with 2–3 cells and no independent header, where one cell contains an accounting/value block and another cell contains an explanation.

Example source meaning:

```text
Nợ TK 632
Có TK 156
       ↔
Theo PP tính giá xuất kho mà DN áp dụng
```

Canonical:

```html
<table class="ct-data-table is-simple">
  <tbody>
    <tr>
      <td>
        <p>Nợ TK 632</p>
        <p>Có TK 156</p>
      </td>
      <td>
        <p>Theo PP tính giá xuất kho mà DN áp dụng</p>
      </td>
    </tr>
  </tbody>
</table>
```

When embedded directly in a parent table cell:

- keep it nested;
- do not add `.ct-table-scroll` around it;
- strip legacy width/height/border/cellpadding/cellspacing/style attributes;
- preserve cell order and visible text;
- preserve Nợ/Có wording exactly;
- do not convert the explanatory cell into a later unrelated paragraph;
- CSS owns desktop side-by-side and mobile stacking.

### 18.3 Safe flattening cases

Flatten/unwrap only when the nested table is presentation-only, for example:

- one-cell wrapper around prose;
- spacer/alignment cells;
- empty companion cells;
- cells whose separation carries no communicative meaning.

When flattening, preserve block order and item boundaries.

### 18.4 Genuine nested data matrix

If the nested table is itself real tabular data with multiple meaningful rows/headers, preserve semantic table structure if no simpler representation can retain all relationships. Flag **Needs review** if responsive behavior is uncertain.

Visual inconvenience is not enough reason to destroy source structure.

## 19. Links and references

Preserve exact existing `href` when safe.

Do not:

- resolve relative URL by guessing;
- replace source links with modern equivalents;
- add internal SEO links;
- add CTA links.

SEO linking belongs to different workflow.

## 20. Images

Do not download, upload, rehost or replace images during transformation.

Only normalize HTML structure around existing image references.

## 21. Empty and redundant markup

Safe to remove:

```html
<span></span>
<p>&nbsp;</p>
<div></div>
```

when they contain no meaningful content and do not preserve required table/list structure.

Be conservative around intentionally blank table cells and nested support-table cells.

After removal/unwrapping, serialize canonical HTML without consecutive blank physical lines. Adjacent block elements separated by at most one newline unless meaningful whitespace is part of `pre`/code-like content.

## 22. Duplicate content

Do not automatically delete duplicate-looking factual paragraphs.

The narrow title exception is only section 7.2: masthead metadata must confirm exact/no-information duplication.

If other duplication is exact and obviously caused by markup duplication, report for review rather than silently deleting.

## 23. Unsupported legacy components

If source contains a presentation widget with no canonical semantic equivalent:

- unwrap it;
- preserve meaningful text;
- preserve safe links/images;
- preserve meaningful row/column associations when the widget contains tabular grouping;
- report removed widget under **Removed**.

Do not create new EDS class for one article.

## 24. Semantic confidence

Use three implicit confidence levels:

### High
Structure/meaning explicit, or exact title duplicate confirmed by supplied metadata.

→ transform directly.

### Medium
Semantic function strongly implied.

→ transform conservatively.

### Low
Meaning, emphasis role, peer-list-vs-definition role, nested-table role or title-root status ambiguous.

→ preserve with simpler canonical markup and add **Needs review**.

For ambiguous opening title without metadata, preserve as `ct-article-intro` when it is high-confidence title-root. For ambiguous legacy highlight, prefer plain prose/`strong`/`ct-key-emphasis` over inventing decisive `ct-key-highlight`. For ambiguous list-vs-definition, prefer normal list/prose over `dl`. For ambiguous nested tables, preserve cell relationships when flattening could lose meaning.

## 25. Output purity

Canonical HTML section must contain no:

- markdown fences when machine consumption requires raw HTML;
- explanatory prose mixed into HTML;
- review notes as HTML comments;
- temporary classes;
- TODO comments;
- AI annotations;
- visual implementation details copied from EDS docs.

QA notes belong outside HTML.

## 26. Bulk-migration readiness

Before bulk use, validate against at least:

- metadata-confirmed exact duplicate body-title articles;
- title-like first block with extra scope/context;
- title-like first block without metadata;
- shifted-heading articles;
- difficult accounting-entry articles;
- **child-account / peer-member list articles**;
- heavy legacy font/span articles;
- emphasis-heavy red/yellow/cyan legacy articles;
- large tables;
- dense 2-column comparison tables;
- meaningful nested 1-row support tables;
- genuine nested data matrices;
- legal-heavy articles;
- mixed image/table articles;
- nested list articles;
- relative-link articles;
- repeated callouts.

Recommended gate: 20–30 difficult legacy articles before full corpus migration.

## 27. Versioning

Changes that add/remove canonical classes/tags require spec version review.

Suggested policy:

- `1.3.x` — clarifications and classification corrections that keep the same canonical vocabulary;
- `1.x` — compatible semantic/heading-normalization additions;
- `2.0` — vocabulary/output-contract breaking change.

EDS palette, typography, spacing or decorative refinements alone do **not** require semantic transformation version changes as long as canonical vocabulary/meaning remain unchanged.

v1.1 added title-root/rebase normalization.

v1.2 added `mark.ct-key-highlight`, `p.ct-source-note` and `.ct-key-line.is-result`.

v1.3 added `p.ct-article-intro` and `span.ct-key-emphasis`, and changed title-root behavior from probability-based deletion to preservation-by-default unless exact duplication is metadata-confirmed.

v1.3.1 clarifies **peer-member list precedence**: sibling account/category/type enumerations use normal `ul/li` by default; `.ct-definition-list` is reserved for genuine glossary/term-definition semantics.

v1.3.2 adds **nested-table relationship preservation** without adding vocabulary: meaningful nested support tables remain nested `ct-data-table.is-simple`; presentation-only nested wrappers may still be flattened.

Do not silently change transformation behavior without version/update fixtures.
