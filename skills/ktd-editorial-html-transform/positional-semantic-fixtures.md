# KTD Editorial Transform — Positional Semantic Fixtures

**Bound canonical skill:** v1.4.3  
**Bound EDS:** v2.4.3  
**Purpose:** regression fixtures for meaningful position/group relationships, coherent formal-document/form scope, source-backed formal alignment and contextual official-document presentation.

The fixtures below are semantic contracts, not pixel-perfect snapshots.

---

## P01 — Official header, issuer ↔ authority

### Source intent

```text
LEFT                                  RIGHT
BỘ / CƠ QUAN ...                      CỘNG HÒA ...
Số: 123/...                           Độc lập - Tự do - Hạnh phúc
                                      Hà Nội, ngày ...
```

### Expected canonical shape

```html
<section class="ct-official-document">
  <div class="ct-official-header">
    <div class="ct-official-header__issuer">
      <p>...</p>
      <p>Số: 123/...</p>
    </div>
    <div class="ct-official-header__authority">
      <p>...</p>
      <p>Độc lập - Tự do - Hạnh phúc</p>
      <p>Hà Nội, ngày ...</p>
    </div>
  </div>
</section>
```

### Pass

- wording intact;
- two semantic role groups intact;
- source order intact;
- sanitizer preserves all canonical classes.

### Fail

All text is present but emitted as unrelated serial paragraphs.

---

## P02 — Official header encoded by legacy 1×2 table

### Source

```html
<table style="width:100%">
  <tr>
    <td style="width:50%;text-align:center">CƠ QUAN...<br>Số: ...</td>
    <td style="width:50%;text-align:center">CỘNG HÒA...<br>Độc lập...<br>..., ngày ...</td>
  </tr>
</table>
```

### Expected

Strip table mechanics and inline styles **after** identifying the two semantic role groups. Map to `ct-official-header`; do not preserve a fake data matrix and do not flatten to prose.

---

## P03 — Two-party signature region

### Source intent

```text
NGƯỜI LẬP / NGƯỜI NỘP                 CƠ QUAN / NGƯỜI XÁC NHẬN
(ký, ghi rõ họ tên)                   (ký, đóng dấu...)
```

### Expected

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">
    <p><strong>NGƯỜI LẬP / NGƯỜI NỘP</strong></p>
    <p>(ký, ghi rõ họ tên)</p>
  </div>
  <div class="ct-signature-party">
    <p><strong>CƠ QUAN XÁC NHẬN</strong></p>
    <p>(ký, đóng dấu)</p>
  </div>
</div>
```

### Fail

```html
<p>NGƯỜI LẬP / NGƯỜI NỘP</p>
<p>(ký, ghi rõ họ tên)</p>
<p>CƠ QUAN / NGƯỜI XÁC NHẬN</p>
<p>(ký, đóng dấu...)</p>
```

Even though visible text is complete, the pair relationship is lost.

---

## P04 — Three meaningful signatory parties

Source contains three distinct approval/signature cells.

Expected:

- exactly three `ct-signature-party` children;
- source order preserved;
- each label/note/name remains in its source party;
- no invented party labels.

---

## P05 — Truly decorative 1×2 layout

### Source intent

Left cell contains article prose. Right cell is an empty spacer used only for visual alignment. There is no party, label/value, official or counterpart relation.

Expected: Type-A/layout-only unwrap is allowed. Preserve visible prose order. Do not invent a positional component.

---

## P06 — Text coverage false positive

Source contains two meaningful signatory parties. Transformed output retains 100% normalized visible text but removes party wrappers and serializes lines.

Expected Step-4 result:

```text
Source Coverage: 100%
Visible Text: PASS
Positional Fidelity: FAIL
Final: FAIL — FIX BEFORE PUBLISH
```

This fixture is the main v2.4.x regression guard.

---

## P07 — Sanitizer survival

### Input

```html
<section class="ct-official-document rogue">
  <div class="ct-official-header rogue">
    <div class="ct-official-header__issuer rogue"><p>A</p></div>
    <div class="ct-official-header__authority rogue"><p>B</p></div>
  </div>
  <div class="ct-signature-grid rogue">
    <div class="ct-signature-party rogue"><p>C</p></div>
    <div class="ct-signature-party rogue"><p>D</p></div>
  </div>
</section>
```

### Expected sanitized structure

```html
<section class="ct-official-document">
  <div class="ct-official-header">
    <div class="ct-official-header__issuer"><p>A</p></div>
    <div class="ct-official-header__authority"><p>B</p></div>
  </div>
  <div class="ct-signature-grid">
    <div class="ct-signature-party"><p>C</p></div>
    <div class="ct-signature-party"><p>D</p></div>
  </div>
</section>
```

Arbitrary `rogue` class is stripped; canonical classes survive.

---

## P08 — Conflicting section roots

### Input

```html
<section class="ct-official-document ct-accounting-group">...</section>
```

Expected sanitizer behavior: do not choose one root by guess; strip conflicting section root classes and surface the existing unsupported-format warning path.

---

## P09 — Mobile presentation

Canonical HTML has two `ct-signature-party` children in source order.

At narrow viewport CSS may stack them vertically.

Expected semantic result: PASS, because group wrappers and source order remain intact. Responsive stacking is presentation, not transform-time flattening.

---

## P10 — Ordinary legal prose is not Official Document

Source is an article paragraph explaining a tax regulation and cites an Article/Clause, but has no formal document header/form structure.

Expected: ordinary prose / legal callout / source note as justified by source. Do **not** wrap entire article in `ct-official-document`.

---

## P11 — Ambiguous official roles

Source has a clear two-party/side structure but evidence is insufficient to safely name one side `issuer` vs `authority`.

Expected: preserve the safest recoverable grouping/structure and mark Needs review. Do not invent role semantics merely to force canonical official-header classes.

---

## P12 — Signature table nested in a larger form

A complex form table contains one cell with a nested 1×2 signature table.

Expected:

1. classify parent independently;
2. classify nested signature relationship before Type-A unwrap;
3. map nested signatory groups to `ct-signature-grid` when safe;
4. do not let nested signature structure change parent table density/classification;
5. no nested `ct-table-scroll` invented.

---

## P13 — One formal signer anchored right by a blank left companion

### Source intent

A formal/official document ends with a one-row two-cell signature layout:

```text
LEFT: blank / unused                   RIGHT: centered signer block
                                       KT. CỤC TRƯỞNG
                                       PHÓ CỤC TRƯỞNG

                                       Đặng Ngọc Minh
```

The left cell has no visible text, but its existence plus the populated right cell is evidence that the **single signer region is intentionally anchored to the right**. The signer text is centered inside that right region; it is not centered across the full document.

### Expected canonical shape

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">
    <p><strong>KT. CỤC TRƯỞNG</strong></p>
    <p><strong>PHÓ CỤC TRƯỞNG</strong></p>
    <p><strong>Đặng Ngọc Minh</strong></p>
  </div>
</div>
```

### Required semantics

- exactly one `ct-signature-party`;
- no fake/empty party created for the blank left source cell;
- blank companion may be removed only after its positional evidence has been mapped;
- signer region remains right-anchored at larger viewport presentation;
- signer text remains centered inside its own region;
- mobile may expand the one-party grid to full width without changing canonical grouping;
- no `ct-left`, `ct-right` or generic two-column class invented.

### Fail

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">...</div>
  <div class="ct-signature-party"></div>
</div>
```

because it invents a semantic party that does not exist.

Also FAIL:

```html
<p><strong>KT. CỤC TRƯỞNG</strong></p>
<p><strong>PHÓ CỤC TRƯỞNG</strong></p>
<p><strong>Đặng Ngọc Minh</strong></p>
```

when that output becomes a full-width centered signature region, because visible text survives but the source-backed right-side anchoring is lost.

---

## P14 — Coherent official tax form scope

### Source intent

A legacy tax form is encoded as a contiguous sequence of headings/divs/tables:

```text
Phụ lục / TÊN BIỂU MẪU / mã biểu mẫu
[01] Kỳ tính thuế
[02] Tên người nộp thuế
[03] Mã số thuế: | blank slots ...
[04] Tên đại lý thuế
[05] Mã số thuế: | blank slots ...
large administrative matrix [06]...[24]
unit / abbreviation legend
Tôi cam đoan ...
LEFT PARTY: NHÂN VIÊN ĐẠI LÝ THUẾ
RIGHT PARTY: NGƯỜI NỘP THUẾ / ĐẠI DIỆN HỢP PHÁP
```

A separate article `Xem thêm:` block follows after the form.

### Expected canonical shape

```html
<section class="ct-official-document">
  <!-- exact source-backed form title / coded fields -->

  <!-- form-slot tables stay canonical form-slot/data-table structures -->

  <!-- administrative matrix keeps its own is-complex/header/span semantics -->

  <p>...Tôi cam đoan...</p>

  <div class="ct-signature-grid">
    <div class="ct-signature-party">
      <!-- NHÂN VIÊN ĐẠI LÝ THUẾ + its own fields -->
    </div>
    <div class="ct-signature-party">
      <!-- date + NGƯỜI NỘP THUẾ / ĐẠI DIỆN... + signature note -->
    </div>
  </div>
</section>

<!-- Xem thêm / article content remains outside -->
```

### Required semantics

- one justified `ct-official-document` scope encloses the coherent form-owned range;
- child form-slot/simple/complex tables retain their independent semantics;
- two signature parties remain distinct and source ordered;
- `ct-official-header` is **not required** because this source form does not necessarily contain an issuer↔authority pair;
- no invented quốc hiệu, issuing agency or form metadata;
- form-owned legend/declaration stays inside;
- article lead-in and post-form `Xem thêm` remain outside when source does not make them part of the form;
- no additional `ct-form-card` or `ct-signature-box` class is introduced;
- outer official-document frame is the primary visual boundary; signature grid does not need a nested card frame.

---

## P15 — Fragmented-form false PASS must fail

### Source intent

Same coherent form as P14.

### Incorrect canonical result

Every child is individually transformed correctly:

```text
form title / coded fields
form-slot grid
complex administrative table
declaration
2-party ct-signature-grid
```

but all are emitted as unrelated article-root siblings without a surrounding `section.ct-official-document` even though source evidence clearly establishes one form boundary.

### Expected Step-4 result

```text
Source Coverage: 100%
Visible Text Fidelity: PASS
Table Fidelity: PASS
Positional Signature Fidelity: PASS
Formal Form Scope Fidelity: FAIL
Final: FAIL — FIX BEFORE PUBLISH
```

This fixture prevents a false PASS where local semantics are correct but document-level scope is lost.

Also FAIL when the transformer wraps unrelated article lead-in or post-form `Xem thêm` inside the form despite clear source boundary evidence.

---

## P16 — Article content ABOUT a form is not automatically content OF the form

### Source intent

The article contains:

```text
ARTICLE H2:
Mẫu 05-2/BK-QTT-TNCN Bảng kê chi tiết cá nhân ...

EDITORIAL WARNING:
Chú ý: Mẫu 05-2/BK-QTT-TNCN này thay thế cho mẫu ...

PRINTED FORM START:
Phụ lục
BẢNG KÊ CHI TIẾT CÁ NHÂN
THUỘC DIỆN TÍNH THUẾ THEO THUẾ SUẤT TOÀN PHẦN
(Kèm theo ...)
[01] Kỳ tính thuế ...
...
```

The article heading describes the form, and the warning explains/replaces the form, but source structure shows the printed form itself begins at `Phụ lục` / the formal title block.

### Expected canonical boundary

```html
<h2>Mẫu 05-2/BK-QTT-TNCN ...</h2>

<div class="ct-content-box is-warning">
  ...
</div>

<section class="ct-official-document">
  <p class="ct-align-center">
    <strong>Phụ lục</strong><br>
    <strong>BẢNG KÊ CHI TIẾT CÁ NHÂN</strong><br>
    ...
  </p>
  ...
</section>
```

### Pass

- article H2 stays outside;
- editorial warning stays outside;
- official scope starts at the first source-backed printed-form content;
- source order remains intact.

### Fail

The transformer wraps the article H2 and editorial warning inside `ct-official-document` merely because they discuss the same form.

Canonical shorthand:

> **Content ABOUT a formal document is not automatically content OF that formal document.**

---

## P17 — Source-backed formal alignment is preserved

### Source intent

Inside a genuine official form:

```text
CENTER:
Phụ lục
BẢNG KÊ CHI TIẾT CÁ NHÂN
...
[01] Kỳ tính thuế ...

RIGHT, directly above the matrix:
Đơn vị tiền: Đồng Việt Nam
```

Source alignment is part of the document identity/relationship: the title block is centered as the formal form heading, while the unit label is anchored to the matrix edge.

### Expected canonical shape

```html
<section class="ct-official-document">
  <p class="ct-align-center">...</p>
  ...
  <p class="ct-align-right"><em>Đơn vị tiền: Đồng Việt Nam</em></p>
  ...
</section>
```

### Pass

- no inline `text-align` survives;
- existing canonical alignment classes preserve source-backed formal positioning;
- no alignment is invented where source lacks evidence.

### Fail

All wording survives but both lines are normalized to ordinary left-aligned prose, causing the formal title/unit relationship to be lost.

This is a positional/formal-alignment fidelity failure, not a reason to preserve arbitrary legacy alignment everywhere.

---

## P18 — Official-document table presentation is contextual, not semantic reclassification

### Source intent

Two structurally identical simple matrices exist:

1. ordinary editorial table outside any official document;
2. official-form table inside `section.ct-official-document`.

Both are semantically `ct-data-table is-simple`.

### Expected canonical HTML

```html
<table class="ct-data-table is-simple">...</table>

<section class="ct-official-document">
  <table class="ct-data-table is-simple">...</table>
</section>
```

### Presentation contract

- outside official scope: ordinary editorial simple-table treatment remains available, including deep-teal header/white text;
- inside official scope: CSS may use a more formal-neutral paper/document treatment, quieter header tones, tighter/squarer geometry, subdued/no zebra and no row-hover emphasis;
- semantic class remains `is-simple` in both cases;
- the transformer must never choose `is-simple`/`is-complex` to obtain a preferred color treatment;
- form-slot and complex tables inside official scope receive the same contextual formal-document visual language while preserving their own semantics.

### Fail

- transformer invents `ct-official-table`, `is-government`, `is-formal-table` or another presentation class;
- table is reclassified simple↔complex merely because it is inside an official document;
- contextual CSS leaks out and removes the established editorial simple-table treatment outside `ct-official-document`.

---

# Completion gate

The positional/form-scope suite passes only when:

```text
P01–P04 preserve party/role grouping and source order
P05 still permits genuine layout-only cleanup
P06 blocks text-only false PASS
P07 canonical classes survive sanitizer
P08 conflicting section roots are not guessed
P09 responsive stack keeps semantic grouping
P10 prevents over-classification
P11 preserves ambiguity instead of inventing roles
P12 preserves parent/child locality
P13 preserves one-party right-side anchoring without inventing a blank party
P14 preserves one coherent formal-form scope while keeping child semantics independent
P15 blocks false PASS when child fidelity succeeds but form scope is lost or over-wrapped
P16 separates article content ABOUT a form from printed content OF the form
P17 preserves source-backed formal alignment without preserving arbitrary legacy alignment
P18 keeps official-table presentation contextual/CSS-owned without semantic reclassification or global visual regression
```