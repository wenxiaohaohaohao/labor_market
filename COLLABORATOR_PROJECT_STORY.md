# 进入放松、产品市场竞争与企业劳动市场势力

合作者讨论稿

## 一句话概括

本文研究一个直接降低企业进入门槛的制度改革，是否能够通过增强产品市场竞争和增加劳动者外部雇主选择，约束企业在劳动市场上的工资设定权。核心问题不是简单问“竞争是否提高工资”，而是问：当企业进入制度被放松以后，企业的 labor markdown 是否下降，工资和边际产出之间的缺口是否收窄。

当前最稳妥的英文题目是：

```text
Can Entry Liberalization Discipline Labor-Market Power? Evidence from Chinese Manufacturing
```

更具体的版本是：

```text
Can Entry Deregulation Discipline Labor-Market Power? Evidence from China's Business Registration Reform
```

## 项目的直觉

很多关于产品市场竞争的论文关注企业进入、价格、markup、利润率和生产率。很多关于劳动市场势力的论文关注企业是否支付低于劳动边际收益产品的工资。这个项目的连接点是：如果产品市场改革降低了进入门槛，它不仅会改变产品市场的竞争结构，也会改变劳动者面对的潜在雇主集合。

2014 年中国商事制度改革适合讲这个故事。改革的核心不是劳动合同、最低工资或社保政策，而是企业设立制度：注册资本制度、工商登记便利化、前置审批清理、证照办理简化等。也就是说，它首先作用于企业进入和产品市场结构，而不是直接作用于工资规则。

这使得本文可以提出一个清楚的经济学问题：

> 一个产品市场侧的进入放松改革，能否间接约束企业在劳动市场上的 monopsony power？

## 为什么不直接把产品市场竞争当作 X

截图讨论中最重要的结论是：主解释变量不能设成 `Product Market Competition`、`Markup`、`HHI`、`EntryRate` 或市场份额本身。

原因很简单。这些变量都是改革后的均衡结果。它们同时受需求、生产率、出口、地方政策、行业景气、企业进入退出和企业策略影响。如果直接把它们放在主回归右边解释 labor markdown，审稿人会质疑它们是 endogenous equilibrium outcomes，甚至是 post-treatment controls。

更稳妥的顶刊写法是：

1. 先构造一个政策冲击暴露度：`Post2014 x PreReformEntryBarrier`。
2. 用这个冲击暴露度估计 labor markdown 的 reduced-form effect。
3. 再证明同一个冲击确实改变了产品市场结构，例如 entry、exit、HHI、CR4、markup 和 price-cost margin。
4. 最后展示 labor-market effect 集中出现在产品市场结构调整更强、改革前进入壁垒更高或初始竞争较弱的行业。

因此，本文的机制语言应写成：

> The pattern is consistent with a product-market competition channel.

不应写成：

> Product-market competition is the fully identified causal mediator.

## 核心因果故事

项目的主线可以写成三步。

第一步，2014 年商事制度改革降低企业进入成本：

```text
Business Registration Reform
  -> Entry Cost decreases
  -> Firm Entry increases
```

第二步，更多潜在进入者改变产品市场结构：

```text
Firm Entry increases
  -> Product-Market Competition increases
  -> Markup, HHI, CR4, and Price-Cost Margin decline
```

第三步，企业进入也改变劳动市场：

```text
Firm Entry increases
  -> Employer Options increase
  -> Residual Labor Supply Elasticity rises
  -> Labor Markdown declines
```

经济含义是：当劳动者有更多潜在雇主时，原有企业面对的残余劳动供给曲线更有弹性，企业压低工资相对边际收益产品的空间下降。因此，一个看似产品市场侧的改革，可能通过雇主竞争和外部选择影响劳动市场势力。

## 主解释变量

主解释变量应写成：

```text
ReformExposure_{j,t} = Post2014_t x PreReformEntryBarrier_j
```

其中：

- `j` 是行业，若数据允许也可以是城市-行业单元。
- `Post2014_t` 表示 2014 年改革后的时期。
- `PreReformEntryBarrier_j` 表示改革前行业进入壁垒。

这个设计的好处是：全国性改革本身不能只用一个 post dummy 识别，因为它会和宏观时间趋势混在一起。真正有识别力的是不同改革前进入壁垒行业在改革后的差异化暴露。

## 首选 exposure：改革前注册资本负担

截图讨论中最推荐的 exposure 是改革前进入者的注册资本负担：

```text
CapitalBarrier_j =
  Median Paid-in Registered Capital of Entrants_{j,2010-2013}
  / Median Assets or Sales of Entrants_{j,2010-2013}
```

直觉是：2014 年注册资本登记制度改革把实缴登记制改为认缴登记制。改革前进入一个行业所需的前置资本承诺越高，该行业受到注册资本制度放松的冲击越大。

这比使用低进入率更干净。低进入率可能来自制度壁垒，也可能来自需求下降、技术门槛高、资本密集度高或行业生命周期。注册资本负担更接近改革本身的制度内容。

备选 exposure 可以包括：

| 变量 | 解释 | 使用位置 |
|---|---|---|
| `Paid-in Registered Capital / Employment` | 改革前单位就业对应的注册资本负担 | 稳健性 |
| `- EntryRate_{j,pre}` | 改革前进入率越低，进入限制可能越强 | 稳健性，不宜作为唯一主指标 |
| `IncumbentShare / YoungFirmShare` | 老企业占比高、年轻企业占比低反映历史进入受限 | 辅助指标 |
| `LicenseDependence` | 行业对前置许可或先证后照的依赖程度 | 若能整理行政许可数据，可作为强制度指标 |

若能做到城市-行业层面，可以进一步构造：

```text
ReformExposure_{c,j,t}
  = InitialIndustryShare_{c,j,pre}
  x PreReformEntryBarrier_j
  x Post2014_t
```

这个版本接近 Autor-Dorn-Hanson 或 Topalova 式的 exposure design：用初始产业结构决定一个地区受到全国性冲击的强度。

## 主结果变量

主结果是企业层面的 labor markdown：

```text
LaborMarkdown_{i,j,c,t}
```

它度量企业支付工资低于劳动边际收益产品的程度。若使用更结构化的定义，可以写成：

```text
LaborMarkdown = (MRPL - wage) / MRPL
```

但这里必须谨慎。labor markdown 不能简单等同于低 labor share，也不能只靠投入份额机械推出。后续实证需要明确 production function、labor supply、工资、就业和边际产出的估计方法。

可以作为补充结果的变量包括：

- wage markdown
- wage / marginal revenue product gap
- wage growth
- wage-productivity pass-through
- rent sharing
- labor share
- employment adjustment

## 基准回归

企业层面主回归可以写成：

```text
Markdown_{i,j,c,t}
  = beta (Post2014_t x CapitalBarrier_{j,pre})
  + firm FE
  + year FE
  + city FE
  + controls_{i,t}
  + error_{i,j,c,t}
```

其中 `controls_{i,t}` 可以包括企业年龄、规模、资本密集度、出口状态、所有制等企业特征。

核心预测是：

```text
beta < 0
```

含义是：改革前注册资本负担越高的行业，2014 年改革后进入门槛下降越明显，企业 labor markdown 下降越多。

如果 treatment 构造到城市-行业层面，回归可以吸收更强的固定效应：

```text
Markdown_{i,j,c,t}
  = beta ReformExposure_{c,j,t}
  + firm FE
  + city x year FE
  + industry x year FE
  + controls_{i,t}
  + error_{i,j,c,t}
```

最终固定效应必须和 treatment 变异层级匹配，不能把主解释变量完全吸收掉。

## Reform validation

在解释 labor markdown 之前，必须先证明改革确实改变了产品市场结构。这一步不是 mediation，而是 first-stage 或 reform validation。

可以估计：

```text
Y_{j,t}
  = alpha ReformExposure_{j,t}
  + fixed effects
  + error_{j,t}
```

其中 `Y` 包括：

- EntryRate
- ExitRate
- HHI
- CR4
- Markup
- PriceCostMargin

建议写法是：

> The reform generated economically meaningful changes in product-market structure.

这个表述比“产品市场竞争是唯一机制”更稳。它说明改革确实改变了产品市场环境，同时避免对内生均衡变量做过强的因果中介声明。

## 机制与异质性

直接把 `Competition_{j,t}` 放进主回归右边不稳。更稳的做法是检验改革效应是否集中在理论上更应该发生作用的地方。

可以写成：

```text
Markdown_{i,j,t}
  = beta ReformExposure_{j,t}
  + gamma ReformExposure_{j,t} x InitialCompetition_{j,0}
  + FE
  + error_{i,j,t}
```

或者：

```text
Markdown_{i,j,t}
  = beta ReformExposure_{j,t}
  + gamma ReformExposure_{j,t} x InitialEntryBarrier_{j,0}
  + FE
  + error_{i,j,t}
```

应重点看以下异质性：

| 维度 | 预期 |
|---|---|
| 改革前进入壁垒高 | labor markdown 下降更明显 |
| 初始产品市场集中度高 | 产品市场结构调整更强 |
| 改革后进入反应大 | markdown 下降更符合竞争渠道 |
| 劳动者流动性弱 | markdown 下降可能较弱，或改革效果取决于是否真正增加 outside options |
| 初始雇主集中度高 | 若新进入改善雇主选择，劳动市场 discipline effect 更强 |

## 动态事件研究

由于 2014 年位于 2007-2020 数据窗口中部，项目可以做动态 event study。

```text
Y_{i,j,c,t}
  = sum_{k != -1} beta_k PreReformEntryBarrier_j x 1[t - 2014 = k]
  + fixed effects
  + controls
  + error_{i,j,c,t}
```

这一步要回答两个问题：

1. 2007-2013 年高进入壁垒行业和低进入壁垒行业是否存在系统性 pre-trend。
2. 2015 年以后 labor markdown、工资、进入率和产品市场结构是否出现符合机制的动态变化。

2014 年可以作为改革启动或过渡年。若担心 2020 年疫情影响，基准样本应使用 2007-2019，2020 年单独作为稳健性或中期持续性检验。

## 论文贡献

这篇文章的贡献可以写成四点。

第一，它把 entry deregulation 的结果从企业进入、产品市场竞争和 markup 推进到劳动市场势力。现有文献通常问改革是否促进进入或提高效率，本文进一步问它是否改变企业对工人的工资设定权。

第二，它把 product-market power 和 labor-market power 放在一个实证框架中。产品市场改革可能改变企业面对的产品需求，也可能改变劳动者面对的雇主选择，二者共同影响工资和劳动收入分配。

第三，它提供一个清楚的中国制造业制度背景。2014 年商事制度改革是全国性改革，但改革前不同行业的进入壁垒不同，因此可以构造差异化 exposure。

第四，它强调顶刊写作中的识别纪律：主 X 是政策冲击暴露度，而不是改革后竞争结果本身。产品市场竞争是机制证据，不是主识别变量。

## 与 2018 贸易战设计的关系

截图中也出现了 2018 年美国 Section 301 对华加征关税的 shift-share 暴露度设计。这个设计可以写成：

```text
USTariffExposure_{g,t}
  = sum_k [X^{US}_{g,k,2016} / X_{g,2016}]
  x USTariff_{k,t}
```

但它和 2014 商事制度改革不是同一个故事。2018 贸易战是外部市场准入恶化和出口租金收缩冲击；2014 商事制度改革是进入成本下降和市场准入放松冲击。

两者都能研究 product-market shocks 和 labor-market power，但方向不同：

- 2014 改革更适合问：进入放松能否 discipline labor-market power？
- 2018 贸易战更适合问：外部出口租金压缩会 discipline 还是 amplify labor-market power？

当前项目建议以 2014 改革为主线。2018 贸易战可以保留为另一篇文章、附录讨论，或未来扩展。

## 给合作者的关键决策点

后续需要尽快确认以下事项。

1. 数据窗口：最终使用 2007-2020、2010-2020，还是 2007-2019 作为基准。
2. 企业数据来源：是否能拿到企业注册资本、paid-in capital、assets、sales、employment、wage bill、industry、city 和 entry year。
3. entrants 定义：使用新注册企业、首次出现在数据中的企业，还是企业年龄低于某阈值的企业。
4. `CapitalBarrier` 分母：使用 assets 还是 sales，需要按数据质量决定。
5. labor markdown 估计方法：需要明确 production function、MRPL、wage、labor supply elasticity 或替代测度。
6. 固定效应结构：根据 treatment 层级决定是否使用 firm FE、city-year FE、industry-year FE。
7. 政策来源：2014 改革文件、国务院材料、World Bank 报告和前置审批清理证据需要正式核验。

## 合作者版摘要

本文拟利用 2014 年中国商事制度改革作为进入放松冲击，研究产品市场改革是否能够约束企业劳动市场势力。改革降低了企业设立中的注册资本、登记和审批成本；改革前进入资本负担更高的行业，理论上受到更强的进入放松冲击。我们将主解释变量构造为改革后时期与改革前进入壁垒的交互项，估计其对企业 labor markdown 的 reduced-form effect。

核心预测是，进入壁垒放松更强的行业在改革后 labor markdown 下降更多。机制上，改革应首先带来产品市场结构变化，例如进入率上升、集中度下降、markup 或 price-cost margin 下降；同时，新增企业提高劳动者外部雇主选择，使企业面对的残余劳动供给更有弹性，从而降低工资相对劳动边际收益产品的缺口。

本文的识别纪律是：不把产品市场竞争、markup、HHI 或进入率直接当作主解释变量，因为它们是改革后的均衡结果。论文先估计政策冲击暴露度对 labor markdown 的主效应，再用产品市场结构变量做 reform validation 和机制异质性分析。这种写法更接近 applied micro 和 top-field journal 的标准：主效应直接，机制分层证明，避免把内生机制变量当成外生冲击。
