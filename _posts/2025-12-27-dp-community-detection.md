---
title: "[Paper Review] Differentially Private Community Detection for Stochastic Block Models"
date: 2025-12-28 01:00:00 +0900
categories: [paper-review, differential-privacy]
tags: [DP, graph, community-detection, SBM]
math: true
---

## Paper Information

- **Title**: Differentially Private Community Detection for Stochastic Block Models
- **Authors**: Mohamed Seif, Dung Nguyen, Anil Vullikanti, Ravi Tandon
- **Venue**: ICML 2022
- **Link**: [arXiv:2202.00636](https://arxiv.org/abs/2202.00636)

---

## 1. Problem Statement

- Graph is generated from a stochastic block model (SBM).
  - $ n $ vertices, $ r $ communities, $ p $ and $ q $ the intra-community and inter-community connection probabilities.
- Community detection problem in edge DP.

---

## 2. Motivation and Background

- Consider the dense regime with $ p = a \log ( n ) / n $ and $ q = b \log ( n ) / n $ for some constants $ a > b > 0 $.
- **Exact recovery**: An estimator satisfies exact recovery if the probability of error is in $ o( 1 ) $.
  - It is known that exact recovery is possible if and only if $ \sqrt{a} - \sqrt{b} > \sqrt{r} $.
- Prior results on exact recovery without privacy
  - The optimal maximum likelihood (ML) estimator is computationally intractable.
  - SDP relaxation of the ML estimator can also achieve the same recovery threshold.

---

## 3. Main Contributions

- Differentially private algorithms for community detection in SBM.
  - Stability based mechanisms.
  - Sampling based mechanisms.
  - Randomized Response (RR) based mechanism.

---

## 4. Technical Overview

- **Input**: $ G ( V, E ) \in \mathcal{G} $.
- **Output**: A labelling vector $ \hat{\sigma} \in \mathcal{L} $.

### 4.1 Stability-based Mechanisms

- **Stability**: minimum number of edge modifications changes the output of the estimator.
- First, privately compute the stability of this estimator.
- Release the non-private estimate $ d_{\hat{\sigma}} ( G ) $ only if the graph $ G $ is stable enough.
<br>

- Algorithm
  - $ d_{\hat{\sigma}} ( G ) \leftarrow $ stability of $ \hat{\sigma} $ with respect to graph $ G $.
  - $ \tilde{d} \leftarrow d_{\hat{\sigma}} ( G ) + Lap ( 1 / \epsilon ) $
  - **if** $ \tilde{d} > {\log{1 / \delta} \over \epsilon} $ **then** output $ d_{\hat{\sigma}} ( G ) $, **else** output $ \bot $.
<br>

- Privacy Analysis
  - Satisfies $ ( \varepsilon, \delta ) $-edge DP for any community detection algorithm $ \hat{\sigma} $.
<br>

- Error / Utility Analysis
  - The algorithm satisfies exact recovery if
    - $ r = 2 $ and $ \sqrt{a} - \sqrt{b} > \sqrt{2} \times \sqrt{1 + {t + 1 \over 2 \epsilon}}$.
    - $ r > 2 $ and $ \sqrt{a} - \sqrt{b} > \sqrt{r} \times \sqrt{1 + {t + 1 \over \epsilon} \times ( 1 + \log{\sqrt{a \over b}} )}$.
    - $ r \geq 2 $ and $ \sqrt{a} - \sqrt{b} > \sqrt{r} \times \sqrt{2 + {t + 1 \over \epsilon} \times ( 1 + \log{\sqrt{a \over b}} )}$.
  - for any $ \epsilon > 0 $ and $ \delta = n^{-t}, t > 0 $.
<br>

- Time Complexity
  - Using ML estimator : exponential time.
  - Using SDP relaxation : quasi-polynomial time.

### 4.2 Sampling based mechanisms

- Both of the mechanisms can achieve pure edge-DP, but sampling step in these mechanisms takes exponential time.

#### 4.2.1 Bayseian Sampling Mechanism

- Algorithm
  - For every $ \sigma \in \mathcal{L} $, calculate $ Pr (\sigma | G) $.
  - Sample and output a labeling $ \hat{\sigma} \in \mathcal{L} $ with probability $ Pr (\hat{\sigma} | G) $.
<br>

- Privacy Analysis
  - Satisfies $ \varepsilon $-edge DP for $ \forall \epsilon \geq \epsilon_{0} = \log{({a \over b})} $.
<br>

- Error / Utility Analysis
  - The algorithm satisfies exact recovery if $ r = 2 $ and $ \sqrt{a} - \sqrt{b} > \max[\sqrt{2}, {2 \over ( \sqrt{2} - 1 )( 1 - e^{-\epsilon_{0}} )}]$.

#### 4.2.2 Exponential Mechanism
- Does not require the knowledge of $ ( a, b )$.
- Define $ score ( \sigma ) = E_{inter}( G, \sigma ) $ as number of cross-community edges.
<br>

- Algorithm
  - For every $ \sigma \in \mathcal{L} $, calculate $ score ( \sigma ) $.
  - Sample and output a labeling $ \hat{\sigma} \in \mathcal{L} $ with probability $ exp(-\epsilon \times score( \sigma )) $.
<br>

- Privacy Analysis
  - Satisfies $ \varepsilon $-edge DP.
<br>

- Error / Utility Analysis
  - The algorithm satisfies exact recovery if $ r = 2 $ and $ \sqrt{a} - \sqrt{b} > \max[\sqrt{2}, {2 \over ( \sqrt{2} - 1 )\epsilon}]$.

### 4.3 Graph Perturbation Mechanism via Randomized Response (RR)
- For a graph with an adjacency matrix $ A $, perturb each element independently to satsify $ \varepsilon $-edge DP.
  - Pick perturbation probability $ \mu = 1 / ( e^{\epsilon} + 1 )$.
<br>

- Algorithm
  - Perturb $ A \rightarrow \tilde{A} $ via Randomized Response mechanism.
  - Apply community detection algorithm on $ \tilde{A} $.
  - Output $ \hat{\sigma} ( \tilde{A} ) $.
<br>

- Privacy Analysis
  - Satisfies $ \varepsilon $-edge DP for $ \forall \epsilon \geq \epsilon_{n} = \Omega (\log{n}) $.
<br>

- Error / Utility Analysis
  - The algorithm satisfies exact recovery if $ r = 2 $ and $ \sqrt{a} - \sqrt{b} > \sqrt{2} \times {\sqrt{e^{\epsilon} + 1} \over \sqrt{e^{\epsilon} - 1}} + {1 \over \sqrt{e^{\epsilon} - 1}}$.
<br>

---

## 5. My Commentary

- ...