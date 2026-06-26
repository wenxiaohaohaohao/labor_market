# Labor Market Power and Product-Market Entry Reform

## Project Overview

**Working title**

Can Entry Liberalization Discipline Labor-Market Power? Evidence from Chinese Manufacturing

**中文题目**

进入放松能否约束企业劳动市场势力？来自中国制造业的证据

This project studies whether a product-market reform that lowers entry barriers can discipline firms' labor-market power. The design uses China's 2014 Business Registration Reform as an entry deregulation shock. The core empirical question is whether firms in industries more exposed to pre-reform entry barriers experienced larger declines in labor markdowns after the reform.

The project story is singular:

| Design | Shock | Current role |
|---|---|---|
| Main design | 2014 Business Registration Reform | Project core because it directly changes entry costs and fits the Chinese manufacturing setting |
| Method reference only | 2018 U.S. Section 301 tariff exposure materials | Used only to learn the exposure-design logic for constructing `X`, not as a project story |

The 2018 tariff materials are not part of the project's economic narrative. They are retained only as a reference for how to construct an exposure variable from pre-determined structure and a policy shock.

## Current Materials

| File | Role in the project |
|---|---|
| `references/2014商事制度改革_政策背景与识别合理性.pdf` | Main policy background and identification memo for the 2014 Business Registration Reform |
| `references/外部产品市场冲击与劳动市场势力_研究项目说明.pdf` | Method reference for exposure construction; not the current paper story |
| `references/PDBCLS.pdf` | Gouin-Bonenfant (2022), core theory reference on productivity dispersion, between-firm wage competition, and the labor share |
| `references/AERI_2024_0570_final (3).pdf` | Rubens, Wu, and Xu, method reference on separating wage markdowns from labor-augmenting productivity |
| `COLLABORATOR_PROJECT_STORY.md` | Collaborator-facing project story distilled from the screenshot discussion |
| `legacy_files/gpt_screenshots/*.png` | Local-only legacy GPT discussion screenshots; intentionally ignored and not pushed to the remote repository |

External bibliographic status and policy-source details have not yet been independently verified in this repository. Treat the current PDFs and screenshots as project materials to be checked during the literature and citation verification stage.

## Research Question

The main research question is:

> Can entry deregulation discipline firms' labor-market power?

The paper breaks this question into four testable sub-questions:

1. Did the 2014 Business Registration Reform generate economically meaningful changes in product-market structure, such as higher entry, lower concentration, lower markups, or lower price-cost margins?
2. Did firms in industries more exposed to pre-reform entry barriers experience lower labor markdowns after the reform?
3. Are the labor-market effects stronger in settings where entry deregulation should matter more, such as high-barrier industries, initially concentrated industries, or local labor markets with limited outside options?
4. Do aggregate labor-share effects reflect within-firm changes in wage setting, between-firm reallocation, or both?

## Core Economic Mechanism

The preferred mechanism is not "competition itself causes labor-market power" as a direct regression control. Competition variables such as entry, HHI, markup, CR4, and market shares are equilibrium outcomes. The paper should use an externally timed reform shock interacted with pre-reform exposure, then show that the reform changed product-market structure.

The causal chain is:

```text
Business Registration Reform
  -> entry cost decreases
  -> firm entry increases
  -> product-market competition increases
  -> product markups and rents decline
```

The labor-market channel is:

```text
firm entry increases
  -> worker outside options improve
  -> residual labor supply elasticity facing incumbent firms rises
  -> labor markdown declines
```

The reallocation channel is:

```text
entry deregulation and stronger competition
  -> inefficient firms exit or shrink
  -> high-productivity firms expand
  -> aggregate labor share may move differently from within-firm markdowns
```

This last channel is important because a reform can lower markdowns inside firms while aggregate labor shares still depend on reallocation across firms. Gouin-Bonenfant (2022) is the key reference for this logic.

## Treatment Construction

The main explanatory variable should be a policy-shock exposure, not product-market competition itself:

```text
ReformExposure_{j,t} = Post2014_t x PreReformEntryBarrier_j
```

where `j` is an industry or a finer industry cell, and `Post2014_t` indicates years after the 2014 reform. The preferred pre-reform exposure is a measure of how costly entry was before the reform.

### Preferred Exposure

The preferred measure is pre-reform paid-in registered-capital burden among entrants:

```text
CapitalBarrier_j =
  median(Paid-in Registered Capital of Entrants_{j,2010-2013})
  / median(Assets or Sales of Entrants_{j,2010-2013})
```

Economic interpretation: industries where entrants needed more paid-in registered capital before the reform should be more affected by the switch from paid-in registration to subscribed-capital registration.

### Alternative Exposures

| Exposure | Construction | Use |
|---|---|---|
| Low entry rate | `- EntryRate_{j,2010-2013}` | Robustness; less clean because low entry can reflect demand or technology |
| Incumbent dominance | `IncumbentShare_{j,2010-2013} / YoungFirmShare_{j,2010-2013}` | Robustness for historically restricted entry |
| License dependence | share of firms or subindustries requiring pre-entry approval | Strong institutional interpretation if data can be built |
| Low-entry high-profit industries | `HighProfitMargin_{j,pre} x LowEntryRate_{j,pre}` | Robustness only because it is more exposed to endogeneity concerns |

If city-industry data are available, a stronger exposure can be constructed as:

```text
ReformExposure_{c,j,t}
  = InitialIndustryShare_{c,j,pre} x PreReformEntryBarrier_j x Post2014_t
```

This version follows the spirit of shift-share exposure designs and allows richer fixed effects.

## Outcomes

### Main Outcome

The main outcome is firm-level labor markdown:

```text
LaborMarkdown_{i,t} = (MRPL_{i,t} - w_{i,t}) / MRPL_{i,t}
```

or an equivalent structural markdown measure derived from a production model and labor-supply structure.

This variable should not be mechanically equated with low labor share. Rubens, Wu, and Xu warn that production approaches relying only on input expenditure shares do not separately identify wage markdowns from labor-augmenting productivity. The project therefore needs a clear markdown construction strategy before making strong monopsony claims.

### Secondary Outcomes

| Category | Variables | Purpose |
|---|---|---|
| Wage outcomes | average wage, wage bill per worker, wage growth | Test wage adjustment |
| Pass-through | wage-productivity pass-through, rent sharing | Test whether productivity or rents are passed to workers |
| Distribution | labor share, compensation share | Study income distribution effects |
| Product market | entry rate, exit rate, HHI, CR4, markup, price-cost margin | Validate the product-market reform channel |
| Reallocation | top-firm value-added share, productivity dispersion, between-firm labor-share decomposition | Separate within-firm effects from reallocation |

## Baseline Empirical Design

The cleanest baseline is a reduced-form effect of reform exposure on labor markdown:

```text
Markdown_{i,c,j,t}
  = beta ReformExposure_{j,t}
  + firm FE
  + year FE
  + city FE
  + controls_{i,t}
  + error_{i,c,j,t}
```

The expected sign under the discipline hypothesis is:

```text
beta < 0
```

That is, labor markdowns should decline more after 2014 in industries where pre-reform entry barriers were higher.

If the treatment is available at the city-industry level, the preferred specification can be stronger:

```text
Markdown_{i,c,j,t}
  = beta ReformExposure_{c,j,t}
  + firm FE
  + city x year FE
  + industry x year FE
  + controls_{i,t}
  + error_{i,c,j,t}
```

The exact fixed-effect structure must match the level of treatment variation. A fixed effect that fully absorbs the treatment should not be included.

## Reform Validation

Before interpreting labor-market effects, the paper must show that the reform changed product-market structure:

```text
Y_{c,j,t}
  = alpha ReformExposure_{c,j,t}
  + fixed effects
  + error_{c,j,t}
```

where `Y` includes:

```text
EntryRate, ExitRate, HHI, CR4, Markup, PriceCostMargin
```

The correct language is:

> The reform generated economically meaningful changes in product-market structure.

The paper should not claim that every mechanism variable is a separately identified causal mediator. These variables are post-reform equilibrium outcomes, so they belong in reform validation, mechanism evidence, and heterogeneity analysis, not as ordinary controls in the main regression.

## Dynamic Event Study

The event-study design should test whether high- and low-exposure industries were on similar pre-trends before 2014:

```text
Y_{i,c,j,t}
  = sum_{k != -1} beta_k PreReformEntryBarrier_j x 1[t - 2014 = k]
  + fixed effects
  + controls
  + error_{i,c,j,t}
```

Key checks:

1. Coefficients for 2007-2013 should not show systematic pre-trends.
2. 2014 may be treated as a transition year because the reform began in March 2014.
3. The baseline window should likely be 2007-2019 if 2020 is contaminated by COVID-19. The 2020 outcome can be used as a robustness or medium-run persistence check.

## Heterogeneity and Mechanism Tests

Top-journal positioning is stronger if the paper shows where the effect is concentrated.

Recommended heterogeneity tests:

| Heterogeneity dimension | Prediction |
|---|---|
| High initial entry barriers | Stronger decline in labor markdown after reform |
| High initial product-market concentration | Stronger product-market restructuring |
| Low worker mobility or weak outside options | Smaller markdown decline or weaker pass-through |
| High initial monopsony or employer concentration | Stronger potential discipline effect if new entrants improve outside options |
| Industries with larger post-reform entry response | Stronger consistency with product-market competition channel |

Suggested regression:

```text
Markdown_{i,c,j,t}
  = beta ReformExposure_{j,t}
  + gamma ReformExposure_{j,t} x InitialCondition_{j,pre}
  + fixed effects
  + controls
  + error_{i,c,j,t}
```

This is safer than placing post-reform competition variables directly on the right-hand side of the main regression.

## Data Requirements

The project requires the following data modules:

| Module | Required variables | Purpose |
|---|---|---|
| Firm financial and production data | sales, value added, inputs, capital, materials, wage bill, employment, profits | Estimate production, markdowns, markups, labor share, and firm outcomes |
| Business registration data | registered capital, paid-in capital, entry year, firm age, ownership, industry, location | Construct pre-reform entry barriers and entry responses |
| Industry or city-industry panel | entry rate, exit rate, HHI, CR4, market shares | Validate product-market restructuring |
| Labor-market data | employment, wage bill, worker mobility, employer concentration, unemployment or local labor demand | Measure outside options and local labor-market conditions |
| Policy and institutional data | license dependence, pre-entry approval requirements, reform timing | Construct alternative entry-barrier measures |

The 2018 tariff-war memo remains useful only as an exposure-design reference. The current paper does not require China Customs tariff-war variables.

## Contribution

The project can make four contributions.

1. It moves the entry deregulation literature beyond product-market entry, markups, and firm performance by asking whether entry reforms also change labor-market power.
2. It connects product-market power and labor-market power in one empirical design, while avoiding the mistake of treating product-market competition as an exogenous right-hand-side variable.
3. It studies whether labor-market discipline comes from better outside options, stronger wage-productivity pass-through, or reallocation across firms.
4. It offers a China manufacturing setting with a clear institutional reform in the middle of a long firm panel.

The best paper framing is:

> The paper first estimates the reduced-form effect of entry-reform exposure on labor markdowns. It then shows that the effect is concentrated in industries where the reform induced stronger product-market restructuring, measured by entry, exit, concentration, markup, and price-cost-margin responses. This pattern is consistent with a product-market competition channel.

## Main Identification Risks

| Risk | Why it matters | Planned response |
|---|---|---|
| Pre-reform entry barriers are not random | High-barrier industries may already have different wage or productivity trends | Event-study pre-trend tests, alternative exposure measures, industry trends, placebo reform years |
| Post-treatment controls | Entry, HHI, markups, and market shares are equilibrium outcomes | Use them as outcomes, validation tests, or heterogeneity variables, not baseline controls |
| Firm observation changes | Registration reform may change which firms appear in the data | Separate incumbent-firm and entrant-firm analyses; use balanced or continuing-firm samples as robustness |
| Concurrent policies | Other policies around 2014 may affect firm entry, wages, or competition | Add city-year fixed effects where possible; exclude sensitive sectors; control for known policy exposures |
| Markdown measurement | Low labor share is not identical to monopsony | Use structural markdown measures; report wage, wage-productivity pass-through, and labor-share alternatives |
| COVID-19 contamination | 2020 may mix reform dynamics with pandemic shocks | Use 2007-2019 as baseline; treat 2020 separately |
| Reallocation | Aggregate labor share can move through between-firm composition | Decompose within-firm and between-firm components |

## Exposure-Design Lesson From the 2018 Tariff Materials

The earlier tariff memo is useful because it shows how to construct a policy exposure from pre-determined structure and a policy shock:

```text
USTariffExposure_{g,t}
  = sum_k [X^{US}_{g,k,2016} / X_{g,2016}] x USTariff_{k,t}
```

The current paper borrows the construction logic, not the tariff story. The corresponding entry-reform exposure is:

```text
EntryReformExposure_{j,t}
  = PreReformEntryBarrier_j x Post2014_t
```

or, if city-industry variation is available:

```text
EntryReformExposure_{c,j,t}
  = InitialIndustryShare_{c,j,pre} x PreReformEntryBarrier_j x Post2014_t
```

Thus, the Section 301 materials are a methodological reference for building `X`; the paper's economic story remains entry liberalization and labor-market power in Chinese manufacturing.

## Recommended Next Steps

1. Confirm the available firm panel years and whether 2007-2020 or 2010-2020 is the feasible baseline window.
2. Build the pre-reform `CapitalBarrier_j` measure from entrant registered-capital data.
3. Construct alternative `EntryBarrier` measures for robustness.
4. Estimate first-stage reform effects on entry, exit, concentration, markups, and price-cost margins.
5. Finalize the labor markdown measure and document its assumptions.
6. Run the baseline markdown regression and event-study pre-trend checks.
7. Add heterogeneity by initial concentration, local labor-market outside options, and initial entry barriers.
8. Decompose aggregate labor-share changes into within-firm and between-firm components.
9. Verify all literature references, policy sources, and citation details before drafting the introduction and literature review.
