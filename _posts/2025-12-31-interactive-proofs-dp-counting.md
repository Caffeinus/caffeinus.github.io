---
title: "[Paper Review] Interactive Proofs For Differentially Private Counting"
date: 2025-12-31
categories: [paper-review, differential-privacy, cryptography]
tags: [differential-privacy, cryptography, secure-multiparty-computation, verifiable-computation, zero-knowledge]
math: true
---

## Article Information

- **Title**: Interactive Proofs For Differentially Private Counting
- **Authors**: Ari Biswas, Graham Cormode
- **Venue**: CCS '23
- **Link**: [ACM DL](https://dl.acm.org/doi/10.1145/3576915.3616681)

---

## 1. Problem Statement

- Calculate aggregate statistics using Differential Privacy.
  - In trusted curator and client-server multiparty setting.
- Entity responsible for releasing DP statistics must also output a zero knowledge proof (ZKP) to verify that the statistic was computed correctly.
  -  with respect to committed client inputs, and the private randomness generated faithfully.

---

## 2. Motivation and Background

- We want to calculate aggregate statistics using Differential Privacy.
  - The malicious (releasing) entity can abuse the protocol and pick noise chosen to distort the statistics.
  - To ensure public trust in DP, it is critical to verify that any loss in utility can be attributed solely to unavoidable DP randomness.
<br>
- **Indistinguishability**: two probability distributions are computationally indistinguishable if for all non-uniform PPT turing machines $ D $("distinguishers"), the two output distributions of $ D $ differ by at most a negligible function.
  - Formally, $ \forall D, \forall \kappa \in \mathbb{N}, \exists \mu (\kappa) $ negligible s.t. $ \vert \Pr[D(X_{\kappa}) = 1] - \Pr[D(Y_{\kappa}) = 1] \vert \leq \mu (\kappa)$.
- **Commitments**: Ensures that participants cannot change their response during the protocol.
  - We will write Commitment algorithm as $ Com : M_{pp} \times R_{pp} \rightarrow C_{pp} $. for public parameter $ pp $.
  - $ M_{pp} $: message space, $ R_{pp} $: randomness space.
  - **Hiding**: A commitment $ c_{x} $ reveals no information about $ x, r_{x} $ to a computationally bounded adversary.
  - **Binding**: There is no efficient algorithm that can find $ x', r_{x'} $ such that $ Com(x', r_{x'}) = Com(x, r_{x}) $.
  - **Zero Knowledge OR Opening**: the committing party can prove to a poly-time verifier that $ c_{x} $ is a commitment to either 1 or 0 without revealing which one it is.
- **Homomorphic Commitments**
  - For all $ x_{1}, x_{2} \in M_{pp} $ and  $ r_{1}, r_{2} \in R_{pp} $, operator $ \otimes $ satisfies $ Com(x_{1}, r_{1}) \otimes Com(x_{2}, r_{2}) = Com(x_{1} + x_{2}, r_{1} + r_{2}) $.
<br> 
- **Information Theoric DP**: Original privacy definition.
  - An algorithm $ M : \mathcal{X}^{n} \times \mathcal Q \rightarrow \mathcal{Y}$ satsifies $(\epsilon, \delta) $-DP means,
  - For all neighboring datasets $ X \sim X' $, query $ Q \in \mathcal{Q} $, and set of output $ T \subseteq \mathcal{Y} $,
  - $ \Pr[M_{Q}(X) \in T] \leq e^{\epsilon} \Pr[M_{Q}(X') \in T] + \delta $.
- **Computational DP(IND-CDP)**: Indistinguishability concept involved.
  - Fix $ \kappa, n \in \mathbb{N} $.
  - Let $ \delta(\kappa) \leq \kappa^{-\omega(1)} $ be a negligible function.
  - The family of algorithms $ M = \{ M_{\kappa} : \mathcal{X}^{n}_{\kappa} \rightarrow \mathcal{Y}_{\kappa} \} $ is computationally $\epsilon$-DP means,
  - For all non-uniform PPT turing machines $ D $, $ X \sim X' $, $ T \subseteq \mathcal{Y}_{\kappa} $,
  - $ \Pr[D(M_{\kappa}(X, Q) \in T) = 1] \leq e^{\epsilon} \Pr[D(M_{\kappa}(X', Q) \in T) = 1] + \delta(\kappa) $.
- **DP error**: Define the expected error of the mechanism $ \mathcal{M} $ relative to $ \mathcal{Q} $ as $ Err_{\mathcal{M}, \mathcal{Q}} = \mathbb{E}[\lVert \mathcal{Q}(X) - \mathcal{M}_{\mathcal{Q}}(X) \rVert_{1}] $.

---

## 3. Main Contributions

- Formal definition for Interactive Proofs For Differential Privacy in both the trusted curator and client-server multiparty setting.
- Instantiations of Verifiable DP by computing DP counting queries.
  - both in the trusted curator and client-server multiparty setting.
- Experiments to show that their protocols with formal theoretical guarantees are also practical.
- Information-theoretic verifiable DP is impossible.

---

## 4. Technical Overview

### 4.1 Security Models for Verifiable DP

### 4.2 Verifiable Binomial Mechanism

### 4.3 Seperation under Verifiable DP

---

## 5. My Commentary

- ...

---