# KTD Editorial HTML Transform Skill

**Skill name:** `ktd-editorial-html-transform`  
**Project:** Kế Toán Diệu Tâm  
**Version:** 1.3.2  
**Status:** Canonical transformation skill  
**Mode:** FORMAT-ONLY SEMANTIC TRANSFORMATION

## 1. Purpose

Transform legacy accounting/tax HTML into canonical semantic HTML compatible with the Kế Toán Diệu Tâm Editorial Design System (**EDS v2.3.4 — Inline Emphasis Hierarchy + Adaptive / Embedded Tables**) and the editorial sanitizer.

This skill is for **presentation and semantic normalization only**.

It must preserve the source article's factual content, meaningful visible text, item boundaries, cross-column relationships and meaning.

### Canonical references

Use these sources in this order when transformation behavior or presentation ownership is unclear:

1. `docs/21-content-editorial-design-system.md` — canonical EDS v2.3.4 visual + semantic reference;
2. `transformation-spec.md` — transformation boundary and classification rules;
3. `canonical-examples.md` — canonical markup examples;
4. `qa-checklist.md` — completion gate.

The skill owns semantic HTML decisions only. It must **not** encode Google Sans, Fresh Editorial colors, H2 gold accents, highlight colors, spacing, shadows, widths or other visual presentation into article HTML. Those belong to EDS CSS.

## 2. Primary rule

> Nội dung quyết định semantic.  
> Semantic quyết định component.  
> Component quyết định họ màu.  
> Vị trí lặp quyết định sắc độ.  
> Hierarchy quyết định cường độ.  
> CSS quyết định presentation.  
> HTML không tự trang trí.  
> Không xóa nội dung có nghĩa chỉ để sửa hierarchy.  
> Không đổi một danh sách peer-items thành glossary chỉ vì mỗi item có label đậm.  
> Không flatten nested table nếu quan hệ giữa các cột mang nghĩa.

The transformer decides **what the content means structurally**, not how it should look visually.

Legacy red/yellow/blue/green text and background colors are evidence to inspect, never direct semantic mappings.

## 3. Non-negotiable content fidelity

Do **not**:

- rewrite sentences;
- improve wording;
- summarize;
- shorten;
- expand;
- add examples;
- remove knowledge;
- collapse separate source items into one text run;
- reattach one item's description to another item's label;
- flatten a meaningful nested column relationship into unrelated sequential paragraphs;
- correct accounting content;
- update laws or regulations;
- change legal citations;
- change dates;
- change amounts;
- change percentages;
- change account codes;
- change account names;
- change formulas;
- change Nợ/Có meaning;
- infer facts not present in the source;
- invent URLs;
- invent image URLs;
- invent headings;
- invent missing legal references.

If source content appears wrong, outdated, duplicated, awkward or contradictory, preserve it and report it under **Needs review**.

A title-like first body block is a special structural case, but **hierarchy correction does not imply content deletion**. It may be removed only when supplied masthead-title metadata confirms an exact/no-information duplicate under section 7. Otherwise meaningful opening text must remain visible, usually as `ct-article-intro`.

## 4. Input

Expected input:

- legacy HTML article;
- optionally source URL or metadata supplied by the caller;
- **article title metadata should be supplied whenever available**.

The skill must treat the provided source HTML as authoritative content.

When article title metadata is available, use it only to classify a title-like first body block. Do not rewrite either title or body text to force a match.

## 5. Output

Return exactly two logical sections:

### A. Canonical HTML

Only the transformed article HTML.

### B. Conversion / QA Report

Use these groups:

- **Converted**
- **Removed**
- **Needs review**

The report must describe structural changes, not rewrite the article.

## 6. Canonical body vocabulary

Allowed body semantics include:

- `p`
- `h2`
- `h3`
- `h4`
- `strong`
- `em`
- `p.ct-article-intro`
- `span.ct-key-emphasis`
- `mark.ct-key-highlight`
- `p.ct-source-note`
- `blockquote`
- `ul`
- `ol`
- `.ct-checklist`
- `.ct-steps`
- `.ct-content-box.is-note`
- `.ct-content-box.is-info`
- `.ct-content-box.is-warning`
- `.ct-content-box.is-legal`
- `.ct-content-box.is-example`
- `.ct-key-line.is-formula`
- `.ct-key-line.is-process`
- `.ct-key-line.is-result`
- `.ct-accounting-entry`
- `.ct-accounting-entry__title`
- `.ct-accounting-entry__line.is-debit`
- `.ct-accounting-entry__line.is-credit`
- `.ct-accounting-entry__side`
- `.ct-accounting-group`
- `.ct-accounting-group__title`
- `.ct-definition-list`
- `.ct-fact-list`
- `.ct-data-table.is-simple`
- `.ct-data-table.is-complex`
- `.ct-table-scroll`
- `.ct-editorial-media`
- `.ct-faq`
- `.ct-related-content`

Do not invent new classes.

## 7. Article title root + H1 + intro rule

Article body must never contain `h1`.

The page masthead owns the article title. Legacy content may contain a title-like first `h1` or `h2`. **Do not let that title-root become the parent level for all real body sections. Do not delete it by default either.**

Content preservation and heading-tree normalization are two separate decisions.

### 7.1 Strongest signal: external article title metadata

If article title metadata is available, compare it with the first meaningful body `h1`/`h2` after conservative normalization.

Safe normalization may:

- decode HTML entities;
- strip presentation-only tags;
- trim/collapse whitespace;
- ignore insignificant case/punctuation differences.

It must not rewrite words, remove substantive phrases or use paraphrase to manufacture a match.

### 7.2 Exact/no-information duplicate

If the first title-like block is fully represented by the masthead title and contains **no additional meaningful scope/context**:

1. remove it from canonical body HTML;
2. report the removal explicitly;
3. repair the remaining heading tree so real major sections begin at H2.

This is the only automatic title-text deletion case.

### 7.3 Title-like block with additional meaning

If the first title-like block overlaps the masthead title but contains additional scope, objects, conditions, examples or descriptive information, preserve the complete visible source text as:

```html
<p class="ct-article-intro">...</p>
```

Do not summarize, shorten or rewrite it.

Then repair descendant heading levels independently. Example: if source H2 was acting as title-root and source H3s are real major sections, source H3 → canonical H2 even though source H2 text remains as `ct-article-intro`.

### 7.4 High-confidence fallback without title metadata

When external title metadata is unavailable, a first H1/H2 may still be classified as a probable title-root only when structure is high-confidence, for example:

- it is the first meaningful block;
- it reads like a broad article title rather than a local section label;
- it is followed by introductory prose;
- next structural headings are one level deeper and form multiple peer major sections, often numbered `1.`, `2.`, `3.`;
- there are no peer sections at the same source level as the candidate root.

In this case:

1. **do not delete the text**;
2. convert it to `p.ct-article-intro`;
3. rebase descendants when structurally clear;
4. add **Needs review** because masthead metadata did not confirm classification.

This replaces the older rule that allowed probable title roots to be removed without metadata.

### 7.5 Rebase rule

If title-root was source `h1`:

- source `h2` remains canonical `h2`;
- source `h3` remains canonical `h3`;
- source `h4` remains canonical `h4`.

If title-root was source `h2` and it acted as root of the whole article:

- source `h3` → canonical `h2`;
- source `h4` → canonical `h3`;
- never promote any body heading above `h2`.

Do not perform a blind global shift if the source contains multiple independent heading trees. Rebase only the subtree structurally owned by the title-root.

### 7.6 Ordinary in-body H1

If an in-body `h1` is not the article-title root, convert it to the appropriate H2/H3/H4 only when hierarchy is structurally clear. If ambiguous, preserve the text using the safest heading level and flag **Needs review**.

## 8. Transformation workflow

Use this order:

1. Read the entire source before transforming.
2. Detect/classify any title-like first block and decide preservation vs exact-duplicate removal.
3. Establish required heading rebase independently of title-text preservation.
4. Identify the article's true body section hierarchy.
5. Identify legacy presentation-only markup, including color/background emphasis.
6. Identify semantic blocks.
7. Identify article intro, key emphasis, key highlight, source attribution and result semantics where meaning is clear.
8. Normalize headings using the repaired body hierarchy.
9. Normalize prose and **classify peer lists before considering definition/fact structures**.
10. Normalize callouts.
11. Normalize intro/inline emphasis/source notes/key lines.
12. Normalize accounting entries.
13. Normalize genuine definition/fact structures only after peer-list exclusion.
14. Normalize tables, **classifying nested tables before flattening/unwrap decisions**.
15. Normalize media and links.
16. Remove presentation-only markup.
17. Normalize canonical source whitespace.
18. Verify content fidelity, including opening title text, item boundaries, table-cell boundaries, nested column relationships and emphasis preservation.
19. Produce QA report.

Do not transform block-by-block without understanding the article structure first.

## 9. Legacy presentation removal

Remove presentation-only HTML such as:

- inline `style`;
- legacy `font`;
- redundant `span`;
- visual-only colors;
- fixed widths;
- legacy font-family declarations;
- margin-based fake hierarchy;
- decorative background colors;
- article-specific card styling;
- arbitrary legacy classes.

Before stripping legacy red/yellow/blue/green/background styling, determine whether emphasized text carries a semantic role that should survive as:

- plain prose;
- `strong`;
- `ct-key-emphasis`;
- `ct-key-highlight`;
- key-line;
- semantic callout.

Preserve meaningful text contained inside removed wrappers.

## 10. Security / sanitizer compatibility

Output must be designed to survive `sanitizeEditorialHtml()`.

Never intentionally output:

- `script`
- `style`
- `iframe`
- `object`
- `embed`
- forms or controls
- event handlers
- `data-*`
- inline styles
- arbitrary classes

Do not rely on unsupported attributes for presentation.

## 11. Accounting principle

**Nợ/Có does not mean good/bad, positive/negative, income/expense or profit/loss.**

Never infer debit/credit from visual color or business sentiment.

Only mark a line as debit or credit when source explicitly identifies it.

Canonical example:

```html
<div class="ct-accounting-entry">
  <p class="ct-accounting-entry__title">Định khoản</p>
  <div class="ct-accounting-entry__line is-debit">
    <strong class="ct-accounting-entry__side">Nợ</strong>
    <span>TK 642 — Chi phí quản lý doanh nghiệp</span>
  </div>
  <div class="ct-accounting-entry__line is-credit">
    <strong class="ct-accounting-entry__side">Có</strong>
    <span>TK 111 — Tiền mặt</span>
  </div>
</div>
```

The visible words `Nợ` and `Có` must remain.

## 12. Accounting neutral fallback

If a journal-entry-like line cannot be confidently classified from source content:

```html
<div class="ct-accounting-entry__line">
```

Do not guess `is-debit` or `is-credit`. Add ambiguity to **Needs review**.

## 13. Accounting groups

Use:

```html
<section class="ct-accounting-group">
```

only when multiple accounting entries belong to one clearly identified business event, case or accounting treatment.

Do not wrap unrelated entries merely because they appear near each other.

## 14. Callout discipline

A callout is semantic, not decorative.

Use:

- `is-note` — key insight, main principle, important conclusion;
- `is-info` — neutral additional information or “cần biết”;
- `is-warning` — risk, mistake, penalty, easily misunderstood condition;
- `is-legal` — legal basis, official rule, decree/circular/article reference;
- `is-example` — worked example, calculation, assumed scenario, practical case.

Do not turn ordinary paragraphs into cards.

Avoid excessive callouts. Repetition in source styling does not justify repetition in semantic callouts.

## 15. Key lines

Use:

```html
<p class="ct-key-line is-formula">
```

for compact formulas.

Use:

```html
<p class="ct-key-line is-process">
```

for compact linear processes.

Use:

```html
<p class="ct-key-line is-result">
```

for a resolved final answer/conclusion after a formula, worked example or decision path.

Do not use `is-result` merely because a paragraph contains a number.

If every step needs explanation, use `.ct-steps` instead.

## 15A. Article intro — `ct-article-intro`

Canonical:

```html
<p class="ct-article-intro">...</p>
```

Use only for a title-like opening block that contains meaningful scope/context which should remain visible but should not participate in body heading hierarchy.

Do not:

- invent intro when source has none;
- rewrite title text into marketing copy;
- summarize/shorten source wording;
- use intro for ordinary middle-of-article prose.

## 15B. Key emphasis — `ct-key-emphasis`

Canonical:

```html
<span class="ct-key-emphasis">...</span>
```

Use for a **longer phrase, clause or list-like phrase** that source meaningfully emphasizes and readers benefit from scanning quickly, when:

- `strong` would flatten the intended hierarchy;
- background highlight would be too heavy for the length;
- content is not a whole formula/result/callout.

Typical pattern: a semicolon-separated list of directly includable costs that legacy source rendered as one long red span.

Do not:

- map every red span to `ct-key-emphasis`;
- use it for decorative brand/name coloring;
- wrap whole long paragraphs when only one clause matters;
- create multiple emphasis color variants.

Legacy color is evidence, not meaning.

## 15C. Inline semantic highlight — `ct-key-highlight`

Canonical:

```html
<mark class="ct-key-highlight">...</mark>
```

Use only for a **short phrase inside normal prose** whose emphasis is semantically decisive, such as:

- a timing condition;
- threshold;
- exception;
- scope limit;
- wording whose omission from visual emphasis could materially affect application of the rule.

Do not:

- map every red span or yellow/cyan background to highlight;
- highlight full paragraphs or long lists;
- create multiple highlight color classes;
- use it where `strong`/`ct-key-emphasis` is sufficient;
- use it where entire block should be warning/legal/note/formula/result.

### Emphasis precedence

Use the smallest sufficient semantic:

```text
plain prose
  ↓
strong
  ↓
ct-key-emphasis
  ↓
ct-key-highlight
  ↓
key-line
  ↓
callout
```

Avoid nesting `ct-key-emphasis` and `ct-key-highlight`. If a longer emphasized clause contains one decisive short phrase, split the spans so each semantic owns its own text range.

## 15D. Source attribution — `ct-source-note`

Canonical:

```html
<p class="ct-source-note">Theo Khoản 1 Điều 4 Thông tư ...</p>
```

Use only when source contains a short attribution/reference line attached to preceding content.

Do not invent/update citations.

If source contains a full legal explanation/basis section, use `.ct-content-box.is-legal` instead.

## 16. Lists

Use normal `ul` / `ol` for ordinary grouped information.

### 16.1 Peer-member lists — preferred for sibling categories

Use a normal `ul` when the source introduces a **declared family of sibling items**, especially wording such as:

- “có 4 tài khoản cấp 2”;
- “gồm các loại”;
- “gồm các nhóm”;
- “gồm các trường hợp”;
- “bao gồm các khoản”;
- several similarly shaped category members listed one after another.

A common legacy pattern is:

```html
<p><strong>- Tài khoản 2141 - ...:</strong> Phản ánh...</p>
<p><strong>- Tài khoản 2142 - ...:</strong> Phản ánh...</p>
```

Canonical:

```html
<ul>
  <li><strong>Tài khoản 2141 - ...:</strong> Phản ánh...</li>
  <li><strong>Tài khoản 2142 - ...:</strong> Phản ánh...</li>
</ul>
```

Rules:

- preserve every source item as a separate `li`;
- keep each strong label attached to its own explanation;
- treat leading `-`, `•` or similar characters as presentation-only list markers when they clearly function only as markers, so they are not duplicated beside the EDS bullet;
- do not create a Definition List merely because each item has `strong label + explanation`;
- prefer this primitive structure when items are siblings in one family rather than concepts being defined.

Use:

```html
<ul class="ct-checklist">
```

only for genuine checklists, documents, requirements or items to verify.

Use:

```html
<ol class="ct-steps">
```

only when sequence/order matters.

Do not convert every bulleted paragraph into a special list component.

## 17. Definition list

Use:

```html
<dl class="ct-definition-list">
  <dt>...</dt>
  <dd>...</dd>
</dl>
```

only for genuine **term/concept → definition/explanation** structures, such as:

- terminology/glossary;
- a tax/business code being defined as a concept rather than merely enumerated as a peer member;
- repeated terms that can stand independently as concepts followed by their definitions.

Good fit:

```text
Khấu hao → định nghĩa...
Giá trị còn lại → định nghĩa...
```

Not a Definition List by default:

```text
Tài khoản 214 có 4 tài khoản cấp 2:
- TK 2141: mô tả...
- TK 2142: mô tả...
- TK 2143: mô tả...
- TK 2147: mô tả...
```

That pattern is a **peer-member list** and should normally become `ul > li > strong + text`.

When uncertain between normal list and Definition List, prefer the simpler normal list/prose structure and add **Needs review** rather than forcing `dl`.

Do not use Definition List merely for arbitrary two-column presentation.

## 18. Fact list

Use:

```html
<dl class="ct-fact-list">
  <dt>...</dt>
  <dd>...</dd>
</dl>
```

for compact key/value facts such as:

- document number;
- issue date;
- authority;
- status;
- effective date;
- short metadata.

Do not use it for long narrative explanations.

## 19. Tables

Use semantic table markup:

- `table`
- `caption`
- `thead`
- `tbody`
- `tfoot`
- `tr`
- `th`
- `td`

Use `scope="col"` / `scope="row"` when clear.

### 19.1 Simple table

```html
<table class="ct-data-table is-simple">
```

Use for roughly 2–3 columns or tables that naturally fit the reading lane.

### 19.2 Complex table

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">
```

Use for:

- 4+ columns;
- dense matrices;
- long headers;
- `rowspan` / `colspan`;
- tax rate matrices;
- tables that genuinely need horizontal space;
- 2–3 column comparison tables whose cells contain many paragraphs/bút toán.

Do not convert data tables into images.

### 19.3 Nested table classification — do not flatten by default

A nested legacy table inside a parent `td`/`th` must be classified **before** deciding to unwrap or flatten it.

Ask:

> If the nested table's cell boundaries disappeared, would the reader lose a meaningful association between content on the left/right or between rows/columns?

If **yes**, preserve the relationship.

#### Embedded support table

A common legacy pattern is a one-row, 2–3-cell mini-table used inside a larger comparison cell, where the cells encode a meaningful support relationship such as:

```text
Nợ TK 632 / Có TK 156  |  Theo PP tính giá xuất kho mà DN áp dụng
```

Canonical:

```html
<td>
  <p><strong>Bút toán 2: Ghi nhận giá vốn bán hàng</strong></p>
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
  <p>(Đối với những doanh nghiệp...)</p>
</td>
```

Rules:

- keep it nested directly in the parent cell;
- classify it `ct-data-table is-simple`;
- do **not** wrap this embedded support table in another `.ct-table-scroll`;
- strip legacy widths, cellspacing, cellpadding and inline styles;
- preserve every nested cell's visible text and its original column association;
- do not turn the right-hand explanation into a later unrelated paragraph;
- do not invent a heading/label for either side;
- Nợ/Có text remains explicit; do not infer or alter accounting meaning;
- EDS CSS owns desktop side-by-side presentation and mobile stacking.

#### When flattening is allowed

Flatten/unwrap a nested table only when its cells are genuinely presentation-only and **no meaningful association depends on the row/column boundary**.

Examples:

- a single-cell wrapper around prose;
- cells used only for spacer/alignment;
- an empty companion cell;
- duplicated content whose cell position carries no meaning.

When flattening, preserve the original block order and item boundaries.

#### Genuine nested data matrix

If a nested table is itself a real data matrix with headers/multiple meaningful rows and cannot be represented more simply without information loss, preserve it as semantic table markup and add **Needs review** if responsive behavior is uncertain.

Do not automatically flatten nested tables merely because nested tables are visually inconvenient.

## 20. Media

Canonical:

```html
<figure class="ct-editorial-media is-center is-content-width">
  <img src="..." alt="...">
  <figcaption>...</figcaption>
</figure>
```

Rules:

- preserve existing safe image URLs;
- preserve meaningful existing alt text;
- preserve source caption;
- do not invent new image URLs;
- do not invent R2 URLs;
- do not add width via inline style;
- if image source is legacy/uncertain, preserve when allowed and flag review rather than fabricating replacement.

## 21. Links

Preserve valid source links.

Do not invent links.

Do not rewrite a relative legacy URL into a guessed destination.

If a link is unsafe/cannot survive sanitizer, preserve surrounding text and report removed link under **Removed** or **Needs review**.

## 22. Heading hierarchy

Body hierarchy after title-root handling:

```text
H2 → major section
H3 → subsection
H4 → local sub-subsection
```

Do not use heading level for visual size.

Do not skip hierarchy casually.

Do not convert bold paragraphs to headings unless they clearly function as section labels.

A title-like opening block is **not** a major body section and must not force real sections down to H3. If its text must remain, use `ct-article-intro`.

## 23. Strong and emphasis

Use `strong` for:

- key terms;
- account codes;
- important figures;
- deadlines;
- short conclusions;
- the lead label inside a normal peer-list item.

Use `ct-key-emphasis` for longer scan-worthy clauses where strong is too flat but highlight is too heavy.

Use `ct-key-highlight` only for short decisive conditions/thresholds/exceptions/scope limits.

Do not wrap entire long paragraphs in `strong`, `ct-key-emphasis` or `ct-key-highlight`.

Use `em` sparingly and only where emphasis already exists or is structurally justified.

## 24. Quote

Use `blockquote` only for genuine quoted text or clearly attributed quotations.

Do not use `blockquote` as a visual callout replacement.

## 25. FAQ

Use `.ct-faq` only when source content is genuinely question-and-answer.

Do not convert ordinary subheadings into FAQ merely to create collapsible UI.

## 26. Related content

Use `.ct-related-content` only when source contains an explicit related-resource/article reference block.

Do not create related links from general knowledge.

## 27. Repetition

Do not manually encode A/B presentation variants.

EDS CSS owns repeated-component tint rhythm.

HTML should contain only semantic classes.

Do not alternate emphasis/highlight colors. EDS v2.3.4 has one controlled key-emphasis family and one key-highlight family.

## 27A. Canonical source whitespace

Canonical HTML must be clean and deterministic at source level as well as semantic level.

After semantic transformation and before fidelity audit:

- remove presentation-only empty paragraphs such as `<p>&nbsp;</p>`, `<p><br></p>` and empty `<p></p>` when they carry no meaningful content;
- remove whitespace-only nodes left by unwrapped/removed legacy wrappers;
- do not emit consecutive blank physical lines between block-level elements;
- separate adjacent block-level elements with at most one newline;
- do not add blank lines to create visual spacing — CSS owns layout/rhythm;
- do not collapse meaningful whitespace inside `pre` or code-like content;
- verify whitespace cleanup does not change visible text, table data, list content, URLs or semantic structure.

Source cleanliness must never compensate for a CSS spacing bug.

## 28. Content fidelity audit

Before returning output, compare source vs canonical output for:

- **complete visible text of any title-like first body block**;
- article title metadata when supplied;
- every body heading text that should remain;
- every paragraph;
- every source peer-item boundary;
- every label → description association;
- every list item;
- every amount;
- every percentage;
- every date;
- every account code;
- every occurrence of Nợ/Có;
- every legal citation;
- every top-level table cell;
- every nested table cell whose row/column relation carries meaning;
- every meaningful left/right or row/column association in preserved embedded support tables;
- every link destination;
- every image source;
- every caption.

Also verify meaningful source emphasis is neither blindly discarded nor blindly preserved as legacy color. Visible text must remain identical while semantic emphasis may normalize.

When a presentation-only list marker (`-`, `•`) is replaced by semantic `<li>` structure, its removal is permitted only when it carries no lexical meaning beyond marking the list item.

No factual or meaningful visible text may disappear silently.

If an exact duplicate title is removed, record it and verify its complete text is represented by supplied masthead metadata.

If metadata is absent, a title-like opening block must not be removed; preserve it as intro and report review.

## 29. Ambiguity policy

When semantic classification is uncertain:

1. choose the least opinionated valid structure;
2. preserve content;
3. preserve item boundaries and meaningful table-cell associations;
4. do not guess;
5. add a **Needs review** item.

Examples:

- unclear exact duplicate vs added opening meaning → preserve as intro + review;
- probable title-root without metadata → intro + review, never silent deletion;
- unclear debit/credit → neutral accounting line;
- unclear callout meaning → normal paragraph;
- unclear red/yellow highlight meaning → strip legacy color, use plain/strong/key-emphasis conservatively and flag if material;
- unclear key-emphasis vs key-highlight → prefer strong/key-emphasis; reserve highlight for clearly decisive short phrases;
- unclear result vs formula → formula/prose conservatively;
- unclear heading hierarchy → conservative heading level + review note;
- unclear normal list vs Definition List → **prefer normal UL/LI or prose**, preserve source item boundaries, and flag review rather than forcing DL;
- unclear fact vs definition list → preserve as prose/list + review note;
- unclear nested table: if flattening could destroy a left/right, label/explanation, accounting/basis or row/column association → preserve semantic table structure and flag review rather than flattening.

## 30. Conversion report

Example:

```text
Converted
- Converted a title-like opening H2 with additional scope into ct-article-intro.
- Rebasing restored source H3 major sections to canonical H2.
- Converted a declared family of child accounts from indented paragraphs to normal UL/LI while preserving each label + explanation pair.
- Preserved a meaningful one-row nested support table as nested ct-data-table.is-simple so accounting lines remain associated with their explanatory note.
- Converted a long legacy red scan-worthy cost clause to ct-key-emphasis based on meaning, not color.
- Converted a decisive timing condition to ct-key-highlight.
- Converted one worked scenario to is-example.
- Converted one short legal attribution to ct-source-note.
- Converted one final calculated answer to ct-key-line.is-result.
- Converted journal entries to ct-accounting-entry.
- Converted dense 5-column table to is-complex.

Removed
- Inline red/yellow/blue colors and widths.
- Presentation-only leading hyphen/bullet markers replaced by semantic list structure.
- Empty spans.
- Unsupported presentation-only classes.
- Exact duplicate body title fully represented by supplied masthead title metadata.  # only when applicable

Needs review
- Opening title-like block was preserved as intro because masthead title metadata was unavailable.  # when applicable
- One legacy link target is relative and may not resolve.
- One accounting line does not explicitly identify Nợ or Có.
```

Do not include generic praise/commentary.

## 31. Definition of done

A transformation is complete only when:

- canonical vocabulary is used;
- source meaning, meaningful visible text, item boundaries and meaningful table-cell associations are unchanged;
- title-like first block was evaluated before heading normalization;
- title-like opening content with additional meaning is preserved as `ct-article-intro`;
- no title-like opening text was removed without metadata-confirmed exact/no-information duplication;
- real major body sections begin at H2 rather than being demoted by title-root;
- peer-member families are represented as normal list/prose unless they are genuine glossary definitions;
- no `ct-definition-list` was created solely because each source line has a bold label followed by explanation;
- nested tables were classified before flattening;
- meaningful nested left/right or row/column relationships were preserved;
- presentation-only nested wrappers were unwrapped only when cell boundaries carried no meaning;
- no inline styles/arbitrary classes remain;
- no font/color/spacing/H2-accent/highlight-color presentation is encoded into canonical HTML;
- H1 is absent from body;
- meaningful legacy emphasis was semantically classified rather than blindly copied/discarded;
- `ct-key-emphasis` is reserved for longer scan-worthy clauses;
- `ct-key-highlight` is short, decisive and sparse;
- `ct-source-note` is source-backed and not invented;
- `is-result` is used only for resolved outputs/conclusions;
- journal entries use accounting semantics where appropriate;
- tables are classified;
- semantic callouts are not overused;
- sanitizer-compatible markup is produced;
- canonical source has no consecutive blank lines/presentation-only empty paragraphs;
- whitespace cleanup preserves visible text and semantic structure;
- fidelity audit includes opening content, source item boundaries and meaningful nested table associations;
- QA report is present;
- ambiguities are surfaced rather than guessed.
