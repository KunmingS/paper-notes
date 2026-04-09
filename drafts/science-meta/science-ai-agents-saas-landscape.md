---
source: user notes (collected from web)
source_url: ~
fetched: 2026-04-08
---

# Science AI agents and SaaS landscape — products and business models

Notes I collected on the commercial science-AI landscape: which agent-shaped SaaS products exist, and how they're monetized.

---

## Agent-shaped SaaS in scientific research

科研领域已经有不少这类 AI agent 形态的 SaaS 产品了，而且发展很快。几个代表性的：

### 文献与综述方向

**Elicit** 是目前科研领域最有代表性的 AI 产品，能搜索 1.38 亿+ 篇论文，支持系统性综述、数据提取、研究报告生成等多步工作流，底层用的就是 Claude Opus。Elicit 它不只是聊天，而是提供结构化表格和自动化流程，已经有制药公司用它做临床试验文献分析。

### 自主科研 agent 方向

**Edison Scientific** 开发的 **Kosmos** 是一个"AI 科学家"，能并行执行数百个研究任务，把几个月的工作压缩到一天。他们的技术报告描述了 Kosmos 独立完成的七项发现，其中四项是全新的文献贡献，包括识别出一种新的神经元衰老机制。 (Genengnews)

**Lila Sciences** 则在做"科学超级智能"，通过自主实验室来规模化科学方法。 (Genengnews)

### 药物研发方向

这个赛道更热——**Formation Bio**、**Recursion**、**Insilico Medicine** 等公司都在用 AI agent 做药物靶点发现、分子设计、临床数据分析。

不过目前大多数科研 agent 产品还是聚焦在文献分析、数据提取、假设生成这些"干"的环节。真正闭环到"设计实验→执行实验→分析结果"的全自动科研，还处于非常早期的阶段。

---

## Business models for science AI SaaS

科研 AI SaaS 目前的盈利模式其实比较清晰，主要有几种：

### 1. 分层订阅制（最主流）

以 Elicit 为例：
- 免费版提供 5,000 次一次性积分
- Plus 版 $12/月，适合研究生和独立研究者
- Pro 版 $49/月，支持批量数据提取和高级工作流
- Team 版 $79/人/月，面向团队协作

(CostBench)

核心逻辑是：免费版让你尝到甜头，但功能受限（比如每月只能生成 2 份报告），研究者一旦用上瘾，自然会升级。团队用户的生命周期价值是个人用户的 3-4 倍。 (Miracuves)

### 2. 企业/机构许可

这是真正的利润来源。卖给制药公司、咨询公司、大型研究机构，按年签合同，价格远高于个人订阅。比如 Formation Bio 这样的药企用 Elicit 做临床试验分析，付的是企业级价格。

### 3. API 访问

Elicit 提供 API，让其他产品可以调用它的论文搜索和报告生成能力。这相当于 B2B2C，把自己变成科研基础设施的一层。

### 4. 成本结构

AI 计算和云托管大概占收入的 30%，研发占 20%，获客和营销占 15%。 (Miracuves) 因为底层模型调用（比如 Claude Opus）本身就贵，所以毛利率远没有传统 SaaS 那么高。

### 当前挑战

坦率说，目前的挑战是：科研用户群体相对小众，个人付费意愿不算强（很多研究者习惯用免费工具），所以大部分科研 AI SaaS 的真正增长引擎是企业端——制药、生物科技、政策咨询这些愿意为效率买单的行业客户。纯学术端很难撑起大规模商业化。
