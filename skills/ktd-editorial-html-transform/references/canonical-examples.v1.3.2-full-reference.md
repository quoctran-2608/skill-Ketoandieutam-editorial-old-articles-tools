# KTD Editorial Transform — Canonical Examples

**Applies to:** EDS v2.3.4 — Inline Emphasis Hierarchy + Adaptive / Embedded Tables / Skill v1.3.2  
**Canonical EDS reference:** `docs/21-content-editorial-design-system.md`

These examples illustrate semantic decisions. They are not permission to rewrite source content or encode visual presentation into HTML.

Canonical snippets intentionally avoid presentation-only blank lines. CSS owns spacing.

---

## Example 1 — Legacy inline-styled warning

### Input

```html
<div style="background:#fee;color:red;padding:20px">
  <p><strong>Lưu ý:</strong> Nộp hồ sơ quá thời hạn có thể phát sinh xử phạt.</p>
</div>
```

### Canonical

```html
<aside class="ct-content-box is-warning">
  <p class="ct-content-box__title">Lưu ý</p>
  <div class="ct-content-box__body">
    <p>Nộp hồ sơ quá thời hạn có thể phát sinh xử phạt.</p>
  </div>
</aside>
```

Reason: meaning is warning/risk; legacy red is not itself the reason.

---

## Example 2 — Accounting entry from indented paragraphs

### Input

```html
<p style="margin-left:40px"><strong>Nợ TK 642:</strong> 10.000.000 đồng</p>
<p style="margin-left:40px"><strong>Nợ TK 133:</strong> 1.000.000 đồng</p>
<p style="margin-left:40px"><strong>Có TK 111:</strong> 11.000.000 đồng</p>
```

### Canonical

```html
<div class="ct-accounting-entry">
  <p class="ct-accounting-entry__title">Định khoản</p>
  <div class="ct-accounting-entry__line is-debit">
    <strong class="ct-accounting-entry__side">Nợ</strong>
    <span>TK 642: 10.000.000 đồng</span>
  </div>
  <div class="ct-accounting-entry__line is-debit">
    <strong class="ct-accounting-entry__side">Nợ</strong>
    <span>TK 133: 1.000.000 đồng</span>
  </div>
  <div class="ct-accounting-entry__line is-credit">
    <strong class="ct-accounting-entry__side">Có</strong>
    <span>TK 111: 11.000.000 đồng</span>
  </div>
</div>
```

---

## Example 3 — Genuine definition list

### Input

```html
<p><strong>Khấu hao:</strong> Việc phân bổ có hệ thống giá trị phải khấu hao của tài sản trong suốt thời gian sử dụng hữu ích.</p>
<p><strong>Giá trị còn lại:</strong> Nguyên giá sau khi trừ giá trị hao mòn lũy kế.</p>
```

### Canonical

```html
<dl class="ct-definition-list">
  <dt>Khấu hao</dt>
  <dd>Việc phân bổ có hệ thống giá trị phải khấu hao của tài sản trong suốt thời gian sử dụng hữu ích.</dd>
  <dt>Giá trị còn lại</dt>
  <dd>Nguyên giá sau khi trừ giá trị hao mòn lũy kế.</dd>
</dl>
```

Reason: each `dt` is a genuine term being defined. This is not merely a list of sibling members in one category.

---

## Example 4 — Fact list

### Input

```html
<p><strong>Số văn bản:</strong> 99/2025/TT-BTC</p>
<p><strong>Cơ quan ban hành:</strong> Bộ Tài chính</p>
<p><strong>Ngày hiệu lực:</strong> 01/01/2026</p>
```

### Canonical

```html
<dl class="ct-fact-list">
  <dt>Số văn bản</dt>
  <dd>99/2025/TT-BTC</dd>
  <dt>Cơ quan ban hành</dt>
  <dd>Bộ Tài chính</dd>
  <dt>Ngày hiệu lực</dt>
  <dd>01/01/2026</dd>
</dl>
```

---

## Example 5 — Simple table

```html
<table class="ct-data-table is-simple">
  <thead><tr><th scope="col">Nội dung</th><th scope="col">Mức áp dụng</th></tr></thead>
  <tbody><tr><td>...</td><td>...</td></tr></tbody>
</table>
```

---

## Example 6 — Complex table

```html
<div class="ct-table-scroll">
  <table class="ct-data-table is-complex">
    <thead><tr><th scope="col">...</th><th scope="col">...</th><th scope="col">...</th><th scope="col">...</th></tr></thead>
    <tbody><tr><td>...</td><td>...</td><td>...</td><td>...</td></tr></tbody>
  </table>
</div>
```

---

## Example 7 — Compact formula

### Input

```html
<p><strong>Thuế phải nộp = Doanh thu tính thuế × Thuế suất</strong></p>
```

### Canonical

```html
<p class="ct-key-line is-formula"><strong>Thuế phải nộp = Doanh thu tính thuế × Thuế suất</strong></p>
```

---

## Example 8 — Process

### Input

```html
<p>Chứng từ → Hạch toán → Sổ sách → Báo cáo → Quyết toán</p>
```

### Canonical

```html
<p class="ct-key-line is-process"><strong>Chứng từ → Hạch toán → Sổ sách → Báo cáo → Quyết toán</strong></p>
```

---

## Example 9 — Legal block

```html
<aside class="ct-content-box is-legal">
  <p class="ct-content-box__title">Căn cứ pháp lý</p>
  <div class="ct-content-box__body"><p>...</p></div>
</aside>
```

Do not update/correct legal content in FORMAT-ONLY mode.

---

## Example 10 — Ambiguous accounting line

### Input

```html
<p>TK 3331: 5.000.000 đồng</p>
```

### Canonical

```html
<div class="ct-accounting-entry__line">
  <strong class="ct-accounting-entry__side">TK</strong>
  <span>3331: 5.000.000 đồng</span>
</div>
```

### QA

```text
Needs review
- The source does not explicitly identify whether TK 3331 is Nợ or Có in this line.
```

---

## Example 11 — Presentation-only bold paragraph

### Input

```html
<p style="font-size:18px;color:#006633"><strong>Doanh nghiệp cần lưu ý nội dung sau.</strong></p>
```

### Canonical

```html
<p><strong>Doanh nghiệp cần lưu ý nội dung sau.</strong></p>
```

Do not manufacture a card from visual prominence alone.

---

## Example 12 — Unsupported wrapper

### Input

```html
<div class="legacy-red-card" style="border:3px solid red"><p>Nội dung có ý nghĩa cần giữ.</p></div>
```

### Canonical

```html
<p>Nội dung có ý nghĩa cần giữ.</p>
```

---

## Example 13 — H2 visual signature belongs to CSS

### Input

```html
<p style="font-size:28px;font-weight:700;border-bottom:2px solid #d0a13a">Quản lý doanh thu theo từng kênh</p>
```

### Canonical

```html
<h2>Quản lý doanh thu theo từng kênh</h2>
```

Do not reproduce the gold rule in HTML.

---

## Example 14 — Legacy font/colors removed

### Input

```html
<p style="font-family:'Times New Roman';font-size:16px;color:#145238">Dữ liệu cần được đối chiếu định kỳ.</p>
```

### Canonical

```html
<p>Dữ liệu cần được đối chiếu định kỳ.</p>
```

---

## Example 15 — Exact duplicate body title may be removed

CMS title metadata:

```text
Hướng dẫn cách hạch toán các khoản chi phí khác - Tài khoản 811
```

### Input

```html
<h2>Hướng dẫn cách hạch toán các khoản chi phí khác - <strong>Tài khoản 811</strong></h2>
<p>Áp dụng chế độ kế toán theo Thông tư...</p>
<h3>1. Tài khoản 811 - Chi phí khác</h3>
<h4>Nguyên tắc kế toán</h4>
<h3>2. Kết cấu và nội dung Tài khoản 811</h3>
```

Because the first H2 is an external-metadata-confirmed **no-information duplicate**, canonical may remove it:

```html
<p>Áp dụng chế độ kế toán theo Thông tư...</p>
<h2>1. Tài khoản 811 - Chi phí khác</h2>
<h3>Nguyên tắc kế toán</h3>
<h2>2. Kết cấu và nội dung Tài khoản 811</h2>
```

### QA

```text
Removed
- Exact duplicate body title fully represented by the masthead title metadata.
```

---

## Example 16 — Decisive short condition → `ct-key-highlight`

### Input

```html
<p>Nguyên giá là toàn bộ các chi phí <span style="color:red">tính đến thời điểm đưa tài sản vào trạng thái sẵn sàng sử dụng</span>.</p>
```

### Canonical

```html
<p>Nguyên giá là toàn bộ các chi phí <mark class="ct-key-highlight">tính đến thời điểm đưa tài sản vào trạng thái sẵn sàng sử dụng</mark>.</p>
```

Do not preserve red.

---

## Example 17 — Short legal attribution → source note

### Input

```html
<p style="text-align:right"><em>(Theo Khoản 1 Điều 4 Thông tư 45/2013/TT-BTC)</em></p>
```

### Canonical

```html
<p class="ct-source-note">(Theo Khoản 1 Điều 4 Thông tư 45/2013/TT-BTC)</p>
```

---

## Example 18 — Formula and resolved result differ

### Input

```html
<p><strong>Nguyên giá = Giá mua + Chi phí trực tiếp</strong></p>
<p style="background:#f0ffff"><strong>Nguyên giá chính thức: 8.700.000.000 đồng</strong></p>
```

### Canonical

```html
<p class="ct-key-line is-formula"><strong>Nguyên giá = Giá mua + Chi phí trực tiếp</strong></p>
<p class="ct-key-line is-result"><strong>Nguyên giá chính thức: 8.700.000.000 đồng</strong></p>
```

---

## Example 19 — Color alone is not enough

### Input

```html
<p><span style="color:red">Kế toán Diệu Tâm</span> hướng dẫn nội dung sau.</p>
```

### Canonical

```html
<p>Kế toán Diệu Tâm hướng dẫn nội dung sau.</p>
```

---

## Example 20 — Title-like opening with extra scope → `ct-article-intro`

Assume CMS title metadata is:

```text
Cách tính nguyên giá TSCĐ hữu hình
```

### Input

```html
<h2>Hướng dẫn cách tính Nguyên giá TSCĐ hữu hình, cách xác định nguyên giá TSCĐ mua sắm, xây dựng, sản xuất, được cho biếu tặng, mua trả chậm, trả góp, góp vốn...</h2>
<p>Căn cứ pháp lý...</p>
<h3>1) Cách xác định Nguyên giá TSCĐ hữu hình mua sắm</h3>
<h3>2) Cách xác định Nguyên giá TSCĐ hữu hình tự xây dựng hoặc tự sản xuất</h3>
```

The first H2 overlaps with the masthead title but adds meaningful scope. **Do not delete it.**

### Canonical

```html
<p class="ct-article-intro">Hướng dẫn cách tính Nguyên giá TSCĐ hữu hình, cách xác định nguyên giá TSCĐ mua sắm, xây dựng, sản xuất, được cho biếu tặng, mua trả chậm, trả góp, góp vốn...</p>
<p>Căn cứ pháp lý...</p>
<h2>1) Cách xác định Nguyên giá TSCĐ hữu hình mua sắm</h2>
<h2>2) Cách xác định Nguyên giá TSCĐ hữu hình tự xây dựng hoặc tự sản xuất</h2>
```

The source H2 text is preserved exactly while its heading-root role is removed.

---

## Example 21 — Title-like opening without metadata → intro + review

### Input

```html
<h2>Hướng dẫn cách tính Nguyên giá TSCĐ hữu hình, gồm nhiều trường hợp...</h2>
<h3>1) Mua sắm</h3>
<h3>2) Tự xây dựng</h3>
```

No CMS title metadata is supplied.

### Canonical

```html
<p class="ct-article-intro">Hướng dẫn cách tính Nguyên giá TSCĐ hữu hình, gồm nhiều trường hợp...</p>
<h2>1) Mua sắm</h2>
<h2>2) Tự xây dựng</h2>
```

### QA

```text
Needs review
- The first H2 was a high-confidence title-root and was preserved as ct-article-intro because masthead title metadata was unavailable.
```

**Never delete this opening text without metadata.**

---

## Example 22 — Long legacy red clause → `ct-key-emphasis`

### Input

```html
<p>
  ... như:
  <span style="color:red">lãi tiền vay phát sinh trong quá trình đầu tư mua sắm tài sản cố định; chi phí vận chuyển, bốc dỡ; chi phí nâng cấp; chi phí lắp đặt, chạy thử; lệ phí trước bạ và các chi phí liên quan trực tiếp khác.</span>
</p>
```

The clause is long, scan-worthy and meaningfully emphasized, but a background highlight across the whole span would be too heavy.

### Canonical

```html
<p>... như: <span class="ct-key-emphasis">lãi tiền vay phát sinh trong quá trình đầu tư mua sắm tài sản cố định; chi phí vận chuyển, bốc dỡ; chi phí nâng cấp; chi phí lắp đặt, chạy thử; lệ phí trước bạ và các chi phí liên quan trực tiếp khác.</span></p>
```

Do not preserve red and do not convert the whole clause to `ct-key-highlight`.

---

## Example 23 — Emphasis + highlight should be split, not nested

### Input meaning

A longer emphasized clause contains one short decisive timing condition.

### Canonical pattern

```html
<p>
  <span class="ct-key-emphasis">Các chi phí liên quan trực tiếp phải chi ra</span>
  <mark class="ct-key-highlight">tính đến thời điểm đưa TSCĐ vào trạng thái sẵn sàng sử dụng</mark>
  <span class="ct-key-emphasis">như chi phí vận chuyển, bốc dỡ, lắp đặt, chạy thử...</span>
</p>
```

Avoid nesting one semantic inside the other.

---

## Example 24 — Peer account members → normal list, not definition list

### Input

```html
<p><strong>Tài khoản 214 - Hao mòn TSCĐ, có 4 tài khoản cấp 2:</strong></p>
<p style="margin-left:40px"><strong>- Tài khoản 2141 - Hao mòn TSCĐ hữu hình:</strong> Phản ánh giá trị hao mòn của TSCĐ hữu hình trong quá trình sử dụng...</p>
<p style="margin-left:40px"><strong>- Tài khoản 2142 - Hao mòn TSCĐ thuê tài chính:</strong> Phản ánh giá trị hao mòn của TSCĐ thuê tài chính trong quá trình sử dụng...</p>
<p style="margin-left:40px"><strong>- Tài khoản 2143 - Hao mòn TSCĐ vô hình:</strong> Phản ánh giá trị hao mòn của TSCĐ vô hình trong quá trình sử dụng...</p>
<p style="margin-left:40px"><strong>- Tài khoản 2147 - Hao mòn BĐSĐT:</strong> Tài khoản này phản ánh giá trị hao mòn BĐSĐT dùng để cho thuê hoạt động...</p>
```

These are four sibling members of one declared family, not four glossary terms. Preserve the item boundaries with a normal list and keep each label attached to its explanation.

### Canonical

```html
<p><strong>Tài khoản 214 - Hao mòn TSCĐ, có 4 tài khoản cấp 2:</strong></p>
<ul>
  <li><strong>Tài khoản 2141 - Hao mòn TSCĐ hữu hình:</strong> Phản ánh giá trị hao mòn của TSCĐ hữu hình trong quá trình sử dụng...</li>
  <li><strong>Tài khoản 2142 - Hao mòn TSCĐ thuê tài chính:</strong> Phản ánh giá trị hao mòn của TSCĐ thuê tài chính trong quá trình sử dụng...</li>
  <li><strong>Tài khoản 2143 - Hao mòn TSCĐ vô hình:</strong> Phản ánh giá trị hao mòn của TSCĐ vô hình trong quá trình sử dụng...</li>
  <li><strong>Tài khoản 2147 - Hao mòn BĐSĐT:</strong> Tài khoản này phản ánh giá trị hao mòn BĐSĐT dùng để cho thuê hoạt động...</li>
</ul>
```

The source hyphens are presentation/list markers and are not duplicated inside the `<li>` text.

Use the same rule for sibling categories such as “có N loại”, “gồm các trường hợp”, “gồm các nhóm”, “có các tài khoản cấp 2”, or similar peer-member enumerations.

Do **not** transform this pattern to `.ct-definition-list` merely because each item has a bold label followed by explanatory prose.

---

## Example 25 — Meaningful nested support table must not be flattened

### Input

```html
<td>
  <p><strong>Bút toán 2: Ghi nhận giá vốn bán hàng</strong></p>
  <table border="0">
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
  <p>(Đối với những doanh nghiệp tính giá xuất kho theo PP bình quân gia quyền...)</p>
</td>
```

The nested 2-cell row is not merely a spacer. Its left/right boundary communicates that the explanatory note applies to the paired `Nợ/Có` block. Flattening it to three sequential paragraphs destroys that association.

### Canonical

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
  <p>(Đối với những doanh nghiệp tính giá xuất kho theo PP bình quân gia quyền...)</p>
</td>
```

Rules demonstrated:

- keep the support table nested;
- classify it `is-simple`;
- do not wrap it in `.ct-table-scroll`;
- strip source widths/borders/cellspacing/padding presentation;
- preserve both nested cell boundaries and visible text;
- EDS CSS keeps it side-by-side on wider screens and stacks its cells on mobile;
- do not flatten merely because nested tables are visually inconvenient.
