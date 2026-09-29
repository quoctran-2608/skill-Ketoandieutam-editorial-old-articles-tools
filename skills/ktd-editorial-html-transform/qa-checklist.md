# KTD Editorial Transform — QA Checklist v1.4.3

**Applies to:** EDS v2.4.3 / Skill v1.4.3 / Compact v1.1.3  
**Canonical EDS reference:** `docs/21-content-editorial-design-system.md`  
**Purpose:** full completion gate for direct or staged transformation.

---

## A. Content fidelity

- [ ] No sentence/fact was rewritten, added or silently removed.
- [ ] Opening title-like visible text was audited.
- [ ] Title-like text removed only with metadata-confirmed exact/no-information duplication.
- [ ] Added-scope/missing-metadata title content preserved as `ct-article-intro` where applicable.
- [ ] Peer-item boundaries and label→description pairing are intact.
- [ ] Amounts/percentages/dates/accounts/Nợ/Có/legal refs/formulas match source.
- [ ] Top-level and meaningful nested table values match source.
- [ ] Meaningful empty form cells/character slots are preserved.
- [ ] Meaningful nested row/column/header associations are intact.
- [ ] Meaningful `rowspan/colspan` values match source exactly.
- [ ] Source-backed callout title/label text is preserved; no callout title was invented.
- [ ] Meaningful positional group boundaries are intact.
- [ ] Official-document role groups are preserved when source contains them.
- [ ] Signatory/approval party count/order/text membership matches source.
- [ ] Source-backed single-signature side anchoring is preserved when source clearly encodes it.
- [ ] **Coherent formal-form ownership/boundary is preserved when title/fields/form-slots/tables/declaration/signatures jointly belong to one source-backed official form.**
- [ ] Article/editorial content that is merely **about** a form/document is not swallowed into the official scope unless source proves it is content **of** the printed/formal document.
- [ ] Source-backed formal alignment/position such as centered formal title, official place/date, matrix unit label or signature placement is preserved when it carries formal-document identity/relationship.
- [ ] Text preservation is not used as a substitute for relationship, scope or formal-alignment preservation.

---

## A2. Inventory / staged orchestration gate

When Compact 5-step workflow is used:

- [ ] Source Semantic Inventory was created before EDS mapping/class selection.
- [ ] Inventory IDs remain stable (`S01`, `S02`, ...); repair does not rewrite/delete/relabel them merely to make HTML pass.
- [ ] Inventory is treated as evidence, not an answer key.
- [ ] Inventory includes plain structural regions, not only colorful/decorated ones.
- [ ] Inventory records meaningful `Relations` such as parent/child, left↔right, issuer↔authority, signer↔signer, single signer↔source-backed side anchor, label↔value, header↔data where present.
- [ ] When coherent formal-form cues exist, Inventory records form-scope relation such as `formal form scope ↔ title/fields/form-slots/tables/declaration/signatures`.
- [ ] Inventory distinguishes adjacent article/editorial material **about** the form from source-backed printed/form-owned content where source boundary evidence supports that distinction.
- [ ] Inventory records source-backed formal alignment when loss of that alignment could change document identity/relationship.
- [ ] Step 2 explicitly checks positional risk before generic layout cleanup when relevant.
- [ ] Step 2 explicitly defines source-backed formal-form start/end when coherent form cues exist, or records boundary ambiguity for review.
- [ ] Step 2 explicitly keeps article H2/warning/lead-in outside the form when they describe the form but source shows printed-form start later.
- [ ] Step 3 returns **exactly one fenced `html` code block** in the production 5-prompt workflow.
- [ ] Inside the Step-3 fence is Canonical HTML only; outside the fence is no text.
- [ ] Step 3 does not emit preliminary notes, PASS/FAIL, QA summary or explanatory HTML comments.
- [ ] The Step-3 fence is a transport wrapper for copyability, not part of the Canonical HTML artifact.
- [ ] Step 4 reconciles every `Sxx` item.
- [ ] Source Coverage = 100% before PASS or PASS WITH NEEDS REVIEW.
- [ ] Step 4 independently audits visible text, positional fidelity, formal alignment **and formal-form scope fidelity when applicable**.
- [ ] Step 5 runs only for clearly fixable transform error, not to force away genuine source ambiguity.
- [ ] Step 5 outputs revised HTML but does not declare final PASS.
- [ ] Every repaired revision returns to Step 4 for full QA.
- [ ] If same repair failure repeats roughly 2–3 times, automatic repair stops and human review is required.

---

## B. Heading / intro

- [ ] No H1 in body.
- [ ] Major sections H2, subsections H3, local H4.
- [ ] No H5/H6 in canonical article body.
- [ ] Heading rebase was independent from opening-text preservation.
- [ ] Missing title metadata is reported when title-root fallback is used.
- [ ] Color/size alone was not treated as sufficient heading semantics.
- [ ] Meaningful opening scope/context was not deleted merely to repair hierarchy.
- [ ] A form title inside an official-form scope was not falsely promoted to article H1 merely because it is visually prominent.
- [ ] An article H2 that describes/introduces a form remains an article heading when source shows the actual printed form begins later; it is not absorbed into `ct-official-document` merely by topical similarity.

---

## C. Lists / inline semantics

- [ ] Normal peers use UL/LI before DL consideration.
- [ ] Legacy list markers are not duplicated beside semantic bullets.
- [ ] `ct-key-emphasis` is longer scan-worthy meaning, not just colored text.
- [ ] `ct-key-highlight` is short decisive meaning, not just yellow/cyan paint.
- [ ] Emphasis/highlight are not nested.
- [ ] Genuine italics/quotation semantics are preserved where meaningful.
- [ ] Checklist is used only for genuine completion/verification items.
- [ ] Steps are used only when ordered sequence matters.
- [ ] Definition List is genuine term→definition.
- [ ] Fact List is concise metadata key→value.

---

## D. Callouts / key lines / source notes

- [ ] Note/info/warning/legal/example match actual function.
- [ ] `is-legal` is used for substantive legal rule/requirement quotation, not as a substitute for an entire Official Document/Form.
- [ ] Every **new** content-box root is `div.ct-content-box` with exactly one semantic variant.
- [ ] Optional content-box title is `p.ct-content-box__title`.
- [ ] Content-box body is `div.ct-content-box__body`.
- [ ] No new `aside.ct-content-box` root remains.
- [ ] No new `blockquote.ct-content-box` root remains.
- [ ] No new `div.ct-content-box__title` remains.
- [ ] A new content-box with zero semantic variants fails QA; AI does not invent `is-note`.
- [ ] A new content-box with multiple semantic variants fails QA; AI does not choose arbitrary winner.
- [ ] No visible title such as “Ví dụ”, “Lưu ý”, “Định khoản” was invented when source had no standalone label/title.
- [ ] Formula/process/result are correctly distinguished.
- [ ] Source-note is short/source-backed and not invented.
- [ ] Paragraph lead-in such as `<strong>Lưu ý:</strong>` was not automatically promoted to a content box without source evidence.
- [ ] A genuine editorial warning about a form may remain a warning **outside** the official-form scope when source shows it is explanatory article content rather than printed form content.

---

## E. Accounting

- [ ] Debit/credit only when explicit.
- [ ] Literal Nợ/Có may remain in semantic tables when table structure is primary.
- [ ] Ambiguous accounting uses neutral fallback + review.
- [ ] `ct-accounting-entry__title` exists only when source has real title/label.
- [ ] Visible “Định khoản” is never invented.
- [ ] Account codes, amounts and order match source.
- [ ] Entry↔explanation relationships remain intact.

---

## F. Definition / Fact / FAQ / Related / Media

- [ ] Definition List is genuine term→definition.
- [ ] Peer account/type/category families are not over-classified.
- [ ] Fact List is concise metadata key→value.
- [ ] FAQ is used only for genuine question→answer material.
- [ ] Ordinary heading ending `?` was not automatically converted to FAQ.
- [ ] Related-content block is source-backed and destination URL was not invented.
- [ ] Editorial media uses source-backed sanitizer-compatible image/media only.
- [ ] Image width/alignment is not invented without source/context evidence.
- [ ] Unsafe relative media is reported for migration; caption meaning is preserved when appropriate.
- [ ] `Xem thêm` / related-content after a formal form is not accidentally swallowed into the form scope unless source clearly makes it form-owned.

---

## G. Top-level tables

- [ ] Simple/complex classification reflects semantic/density complexity, not viewport width or preferred header color.
- [ ] A genuine **2–4 effective-column** matrix is a default `is-simple` candidate when relationship is straightforward, header absent/one-level, and no meaningful span/header hierarchy or other dense structural complexity exists.
- [ ] Exactly 4 columns alone does **not** force `is-complex`.
- [ ] Many body rows alone does **not** force `is-complex`.
- [ ] Longer prose cells alone do **not** force `is-complex`.
- [ ] **5+ effective columns** are a strong complex cue, while structural evidence still governs classification.
- [ ] A 4-column table with genuine spans, multi-row header hierarchy or other structural complexity may still be `is-complex`.
- [ ] Top-level complex keeps one `.ct-table-scroll` compatibility wrapper.
- [ ] `.ct-table-scroll` is **not** treated as request for horizontal scrolling.
- [ ] TH/scope are used only where semantically clear.
- [ ] No meaningful cells were merged/split/reordered.
- [ ] Meaningful blank form slots remain separate cells.
- [ ] No fixed legacy layout width/min-width remains.
- [ ] No transform decision was made because table “would be too wide”.
- [ ] No table was reclassified simple↔complex merely for preferred header appearance.
- [ ] Any source table converted into Official Header or Signature Grid was classified as positional semantic structure first.
- [ ] A table was not flattened solely because it was a “signature layout”.
- [ ] A blank companion cell beside a formal single signer was evaluated for source-backed side-anchor meaning before cleanup.
- [ ] A table belonging to a coherent formal form remains inside that form's `ct-official-document` scope even though its own simple/complex/form-slot semantics are independently classified.
- [ ] A table remains the same semantic class whether its CSS presentation is ordinary editorial or contextual official-document presentation.
- [ ] No `ct-official-table`, `is-government`, `is-formal-table` or equivalent presentation class was invented.

---

## H. Global fit-only invariant

At desktop, tablet and mobile:

- [ ] Every editorial table resolves to `width:100%` / `max-width:100%` of container.
- [ ] No table uses `max-content` or forced wide working canvas.
- [ ] No table/wrapper renders horizontal scrollbar.
- [ ] No sticky first-column behavior exists.
- [ ] Cell text wraps rather than forcing table expansion.
- [ ] Wide matrices use progressively smaller shared typography/padding instead of overflow.
- [ ] Page-level horizontal overflow is not caused by editorial tables.
- [ ] Transformer did not encode width/min-width/sticky/scroll decisions in HTML.

---

## I. Segmented form-slot grids

For patterns such as `[03] Mã số thuế:` + many blank character cells:

- [ ] Pattern is detected **before** generic header normalization.
- [ ] Source has one field-label/body row rather than genuine matrix header.
- [ ] Blank cells are recognized as meaningful form slots, not presentation junk.
- [ ] Actual blank-slot evidence exists after first field-label cell; high cell count alone is insufficient.
- [ ] All source slots remain separate cells.
- [ ] High cell count may be classified `is-complex` without inventing new class.
- [ ] Field label remains body `<td>` unless source genuinely supplied header semantics.
- [ ] No fake `<thead>` or `<th>` was invented for form label.
- [ ] Transformer does not collapse slots or add width/scroll instructions.
- [ ] Legacy slot widths/heights are removed so EDS can distribute evenly.
- [ ] Desktop form row uses readable form-specific density/height instead of generic 11+ ultra-dense styling.
- [ ] Mobile form row uses dedicated compact-but-readable density/height.
- [ ] Slot cells after label are visually distributed evenly under fixed layout.
- [ ] Populated one-row 10+ cell peer matrix **does not** receive form-slot label-width/density treatment.
- [ ] When source form scope is coherent, the form-slot grid remains within the same `ct-official-document` scope as its related coded fields, matrix, declaration and signatures.
- [ ] When inside `ct-official-document`, form-slot presentation is formal-neutral/contextual without changing its semantic table class or slot count.

---

## J. Nested Type A/B/C/D

Every nested table:

- [ ] was classified before flattening;
- [ ] preserves meaningful left/right, row/column, label/explanation, accounting/basis, condition/treatment, value/note and positional-party relationships.
- [ ] broader formal-form ownership is preserved independently of nested table type when applicable.

### Type A

- [ ] Unwrapped only if boundary/grouping was presentation-only.
- [ ] Visible block order remained intact.
- [ ] Positional-semantic gate returned NO before unwrap.
- [ ] Official-header/signature/party relation was not incorrectly treated as Type A.
- [ ] Blank-left + signer-right source geometry was checked for source-backed side anchoring before Type-A cleanup.
- [ ] A legacy wrapper carrying still-unmapped coherent formal-form boundary evidence was not discarded as Type A.

### Type B — support relation

- [ ] One meaningful body row, 2–3 cells, no meaningful header/footer/span.
- [ ] Nested `is-simple` directly in parent cell.
- [ ] No child `.ct-table-scroll`.
- [ ] Cell order/association preserved.
- [ ] Mobile stacking is CSS-owned.
- [ ] A true signatory-party relation uses Signature Grid instead when evidence supports it.
- [ ] A source-backed single signer anchored to one side uses the one-party Signature Grid rule instead of generic Type B when evidence supports it.

### Type C — small matrix

- [ ] **2–4 effective columns**, multi-row and/or simple one-level `thead`, no meaningful complex spans/header hierarchy.
- [ ] Child remains nested `is-simple` and tabular on mobile.
- [ ] A nested 4-column simple matrix is not promoted to Type D solely because it has four columns.
- [ ] Rows/headers/scope/cell order preserved.
- [ ] No child wrapper.
- [ ] Parent is **not** promoted/widened merely to gain viewport width.
- [ ] Child fits parent through CSS density/wrapping.
- [ ] Nested simple `thead` may use quiet light support styling without semantic change.

### Type D — complex nested matrix

- [ ] **5+ effective columns OR meaningful spans OR complex/multi-row headers OR dense structural matrix** justify nested `is-complex`.
- [ ] Meaningful rowspan/colspan preserved exactly.
- [ ] Genuine multi-row `thead` hierarchy remains separate rows.
- [ ] No child wrapper.
- [ ] Parent is not widened/promoted for scrolling.
- [ ] Child remains tabular and fits parent width.
- [ ] Child column count/spans do not alter parent semantic classification.

---

## K. Header/span/depth

- [ ] Meaningful `thead` excludes Type-B stacking and segmented form-slot rows.
- [ ] rowspan/colspan excludes Type-B stacking.
- [ ] Headers were not removed to simplify mobile.
- [ ] Malformed spans are not guessed; they trigger review.
- [ ] Meaningful nested depth >1 triggers Needs review and cannot automatically PASS.
- [ ] Transformer did not alter span values or cell order to repair visual borders.
- [ ] Transformer did not flatten or invent header rows for visual presentation.
- [ ] Transformer did not infer “code/index” semantics from terminal-row position alone.

### Span-safe visual gridline gate

For any table containing direct `rowspan` or `colspan`:

- [ ] EDS uses collapsed grid-border model for **that table only**.
- [ ] Every effective internal column boundary remains visible.
- [ ] Every effective internal row boundary remains visible where grid defines one.
- [ ] A later-row DOM `:last-child` that is **not** effective final column does not lose right separator.
- [ ] Mixed rowspan + colspan multi-level headers do not show missing internal vertical lines.
- [ ] Same rule works for nested span matrices.
- [ ] Span attributes inside nested child do **not** switch parent to collapsed model.

### Complex light-header visual gate — ordinary editorial context

For genuine `is-complex` tables **outside `ct-official-document`**:

- [ ] Top-level simple headers remain deep teal with white text.
- [ ] Nested simple headers remain quiet/light when support `thead` exists.
- [ ] Complex header text is dark on light backgrounds.
- [ ] First complex `thead` row uses major-group tint `#EAF2EE`, text `#244D45`, weight 700.
- [ ] Intermediate rows use `#F5F8F6`, text `#30463F`, weight 600.
- [ ] Terminal leaf row in normal 2–3 row `thead` defaults `#FFFFFF`, text `#33433D`, weight 700.
- [ ] Very deep 4+ row `thead` may use `#EEF4F1`, text `#315A50`, weight 700.
- [ ] Single-row complex headers use major-group light tint rather than deep teal.
- [ ] Complex header cells use `vertical-align: middle`.
- [ ] Complex `tfoot > th` uses light major-group treatment.
- [ ] Grid border `#C8D6CF` remains visible with span-safe collapsed borders.
- [ ] No inline background/color styles emitted by transformer.
- [ ] No fake class such as `is-light-header` invented.

### Official-document contextual table visual gate

For any `ct-data-table` inside `ct-official-document`:

- [ ] Semantic `is-simple` / `is-complex` classification is unchanged by presentation context.
- [ ] Simple headers no longer require global deep-teal/white treatment inside official scope; CSS may use formal-neutral light header tones with dark text.
- [ ] Complex hierarchy remains legible but uses restrained formal-neutral/paper tones rather than brand-heavy presentation.
- [ ] Form-slot tables use near-white/form-like cells and visible gridlines without inventing a new class.
- [ ] Border radius is restrained/squarer than ordinary editorial cards/tables.
- [ ] Zebra treatment is absent or materially subdued within official scope.
- [ ] Row-hover emphasis is disabled within official scope.
- [ ] Grid/border contrast remains sufficient to preserve administrative form structure.
- [ ] Ordinary editorial tables outside `ct-official-document` retain their established presentation.
- [ ] No transform-side inline style/class is used to activate the contextual mode; ancestor context alone owns it.

---

## L. Per-table selector locality + responsive ownership

```text
all top-level tables        → fit 100%
all nested matrices         → fit parent
column density              → own direct rows/cells only
span-border model           → own direct cells only
form-slot mode              → own direct blank-slot row only
nested child complexity     → never changes parent presentation
formal-form scope           → broader semantic boundary, independent from child table type
segmented form slots        → readable dedicated density/height
Type B                      → may stack on mobile
Type C                      → remain tabular
Type D                      → remain tabular
rowspan/colspan             → preserve / span-safe collapsed grid
official header             → may stack groups while wrappers remain
formal official form        → outer ct-official-document scope remains
multi-party signature       → may stack parties while wrappers remain
one-party anchored signer   → may expand full width on mobile while canonical grouping remains
top-level simple header outside official scope → deep teal / white
nested simple header outside official scope    → quiet light
complex header outside official scope          → light hierarchy / dark text
official-document tables    → contextual formal-neutral presentation; semantic classes unchanged
horizontal scroll           → forbidden
sticky column               → forbidden
```

- [ ] No nested scrollbar exists inside parent cell.
- [ ] No outer table scrollbar exists either.
- [ ] No page-level horizontal overflow comes from editorial tables.
- [ ] Parent 2-column table remains base density when child is 12+ columns.
- [ ] Parent no-span table remains separate-border model when only child contains spans.
- [ ] Child independently receives own density/span model.
- [ ] Official-document contextual selectors do not leak to ordinary editorial tables outside the official scope.

---

## M. Links / media

- [ ] No URL was invented.
- [ ] Safe absolute/root-relative/anchor/mailto/tel URLs remain when sanitizer-compatible.
- [ ] Legacy relative `filename.html`, `assets/...`, `../page.html` was not guessed or prepended with `/`.
- [ ] Visible link text is preserved when unsafe destination is removed.
- [ ] Unsafe link migration appears in Needs review.
- [ ] Relative image path is not invented into CDN/R2 URL.
- [ ] Media removal/migration is reported.
- [ ] Meaningful caption text is preserved when appropriate.

---

## N. HTML / sanitizer

- [ ] No inline style/font/event/data-* or arbitrary class remains.
- [ ] Existing EDS tags/classes only.
- [ ] No scripts/iframes/forms/input controls.
- [ ] No unsafe guessed URL.
- [ ] New canonical content boxes use only `div.ct-content-box` + one variant, optional `p.ct-content-box__title`, `div.ct-content-box__body`.
- [ ] Canonical `div` content-box survives `sanitizeEditorialHtml()` with classes intact.
- [ ] Legacy `aside.ct-content-box` survives sanitizer with variant for migration compatibility.
- [ ] Legacy `blockquote.ct-content-box` survives sanitizer with variant for migration compatibility.
- [ ] Legacy `div.ct-content-box__title` survives sanitizer for migration compatibility.
- [ ] Orphan semantic variant without `ct-content-box` root is stripped.
- [ ] Generic `ct-content-box` root with no variant stays generic; sanitizer does not invent `is-note`.
- [ ] Conflicting content-box variants are removed rather than selecting arbitrary winner.
- [ ] Backward compatibility is not treated as permission to generate legacy content-box markup.
- [ ] Nested tables use supported table tags, `is-simple/is-complex`, scope, rowspan, colspan.
- [ ] No new table class invented for fit-only/form-slot/span-grid/light-header/locality/contextual official-document presentation.

### Positional / formal-scope sanitizer contract

- [ ] `section.ct-official-document` survives sanitizer.
- [ ] Formal Form Scope Detection reuses `section.ct-official-document`; no new `ct-form-card`/wrapper class was invented.
- [ ] `div.ct-official-header` survives sanitizer.
- [ ] `div.ct-official-header__issuer` survives sanitizer.
- [ ] `div.ct-official-header__authority` survives sanitizer.
- [ ] `div.ct-signature-grid` survives sanitizer.
- [ ] `div.ct-signature-party` survives sanitizer.
- [ ] A one-party `ct-signature-grid` is used only when source-backed single-signature side anchoring is established.
- [ ] No fake/empty `ct-signature-party` is invented to reproduce a blank source cell.
- [ ] `ct-official-header` is not invented merely because `ct-official-document` is used for a headerless formal form.
- [ ] Existing canonical alignment classes may preserve source-backed formal positioning; no new official-alignment class is invented.
- [ ] Arbitrary companion classes are stripped.
- [ ] `ct-official-document` and `ct-accounting-group` are not combined on same section root.
- [ ] No generic `ct-two-col`, `ct-left`, `ct-right`, `ct-document-card`, `ct-form-card`, `ct-signature-box`, `ct-official-table`, `is-government` exists.

---

## O. Positional fidelity — blocking gate

For **every** `Sxx` with positional/group relation complete:

```text
Sxx:
Source groups/parties:
Source order:
Source relation:
Canonical groups/parties:
Canonical order:
Canonical relation:
Result: PASS | REVIEW | FAIL
```

Questions:

- [ ] Are all visible source words present?
- [ ] Are same semantic groups/parties still distinguishable?
- [ ] Is source order preserved?
- [ ] Was source table/div removed only **after** relationship classification?
- [ ] Did a source two-column/parallel relation become unrelated sequential prose?
- [ ] If official-document header: issuer and authority groups intact?
- [ ] If signatures/approval: all meaningful parties intact with correct membership?
- [ ] If a single signer is source-backed to one side: is that side-anchor relation preserved rather than becoming page-centered?
- [ ] Was a blank companion region removed without inventing a fake party only after its positional evidence was mapped?
- [ ] If formal title/unit/place-date alignment carries source-backed official meaning: is that alignment preserved through supported canonical alignment rather than normalized away?
- [ ] If label/explanation: association intact?
- [ ] Do canonical positional classes survive sanitizer?

### Blocking failure examples

```text
Source:
issuing agency + document number on left
national heading/motto/date on right

Output:
all lines preserved but serialized as ordinary paragraphs

→ FAIL
```

```text
Source:
taxpayer/signatory party A ↔ authority/confirming party B

Output:
both labels preserved but merged into one undifferentiated prose sequence

→ FAIL
```

```text
Source:
blank left companion | centered signer in right region

Output:
same signer words preserved but centered across the whole official document

→ FAIL
```

```text
Source:
centered official form title + right-aligned unit line tied to matrix

Output:
all words survive but both become ordinary left-aligned prose

→ FAIL when source evidence shows the alignment carries formal-document identity/relationship
```

### Responsive non-failure

```text
Canonical HTML retains two semantic party wrappers.
CSS stacks them on mobile in source order.
→ PASS
```

```text
Canonical HTML retains one source-backed signature party.
CSS expands that one-party region to full width on narrow mobile.
→ PASS
```

**All source text preserved + meaningful positional relationship, source-backed formal alignment or source-backed single-signer side anchoring lost = FAIL — FIX BEFORE PUBLISH.**

---

## P. Official Document QA

Use `section.ct-official-document` only when formal/official document or formal-form semantics are real.

General:

- [ ] root scope justified;
- [ ] ordinary legal article not falsely wrapped as official document;
- [ ] content ABOUT the form/document is not automatically treated as content OF the printed/formal document;
- [ ] article H2/lead-in/editorial warning remains outside when source proves the formal printed scope starts later;
- [ ] a restrained neutral outer frame/padding, when present, is CSS-owned presentation of the genuine official-document/form root rather than inline styling or a new semantic wrapper;
- [ ] source-backed formal alignment is preserved only when it carries document identity/relationship; arbitrary legacy alignment is still normalized away;
- [ ] table presentation inside official scope is contextual/CSS-owned and does not change semantic table classification.

If official header exists:

- [ ] `ct-official-header` exists;
- [ ] issuer group source-backed;
- [ ] authority group source-backed;
- [ ] exact text/internal order preserved;
- [ ] no missing information invented;
- [ ] source table mechanics removed only after relationship mapping;
- [ ] not replaced by `ct-content-box.is-legal`;
- [ ] ambiguous role naming is preserved/reviewed rather than guessed.

If source is a headerless formal form:

- [ ] `section.ct-official-document` may still be justified by formal-form scope;
- [ ] `ct-official-header`, issuer or authority wrappers were **not invented** merely to make the form look official.

---

## Q. Signature Grid QA

When signatory/approval/confirmation semantics exist:

- [ ] `ct-signature-grid` is used when mapping is justified.
- [ ] For multiple meaningful source parties, number of `ct-signature-party` groups equals meaningful source parties.
- [ ] Source order preserved.
- [ ] Each label/title/name/note belongs to correct party.
- [ ] No invented signature line/name/stamp/date.
- [ ] No blanket `signature layout → unwrap` logic.
- [ ] A one-party block with **no** meaningful side evidence is not unnecessarily promoted to grid.
- [ ] A source-backed single signer anchored to the right may use exactly one `ct-signature-party` inside `ct-signature-grid`.
- [ ] No fake/empty party is invented for a blank source companion cell.
- [ ] Signer text may remain centered inside its own party region, but the source-backed right-side region does not become centered across the whole document on larger screens.
- [ ] Mobile stacking/expansion keeps party wrappers and source order.
- [ ] When signature grid belongs to a coherent official form, it remains inside that `ct-official-document` and does not gain a separate semantic/card wrapper solely for another frame.
- [ ] Within an official document, any visual separator before the signature zone is CSS-owned and does not introduce another semantic box/card.

---

## Q2. Formal Form Scope Fidelity — blocking gate

Run this gate whenever source contains coherent administrative/tax-form cues such as `Mẫu`/`Phụ lục`, form code/reference, systematic `[01]...[NN]` fields, segmented form slots, an administrative matrix, form-owned unit/legend, declaration/certification or signature parties.

No cue quota is mechanical. First determine whether source evidence establishes one bounded/coherent form.

### Scope-start audit

- [ ] Source-backed form title/appendix title or first clearly form-specific field defines a justified start.
- [ ] Article lead-in/explanation before that start remains outside unless source clearly makes it part of the form.
- [ ] Article heading that names/describes the form remains outside when source shows the printed form begins later.
- [ ] Editorial warning/notice about replacement/effect of the form remains outside when it is article commentary rather than printed form content.
- [ ] Form title/code/reference wording is preserved.
- [ ] The distinction **ABOUT the form ≠ OF the form** was explicitly checked.

### Scope-body audit

- [ ] Systematic coded fields remain within the form scope.
- [ ] Segmented form-slot grids remain within scope and preserve exact meaningful slots.
- [ ] Form-owned simple/complex matrices remain within scope while keeping their own table semantic classification.
- [ ] Form-owned unit-of-measure lines, legends or abbreviation notes remain within scope when source makes them part of the form.
- [ ] Declaration/certification/`cam đoan` remains within scope when source-backed.
- [ ] A legacy outer wrapper was not discarded before its scope evidence was mapped.

### Source-backed formal alignment audit

- [ ] Formal title/appendix block centered in source remains centered through a supported canonical alignment class when that positioning carries formal-document identity.
- [ ] Unit/currency label aligned to the matrix edge remains source-backed aligned when that position conveys its relationship to the matrix.
- [ ] Official place/date or approval positioning is preserved when source evidence makes it meaningful.
- [ ] No new alignment is invented merely to make the document look more official.
- [ ] Arbitrary legacy center/right alignment that carries no semantic/formal relationship may still be normalized.

### Scope-end audit

- [ ] Signature/approval region remains inside the same form scope when it is the form's concluding certification/signature area.
- [ ] Party count/order/membership remains independently correct inside `ct-signature-grid`.
- [ ] The scope ends at the last clearly form-owned content.
- [ ] `Xem thêm`, editorial commentary or ordinary post-form prose stays outside unless source clearly makes it form-owned.

### Header / presentation audit

- [ ] Headerless formal form does not invent `ct-official-header`.
- [ ] No national heading/agency/date is invented.
- [ ] Outer `ct-official-document` frame is the main visual boundary; no nested signature/form card is invented just to add another border.
- [ ] Child tables keep their own semantic classes/borders; contextual official-document presentation is CSS-owned.
- [ ] Ordinary editorial table styling outside official scope remains unaffected.

### Blocking failure

```text
Source:
form title/code → coded fields → form-slot → matrix → declaration → signatures

Output:
every field/table/signature is individually correct
BUT they are emitted as unrelated article-root siblings with no justified form scope

→ FORMAL FORM SCOPE FIDELITY: FAIL
→ FAIL — FIX BEFORE PUBLISH
```

```text
Source:
article H2 + editorial warning ABOUT a form
then printed form starts at Phụ lục

Output:
H2 + warning + printed form all wrapped inside ct-official-document

→ OVER-WRAPPED FORM SCOPE: FAIL
→ FAIL — FIX BEFORE PUBLISH
```

Over-wrapping is also a fixable failure when unrelated article lead-in, `Xem thêm` or editorial commentary is swallowed into the form despite clear source boundaries.

---

## Q3. Official Document Contextual Presentation — CSS-owned regression gate

This gate validates presentation ownership; it must **not** cause transform-side semantic changes.

- [ ] `.ct-official-document` remains the single outer formal-document surface/boundary.
- [ ] Tables inside that ancestor use restrained formal-neutral presentation rather than ordinary brand-heavy editorial table styling.
- [ ] An `is-simple` table inside official scope remains `is-simple`.
- [ ] An `is-complex` table inside official scope remains `is-complex`.
- [ ] Form-slot grids remain structurally identical and preserve exact blank slots.
- [ ] Official contextual CSS may use quieter header fills, dark text, squarer radius, subdued/no zebra and disabled row hover.
- [ ] Ordinary editorial simple tables outside official scope retain deep-teal/white presentation.
- [ ] No new HTML class/variant is required to activate official-table presentation.
- [ ] Signature zone may receive a subtle CSS-owned separator/rhythm inside official scope but no nested semantic card/frame.
- [ ] Contextual selectors do not mutate nested parent/child semantic classification or span fidelity.

Failure examples:

```text
Same 3-column source matrix
outside form → is-simple
inside form  → changed to is-complex just to get a lighter header

→ FAIL
```

```text
Official table styling leaks globally and ordinary editorial simple tables lose their established teal header treatment

→ PRESENTATION REGRESSION
```

---

## R. Conversion report

- [ ] Material Type B/C/D preservation is reported.
- [ ] Meaningful blank form-slot preservation reported when material.
- [ ] Fake-header avoidance reported when relevant.
- [ ] Populated wide one-row matrices are not described as form slots without evidence.
- [ ] Genuine complex multi-row header hierarchy preservation reported when material.
- [ ] Legacy content-box tag normalization reported when material.
- [ ] Official-header/signature mapping reported when material.
- [ ] Source-backed one-party signature side-anchor mapping reported when material.
- [ ] **Coherent formal-form scope mapping is reported when material.**
- [ ] ABOUT-vs-OF boundary decision is reported when adjacent article material could be confused with printed form content.
- [ ] Source-backed formal alignment preservation is reported when material.
- [ ] Depth >1 / malformed spans / low-confidence association appears under Needs review.
- [ ] Link/media migration issues reported.
- [ ] Report does not present header colors/tints/responsive stacking/contextual official-table styling as transform-side decisions.
- [ ] In inventory-controlled mode, every `Sxx` is accounted for and Source Coverage stated.

---

## Mandatory table regression suite

Use `nested-table-fixtures.md` and cover:

```text
A  1×2 support
B  1×3 support
C  multi-row 2-col matrix
D  3-col matrix + thead
D2 4-col structurally simple matrix + one-level header → is-simple
D3 4-col many-row/long-prose matrix without structural complexity → is-simple
D4 4-col matrix + meaningful spans/multi-row hierarchy → is-complex
D5 5-col matrix → strong complex cue
E  rowspan
F  colspan
G  nested 5-col complex
H  parent 5-col + child support
I  meaningful depth >1
J  malformed spans
K  one-row segmented form grid with 10+ cells + blank slots
L  12+ column multi-row header/span matrix
M  rowspan where later-row DOM last child is not effective last column
N  mixed rowspan + colspan multi-level header gridline case
O  complex multi-row light-header hierarchy
P  populated one-row 10+ cell non-form matrix
Q  parent 2-col/no-span + nested 12-col/span child locality
```

## Mandatory content-box sanitizer suite

Use `content-box-sanitizer-fixtures.md` and cover:

```text
R  canonical div.ct-content-box + variant + p title + div body survives unchanged
S  legacy aside.ct-content-box + variant survives for migration compatibility
T  legacy blockquote.ct-content-box + variant survives for migration compatibility
U  legacy div.ct-content-box__title survives for migration compatibility
V  orphan semantic variant without ct-content-box root is stripped
W  generic ct-content-box with no variant remains generic; no is-note invention
X  conflicting semantic variants are removed; no arbitrary winner
Y  consecutive-example regression retains rhythm and canonicalizes title tag on re-transform
```

## Mandatory positional / formal-scope suite

Use `positional-semantic-fixtures.md` and cover:

```text
P01 official issuer/number ↔ authority/national/date header
P02 official header from legacy 1×2 table
P03 two-party signature/confirmation
P04 three-party signature
P05 truly decorative 1×2 layout still unwraps
P06 text coverage 100% but grouping lost → FAIL
P07 canonical positional classes survive sanitizer
P08 conflicting section roots are not guessed
P09 mobile stack preserves wrappers/source order
P10 ordinary legal prose is not Official Document
P11 ambiguous official role naming → preserve + review
P12 signature relation nested inside larger form preserves parent locality
P13 one signer in right source region + blank left companion → one-party Signature Grid; no fake party; side anchor preserved
P14 coherent official tax form → one ct-official-document scope across form-owned title/codes/slots/matrix/declaration/two-party signature; unrelated article content stays outside
P15 children correct but form scope lost → FAIL
P16 article heading/warning ABOUT form stays outside when printed form begins later → over-wrap otherwise FAIL
P17 centered formal title + right-aligned unit/matrix relation preserve source-backed alignment
P18 identical semantic table class receives contextual official presentation only through ancestor; ordinary editorial styling does not regress
```

Representative viewports:

```text
1280 1024 900 768 430 390 360 320
```

---

## Final PASS criteria

PASS requires all of the following:

1. source meaning/visible text/items/table relationships intact;
2. Source Coverage = 100% in staged mode;
3. no body H1 / title-root loss;
4. no peer-list overclassification;
5. every new content box uses canonical sanitizer-safe `div / optional p / div` structure;
6. every new content box has exactly one semantic variant;
7. no new legacy content-box root/title shape;
8. canonical content-box classes survive sanitizer;
9. sanitizer never invents missing content-box variant or chooses conflicting winner;
10. every nested table classified before flattening;
11. structurally simple 2–4-column matrices are not over-promoted to complex solely because of four columns, many rows or long prose;
12. meaningful empty form slots preserved;
13. no fake form-grid header;
14. populated wide matrix not misclassified form-slot;
15. genuine header hierarchy/spans preserved;
16. child does not mutate parent semantics/presentation scope;
17. no transform-side scroll/width/sticky logic;
18. links/media are not guessed;
19. official-document/form semantics used only when source supports them;
20. coherent formal forms preserve one justified `ct-official-document` boundary across form-owned title/fields/tables/declaration/signature;
21. article/editorial content ABOUT a form is not swallowed into content OF the form when source boundary proves otherwise;
22. unrelated article lead-in/commentary/related-content is not swallowed into formal-form scope;
23. headerless form does not invent `ct-official-header`;
24. source-backed formal title/unit/place-date/signature alignment is preserved when it carries formal-document identity/relationship;
25. official issuer↔authority grouping preserved when present;
26. signature/approval party count/order/membership preserved;
27. source-backed single-signature side anchoring preserved when present;
28. no fake blank signature party invented;
29. **no meaningful positional relationship, source-backed formal alignment or formal-form scope lost even when visible text remains complete;**
30. official-document table presentation is CSS/context-owned and does not alter semantic table classes or leak into ordinary editorial tables;
31. no arbitrary style/class/data/event-handler/unsafe URL;
32. sanitizer compatibility expected;
33. remaining source ambiguity explicitly Needs review.

### Final statuses

```text
PASS
→ all fidelity gates pass; no unresolved source ambiguity.

PASS WITH NEEDS REVIEW
→ fidelity passes; genuine source/external ambiguity remains.

FAIL — FIX BEFORE PUBLISH
→ fixable transform/fidelity error exists.
```

Do not run Step 5 merely to turn PASS WITH NEEDS REVIEW into PASS.

After Step 5, always rerun Step 4 on full revised HTML.
