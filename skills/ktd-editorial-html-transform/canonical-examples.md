# KTD Editorial Transform — Canonical Examples

**Applies to:** EDS v2.4.3 / Skill v1.4.3 / Compact v1.1.3  
**Canonical EDS reference:** `docs/21-content-editorial-design-system.md`

These examples illustrate semantic decisions. They are not permission to rewrite source content or encode presentation into article HTML.

The v1.4.3 set is additive: it preserves the mature v1.3.8 examples, retains all v1.4.1 official-document/signature positional cases, retains v1.4.2 formal-form scope cases, and adds official-boundary/formal-alignment/contextual-presentation cases.

---

## Example 1 — Warning from legacy red box

Input:

```html
<div style="background:#fee;color:red;padding:20px"><p><strong>Lưu ý:</strong> Nộp hồ sơ quá hạn có thể phát sinh xử phạt.</p></div>
```

Canonical:

```html
<div class="ct-content-box is-warning">
  <p class="ct-content-box__title">Lưu ý</p>
  <div class="ct-content-box__body"><p>Nộp hồ sơ quá hạn có thể phát sinh xử phạt.</p></div>
</div>
```

Reason: warning meaning, not red paint.

The content-box tag contract is fixed: `div` root + optional source-backed `p.ct-content-box__title` + `div.ct-content-box__body`. Do not emit new `aside.ct-content-box`, `blockquote.ct-content-box`, or `div.ct-content-box__title`. Sanitizer support for those legacy shapes is migration compatibility only.

---

## Example 2 — Accounting entry without invented title

Source explicitly says:

```text
Nợ TK 642: 10.000.000 đồng
Có TK 111: 10.000.000 đồng
```

Canonical:

```html
<div class="ct-accounting-entry">
  <div class="ct-accounting-entry__line is-debit">
    <strong class="ct-accounting-entry__side">Nợ</strong>
    <span>TK 642: 10.000.000 đồng</span>
  </div>
  <div class="ct-accounting-entry__line is-credit">
    <strong class="ct-accounting-entry__side">Có</strong>
    <span>TK 111: 10.000.000 đồng</span>
  </div>
</div>
```

Only use debit/credit when explicit in source. Because the source did not contain a standalone title, do **not** invent `Định khoản`.

If source genuinely contains a standalone label/title, `p.ct-accounting-entry__title` may preserve that source-backed text.

---

## Example 3 — Genuine definition list

```html
<dl class="ct-definition-list">
  <dt>Khấu hao</dt>
  <dd>Việc phân bổ có hệ thống giá trị phải khấu hao...</dd>
  <dt>Giá trị còn lại</dt>
  <dd>Nguyên giá sau khi trừ giá trị hao mòn lũy kế.</dd>
</dl>
```

This is glossary semantics, not a peer-member family.

---

## Example 4 — Peer account members

Input meaning:

```text
Tài khoản 214 có 4 tài khoản cấp 2:
- TK 2141: ...
- TK 2142: ...
```

Canonical:

```html
<p><strong>Tài khoản 214 có 4 tài khoản cấp 2:</strong></p>
<ul>
  <li><strong>Tài khoản 2141:</strong> ...</li>
  <li><strong>Tài khoản 2142:</strong> ...</li>
</ul>
```

Do not use Definition List merely because labels are bold.

---

## Example 5 — Fact list

```html
<dl class="ct-fact-list">
  <dt>Số văn bản</dt><dd>99/2025/TT-BTC</dd>
  <dt>Ngày hiệu lực</dt><dd>01/01/2026</dd>
</dl>
```

Use this only when the source is genuinely concise metadata-like key→value information.

---

## Example 6 — Simple top-level table

```html
<table class="ct-data-table is-simple">
  <thead>
    <tr><th scope="col">Nội dung</th><th scope="col">Mức áp dụng</th></tr>
  </thead>
  <tbody>
    <tr><td>...</td><td>...</td></tr>
  </tbody>
</table>
```

EDS presentation: top-level simple header uses deep teal + white text. This presentation does not justify changing a complex source table into `is-simple`.

---

## Example 7 — Complex top-level table

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">
    <thead>
      <tr>
        <th scope="col">A</th><th scope="col">B</th><th scope="col">C</th>
        <th scope="col">D</th><th scope="col">E</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
    </tbody>
  </table>
</div>
```

The wrapper remains canonical/backward-compatible, but EDS fits the complete table to `100%`; it is **not** a horizontal-scroll request. `is-complex` receives the light header hierarchy from CSS.

---

## Example 8 — Formula vs result

```html
<p class="ct-key-line is-formula"><strong>Nguyên giá = Giá mua + Chi phí trực tiếp</strong></p>
<p class="ct-key-line is-result"><strong>Nguyên giá chính thức: 8.700.000.000 đồng</strong></p>
```

Use these only when source meaning supports formula/result semantics.

---

## Example 9 — Article title with extra scope

Input:

```html
<h2>Hướng dẫn cách tính Nguyên giá TSCĐ hữu hình, gồm mua sắm, xây dựng, sản xuất...</h2>
<h3>1) Mua sắm</h3>
<h3>2) Tự xây dựng</h3>
```

Without metadata confirming an exact/no-information duplicate:

```html
<p class="ct-article-intro">Hướng dẫn cách tính Nguyên giá TSCĐ hữu hình, gồm mua sắm, xây dựng, sản xuất...</p>
<h2>1) Mua sắm</h2>
<h2>2) Tự xây dựng</h2>
```

Opening preservation and heading rebase are separate decisions.

---

## Example 10 — Key emphasis vs highlight

```html
<p>
  <span class="ct-key-emphasis">Các chi phí liên quan trực tiếp phải chi ra</span>
  <mark class="ct-key-highlight">tính đến thời điểm đưa tài sản vào trạng thái sẵn sàng sử dụng</mark>
  <span class="ct-key-emphasis">như vận chuyển, lắp đặt, chạy thử...</span>
</p>
```

Do not nest emphasis/highlight. Do not choose either solely from legacy color.

---

# Nested/table examples — retained from v1.3.8

## Example 11 — Type A: truly layout-only wrapper → unwrap

Input:

```html
<td>
  <table><tr><td><p>Nội dung bình thường.</p></td></tr></table>
</td>
```

If the nested cell boundary and position carry no meaning:

```html
<td><p>Nội dung bình thường.</p></td>
```

This example does **not** authorize flattening official/signature relations. Positional gate must run first.

---

## Example 12 — Type B: 1×2 support relation

Input meaning:

```text
Nợ TK 632 / Có TK 156  |  Theo PP tính giá xuất kho mà DN áp dụng
```

Canonical:

```html
<table class="ct-data-table is-simple">
  <tbody>
    <tr>
      <td><p>Nợ TK 632</p><p>Có TK 156</p></td>
      <td><p>Theo PP tính giá xuất kho mà DN áp dụng</p></td>
    </tr>
  </tbody>
</table>
```

Desktop: side-by-side. Mobile: may stack. No child wrapper.

---

## Example 13 — Type B: 1×3 support relation

```html
<table class="ct-data-table is-simple">
  <tbody>
    <tr><td>Giá trị</td><td>Điều kiện</td><td>Ghi chú</td></tr>
  </tbody>
</table>
```

With no header/spans and a single local support row, mobile may stack in source order.

---

## Example 14 — Type C: multi-row 2-column matrix

```html
<table class="ct-data-table is-simple">
  <tbody>
    <tr><td>Trường hợp A</td><td>Cách xử lý A</td></tr>
    <tr><td>Trường hợp B</td><td>Cách xử lý B</td></tr>
    <tr><td>Trường hợp C</td><td>Cách xử lý C</td></tr>
  </tbody>
</table>
```

This stays tabular on mobile. Do **not** stack every cell like Type B. Do not widen/promote its parent merely for viewport width; CSS fits matrix to parent cell.

---

## Example 15 — Type C: small matrix with `thead`

```html
<table class="ct-data-table is-simple">
  <thead>
    <tr><th scope="col">Khoản</th><th scope="col">Điều kiện</th><th scope="col">Xử lý</th></tr>
  </thead>
  <tbody>
    <tr><td>...</td><td>...</td><td>...</td></tr>
  </tbody>
</table>
```

Meaningful header makes this a matrix, not support relation. If nested, EDS may use quiet light support header while semantics remain `is-simple`.

---

## Example 16 — Type D: rowspan → nested complex

```html
<table class="ct-data-table is-complex">
  <tbody>
    <tr><td rowspan="2">Nhóm A</td><td>Xử lý 1</td></tr>
    <tr><td>Xử lý 2</td></tr>
  </tbody>
</table>
```

Preserve `rowspan`; never support-stack this table. EDS fits it to parent width and uses span-safe collapsed grid borders for the child itself.

---

## Example 17 — Type D: colspan → nested complex

```html
<table class="ct-data-table is-complex">
  <thead><tr><th colspan="2">Thông tin chung</th></tr></thead>
  <tbody><tr><td>A</td><td>B</td></tr></tbody>
</table>
```

Preserve exact span value. EDS owns border rendering; transformer does not alter span to “fix” lines.

---

## Example 18 — Nested complex matrix: no parent widening

Canonical:

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">
    <tbody>
      <tr>
        <td>
          <table class="ct-data-table is-complex">
            <tbody>
              <tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
            </tbody>
          </table>
        </td>
        <td>...</td>
      </tr>
    </tbody>
  </table>
</div>
```

There is no child wrapper. Outer compatibility wrapper does not instruct scrolling. Parent and child both fit available width. Each table computes own density from own rows.

---

## Example 19 — Parent 5+ columns + child support relation

Parent remains `width:100%`; no sticky first column and no horizontal scroll. Child support remains nested `is-simple` and may stack on mobile.

Child complexity must not be used to reclassify or widen parent.

---

## Example 20 — Meaningful depth >1

```text
Top-level table
  └─ meaningful nested table
       └─ meaningful nested table
```

Do not blindly flatten. Recursively remove presentation-only levels where safe. If meaningful depth >1 remains:

```text
Needs review
- Meaningful nested-table depth exceeds automatic depth-1 support; content/relationships were preserved and human review is required.
```

The transformation does not automatically PASS.

---

## Example 21 — Malformed spans

If source `rowspan/colspan` is ambiguous or malformed, do not invent repaired values. Preserve safest recoverable structure and flag Needs review.

---

## Example 22 — Accounting table remains table-owned

If a comparison matrix contains literal Nợ/Có inside cells and cell relationship is primary, keep literal Nợ/Có in cells. Do not create accounting cards inside every table cell unless source structure clearly calls for separate accounting-entry components.

---

## Example 23 — No horizontal table scrollbar

Forbidden transform/presentation assumptions:

```text
5+ columns → scroll
nested complex → widen parent
sticky first column
min-width: 720px / 960px
width: max-content
```

Canonical HTML may still contain top-level compatibility wrapper:

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">...</table>
</div>
```

but CSS must fit table to wrapper rather than scroll it.

---

## Example 24 — Segmented form grid: preserve body cells, do not invent header

Source meaning:

```text
[03] Mã số thuế: | blank | blank | blank | blank | ...
```

Canonical:

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">
    <tbody>
      <tr>
        <td><strong>[03]</strong> Mã số thuế:</td>
        <td></td><td></td><td></td><td></td><td></td>
        <td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td>
      </tr>
    </tbody>
  </table>
</div>
```

Required:

- all blank slots remain separate cells;
- label remains body `<td>`;
- **do not create `<thead>` or `<th>`** because label is first/bold;
- remove legacy cell widths/heights;
- blank-slot evidence, not cell count alone, distinguishes this from populated matrix;
- EDS owns readable form-row density/height and slot distribution.

---

## Example 25 — Wide multi-level span matrix

A 12+ column table with multi-row `thead`, `rowspan` and `colspan` remains semantic `is-complex`. Preserve every span and header relationship.

EDS:

- fits complete matrix to viewport width;
- uses no sticky column or horizontal scrollbar;
- switches only the table whose own direct cells contain spans to collapsed grid-border model;
- renders complex headers with generalized light hierarchy.

---

## Example 26 — DOM `:last-child` is not effective last column

Source grid:

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

In third DOM row, `B1 detail` is `:last-child`, but effective columns continue through `B2` and `D` rowspans.

Transformer action: **none beyond preserving exact spans/cell order**.

EDS action: collapsed span grid keeps the right separator after `B1 detail`. Never mutate HTML to compensate for CSS border heuristics.

---

## Example 27 — Complex multi-row header hierarchy

Canonical:

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">
    <thead>
      <tr>
        <th rowspan="3">STT</th>
        <th colspan="4">Thu nhập chịu thuế (TNCT)</th>
        <th colspan="2">Số thuế TNCN đã khấu trừ</th>
      </tr>
      <tr>
        <th rowspan="2">Tổng số</th>
        <th colspan="2">Trong đó: TNCT được giảm thuế</th>
        <th rowspan="2">Khoản khác</th>
        <th rowspan="2">Tổng số</th>
        <th rowspan="2">Trong đó...</th>
      </tr>
      <tr>
        <th>Làm việc tại KKT</th>
        <th>Theo Hiệp định</th>
      </tr>
      <tr>
        <th>[06]</th><th>[11]</th><th>[13]</th><th>[14]</th><th>[15]</th><th>[16]</th><th>[17]</th>
      </tr>
    </thead>
  </table>
</div>
```

Transformer requirements:

- preserve genuine header rows;
- preserve exact row/col spans;
- keep `is-complex` because structure is genuinely complex;
- do not add style/presentation classes or fake rows;
- do not reclassify to obtain preferred color;
- do not assign code/index semantics to terminal row unless source supports it.

EDS renders first/intermediate levels with light tonal hierarchy. Normal 2–3-row terminal leaf is white; very deep 4+ row administrative header may use subtle terminal accent.

---

## Example 28 — Populated wide one-row table is not a form-slot grid

Input:

```html
<table>
  <tr>
    <td>A</td><td>B</td><td>C</td><td>D</td><td>E</td>
    <td>F</td><td>G</td><td>H</td><td>I</td><td>J</td>
  </tr>
</table>
```

This is **not** automatically segmented form grid. There are no blank character slots after a field label.

Canonical keeps normal matrix structure/classification. EDS applies generic wide-matrix density; it must not give first cell form-label width.

---

## Example 29 — Parent/child selector locality

Canonical:

```html
<table class="ct-data-table is-simple">
  <tbody>
    <tr>
      <td>Parent A</td>
      <td>
        <table class="ct-data-table is-complex">
          <thead>
            <tr><th rowspan="2">A</th><th colspan="11">Group</th></tr>
            <tr><th>B1</th><th>B2</th><th>B3</th><th>B4</th><th>B5</th><th>B6</th><th>B7</th><th>B8</th><th>B9</th><th>B10</th><th>B11</th></tr>
          </thead>
          <tbody><tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr></tbody>
        </table>
      </td>
    </tr>
  </tbody>
</table>
```

Expected presentation ownership:

```text
parent → 2-column base density, border-collapse separate
child  → own 11+ density, border-collapse collapse
```

Transformer does not add locality class. EDS selectors inspect direct rows/cells of each table rather than descendant rows/cells.

---

## Example 30 — Full table fidelity principle

A transform may change table shell/presentation, but it must not change:

- cell visible text;
- meaningful empty slots;
- row/cell order;
- header hierarchy;
- spans;
- Nợ/Có;
- amounts/dates/account codes;
- meaningful associations;
- parent/child locality.

For complete stress fixtures, use `nested-table-fixtures.md`.

---

# Positional-semantic examples — retained from v1.4.2

## Example 31 — Official document header from legacy 1×2 table

Source intent:

```text
LEFT                                  RIGHT
BỘ / CƠ QUAN ...                      CỘNG HÒA ...
Số: 123/...                           Độc lập - Tự do - Hạnh phúc
                                      Hà Nội, ngày ...
```

A legacy source may implement this as a one-row two-cell table. The table mechanics are presentation, but the two **role groups** are meaningful.

Canonical when evidence supports the roles:

```html
<section class="ct-official-document">
  <div class="ct-official-header">
    <div class="ct-official-header__issuer">
      <p><strong>BỘ / CƠ QUAN ...</strong></p>
      <p>Số: 123/...</p>
    </div>
    <div class="ct-official-header__authority">
      <p><strong>CỘNG HÒA ...</strong></p>
      <p>Độc lập - Tự do - Hạnh phúc</p>
      <p>Hà Nội, ngày ...</p>
    </div>
  </div>
  ...
</section>
```

Required:

- preserve exact source words;
- preserve internal line order;
- preserve issuer↔authority grouping;
- remove legacy table mechanics only after mapping the relationship;
- do not invent missing document lines;
- do not replace whole header/document with `ct-content-box.is-legal`.

---

## Example 32 — Two-party signature / confirmation region

Source intent:

```text
NGƯỜI NỘP / KÝ                  ↔                  CƠ QUAN XÁC NHẬN / KÝ
```

Canonical:

```html
<div class="ct-signature-grid">
  <div class="ct-signature-party">
    <p><strong>NGƯỜI NỘP</strong></p>
    <p>(Ký, ghi rõ họ tên)</p>
  </div>
  <div class="ct-signature-party">
    <p><strong>CƠ QUAN XÁC NHẬN</strong></p>
    <p>(Ký, đóng dấu)</p>
  </div>
</div>
```

Preserve meaningful party count, source order and membership. CSS may stack parties on mobile; wrappers remain.

---

## Example 33 — Text preserved but relation lost = FAIL

Incorrect transform:

```html
<p><strong>NGƯỜI NỘP</strong></p>
<p>(Ký, ghi rõ họ tên)</p>
<p><strong>CƠ QUAN XÁC NHẬN</strong></p>
<p>(Ký, đóng dấu)</p>
```

All words survived, but original two-party parallel relation was serialized into generic prose.

Step-4 result must be:

```text
Visible Text Fidelity: PASS
Positional Fidelity: FAIL
Final Result: FAIL — FIX BEFORE PUBLISH
```

This is the central positional anti-regression rule.

---

## Example 34 — Truly decorative 1×2 layout can still unwrap

Source has meaningful prose in the left cell and an empty right cell used only for visual spacing. There is no second party, role, label/value relation, official header, signatory or counterpart association.

Expected:

- positional gate returns NO;
- unwrap presentation-only table shell;
- preserve prose order;
- do not invent positional component.

The rule is **not** “preserve every two-column layout”. The rule is:

> classify relationship first, then remove presentation-only markup only when no meaning is lost.

---

## Example 35 — Ordinary legal prose is not Official Document

Source:

```text
Theo Khoản ... Điều ..., doanh nghiệp cần ...
```

Possible canonical forms are ordinary prose, `ct-source-note`, or `ct-content-box.is-legal` if source structure/function supports a substantive legal rule quotation.

Do **not** wrap article in `ct-official-document` merely because it cites law.

---

## Example 36 — Ambiguous official roles

Source clearly contains two parallel official-looking groups, but evidence is insufficient to safely name one `issuer` and the other `authority`.

Expected:

- preserve grouping/relationship with the safest supported structure;
- do not invent role labels merely to force a component;
- record Needs review;
- never serialize the groups merely to avoid ambiguity.

---

## Example 37 — Signature table nested in larger form

Source:

```text
Parent form matrix
  └─ one cell contains nested 1×2 signatory table
```

Expected reasoning:

1. classify parent independently;
2. classify nested signatory relation before Type-A unwrap;
3. map nested parties to `ct-signature-grid` when evidence is sufficient;
4. preserve source party order/membership;
5. do not let nested signature structure reclassify parent table;
6. do not invent nested `ct-table-scroll`.

---

## Example 38 — Final fidelity principle before form-scope addition

A valid transform may change legacy presentation technology, but it must preserve:

```text
wording
facts
item boundaries
heading meaning
emphasis meaning
accounting sides
cell/row/header/span relationships
meaningful blank slots
parent/child table relationships
issuer↔authority grouping
signatory/approval party grouping
safe source references
```

Canonical shorthand:

> **Legacy paint/layout is evidence. Meaning determines semantic structure. Meaningful positional relationship > layout-only cleanup. CSS owns final presentation.**

---

# Formal-form scope examples — retained from v1.4.2

## Example 39 — Coherent tax form stays one Official Document scope

Source intent:

```text
Phụ lục / TÊN BIỂU MẪU / mã biểu mẫu
[01] Kỳ tính thuế
[02] Tên người nộp thuế
[03] Mã số thuế: segmented blank slots
[04] Tên đại lý thuế
[05] Mã số thuế: segmented blank slots
administrative multi-row/span matrix [06]...[24]
(KKT: ...; BH: ...; DN: ...)
Tôi cam đoan ...
LEFT: NHÂN VIÊN ĐẠI LÝ THUẾ
RIGHT: NGƯỜI NỘP THUẾ / ĐẠI DIỆN HỢP PHÁP
```

A separate article `Xem thêm:` block follows afterward.

Canonical skeleton:

```html
<section class="ct-official-document">
  <p><strong>Phụ lục</strong></p>
  <p><strong>TÊN BIỂU MẪU ...</strong></p>
  <p><strong>[01]</strong> Kỳ tính thuế: ...</p>
  <p><strong>[02]</strong> Tên người nộp thuế: ...</p>

  <div class="ct-table-scroll">
    <table class="ct-data-table is-complex">
      <tbody>
        <tr>
          <td><strong>[03]</strong> Mã số thuế:</td>
          <td></td><td></td><td></td><td></td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- [04]/[05] and the large administrative matrix keep their own table semantics -->

  <p><em>(KKT: ...; BH: ...; DN: ...)</em></p>
  <p>Tôi cam đoan ...</p>

  <div class="ct-signature-grid">
    <div class="ct-signature-party">
      <p><strong>NHÂN VIÊN ĐẠI LÝ THUẾ</strong></p>
      <p>Họ và tên: ...</p>
      <p>Chứng chỉ hành nghề số: ...</p>
    </div>
    <div class="ct-signature-party">
      <p>..., ngày ... tháng ... năm ...</p>
      <p><strong>NGƯỜI NỘP THUẾ hoặc<br>ĐẠI DIỆN HỢP PHÁP CỦA NGƯỜI NỘP THUẾ</strong></p>
      <p><em>Ký, ghi rõ họ tên; chức vụ và đóng dấu(nếu có)</em></p>
    </div>
  </div>
</section>

<p>Xem thêm: ...</p>
```

Required:

- exactly one source-backed `ct-official-document` boundary for the coherent form;
- child form-slot and complex matrices keep their own semantics;
- two signature parties keep source order/membership;
- no `ct-official-header` is invented merely because this is an official form;
- no national heading/agency/date is invented;
- `Xem thêm` remains outside when it is article content after the form;
- no separate `ct-form-card`/`ct-signature-box` is invented;
- outer official-document frame provides the main visual boundary; child table borders remain table-owned.

---

## Example 40 — Children correct but formal-form scope lost = FAIL

Incorrect transform:

```text
form title at article root
coded fields at article root
correct form-slot table
correct complex administrative table
correct declaration paragraph
correct two-party ct-signature-grid
```

All text, table cells, spans and signature parties may be individually correct.

But if source clearly proves those pieces belong to one coherent official form and output does **not** preserve a `section.ct-official-document` boundary around the form-owned range:

```text
Visible Text Fidelity: PASS
Table Fidelity: PASS
Positional Signature Fidelity: PASS
Formal Form Scope Fidelity: FAIL
Final Result: FAIL — FIX BEFORE PUBLISH
```

Over-wrapping is also a failure when unrelated article lead-in or post-form `Xem thêm` is absorbed inside the form despite clear source boundaries.

Canonical shorthand for v1.4.2:

> **Preserve local semantics and preserve the source-backed semantic scope that owns them. A form is more than the sum of its tables.**

---

# Official-document fidelity examples — v1.4.3

## Example 41 — ABOUT the form ≠ OF the form

Source sequence:

```text
ARTICLE H2:
Mẫu 05-2/BK-QTT-TNCN Bảng kê chi tiết cá nhân ...

EDITORIAL WARNING:
Chú ý: Mẫu 05-2/BK-QTT-TNCN này thay thế cho mẫu ...

PRINTED FORM:
Phụ lục
BẢNG KÊ CHI TIẾT CÁ NHÂN
THUỘC DIỆN TÍNH THUẾ THEO THUẾ SUẤT TOÀN PHẦN
(Kèm theo ...)
[01] Kỳ tính thuế ...
...
```

Correct canonical boundary:

```html
<h2>Mẫu 05-2/BK-QTT-TNCN Bảng kê chi tiết cá nhân ...</h2>

<div class="ct-content-box is-warning">
  <p class="ct-content-box__title">Chú ý:</p>
  <div class="ct-content-box__body">
    <p>Mẫu 05-2/BK-QTT-TNCN này thay thế cho mẫu ...</p>
  </div>
</div>

<section class="ct-official-document">
  <p class="ct-align-center">
    <strong>Phụ lục</strong><br>
    <strong>BẢNG KÊ CHI TIẾT CÁ NHÂN</strong><br>
    <strong>THUỘC DIỆN TÍNH THUẾ THEO THUẾ SUẤT TOÀN PHẦN</strong><br>
    <em>(Kèm theo ...)</em><br>
    <strong>[01]</strong> Kỳ tính thuế ...
  </p>
  ...
</section>
```

The article heading and editorial warning discuss the form but are not printed content of the form when source boundary evidence places the printed form start at `Phụ lục` / formal title block.

Blocking rule:

> **Content ABOUT a formal document is not automatically content OF that formal document.**

Wrapping the H2/warning into `ct-official-document` is an over-wrap failure even if visible text and local callout semantics are correct.

---

## Example 42 — Preserve source-backed formal alignment

Source shows:

```text
CENTER:
Phụ lục
BẢNG KÊ CHI TIẾT CÁ NHÂN
...
[01] Kỳ tính thuế ...

RIGHT ABOVE MATRIX:
Đơn vị tiền: Đồng Việt Nam
```

Canonical:

```html
<section class="ct-official-document">
  <p class="ct-align-center">
    <strong>Phụ lục</strong><br>
    <strong>BẢNG KÊ CHI TIẾT CÁ NHÂN</strong><br>
    ...
  </p>

  ...

  <p class="ct-align-right"><em>Đơn vị tiền: Đồng Việt Nam</em></p>

  ...
</section>
```

This does **not** authorize preserving arbitrary legacy alignment. Preserve alignment only when source evidence shows it participates in formal-document identity/relationship, such as formal title centering, issuer/authority positioning, place/date, unit label at the matrix edge or signature/approval positioning.

Text preserved but meaningful formal alignment normalized away = positional/formal-alignment fidelity failure.

---

## Example 43 — Same table semantics, contextual official-document presentation

Canonical HTML:

```html
<table class="ct-data-table is-simple">
  <thead><tr><th>Nội dung</th><th>Mức áp dụng</th></tr></thead>
  <tbody><tr><td>...</td><td>...</td></tr></tbody>
</table>

<section class="ct-official-document">
  <table class="ct-data-table is-simple">
    <thead><tr><th>Nội dung</th><th>Mức áp dụng</th></tr></thead>
    <tbody><tr><td>...</td><td>...</td></tr></tbody>
  </table>
</section>
```

Both tables remain `is-simple` because their structures are semantically simple.

Presentation ownership:

```text
outside ct-official-document
→ ordinary editorial simple-table presentation may remain deep teal / white

inside ct-official-document
→ CSS may switch to restrained formal-neutral document treatment
→ quieter header tones
→ squarer geometry
→ subdued/no zebra
→ no row-hover emphasis
```

No transform-side class or semantic reclassification is allowed merely to obtain the formal visual treatment.

Forbidden inventions:

```text
ct-official-table
is-government
is-formal-table
```

Canonical shorthand for v1.4.3:

> **Semantic table class stays semantic. The official-document ancestor owns contextual presentation.**