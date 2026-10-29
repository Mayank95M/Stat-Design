# Design Research Statistics

A single-file statistics workbench for design science research: inter-coder
agreement and theme analysis on the qualitative side, parametric and
non-parametric inference on the quantitative side, and a decision guide that
recommends a test and tells you what to do with the result.

Everything runs in the browser. No server, no build step, no dependencies, and
no data ever leaves the machine.

---

## Deploying it

`index.html` is the whole application. Pick whichever of these suits you.

**Netlify (fastest).** Go to <https://app.netlify.com/drop> and drag the
`design-stats` folder onto the page. You get a live URL in about ten seconds.

**GitHub Pages.** Create a repository, put `index.html` at the root, then in
Settings → Pages set the source to `main` / root. It publishes at
`https://<username>.github.io/<repo>/`.

**Vercel.** `vercel deploy` from inside the folder, or drag it into the
dashboard.

**Any shared host.** Upload `index.html` by FTP. It is a static file and needs
nothing configured.

**No deployment at all.** Double-click `index.html`. It works from `file://`,
offline, on a machine with no internet connection.

The only external request the page makes is to Google Fonts for IBM Plex. If
that request fails, the page falls back to system fonts and everything else
works normally.

---

## Using it

**Guide me** asks two to five questions and recommends a test, with the reason
it chose that one. Recommendations are ranked: one leader, then alternatives
and companions worth running alongside. It now has entry points for theme
analysis and for questionnaire scoring as well as for comparisons and
relationships.

**All tests** lists all 54 tests in eight classes, with a table pairing every
common parametric test with its non-parametric counterparts. The index on the
left shows all eight classes at once; open one to see its tests. Search matches
names, purposes, tags and class names, so "Likert", "two coders", "trend" or
"non-parametric" all find something.

**Concepts** explains fourteen ideas students most often get wrong (p-values,
effect sizes, power, FWER versus FDR, Likert items versus Likert scales,
saturation, and so on), each with what to do in practice and links to the
relevant tests.

**Log** keeps every test you run, newest first, with its headline figures and
write-up line. Copy all of it at once, or download it as a Markdown file, to
assemble a results section. It is stored in this browser only; clearing the
browser's site data removes it.

Every parametric test page links to its non-parametric alternatives and vice
versa. Where the two use the same data layout, your pasted data carries over.

### Getting data in

Paste straight from Excel, Google Sheets or a CSV, or use **Open file** for a
CSV, TSV or text file. (Excel files can't be read directly; copy the cells and
paste them.) Tabs, commas, semicolons and spaces are detected automatically, as
are header rows and label columns. Three controls override the guess:
**Layout** (groups down columns or across rows), **First row** (header or data)
and **First column** (labels or data).

Under the box, a line reports what was actually read (`Read: 3 columns,
n = 10 / 10 / 10`). Check it before running. If the data doesn't fit the test,
for example three columns pasted into a two-group test, that line says so and
suggests what to use instead, rather than quietly analysing part of the data.

The reader copes with what spreadsheets actually produce. Decimal commas
(`3,5`), thousands separators (`1,234` or `1.234,5`), percentages, the Unicode
minus sign, quoted CSV fields and Windows line endings are all understood.
Blank cells and the usual missing-value markers (`NA`, `n/a`, `-`, `.`, `?`,
`#N/A`, `#DIV/0!` and similar) count as missing. For paired and repeated
designs, rows with a missing value are dropped as whole rows. Whenever the
reader interprets something, such as decimal commas, dropped rows or ignored
text, the `Read:` line and the results say so. CSV files saved by Excel on
Windows, which are not UTF-8, are decoded correctly. Workbooks, PDFs and images
are recognised and refused with a plain explanation, and values beyond
10^±50 are refused rather than silently overflowing.

### Getting results out

Every test returns headline statistics, effect sizes, assumption warnings in
amber, any relevant tables and charts, and a copyable write-up line formatted
for a paper. Each table has its own **Copy** button that pastes into Excel or
Word as a table. Very long tables show their first 500 rows on the page, and
**Copy** still takes every row. **Where to go next** suggests follow-ups based on what actually
happened, and those cards are clickable.

Deep links work: `index.html#kripp_alpha` opens Krippendorff's alpha directly,
and `#all`, `#concepts` and `#log` open those pages.

---

## What is included

**Agreement and reliability (7).** Cohen's kappa (unweighted, linear,
quadratic, with prevalence and bias indices and PABAK; weights follow the code
values, so an unused scale point still counts as a step), Fleiss' kappa,
Krippendorff's alpha (four levels, bootstrap CI, missing codes allowed), Gwet's
AC1/AC2, percent agreement, ICC (all six Shrout–Fleiss forms), Kendall's W.

**Qualitative themes (3).** Theme prevalence with Wilson intervals in batch.
Theme-by-theme comparison across stakeholder groups, with exact
Fisher–Freeman–Halton tests, a Benjamini–Hochberg, Holm or Bonferroni correction
across themes, and pairwise follow-ups that name the groups that differ.
Thematic saturation by the base size, run length and new-information threshold
of Guest, Namey and Chen (2020, *PLOS ONE*), reported in their "6+2" notation
with a sensitivity table across all twelve parameter choices.

**Frequencies and categories (8).** Chi-square tests of independence and
goodness of fit, Fisher's exact (including Freeman–Halton for R×C, exact where
the tables can be enumerated and seeded Monte Carlo with its standard error
beyond that), McNemar,
Cochran's Q, one- and two-proportion tests, odds ratios and risk measures.

**Screening and assumptions (5).** Descriptives, Shapiro–Wilk, Levene and
Brown–Forsythe, Bartlett, Grubbs.

**Parametric tests (9).** One-sample, independent (Welch by default) and paired
t-tests; one-way ANOVA with Tukey HSD or Games–Howell; repeated-measures ANOVA
with Greenhouse–Geisser and Huynh–Feldt corrections; two-way ANOVA (Type III
sums of squares); Pearson and
partial correlation; multiple regression with VIF and Durbin–Watson.

**Non-parametric tests (15).** One-sample Wilcoxon signed-rank (with a sign test
and Hodges–Lehmann estimate alongside), sign test, Mann–Whitney U (with a
Hodges–Lehmann shift), Brunner–Munzel (for groups with unequal spreads),
permutation test on means or medians (exact up to 200,000 splits, seeded Monte
Carlo beyond), Wilcoxon signed-rank (exact to n = 50), Kruskal–Wallis with Dunn
post-hoc, Jonckheere–Terpstra trend test (exact when untied), Friedman with
post-hoc comparisons, Page's L trend test (exact up to eight conditions),
aligned rank transform ANOVA for two crossed factors (Wobbrock et al., 2011),
Mood's median, two-sample Kolmogorov–Smirnov, Spearman, Kendall's tau-b.

**Scales and questionnaires (4).** Likert item analysis (diverging stacked bar
chart, medians and distributions, each item tested against the neutral point
with a correction across items), SUS scoring with the 68-point benchmark,
NASA-TLX (raw or weighted, 0–100 or 20-step scales, subscale profile), Cronbach's
alpha with item-rest correlations and alpha-if-dropped.

**Planning and corrections (3).** Six multiple-comparison methods side by side;
power and sample size for seven test types (the form shows only the fields for
what you are solving for); an effect-size converter between d, r, odds ratios
and η², or from a reported t, F, χ² or z.

---

## Verification

Every figure below comes from the code that ships in this file.

**Reference values (5,463 cases, all within tolerance).** Randomised data sets
for all 54 tests were run through the real parser and test code, with every
digit kept, and compared with established implementations: SciPy 1.18,
statsmodels 0.15, pingouin 0.7, scikit-posthocs, irrCAC (Gwet's own package),
the `krippendorff` package, brute-force enumeration for exact tests, and
40-digit arithmetic (mpmath) for exact tests on counts up to 10⁹. The default
tolerance is a relative error of 10⁻⁶, tighter where the method allows. Two
published benchmarks also reproduce: the `irr::kripp.alpha` documentation
matrix (.743 / .815 / .849 / .797 at the four levels) and Shrout & Fleiss
(1979) Table 2 for all six ICC forms.

**Hostile input (11,775 runs).** Every test was fed empty and one-row pastes,
junk text, HTML, emoji, byte-order marks, CRLF, semicolon and quoted CSV,
decimal commas, missing-value markers in random cells, typos, constant and
all-zero columns, transposed and very wide tables, codes named like JavaScript
built-ins (`constructor`, `__proto__`, `toString`), extreme magnitudes, and out
of range option values. Each run must either produce a clean result or a plain
explanation; none crashed, leaked an internal message, showed NaN or
"undefined", or took more than five seconds.

**Size (224 runs).** Up to 300,000 values per paste, 5,000 × 30 rating
matrices, 200 themes over a million participants, and 2 × 2 tables with
counts of 10⁸. Nothing failed or hung; the slowest case, 300,000 values in a
Mann–Whitney test, takes about three seconds.

**Invariance and range (335 checks).** For the tests whose statistics do not
depend on units, shifting the data by 10⁸ or rescaling it by 10⁻⁷ or 10⁶ leaves
the statistics and p-values unchanged (150 checks). Every example rescaled to
anywhere between 10⁻⁴⁹ and 10⁴⁹ still gives clean output (185 runs).

**Interface (233 runs in Chromium).** Every test was run through the built
page with each choice of each menu option, plus the guide, a pasted HTML payload (shown as
text, never executed), decimal-comma data, keyboard-only use, file import (CSV,
Windows-1252 CSV, a binary file, a 21 MB file), the log (copy, download,
two-step clear), search, browser history, a browser with storage and clipboard
blocked, and a 375 px phone screen (no sideways scrolling). No page errors.

**Structure.** All 62 paths through the guide end in a real test with a reason;
every example parses exactly as before and runs with every option.

## Changes in this version

Testing turned up the following, all now fixed.

- Several statistics disagreed with reference implementations: Welch's
  ANOVA, the Tukey and Games–Howell critical values, Clopper–Pearson intervals,
  the p-values of Cohen's and Fleiss' kappa (now the null-hypothesis variance),
  Gwet's AC1 and its standard error, ICC confidence intervals, Kendall's tau-b
  with ties, two-way ANOVA (now Type III), and the power calculations (now
  exact noncentral distributions). Kendall's tau and Kolmogorov–Smirnov gained
  exact small-sample p-values, Mann–Whitney's exact range was extended to 50
  per group, and Fisher's exact test now reports the conditional odds ratio
  with an exact interval.
- Weighted kappa and Gwet's AC2 weighted disagreements by category position
  rather than code value, which is wrong when a scale point is unused.
- Codes or factor levels named `constructor`, `toString`, `valueOf` or
  `__proto__` were dropped or miscounted.
- The aligned rank transform's tie handling depended on measurement units, so
  rescaling the data changed the p-value.
- Exact tests on large counts hung or exhausted memory: the one-proportion test
  at n = 10⁹, McNemar and the sign test, Fisher's exact test with counts near
  10⁸, and Freeman–Halton tables that are wide rather than large. Theme
  comparisons slowed down in proportion to group size.
- Krippendorff's alpha on continuous ratings built a table with one cell per
  pair of distinct values: two minutes, or a crash, for 20,000 units.
- Post-hoc tests for many groups were slow (Games–Howell with 100 groups took
  over a minute); post-hoc tables now stop at 20 groups, with a hint that the
  data may be transposed.
- Results with tens of thousands of rows froze the page for tens of seconds,
  and a scatter plot of more than about 125,000 points crashed the page.
- The parser could split a single column of decimal-comma numbers into two
  columns and misread space-grouped thousands; delimiters are now chosen by
  their consistency across rows.
- Extremely small values underflowed into wrong results, Excel's
  Windows-encoded CSV files lost their accented characters, and an over-long
  column list produced a misleading "exactly 99 groups" message.

## Things to know before you cite anything from it

Two-way ANOVA uses Type III sums of squares, the SPSS default; with unequal
cell sizes, say so in the write-up, because other software may default to Type
I or II. The aligned rank transform ANOVA is for between-subjects designs and
is exact only when cells are balanced; for repeated measures or unequal cells,
use ARTool in R.

Some limits keep the page responsive. Fisher's exact test on a large R×C table
and the theme comparison on large groups use seeded Monte Carlo, and say how
many tables were simulated. Pairwise post-hoc tables are not produced beyond
20 groups. Agreement coefficients refuse more than 1,000 distinct codes, which
almost always means measurements were pasted where codes were expected, and
ratio-level alpha stops at 4,000 distinct values.

Saturation results depend on how fine-grained the codebook is. Report the base
size, run length and threshold with the result.

More generally, this is checked, but it is one implementation. For numbers going
into a paper or a thesis, confirm the headline figures in R, JASP or SPSS. The
write-up lines are designed to make that comparison quick.

---

© 2025 Mayank Mayookh
