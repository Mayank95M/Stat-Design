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

### Getting results out

Every test returns headline statistics, effect sizes, assumption warnings in
amber, any relevant tables and charts, and a copyable write-up line formatted
for a paper. Each table has its own **Copy** button that pastes into Excel or
Word as a table. **Where to go next** suggests follow-ups based on what actually
happened, and those cards are clickable.

Deep links work: `index.html#kripp_alpha` opens Krippendorff's alpha directly,
and `#all`, `#concepts` and `#log` open those pages.

---

## What is included

**Agreement and reliability (7).** Cohen's kappa (unweighted, linear,
quadratic, with prevalence and bias indices and PABAK), Fleiss' kappa,
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
goodness of fit, Fisher's exact (including Freeman–Halton for R×C), McNemar,
Cochran's Q, one- and two-proportion tests, odds ratios and risk measures.

**Screening and assumptions (5).** Descriptives, Shapiro–Wilk, Levene and
Brown–Forsythe, Bartlett, Grubbs.

**Parametric tests (9).** One-sample, independent (Welch by default) and paired
t-tests; one-way ANOVA with Tukey HSD or Games–Howell; repeated-measures ANOVA
with Greenhouse–Geisser and Huynh–Feldt corrections; two-way ANOVA; Pearson and
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

Four harnesses were run against the code that ships in this file.

**Original numerical checks (62).** Krippendorff's alpha reproduces the
documented `irr::kripp.alpha` test matrix at all four levels (.743 / .815 /
.849 / .797). ICC reproduces Shrout & Fleiss (1979) Table 2. Power matches
G\*Power. Exact tests match R for Mann–Whitney, Wilcoxon, Fisher, McNemar and
the binomial. `p.adjust` matches R for Holm and BH. The studentized range
distribution for Tukey and Games–Howell agrees with published critical values to
5 × 10⁻⁴.

**New-test numerical checks (98).** The one-sample Wilcoxon, sign test, Page's
L, Brunner–Munzel and one-sided permutation test match SciPy 1.17
(`wilcoxon`, `binomtest`, `page_trend_test`, `brunnermunzel`,
`permutation_test`) in exact and asymptotic modes. Two-sided permutation
p-values match brute-force enumeration, and the Monte Carlo branch lands within
its stated error of the exact answer. Jonckheere–Terpstra exact p-values match
enumeration of every possible assignment, and its tie-corrected variance matches
the enumerated variance exactly. The aligned rank transform matches an
independent implementation using statsmodels, and passes the alignment check
ARTool reports. Freeman–Halton p-values match SciPy's `fisher_exact` for 2×2
tables and brute-force enumeration for 2×k. Saturation matches an independent
implementation of the Guest et al. procedure for all twelve parameter
combinations. The largest relative deviation across the exact-tolerance checks
is 3 × 10⁻⁸.

**Structure.** All 54 tests run their examples, every option value on every
test was exercised, all 62 paths through the decision guide resolve to a real
test with a justification and exactly one leading recommendation, and malformed
input produces a readable explanation rather than a crash.

**Interface (60 checks).** Driven end to end through the built page: the eight
classes, the pairing table, counterpart links carrying data across, every test
run from its example, the Likert chart, saturation curve and TLX profile, file
import, the log (persist, replace on re-run, copy, download, two-step clear),
the concepts page, conditional fields, and labels on every control. Layouts were
also checked in headless Chromium at desktop and phone widths.

## Things to know before you cite anything from it

Two-way ANOVA uses Type I sums of squares, so it is exact only for balanced
designs. The aligned rank transform ANOVA is for between-subjects designs and
is exact only when cells are balanced; for repeated measures or unequal cells,
use ARTool in R.

Saturation results depend on how fine-grained the codebook is. Report the base
size, run length and threshold with the result.

More generally, this is checked, but it is one implementation. For numbers going
into a paper or a thesis, confirm the headline figures in R, JASP or SPSS. The
write-up lines are designed to make that comparison quick.

---

© 2025 Mayank Mayookh
