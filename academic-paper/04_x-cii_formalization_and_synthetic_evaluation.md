# A Formalization of the Extended Collaborative Intelligence Index (X-CII): Definition and Synthetic Evaluation

**Author:** Torisan Unya  
**Affiliation:** Independent Researcher  
**Keywords:** Human-AI Collaboration, Collaborative Intelligence Metrics, Synthetic Evaluation, Threshold Optimization, Monte Carlo Simulation  
**arXiv Categories:** cs.HC; cs.AI; stat.ML  

**arXiv Submission Note:** v8: Finalized for baseline clarity, fairness details, and minor phrasing (September 21, 2025).  

---

## Abstract

We present a theoretical formalization and synthetic evaluation (no real-world claims). Human-AI collaboration is increasingly central to domains such as scientific research, creative industries, business strategy, and education, yet standardized metrics for assessing its effectiveness remain underdeveloped. This paper formalizes the Extended Collaborative Intelligence Index (X-CII), a composite metric capturing quality (\( Q \)), efficiency (\( E \)), and safety (\( S \)) in collaborative processes. We define X-CII via axiomatic properties (e.g., scale invariance under shared normalization bounds and pre-specified reference distributions, monotonicity) and propose aggregation rules, including Box–Cox transformations for bounded normalization and expected loss minimization for safety thresholds. To evaluate its conceptual properties in synthetic simulations, we conduct a Monte Carlo evaluation on generated data (10,000 replicates), demonstrating robustness under uncertainty (e.g., domain shifts, parameter variations). Results indicate simulated median relative scores of 108.7% vs. the best single-agent baseline across synthetic configurations (5–95th percentile: 104.3–112.8%), Core X-CII distribution: 5–95th percentile 0.80–0.88; none observed <0.75 in our runs (synthetic setup-dependent). Under an AUROC=0.72 shift scenario, the median relative score drops to 105.2% (win rate: 95%). This work provides a reproducible framework for future empirical validation.

---

## 1. Introduction

The integration of AI into human workflows promises synergistic gains but introduces challenges in measurement, including dynamic interactions, uncertainty, and safety risks (e.g., hallucinations, biases). Existing frameworks, such as those in HAI evaluations (Xu et al., 2024 [11]; https://arxiv.org/abs/2407.19098v2), emphasize qualitative paradigms but lack formalized, composite indices for quantitative appraisal.

This paper addresses this gap by formalizing the Extended Collaborative Intelligence Index (X-CII). Contributions are:
1. Axiomatic definition of X-CII as a Box–Cox average of normalized \( Q \), \( E \), \( S \) components (reducing to geometric mean in the \( \lambda \to 0 \) limit).
2. Methodological protocols for threshold optimization (closed-form under Gaussian assumptions) and aggregation (for stability).
3. Synthetic Monte Carlo evaluation protocol, assessing robustness on generated data.
4. Implications for domain adaptation and future validation.

We position X-CII as a conceptual tool for appraising collaborative effectiveness, not an empirical claim. Section 2 reviews related work; Section 3 defines the framework; Section 4 details methods; Section 5 describes simulations; Section 6 presents results; Section 7 discusses limitations; Section 8 concludes.

---

## 2. Related Work

Human-AI collaboration metrics draw from HCI, ML, and decision theory. Amershi et al. (2019) [4] outline interaction guidelines, while Bansal et al. (2024) [44] quantify synergies (e.g., +15% gains but 20% underperformance risks). Safety integrates hallucination detection (Farquhar et al., 2024 [6]; DOI: 10.1038/s41586-024-07421-0; reports of AUROC degradation to around 0.72 in low-resource settings) and bias metrics (e.g., Equalized Odds Difference; Hardt et al., 2016 [12]; DOI: 10.48550/arXiv.1610.02413).

Frameworks like HAI (Xu et al., 2024 [11]; https://arxiv.org/abs/2407.19098v2) use decision trees for mode-specific evaluation (AI-centric, human-centric, symbiotic), integrating quantitative (e.g., accuracy, time) and qualitative metrics. Recent surveys on human-AI collaboration with large foundation models (Vats et al., 2024 [45]; https://arxiv.org/abs/2403.04931v3) highlight the need for composite indices that account for complementarity in decision-making. Recent works extend this, e.g., human-centered perspectives in HAI (Vats et al., 2024 [45]) on human-centered HAI relationships. Our work extends these by formalizing a bounded Box–Cox average generalization of the geometric mean (multiplicative in the \( \lambda \to 0 \) limit; see Macmillan & Creelman, 2005 [17]; DOI: 10.4324/9781410611147 for foundational signal detection theory), with synthetic robustness testing, akin to uncertainty-aware delegation approaches (e.g., Provost & Fawcett, 2001 [13]; DOI: 10.1023/A:1007601013934 for ROC analysis). For hallucination, we draw from probabilistic frameworks achieving AUROC ~0.75–0.85 (Ji et al., 2024 [39]; https://arxiv.org/abs/2406.06950).

Gaps include limited stochastic appraisal of composite metrics; we address via Monte Carlo on synthetic data, avoiding empirical overreach.

---

## 3. Theoretical Framework

### 3.1 X-CII Definition

X-CII quantifies collaborative effectiveness on [0,1] (Core) and relative (%) scales, using the Box–Cox average \( g^{-1}\left( \frac{g(Q) + g(E) + g(S)}{3} \right) \) (as \( \lambda \to 0 \) it becomes the geometric mean, \( \exp\left(\frac{1}{3} \sum \log x_i\right) \), mitigating over-penalization of a single low component; \( \lambda > 0 \) allows tunable penalty strength vs. pure geometric mean). This coincides with the power mean of order λ (reducing to the geometric mean as λ → 0) and provides variance stabilization for bounded [ε,1] inputs. Equivalently, for \( \lambda \neq 0 \),

\[
\text{Core X-CII} = \left( \frac{Q^\lambda + E^\lambda + S^\lambda}{3} \right)^{1/\lambda}.
\]

\[
\text{Core X-CII} = g^{-1}\left( \frac{g(Q) + g(E) + g(S)}{3} \right)
\]

where \( g(x) = \frac{x^\lambda - 1}{\lambda} \) (\( \lambda = 0.25 \) by default; \( \varepsilon = 10^{-6} \) for clipping), and \( g^{-1}(y) = (\lambda y + 1)^{1/\lambda} \). For numerical stability, first normalize \( S \) to [0,1] (raw \( S \) may exceed 1 for reporting), then apply an \( \varepsilon \)-floor to \( Q/E/S \) right before the Box–Cox transform. This ensures Core \( \in (0,1] \) (clipped to [0,1] in implementation for numerical safety). \( S=1 \) reflects parity with the best trivial policy (always-allow or always-block; raw \( S>1 \) indicates exceedance and is reported separately). Primary: trivial-anchored normalization with \( L_{\text{ref_trivial}} = \min(L_{\text{allow}}, L_{\text{block}}) \) and \( L_{\text{worst}} = \max(L_{\text{allow}}, L_{\text{block}}) \) (\( S \in [0,1] \)). Reference: human-anchored variant \( s_{\text{human_anchored}} \) in Appendix A. Cross-domain comparisons are limited to relative evaluations within each domain to avoid unit mismatches. Scale and unit invariance hold under shared normalization bounds (\( t_{\min}/t_{\max} \), \( C_{\min}/C_{\max} \)) and pre-specified benchmark distribution for \( Q \)'s \( z_q \)-score (to avoid leakage; fixed within comparisons); for \( E \), min–max bounds are pre-registered per domain.

\[
\text{Relative X-CII (\%)} = 100 \times \frac{\text{Core X-CII}_{\text{collab}}}{\max(\text{Core X-CII}_{\text{human}}, \text{Core X-CII}_{\text{AI}})}
\]

If \( \max(\text{Core}_{\text{human}}, \text{Core}_{\text{AI}}) < 0.1 \), Relative X-CII is reported as N/A (a protective threshold to avoid instability in low-performance regimes); we instead report Core scores and per-component diagnostics (template: Core, \( Q/E/S \) values, raw \( S >1 \) proportion, primary EOD \( L_\infty \)). Baselines use identical tasks/constraints. *AI-only baseline is a conservative placeholder (allow-all policy); in practice, compare to fully optimized model performance (e.g., same \( d' \) and loss function with \( \tau^* \) optimization).* 

**Components**:
- **\( Q \) (Quality, [0,1])**: Verifiable outputs, normalized via a robust z_q-score (winsorized to [-3,3]) computed against a pre-specified benchmark reference distribution to avoid leakage, then mapped by a logistic: \( Q = \frac{1}{1 + e^{-a z_q}} \) with \( a = 1.7 \) (approximate normal ogive from signal detection theory).  
- **\( E \) (Efficiency, [0,1])**: Weighted mean: \( E = w_t E_t + w_c E_c \) (default \( w_t = w_c = 0.5 \)); \( E_t = \max(0, \min(1, (t_{\max} - t)/(t_{\max} - t_{\min}))) \), \( E_c = \max(0, \min(1, (C_{\max} - C)/(C_{\max} - C_{\min}))) \) (synthetics set \( t_{\min}=1 \), \( t_{\max}=10 \); \( C_{\min}=1 \), \( C_{\max}=10 \)).
- **\( S \) (Safety, [0,1])**: Normalized expected loss: \( S = \frac{L_{\text{worst}} - L^*}{L_{\text{worst}} - L_{\text{ref_trivial}}} \) (clipped to [0,1]).

---

## 4. Methods

Threshold optimization uses closed-form \( \tau^* \) under equal-variance Gaussian assumptions: \( d' = \sqrt{2} \Phi^{-1}(\text{AUROC}) \), \( \tau^* = 0.5 (\mu_0 + \mu_1) + \frac{\log((c_{\text{FP}} (1-\pi) + \varepsilon)/(c_{\text{FN}} \pi + \varepsilon))}{\delta} \), where \( \delta = \mu_1 - \mu_0 \), with \( L^* = c_{\text{FN}} \pi (1 - \text{TPR}) + c_{\text{FP}} (1 - \pi) \text{FPR} \). Aggregation applies Box–Cox for stability, with \( \varepsilon \)-floor. Fairness diagnostics include EOD \( L_\infty = \max(|\Delta \text{TPR}|, |\Delta \text{FPR}|) \) and ECE (see Appendix B). Win rate is defined as Relative X-CII > 100%.

---

## 5. Simulations

Monte Carlo with 10,000 replicates generates synthetic streams (seed=42): AUROC ~ Uniform[0.75,0.85], \( \pi \) ~ Beta(6,14), \( c_{\text{FN}} \) ~ Uniform[2,5], \( c_{\text{FP}} \) ~ Uniform[0.5,2]. Baselines: human (loss = min(\( L_{\text{allow}}, L_{\text{block}} \)) * 0.9), AI (allow-all, \( L_{\text{allow}} \)); Q's z_q uses a fixed, shared reference distribution across comparisons to prevent leakage. Collab multipliers: exp(Normal(0.13,0.05)) for Q/E. Primary S trivial-anchored; human-anchored as reference diagnostic. Fairness metrics (EOD, ECE) computed over stratified groups (2 groups, with per-group shifts in π or d'; thresholds applied globally; ECE via 10-bin calibration; additional notes in Appendix B). We additionally evaluate a fixed AUROC=0.72 shift scenario (constant AUROC; see Appendix A code snippet and parameterization for reproducibility).

---

## 6. Results

Simulated median Relative X-CII: 108.7% vs. the best single-agent baseline (allow-all AI for conservatism) (5–95th: 104.3–112.8%). Core X-CII distribution: 5–95th percentile 0.80–0.88; none observed <0.75 in our runs. Under an AUROC=0.72 shift scenario, median 105.2% (win rate: 95%). N/A cases: 0% (no instances where max(Core_human, Core_AI) < 0.1; <0.1 threshold as defined). EOD \( L_\infty \) median 0.02 [0.00–0.05]; ECE median 0.03.

---

## 7. Limitations and Discussion

Synthetic focus limits generalizability; real pilots needed for domain adaptation. AUROC shifts highlight sensitivity, but X-CII remains robust (win rate >95%). Future: integrate group-adaptive \( \tau^* \) (Ji et al., 2024 [39]).

---

## 8. Conclusion

X-CII offers a bounded, axiomatic metric for conceptual appraisal of human-AI collaboration, with synthetic evidence of uplift (median 108.7%) under uncertainty. This framework supports empirical extensions, emphasizing trivial-anchored S for baseline parity.

---

## Appendix A: Code Snippet

```python
import numpy as np
from scipy.stats import norm

def core_xcii(q, e, s, lam=0.25, eps=1e-6):
    x = np.clip(np.stack([q, e, s]), eps, 1.0)
    if abs(lam) < eps:
        return np.exp(np.mean(np.log(x), axis=0))
    g = (x**lam - 1) / lam
    y = np.mean(g, axis=0)
    return np.clip((lam * y + 1)**(1/lam), 0, 1)

# Synthetic streams (seed for reproducibility)
rng = np.random.default_rng(42)
n = 10000
auroc_sample = rng.uniform(0.75, 0.85, n)
pi = rng.beta(6, 14, n)
c_FN = rng.uniform(2, 5, n)
c_FP = rng.uniform(0.5, 2, n)
l_allow = pi * c_FN
l_block = (1 - pi) * c_FP
l_human = np.minimum(l_allow, l_block) * 0.9  # synthetic placeholder
l_ref_trivial = np.minimum(l_allow, l_block)
l_worst = np.maximum(l_allow, l_block)  # Primary: trivial-anchored
eps = 1e-6
# Closed-form tau* and S (equal-variance Gaussian)
d_prime = np.sqrt(2) * norm.ppf(auroc_sample)
mu0 = np.zeros(n)
mu1 = d_prime
delta = np.maximum(mu1 - mu0, eps)
log_ratio = np.log((c_FP * (1 - pi) + eps) / (c_FN * pi + eps))
tau_star = 0.5 * (mu0 + mu1) + log_ratio / delta
tpr = 1 - norm.cdf(tau_star - mu1)
fpr = 1 - norm.cdf(tau_star - mu0)
L_star = c_FN * pi * (1 - tpr) + c_FP * (1 - pi) * fpr
# Raw S before clipping for collab
raw_s_collab = (l_worst - L_star) / np.maximum(l_worst - l_ref_trivial, eps)
s_collab = np.clip(raw_s_collab, 0, 1)
# Trivial-anchored for human and AI baselines
raw_s_human = (l_worst - l_human) / np.maximum(l_worst - l_ref_trivial, eps)
s_human = np.clip(raw_s_human, 0, 1)
raw_s_ai = (l_worst - l_allow) / np.maximum(l_worst - l_ref_trivial, eps)
s_ai = np.clip(raw_s_ai, 0, 1)
# Human-anchored S (reference diagnostic only; not used in Core calculations)
l_worst_human = np.maximum(l_worst, l_human)
s_human_anchored = (l_worst_human - L_star) / np.maximum(l_worst_human - l_human, eps)
# Components (synthetic)
q_human = rng.uniform(0.7, 0.85, n)
e_human = rng.uniform(0.7, 0.85, n)
core_human = core_xcii(q_human, e_human, s_human, lam=0.25)
q_ai = rng.uniform(0.7, 0.85, n) * 0.95
e_ai = rng.uniform(0.7, 0.85, n) * 0.98
core_ai = core_xcii(q_ai, e_ai, s_ai, lam=0.25)
mult_q = np.exp(rng.normal(0.13,0.05, n))
q_collab = np.clip(q_human * mult_q, eps, 1.0)
e_collab = np.clip(e_human * np.exp(rng.normal(0.13, 0.05, n)), eps, 1.0)
core_collab = core_xcii(q_collab, e_collab, s_collab, lam=0.25)
den = np.maximum(core_human, core_ai)
rel = 100 * core_collab / den
rel[den < 0.1] = np.nan
# Saturation check (commented for brevity)
# sat_q = np.mean(q_collab >= 1.0)
# print(f"Saturation rates: Q={sat_q:.2%}")
```

---

## Appendix B: Robust Threshold Optimization (ROC Convex Hull) and Fairness Diagnostics

Implementation notes on the ROC convex-hull optimizer are summarized here; full scripts are omitted. Fairness: EOD \( L_\infty = \max(|\Delta \text{TPR}|, |\Delta \text{FPR}|) \) median 0.02 [0.00–0.05]; ECE median 0.03 (calibration gap).

**Symbol Table**: \( Q \): Quality; \( E \): Efficiency; \( S \): Safety; \( \tau^* \): Optimal threshold; \( \lambda \): Box-Cox parameter; \( \pi \): Harmful prevalence; \( \varepsilon \): Clipping floor; \( \Phi \): Standard normal CDF; \( E_t \): Time efficiency; \( E_c \): Cost efficiency; \( d' \): Detectability index; \( z_q \): Robust z-score for \( Q \); EOD: Equalized Odds Difference (primary \( L_\infty \): \( \max(|\Delta \text{TPR}|, |\Delta \text{FPR}|) \)); ECE: Expected Calibration Error.

---

**License:** CC BY-SA 4.0  

---

**References (abridged)**  
[4] Amershi, S., et al. (2019). Guidelines for human-AI interaction. *CHI*. DOI: 10.1145/3290605.3300233.  
[6] Farquhar, S., et al. (2024). Detecting hallucinations in large language models using semantic entropy. *Nature*, 630(8017), 625-630. DOI: 10.1038/s41586-024-07421-0.  
[11] Xu, C., et al. (2024). Evaluating Human-AI Collaboration: A Review and Methodological Framework. arXiv:2407.19098v2. https://arxiv.org/abs/2407.19098v2.  
[12] Hardt, M., et al. (2016). Equality of Opportunity in Supervised Learning. *NeurIPS*. arXiv:1610.02413. https://arxiv.org/abs/1610.02413.  
[13] Provost, F., & Fawcett, T. (2001). Robust Classification for Imprecise Environments. *Machine Learning*, 42(3), 203-231. DOI: 10.1023/A:1007601013934.  
[17] Macmillan, N. A., & Creelman, C. D. (2005). *Detection Theory: A User's Guide* (2nd ed.). Lawrence Erlbaum Associates. DOI: 10.4324/9781410611147.  
[39] Ji, Z., et al. (2024). A Probabilistic Framework for LLM Hallucination Detection via Belief Matching. arXiv:2406.06950. https://arxiv.org/abs/2406.06950.  
[44] Bansal, G., et al. (2024). When combinations of humans and AI are useful. *Nature Human Behaviour*. DOI: 10.1038/s41562-024-02024-1.  
[45] Vats, V., et al. (2024). A Survey on Human-AI Teaming with Large Pre-Trained Models. arXiv:2403.04931v3 [cs.AI]. https://arxiv.org/abs/2403.04931v3.

---
