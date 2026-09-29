# KTD Editorial Transform — Table Hardening Fixtures

**Applies to:** EDS v2.3.9 / `ktd-editorial-html-transform` v1.3.7  
**Mode:** FORMAT-ONLY SEMANTIC TRANSFORMATION

## Global invariants

- no meaningful visible text disappears;
- meaningful row/column associations are never flattened;
- meaningful empty form slots are preserved;
- no amount/account/date/legal text changes;
- no legacy inline width/style/cellpadding/cellspacing survives;
- no nested `.ct-table-scroll` exists inside a parent cell;
- meaningful rowspan/colspan is preserved;
- meaningful nesting depth >1 cannot automatically PASS;
- **no editorial table may render a horizontal scrollbar at any viewport**;
- **no editorial table uses sticky first-column behavior**;
- segmented form grids require actual blank-slot evidence and keep readable row height/density;
- populated wide one-row matrices are not mistaken for form grids;
- rowspan/colspan matrices keep every effective internal gridline;
- parent density/span presentation is independent from nested child structure;
- simple/complex classification is never changed merely to obtain a header color;
- genuine complex multi-row header hierarchy remains source-faithful;
- terminal header position alone does not imply code/index semantics.

---

## Fixture A — 1×2 support

```text
Nợ TK 632 / Có TK 156 | Theo PP tính giá xuất kho mà DN áp dụng
```

Canonical child: nested `.ct-data-table.is-simple`.

Expected:
- desktop side-by-side;
- mobile stacked cells;
- no child wrapper;
- no horizontal overflow.

---

## Fixture B — 1×3 support

```text
Giá trị | Điều kiện | Ghi chú
```

Expected:
- one-row nested `is-simple`;
- mobile stack all 3 cells in source order;
- no invented headers;
- no horizontal overflow.

---

## Fixture C — multi-row 2-column small matrix

```html
<table>
  <tr><td>Trường hợp A</td><td>Cách xử lý A</td></tr>
  <tr><td>Trường hợp B</td><td>Cách xử lý B</td></tr>
  <tr><td>Trường hợp C</td><td>Cách xử lý C</td></tr>
</table>
```

Canonical child: nested `.ct-data-table.is-simple`.

Expected:
- never Type-B stack;
- remains two-column table on mobile;
- parent is not widened merely for readability;
- child fits parent cell with compact CSS;
- no scroll region at parent or child.

---

## Fixture D — 3-column matrix + `thead`

```text
THEAD: Khoản | Điều kiện | Xử lý
ROWS: ...
```

Canonical child: nested `.ct-data-table.is-simple` when no complex spans.

Expected:
- preserve `thead/th/scope`;
- remains tabular on mobile;
- fits parent cell;
- nested simple header uses quiet light support treatment rather than being reclassified complex;
- no child/outer horizontal scroll.

---

## Fixture E — meaningful rowspan

Expected:
- nested `.ct-data-table.is-complex`;
- exact rowspan preserved;
- no support stacking;
- fit parent cell;
- no sticky/scroll treatment;
- collapsed span-safe border model keeps effective gridlines;
- parent border model is unaffected if parent itself has no spans.

---

## Fixture F — meaningful colspan

Same as E:
- nested complex;
- exact colspan;
- no child wrapper;
- no flattening;
- fit parent;
- collapsed span-safe border model only for the table whose direct cells contain the span.

---

## Fixture G — nested 5-column matrix

Canonical pattern:

```html
<table class="ct-data-table is-complex">
  ...
  <td><table class="ct-data-table is-complex">...</table></td>
</table>
```

If the top-level table is already complex it may retain the canonical compatibility wrapper around the top-level table only.

Expected:
- child remains semantic table;
- child width = parent-cell width;
- no min-width / max-content canvas;
- no horizontal scrollbar anywhere;
- document does not overflow horizontally;
- nested complex `thead`, when present, uses the same light hierarchy as other `is-complex` tables;
- child width/density does not change parent density unless parent independently qualifies.

---

## Fixture H — top-level 5+ columns + child support

Expected:
- parent fits 100% rather than scrolling;
- no sticky first column;
- child support remains local and may stack on mobile;
- complete nested tree fits viewport.

---

## Fixture I — meaningful depth >1

```text
Top-level
  └─ meaningful nested
       └─ meaningful nested
```

Policy:
1. recursively classify deepest;
2. unwrap presentation-only levels when safe;
3. preserve meaningful remaining structure;
4. Needs review;
5. no automatic PASS.

Presentation still fits 100%; the review gate is structural, not responsive-width related.

---

## Fixture J — malformed/ambiguous spans

- do not guess repaired rowspan/colspan;
- preserve safest recoverable structure;
- Needs review;
- no automatic PASS.

---

## Fixture K — segmented form grid, 10+ cells with blank-slot evidence

Example meaning:

```text
[03] Mã số thuế: | □ | □ | □ | □ | □ | □ | □ | □ | □ | □ | □ | □ | □ | □ |
```

Expected canonical semantics:
- every blank slot preserved as a separate `<td>`;
- normally top-level `is-complex` because cell count is high;
- label remains a `<td>` in the same `<tbody>` row;
- all following slot cells are canonical blank cells in the template case;
- **no invented `<thead>` / `<th>`**;
- no new form-grid class required;
- legacy widths/heights removed.

Expected EDS presentation:
- structural heuristic sees `one row + no thead + 10+ cells + blank-slot evidence`;
- generic 11+ ultra-dense matrix typography is overridden;
- desktop row target height about 38px, font about 13px;
- mobile row target height about 32px, font about 10.5px;
- first label cell gets useful width;
- remaining slot cells divide residual fixed-layout width evenly;
- width remains exactly within viewport;
- no scrollbar on desktop/mobile.

---

## Fixture L — 12+ column multi-row header/span matrix

Example characteristics:

```text
12 effective columns
multi-level thead
rowspan + colspan
footer total row
```

Expected:
- exact source span values preserved;
- header hierarchy remains semantic;
- no sticky first-column behavior;
- table `width:100%`, fixed layout;
- progressive typography/padding compression based on this table's own rows;
- span-safe collapsed border model based on this table's own direct span cells;
- no horizontal scrollbar at any viewport;
- because it is `is-complex`, header presentation uses the light hierarchy.

---

## Fixture M — DOM last-child is not effective last column

Purpose: regression for missing vertical separator caused by rowspan occupancy.

Example:

```html
<table>
  <thead>
    <tr>
      <th rowspan="3">A</th>
      <th colspan="2">B group</th>
      <th rowspan="3">D</th>
    </tr>
    <tr>
      <th>B1</th>
      <th rowspan="2">B2</th>
    </tr>
    <tr>
      <th>B1 detail</th>
    </tr>
  </thead>
</table>
```

On the third DOM row, `B1 detail` is the DOM `:last-child`, but it is **not** the effective last column because `B2` and `D` are still occupied by rowspans.

Expected:
- canonical spans unchanged;
- EDS collapsed span-safe grid preserves right separator after `B1 detail`;
- no CSS rule based on `tr > :last-child` may erase this effective internal boundary;
- no missing vertical line.

---

## Fixture N — mixed rowspan + colspan multi-level header

Use a 10–15 effective-column matrix with:

- leading fields `rowspan=3`;
- middle grouped headings `colspan=2..4`;
- secondary headings with their own `rowspan=2`;
- tertiary headings occupying only part of the logical width;
- total/footer `colspan`.

Expected:
- all source spans exact;
- all group boundaries visible;
- every effective vertical separator represented by browser collapsed grid;
- footer boundaries remain consistent;
- outer wrapper only clips/fits, never scrolls;
- no sticky behavior.

This fixture directly models administrative/tax forms such as multi-level declaration schedules.

---

## Fixture O — complex multi-row light-header hierarchy

Use genuine `is-complex` matrices with 1, 2, 3 and 4 `thead` rows.

Expected canonical semantics:
- preserve every genuine source header row;
- preserve exact `rowspan/colspan`;
- remain `is-complex` because structure is actually complex, not because light header is desired;
- no inline style/background/color classes;
- no invented or flattened rows for presentation;
- do not label terminal row as code/index unless source itself says so.

Expected EDS presentation:

```text
first thead row            → #EAF2EE / #244D45 / 700
intermediate rows          → #F5F8F6 / #30463F / 600
normal 2–3 row terminal    → #FFFFFF / #33433D / 700
very deep 4+ row terminal  → #EEF4F1 / #315A50 / 700
complex tfoot th           → #EAF2EE / #244D45 / 700
top-level simple header    → unchanged deep teal / white
nested simple header       → quiet light support header
```

Also verify:
- complex header cells use `vertical-align: middle`;
- light presentation does not remove span-safe gridlines;
- body zebra/hover behavior remains readable;
- no semantic reclassification was performed to alter color.

---

## Fixture P — populated one-row 10+ cell non-form matrix

Purpose: negative regression for over-broad form-slot heuristic.

Example:

```html
<table class="ct-data-table is-complex">
  <tbody>
    <tr>
      <td>A</td><td>B</td><td>C</td><td>D</td><td>E</td>
      <td>F</td><td>G</td><td>H</td><td>I</td><td>J</td>
    </tr>
  </tbody>
</table>
```

Expected:
- NOT a segmented form grid;
- no 32%/36% first-cell label width;
- generic wide-matrix density applies;
- cells remain peer columns under fixed layout;
- no horizontal overflow.

---

## Fixture Q — parent locality: 2-col/no-span parent + 12-col/span child

Purpose: prove nested descendant selectors do not leak into parent.

Example:

```html
<table id="parent" class="ct-data-table is-simple">
  <tbody>
    <tr>
      <td>Parent A</td>
      <td>
        <table id="child" class="ct-data-table is-complex">
          <thead>
            <tr><th rowspan="2">A</th><th colspan="11">Group</th></tr>
            <tr><!-- 11 child headers --></tr>
          </thead>
          <tbody><!-- 12 child cells --></tbody>
        </table>
      </td>
    </tr>
  </tbody>
</table>
```

Expected desktop:

```text
parent font/density       → base 2-col table density
parent border-collapse    → separate
child font/density        → own 11+ density
child border-collapse     → collapse
```

Expected mobile:
- same locality relationship;
- parent does not become 11+ dense because of child;
- parent does not become span-collapsed because of child;
- child independently receives its own compact/span-safe rendering;
- document has no page-level horizontal overflow.

---

# Responsive validation matrix

```text
Desktop: 1280, 1024
Tablet:   900, 768
Mobile:   430, 390, 360, 320
```

Expected policy:

```text
ALL top-level tables               → fit 100%
Type B support                     → desktop side-by-side / mobile stack
Type C small matrix                → remain tabular + fit parent
Type D complex/spans               → remain tabular + fit parent
Segmented form grid                → dedicated density only with blank-slot evidence
Populated wide one-row matrix      → generic matrix density, not form mode
12+ col span matrix                → fit with dense typography + complete gridlines
Top-level simple header            → deep teal / white
Nested simple header               → quiet light
Complex normal terminal leaf       → white / dark
Very deep complex terminal         → subtle accent allowed
Parent/child table heuristics       → independent scopes
Meaningful depth >1                → review / no auto-PASS
Horizontal scrollbar               → NEVER
Sticky first column                → NEVER
```

# Regression pass criteria

- A/B stack only where intended and never overflow;
- C/D remain tabular without parent widening;
- E/F preserve spans and local gridlines;
- G fits nested complex content without inner/outer scroll and without shrinking parent by descendant count;
- H has no sticky/scroll ownership behavior;
- I/J correctly block automatic PASS;
- K preserves every meaningful blank slot, avoids fake headers, retains readable row height and evenly distributed slots;
- L preserves multi-level headers/spans and fits viewport;
- M proves a DOM-last-child internal boundary is not erased;
- N preserves all mixed-span effective gridlines;
- O preserves source header hierarchy and validates generalized light complex-header presentation without inline styling;
- P proves a populated 10+ one-row matrix does not trigger form mode;
- Q proves parent density/border model is independent from nested child density/spans;
- normalized visible text and meaningful associations pass for A–H/K–Q;
- document scrollWidth is not increased by editorial tables at any tested viewport.