# KTD Editorial HTML Transform — Compact Runtime Skill

**Skill name:** `ktd-editorial-html-transform-compact`  
**Runtime version:** 1.1.3  
**Bound canonical skill:** `ktd-editorial-html-transform` v1.4.3  
**Bound EDS:** v2.4.3 — Official Document Fidelity & Presentation Hardening  
**Mode:** FORMAT-ONLY SEMANTIC TRANSFORMATION  
**Runtime policy:** one file only.

---

# 0. Mission

Transform legacy accounting/tax/legal article HTML into canonical semantic HTML for Kế Toán Diệu Tâm while preserving wording, facts, item boundaries, table relationships, meaningful source structure, semantic grouping, meaningful positional relationships, coherent formal-document/form scope, exact ABOUT-vs-OF document boundaries and source-backed formal alignment.

Preferred runtime is a staged closed loop:

```text
STEP 1  OBSERVE SOURCE WITHOUT EDS MAPPING
        ↓
        Source Semantic Inventory

STEP 2  READ THIS SKILL + PLAN
        ↓
        Transform Plan

STEP 3  TRANSFORM
        ↓
        Canonical HTML ONLY

STEP 4  RECONCILE + FIDELITY QA
        ↓
        100% inventory coverage + QA

        PASS                         → STOP
        PASS WITH NEEDS REVIEW      → STOP / human or external review
        FAIL with fixable transform → STEP 5

STEP 5  MINIMAL REPAIR
        ↓
        Revised Canonical HTML
        ↓
        RETURN TO STEP 4
```

**Preferred orchestration:** Step 1 happens before the model sees this skill. This keeps inventory independent from EDS classes.

A single-run implementation may execute Steps 1–4 in one run only when explicitly requested, but employee-facing workflow intentionally separates them for traceability. Step 5 is conditional only.

This compact file is self-contained for runtime use. Canonical skill v1.4.3 is governance source of truth; if a **semantic transformation rule** conflicts, canonical wins. In staged mode, however, the **current step prompt controls output timing and stop point**.

**Additive-upgrade guarantee:** v1.1.3 retains the complete v1.1.2/v1.1.1 runtime contract and adds exact official-form boundary hardening, source-backed Formal Alignment Fidelity and explicit CSS ownership of contextual Official Document Table Presentation. Unchanged mature guards are not removed merely to shorten the file.

---

# 1. Pre-skill Step-1 prompt contract

Before exposing this skill, orchestrator should instruct AI to:

> Read the entire source first. Do not transform it yet and do not choose any EDS class. Create a Source Semantic Inventory in source order. Inventory every region whose visual treatment, structure, grouping, position, table relationship, blank form cells, emphasis, list pattern, accounting pattern, link/media, heading-like presentation, official-document structure, coherent formal-form scope, boundary ownership, source-backed formal alignment, signatory/approval grouping or layout may carry meaning. Use IDs S01, S02... For each item record Location, short Source excerpt/structure, Evidence, neutral Probable role, Relations, Confidence and Risk. Include meaningful structure even when it has no special color or decoration.

The resulting inventory becomes an input to this skill.

For positional/scope/alignment regions, `Relations` should explicitly note where applicable:

```text
left ↔ right
issuer ↔ authority
party A ↔ party B
signer ↔ signer
single signer ↔ source-backed right-side anchor
formal form scope ↔ title/fields/form-slots/tables/declaration/signatures
editorial ABOUT-form material ↔ outside formal scope
printed form title ↔ centered formal identity
unit/date line ↔ source-backed right/edge association
label ↔ explanation
heading ↔ content
header ↔ data
parent ↔ child
account entry ↔ explanation
```

Plain text can still carry positional, boundary, scope or formal-alignment meaning.

---

# 2. Core invariants

> Content determines semantic meaning.  
> Semantic meaning determines canonical structure.  
> CSS determines presentation.  
> Legacy paint is evidence, never a direct mapping.  
> Preserve first; simplify only when meaning is not lost.  
> **Meaningful positional relationship > generic layout-only cleanup.**  
> **Coherent formal-form scope > fragment-by-fragment normalization when source proves one bounded official unit.**  
> **Editorial material ABOUT a document/form ≠ printed/official content OF that document/form.**  
> **Source-backed formal alignment survives only when it carries formal identity/relationship; aesthetics alone never justify alignment classes.**

Non-negotiable:

- do not rewrite/improve/summarize/shorten/expand source wording;
- do not correct apparent typos, laws, dates, amounts, percentages, account codes or formulas;
- do not invent facts, headings, labels, URLs, images or citations;
- do not invent names, signatures, stamps, official roles or missing document metadata;
- do not collapse separate meaningful items;
- do not detach descriptions from labels;
- do not flatten meaningful row/column or left/right relationships;
- do not flatten issuer↔authority or signer↔signer relationships;
- do not flatten a source-backed right-side single-signature anchor into a page-centered signature block;
- do not fragment a coherent official/tax form into unrelated article-root siblings when source evidence shows one form boundary;
- do not absorb unrelated article lead-in/commentary/related-content into a formal-form scope merely because it is adjacent;
- do not absorb an article H2/H3 or editorial warning that merely describes/explains a form into the printed form unless source ownership proves it belongs there;
- do not strip source-backed centered/right formal alignment before deciding whether it preserves printed form title identity, unit/date edge association, role or signature relation;
- do not preserve every legacy `text-align` mechanically; decorative alignment still normalizes away;
- do not merge/split meaningful table cells without source evidence;
- do not remove meaningful blank form cells;
- do not change Nợ/Có meaning;
- do not classify an official header/signature/form boundary as layout-only before checking relationship/scope meaning;
- do not invent `ct-official-header` for a headerless form;
- do not create a new signature-box/form-card class just to add borders;
- do not add inline CSS for presentation;
- do not invent classes;
- do not emit new content boxes as `aside.ct-content-box` or `blockquote.ct-content-box`;
- do not emit a content-box title as `div.ct-content-box__title`;
- do not rewrite/delete/relabel Source Semantic Inventory merely to make transformed HTML pass QA;
- do not self-approve staged transform before Step 4;
- do not turn ordinary legal prose into Official Document merely because it cites law;
- do not use `is-legal` as a substitute for official-document structure;
- do not reclassify `is-simple ↔ is-complex` merely to obtain the official-document formal-neutral table palette.

If source appears wrong/outdated/contradictory: preserve it and report **Needs review**.

---

# 3. Required inputs

1. Original source HTML/text.
2. Source Semantic Inventory from Step 1.
3. Optional CMS/article title metadata.
4. Optional trusted source URL/media metadata.

If inventory is missing in a single-run context, create it before transformation using Section 4. Do not assign EDS classes while creating it.

**Important:** inventory is an **evidence checklist, not an answer key**. `Probable role` is only neutral observation. During Step 3, source evidence + this skill decide mapping. If inventory interpretation conflicts with source, preserve source and explain mismatch during reconciliation rather than forcing source into the inventory guess.

---

# 4. Source Semantic Inventory contract

Use stable IDs `S01`, `S02`, ... in source order.

```text
S01
Location: opening / section 2 / table 3 row 4 / etc.
Source excerpt / structure: exact short excerpt or structural description
Evidence: visual/structural evidence only
Probable role: neutral natural-language description, NOT EDS class
Relations: parent/child, sibling-family, left↔right, issuer↔authority, signer↔signer, single signer↔right-side anchor, formal-form scope↔children, ABOUT-form↔outside, formal alignment↔identity/edge, row/column, label↔value, etc.
Confidence: high | medium | low
Risk: what may be lost/misread during normalization
```

Inventory signals include:

- title-like first block / oversized heading;
- real or fake headings;
- bold/italic/underline;
- colored/highlighted text/background;
- boxed/bordered/shaded blocks;
- centered/right-aligned special lines;
- legal/source attribution;
- `Lưu ý`, `Chú ý`, `Ví dụ`, `Kết luận`, `Như vậy`;
- process/formula/result lines;
- manual bullets;
- peer-member sequences;
- term→definition or fact key→value sequences;
- Nợ/Có/accounting groups;
- tables, layout tables, form-slot grids;
- nested tables;
- multi-row headers, `rowspan`, `colspan`;
- meaningful blank cells;
- links/images;
- decorative separators/empty spacers;
- FAQ/related-content/checklist/step patterns;
- official/formal document structures;
- **coherent formal-form cues:** `Mẫu`, `Phụ lục`, form name/code/reference, `[01]...[NN]` coded fields, segmented slots, administrative data matrix, unit/legend, declaration/certification, signature/approval regions and wrapper/sequence evidence tying them together;
- **boundary ownership cues:** article heading/intro/warning ABOUT the form versus printed/form-owned content OF the form;
- **formal-alignment cues:** centered printed form title, right-aligned unit/date line, issuer/authority placement, signature/approval positioning, or other source-backed alignment whose removal can weaken document identity/edge association;
- signature/approval/confirmation groups;
- single-signature layouts where blank/unused companion space or column geometry clearly anchors the signer to one side;
- any left↔right or parallel/opposed grouping;
- anything whose meaning may disappear when presentation markup is stripped.

Do not inventory only colorful content. Plain structural relationships, exact boundaries and formal alignments matter too.

---

# 5. Canonical vocabulary

Body H1 is forbidden.

Core tags:

```text
p h2 h3 h4 strong em blockquote
ul ol li
mark span
dl dt dd
table caption thead tbody tfoot tr th td
figure img figcaption
details summary
aside div section
```

Canonical classes:

```text
ct-align-left ct-align-center ct-align-right
ct-article-intro
ct-key-emphasis
ct-key-highlight
ct-source-note

ct-checklist
ct-steps

ct-content-box
is-note is-info is-warning is-legal is-example
ct-content-box__title
ct-content-box__body

ct-key-line
is-process is-formula is-result

ct-data-table
is-simple is-complex
ct-table-scroll

ct-accounting-entry
ct-accounting-entry__title
ct-accounting-entry__line
ct-accounting-entry__side
is-debit is-credit
ct-accounting-group
ct-accounting-group__title

ct-definition-list
ct-fact-list

ct-editorial-media
is-left is-center is-right
is-content-width is-medium is-natural is-custom

ct-faq
ct-faq__item
ct-faq__answer

ct-related-content
ct-related-content__label
ct-related-content__link
ct-related-content__type
ct-related-content__title
ct-related-content__summary

ct-official-document
ct-official-header
ct-official-header__issuer
ct-official-header__authority
ct-signature-grid
ct-signature-party
```

Formal Form Scope Detection and Official Document Table Presentation add **no new class**. Formal alignment reuses existing `ct-align-left/center/right` on supported elements.

Do not invent visual variants such as `ct-two-col`, `ct-left`, `ct-right`, `ct-document-card`, `ct-form-card`, `ct-signature-box`, `ct-official-table`, `is-government`.

## Content-box tag contract — MUST FOLLOW EXACTLY

For every **new canonical content box**:

```html
<div class="ct-content-box is-example">
  <p class="ct-content-box__title">Ví dụ</p>
  <div class="ct-content-box__body">
    <p>...</p>
  </div>
</div>
```

Rules:

- root = `div.ct-content-box` + exactly one of `is-note/is-info/is-warning/is-legal/is-example`;
- title, when source actually has one = `p.ct-content-box__title`;
- body wrapper = `div.ct-content-box__body`;
- if source has no standalone title/label, omit title; do not invent visible text;
- **forbidden in new output:** `aside.ct-content-box`, `blockquote.ct-content-box`, `div.ct-content-box__title`;
- sanitizer may preserve those legacy shapes for migration compatibility, but transformer must normalize them;
- if root has zero or multiple semantic variants, transformer QA fails; do not invent a missing variant or choose arbitrary winner.

This removes unnecessary AI choice: model decides only **whether block is content box** and **which semantic variant**; never root tag.

---

# 6. Step-3 transformation order

1. Read source + inventory completely.
2. Resolve title-like opening.
3. Reconstruct true heading tree independently from opening preservation.
4. **Run positional-semantic gate before generic layout cleanup.**
5. **Detect coherent formal-document/form scope before classifying child tables independently.**
6. **Run ABOUT-vs-OF boundary gate: separate editorial headings/warnings/commentary from printed/official form-owned content.**
7. **Run Formal Alignment Fidelity gate before stripping source alignment inside official/form regions.**
8. Identify official-document/header and signatory/approval structures, including source-backed single-signature side anchoring.
9. Normalize prose, lists, peer groups, definitions/facts.
10. Classify emphasis, callouts and key lines from meaning.
11. Normalize every content box to exact `div/p/div` contract.
12. Normalize accounting.
13. Classify every table recursively **before** stripping/flattening it.
14. Detect form-slot grids before generic matrix/header normalization.
15. Preserve genuine header rows/spans/nested relations.
16. Map supported official/signature relationships to canonical positional components **inside preserved formal scope when applicable**.
17. Preserve source-backed meaningful formal alignment using only existing `ct-align-*` classes.
18. Normalize links/media and special structures.
19. Strip presentation-only markup/layout shells only after relationship/scope/boundary/alignment classification.
20. Clean whitespace.
21. **Staged mode:** current production Step-3 prompt requires **exactly one fenced `html` code block containing Canonical HTML only**. The fence is a transport wrapper for copyability, not part of the Canonical HTML artifact. Do not output notes, explanation, QA, PASS/FAIL, explanatory HTML comments, or any text before/after the fence.
22. **Single-run mode only:** after Step-3 HTML is complete, continue to Sections 31–35 for reconciliation and QA.

---

# 7. Opening title / heading tree

Page masthead owns H1. Article body contains no H1.

Decision:

```text
CMS title metadata available?
  exact/no-information duplicate
    → remove + report

  overlaps title but adds meaningful scope/context
    → preserve FULL source text as <p class="ct-article-intro">

  not duplicate
    → preserve meaning and classify normally

No CMS title metadata + high-confidence article-title root
    → preserve FULL text as ct-article-intro + Needs review
```

Heading normalization:

- true major sections → H2;
- subsection under H2 → H3;
- subsection under H3 → H4;
- no H5/H6 in canonical article body;
- do not infer heading from color alone;
- title-root preservation and heading rebase are separate;
- never delete meaningful opening text just to repair hierarchy;
- an article heading that names/describes an official form is **not automatically printed form content**; formal-form ownership is decided separately.

---

# 8. Inline emphasis ladder

Use smallest sufficient semantic:

```text
plain
→ strong
→ ct-key-emphasis
→ ct-key-highlight
→ ct-key-line
→ ct-content-box
```

- `strong`: ordinary local emphasis/label/term.
- `span.ct-key-emphasis`: longer scan-worthy phrase/clause; stronger than `strong`, lighter than highlight.
- `mark.ct-key-highlight`: short decisive condition/threshold/exception/timing/scope.
- do not highlight long paragraphs.
- do not nest `ct-key-emphasis` and `ct-key-highlight`; split ranges.

Legacy paint alone never decides semantics:

```text
red ≠ warning automatically
yellow/cyan background ≠ highlight automatically
blue ≠ heading automatically
green background ≠ example automatically
```

Preserve genuine source italics as `em` when they carry emphasis/citation meaning. Preserve genuine quotation semantics as `blockquote`; do not manufacture blockquote from indentation alone.

---

# 9. Source notes, callouts, key lines

Short attribution/citation line:

```html
<p class="ct-source-note">(Theo Khoản ... Điều ...)</p>
```

Whole-block callout mapping:

```text
is-note    → insight/principle/key takeaway
is-info    → neutral additional information
is-warning → risk/error/penalty/caution
is-legal   → official/legal rule/requirement quotation
is-example → example/case/calculation scenario
```

Canonical callout:

```html
<div class="ct-content-box is-warning">
  <p class="ct-content-box__title">Lưu ý</p>
  <div class="ct-content-box__body">
    <p>...</p>
  </div>
</div>
```

Change only semantic variant. Preserve source wording. Title optional and must come from source meaning/text.

Key lines:

```text
is-process → compact process/sequence
is-formula → compact calculation/formula/rule expression
is-result  → resolved conclusion/final answer/result
```

Use legal callout for substantive legal rule; use `ct-source-note` for short attribution.

**Do not use `is-legal` for an entire official document/header/form merely because it is legal/official.** Official document/form structure has separate semantics in Sections 13–15.

An editorial `is-warning` ABOUT a form may remain outside `ct-official-document` when source evidence shows it is article/editorial material rather than printed form content.

---

# 10. Lists / checklist / steps / definitions / facts

## Peer members

Declared sibling families such as:

```text
“có N tài khoản cấp 2”
“gồm các loại/nhóm/trường hợp”
“bao gồm các khoản”
```

with parallel `bold label + description` items → normal `ul/li + strong`.

Remove manual source marker (`-`, `•`, `ü`, `Ø`, `+`) when semantic list owns marker.

## Checklist

Use `.ct-checklist` only when items are genuinely completion/verification items. Do not convert ordinary bullet list merely because items look actionable.

## Steps

Use `.ct-steps` only for ordered procedure/process where sequence matters. Otherwise normal `ol` or prose.

## Definition list

Use `.ct-definition-list` only for genuine:

```text
term/concept → definition
```

A bold label alone is not enough.

## Fact list

Use `.ct-fact-list` for concise metadata-like key→value facts, not explanatory prose.

Ambiguous list vs definition → prefer normal list/prose + review.

---

# 11. Accounting

Nợ/Có is explicit accounting side, not color/sentiment.

```html
<div class="ct-accounting-entry">
  <div class="ct-accounting-entry__line is-debit">
    <strong class="ct-accounting-entry__side">Nợ</strong>
    <span>TK ...</span>
  </div>
  <div class="ct-accounting-entry__line is-credit">
    <strong class="ct-accounting-entry__side">Có</strong>
    <span>TK ...</span>
  </div>
</div>
```

Rules:

- `.is-debit/.is-credit` only when source explicitly says Nợ/Có;
- accounting entry title optional;
- **never invent visible “Định khoản”** when source has no title;
- multiple related entries may use `.ct-accounting-group`;
- when table comparison/support relation is primary, Nợ/Có may remain literal inside cells instead of nested accounting cards;
- preserve codes, amounts and order exactly.

---

# 12. Other semantic structures

## Editorial media

Use `.ct-editorial-media` when valid source image/media survives sanitizer and semantic figure/caption structure is useful. Do not invent width/alignment not supported by source/context.

## FAQ

Use `.ct-faq` only for genuine question→answer material. Do not turn ordinary headings into FAQ just because they end with `?` unless source structure/meaning supports Q&A.

## Related content

Use `.ct-related-content` for genuine in-body related-resource block. Preserve visible title/type/summary/link semantics; do not invent destination URLs.

Post-form `Xem thêm`/related content stays outside `ct-official-document` unless source proves it is printed/form-owned.

---

# 13. Positional-semantic + scope precedence gate

Before unwrapping any layout table/div/grid ask:

> If these regions are serialized into ordinary prose, will reader lose who belongs to which side/role/party, who issues vs represents authority, who signs/approves/confirms, whether a single signer is intentionally anchored to one side, label↔explanation association, **whether several form fields/tables/declarations/signatures jointly belong to one coherent formal form**, **whether an adjacent heading/warning is editorial ABOUT the form rather than printed OF the form**, or another meaningful parallel/opposed relationship?

```text
YES
→ not layout-only
→ preserve/map relationship or scope

UNCERTAIN
→ preserve safest grouping/scope
→ Needs review

NO
→ layout-only cleanup may proceed
```

Old table markup, fixed widths, centered/right-aligned text, blank spacer cells or Office styles do not bypass this gate. A blank companion cell may be presentation-only as content while still providing evidence that the neighboring signer region is positionally anchored.

A legacy outer table/div may be presentation-only implementation while still carrying **formal-form boundary evidence** for the children it groups. Conversely, adjacency inside one legacy wrapper does not prove editorial material belongs to the printed form.

**Precedence:**

```text
meaningful positional relationship / exact coherent formal-form scope
> generic layout cleanup
> markup simplification
```

---

# 14. Official Document + Formal Form Scope

Use `section.ct-official-document` only for genuine formal/official document, declaration, administrative/tax form, notice, decision, dispatch/công văn or meaningful official-document fragment, not ordinary prose merely discussing law.

## 14.1 Formal Form Scope Detection

Detect the **whole coherent form scope before child-table classification**.

Common source cues:

```text
Mẫu / Phụ lục / form name / form code
“kèm theo ...” or official reference
systematic field codes [01], [02], [03]...
segmented digit/character slots
administrative data matrix / bảng kê
unit line / legend / abbreviation note owned by the form
declaration / certification / cam đoan
signature / approval / taxpayer / agent regions
legacy wrapper or contiguous table/div sequence tying these pieces together
```

No mechanical “N cues = form” quota. Decide from **coherence + boundary evidence**.

### ABOUT vs OF boundary gate — v1.1.3

Classify adjacent nodes before choosing FORM START:

```text
EDITORIAL / ARTICLE MATERIAL ABOUT THE FORM
vs
PRINTED / OFFICIAL CONTENT OF THE FORM
```

Common ABOUT-form nodes that stay outside unless source proves printed/form ownership:

- article H2/H3 naming or introducing the form;
- editorial warning/note explaining replacement, effective date or usage;
- article lead-in/caption/intro;
- post-form `Xem thêm` / related-content / commentary.

Common OF-form start evidence:

- printed `Phụ lục` / formal form title block;
- official form code/title printed in the form;
- first clearly form-specific coded field when no separate printed title exists.

Canonical boundary example:

```text
article H2 describing Mẫu 05-2/...             → OUTSIDE
warning “Chú ý: Mẫu này thay thế...”           → OUTSIDE
printed “Phụ lục / BẢNG KÊ...”                → FORM START
[01]...[NN], slots, matrix, declaration        → INSIDE
signature parties                              → INSIDE / END
Xem thêm                                       → OUTSIDE
```

If source proves a warning/note is printed as part of the official form, keep it inside. Source ownership—not keyword or adjacency—decides.

When evidence supports one form:

```text
START
→ source-backed printed form title / appendix title / first form-specific field

MIDDLE
→ coded fields
→ form-slot grids
→ simple/complex tables
→ form-owned units/legends/notes
→ declaration/certification

END
→ signature/approval region
→ or last clearly form-owned content
```

Canonical pattern:

```html
<section class="ct-official-document">
  <!-- source-backed printed form title/fields -->
  <!-- form-slot/simple/complex tables keep own semantics -->
  <p>...</p><!-- declaration if source-backed -->
  <div class="ct-signature-grid">
    <div class="ct-signature-party">...</div>
    <div class="ct-signature-party">...</div>
  </div>
</section>
```

Rules:

1. `ct-official-document` owns the **scope/boundary**, not each child presentation.
2. Child tables still classify independently.
3. Signature Grid still owns party grouping.
4. `ct-official-header` is **optional**; do not invent issuer↔authority header for a headerless form.
5. Do not invent quốc hiệu/agency/date just to make the form look official.
6. Do not create a nested signature card/frame inside an already bounded official form.
7. Do not lose outer scope merely because legacy source uses multiple sibling tables/divs.
8. If exact boundary is uncertain, preserve safest contiguous formal fragment + Needs review.
9. **Under-wrap** and **over-wrap** are both fixable fidelity failures when source boundary is clear.

Correct child tables/signatures are **not enough** if coherent form scope or exact source-backed boundary is wrong.

## 14.2 Formal Alignment Fidelity — v1.1.3

Before stripping `text-align` inside a genuine official document/form ask:

> Does this source alignment preserve formal document identity, edge association, official role/date/unit placement, signature relationship or another positional meaning that would be weakened if normalized to ordinary left prose?

```text
YES
→ preserve using existing ct-align-left / ct-align-center / ct-align-right on supported elements

UNCERTAIN
→ preserve safest supported alignment/grouping + Needs review

NO
→ strip legacy alignment; normal CSS flow owns presentation
```

Typical justified mappings:

```html
<p class="ct-align-center">
  <strong>Phụ lục</strong><br>
  <strong>BẢNG KÊ CHI TIẾT CÁ NHÂN</strong><br>
  <em>(Kèm theo ...)</em>
</p>

<p class="ct-align-right"><em>Đơn vị tiền: Đồng Việt Nam</em></p>
```

Inspect source-backed place/date, issuer/authority and certification/signature alignment similarly when position carries meaning.

Do **not** preserve every centered/right line. Decorative/spacer alignment normalizes away. Do not invent `ct-form-title`, `ct-unit-right`, `ct-official-center` or inline style.

## 14.3 Official two-side header

```html
<section class="ct-official-document">
  <div class="ct-official-header">
    <div class="ct-official-header__issuer"><p>...</p></div>
    <div class="ct-official-header__authority"><p>...</p></div>
  </div>
  ...
</section>
```

Preserve exact text, source order and internal grouping.

If legacy 1×2 table only places two semantic groups such as:

```text
issuing agency / document number
↔
national/authority heading / motto / place-date
```

remove table mechanics only **after** mapping relationship to official header.

Never substitute `is-legal` for official header.

If relation is clear but issuer/authority role naming lacks enough evidence, preserve safest grouped relation + Needs review rather than guessing.

Official document/form body may contain recipient, prose, legal citations, coded fields, form-slot grids, data tables, units/legends, declaration and signature region. Do not make every child a card/callout.

## 14.4 Official Document Table Presentation ownership

Table semantics are unchanged by ancestor context:

```text
is-simple remains is-simple
is-complex remains is-complex
form-slot remains the same structural table
```

CSS under `ct-official-document` uses a formal-neutral document palette, clearer neutral grid, minimal radius, no editorial zebra/hover treatment and paper-like form-slot styling. **Transformer must not add a class or change semantic classification to obtain this visual mode.**

Ordinary tables outside `ct-official-document` retain normal EDS presentation, including deep-teal top-level simple headers.

---

# 15. Signature Grid

Use when either:

1. two or more distinct signatory/approval/confirmation regions form a meaningful relationship; **or**
2. a single signatory region has clear source-backed positional meaning, especially a formal-document layout where an empty/unused left companion region and a populated right region show that the signer is intentionally anchored to the right.

Multi-party canonical:

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">
    <p><strong>...</strong></p><p>...</p>
  </div>
  <div class="ct-signature-party">
    <p><strong>...</strong></p><p>...</p>
  </div>
</div>
```

Source-backed single signer anchored right:

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">
    <p><strong>KT. ...</strong></p>
    <p><strong>PHÓ ...</strong></p>
    <p><strong>...</strong></p>
  </div>
</div>
```

For a one-party grid, the **single child is semantic evidence of a source-backed right-side signature anchor**. CSS keeps the party centered inside its own signature region while anchoring that region to the right on larger screens; mobile may expand it to full width. Do not create an empty fake `ct-signature-party` merely to occupy the left side.

Rules:

- preserve meaningful party count;
- preserve source order;
- keep each party label/title/name/note together;
- do not invent visible placeholders/underscores, names, stamps or dates;
- legacy table may be replaced by signature grid when cells primarily place signatory parties or preserve a source-backed single-signature side anchor;
- a blank companion cell may be removed as markup/content while its positional evidence is preserved by the one-party grid;
- CSS may stack/expand parties on mobile; transform must not merge them;
- one-party signature with **no** meaningful side anchoring normally remains ordinary grouped prose;
- a single signer originally anchored right must not become centered across the entire document after transform;
- when signature belongs to a coherent formal form, keep it **inside** that `ct-official-document`; do not add a separate semantic wrapper/card just for another border;
- CSS may add only subtle direct signature-zone separator/rhythm; no semantic class changes;
- **never use “signature layout” as an automatic Type-A/layout-only example.**

---

# 16. Top-level table gate

Before changing any table classify it as:

```text
A. truly layout-only
B. segmented form-slot grid
C. simple data matrix
D. complex data matrix
E. supported positional semantic structure (official/signature)
```

**Formal-scope precedence:** when table belongs to a coherent official form, preserve/map the outer `ct-official-document` scope first, then classify the table itself. Scope and table semantics coexist.

### A. Truly layout-only

Unwrap only when row/cell boundaries and group position are presentation-only, e.g. single-cell prose wrapper, spacer/alignment shell, redundant visual container **after positional/scope gate returns NO**. A legacy wrapper cannot be discarded at scope level before any formal-form boundary it evidences has been preserved.

### B. Form-slot grid

See Section 19.

### C. Simple matrix

```html
<table class="ct-data-table is-simple">...</table>
```

**Default simple candidate:** genuine **2–4 effective-column** matrix when:

- relationship is straightforward row/column matrix;
- header absent or one-level/simple;
- no meaningful multi-row header hierarchy;
- no meaningful `rowspan/colspan` creating structural hierarchy;
- no structurally dense nested matrix;
- content may contain longer prose, but matrix relationship remains simple.

When these conditions hold, **prefer `is-simple`** rather than promoting to complex merely because table has four columns, many rows or long-text cells.

The following facts **alone are NOT sufficient** to classify complex:

- exactly 4 effective columns;
- many body rows;
- long prose in one or more cells;
- visually prominent but one-level first row.

### D. Complex matrix

Use top-level compatibility wrapper:

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">...</table>
</div>
```

Strong complex cues:

- **5+ effective columns**;
- genuinely dense structural matrix/content;
- long **multi-row/hierarchical** headers;
- meaningful `rowspan` / `colspan`;
- dense comparison/accounting matrix with structural complexity;
- high-cell-count meaningful form grid.

A 4-column table may still be complex when another strong cue exists. Column count is a cue, not a substitute for structural classification.

Never classify simple↔complex merely to obtain preferred color/width or official-document visual mode. Conversely, do not over-classify a structurally simple 2–4-column matrix as complex out of caution alone.

### E. Positional semantic

When cells primarily encode official/signatory role grouping rather than data matrix semantics, map to specific canonical component after preserving group boundaries. This includes a source-backed single-signature right anchor when table geometry clearly carries that positional meaning.

---

# 17. Fit-only table invariant

Transformer has **no horizontal-scroll decision**.

```text
simple table  → fit 100%
complex table → fit 100%
nested table  → fit parent cell
```

Never:

- add fixed width/min-width to force a canvas;
- invent responsive/scroll classes;
- create nested scroll wrappers;
- flatten meaningful wide table because it is wide;
- promote/widen parent solely because child is complex;
- alter semantics for responsive appearance.

CSS owns fit density, font size, padding, wrapping, gridlines, header colors and contextual official-document table presentation.

`ct-table-scroll` remains a **compatibility wrapper**, not a scroll instruction.

---

# 18. Table integrity

For every semantic table preserve:

- meaningful visible text per cell;
- row order;
- cell order;
- header relationships;
- meaningful blank cells;
- exact meaningful `rowspan`/`colspan`;
- Nợ/Có/account codes/amounts/dates;
- nested parent-child association;
- meaningful left/right association;
- formal-form ownership when table belongs to a coherent official form.

Strip legacy fixed widths/heights/cellpadding/cellspacing when presentation-only.

Do not repair spans by guess. Ambiguous/malformed spans → safest faithful structure + Needs review.

Do not change semantic table class because the same table receives a different formal-neutral palette inside `ct-official-document`.

---

# 19. Segmented form-slot grid

Typical source:

```text
[03] Mã số thuế: | □ | □ | □ | □ | ...
```

Detection requires **actual blank-slot evidence**, not cell count alone:

- one body row;
- no genuine heading row;
- first cell is field label/code;
- many following cells are blank character/digit slots;
- slot position/count meaningful.

Rules:

1. preserve every meaningful slot;
2. normally high-cell-count form grid = `is-complex`;
3. keep label + slots same `tbody` row;
4. do **not** invent `thead`;
5. do **not** convert label cell to `th` merely because first/bold;
6. do not collapse blank slots;
7. strip legacy width/height/style;
8. do not add scroll/width logic;
9. one-row 10+ table with populated peer values = ordinary matrix, **not** form-slot.

A form-slot grid may sit inside `ct-official-document`; outer form scope does not change slot semantics. CSS may use paper-like neutral label/slot styling under that ancestor without adding HTML classes.

---

# 20. Header / span fidelity

For genuine headers:

- use `thead` for real heading rows/groups;
- use `th` for true header cells;
- preserve meaningful multi-row hierarchy;
- preserve exact `rowspan`/`colspan`.

Complex header hierarchy:

```text
major group row
→ intermediate group row(s)
→ terminal leaf row
```

Never:

- flatten meaningful header rows;
- invent extra header rows;
- infer terminal row = “code/index” merely because last;
- mutate cell order/spans to repair visual borders.

EDS presentation is CSS-owned:

```text
ordinary top-level simple header → deep teal / white
ordinary nested simple header    → quiet light
ordinary complex header          → light hierarchy
inside ct-official-document      → formal-neutral contextual hierarchy, semantic class unchanged
```

---

# 21. Nested table gate

Before flattening nested table ask:

> Would removing row/cell boundaries destroy meaningful left/right, row/column, label/explanation, accounting/basis, condition/treatment, value/note or positional party/role association?

If yes → preserve nested table or map specific positional component.

Each table is independent semantic scope. Child columns/spans must not reclassify parent. Broader formal-form ownership is preserved independently from table type.

### Type A — truly layout-only

Unwrap only when boundaries carry no semantic dependence on position and do not provide still-unmapped formal-form boundary evidence.

### Type B — one-row support relation

Shape:

- one meaningful row;
- 2–3 cells;
- no meaningful thead/tfoot;
- no span;
- local support relation such as accounting lines ↔ explanation/basis.

```html
<table class="ct-data-table is-simple">
  <tbody><tr><td>Primary</td><td>Explanation</td></tr></tbody>
</table>
```

Directly inside parent cell; **no child `ct-table-scroll`**. Preserve cell order/association. CSS may stack on mobile.

If relation is actually signatory/approval party grouping, Signature Grid takes precedence. If two-cell row is blank left + formal signer right, evaluate source-backed single-signature anchor before Type A/B.

### Type C — embedded small matrix

**2–4 effective columns**, multiple meaningful rows and/or simple one-level `thead`, no meaningful complex spans/header hierarchy → nested `.ct-data-table.is-simple`; remain tabular; no child wrapper.

A nested 4-column matrix is not Type D merely because it has four columns. Promote only with genuine complex cue.

### Type D — nested complex matrix

**5+ effective columns** OR meaningful spans OR complex/multi-row headers OR dense numeric/accounting matrix with structural complexity → nested `.ct-data-table.is-complex`; preserve structure; no child wrapper; do not widen/promote parent.

---

# 22. Nested depth + locality

Automatic confidence covers one meaningful nested level:

```text
Top-level table
  └─ Nested table
```

Meaningful depth >1:

1. classify deepest first;
2. unwrap presentation-only levels if safe;
3. preserve remaining meaningful structure;
4. Needs review;
5. no automatic full PASS.

Per-table locality:

```text
parent semantics    ← parent direct rows/cells
child semantics     ← child direct rows/cells
form-slot evidence  ← current table direct cells
span model          ← current table direct cells
formal-form scope   ← broader source continuity/boundary evidence
formal alignment    ← source-backed identity/edge/role evidence
```

Never let nested child density/spans mutate parent semantic classification.

---

# 23. Links

Preserve source links only when sanitizer-compatible.

Safe categories:

```text
https://...
http://...
/root-relative-path
#valid-anchor
mailto:...
tel:...
```

Legacy relative links such as:

```text
filename.html
assets/...
../page.html
```

must not be “fixed” by guessing/prepending `/`.

If unsafe:

- preserve visible link text;
- remove unsafe clickable destination if required;
- report migration/Needs review.

Never invent URL.

---

# 24. Media

Preserve image/media only when source URL/path can satisfy current sanitizer/media contract.

Do not guess CDN/R2/root-relative destination.

If unsafe legacy relative image cannot survive:

- remove image element if required;
- preserve meaningful caption text where appropriate;
- report media migration required.

---

# 25. Presentation-only removal

After semantic classification, remove safely:

- inline `style`;
- font face/size markup;
- `mso-*` and Office-only classes;
- redundant spans;
- visual-only colors/backgrounds;
- presentation-only fixed table dimensions;
- manual bullets replaced by semantic list markers;
- empty spacer paragraphs;
- decorative separators;
- truly layout-only table shells.

Do not remove a presentation artifact before deciding whether it carries meaning recorded in inventory. In particular, blank signature companion may be removed only after its positional evidence has been mapped.

A legacy outer wrapper/table of a coherent formal form may be stripped only **after** its semantic boundary is preserved by `section.ct-official-document`.

Source alignment inside official/form regions must pass Formal Alignment Fidelity before removal. Preserve only meaningful source-backed alignment using existing `ct-align-*` classes.

---

# 26. Sanitizer / security contract

Canonical output must not intentionally contain:

```text
script
style
iframe
form/input controls
event handlers
arbitrary data-* attributes
arbitrary classes
unsafe guessed URLs
```

Use only supported semantic tags/classes/attributes. `rowspan`, `colspan`, safe `scope`, valid links and canonical media attributes may be preserved when supported.

Content-box sanitizer gate:

```text
NEW canonical root → div.ct-content-box + one semantic variant
optional title     → p.ct-content-box__title
body wrapper       → div.ct-content-box__body
```

Before PASS, reject/normalize new output containing:

```text
aside.ct-content-box
blockquote.ct-content-box
div.ct-content-box__title
```

Also reject roots with zero/multiple semantic variants. Sanitizer may preserve generic `ct-content-box` for malformed/legacy input, but transformer must not invent `is-note` or choose arbitrary conflicting variant.

Positional sanitizer contract:

```text
section → ct-official-document

div → ct-official-header
      ct-official-header__issuer
      ct-official-header__authority
      ct-signature-grid
      ct-signature-party
```

Formal-form scope uses existing `section.ct-official-document`; no new class/permission. Formal alignment uses existing `ct-align-left/center/right` on supported elements. No inline alignment style.

`section.ct-official-document` and `section.ct-accounting-group` must not coexist on same element.

Sanitizer legacy compatibility is migration safety, not generation rule.

---

# 27. Canonical whitespace

- no empty presentation paragraphs;
- no repeated blank blocks for spacing;
- CSS owns rhythm;
- preserve meaningful `pre/code` whitespace;
- remove Office/list-marker noise without merging items;
- do not invent visible spacer text/underscore lines merely to preserve official/signature alignment.

---

# 28. Ambiguity policy

```text
preserve content
→ preserve relationship/group membership
→ preserve exact coherent formal scope when source-backed
→ distinguish ABOUT-form from OF-form
→ preserve source-backed formal alignment when meaning-bearing
→ choose less destructive supported structure
→ do not guess
→ Needs review
```

Defaults:

- peer-list vs definition-list → normal list/prose;
- possible nested relation → preserve table rather than flatten;
- possible positional relation → preserve grouping rather than serialize;
- coherent formal-form cues but uncertain exact boundary → preserve safest contiguous formal fragment + Needs review;
- article H2/warning adjacent to form but ownership unclear → safest boundary + review, not adjacency-based guess;
- meaningful centered/right formal alignment uncertain → preserve safest supported alignment + review rather than destructive strip;
- single signer with clear right-side source anchor → one-party signature grid;
- single signer without clear side anchor → ordinary grouped prose / safest structure, not invented alignment;
- possible form-slot → require real slot evidence, otherwise matrix;
- possible multi-row header → preserve row/span boundaries;
- malformed span → no invented repair;
- unclear Nợ/Có → neutral text/line + review;
- unclear official role naming → preserve relation + review rather than invent role semantics.

---

# 29. Step-4 Inventory Reconciliation

Return to **every `Sxx` item** after transformation.

Allowed dispositions:

```text
Converted
Preserved
Normalized
Removed legitimately
Needs review
```

Format:

```text
S01 → ct-content-box.is-warning → Converted → PASS
S02 → nested is-simple support relation → Preserved/Normalized → PASS
S03 → ul/li + strong peer list → Converted → PASS
S04 → decorative separator → Removed legitimately → PASS
S05 → unsafe relative href removed; text preserved → Needs review
S06 → official issuer↔authority pair → Converted → PASS
S07 → two signatory parties → Converted → PASS
S08 → single signer anchored right in source → one-party ct-signature-grid → Converted → PASS
S09 → coherent tax form scope → section.ct-official-document containing its form-owned children → Converted → PASS
S10 → article H2/warning ABOUT form → remains outside official scope → Preserved → PASS
S11 → printed centered form title → ct-align-center inside official scope → Converted → PASS
S12 → right-aligned unit line → ct-align-right inside official scope → Converted → PASS
```

No inventory item may disappear without explanation.

Calculate:

```text
SOURCE COVERAGE
= reconciled inventory items / total inventory items
```

Completion requires **100%**. Needs-review item still counts as reconciled when explicitly accounted for.

---

# 30. Independent fidelity audit

Inventory coverage does not prove fidelity. Run these checks separately.

## Visible text

Compare normalized source visible text vs canonical visible text after allowing only legitimate presentation-only removals such as manual list markers, decorative separators, empty layout paragraphs, truly layout-only shells and unsafe href attributes while preserving visible text.

Do not over-normalize away real differences.

Report when practical:

```text
Normalized source visible text:    N characters
Normalized canonical visible text: N characters
Result: PASS / REVIEW / FAIL
```

## Heading

- body H1 = 0;
- major sections = H2;
- valid H2/H3/H4 hierarchy;
- opening meaningful text not silently lost;
- article heading ABOUT a form is not automatically swallowed into printed form scope.

## Lists

- peer item count preserved;
- no `• -` double marker;
- no peer family wrongly converted to definition list.

## Callouts / sanitizer

For every `ct-content-box`:

- root canonical `div` in new output;
- exactly one semantic variant;
- title if present = `p.ct-content-box__title`;
- body = `div.ct-content-box__body`;
- no source title invented;
- no new legacy `aside/blockquote` root;
- no `div.ct-content-box__title`.

If callout is adjacent to a formal form, verify source ownership. An editorial warning ABOUT the form remains outside when source proves it is not printed/form-owned.

## Accounting

- every explicit Nợ/Có preserved;
- side correct;
- codes/amounts unchanged;
- no invented title.

## Tables — every table

Verify:

- semantic classification justified;
- **structurally simple 2–4-column matrices are not over-promoted to `is-complex` merely because they have four columns, many rows, or longer prose cells**;
- 5+ columns are strong complex cue, not automatic override of stronger structural evidence;
- visible cell text preserved;
- row/cell order preserved;
- meaningful blank cells preserved;
- form-slot exact slots preserved;
- populated 10+ row not misclassified form-slot;
- genuine `thead` rows preserved;
- exact `rowspan/colspan` preserved;
- terminal leaf semantics not invented;
- Type B association preserved;
- Type C 2–4-column simple matrices remain simple when no complex cue exists;
- Type D structure/spans preserved;
- child did not reclassify parent;
- no nested `ct-table-scroll` inside cells;
- no invented width/min-width/scroll markup;
- form-owned tables remain inside justified coherent official-form scope;
- official-document contextual visual mode did not cause semantic reclassification or new presentation class.

Meaningful depth >1 or malformed spans cannot receive automatic full PASS.

## Links/media

- no invented URL/media destination;
- unsafe relative URL not silently rewritten;
- visible link text preserved;
- removed media/link migration reported.

## Positional fidelity — MANDATORY v1.1.3 gate

For every positional `Sxx` verify:

```text
all visible text preserved
AND
same semantic groups/parties preserved
AND
source order preserved
AND
issuer ↔ authority relation preserved when present
AND
signatory/approval/confirmation parties remain distinct
AND
single-signature side anchoring preserved when source clearly encodes it
AND
party text remains in correct party
AND
no semantic pair serialized into unrelated prose
AND
canonical positional classes survive sanitizer/editor
```

For source-backed single signer anchored right:

```text
one signer remains one signer
blank companion is not invented as a fake party
signer region is not flattened into full-width centered prose
one-party ct-signature-grid is used only when right-side anchor is source-backed
```

**If all words remain but meaningful left/right, single-signer side anchor or party/group relationship is lost → FAIL — FIX BEFORE PUBLISH.**

## Formal Form Scope Fidelity — MANDATORY when cues exist

For every coherent formal-form region verify:

```text
exact source-backed printed form start/end preserved
article H2/lead-in ABOUT form remains outside when not printed/form-owned
editorial warning/note ABOUT form remains outside when not printed/form-owned
printed form title/code remains in scope
coded fields remain in scope
form-slot grids remain in scope + structurally intact
simple/complex form tables remain in scope + keep own semantic classification
form-owned unit/legend/declaration remains in scope
signature/approval region remains in scope
form pieces are not emitted as unrelated article-root siblings
ct-official-header is not invented when absent
editorial commentary / related-content after form remains outside
```

**Child tables/signatures correct but coherent formal-form boundary lost → FAIL — FIX BEFORE PUBLISH.**

**Editorial ABOUT-form material swallowed into official scope despite clear source boundary → FAIL — FIX BEFORE PUBLISH.**

## Formal Alignment Fidelity — MANDATORY when evidence exists

For each meaningful source-backed alignment verify:

```text
printed formal title centered in source → ct-align-center when formal identity depends on it
unit/currency line right-aligned to following matrix → ct-align-right when edge association is source-backed
official date/place/role alignment → preserved when position carries meaning
signature/approval position → preserved through positional component/alignment contract
existing canonical ct-align-* only
no inline style / invented visual class
no meaningless decorative alignment preserved mechanically
```

**All words remain + clear source-backed formal identity/edge association lost → FAIL — FIX BEFORE PUBLISH.**

If source certainty is insufficient, preserve safest supported alignment + REVIEW rather than guess.

## Sanitizer-oriented QA

```text
No inline style
No body H1
No arbitrary classes/data-*
No scripts/iframes/forms/event handlers
Canonical classes only
Canonical content-box tags in new output
Supported table tags/attributes only
No guessed unsafe URL
Positional classes only on supported tags
Formal form scope uses existing section.ct-official-document only
Formal alignment uses existing ct-align-left/center/right only
```

---

# 31. Runtime output contract

## Staged mode — preferred production 5-prompt workflow

Current step prompt controls output and stop point.

```text
STEP 1
→ Source Semantic Inventory only

STEP 2
→ Transform Plan / readiness only

STEP 3
→ EXACTLY ONE fenced code block labelled html
→ INSIDE the fence: Canonical HTML ONLY
→ OUTSIDE the fence: NO text
→ NO preliminary notes
→ NO final reconciliation
→ NO PASS/FAIL declaration
→ NO explanatory HTML comments
→ code fence = transport wrapper only; it is NOT part of Canonical HTML artifact

STEP 4
→ Inventory Reconciliation + Fidelity/Structural/Positional/Form-Scope/Formal-Alignment QA + Final Result

STEP 5 conditional
→ Repair Summary + full Revised Canonical HTML + Remaining Needs Review
→ NO final PASS declaration
→ then return to STEP 4
```

Do not emit future-step artifacts early merely because this skill describes whole workflow.

## Single-run mode

Only when explicitly asked to perform full run in one turn, produce three logical outputs:

### A. Canonical HTML
Only transformed article body HTML.

### B. Inventory Reconciliation

Include:

- total inventory items;
- reconciled items;
- Source Coverage percentage;
- one entry per `Sxx`.

### C. Conversion / QA Report

Use:

```text
Converted
Removed
Needs review
Semantic inventory / counts
Visible-text fidelity audit
Heading audit
Emphasis/callout audit
List audit
Accounting audit
Table audit
Links/media audit
Positional fidelity audit
Formal-form scope audit
Formal-alignment fidelity audit
Sanitizer-oriented QA
Final result
```

Do not describe speculative CSS behavior as transform decisions.

---

# 32. Step-5 minimal repair contract

Step 5 is a **REPAIR PASS**, not rewrite pass.

Inputs:

1. Source;
2. fixed Source Semantic Inventory;
3. this Compact Skill;
4. current Canonical HTML;
5. full Step-4 QA report;
6. Required Corrections when present.

Classify issues:

### A. FIXABLE TRANSFORM ERROR

Examples:

- omitted source paragraph;
- wrong heading level;
- wrong list structure;
- missing semantic emphasis;
- wrong callout;
- wrong Nợ/Có;
- missing item/cell;
- wrong rowspan/colspan;
- wrongly flattened nested table;
- form-slot error;
- **structurally simple 4-column table over-classified as complex without another complex cue**;
- relative URL modified;
- arbitrary class/inline style;
- unsupported markup;
- official header serialized into prose;
- signature parties merged/lost;
- source-backed single signer anchored right transformed into full-width centered signature/prose;
- coherent formal form fragmented into sibling fields/tables/declaration/signature instead of one source-backed `ct-official-document` scope;
- article H2/lead-in/editorial warning ABOUT form incorrectly wrapped inside official scope;
- source-backed printed form title loses center alignment;
- source-backed unit/date line loses meaningful right/edge alignment.

→ must repair minimally.

### B. SOURCE AMBIGUITY / EXTERNAL MIGRATION ISSUE

Examples:

- possibly outdated law;
- source typo;
- missing CMS title metadata;
- relative URL/media migration;
- malformed table insufficient evidence;
- nested depth >1 requiring human review;
- ambiguous official role naming without enough source evidence;
- ambiguous single-signature placement where source does not clearly establish side anchor;
- ambiguous exact start/end of suspected formal form;
- ambiguous whether centered/right alignment is semantically meaningful versus decorative.

→ do not “fix” source; preserve safest structure/alignment + Needs review.

Minimal Repair Principle:

1. reread full Source;
2. reread relevant Sxx;
3. reread corresponding rule;
4. reread QA finding;
5. locate exact canonical fragment;
6. change smallest necessary region;
7. do not touch already-PASS regions;
8. regression-check related semantic regions;
9. output full revised Canonical HTML after all fixable repairs.

For positional repair:

```text
Source + Inventory stay fixed
→ restore missing official/signature grouping from source evidence
→ for source-backed right-side single signer, use one-party ct-signature-grid without fake blank party
→ preserve wording, source order and party membership exactly
→ do not invent role text/name/date/stamp
→ return revised HTML to Step 4
```

For formal-form boundary repair:

```text
Source + Inventory stay fixed
→ identify exact printed/form-owned start/end
→ move editorial ABOUT-form H2/warning/lead-in outside when source proves they are not printed
→ wrap only form-owned range in section.ct-official-document
→ keep existing child table/form-slot/signature semantics intact
→ keep post-form Xem thêm/commentary outside
→ do not invent ct-official-header or missing form metadata
→ return revised HTML to Step 4
```

For formal-alignment repair:

```text
Source + Inventory stay fixed
→ restore only clearly source-backed meaningful alignment
→ use existing ct-align-left/center/right on supported element
→ do not invent text/style/class
→ do not preserve unrelated decorative alignment
→ return revised HTML to Step 4
```

Never repair one issue by rewriting prose, changing data, changing already-PASS blocks, changing simple↔complex for aesthetics or adding decoration.

Same repair failure repeated ~2–3 times → stop automatic repair, human review.

---

# 33. Final PASS gate

Complete only when:

```text
Source Semantic Inventory exists
Source Coverage = 100%
Body H1 = 0
Visible meaning preserved
No unexplained inventory item disappeared
Heading hierarchy valid
Peer lists not over-classified
Emphasis/callouts based on meaning, not paint
Every new content box uses div root + optional p title + div body
Every new content box has exactly one semantic variant
No new aside/blockquote content-box root remains
Accounting sides preserved
Every table classified before flattening
Structurally simple 2–4-column matrices are not over-promoted to complex solely because of column count/row count/long prose
Meaningful blank form slots preserved
Populated wide rows not misclassified form-slot
Header rows/spans preserved
Nested relations preserved
Parent/child table semantics independent
No transform decision depends on horizontal scroll
Links/media not guessed
No inline style / arbitrary class/data-*
Official-document semantics used only when source supports them
Coherent formal forms preserve one justified ct-official-document scope across printed/form-owned title/fields/tables/declaration/signature
Article H2/lead-in/editorial warning ABOUT form remains outside when source does not make it printed/form-owned
Unrelated article prose/related-content is not swallowed into formal-form scope
ct-official-header is not invented for headerless forms
Source-backed formal alignment is preserved with existing ct-align-* when meaning-bearing
Official issuer↔authority grouping preserved
Signature party count/order/membership preserved
Source-backed single-signature side anchoring preserved when present
No fake blank signature party invented
No meaningful positional relationship/formal-form scope/formal alignment serialized away
Official-document contextual table presentation does not alter semantic classification
Sanitizer compatibility expected
Needs-review items explicit
```

If non-reviewable fidelity condition fails:

```text
FAIL — FIX BEFORE PUBLISH
```

If fidelity passes but genuine source ambiguity remains:

```text
PASS WITH NEEDS REVIEW
```

Conditional repair:

```text
STEP 4 = PASS
→ STOP

STEP 4 = PASS WITH NEEDS REVIEW
→ do not run STEP 5 merely to force PASS
→ resolve only through human/external review when appropriate

STEP 4 = FAIL with clearly fixable transform error
→ STEP 5 minimal repair
→ preserve Source + Inventory as fixed baselines
→ output full revised HTML
→ RETURN TO STEP 4
```

---

# 34. Runtime decision card

```text
OPENING
exact duplicate title?        → remove only with metadata
meaningful title-like opening → ct-article-intro
body H1                       → never

EMPHASIS
ordinary local emphasis        → strong
long scan-worthy clause        → ct-key-emphasis
short decisive condition       → ct-key-highlight
compact process/formula/result → ct-key-line
whole semantic block           → ct-content-box

CALLOUT MARKUP
root                           → div.ct-content-box + exactly one variant
optional source-backed title   → p.ct-content-box__title
body                           → div.ct-content-box__body
new aside/blockquote root      → forbidden; normalize before PASS
zero/conflicting variants      → FAIL transform QA; do not guess

LISTS
peer members                   → ul/li + strong
completion/check items         → ct-checklist only when genuine
ordered procedure              → ct-steps only when genuine
term→definition                → ct-definition-list
concise key→value              → ct-fact-list

ACCOUNTING
explicit Nợ/Có                 → debit/credit
no source title                → never invent “Định khoản”

FORM SCOPE
coherent official/tax form     → one section.ct-official-document scope
ABOUT form                     → article H2/lead-in/editorial warning/commentary stays outside unless source proves printed ownership
OF form                        → printed form title/fields/slots/matrix/declaration/signature inside scope
form start/end                 → exact source-backed boundary
headerless formal form         → official-document allowed; do NOT invent ct-official-header
post-form Xem thêm             → outside unless truly form-owned
child tables/signatures        → keep own semantics inside scope

FORM ALIGNMENT
printed form title centered    → ct-align-center when source-backed identity requires it
unit/date line right/edge      → ct-align-right when source-backed association requires it
decorative alignment only      → normalize away
uncertain meaningful alignment → safest supported alignment + review

POSITION
meaningful left/right grouping → preserve/map before cleanup
official issuer↔authority      → ct-official-header when evidence supports roles
multiple signatories/approvers → ct-signature-grid
single signer anchored right   → one-party ct-signature-grid when source clearly encodes right-side anchor
single signer, no side evidence→ ordinary grouped prose / safest structure
plain layout with no relation  → unwrap allowed

TABLE
truly layout-only              → unwrap
form-slot                      → label + blank slots stay tbody
simple 2–4 col matrix          → prefer is-simple when structure/header are simple
5+ col / span / header tree    → strong is-complex cue
4 columns alone                → NOT a complex cue
inside official document       → same semantic class; CSS formal-neutral context only
nested support 1×2/1×3         → nested is-simple; no child wrapper
nested small 2–4 col matrix    → nested is-simple; remain table
nested complex                 → nested is-complex; no child wrapper
rowspan/colspan                → preserve exact values
wide table                     → fit-only; transformer makes no scroll decision

LINK/MEDIA
unsafe relative path           → do not guess destination

AMBIGUOUS
preserve content + relationship/scope/alignment → Needs review

FINAL
reconcile every Sxx → coverage 100% → independent fidelity audit
text preserved but relation/form scope/clear formal alignment lost → FAIL
```

---

# 35. Version binding

Compact runtime **v1.1.3** is synchronized to:

```text
ktd-editorial-html-transform v1.4.3
EDS v2.4.3
```

### What v1.0.2 already contained and v1.1.3 retains

- complete Source Semantic Inventory contract;
- opening/H1 rules;
- inline emphasis ladder;
- source note/callout/key-line semantics;
- peer-list/checklist/steps/definition/fact rules;
- accounting rules;
- media/FAQ/related-content rules;
- table layout/form-slot/simple/complex classification;
- fit-only table invariant;
- table integrity;
- form-slot negative rules;
- header/span hierarchy;
- nested Type A/B/C/D;
- depth/locality;
- safe-link categories and relative-URL no-guess rule;
- media migration rule;
- presentation-only removal;
- sanitizer/security contract;
- canonical whitespace;
- ambiguity policy;
- inventory reconciliation;
- visible-text/table/link/media/sanitizer QA;
- staged + single-run output contracts;
- final PASS + conditional repair loop.

### What v1.1.1 added / clarified and v1.1.3 retains

- meaningful positional precedence;
- Official Document / Official Header;
- Signature Grid / Signature Party;
- source-backed single-signature side-anchor preservation using one-party Signature Grid when appropriate;
- removal of blanket `signature layout → unwrap` shortcut;
- Step-1 positional inventory requirements;
- Step-4 blocking positional fidelity audit;
- Step-5 positional minimal repair;
- synchronized Step-3 HTML-only production contract with a single fenced `html` transport wrapper;
- simple-table tuning: structurally simple 2–4-column matrices are preferred as `is-simple`; 5+ columns become strong column-count cue for `is-complex`; four columns/many rows/long prose alone do not force complex classification.

### What v1.1.2 added and v1.1.3 retains

- **Formal Form Scope Detection** before child-table normalization;
- inventory cues/relations for form title/code, coded fields, form slots, matrices, units/legends, declarations and signatures;
- one `section.ct-official-document` scope for coherent administrative/tax forms;
- child table/signature semantics remain independent inside scope;
- headerless forms do not invent `ct-official-header`;
- article lead-in/commentary/related-content stay outside unless source-owned by form;
- Step-4 blocking Formal Form Scope Fidelity audit;
- Step-5 minimal repair for fragmented/over-wrapped form scopes;
- no new class or sanitizer permission.

### What v1.1.3 adds

- explicit **ABOUT-form vs OF-form boundary gate**, including article H2/lead-in/editorial warning exclusions when they are not printed/form-owned;
- exact source-backed form start/end becomes blocking scope fidelity;
- **Formal Alignment Fidelity** using existing `ct-align-left/center/right`, including centered printed form title and right-aligned unit/date edge association when source-backed;
- negative rule against preserving every legacy alignment mechanically;
- official-document contextual table/form-slot/signature-zone presentation is explicitly CSS-owned and cannot change `is-simple/is-complex` semantics;
- Step-4/Step-5 guards for over-wrap, lost meaningful alignment and semantic reclassification for aesthetics;
- no new HTML class or sanitizer permission.

**Compact v1.1.3 is intentionally a full runtime contract, not a shortened summary of prior versions.**

---

# 36. Final runtime principle

> **New capability is additive. Preserve the complete mature transform guardrails, then add new semantics. Never trade fidelity for shorter instructions. Preserve exact source-backed document/form boundary, distinguish ABOUT from OF, preserve meaningful formal alignment only when evidence supports it, and let CSS own contextual official-document presentation.**