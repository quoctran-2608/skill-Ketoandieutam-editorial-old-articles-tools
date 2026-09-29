# KTD Editorial Transform — QA Checklist

**Applies to:** EDS v2.3.4 — Inline Emphasis Hierarchy + Adaptive / Embedded Tables / Skill v1.3.2  
**Canonical EDS reference:** `docs/21-content-editorial-design-system.md`

Use this checklist after every transformation.

## A. Content fidelity

- [ ] No sentence was rewritten.
- [ ] No paragraph meaning changed.
- [ ] No factual statement was added.
- [ ] No factual statement was removed silently.
- [ ] The complete visible text of any title-like first body block was audited.
- [ ] A title-like first block was removed only when external masthead metadata confirmed an exact/no-information duplicate.
- [ ] If the title-like first block contained additional scope/context, that content was preserved as `ct-article-intro`.
- [ ] If article title metadata was unavailable, title-like opening text was preserved as `ct-article-intro` and flagged for review rather than deleted.
- [ ] Source item boundaries are preserved: sibling items do not collapse into one continuous text run.
- [ ] Label → description relationships remain attached to the correct source item.
- [ ] Meaningful nested table cell associations are preserved; a left/right or row/column relation was not flattened into unrelated sequential paragraphs.
- [ ] All monetary values match source.
- [ ] All percentages match source.
- [ ] All dates match source.
- [ ] All account codes/names match source.
- [ ] Every visible `Nợ` / `Có` is preserved correctly.
- [ ] Legal document names/numbers match source.
- [ ] Formulas match source.
- [ ] Top-level and meaningful nested table cell values match source.
- [ ] Quoted text matches source.
- [ ] Meaningful source emphasis was evaluated before legacy colors/backgrounds were stripped.

## B. Heading hierarchy + opening title

- [ ] No H1 exists in article body.
- [ ] A title-like first H1/H2 was classified before body hierarchy was finalized.
- [ ] Content-preservation decision and heading-rebase decision were made separately.
- [ ] An exact duplicate title did not remain as a fake H2.
- [ ] A meaningful opening title did not disappear just to fix hierarchy.
- [ ] If source H2 acted as title-root, source H3 major sections were promoted to canonical H2 where appropriate.
- [ ] If source H1 acted as title-root, source H2 major sections remained canonical H2.
- [ ] Rebase affected only the structural subtree owned by that root.
- [ ] Major sections use H2.
- [ ] Subsections use H3.
- [ ] H4 is used only as a local sub-subsection.
- [ ] Legacy visual size/color/background was not used as sole hierarchy evidence.
- [ ] H2 contains semantic heading text only; Fresh Gold decoration remains CSS-owned.

## C. Article intro

- [ ] `ct-article-intro` is used only for meaningful title-like opening scope/context.
- [ ] Intro text is copied from source, not rewritten/summarized.
- [ ] `ct-article-intro` is not used for ordinary middle-of-article prose.
- [ ] Intro does not participate in the H2/H3/H4 tree.
- [ ] Exact duplicate with no added meaning is not unnecessarily preserved as intro when masthead metadata confirms duplication.
- [ ] Missing metadata case is reported under Needs review.

## D. Prose, lists and inline emphasis

- [ ] Ordinary paragraphs remain paragraphs.
- [ ] Normal grouped items use UL/OL.
- [ ] Sibling members introduced by wording such as “có N tài khoản cấp 2”, “gồm các loại”, “gồm các nhóm”, or “gồm các trường hợp” are evaluated as a normal peer list before considering Definition List.
- [ ] A repeated pattern `strong label + explanation` is not automatically converted to `ct-definition-list`.
- [ ] When peer items are converted to `<li>`, legacy `-`/`•` markers used only as presentation are not duplicated inside item text.
- [ ] Each peer-list item remains a separate `<li>` so the renderer cannot visually concatenate neighboring items.
- [ ] Checklist is used only for genuine checklist/requirements.
- [ ] Steps are used only for ordered procedures.
- [ ] No card-per-bullet conversion occurred.
- [ ] Ordinary local emphasis uses `strong` where sufficient.
- [ ] `ct-key-emphasis` is used only for a longer scan-worthy clause/list-like phrase with meaningful emphasis.
- [ ] `ct-key-emphasis` was not created merely because source text was red.
- [ ] `ct-key-highlight` is used only for a short decisive condition/exception/threshold/scope phrase.
- [ ] Legacy red text was not automatically converted to `ct-key-highlight`.
- [ ] Legacy yellow/cyan background was not automatically converted to `ct-key-highlight`.
- [ ] `ct-key-highlight` does not wrap a long paragraph/list.
- [ ] `ct-key-emphasis` and `ct-key-highlight` are not nested; overlapping meanings are split when needed.
- [ ] No red/yellow/blue/green highlight variant class was invented.

## E. Content boxes

- [ ] `is-note` is a genuine insight/principle.
- [ ] `is-info` is neutral additional information.
- [ ] `is-warning` is a real risk/error/penalty warning.
- [ ] `is-legal` is genuinely legal/official-rule content.
- [ ] `is-example` is a real example/case/calculation.
- [ ] Callouts are not overused.
- [ ] Legacy color alone did not determine semantic type.
- [ ] Fresh Editorial colors/tints were not encoded into HTML.

## F. Key lines / source notes

- [ ] `is-formula` is an actual compact formula/calculation rule.
- [ ] `is-process` is an actual compact process chain.
- [ ] `is-result` is a resolved final answer/conclusion, not every paragraph containing a number.
- [ ] Formula and result are distinguished when both appear.
- [ ] `ct-source-note` is used only for a source/citation line present in source.
- [ ] Citation text was not invented/corrected/updated.
- [ ] A full legal explanation was not reduced to source-note when `is-legal` is appropriate.

## G. Accounting

- [ ] Accounting markup is used only for actual journal entries.
- [ ] Every explicit Nợ line has `is-debit` when transformed to accounting-entry markup.
- [ ] Every explicit Có line has `is-credit` when transformed to accounting-entry markup.
- [ ] Nợ/Có preserved inside semantic comparison/support tables remains literal source text if table structure is the primary owner.
- [ ] No debit/credit was inferred from account type alone.
- [ ] Ambiguous lines use neutral fallback.
- [ ] Visible side label remains in `ct-accounting-entry__side` when accounting-entry markup is used.
- [ ] Related entries are grouped only when semantically related.
- [ ] Debit/credit colors are CSS-owned.

## H. Definition / Fact list

- [ ] Definition List is used for genuine glossary/term → definition structures, not merely any bold label followed by explanation.
- [ ] A declared family of peer members (for example TK 2141/2142/2143/2147 under “có 4 tài khoản cấp 2”) uses normal UL/LI unless the source genuinely functions as a glossary.
- [ ] Definition terms can stand independently as concepts being defined; if they are simply sibling members of one category, prefer UL/LI.
- [ ] Fact list is used for key → concise value metadata.
- [ ] No DL is used only for visual two-column layout.
- [ ] Long narrative values are not forced into Fact List.
- [ ] When list vs definition is ambiguous, the simpler normal list/prose structure is preferred and ambiguity is reported rather than forcing DL.

## I. Tables

- [ ] Table remains semantic table data when row/column boundaries carry meaning.
- [ ] Header cells use TH where appropriate.
- [ ] `scope` is added where clear.
- [ ] Simple/complex classification is reasonable.
- [ ] Top-level complex table is wrapped in `.ct-table-scroll`.
- [ ] No data cells were merged/split without source evidence.
- [ ] No data table was converted to an image.
- [ ] No fixed inline widths remain.
- [ ] Every nested table was classified before flattening or unwrap.
- [ ] A single-cell/spacer-only nested table was unwrapped only when its cell boundaries carried no semantic association.
- [ ] A nested one-row 2–3-cell table with meaningful cross-column relation is preserved as nested `.ct-data-table.is-simple`.
- [ ] Embedded support table is **not** wrapped in a second `.ct-table-scroll`.
- [ ] Embedded support table preserves original cell order and left/right association.
- [ ] The right-hand explanation/note was not converted into a later unrelated paragraph.
- [ ] Genuine nested data matrix is not flattened merely to avoid nested-table presentation complexity.
- [ ] EDS CSS, not article HTML, owns whether embedded cells remain side-by-side or stack on mobile.

## J. Media

- [ ] Existing safe image URL preserved.
- [ ] Alt text preserved where available.
- [ ] Caption preserved.
- [ ] No image/R2 URL invented.
- [ ] No inline width/style added.

## K. Links

- [ ] Existing safe href preserved exactly.
- [ ] No URL invented.
- [ ] No relative URL guessed into an absolute URL.
- [ ] Removed/unsafe link is reported.
- [ ] No SEO/internal link insertion occurred.

## L. HTML cleanliness

- [ ] No inline style remains.
- [ ] No legacy font tag remains.
- [ ] No font/color/background/border/shadow/spacing presentation remains inline.
- [ ] Google Sans is not encoded in canonical HTML.
- [ ] No arbitrary presentation class remains.
- [ ] No unsupported `ct-*` class was invented.
- [ ] No event handler or `data-*` attribute was added.
- [ ] No script/iframe/embed/object markup remains.
- [ ] Empty presentation wrappers/paragraphs removed where safe.
- [ ] No consecutive blank physical lines exist.
- [ ] Meaningful `pre`/code whitespace is preserved.
- [ ] Whitespace cleanup does not change visible text/semantic structure.

## M. Visual ownership / EDS v2.3.4

- [ ] Canonical HTML expresses semantic structure only.
- [ ] EDS typography/palette/H2 decoration is not duplicated inline.
- [ ] Normal peer lists rely on shared EDS list CSS; no per-article list styling is added.
- [ ] `ct-article-intro` does not encode its font-size/color/margin inline.
- [ ] `ct-key-emphasis` does not encode bronze/color/weight inline.
- [ ] `ct-key-highlight` does not encode cream/green paint inline.
- [ ] `ct-source-note` does not encode alignment/italic/font-size inline.
- [ ] `is-result` does not encode green background/border inline.
- [ ] Embedded support table does not carry source width/cellpadding/cellspacing/style attributes.
- [ ] Responsive behavior is not encoded per article.
- [ ] CSS/system ownership wins over per-article visual hacks.

## N. Sanitizer compatibility

- [ ] Output uses only allowed canonical tags/classes.
- [ ] Normal peer lists use sanitizer-native `ul`/`li`/`strong` without requiring a new class.
- [ ] Nested support table uses existing sanitizer-supported `table.ct-data-table.is-simple` / `tbody` / `tr` / `td` vocabulary.
- [ ] `p.ct-article-intro` matches sanitizer contract.
- [ ] `span.ct-key-emphasis` matches sanitizer contract.
- [ ] `mark.ct-key-highlight` matches sanitizer contract.
- [ ] `p.ct-source-note` matches sanitizer contract.
- [ ] `.ct-key-line` has exactly one variant among `is-process`, `is-formula`, `is-result`.
- [ ] Accounting variants are not conflicting.
- [ ] `ct-definition-list` / `ct-fact-list` are not combined.
- [ ] Heading IDs, if used, are sanitizer-safe.

## O. Conversion report

- [ ] Converted section lists meaningful structural conversions.
- [ ] Conversion of a sibling-member block to normal UL/LI is reported when material.
- [ ] Preservation of a meaningful nested support table is reported when material.
- [ ] Conversion to `ct-article-intro` is reported when applicable.
- [ ] Heading rebasing is reported when it changes source levels.
- [ ] Semantic recovery from legacy emphasis is reported when material.
- [ ] Removed section lists only true presentation removals and metadata-confirmed exact title duplicates.
- [ ] Needs review lists intro classification when title metadata was unavailable.
- [ ] Needs review lists ambiguous list-vs-definition/emphasis/hierarchy/accounting/link/media/nested-table issues.
- [ ] No review note is hidden inside article HTML.

## Pass criteria

A transformed article passes only if:

1. source meaning, meaningful visible text, source item boundaries and meaningful nested table associations are intact;
2. opening title-like content was never deleted without metadata-confirmed exact duplication;
3. title-root handling was separated from heading-tree repair;
4. real major body sections begin at H2;
5. peer-member enumerations are not over-classified as Definition Lists;
6. meaningful nested mini-tables are not blindly flattened;
7. `ct-article-intro`, `ct-key-emphasis`, `ct-key-highlight` and existing semantics are used correctly;
8. meaningful legacy emphasis is classified rather than copied as arbitrary color;
9. sanitizer compatibility is expected;
10. low-confidence decisions are surfaced;
11. no presentation hacks remain in HTML;
12. canonical source whitespace is deterministic and clean.

For corpus migration, do not proceed until 20–30 difficult fixtures — including exact-title, intro-preservation, missing-metadata, emphasis-heavy red/yellow/cyan, peer-account/member-list, dense comparison table and meaningful nested support-table cases — have passed this checklist with human review.
