# KTD Editorial Transform — Full Reference Preservation Index

**Current canonical runtime:** EDS v2.3.10  
**Current canonical transform skill:** `ktd-editorial-html-transform` v1.3.8  
**Current compact runtime skill:** `ktd-editorial-html-transform-compact` v1.0.2

This index preserves the complete pre-hardening v2.3.4 / v1.3.2 documentation while the current files carry newer nested-table, fit-only, segmented-form, span-grid, complex-header, selector-locality and sanitizer-safe content-box rules.

## Precedence

Use references in this order:

1. Current `SKILL.md`, `transformation-spec.md`, `canonical-examples.md`, `qa-checklist.md`, `nested-table-fixtures.md`, `content-box-sanitizer-fixtures.md`, compact runtime `../ktd-editorial-html-transform-compact/SKILL.md`, and `docs/21-content-editorial-design-system.md` for rules changed by v2.3.5–v2.3.10 / v1.3.3–v1.3.8.
2. The frozen full-reference files below remain normative for unchanged details documented more extensively in v2.3.4 / v1.3.2.
3. On any conflict, the current EDS v2.3.10 / canonical skill v1.3.8 rule wins. Compact v1.0.2 must stay synchronized to that canonical contract.

## Frozen full references

- `references/SKILL.v1.3.2-full-reference.md`
- `references/transformation-spec.v1.3.2-full-reference.md`
- `references/canonical-examples.v1.3.2-full-reference.md`
- `references/qa-checklist.v1.3.2-full-reference.md`
- `../../docs/references/editorial/content-editorial-design-system-v2.3.4-full-reference.md`

These files are immutable snapshots of the last complete detailed reference before nested-table hardening. They prevent loss of canonical knowledge while allowing current files to define later deltas.

## v2.3.5 / v1.3.3 hardening delta

Added:

- nested-table classification before flattening;
- Type A layout-only unwrap;
- Type B one-row 2–3-cell support relation;
- Type C small multi-row 2–3-column matrix;
- Type D complex nested matrix including headers/spans/wide/dense structures;
- `rowspan` / `colspan` preservation;
- meaningful nesting depth > 1 => `Needs review`, no automatic PASS;
- regression fixtures at desktop/tablet/mobile widths.

The original v2.3.5/v1.3.3 presentation strategy also introduced parent promotion and single-scroll ownership for wide nested matrices.

## v2.3.6 / v1.3.4 simplification delta

Superseded prior scroll-width complexity with:

- every editorial table fits 100% of its container at every viewport;
- no horizontal table scrollbar;
- no sticky first column;
- no `max-content` / forced wide working canvas;
- no parent promotion merely to gain width;
- progressive shared font-size/padding compression for 5+, 8+, and 11+ columns;
- cell text wraps instead of expanding table width;
- one-row segmented form grids preserve all meaningful blank slots;
- Type B may still stack on mobile;
- Type C/D remain tabular and fit their parent.

## v2.3.7 / v1.3.5 form/span hardening delta

Added two structural guarantees without expanding sanitizer vocabulary.

### Segmented form-slot grids

- detect one-row field-label + meaningful blank-slot structures before generic header normalization;
- preserve label + slots as body cells;
- **do not invent `<thead>/<th>`** merely because the label is first/bold;
- dedicated readable form density/height;
- fixed-layout residual width shared by slot cells.

### Span-safe gridlines

- span tables use collapsed grid-border model;
- browser resolves effective boundaries rather than DOM-last-child guesses;
- transformer preserves spans/cell order and never mutates HTML to compensate for CSS borders.

## v2.3.8 / v1.3.6 complex-header hierarchy delta

Changed presentation of genuine complex headers without adding sanitizer vocabulary or a new HTML class:

```text
top-level is-simple
→ deep-teal header + white text

is-complex
→ light hierarchical header + dark text
```

Added:

- major/intermediate light tonal groups;
- complex header vertical middle alignment;
- light total/footer header treatment;
- transformer preservation of genuine multi-row `thead` row order and exact spans;
- prohibition on semantic reclassification merely for header color.

## v2.3.9 / v1.3.7 audit-hardening delta

A full cross-check of EDS/runtime/skill found and corrected selector-scope and over-generalization bugs.

### 1. Per-table selector locality

Older CSS used descendant-wide tests such as:

```text
:has(tr > :nth-child(11))
:has([rowspan])
```

A nested 12-column/span child could therefore influence parent density or border-collapse.

Current rule:

```text
column-density detection
→ direct rows/cells of current table only

span detection
→ direct th/td of current table only

child complexity
→ never changes parent presentation
```

Example:

```text
Parent 2-col/no-span → base density + separate border model
Child 12-col/span    → own dense typography + collapsed span grid
```

### 2. Form-slot false-positive prevention

High cell count alone is no longer sufficient.

Current semantic/presentation evidence:

```text
one row
+ no genuine thead
+ first field-label cell
+ many following blank character/digit slots
```

A populated one-row 10+ cell matrix stays an ordinary matrix and must not receive a 32–36% first-label width.

### 3. Generalized complex terminal leaf

The terminal row of every complex `thead` is no longer automatically treated as a semantic code/index band.

Current presentation:

```text
first row               → #EAF2EE / #244D45 / 700
intermediate rows       → #F5F8F6 / #30463F / 600
normal terminal leaf    → #FFFFFF / #33433D / 700
very deep 4+ terminal   → optional #EEF4F1 / #315A50 / 700 accent
```

The accent is presentation only; transformer never infers code/index meaning from row position.

### 4. Nested simple-header clarification

Top-level simple tables retain deep-teal/white headers. Nested simple tables with a support `thead` intentionally use a quiet light header. This presentation difference does not change `is-simple` semantics.

This v2.3.9/v1.3.7 rule supersedes older references that:

- allowed descendant child structure to affect parent CSS heuristics;
- described `one-row + no thead + 10+ cells` alone as sufficient form-slot evidence;
- implied every terminal complex-header row was a code/index band;
- implied every `is-simple` header, including nested support tables, must be deep teal.

## v2.3.10 / v1.3.8 / compact v1.0.2 sanitizer-safe callout delta

A runtime audit found that class vocabulary alone was insufficient: the sanitizer class contract is **tag-sensitive**.

A model could emit a content-box root/title using tags that the old sanitizer did not preserve, causing semantic classes to disappear before CSS rendering. The fix has two parts: sanitizer compatibility for legacy content and a **single canonical generation shape** for future transforms.

### Canonical generation contract

All new transformed content boxes use:

```html
<div class="ct-content-box is-example">
  <p class="ct-content-box__title">Ví dụ</p>
  <div class="ct-content-box__body">...</div>
</div>
```

Rules:

```text
root           → div.ct-content-box + exactly one semantic variant
optional title → p.ct-content-box__title
body           → div.ct-content-box__body
```

New canonical output must not use:

```text
aside.ct-content-box
blockquote.ct-content-box
div.ct-content-box__title
```

Why `div`: it is the neutral, predictable root for a reusable presentation component. `blockquote` falsely asserts quotation semantics for many legal/example/warning blocks, while `aside` can imply complementary/side content even when a legal rule or worked example is central to the article. Fixing the root to `div` also removes an unnecessary choice from the AI.

### Sanitizer migration compatibility

`sanitizeEditorialHtml()` preserves semantic classes for previously transformed legacy shapes:

```text
aside.ct-content-box + variant
blockquote.ct-content-box + variant
div.ct-content-box__title
```

It still strips orphan `is-note/is-info/is-warning/is-legal/is-example` variants when the owning `ct-content-box` root is absent.

This compatibility is **migration safety only**. It does not change the canonical transformer output contract.

### Runtime/QA consequence

Before PASS, transformer/QA verifies that every newly generated content box uses the canonical `div` / optional `p` / `div` shape and that root/title/body classes are expected to survive sanitizer unchanged.

Dedicated regression cases live in `content-box-sanitizer-fixtures.md`.

This v2.3.10/v1.3.8 rule supersedes any older reference that treated `.ct-content-box` as tag-agnostic generation or required `aside` as the canonical content-box root.