# KTD Editorial HTML Transform Skill

**Skill name:** `ktd-editorial-html-transform`  
**Project:** Kế Toán Diệu Tâm  
**Version:** 1.4.3  
**Status:** Canonical transformation skill  
**Mode:** FORMAT-ONLY SEMANTIC TRANSFORMATION

## 1. Purpose

Transform legacy accounting/tax/legal HTML into canonical semantic HTML compatible with the Kế Toán Diệu Tâm Editorial Design System (**EDS v2.4.3 — full-contract additive upgrade**) and the editorial sanitizer.

This skill is for **presentation and semantic normalization only**.

It must preserve:

- factual content;
- meaningful visible text;
- item boundaries;
- table-cell associations;
- row/column/header/span relationships;
- meaningful blank form slots;
- semantic group membership;
- meaningful positional relationships such as issuer↔authority and signatory↔signatory;
- source-backed single-signature side anchoring when placement itself carries meaning;
- coherent formal-document/form scope when title/field/table/declaration/signature regions jointly belong to one bounded official form;
- exact source-backed boundary between editorial material **about** a document/form and printed/official content **of** that document/form;
- source-backed formal alignment when alignment preserves document identity, edge association, official role/date/unit placement or signature relationship.

### Canonical references

1. `docs/21-content-editorial-design-system.md` — canonical EDS v2.4.3 reference;
2. `transformation-spec.md` — transformation/classification contract;
3. `canonical-examples.md` — canonical examples;
4. `nested-table-fixtures.md` — mandatory table/nested-table regression fixtures;
5. `content-box-sanitizer-fixtures.md` — content-box/sanitizer fixtures;
6. `positional-semantic-fixtures.md` — official-document/signature/form-scope regression fixtures;
7. `qa-checklist.md` — completion gate;
8. `FULL_REFERENCE_INDEX.md` — frozen full pre-hardening references for unchanged detail.

The skill owns semantic HTML decisions only. CSS owns typography, colors, widths, density, gridlines, wrapping, responsive stacking and other visual presentation. Contextual table presentation inside `ct-official-document` is CSS-owned and must never change `is-simple/is-complex` classification.

---

## 2. Primary rule

> Nội dung quyết định semantic.  
> Semantic quyết định component.  
> CSS quyết định presentation.  
> HTML không tự trang trí.  
> Không xóa nội dung có nghĩa chỉ để sửa hierarchy.  
> Không đổi peer-items thành glossary chỉ vì label đậm.  
> Không flatten nested table nếu row/cell boundary mang nghĩa.  
> Không flatten positional layout nếu left/right/group membership mang nghĩa.  
> **Mọi editorial table phải fit 100% viewport; transformer không quyết định scroll.**  
> **Form-slot field label không được tự biến thành column header chỉ để “semantic hóa” table.**  
> **Complex table header hierarchy phải preserve theo source; AI không tự chọn màu/tint cho header.**  
> **Nested child complexity không được dùng để reclassify hoặc mutate parent table semantics.**  
> **Canonical content box dùng một cấu trúc duy nhất: `div.ct-content-box`, optional `p.ct-content-box__title`, và `div.ct-content-box__body`.**  
> **Meaningful positional relationship > generic layout-only cleanup.**  
> **Coherent formal-form scope > fragment-by-fragment normalization when source proves the pieces belong to one bounded official unit.**  
> **Editorial material ABOUT a document/form ≠ printed/official content OF that document/form.**  
> **Source-backed formal alignment is preserved only when it carries formal identity/relationship; aesthetics alone never justify alignment classes.**

Legacy paint is evidence to inspect, never a direct semantic mapping.

---

## 3. Non-negotiable fidelity

Do **not**:

- rewrite/improve/summarize/shorten/expand source wording;
- add/remove factual knowledge;
- collapse separate source items;
- detach a description from its correct label;
- flatten meaningful left/right, row/column, issuer/authority, signer/signer or party/party relationships;
- flatten a source-backed right-side single-signature anchor into a page-centered signature block;
- fragment a coherent formal tax/administrative form into unrelated article-root siblings when source evidence shows one form scope;
- swallow unrelated article lead-in, article heading, editorial warning/note, commentary or related-content into an official form merely because it is adjacent in legacy markup;
- treat an article heading that names/describes a form as printed form content without source ownership evidence;
- strip source-backed centered/right formal alignment before deciding whether it preserves form title identity, unit/date edge association or another formal relation;
- preserve every `text-align` mechanically just because source contains it;
- merge/split meaningful table cells without source evidence;
- remove meaningful empty form cells merely because they contain no visible text;
- convert form-slot field labels/blank character slots into a fake header/data matrix;
- classify any populated one-row 10+ cell matrix as form-slot merely because it is wide;
- flatten genuine multi-row table headers merely to simplify markup;
- invent additional header rows just to obtain a visual hierarchy;
- infer that a terminal header row means “code/index” merely because it is last;
- reclassify simple↔complex merely to obtain a preferred header color/width or official-document palette;
- over-promote a structurally simple 2–4-column matrix to complex solely because it has four columns, many rows or longer prose cells;
- let a nested child table’s column count/span structure alter semantic classification of parent;
- treat “signature layout” as blanket presentation-only structure;
- serialize official-document header pairs into ordinary prose when role grouping matters;
- merge distinct signatories/approvers into one undifferentiated prose sequence;
- invent a fake blank signature party merely to recreate source spacing;
- invent `ct-official-header` for a formal form that has no issuer↔authority header pair;
- create a separate “signature card” class/frame to compensate for missing formal-form scope;
- emit new content boxes as `aside.ct-content-box` or `blockquote.ct-content-box`;
- emit `div.ct-content-box__title` for new canonical output;
- change dates, amounts, percentages, account codes/names, formulas or Nợ/Có meaning;
- update laws/legal citations;
- infer facts not present;
- invent URLs/images/headings/citations;
- invent names, signatory roles, stamps, quốc hiệu, issuing authority, document number or dates;
- turn ordinary legal prose into `ct-official-document` merely because it cites law.

If source looks wrong/outdated/contradictory, preserve and report **Needs review**.

---

## 4. Input / output + orchestration compatibility

Input:

- legacy HTML/text;
- optional source URL/metadata;
- article title metadata when available;
- Source Semantic Inventory in staged mode.

Canonical skill supports two execution modes.

### Direct canonical mode

Core deliverables:

#### A. Canonical HTML
Only transformed article HTML.

#### B. Conversion / QA Report

- Converted;
- Removed;
- Needs review;
- fidelity checks;
- structural/table checks;
- positional/form-scope/formal-alignment checks;
- sanitizer checks.

### Inventory-controlled staged mode

Used by Compact Skill and 5-prompt workflow:

```text
STEP 1  observe source before EDS mapping
        → Source Semantic Inventory

STEP 2  read skill + prepare transform plan

STEP 3  transform
        → Canonical HTML only in the current employee workflow

STEP 4  reconcile every inventory item + independent QA
        → PASS / PASS WITH NEEDS REVIEW / FAIL

STEP 5  only when STEP 4 finds a fixable transform error
        → minimally repair HTML
        → rerun STEP 4
```

Rules:

- Source Semantic Inventory = **evidence checklist, not answer key**;
- do not change inventory merely to make transformed HTML appear correct;
- every `Sxx` must be reconciled before final PASS;
- Source Coverage must be `100%` in inventory-controlled mode;
- current step prompt controls artifact emitted and stop point;
- Step 3 must not prematurely run Step-4 QA or declare PASS;
- current production 5-prompt workflow requires Step 3 **exactly one fenced `html` code block; inside the fence is Canonical HTML only and outside the fence is no text**;
- the fence is a transport wrapper for copyability, not part of the Canonical HTML artifact;
- Step 5 never declares final PASS; repaired HTML returns to Step 4;
- if same repair failure repeats ~2–3 times, stop automatic repair and require human review.

Single-run inventory-controlled implementation may bundle:

```text
A. Canonical HTML
B. Inventory Reconciliation
C. Conversion / QA Report
```

when explicitly asked to perform a full single run.

---

## 5. Source Semantic Inventory contract

Use stable IDs `S01`, `S02`, ... in source order.

```text
Sxx
Location:
Source excerpt / structure:
Evidence:
Probable role: neutral natural-language role, NOT EDS class
Relations:
Confidence: high | medium | low
Risk:
```

Inventory signals include:

- title-like first block / oversized heading;
- real/fake headings;
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
- every table, layout table and form-slot grid;
- nested tables;
- multi-row headers, `rowspan`, `colspan`;
- meaningful blank cells;
- links/images/media;
- decorative separators/empty spacers;
- FAQ/related-content/checklist/step patterns;
- official-document structure;
- **formal-form scope cues:** form/template title, “Mẫu”, “Phụ lục”, form code/reference, coded fields such as `[01]...[NN]`, segmented form slots, administrative data matrix, units/legends, declaration/certification, signature regions and legacy wrappers connecting them;
- **boundary ownership cues:** article heading/callout ABOUT the form vs printed/form-owned title/fields OF the form;
- **formal-alignment cues:** centered printed form title, right-aligned unit/date line, issuer/authority alignment, signature/approval positioning or other source-backed alignment whose removal could change document identity/edge association;
- signature/approval/confirmation regions;
- single-signature layouts where blank/unused companion space or column geometry clearly anchors the signer to one side;
- anything whose meaning may disappear when presentation markup is stripped.

For positional/scope structures, `Relations` should explicitly capture where present:

```text
left ↔ right
issuer ↔ authority
party A ↔ party B
signer ↔ signer
single signer ↔ source-backed right-side anchor
formal form scope ↔ title/fields/form-slots/tables/declaration/signatures
editorial ABOUT-form material ↔ outside formal scope
printed form title ↔ centered formal identity
unit/date line ↔ source-backed edge alignment
label ↔ explanation
heading ↔ content
header ↔ data
parent ↔ child
account entry ↔ explanation
```

Do not inventory only colorful content. Plain structural, positional, boundary and formal-alignment relationships matter too.

---

## 6. Canonical body vocabulary

Allowed semantics include:

- `p`, `h2`, `h3`, `h4`, `strong`, `em`, `blockquote`, `ul`, `ol`;
- `p.ct-align-left/.ct-align-center/.ct-align-right` when source-backed alignment fidelity requires it;
- `p.ct-article-intro`;
- `span.ct-key-emphasis`;
- `mark.ct-key-highlight`;
- `p.ct-source-note`;
- `.ct-checklist`, `.ct-steps`;
- `div.ct-content-box.is-note/.is-info/.is-warning/.is-legal/.is-example`;
- optional `p.ct-content-box__title` + `div.ct-content-box__body`;
- `.ct-key-line.is-formula/.is-process/.is-result`;
- `.ct-accounting-entry`, `.ct-accounting-group` family;
- `.ct-definition-list`, `.ct-fact-list`;
- `.ct-data-table.is-simple/.is-complex`, `.ct-table-scroll`;
- `.ct-editorial-media`, `.ct-faq`, `.ct-related-content`;
- `section.ct-official-document`;
- `div.ct-official-header`;
- `div.ct-official-header__issuer`;
- `div.ct-official-header__authority`;
- `div.ct-signature-grid`;
- `div.ct-signature-party`.

Formal Form Scope Detection and Official Document Table Presentation **do not add a class**. The former decides which contiguous source-backed range belongs inside existing `section.ct-official-document`; the latter is CSS ancestor-context presentation only.

Do not invent generic `ct-two-col`, `ct-left`, `ct-right`, `ct-document-card`, `ct-form-card`, `ct-signature-box`, `ct-official-table`, `is-government` or arbitrary presentation classes.

---

## 7. Canonical content-box contract

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

- root = `div.ct-content-box` + exactly one `is-note/is-info/is-warning/is-legal/is-example`;
- title only when source actually has one = `p.ct-content-box__title`;
- body wrapper = `div.ct-content-box__body`;
- if source has no standalone title/label, omit title; do not invent text;
- forbidden in new output: `aside.ct-content-box`, `blockquote.ct-content-box`, `div.ct-content-box__title`;
- sanitizer may preserve legacy shapes for migration compatibility, but transformer normalizes them;
- root with zero/multiple variants fails transform QA;
- do not invent missing variant or arbitrarily choose a winner.

This intentionally removes an unnecessary AI decision: AI chooses only whether block is a content box and which semantic variant applies; it never chooses root tag.

---

## 8. Transformation workflow

1. Read entire source and inventory.
2. Classify title-like first block.
3. Determine heading rebase separately.
4. Identify true section tree.
5. Identify presentation-only markup and meaningful legacy emphasis.
6. **Identify meaningful positional structures before generic layout cleanup.**
7. **Detect coherent formal-document/form scope before classifying its child tables independently.**
8. **Run ABOUT-vs-OF boundary gate: separate editorial introduction/heading/warning/commentary from printed/official form-owned content.**
9. **Run Formal Alignment Fidelity gate before stripping source alignment in official/form regions.**
10. Identify official-document/header and signatory/approval groups, including source-backed single-signature side anchoring, when source supports them.
11. Normalize headings/prose/lists/callouts/inline semantics.
12. Normalize every content box to canonical `div/p/div` contract.
13. Normalize accounting and genuine definition/fact structures.
14. Classify every top-level and nested table recursively before flattening.
15. Detect segmented form-slot grids before generic matrix/header normalization; require actual slot evidence.
16. Preserve genuine table header hierarchy including meaningful `thead`, `rowspan`, `colspan`.
17. Apply table integrity + nested Type A/B/C/D rules; do not reason about scroll/header colors/official palette.
18. Treat each table as independent semantic scope; child density/spans do not mutate parent.
19. Map supported official/signature positional relations to canonical positional components **inside the preserved formal-document scope when applicable**.
20. Preserve source-backed meaningful formal alignment with existing `ct-align-*` classes only when evidence justifies it.
21. Normalize links/media/FAQ/related-content.
22. Strip presentation-only markup only after relationship, scope, boundary and alignment classification.
23. Clean source whitespace.
24. In staged mode, stop after current prompt artifact; no later-stage approval early.
25. If inventory present, reconcile every `Sxx`, require Source Coverage `100%`.
26. Run independent fidelity audit: text, headings, lists, callouts, accounting, tables, links/media, positional/form-scope/boundary/alignment semantics, sanitizer.
27. Produce QA report when current orchestration asks for it.

---

## 9. Article title root / intro / H1

Body never contains H1.

```text
CMS title metadata available?
  exact/no-information duplicate
    → remove + report

  overlaps title but adds meaningful scope/context
    → preserve FULL source text as p.ct-article-intro

  not duplicate
    → preserve/classify normally

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
- an article H2 that introduces/names an official form is **not automatically printed form content**; formal-form ownership is a separate boundary decision.

---

## 10. Legacy presentation removal

Remove after semantic classification:

- inline style;
- font face/size markup;
- `mso-*` and Office-only classes;
- redundant spans;
- visual-only colors/backgrounds;
- presentation-only fixed table widths/heights/cellpadding/cellspacing;
- manual bullets replaced by semantic list markers;
- empty spacer paragraphs;
- decorative separators;
- truly layout-only table shells.

Before stripping legacy emphasis, decide whether meaning survives as:

```text
plain prose
strong
ct-key-emphasis
ct-key-highlight
ct-key-line
ct-content-box
```

Legacy table background/text colors are presentation evidence only. EDS owns header treatments, including the contextual formal-neutral table mode inside `ct-official-document`.

Do not remove a source presentation artifact before deciding whether it encodes a relationship recorded in inventory. A blank signature companion cell may be removed only after its positional evidence has been mapped to the supported signature structure.

A legacy outer wrapper/table that groups a coherent formal form may be removed as implementation only **after** the form boundary has been preserved with `section.ct-official-document`.

A source `text-align:center/right` inside a formal document/form may be removed only after Formal Alignment Fidelity decides whether the alignment is meaningful. Meaningful alignment maps to existing `ct-align-center/right/left`; decorative alignment is normalized away.

---

## 11. Security / sanitizer compatibility

Output must survive `sanitizeEditorialHtml()` and TinyMCE canonical schema.

Never intentionally output:

```text
script
style
iframe
form/input controls
event handlers
arbitrary data-*
arbitrary classes
unsafe guessed URLs
```

Supported semantic table attributes such as valid `rowspan`, `colspan`, `scope` may survive.

Positional sanitizer contract:

```text
section → ct-official-document

div → ct-official-header
      ct-official-header__issuer
      ct-official-header__authority
      ct-signature-grid
      ct-signature-party
```

Formal-form scope reuses `section.ct-official-document`; no sanitizer class expansion is required.

Formal alignment reuses existing supported `ct-align-left/center/right` on allowed elements; do not emit inline style or arbitrary alignment classes.

`ct-official-document` and `ct-accounting-group` are mutually exclusive section-root semantics.

Sanitizer compatibility is a QA condition, not a license to emit malformed/noncanonical HTML and hope sanitizer fixes it.

---

## 12. Inline emphasis / source notes / callouts / key lines

Use smallest sufficient semantic:

```text
plain
→ strong
→ ct-key-emphasis
→ ct-key-highlight
→ ct-key-line
→ ct-content-box
```

- `strong`: ordinary local emphasis/label/term;
- `ct-key-emphasis`: longer scan-worthy phrase/clause;
- `ct-key-highlight`: short decisive condition/threshold/exception/timing/scope;
- do not highlight long paragraphs;
- do not nest key-emphasis/highlight; split ranges.

Legacy paint alone never decides semantics:

```text
red ≠ warning automatically
yellow/cyan background ≠ highlight automatically
blue ≠ heading automatically
green background ≠ example automatically
```

Short attribution:

```html
<p class="ct-source-note">(Theo Khoản ... Điều ...)</p>
```

Callout meanings:

```text
is-note    → insight/principle/key takeaway
is-info    → neutral additional information
is-warning → risk/error/penalty/caution
is-legal   → official/legal rule/requirement quotation
is-example → example/case/calculation scenario
```

Key lines:

```text
is-process → compact process/sequence
is-formula → compact calculation/formula/rule expression
is-result  → resolved conclusion/final answer/result
```

Use `is-legal` for substantive legal rule quotation, `ct-source-note` for short attribution. Do not use `is-legal` as a substitute for a full Official Document structure.

An editorial warning **about** a form may legitimately remain `ct-content-box.is-warning` **outside** `ct-official-document` when source evidence shows it is article/editorial material rather than printed content of the form.

---

## 13. Lists / checklist / steps / definitions / facts

### Peer members

Declared sibling families:

```text
“có N tài khoản cấp 2”
“gồm các loại/nhóm/trường hợp”
“bao gồm các khoản”
```

with parallel `bold label + description` → normal `ul/li + strong`.

Remove manual source marker (`-`, `•`, `ü`, `Ø`, `+`) when semantic list owns marker.

### Checklist

`.ct-checklist` only for genuine completion/verification items.

### Steps

`.ct-steps` only for ordered procedure/process where sequence matters. Otherwise normal `ol` or prose.

### Definition list

`.ct-definition-list` only for genuine:

```text
term/concept → definition
```

Bold label alone insufficient.

### Fact list

`.ct-fact-list` only for concise metadata-like key→value facts, not explanatory prose.

Ambiguous list vs definition → normal list/prose + review.

---

## 14. Accounting

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
- never invent visible “Định khoản”;
- related entries may use `.ct-accounting-group`;
- when table relation is primary, literal Nợ/Có may remain inside cells;
- preserve codes, amounts and order exactly;
- ambiguous Nợ/Có → neutral text/line + Needs review.

---

## 15. Other semantic structures

### Editorial media

Use `.ct-editorial-media` when valid source image/media survives sanitizer and semantic figure/caption is useful.

Do not invent width/alignment unsupported by source/context.

### FAQ

Use `.ct-faq` only for genuine question→answer material.

Do not turn ordinary headings into FAQ merely because they end with `?` unless source structure supports Q&A.

### Related content

Use `.ct-related-content` for genuine in-body related-resource block. Preserve visible title/type/summary/link semantics; never invent destination URLs.

Post-form `Xem thêm`/related content stays outside `ct-official-document` unless source clearly makes it part of the printed official unit.

---

## 16. Positional-semantic precedence gate — MUST RUN BEFORE UNWRAP

Before stripping a layout table/div/grid ask:

> If these regions become ordinary serial prose, will reader lose who belongs to which side/role/party, issuer↔authority, signer↔signer, whether a single signer is intentionally anchored to one side, label↔explanation, **whether several fields/tables/declarations/signatures jointly belong to one formal form**, whether adjacent material is editorial ABOUT the form rather than printed OF the form, or another meaningful parallel/opposed relationship?

```text
YES
→ not layout-only
→ preserve/map relation or scope

UNCERTAIN
→ preserve safest grouped structure
→ Needs review

NO
→ generic layout cleanup may proceed
```

Old table markup, fixed widths, centered/right alignment, spacer cells and Office classes do not answer this semantic question. A blank companion cell may contain no visible text but still provide evidence that the neighboring signer is intentionally anchored to one side.

A legacy outer table/div that links multiple form-owned regions may be presentation technology while still evidencing a meaningful formal-form boundary. Conversely, adjacency inside one legacy wrapper does not prove every neighboring editorial node belongs to the printed form.

---

## 17. Official Document + Formal Form Scope

Use `section.ct-official-document` only for a genuine formal/official document, declaration, administrative/tax form, notice, decision, dispatch/công văn or meaningful fragment.

Do not wrap ordinary explanatory prose solely because it discusses/cites law.

Presentation is CSS-owned. The canonical official-document root receives a restrained neutral outer frame and modest padding so an embedded formal document/form remains a bounded unit after legacy outer-table mechanics are removed. Tables inside receive contextual formal-neutral presentation without changing semantic class. This is not a license to create Official Document semantics from ordinary legal prose.

### 17.1 Formal Form Scope Detection

Detect the **whole formal-form scope before child-table classification** when source presents a coherent administrative/tax form.

Common cues:

```text
Mẫu / Phụ lục / form name / form code
“kèm theo ...” or official form reference
systematic coded fields such as [01], [02], [03]...
segmented character/digit slots
administrative data matrix / bảng kê
unit-of-measure line / legend / abbreviation note belonging to the form
declaration / certification / cam đoan
signature / approval / taxpayer / agent regions
legacy wrapper/table sequence linking those pieces
```

No mechanical cue quota. Decide from **coherence + boundary evidence**.

#### ABOUT vs OF boundary gate — v1.4.3

Before choosing FORM START, classify adjacent nodes as either:

```text
EDITORIAL / ARTICLE MATERIAL ABOUT THE FORM
or
PRINTED / OFFICIAL CONTENT OF THE FORM
```

Common ABOUT-form material that remains outside unless source proves printed/form ownership:

- article H2/H3 naming or introducing the form;
- editorial warning/note explaining replacement, effective date or usage;
- article lead-in/caption/intro;
- post-form `Xem thêm` / related-content / commentary.

Common OF-form start evidence:

- printed `Phụ lục` / formal form title block;
- official form code/title printed as part of the form;
- first clearly form-specific coded field when no separate printed title exists.

Canonical source-backed pattern for the 05-2/BK-QTT-TNCN case:

```text
article H2 describing the form               → OUTSIDE
editorial warning “Chú ý: mẫu này thay...”   → OUTSIDE
“Phụ lục / BẢNG KÊ...” printed form title   → FORM START
[01]...[NN] / slots / matrix / declaration  → INSIDE
signature parties                            → INSIDE / FORM END
Xem thêm                                     → OUTSIDE
```

If source instead proves a warning is printed as part of the official form, keep it inside. Ownership is source-backed, not keyword-based.

When evidence supports one form:

```text
START → source-backed printed form title / appendix title / first form-specific field
MIDDLE → fields + form slots + simple/complex matrices + form-owned notes/legend + declaration
END → signature/approval region or last clearly form-owned content
```

Keep outside the scope:

- article lead-in/explanation preceding the form;
- article heading that merely describes/introduces the form;
- editorial warning/note that comments on the form rather than belongs to it;
- editorial commentary following the form;
- “Xem thêm” / related-content after the form;
- ordinary prose not owned by the form.

Canonical pattern:

```html
<section class="ct-official-document">
  <!-- source-backed printed form title / coded fields -->
  <!-- form-slot/simple/complex tables keep own semantics -->
  <p>...</p><!-- declaration if source-backed -->
  <div class="ct-signature-grid">
    <div class="ct-signature-party">...</div>
    <div class="ct-signature-party">...</div>
  </div>
</section>
```

Rules:

1. `ct-official-document` owns the **form boundary**, not each child’s presentation.
2. Child tables still classify independently as form-slot/simple/complex.
3. Signature Grid still owns party grouping.
4. `ct-official-header` is **optional**; do not invent it for forms without issuer↔authority pair.
5. Do not invent national heading/agency/date to make form look official.
6. Do not add a separate signature card/frame inside an already bounded official form.
7. Do not lose the form scope just because legacy source used sibling tables/divs instead of one semantic wrapper.
8. If boundary is uncertain, preserve the safest contiguous formal fragment + Needs review; do not fragment clearly related form-owned pieces.
9. **Under-wrap** (form-owned child outside) and **over-wrap** (editorial ABOUT-form node inside) are both fixable fidelity failures when source boundary is clear.

A canonical anti-regression case is a tax form with article heading/warning outside → printed form title/code → `[01]...[NN]` fields → taxpayer-ID form-slot → complex matrix → right-aligned unit line → declaration → two-party signature → post-form `Xem thêm` outside. Correct child components alone are **not sufficient** if the outer formal-form boundary or source-backed alignment is lost.

### 17.2 Source-backed Formal Alignment Fidelity

Before stripping `text-align` inside a genuine official document/form ask:

> Does this source alignment preserve formal document identity, edge association, official role/date/unit placement, signature relationship or another positional meaning that would be weakened if normalized to ordinary left prose?

```text
YES
→ preserve using existing canonical ct-align-left / ct-align-center / ct-align-right on a supported element

UNCERTAIN
→ preserve safest supported alignment/grouping
→ Needs review

NO
→ strip legacy alignment; let normal CSS flow own presentation
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

Also inspect source-backed place/date, issuer/authority and certification/signature alignment where position carries meaning.

Do **not** preserve every centered/right legacy line. Aesthetic centering, spacer alignment and arbitrary visual styling still normalize away. Do not invent `ct-form-title`, `ct-unit-right`, `ct-official-center` or inline style.

### 17.3 Official header

Typical source:

```text
issuer / document number  ↔  national/authority heading / motto / place-date
```

Canonical:

```html
<section class="ct-official-document">
  <div class="ct-official-header">
    <div class="ct-official-header__issuer">
      <p>...</p>
    </div>
    <div class="ct-official-header__authority">
      <p>...</p>
    </div>
  </div>
  ...
</section>
```

Rules:

- preserve exact visible text/internal order;
- preserve two role groups;
- source 1×2 table used for this layout may be replaced after relationship classification;
- do not serialize groups into unrelated prose;
- do not invent missing authority/document/date text;
- do not use `is-legal` as document-header substitute;
- if relation clear but role naming ambiguous, preserve relation + Needs review rather than guessing.

Official document/form body can contain recipient, paragraphs, legal citations, coded fields, form slots, tables, legends, declaration and signature region. Do not convert each child into a card merely because it is inside official document.

---

## 18. Signature Grid

Use when either:

1. two or more distinct signatory/approval/confirmation regions form meaningful relationship; **or**
2. one signatory region has clear source-backed positional meaning, especially a formal-document layout where an empty/unused companion region and a populated opposite region show that the signer is intentionally anchored to one side.

Multi-party canonical:

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">
    <p><strong>...</strong></p>
    <p>...</p>
  </div>
  <div class="ct-signature-party">
    <p><strong>...</strong></p>
    <p>...</p>
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

For a one-party grid, the single child is semantic evidence of a source-backed right-side signature anchor. CSS centers text inside the signature region while anchoring that region to the right on larger screens; mobile may expand it to full width. Do not create an empty fake `ct-signature-party` merely to occupy the left side.

Rules:

1. preserve meaningful party count;
2. preserve source order;
3. keep each party label/title/name/note together;
4. do not invent visible underscore placeholders, names, stamps or dates;
5. source table primarily used for party placement or clear single-signer side placement may map to signature grid;
6. a blank companion cell may be removed as content/markup only after its positional evidence has been preserved by the one-party grid;
7. CSS may stack/expand parties on mobile; transform must not merge them;
8. one-party block with **no** meaningful side anchoring normally remains ordinary grouped prose / safest grouping;
9. a single signer originally anchored right must not become centered across the entire document after transform;
10. **“signature layout” is not a blanket layout-only case.**
11. when the signature grid belongs to a coherent formal `ct-official-document`, keep it inside that scope; do not create a separate semantic/card wrapper merely to add another border;
12. contextual CSS may add only subtle separator/rhythm for a direct official-document signature zone; HTML semantics do not change.

---

## 19. Top-level table gate

Before changing any table classify it as:

```text
A. truly layout-only
B. segmented form-slot grid
C. simple data matrix
D. complex data matrix
E. supported positional semantic structure (official/signature)
```

**Scope precedence:** if the table is part of a coherent formal form, preserve/map the outer `ct-official-document` scope first; then classify the table itself using A–E. Formal-form scope and table semantics coexist.

### A. Truly layout-only

Unwrap only when row/cell/group position is presentation-only, e.g. one-cell prose wrapper, spacer/alignment shell, redundant visual container, and positional/scope gate returns NO. A blank companion next to a single signer is not automatically layout-only if it evidences a meaningful side anchor. A legacy wrapper is not “truly layout-only” at scope level until any formal-form boundary it evidences has been preserved.

### B. Form-slot grid

See Section 22.

### C. Simple matrix

```html
<table class="ct-data-table is-simple">...</table>
```

**Default simple candidate:** a genuine **2–4 effective-column** matrix when:

- row/column relationship is straightforward;
- header is absent or one-level/simple;
- no meaningful multi-row header hierarchy;
- no meaningful `rowspan/colspan` creating structural hierarchy;
- no structurally dense nested matrix;
- content may be verbose, but matrix semantics remain simple.

When these conditions hold, **prefer `is-simple`**. Do not promote to complex merely because the table has four columns, many body rows or longer prose cells.

The following facts alone are **not** complex cues:

- exactly 4 effective columns;
- many body rows;
- long text in one or more cells;
- a visually prominent but still one-level header row.

### D. Complex matrix

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">...</table>
</div>
```

Strong complex cues:

- **5+ effective columns**;
- structurally dense matrix/content;
- long multi-row or hierarchical headers;
- meaningful `rowspan/colspan`;
- dense comparison/accounting matrix with structural complexity;
- high-cell-count meaningful form grid.

A 4-column table may still be complex when another strong cue is present. Column count is a cue, not a replacement for structural classification.

Never classify simple↔complex merely to obtain preferred color/width. Conversely, do not over-classify a structurally simple 2–4-column table as complex out of caution alone.

**Official-document context does not alter classification.** The same `is-simple/is-complex` semantics receive a formal-neutral CSS palette under `ct-official-document`; never reclassify to obtain that presentation.

### E. Positional semantic

When cells primarily encode official/signatory role grouping rather than data matrix, map to specific positional component after preserving group boundaries. This includes a source-backed single-signature side anchor when table geometry clearly carries that positional meaning.

---

## 20. Global fit-only table policy

Transformer has **no horizontal-scroll decision**.

```text
simple table  → fit 100%
complex table → fit 100%
nested table  → fit parent cell
```

Never:

- add fixed width/min-width to force canvas;
- invent responsive/scroll classes;
- create nested scroll wrappers;
- flatten a meaningful wide table because it is wide;
- promote/widen parent solely because child is complex;
- alter semantics for responsive appearance.

CSS owns fit density, font size, padding, wrapping, gridlines, header colors and contextual official-document table presentation.

`ct-table-scroll` = compatibility wrapper, not scroll instruction.

---

## 21. Table integrity

For every semantic table preserve:

- meaningful visible text per cell;
- row order;
- cell order;
- header relationships;
- meaningful blank cells;
- exact meaningful `rowspan/colspan`;
- Nợ/Có/account codes/amounts/dates;
- nested parent-child association;
- meaningful left/right relation;
- formal-form ownership when table belongs to a coherent official form.

Strip legacy fixed widths/heights/cellpadding/cellspacing when presentation-only.

Do not repair spans by guess. Ambiguous/malformed spans → safest faithful structure + Needs review.

Do not change semantic classification because official-document contextual table colors/radius/zebra/hover differ from ordinary article tables.

---

## 22. Segmented form-slot grid

Typical source:

```text
[03] Mã số thuế: | □ | □ | □ | □ | ...
```

Detection requires **actual blank-slot evidence**, not cell count alone:

- one body row;
- no genuine heading row;
- first cell field label/code;
- many following blank character/digit slots;
- slot position/count meaningful.

Rules:

1. preserve every meaningful slot;
2. normally high-cell-count form grid = `is-complex`;
3. label + slots same `tbody` row;
4. do not invent `thead`;
5. do not convert label to `th` merely because first/bold;
6. do not collapse blank slots;
7. strip legacy width/height/style;
8. no scroll/width logic;
9. populated one-row 10+ peer values = ordinary matrix, not form-slot.

A form-slot grid can be a child of `ct-official-document`; that outer scope does not change slot/table rules. CSS may render its label/slots with a more neutral paper-like style in official-document context without semantic change.

---

## 23. Header / span fidelity

For genuine headers:

- use `thead` for real heading rows/groups;
- use `th` for true header cells;
- preserve meaningful multi-row hierarchy;
- preserve exact `rowspan/colspan`.

Complex header hierarchy:

```text
major group row
→ intermediate group row(s)
→ terminal leaf row
```

Never:

- flatten meaningful header rows;
- invent extra header rows;
- infer terminal row = code/index merely because last;
- mutate cell order/spans to repair visual borders.

Presentation:

```text
ordinary top-level simple header → dark
ordinary nested simple header    → quiet light
ordinary complex header          → light hierarchy
inside ct-official-document      → formal-neutral contextual hierarchy, semantic class unchanged
```

AI does not encode those colors.

---

## 24. Nested table classification gate

Before flattening nested table ask:

> Would removing row/cell boundaries destroy meaningful left/right, row/column, label/explanation, accounting/basis, condition/treatment, value/note or another meaningful positional association?

YES → preserve table or map specific positional component.

Each table independent semantic scope; child columns/spans do not reclassify parent. If the nested structure belongs to a coherent formal form, its outer official-form ownership is preserved independently of its table type.

### Type A — truly layout-only

Unwrap only when boundaries carry no meaning. Signature/official relation cannot enter Type A without positional gate returning NO. A blank left cell + single formal signer in the right cell must be checked for source-backed side anchoring before Type A cleanup. A wrapper that contributes evidence to a coherent formal-form boundary cannot be discarded at scope level before that boundary is mapped.

### Type B — one-row support relation

Shape:

- one meaningful body row;
- 2–3 cells;
- no meaningful thead/tfoot;
- no span;
- local support relation such as accounting lines ↔ explanation/basis.

Canonical nested `is-simple`, directly inside parent cell, no child `ct-table-scroll`. Preserve cell order/association. CSS may stack on mobile.

If the apparent Type B row is actually signatory placement, Signature Grid precedence applies, including the source-backed one-party side-anchor case.

### Type C — embedded small matrix

**2–4 effective columns**, multiple meaningful rows and/or simple one-level `thead`, no meaningful complex spans/header hierarchy → nested `is-simple`; remain tabular; no child wrapper.

A nested 4-column table remains Type C when its structure is simple. Do not promote solely because of column count.

### Type D — nested complex matrix

**5+ effective columns** OR meaningful spans OR complex/multi-row headers OR dense numeric/accounting matrix with structural complexity → nested `is-complex`; preserve structure; no child wrapper; do not widen/promote parent.

---

## 25. Nesting depth + locality

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
parent semantics   ← parent direct rows/cells
child semantics    ← child direct rows/cells
form-slot evidence ← current table direct cells
span model         ← current table direct cells
formal-form scope  ← broader source continuity/boundary evidence, not child column count
formal alignment   ← source-backed document/edge/role evidence, not table density
```

Never let child density/spans mutate parent classification.

---

## 26. Links

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

Legacy relative links:

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

## 27. Media

Preserve image/media only when source URL/path can satisfy sanitizer/media contract.

Do not guess CDN/R2/root-relative destination.

If unsafe legacy relative image cannot survive:

- remove image element if required;
- preserve meaningful caption text where appropriate;
- report media migration required.

---

## 28. Canonical whitespace

- no empty presentation paragraphs;
- no repeated blank blocks for spacing;
- CSS owns rhythm;
- preserve meaningful `pre/code` whitespace;
- remove Office/list-marker noise without merging items;
- do not create visible spacer text to force official/signature alignment.

---

## 29. Ambiguity policy

```text
preserve content
→ preserve relationship/group membership
→ preserve coherent formal scope when source-backed
→ distinguish ABOUT-form material from OF-form content
→ preserve source-backed formal alignment when meaning-bearing
→ choose less destructive supported structure
→ do not guess
→ Needs review
```

Defaults:

- peer-list vs definition-list → normal list/prose;
- possible nested relation → preserve table rather than flatten;
- possible positional relation → preserve groups rather than serialize;
- coherent formal-form cues with uncertain exact boundary → preserve safest contiguous formal fragment + Needs review;
- article H2/warning adjacent to form but ownership unclear → do not guess; preserve safest boundary + review;
- source-backed centered/right formal alignment with unclear semantic importance → preserve safest supported alignment + review rather than stripping destructively;
- single signer with clear source-backed right-side anchor → one-party signature grid;
- single signer without clear side evidence → ordinary grouped prose / safest structure, not invented alignment;
- possible form-slot → require real slot evidence, otherwise matrix;
- possible multi-row header → preserve row/span boundaries;
- malformed span → no invented repair;
- unclear Nợ/Có → neutral + review;
- ambiguous issuer/authority role naming → preserve relation + review, no guessed role text.

---

## 30. Step-4 Inventory Reconciliation

Return to **every `Sxx`**.

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
S01 → ... → Converted → PASS
S02 → ... → Preserved/Normalized → PASS
S03 → ... → Needs review → REVIEW
S04 → single signer anchored right → one-party ct-signature-grid → Converted → PASS
S05 → coherent tax form scope → section.ct-official-document containing form-owned child structures → Converted → PASS
S06 → article warning ABOUT form → remains outside ct-official-document → Preserved → PASS
S07 → source-centered printed form title → p.ct-align-center inside official scope → Converted → PASS
S08 → right-aligned unit line → p.ct-align-right inside official scope → Converted → PASS
```

No item may disappear without explanation.

Calculate:

```text
SOURCE COVERAGE = reconciled items / total inventory items
```

Completion requires `100%`. Needs-review item counts as reconciled when explicitly accounted for.

---

## 31. Independent fidelity audit

Inventory coverage does not prove fidelity. Run checks independently.

### Visible text

Compare normalized source visible text vs canonical visible text after allowing only legitimate presentation-only removals such as manual markers, decorative separators, empty layout paragraphs, truly layout-only shells and unsafe href attributes while preserving visible text.

Do not over-normalize away real differences.

Report when practical:

```text
Normalized source visible text:    N characters
Normalized canonical visible text: N characters
Result: PASS / REVIEW / FAIL
```

### Heading

- body H1 = 0;
- major sections H2;
- valid H2/H3/H4 hierarchy;
- opening meaningful text not silently lost;
- article heading ABOUT a form is not automatically absorbed into printed formal scope.

### Lists

- peer item count preserved;
- no double marker `• -`;
- no peer family wrongly converted to definition list.

### Callouts / sanitizer

For every `ct-content-box`:

- root canonical `div`;
- exactly one semantic variant;
- optional title = `p.ct-content-box__title`;
- body = `div.ct-content-box__body`;
- no invented source title;
- no new legacy `aside/blockquote` root;
- no `div.ct-content-box__title`.

For editorial callouts adjacent to formal forms:

- source ownership decides inside/outside scope;
- a warning ABOUT the form remains outside when source proves it is editorial, even if semantically valid as `is-warning`.

### Accounting

- every explicit Nợ/Có preserved;
- side correct;
- codes/amounts unchanged;
- no invented title.

### Tables — every table

Verify:

- semantic classification justified;
- **structurally simple 2–4-column matrices are not over-promoted to `is-complex` solely because they have four columns, many rows or longer prose cells**;
- 5+ columns are a strong complex cue; a 4-column table still becomes complex when another genuine structural cue exists;
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
- no nested `ct-table-scroll`;
- no invented width/min-width/scroll markup;
- form-owned tables remain inside the coherent official-form scope when source supports that scope;
- official-document contextual table presentation did **not** cause semantic reclassification or new presentation class.

Meaningful depth >1 or malformed spans cannot receive automatic full PASS.

### Links/media

- no invented URL/media destination;
- unsafe relative URL not silently rewritten;
- visible link text preserved;
- removed media/link migration reported.

### Positional fidelity — mandatory

For each positional `Sxx` verify:

```text
all visible text preserved
same semantic groups/parties preserved
source order preserved
issuer ↔ authority relation preserved when present
signatory/approval parties remain distinct
single-signature side anchoring preserved when source clearly encodes it
party text remains in correct party
no meaningful pair serialized into unrelated prose
canonical positional classes survive sanitizer/editor
```

For a source-backed single signer anchored right, verify:

```text
one signer remains one signer
blank companion is not invented as a fake party
signer region is not flattened into full-width centered prose
one-party ct-signature-grid is used only when right-side anchoring is source-backed
```

### Formal Form Scope Fidelity — mandatory when cues exist

For every source-backed coherent form verify:

```text
printed/form-owned title/code and first form-owned field define a justified start
article heading/lead-in ABOUT the form remains outside when not printed/form-owned
editorial warning/note ABOUT the form remains outside when not printed/form-owned
form-owned coded fields remain in scope
segmented form slots remain in scope and structurally intact
simple/complex matrices remain in scope and keep own table semantics
form-owned unit/legend/declaration remains in scope
signature/approval region remains in scope
form-owned pieces are not emitted as unrelated article-root siblings
ct-official-header is not invented when source lacks issuer↔authority pair
related-content/editorial commentary after form is not swallowed into scope
```

**All child content correct individually + coherent formal-form boundary lost = FAIL — FIX BEFORE PUBLISH.**

**Editorial ABOUT-form material swallowed into official scope despite clear source boundary = FAIL — FIX BEFORE PUBLISH.**

### Formal Alignment Fidelity — mandatory when source evidence exists

For each source-backed meaningful alignment verify:

```text
printed formal title centered in source → canonical alignment remains centered when identity/role depends on it
unit/currency line right-aligned to the following matrix → edge association preserved when source-backed
official date/place/role alignment → preserved when position carries meaning
signature/approval positioning → preserved through positional component/alignment contract
alignment is expressed only through existing canonical ct-align-* classes / positional wrappers
no arbitrary inline style or invented visual class
no meaningless decorative alignment preserved mechanically
```

**All words remain + meaningful formal alignment/edge association is lost = FAIL or REVIEW according to source certainty; when source evidence is clear and loss changes document identity/association, FAIL — FIX BEFORE PUBLISH.**

**All words remain + meaningful positional relationship/group membership or source-backed side anchoring lost = FAIL — FIX BEFORE PUBLISH.**

### Sanitizer-oriented QA

```text
No inline style
No body H1
No arbitrary classes/data-*
No scripts/iframes/forms/event handlers
Canonical classes only
Canonical content-box tags
Supported table tags/attributes
No guessed unsafe URL
Positional classes only on allowed tags
Formal form scope uses existing section.ct-official-document; no invented wrapper class
Formal alignment uses supported ct-align-left/center/right only
```

---

## 32. Runtime output contract

### Staged mode — production 5-prompt workflow

```text
STEP 1
→ Source Semantic Inventory only

STEP 2
→ Transform Plan / readiness only

STEP 3
→ EXACTLY ONE fenced code block labelled html
→ INSIDE the fence: Canonical HTML ONLY
→ OUTSIDE the fence: NO text
→ NO notes/explanation/QA/PASS/FAIL
→ NO explanatory HTML comments
→ fence is transport wrapper only, not part of Canonical HTML artifact

STEP 4
→ Inventory Reconciliation + Fidelity/Structural/Positional/Form-Scope/Formal-Alignment QA + Final Result

STEP 5 conditional
→ Repair Summary + full Revised Canonical HTML + Remaining Needs Review
→ NO final PASS
→ return to STEP 4
```

Do not emit future-step artifacts early.

### Single-run mode

Only when explicitly asked, may produce:

```text
A. Canonical HTML
B. Inventory Reconciliation
C. Conversion / QA Report
```

---

## 33. Conversion report

Report material:

- title/rebase changes;
- list/emphasis/callout normalization;
- accounting normalization;
- table structural classification;
- preserved spans/empty form slots;
- complex header hierarchy preservation;
- nested Type B/C/D preservation;
- official header/signature mapping, including source-backed one-party side anchoring when present;
- coherent formal-form scope preservation when present;
- ABOUT-vs-OF boundary exclusions when material;
- source-backed formal alignment preservation when material;
- legacy content-box tag normalization;
- links/media removed for sanitizer/migration;
- Needs review.

Inventory-controlled mode reports:

```text
Inventory items: N
Reconciled: N
Source Coverage: 100%
S01 → ...
S02 → ...
```

Do not report CSS colors/scroll/contextual formal-table appearance as transform decisions.

---

## 34. Definition of done

Transformation complete only when:

- canonical vocabulary used;
- visible meaning/item/table/positional/scope/alignment relationships intact;
- title-root rules respected;
- peer-member families not over-classified;
- every new content box uses canonical `div` root + optional `p` title + `div` body;
- exactly one semantic content-box variant;
- no new legacy content-box roots/title shapes;
- every table and nested table classified before flattening;
- **structurally simple 2–4-column matrices are not over-promoted to complex solely because of column count, row count or long prose**;
- meaningful empty form slots preserved;
- segmented form label/slots remain body cells; no fake header;
- populated one-row 10+ matrices not form-slot without evidence;
- genuine complex multi-row header hierarchy preserved;
- terminal header semantics not invented;
- no simple/complex reclassification for visual preference or official-document palette;
- nested child density/spans do not mutate parent;
- Type B preserves association;
- Type C preserves rows/headers;
- Type D preserves full complex structure/spans;
- no transformer decision depends on horizontal scroll;
- meaningful depth >1 cannot silently PASS;
- official-document semantics used only when source supports formal document/form structure;
- coherent formal forms preserve one justified `ct-official-document` boundary across their printed/form-owned title/fields/tables/declaration/signature;
- article H2/lead-in/editorial warning ABOUT the form remains outside when source does not make it printed/form-owned;
- unrelated article prose/related-content is not absorbed into formal-form scope;
- `ct-official-header` is not invented for headerless forms;
- source-backed formal title/unit/date alignment is preserved with existing `ct-align-*` when meaning-bearing;
- official header issuer/authority groups preserved;
- signature party count/order/membership preserved;
- source-backed single-signature side anchoring preserved when present;
- no fake blank signature party invented;
- no signature/official/form-scope relation flattened as generic layout-only;
- H1/inline style/arbitrary classes absent;
- links/media not guessed;
- sanitizer/editor compatibility expected;
- in inventory-controlled mode every `Sxx` reconciled and Source Coverage = 100%;
- independent visible-text, structural, table, positional/form-scope/formal-alignment and sanitizer QA passes or remaining source ambiguity explicitly Needs review.

---

## 35. Version delta

### v1.3.5

- targets EDS v2.3.7;
- formalizes segmented form-slot detection before generic header normalization;
- forbids inventing `<thead>/<th>` for label + blank slots;
- preserves meaningful character slots;
- clarifies span border repair is CSS-owned.

### v1.3.6

- targets EDS v2.3.8;
- preserves genuine multi-row `thead` hierarchy;
- forbids flattening/inventing header rows for presentation;
- forbids reclassifying simple/complex for preferred header color;
- CSS owns simple-dark vs complex-light presentation.

### v1.3.7

- targets EDS v2.3.9;
- requires real blank-slot evidence;
- negative rule for populated one-row 10+ matrices;
- parent/child independent scope for density/span semantics;
- no terminal-row code/index assumption;
- documents nested simple quiet header.

### v1.3.8

- targets EDS v2.3.10;
- fixed sanitizer-safe content-box tag contract;
- forbids new legacy content-box tag shapes;
- requires content-box sanitizer compatibility;
- staged Inventory → Transform → QA → conditional Repair workflow aligned.

### v1.4.0

- introduced Official Document / Official Header / Signature Grid semantics;
- established positional precedence before layout cleanup;
- made relation loss blocking even when text remained.

### v1.4.1

- restores the complete v1.3.8 runtime/governance contract instead of replacing it with a shortened rewrite;
- retains all v1.4.0 positional capability;
- restores explicit fit-only, complex cues, form-slot, header/span, nested Type A/B/C/D, locality, links/media, whitespace, staged/single-run, conversion-report and Definition-of-Done rules;
- clarifies simple-table classification so structurally simple 2–4-column matrices remain `is-simple`, while 5+ columns become the strong column-count cue for `is-complex`;
- clarifies source-backed one-party side anchoring: when a formal single signer is clearly placed in the right source region, preserve that relation with a one-party Signature Grid rather than page-centering it; no fake blank party;
- synchronizes the canonical Step-3 output contract with the production fenced-`html` copy workflow;
- synchronizes with EDS v2.4.1 and Compact v1.1.1.

### v1.4.2

- targets EDS v2.4.2 / Compact v1.1.2;
- adds Formal Form Scope Detection before child-table normalization;
- preserves coherent administrative/tax forms as one `section.ct-official-document` across form title/code, coded fields, form-slot grids, simple/complex matrices, form-owned legends/declarations and signature regions;
- keeps child table/signature semantics independent inside the scope;
- makes `ct-official-header` optional and forbids inventing issuer/authority header for headerless forms;
- excludes article lead-in, commentary and related-content that are not form-owned;
- makes fragmented-form scope loss a blocking QA failure even when all child text/tables/signatures survive;
- introduces no new class or sanitizer permission.

### v1.4.3

- targets EDS v2.4.3 / Compact v1.1.3;
- adds explicit **ABOUT-form vs OF-form boundary gate** so article H2/lead-in/editorial warning/commentary are not swallowed into `ct-official-document` unless source proves printed/form ownership;
- makes clear over-wrap and under-wrap blocking failures when source boundary is clear;
- adds **Source-backed Formal Alignment Fidelity** using existing `ct-align-left/center/right`, including centered printed form title and right-aligned unit/date edge associations when meaningful;
- forbids mechanical preservation of all legacy alignment and forbids invented alignment classes;
- records that official-document contextual table/form-slot presentation is CSS-owned and must not change `is-simple/is-complex` semantics;
- retains all mature v1.4.2/v1.4.1/v1.3.8 guards additively.

---

## 36. Final rule

> **New semantic capability must be additive. Do not delete mature transformation guards merely because they are unchanged. Preserve source content, preserve source relationships, preserve exact source-backed formal scope, distinguish editorial material ABOUT a form from printed content OF it, preserve meaningful formal alignment only when evidence supports it, map only evidence-backed semantics, and let CSS own visual presentation.**