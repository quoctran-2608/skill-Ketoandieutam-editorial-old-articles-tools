# Kế Toán Diệu Tâm — Editorial HTML Transformation Specification v1.4.3

**Status:** Canonical  
**Applies to:** Legacy HTML → EDS v2.4.3 canonical HTML  
**Transformation mode:** FORMAT-ONLY SEMANTIC TRANSFORMATION  
**Canonical EDS reference:** `docs/21-content-editorial-design-system.md`

## 1. Objective

Convert heterogeneous legacy accounting/tax/legal HTML into a stable semantic vocabulary. The transformer must preserve wording, factual content, item boundaries, meaningful table relationships, semantic grouping, meaningful positional relationships, coherent formal-document/form scope, exact source-backed document/form boundary and meaningful formal alignment; it is not a writing, legal-update or presentation layer.

EDS v2.4.3 preserves all v2.4.2/v2.4.1/v2.3.10 invariants and adds Official Document Fidelity & Presentation Hardening on top of Formal Form Scope Detection:

> **Every editorial table fits 100% of its available width. Horizontal table scrolling is not part of the transform decision.**

> **Meaningful positional relationship > generic layout-only cleanup.**

> **Coherent formal-form scope > fragment-by-fragment normalization when source proves title/fields/tables/declaration/signatures belong to one bounded official unit.**

> **Editorial material ABOUT a document/form ≠ printed/official content OF that document/form.**

> **Source-backed formal alignment is preserved only when it carries identity, edge, role or positional meaning.**

It retains segmented form-slot readability, rowspan/colspan gridline fidelity, complex light headers, per-table selector locality, sanitizer-safe content-box markup, Official Document / Official Header / Signature Grid semantics and all prior fidelity guards. Contextual formal-neutral table presentation inside `ct-official-document` is CSS-owned and never changes semantic table classification.

---

## 2. Architectural boundary

```text
Legacy HTML + optional metadata
→ semantic transformation v1.4.3
→ canonical HTML
→ sanitizeEditorialHtml()
→ EDS v2.4.3 CSS
→ preview / human review / publish
```

AI owns semantic classification and source-backed scope/boundary/alignment decisions.

Sanitizer owns safety/compatibility.

CSS owns:

- fit/wrap/density;
- table gridlines;
- ordinary header color hierarchy;
- selector locality;
- responsive stacking;
- official-document/form neutral outer frame;
- official-header two-column vs mobile stacking;
- signature-grid layout, including source-backed one-party right-side anchoring;
- subtle direct signature-zone separator/rhythm;
- contextual formal-neutral table/form-slot presentation inside `ct-official-document`;
- all other visual presentation.

Transformer does **not** encode presentation behavior into article HTML.

---

## 3. Core invariants

Preserve unless source itself prevents recovery:

- visible wording/facts;
- opening content;
- peer-item boundaries and label→description pairing;
- dates, amounts, percentages, accounts and Nợ/Có;
- legal references/formulas;
- safe URLs/images;
- table values/cell order;
- meaningful empty form cells/slots;
- meaningful nested rows/columns/headers;
- meaningful multi-row header hierarchy;
- meaningful `rowspan/colspan`;
- semantic callout type and source-backed callout title text;
- official-document role groups;
- signatory/approval party count, order and membership;
- source-backed single-signature side anchoring;
- meaningful left↔right / parallel / opposed grouping;
- coherent formal-form boundary and ownership of printed/form-owned title/codes, fields, slots, matrices, form-owned notes/legends, declaration and signature regions;
- exclusion of editorial/article material that merely talks **about** the form/document when source shows it is not printed/form-owned content;
- source-backed formal alignment when it preserves printed form title identity, unit/date edge association, official role placement or signature relationship.

Title-like text may be removed only when masthead metadata confirms exact/no-information duplication.

Nested/layout boundaries may be removed only when position/grouping/scope carries no meaning.

Text preservation alone is not sufficient evidence of structural, scope, boundary or alignment fidelity.

---

## 4. Canonical semantic vocabulary

Use existing EDS semantics only:

```text
prose/headings/strong/em/blockquote
ct-align-left / ct-align-center / ct-align-right
ct-article-intro
ct-key-emphasis
ct-key-highlight
ct-source-note
lists / ct-checklist / ct-steps
ct-content-box + semantic variant
ct-key-line
accounting family
ct-definition-list
ct-fact-list
ct-data-table.is-simple/is-complex
ct-table-scroll
ct-editorial-media
ct-faq
ct-related-content
ct-official-document
ct-official-header
ct-official-header__issuer
ct-official-header__authority
ct-signature-grid
ct-signature-party
```

Formal Form Scope Detection and Official Document Table Presentation **reuse existing semantics and add no new class**.

Formal Alignment Fidelity reuses existing `ct-align-left/center/right` on supported elements. Do not invent `ct-form-title`, `ct-unit-right`, `ct-official-center` or inline alignment style.

Canonical content-box structure is fixed:

```html
<div class="ct-content-box is-example">
  <p class="ct-content-box__title">Ví dụ</p>
  <div class="ct-content-box__body">
    <p>...</p>
  </div>
</div>
```

Rules:

- root = `div.ct-content-box` + exactly one semantic variant;
- title optional and, when present, must be `p.ct-content-box__title`;
- body wrapper = `div.ct-content-box__body`;
- do not invent title text if source has none;
- new canonical output must not use `aside.ct-content-box`, `blockquote.ct-content-box`, or `div.ct-content-box__title`.

Root tag is intentionally fixed to `div`; model chooses only whether block is content box and which semantic variant applies.

No new table class is required for fit-only rendering, form slots, span-grid hardening, selector locality, complex light-header presentation or formal-neutral official-document table presentation.

No generic positional/presentation classes such as `ct-two-col`, `ct-left`, `ct-right`, `ct-document-card`, `ct-form-card`, `ct-signature-box`, `ct-official-table`, `is-government` are allowed.

---

## 5. Decision precedence

1. classify title/root and repair body heading tree;
2. preserve title text independently of rebase;
3. respect meaningful source structures;
4. **detect meaningful positional/group relationships before generic layout cleanup;**
5. **detect coherent formal-document/form scope before child-table normalization;**
6. **run ABOUT-vs-OF exact boundary gate before choosing official/form start and end;**
7. **run Formal Alignment Fidelity before stripping source center/right alignment inside official/form regions;**
8. identify official-document/header and signature/approval structures, including source-backed single-signature side anchoring, when source supports them;
9. classify peer lists before DL;
10. classify callout meaning, then normalize callout tag structure to canonical `div/p/div`;
11. classify every table as top-level/nested before flattening;
12. detect segmented form-slot grids before generic matrix/header normalization, requiring actual blank-slot evidence;
13. preserve genuine multi-row header hierarchy and spans;
14. apply table integrity and nested Type A/B/C/D rules;
15. treat each table as independent semantic scope; nested child density/spans do not alter parent classification;
16. map supported official/signature layout shells to their canonical semantic components **inside the preserved formal scope when applicable**;
17. preserve source-backed meaningful formal alignment using only existing `ct-align-*` classes;
18. **never make semantic decision based on whether table would scroll, which header color is preferred or whether it is inside official-document context;**
19. preserve more structure/scope/alignment when ambiguity exists;
20. report Needs review rather than guess.

---

## 6. Positional + scope precedence gate

Before unwrapping a table/div/grid or stripping a broader legacy wrapper ask:

> Would serializing/removing these regions destroy who belongs to which side/party, issuer↔authority distinction, signer/approver distinction, source-backed single-signer side anchoring, label↔explanation association, **the fact that multiple fields/tables/declarations/signatures belong to one coherent formal form, the boundary between editorial ABOUT-form material and printed OF-form content, or a source-backed formal alignment/edge association**?

```text
YES       → preserve/map relationship, scope, boundary or alignment
UNCERTAIN → preserve safest grouping/scope/alignment + Needs review
NO        → layout cleanup may proceed
```

The following are **not sufficient** evidence for layout-only semantics:

- legacy table markup;
- fixed widths;
- centered/right-aligned text;
- empty companion/spacer cells;
- Microsoft Office markup;
- signature text placed inside table cells;
- a formal form implemented as several sibling tables/divs.

A blank companion cell may contain no visible text while still evidencing that the neighboring signer region is intentionally anchored to one side.

A legacy outer wrapper may be presentational implementation while still evidencing a meaningful form boundary.

Adjacency inside one wrapper does **not** prove an article heading/warning belongs to printed form content.

Implementation can be presentational while resulting relative position/scope/alignment is semantic.

---

## 7. Title / heading rules

Body H1 forbidden.

- metadata-confirmed exact duplicate → remove + report;
- title-like block with additional meaning → `ct-article-intro`;
- no title metadata but high-confidence root → intro + review;
- major body sections begin at H2;
- true child sections use H3/H4;
- no H5/H6 in canonical body;
- do not infer heading from color alone;
- hierarchy repair must not delete meaningful opening text.

A form title inside a source-backed official-form scope is not automatically an article heading; preserve its form function and wording without inventing H1.

An article H2/H3 that names or introduces a form is not automatically printed form content. Formal-form ownership requires independent source boundary evidence.

---

## 8. Lists / definition / fact

Declared peer families such as child accounts/types/groups/cases use normal UL/LI by default.

Definition List = genuine concept→definition.

Fact List = concise metadata key→value.

Checklist = genuine completion/verification items only.

Steps = ordered procedure where sequence matters.

Manual bullets are removed when semantic list owns marker.

---

## 9. Accounting

Only assign debit/credit when source explicitly says Nợ/Có.

Literal Nợ/Có may remain table text when table structure is primary.

Never infer Nợ/Có from color/account type.

Never invent visible “Định khoản” title when source has none.

Preserve account codes, amounts and source order exactly.

---

## 10. Semantic emphasis / callouts

```text
plain → strong → ct-key-emphasis → ct-key-highlight → key-line → callout
```

Legacy paint is evidence, not meaning.

Callout variants:

```text
is-note    → insight/principle/key takeaway
is-info    → neutral additional information
is-warning → risk/error/penalty/caution
is-legal   → substantive official/legal rule/requirement quotation
is-example → example/case/calculation scenario
```

After choosing variant, always emit canonical content-box tag contract from Section 4.

Short source attribution may use `ct-source-note`.

`is-legal` is **not** a substitute for Official Document/Form structure.

A source-backed editorial warning **about** a form can remain a valid `is-warning` callout **outside** `ct-official-document` when source shows it is not printed/form-owned content.

---

## 11. Official Document + Formal Form Scope semantics

Use `section.ct-official-document` only for genuine formal/official document, administrative/tax form, declaration, notice, decision, dispatch/công văn or meaningful official fragment.

Ordinary legal prose that cites a law is not automatically an Official Document.

### 11.1 Formal Form Scope Detection

Detect whole-form ownership **before** normalizing its child tables independently.

Common cues:

```text
Mẫu / Phụ lục / official form name/code/reference
“kèm theo ...” form reference
systematic coded fields [01], [02], [03]...
segmented character/digit slots
administrative data matrix / bảng kê
unit line / abbreviation legend / form-owned note
declaration / certification / cam đoan
signature / approval / taxpayer / agent regions
legacy wrapper or contiguous sequence tying these pieces together
```

No mechanical cue quota. Decide from **coherence + boundary evidence**.

### 11.1.1 ABOUT vs OF exact boundary gate — v1.4.3

Before choosing FORM START/END, classify adjacent nodes as:

```text
EDITORIAL / ARTICLE MATERIAL ABOUT THE FORM/DOCUMENT
or
PRINTED / OFFICIAL CONTENT OF THE FORM/DOCUMENT
```

Common ABOUT-form material that remains outside unless source proves printed/form ownership:

- article H2/H3 naming or introducing the form;
- editorial warning/note explaining replacement, effective date or usage;
- article lead-in/caption/intro;
- post-form `Xem thêm` / related-content / commentary.

Common source-backed OF-form start evidence:

- printed `Phụ lục` / formal form title block;
- official form title/code printed inside the form;
- first clearly form-specific coded field when no separate printed title exists.

Reference pattern for Mẫu 05-2/BK-QTT-TNCN:

```text
article H2 “Mẫu 05-2/... Ban hành kèm...”            → OUTSIDE
editorial warning “Chú ý: Mẫu này thay thế...”      → OUTSIDE
printed “Phụ lục / BẢNG KÊ CHI TIẾT CÁ NHÂN...”    → FORM START
[01]...[NN], slots, matrix, declaration              → INSIDE
signature parties                                     → INSIDE / END
Xem thêm                                               → OUTSIDE
```

If source proves the warning itself is printed as part of the form, keep it inside. **Source ownership—not keyword or adjacency—decides.**

When one coherent form is established:

```text
START → source-backed printed form/appendix title or first form-specific field
MIDDLE → coded fields + slots + matrices + form-owned notes/legends + declaration
END → signature/approval region or last clearly form-owned content
```

Keep outside:

- article lead-in/explanation before form;
- article heading that merely describes/introduces form;
- editorial callout/warning that comments on form rather than belongs to it;
- editorial commentary after form;
- `Xem thêm` / related-content after form;
- ordinary prose not owned by form.

Canonical composition:

```html
<section class="ct-official-document">
  <!-- source-backed printed form title/fields -->
  <!-- form-slot/simple/complex tables retain own semantics -->
  <p>...</p><!-- declaration if source-backed -->
  <div class="ct-signature-grid">
    <div class="ct-signature-party">...</div>
    <div class="ct-signature-party">...</div>
  </div>
</section>
```

Requirements:

- `ct-official-document` owns the outer scope, not child presentation;
- child tables remain independently simple/complex/form-slot;
- signature grid independently preserves parties;
- `ct-official-header` is optional and **must not be invented** for a headerless form;
- do not invent national heading/agency/date metadata;
- do not create a separate signature-card/form-card wrapper;
- when signature already belongs to official-form scope, outer official frame is the main visual boundary;
- legacy wrapper may be stripped only after its form-boundary meaning has been mapped;
- if exact boundary is uncertain, preserve safest contiguous formal fragment + Needs review;
- **under-wrap** and **over-wrap** are blocking transform errors when source boundary is clear.

Correct child pieces individually are **not sufficient** if coherent form boundary is lost or editorial ABOUT-form nodes are swallowed into it.

### 11.2 Source-backed Formal Alignment Fidelity

Before stripping `text-align:center/right/left` inside an official document/form ask:

> If this alignment is normalized to ordinary prose, does the reader lose formal title identity, edge association, official role/date/unit placement, signature relation or another positional meaning?

```text
YES       → preserve using existing ct-align-left/center/right on supported element
UNCERTAIN → preserve safest supported alignment + Needs review
NO        → strip legacy alignment; normal CSS flow owns presentation
```

Typical justified examples:

```html
<p class="ct-align-center">
  <strong>Phụ lục</strong><br>
  <strong>BẢNG KÊ CHI TIẾT CÁ NHÂN</strong><br>
  <em>(Kèm theo ...)</em>
</p>

<p class="ct-align-right"><em>Đơn vị tiền: Đồng Việt Nam</em></p>
```

Also inspect source-backed place/date, issuer/authority and signature/certification alignment when position carries meaning.

Do **not** preserve every center/right alignment mechanically. Decorative/spacer alignment still normalizes away. Do not invent `ct-form-title`, `ct-unit-right`, `ct-official-center` or inline style.

### 11.3 Official header

Typical official-header source relation:

```text
issuer / document number
↔
national or authority heading / motto / place-date
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

Requirements:

- preserve exact visible wording;
- preserve internal order of each group;
- preserve group count and source order;
- source 1×2 layout table may be replaced only after relationship classification;
- do not invent authority/document/date text;
- do not serialize groups into unrelated prose;
- do not wrap whole document in `is-legal` instead;
- ambiguous role naming → preserve relation + Needs review, no guess.

Presentation remains CSS-owned. A restrained neutral frame around `ct-official-document` preserves boundedness of embedded formal document/form after legacy wrapper mechanics are removed; it must not become a decorative callout/card treatment.

Official document/form body may contain recipient, prose, citations, coded fields, form slots, tables, units/legends, declaration and signature region. Do not turn every child into a card.

### 11.4 Official Document Table Presentation ownership

Tables inside `ct-official-document` keep the **same semantic classes**:

```text
is-simple remains is-simple
is-complex remains is-complex
form-slot remains same structural table
```

CSS ancestor context alone changes presentation to formal-neutral document mode:

- neutral light headers/dark text;
- clearer neutral grid;
- minimal radius;
- paper-white body;
- no editorial zebra/hover treatment;
- neutral form-slot label/slots;
- nested table inherits same document mode.

Ordinary tables outside `ct-official-document` keep normal EDS presentation, including deep-teal top-level simple headers.

Do not add `ct-official-table`, `is-government`, `is-formal-table` or reclassify simple↔complex for aesthetics.

---

## 12. Signature Grid semantics

Use when either:

1. two or more distinct signatory/approval/confirmation regions form a meaningful relation; **or**
2. one signatory region has clear source-backed positional meaning, especially when an empty/unused companion region and a populated opposite region show that signer is intentionally anchored to one side.

Multi-party canonical:

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">...</div>
  <div class="ct-signature-party">...</div>
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

Requirements:

- preserve meaningful party count;
- preserve source order;
- preserve text membership inside correct party;
- do not invent signature lines, names, stamps or dates;
- source table may be replaced when cells primarily encode signatory parties or source-backed single-signer side anchor;
- blank companion cell may be removed only after positional evidence mapped;
- one-party grid must not invent empty fake party;
- one-party signature with no meaningful side evidence normally remains ordinary grouped prose / safest grouping;
- signer text may remain centered inside own region, while region itself remains right-anchored on larger screens when source encodes relation;
- source-right single signer must not become centered across entire official document;
- mobile stacking/expansion is CSS presentation and does not justify semantic flattening;
- if signature belongs to coherent formal form, keep inside `ct-official-document` and do not invent second frame/card;
- contextual CSS may add subtle top separator/rhythm for direct signature zone, no semantic wrapper/class change;
- “signature layout” is **not** automatic Type A/layout-only.

---

## 13. Top-level tables

### Simple matrix

Default simple candidate: genuine **2–4 effective-column** matrix when:

- row/column relationship is straightforward;
- header is absent or one-level/simple;
- no meaningful multi-row header hierarchy;
- no meaningful `rowspan/colspan` creating structural hierarchy;
- no structurally dense nested matrix;
- content may be long, but matrix relationship remains simple.

When conditions hold, prefer `is-simple`.

These facts alone do **not** force complex:

- exactly 4 effective columns;
- many body rows;
- one/more long-prose cells;
- one visually prominent but one-level header row.

### Complex matrix

Strong complex cues:

- **5+ effective columns**;
- genuinely dense structural matrix/content;
- multi-row/hierarchical headers;
- meaningful spans;
- dense comparison/accounting matrix with structural complexity;
- high-cell-count meaningful form grids.

A 4-column table may still be complex when another strong cue exists.

Top-level complex keeps one `.ct-table-scroll` wrapper for canonical/backward compatibility. Under EDS v2.4.3 it **does not imply horizontal scrolling**.

Do not convert data tables into images.

Do not reclassify simple↔complex to influence width/header color or official-document palette. Conversely, do not over-classify structurally simple 2–4-column matrix as complex out of caution alone.

**Scope precedence:** before generic table classification, determine whether source table belongs to coherent formal-form scope or supported official/signature positional structure. Outer scope and child table semantics coexist.

---

## 14. Global fit-only rendering contract

Transformer does not decide width, minimum width, sticky columns or scrolling.

```text
simple table  → width 100%
complex table → width 100%
nested table  → width 100% of parent cell
```

CSS may reduce font-size/padding and wrap content as column count grows.

Transformer must not:

- add fixed width/min-width;
- add child scroll wrapper;
- promote parent only to gain width;
- flatten meaningful data because source is wide;
- invent responsive variant class.

---

## 15. Table integrity

Never merge/split/reorder meaningful source cells.

Preserve:

- meaningful empty cells;
- headers;
- `scope` where valid;
- exact `rowspan/colspan`;
- source row/cell order;
- Nợ/Có/accounts/amounts/dates;
- nested parent-child association;
- meaningful left/right relationship;
- formal-form ownership when table part of coherent official form.

Remove legacy fixed widths/styles when presentation-only.

### Meaningful empty form cells

Blank cells are not automatically junk.

Example:

```text
[03] Mã số thuế: | blank | blank | blank | ...
```

When blank cells encode character slots/field positions, preserve every slot exactly. CSS handles compact fit.

A blank companion cell in signature-layout table may be removable content-wise while still serving as evidence neighboring signer is anchored to one side. Run positional classification before removing.

---

## 16. Segmented form-slot grids

Detection cues:

- one source row;
- no genuine column-heading row;
- first cell field label/code;
- many following blank character/digit slots;
- slot position/count meaningful.

Rules:

- preserve every slot;
- high cell count may justify `is-complex`;
- keep label + slots same `<tbody>` row;
- do **not** invent `<thead>`;
- do **not** promote label cell to `<th>` merely because first/bold;
- do not collapse cells;
- do not invent new class for width;
- do not add horizontal scroll;
- strip legacy widths/heights so EDS distributes slots;
- CSS structural heuristic owns proportions/row height;
- **cell count alone insufficient**: populated one-row 10+ cell table = normal matrix, not segmented form field.

If source genuinely has header row + later data rows, it is matrix, not segmented form grid.

A segmented form-slot grid can remain child of `ct-official-document`; outer form scope does not change table semantics. CSS context may render it more like a printed form without HTML change.

---

## 17. Nested classification gate

Before flattening ask:

> Would removing boundaries destroy left/right, row/column, label/explanation, accounting/basis, condition/treatment, value/note, issuer/authority, signer/signer, single-signer side anchoring or other meaningful positional association?

Yes → preserve semantic table or map supported positional component.

If nested structure is form-owned, broader `ct-official-document` scope remains independently preserved.

---

## 18. Type A — layout-only

Unwrap only single-cell/spacer/alignment/redundant shells whose boundaries/positions carry no meaning **and which do not contain still-unmapped evidence for coherent formal-form scope**.

Preserve visible order.

Signature/approval and official-header relations are not blanket Type-A cases.

Blank companion beside single formal signer is not automatically Type A when it evidences source-backed side anchoring.

---

## 19. Type B — one-row support relation

Pattern:

- one meaningful body row;
- 2–3 cells;
- no meaningful header/footer;
- no rowspan/colspan;
- local support relation.

Canonical nested `is-simple`; no child wrapper.

Desktop/tablet side-by-side; mobile may stack source order.

If source relation is distinct signatory parties, or blank companion + single source-anchored signer, Signature Grid takes precedence.

---

## 20. Type C — embedded small matrix

Pattern:

- **2–4 effective columns**;
- multiple meaningful rows and/or simple one-level `thead`;
- no meaningful complex spans/header hierarchy;
- real matrix relationship.

Child remains nested `is-simple` and stays tabular on mobile.

A nested 4-column matrix is not Type D merely because four columns. Promote only with genuine complex cue.

No parent promotion/widening required. Child fits parent via CSS density/wrapping.

Nested simple `thead` may use quiet light support-header presentation without semantic change.

---

## 21. Type D — genuine nested complex matrix

Use nested `is-complex` for:

- **5+ effective columns**; or
- meaningful spans; or
- complex/multi-row headers; or
- dense numeric/accounting matrix with structural complexity.

Requirements:

- preserve child structure;
- no child wrapper;
- no parent promotion for width;
- preserve spans/headers/cell order;
- preserve genuine multi-row `thead` levels;
- CSS fits child to parent width;
- child column count/spans do not alter parent classification.

---

## 22. Header/span rules

Meaningful `thead` means genuine matrix semantics and excludes Type-B stacking/segmented form-slot rows.

Meaningful rowspan/colspan normally implies Type D; preserve exact values.

Malformed/ambiguous spans → safest structure + review, never invent repair.

Transformer must **not** change spans/cell order to repair visual borders.

EDS uses per-table collapsed grid-border model only when that table’s own direct cells contain `rowspan` or `colspan`; nested child spans must not switch parent border model.

No sticky-column logic exists, so multi-row headers/spans require no scroll-specific treatment.

### Complex-header hierarchy fidelity

Preserve source hierarchy:

```text
major group row
→ intermediate group row(s)
→ terminal leaf row
```

Do not flatten meaningful header rows.
Do not invent header rows for presentation.
Do not infer semantic “code/index” from terminal-row position.

EDS presentation remains CSS-owned:

```text
ordinary top-level simple header → deep teal / white text
ordinary nested simple header    → quiet light support header
ordinary complex table header    → light tonal hierarchy / dark text
inside ct-official-document      → formal-neutral contextual hierarchy; semantic class unchanged
```

---

## 23. Nesting depth

Automatic support guaranteed for one meaningful nested level only.

If depth >1 remains after safely unwrapping presentation-only levels:

- preserve conservatively;
- Needs review;
- forbid automatic PASS.

Depth gate is structural confidence, not width/scroll.

---

## 24. Per-table locality + responsive ownership

```text
all top-level tables        → fit 100%
all nested matrices         → fit parent cell
column-density detection    → own direct rows/cells only
span-border detection       → own direct cells only
form-slot detection         → own direct blank slots only
nested child complexity     → never changes parent presentation
formal-form scope           → broader source boundary, independent from child table density/type
formal alignment            → source-backed identity/edge/role relation, independent from table density
Type B                      → mobile may stack
Type C                      → remain tabular
Type D                      → remain tabular
rowspan/colspan             → never support-stack
official-header groups      → mobile may stack while wrappers remain
formal official form        → outer ct-official-document remains across responsive layouts
multi-party signatures      → mobile may stack while wrappers remain
one-party anchored signer   → mobile may expand full width while canonical grouping remains
horizontal scrollbar        → forbidden
sticky first column         → not used
```

---

## 25. Links / media

Preserve valid sanitizer-compatible source references.

Safe link categories:

```text
https://...
http://...
/root-relative-path
#valid-anchor
mailto:...
tel:...
```

Legacy relative paths:

```text
filename.html
assets/...
../page.html
```

must not be “fixed” by guessing/prepending `/`.

If unsafe:

- preserve visible link text;
- remove unsafe destination if required;
- report migration/Needs review.

Never invent URL.

For media:

- preserve image/media only when path can satisfy current sanitizer/media contract;
- do not guess CDN/R2/root-relative destination;
- if unsafe legacy image cannot survive, remove image if required, preserve meaningful caption where appropriate and report media migration.

---

## 26. Presentation-only removal / whitespace

After semantic classification, safely remove:

- inline `style`;
- font face/size markup;
- `mso-*` / Office-only classes;
- redundant spans;
- visual-only colors/backgrounds;
- presentation-only fixed table dimensions;
- manual bullets replaced by semantic markers;
- empty spacer paragraphs;
- decorative separators;
- truly layout-only shells.

Do not remove artifact before deciding whether it carries meaning recorded in inventory. Blank signature companion may be removed only after positional evidence mapped.

Legacy outer wrapper/table of coherent formal form may be removed as implementation only **after scope represented by `section.ct-official-document`**.

Source formal alignment may be stripped only after Formal Alignment Fidelity. Meaning-bearing alignment maps to existing `ct-align-*`; decorative alignment normalizes away.

Canonical whitespace:

- no empty presentation paragraphs;
- no repeated blank blocks for spacing;
- CSS owns rhythm;
- preserve meaningful `pre/code` whitespace;
- remove Office/list-marker noise without merging items;
- do not insert visible underscore/spacer text merely to align official/signature groups.

---

## 27. Sanitizer / security contract

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

Use supported semantic tags/classes/attributes only.

Content-box sanitizer gate:

```text
new root       → div.ct-content-box + one semantic variant
optional title → p.ct-content-box__title
body wrapper   → div.ct-content-box__body
```

Reject/normalize new output containing:

```text
aside.ct-content-box
blockquote.ct-content-box
div.ct-content-box__title
```

Also reject root with zero/multiple variants. Sanitizer migration compatibility must not become generation rule.

Positional sanitizer contract:

```text
section → ct-official-document

div → ct-official-header
      ct-official-header__issuer
      ct-official-header__authority
      ct-signature-grid
      ct-signature-party
```

Formal-form scope reuses `section.ct-official-document`; **no new sanitizer permission/class needed**.

Formal alignment reuses supported `ct-align-left/center/right` only; no inline style/new class.

One-party `ct-signature-grid` valid only when source-backed single-signature side anchoring established; no fake blank party.

`ct-official-document` and `ct-accounting-group` cannot coexist on same section root.

---

## 28. Ambiguity

```text
preserve content
→ preserve relationship/group membership
→ preserve exact coherent formal scope when source-backed
→ distinguish ABOUT vs OF
→ preserve source-backed meaningful formal alignment
→ choose less destructive structure
→ do not guess
→ Needs review
```

Nested ambiguity favors preserving table semantics over flattening.

Positional ambiguity favors preserving group boundaries over serializing them.

Formal-form cues with uncertain exact boundary favor safest contiguous formal fragment + Needs review rather than fragmenting clearly related pieces.

Article H2/warning adjacent to form but ownership unclear → safest boundary + review, not adjacency guess.

Meaningful formal alignment uncertain → safest supported alignment + review, not destructive strip.

Single signer with clear source-backed right-side anchor → one-party signature grid.

Single signer without clear side evidence → ordinary grouped prose / safest grouping, not invented alignment.

Possible form-slot requires actual blank-slot evidence; otherwise ordinary matrix.

Possible complex-header ambiguity favors preserving source row/span boundaries.

Ambiguous official role naming must not be invented.

---

## 29. Table fidelity audit

For every table verify:

- exact meaningful text per cell;
- meaningful empty cells/slots;
- row/cell order;
- segmented form-grid label/slots remain one body row;
- actual blank-slot evidence before form-slot classification;
- populated one-row 10+ matrices remain normal matrices;
- no fake form-grid `thead/th`;
- left/right association;
- genuine complex multi-row header levels remain separate;
- terminal row not assigned invented code/index semantics;
- header→data relationship;
- exact spans;
- accounts/Nợ/Có/amounts/dates;
- simple/complex classification;
- structurally simple 2–4-column matrix not over-promoted to complex solely for four columns/many rows/long prose;
- 5+ effective columns treated as strong complex cue while structural evidence still governs;
- nested Type C 2–4-column simple matrix remains simple without another complex cue;
- nested Type D requires 5+ columns or genuine spans/header/density complexity;
- parent independent from child density/spans;
- no semantic reclassification merely for visual header treatment or official-document palette;
- no invented width/min-width/scroll;
- no child wrapper;
- any table converted to official/signature component preserved all semantic group boundaries;
- blank signature companion evidence evaluated before cleanup;
- form-owned tables remain inside same justified official-form scope as source form.

Meaningful depth >1 or malformed spans cannot automatically PASS.

---

## 30. Positional + Formal-Scope + Formal-Alignment fidelity audit

For each positional inventory item verify:

- visible text preserved;
- same semantic groups/parties distinguishable;
- source order preserved;
- issuer↔authority relation preserved when present;
- signatory/approval party count/membership preserved;
- source-backed single-signature side anchoring preserved when present;
- no fake blank signature party;
- signer text centers only inside intended region rather than across full document when source anchors right;
- label↔explanation relation preserved;
- no semantic pair serialized into unrelated prose;
- positional classes survive sanitizer/editor.

For source-backed single right signer:

```text
one signer remains one signer
blank companion may be removed after mapping evidence
one-party ct-signature-grid is used
no empty fake party
signer region is not full-width centered on desktop
```

For each coherent formal form verify:

```text
exact source-backed printed/form-owned start/end preserved
article H2/lead-in ABOUT form stays outside when not printed/form-owned
editorial warning/note ABOUT form stays outside when not printed/form-owned
form title/code remains in scope
coded fields remain in scope
form-slot grids remain in scope/intact
simple/complex matrices remain in scope with own semantics
form-owned unit/legend/declaration remains in scope
signature/approval remains in scope
form pieces not emitted as unrelated siblings
ct-official-header not invented when absent
post-form editorial/related content stays outside
```

For source-backed meaningful formal alignment verify:

```text
printed form title centered when source identity requires it
unit/date line remains right/edge-associated when source supports it
official role/date alignment preserved when position carries meaning
signature position preserved
existing ct-align-* only; no inline style/new class
no decorative alignment preserved mechanically
```

**All visible text present + meaningful positional/source-backed single-signer relation lost = FAIL — FIX BEFORE PUBLISH.**

**All child tables/signatures correct + coherent form boundary lost or editorial ABOUT-form material swallowed despite clear source boundary = FAIL — FIX BEFORE PUBLISH.**

**All visible text present + clear source-backed formal identity/edge alignment lost = FAIL — FIX BEFORE PUBLISH.**

Responsive stacking/expansion with wrappers/source order/scope intact is not semantic failure.

---

## 31. Bulk regression gate

Use:

- `nested-table-fixtures.md`;
- `content-box-sanitizer-fixtures.md`;
- `positional-semantic-fixtures.md`.

Representative widths:

```text
1280 1024 900 768 430 390 360 320
```

Legacy/table cases retained:

- wide segmented form grid;
- populated one-row 10+ non-form matrix;
- structurally simple 4-column matrix with one-level header → simple;
- structurally simple 4-column many-row/long-prose matrix → simple;
- 4-column matrix with spans/multi-row hierarchy → complex;
- 5-column matrix → strong complex cue;
- 12+ column matrix with multi-level headers/spans;
- later-row DOM last child not effective last column;
- complex multi-row light-header hierarchy;
- parent 2-col no-span with nested 12-col/span child;
- canonical/legacy content-box sanitizer compatibility.

Positional/form-scope/alignment cases include:

- official issuer/authority pair;
- legacy 1×2 official-header table;
- two-/three-party signature regions;
- source-backed single signer in right region with blank left companion → one-party grid, no fake party;
- genuinely decorative 1×2 layout that may unwrap;
- text-coverage false positive where grouping lost;
- sanitizer survival/conflicting roots;
- mobile stack preserving wrappers;
- ordinary legal prose not over-classified;
- nested signature relation preserving parent locality;
- coherent official tax form: printed form title/code + coded fields + form slots + complex matrix + declaration + two-party signature inside one `ct-official-document`;
- anti-case: article H2 + editorial warning ABOUT form remain outside; printed `Phụ lục / BẢNG KÊ...` starts form;
- anti-case: children individually correct but form scope lost → FAIL;
- anti-case: article lead-in/post-form Xem thêm incorrectly swallowed → FAIL;
- printed centered form title + right-aligned unit line retain meaningful alignment;
- ordinary simple table outside official doc remains ordinary simple visual; same semantic table inside official doc receives CSS formal-neutral presentation without class change.

---

## 32. Staged workflow / output contract

Current production five-prompt mode:

```text
STEP 1 → Source Semantic Inventory only
STEP 2 → Transform Plan / readiness only
STEP 3 → EXACTLY ONE fenced code block labelled html; inside = Canonical HTML only; outside = no text
STEP 4 → Inventory Reconciliation + Fidelity/Structural/Positional/Form-Scope/Formal-Alignment QA + Final Result
STEP 5 → Repair Summary + full Revised Canonical HTML + Remaining Needs Review; then return to STEP 4
```

Step 3 must not output notes, explanations, QA, PASS/FAIL or explanatory HTML comments. Fenced `html` block is transport wrapper for copyability and is not part of Canonical HTML artifact.

Single-run mode may bundle Canonical HTML + Inventory Reconciliation + QA only when explicitly requested.

---

## 33. Version history

- v1.3.1 peer-list precedence;
- v1.3.2 meaningful nested support preservation;
- v1.3.3 Type A/B/C/D hardening, headers/spans, historical parent-promotion + single-scroll ownership;
- v1.3.4 removes scroll/parent-width decisions from AI and adopts global fit-only rendering;
- v1.3.5 detects segmented form-slot grids before header normalization, forbids fake form-grid `thead/th`, formalizes span-grid fidelity as CSS-owned;
- v1.3.6 preserves complex multi-row header hierarchy and forbids semantic reclassification for header color;
- v1.3.7 requires blank-slot evidence, parent/child locality, removes terminal-row code/index assumption, records nested-simple quiet header behavior;
- v1.3.8 locks content-box generation to `div` root / optional `p` title / `div` body;
- v1.4.0 introduces Official Document / Signature Grid and positional-fidelity blocking;
- v1.4.1 restores every detailed v1.3.8 transformation/table/link/media/sanitizer contract while retaining all v1.4.0 positional semantics; clarifies 2–4 simple / 5+ strong complex, fenced-html Step 3, official frame and source-backed single-signer right anchoring;
- v1.4.2 adds Formal Form Scope Detection: coherent administrative/tax forms preserve one `ct-official-document` boundary across title/code, coded fields, form slots, matrices, form-owned legends/declarations and signature regions; child semantics remain independent; headerless forms do not invent `ct-official-header`; unrelated article content stays outside; scope loss becomes blocking QA failure. No new class/sanitizer permission;
- **v1.4.3 hardens ABOUT-vs-OF form/document boundaries, adds source-backed Formal Alignment Fidelity with existing `ct-align-*`, and formalizes CSS-owned contextual Official Document Table Presentation. Ordinary editorial table semantics/visual mode remain unchanged outside official documents.**
