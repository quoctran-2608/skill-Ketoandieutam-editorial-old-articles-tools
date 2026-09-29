# KTD Editorial Transform — Content-box Sanitizer Fixtures

**Applies to:** EDS v2.3.10 / Skill v1.3.8 / Compact v1.0.2

These fixtures guard the sanitizer-safe callout contract discovered during the TSCĐ article regression.

## R — Canonical content box survives unchanged

Input:

```html
<div class="ct-content-box is-example">
  <p class="ct-content-box__title">Ví dụ 2. TSCĐ là vườn cây lâu năm</p>
  <div class="ct-content-box__body"><p>Nội dung ví dụ.</p></div>
</div>
```

Expected semantic classes after `sanitizeEditorialHtml()`:

```text
root div → ct-content-box is-example
p        → ct-content-box__title
body div → ct-content-box__body
```

## S — Legacy ASIDE root remains readable for migration

Input:

```html
<aside class="ct-content-box is-example">
  <p class="ct-content-box__title">Ví dụ cũ</p>
  <div class="ct-content-box__body"><p>Nội dung.</p></div>
</aside>
```

Expected after sanitizer:

```text
aside → ct-content-box is-example preserved
```

Transformer action on the next canonical transform:

```text
normalize root aside → div
```

Legacy preservation is compatibility only, not canonical generation permission.

## T — Legacy BLOCKQUOTE root remains readable for migration

Input:

```html
<blockquote class="ct-content-box is-legal">
  <p>Quy định pháp lý.</p>
</blockquote>
```

Expected after sanitizer:

```text
blockquote → ct-content-box is-legal preserved
```

Transformer must normalize this to canonical `div.ct-content-box.is-legal` on a new transform.

## U — Legacy DIV title remains readable for migration

Input:

```html
<div class="ct-content-box is-example">
  <div class="ct-content-box__title">Ví dụ cũ</div>
  <div class="ct-content-box__body"><p>Nội dung.</p></div>
</div>
```

Expected after sanitizer:

```text
title div → ct-content-box__title preserved
```

Transformer must normalize title `div` → canonical `p`.

## V — Orphan variant is stripped

Input:

```html
<div class="is-warning">Không có owning ct-content-box class.</div>
```

Expected:

```text
class is-warning stripped
visible text preserved
```

## W — Root with no variant stays generic

Input:

```html
<div class="ct-content-box">Nội dung chưa có semantic variant.</div>
```

Expected sanitizer behavior:

```text
ct-content-box preserved
no is-note/is-info/is-warning/is-legal/is-example is invented
```

Transformer QA must still reject this as incomplete new canonical output because generation requires exactly one source-backed semantic variant.

## X — Conflicting root variants stay generic

Input:

```html
<div class="ct-content-box is-warning is-example">Nội dung.</div>
```

Expected sanitizer behavior:

```text
ct-content-box preserved
all conflicting semantic variants removed
no arbitrary winner is chosen
```

Transformer QA must reject such conflicting new output before sanitizer; canonical generation always emits exactly one variant.

## Y — Regression shape from TSCĐ article

Legacy transform shape:

```html
<div class="ct-content-box is-example">
  <div class="ct-content-box__title">Ví dụ 1. TSCĐ hữu hình hình thành do đầu tư xây dựng theo phương thức giao thầu</div>
  <div class="ct-content-box__body">
    <p>...</p>
    <table class="ct-data-table is-simple">...</table>
  </div>
</div>
<div class="ct-content-box is-example">
  <div class="ct-content-box__title">Ví dụ 2. TSCĐ là vườn cây lâu năm</div>
  <div class="ct-content-box__body"><p>...</p></div>
</div>
```

Regression expectation:

1. sanitizer does not strip the two content-box roots or titles;
2. EDS therefore retains box padding/margins/title treatment;
3. table remains the final semantic child of Example 1 without needing an artificial `<br>`/empty paragraph;
4. Example 2 is visually separated by existing component rhythm;
5. future transformer output keeps the same neutral `div` roots but normalizes legacy title `div` elements to canonical `p` titles.

## PASS gate

PASS only if:

```text
canonical div/p/div contract survives sanitizer
legacy aside/blockquote roots survive for migration safety
legacy div title survives for migration safety
orphan variants are stripped
generic root with no variant does not become is-note
conflicting variants do not resolve to an arbitrary semantic type
new canonical transformer output contains no aside/blockquote content-box root and no div title
no CSS/per-article spacing hack is required to repair this regression
```
