# PROJECT ATHENA — LONG-HORIZON STRATEGIC INTELLIGENCE SYSTEM

> **Version 3.0 — Fable Max Remake.** Supersedes the Project Athena PRD V2.0 as the working specification of Athena's objective, algorithms and acceptance. The V2.0 text is preserved unchanged as `docs/athena/ATHENA_PRD_V2.md` (ODA AI PR #258, with the original Word document and the v5.1 Master PRD and Build Plan alongside it) and remains the certified lineage baseline of this document. Every V2 section (1–150) is retained in meaning; Section 50 is the traceability table from V2 to V3. All performance figures in this document are **specification targets or derived bounds**, never measured results. Where a multiplier is derived from a theorem the derivation is shown; where it is a design target it is labelled as one.

### **Agent-Readable Product Requirements Document**

**Version:** 3.0 (Fable Max Remake)  
**Status:** Foundational / Ground-Truth Architecture for the reward side of LVL3.AI's recursive-improvement program  
**Organization:** LVL3.AI  
**Document type:** PRD + Mathematical Contract + Build Plan  
**Owner:** Spencer Brown (human; ratifies every change to the terminal objective)  
**Companion specifications:** RSI Exponential Improvement Fabric PRD v3.0 (`docs/RSI_PRD_V3.md`, PR #262, the engine); Project Sideways v1.0 (PR #264, the runtime); Ladder to Heaven v1.0 (PR #265, per-container improvement loops); Project Superman (PR #259, the leash).  
**Reference model:** `docs/athena/v3/reference_model.py`, validated in `docs/athena/v3/VALIDATION.md`, with recorded output in `docs/athena/v3/reference_results.json`.

**Primary objective:** Specify a long-horizon reward function that a recursively self-improving engine can optimize *hard* without the reward coming apart: an objective that measures growth rather than level, prices survival before growth, weights the far future honestly, assigns credit across years, bounds its own corruptibility, and cannot be rewritten by the engine it aims.

**In one paragraph.** Athena V3 scores a policy by the *growth rate* of the advised entity's strategic capital along its own path, taken in the worst tenth of plausible futures and under the least favourable of the owner's plausible preferences, after first requiring that the policy be admissible and that it not ruin the entity (Definition 3.1). It values the far future by what it knows of the hazard the entity faces, which makes long-lived plans worth more rather than less as they survive (Section 6). It learns from decisions years before their outcomes arrive, with estimators whose bias is bounded (Section 8). It gives the engine that builds capabilities a proxy to optimize, a measured budget of optimization to spend on it, and an audit it cannot see (Section 9); and it keeps the aim itself in a signed manifest that the engine cannot write to (Section 10). Every one of these claims is a proposition with a proof or a citation, every proposition that can be checked numerically is checked by a dependency-free reference model whose output is recorded beside this document, and the whole is tied to the V2 baseline by a 2× capability contract on ten benchmarks (Section 42).

**The three-part program this document belongs to.** In Spencer Brown's framing, recursive self-improvement is the engine, Athena is the reward function, and Superman is the leash. The RSI Fabric (v3.0) makes verified capability production grow exponentially. Athena V3 says what that capability is *for*, over horizons from minutes to decades, and does so in a form the engine can be pointed at. Superman bounds what either may do. Athena is the rider on the elephant: it does not move the elephant, it decides where the elephant should go and notices, early, when the elephant is heading somewhere else. V3 gives the rider a compass (Section 3), a map that is honest about the far horizon (Section 6), reins with a measured length (Section 9), and a saddle that cannot be thrown (Section 10).

**What changed from V2.0 (summary):**

1. **The objective is formal and it measures growth, not level.** V2 §4 maximized the expected terminal value of a resource vector. V3 maximizes the robust long-run *growth rate* of strategic capital (Section 2–3). Proposition 2.1 (Kelly–Breiman) shows the growth-optimal policy almost surely dominates every other policy exponentially; Proposition 2.2 (the ergodicity gap) shows that the V2 ensemble-average objective can prefer a policy that ruins almost every path. The multiplier here is not 2×: in the adverse case the sign of the answer changes.
2. **Survival is a certificate, not a simulation count.** The ruin constraint $P(\text{Ruin}) < \varepsilon$ of V2 §4 and §18 is enforced with barrier certificates (Lundberg, Ville, Prajna) that bound ruin analytically (Proposition 5.1), and with a closed-form drawdown law for fractional-Kelly exposure, $P(\text{drawdown to } x) = x^{2/c-1}$ (Proposition 5.3), which converts a ruin tolerance directly into a position size.
3. **The far future is weighted honestly.** V2 §81 asked for adaptive discounting. V3 derives it: discounting is uncertainty about the hazard rate, a mixture of exponentials is hyperbolic, Bayesian hazard updating makes it time-consistent (Proposition 6.1–6.2), and the far horizon is valued in average-reward form with Blackwell optimality (Proposition 6.4). Under the default (shape-one) hazard prior matched to V2's one-year discount, V3 puts 1.8× the weight of V2's exponential default on year 15 and 5.4× on year 30 (Section 6.4); the kernel is identified from survival data (Proposition 6.3), so in deployment the data set it.
4. **Credit across years is identified, not asserted.** V2 §27 and §98 asked for long-delay credit. V3 supplies the estimators and the conditions under which they are unbiased: the ledger is unconfounded by construction (Proposition 8.1), decisions are valued doubly-robustly (Proposition 8.2), 15-year outcomes are estimated from one-year surrogates with a bias bound (Proposition 8.3), hindsight and counterfactual credit are exact identities (Section 8.4), and the decision state machine is driven by anytime-valid evidence so that no decision is resolved prematurely (Proposition 8.5).
5. **Goodhart is a budget, not a worry.** V2 §44 ran proxy audits. V3 bounds the damage: a quantilizer caps expected harm at $1/q$ times the base rate (Proposition 9.1), the winner's curse from selecting among $n$ candidates is at most $\sigma\sqrt{2\ln n}$ (Proposition 9.2), and no unmeasured side quantity can drift by more than $\text{range}\cdot\sqrt{\text{KL}/2}$ under an optimization budget of KL nats (Proposition 9.3, the Pinsker budget). The audit is an e-process whose false-alarm rate is controlled at every stopping time (Section 9.5).
6. **Objective integrity is an invariant with a coverage bound.** V2 §105 said RSI must never silently redefine terminal objectives. V3 makes the terminal objective a signed, versioned manifest; every admitted change must pass a registered preference suite, and zero failures in $K$ checks bounds its disagreement with the terminal preferences by $\ln(1/\delta)/K$ (Proposition 10.2). The coherence rule of V2 §7.1 becomes a ladder of evidence thresholds whose false-change rate is bounded by Ville's inequality (Proposition 10.1). The commitment structure is Kydland–Prescott's rules-over-discretion, applied to a machine.
7. **Optionality is a number.** V2 §4 listed optionality $O_T$ without defining it. V3 defines it as empowerment, the channel capacity from the entity's action sequences to its future states (Section 7), computable by Blahut–Arimoto, zero in ruin, maximal at hubs, and ties it to real-option value under irreversibility.
8. **Every V2 engine (§5–§142) is restated as an algorithm contract** with inputs, outputs, a guarantee, a complexity, a failure mode and a fallback (Part II), and the whole is tied together by a 2× capability contract against the V2 baseline (Section 42), certified by lower confidence bounds on randomized ablations, with a 4× design target.
9. **Two results are new to this document and are labelled as such:** the **Goodhart speed limit** (Proposition 9.4), which converts an audit cadence and a proxy's error range into the maximum optimization the engine may apply between audits; and the **lessons-before-the-horizon multiplier** (Proposition 8.4), which shows that a program shorter than its own outcome horizon learns nothing from its decisions without surrogates and $r(L-h)$ lessons with them. Both are elementary; their value is that they are the right quantities to put in a manifest. Everything else is standard, specialized, and cited, including the identifiability of the discount kernel from survival data (Proposition 6.3), which is classical.
10. **The document verifies itself and says what it cannot promise.** Section 47 summarizes a self-contained reference model whose unedited output reproduces this document's numbers (twenty-one checks, including the worked decision of Section 3.6, each on its own seed) and detects three planted defects and two failures of the V2 rule; Section 48 lists the impossibility results the design respects, including the one receding-horizon guarantee this document explicitly does *not* make (Proposition 27.1(ii)), and the measurements that would falsify each central claim. An independent review of a draft of this document found two false guarantees and several loose constants; all are corrected here, and the review's method (recompute every number, check every constant) is the standard the document asks of its readers.
11. **The mathematics is drawn, wherever a result exists, from the established literature,** and much of it from work recognized by Nobel prizes: Markowitz (allocation), Nash, Harsanyi and Aumann (actors and equilibria), Lucas (every actor adapts), Kydland and Prescott (commitment over discretion), Hansen and Sargent (robustness), Kahneman, Thaler and Simon (human behavior and bounded rationality), Sims (attention as a resource), Romer, Solow and Arrow (compounding), Heckman, Angrist and Imbens (selection and causal identification; Imbens co-authored the surrogate index), Merton and Scholes (option value), Schelling (commitment and triggers), Akerlof, Spence and Stiglitz (information asymmetry and deception). Section 49 is the foundations index.

**Reading conventions:** MUST / SHALL / SHOULD / MAY follow RFC 2119. Formulas are given in LaTeX for humans and, where an agent must compute them, in fenced pseudo-code or YAML. Section 0.3 is the symbol table. Every proposition carries a status: **standard** (a cited result, specialized), **derived** (an elementary derivation from standard results, new in this document), or **conjecture**. A proposition's assumptions MUST be instantiated against the artifact at hand before it is invoked; a theorem's name is never a certificate.

---

### **0.1 The program on one page**

Seven equations run Athena V3. Everything else in this document is a lever on one of their terms or a check on one of their hypotheses.

$$
\textbf{(1) strategic capital and growth:}\quad W_t=\Phi_\theta(x_t),\qquad g_t=\ln\frac{W_{t+1}}{W_t},\qquad \bar G_T=\frac1T\sum_{t<T}g_t
$$

$$
\textbf{(2) the Athena Functional (lexicographic):}\quad
\mathcal J(\pi)=\operatorname{lex}\Big[\;\pi\in\Pi_{\text{adm}};\;\;
\sup_{P\in\mathcal P}P_\pi(\tau_{\mathcal R}\le T)\le\varepsilon;\;\;
\max\;\min_{\theta\in\Theta_\beta}\operatorname{CVaR}^{-}_{\alpha}\!\big[\bar G_T^{\theta}(\pi)\big];\;\;
\max\;\mathbb E[\bar G_T];\;\;
\max\;\mathbb E[\mathfrak E_n(s_T)];\;\;
\min\;C(\pi)\Big]
$$

$$
\textbf{(3) time:}\quad d(t)=\int_0^1\gamma^{t}\,w(\gamma)\,d\gamma=\mathbb E_\lambda\!\left[e^{-\lambda t}\right],\qquad
V=\sum_{h}w_h V^{(h)}+\rho_\infty
$$

$$
\textbf{(4) credit across years:}\quad
\hat\tau_{\text{long}}=\mathbb E\big[h(S,X)\mid W{=}1\big]-\mathbb E\big[h(S,X)\mid W{=}0\big],\qquad
\hat V_{\text{DR}}=\frac1n\sum_i\Big[\hat Q(x_i,\pi(x_i))+\tfrac{\pi(a_i\mid x_i)}{\mu(a_i\mid x_i)}\big(r_i-\hat Q(x_i,a_i)\big)\Big]
$$

$$
\textbf{(5) Goodhart budget:}\quad
\big|\mathbb E_\pi f-\mathbb E_{\pi_0}f\big|\le\operatorname{range}(f)\sqrt{\tfrac12\operatorname{KL}(\pi\|\pi_0)},\qquad
\mathbb E[\tilde U_{i^*}-U_{i^*}]\le\sigma\sqrt{2\ln n},\qquad
\mathbb E_{q\text{-quant}}[C]\le\tfrac1q\,\mathbb E_{D}[C]
$$

$$
\textbf{(6) survival certificate:}\quad
P_\pi(\tau_{\mathcal R}<\infty)\le B(s_0)\le\varepsilon\ \text{ for any ruin-barrier }B,\qquad
P\big(W\text{ ever reaches }xW_0\big)=x^{2/c-1}\ \text{ at Kelly fraction }c
$$

$$
\textbf{(7) contract:}\quad
\operatorname{LCB}_{95}\!\Big(\frac{\text{V3 score}}{\text{V2 baseline}}\Big)\ge 2\ \text{ on each of ten benchmarks (Section 43)},\qquad \text{design target }4
$$

Read (1) as what Athena measures, (2) as what it wants and in which order, (3) as how it weighs the far future, (4) as how it learns from decisions whose consequences arrive years later, (5) as the length of the reins it gives the engine, (6) as the floor beneath everything, and (7) as what this version promises over the last one.

### **0.2 Machine-readable summary**

```yaml
product:
  name: Project Athena
  organization: LVL3.AI
  version: "3.0"
  codename: fable_max_remake
  role_in_program: reward_function        # RSI Fabric = engine, Athena = reward, Superman = leash
  supersedes: "Project Athena PRD V2.0 (docs/athena/ATHENA_PRD_V2.md, PR #258)"
  reconciles: "Project Athena Master PRD and Build Plan v5.1 (docs/athena/Project_Athena_Master_PRD_Build_Plan_v5.1.md)"
  status: foundational
  companions:
    engine: "docs/RSI_PRD_V3.md (PR #262)"
    runtime: "Project Sideways v1.0 (PR #264)"
    per_container_loops: "docs/LADDER_TO_HEAVEN_PRD.md (PR #265)"
    leash: "Project Superman (PR #259)"
objective:
  measures: long_run_growth_rate_of_strategic_capital      # not terminal level
  order: [admissibility, survival, robust_growth, expected_growth, optionality, parsimony]
  survival: "sup over scenario ambiguity set of P(ruin by T) <= epsilon; certified by barrier, not by zero observed failures"
  robust_growth: "min over preference set Theta_beta of CVaR_alpha (lower tail) of time-average log-growth"
  optionality: "n-step empowerment of the terminal state"
  parsimony: "description length of the policy (PAC-Bayes priced)"
  scalarization_policy: "no scalarization is permanent; every level is reported; the order is a signed manifest"
time:
  discount: "mixture of exponentials = uncertain hazard; hyperbolic kernel; time-consistent under Bayesian hazard updating"
  far_horizon: "average-reward (gain) with Blackwell optimality; no discount"
  horizons: [T0_minutes, T1_days, T2_weeks, T3_quarters, T4_1y, T5_3y, T6_5y, T7_10y, T8_15y_plus]
  coherence_rule: "evidence thresholds tau_mission > tau_doctrine > tau_strategy > tau_tactics; false-change rate <= e^-tau (Ville)"
credit:
  ledger: "decisions are functions of the recorded belief state => logging propensity known, back-door set recorded"
  estimators: [doubly_robust, surrogate_index, hindsight_credit, counterfactual_scm, shapley_sampled]
  resolution: "anytime-valid e-process; a decision is RESOLVED only when its e-value crosses 1/alpha"
goodhart:
  optimization_budget_nats: declared_per_epoch
  selection: "quantilizer with registered q; argmax only inside audited candidate sets"
  audit: "independent slow audit reward; e-process monitor; alarm at e >= 1/alpha"
integrity:
  terminal_manifest: signed_versioned_two_key_human_ratified
  change_gate: "registered preference suite; zero failures in K checks => disagreement <= ln(1/delta)/K"
  drift_detector: "CUSUM on proxy-terminal agreement with declared ARL"
  interruptibility: "safely interruptible policy learning (Orseau-Armstrong); Superman interface"
contract:
  vs_v2_baseline:
    floor: 2.0
    design_target: 4.0
    certification: randomized_ablation_lcb_95_on_ten_benchmarks
  acceptance_items: 48          # V2 had 24
  benchmarks: 10                # V2 had 3
  propositions: 46              # reward-side, with proof or citation; v5.1's ATH-T01..T12 remain in force for the engine side
  new_results: [goodhart_speed_limit_9_4, lessons_before_horizon_8_4]
  explicit_non_guarantees: [recursive_feasibility_of_level1_27_1_ii]
  growth_on_ruin: condition_on_survival      # the convention of Definition 3.1
  reference_model_checks: 21
  negative_controls: 5
releases: [A0_memory, A1_advisor, A2_simulator, A3_allocator, A4_strategic_os, A5_rsi_native_institution]   # V2 §146 retained
```

### **0.3 Symbol table**

| Symbol | Meaning | Where defined |
|---|---|---|
| $s_t\in\mathcal S$ | full strategic state (belief state, ledger, capital, actors, commitments) | 1.1 |
| $x_t\in\mathbb R^d_{>0}$ | strategic capital vector: financial $F$, capability $C$, information $I$, legitimacy $L$, optionality $O$, position $Q$, each a sub-vector of the V2 §5.1 resource schema | 1.2 |
| $\Phi_\theta$ | registered aggregator (homogeneous of degree one); $\theta\in\Theta$ the preference parameters | 1.3 |
| $W_t=\Phi_\theta(x_t)$ | strategic wealth under $\theta$ | 1.3 |
| $g_t,\ \bar G_T$ | one-step log-growth; time-average log-growth over $T$ | 2.1 |
| $\mathcal R\subset\mathcal S$, $\tau_{\mathcal R}$ | ruin set (absorbing); its hitting time | 5.1 |
| $\varepsilon$ | ruin tolerance (owner-declared, per task) | 3.1 |
| $\alpha$ | tail level of the robust-growth criterion | 3.1 |
| $\Theta_\beta$ | $(1-\beta)$ credible set of preference parameters | 4.1 |
| $\mathcal P$ | scenario ambiguity set (Wasserstein ball or finite declared set) | 3.3 |
| $\operatorname{CVaR}^-_\alpha[G]$ | mean of the lower $\alpha$ tail of $G$ (a lower-tail conditional expectation; Section 3.2) | 3.2 |
| $\eta_\ell$ | slack permitted at lexicographic level $\ell$ | 3.1 |
| $\Pi_{\text{adm}}$ | admissible policies (Superman envelope, action-effect classes) | 3.1, 40 |
| $d(t)$, $w(\gamma)$, $\lambda$ | discount kernel; mixture weight over discount factors; hazard rate | 6.1 |
| $V^{(h)}$, $\rho_\infty$ | value head at horizon $h$; far-horizon gain (average reward) | 6.3 |
| $\mathfrak E_n(s)$ | $n$-step empowerment of state $s$ | 7.1 |
| $U$, $\tilde U$ | terminal objective; proxy objective the engine sees | 9.1 |
| $B$ | optimization budget, in nats of $\operatorname{KL}(\pi\|\pi_0)$ | 9.3 |
| $q$ | quantilizer fraction | 9.1 |
| $\mu$, $\pi$ | logging policy (propensity); evaluated policy | 8.2 |
| $S$, $X$, $h(s,x)$ | surrogates; covariates; surrogate index $\mathbb E[Y\mid S{=}s,X{=}x]$ | 8.3 |
| $E_t$ | e-process (nonnegative supermartingale with $E_0=1$) | 8.5, 9.5 |
| $c$ | fraction of the Kelly-optimal exposure | 5.3 |
| $f^*=\mu_e/\sigma^2$, $g^*=\mu_e^2/2\sigma^2$ | Kelly exposure and growth rate (lognormal) | 5.3 |
| $\mathcal K$ | the capability-demand message to the RSI Fabric | 11.1 |
| $\psi$ | information ratio (IDS) | 12.3 |

---
# PART I — THE LONG-TERM REWARD FUNCTION

## **1. Strategic capital: what Athena measures**

### 1.1 State

At decision epoch $t$ the strategic state is the tuple

$$
s_t=\big(b_t,\ x_t,\ \mathcal A_t,\ \mathcal C_t,\ \ell_t,\ m_t\big)
$$

where $b_t$ is the belief state over the latent world (Section 15), $x_t$ the strategic capital vector (1.2), $\mathcal A_t$ the actor models (Sections 19–22), $\mathcal C_t$ the outstanding commitments and open options, $\ell_t$ the decision ledger (8.1), and $m_t$ the terminal manifest version in force (10.1). The state is event-sourced (V2 §125): every component is a fold over an append-only log, so any past $s_u$, $u<t$, can be reconstructed exactly. This is not a convenience. Credit assignment (Section 8) and objective-integrity audits (Section 10) are only identified because the state at the time of each decision is recoverable.

### 1.2 The capital vector

V2 §4 named six terminal quantities, $R_T, C_T, O_T, I_T, L_T, Q_T$, and §5.1 gave an extensible resource schema. V3 keeps both and makes the relation explicit: the capital vector is

$$
x_t=\big(F_t,\ C_t,\ I_t,\ L_t,\ O_t,\ Q_t\big)\in\mathbb R^{d}_{>0},
$$

financial capital $F$ (capital, cash-equivalents, committed funding), capability $C$ (talent, technology, infrastructure, compute, IP, organizational capacity), information $I$ (knowledge, data, calibrated models, secrets held), legitimacy $L$ (trust, reputation, relationships, coordination capacity), optionality $O$ (defined in Section 7 as empowerment; also open real options), and position $Q$ (distribution, geographic access, freedom of action, time). Each is a sub-vector in the V2 §5.1 schema; the schema stays extensible, and every component MUST be measured in registered units with a declared estimator and a declared uncertainty.

Three requirements follow from V2 that V3 makes binding:

- **R1.2.1 Positivity.** Every component is strictly positive. A component that can reach zero is a ruin coordinate and is handled in Section 5, not in the aggregator.
- **R1.2.2 Productivity before quantity (V2 §5.2).** Each component carries its conversion rates into the others: the resource conversion graph of V2 §5.3 is the weighted directed graph $\mathcal G=(x\text{-components},\ \text{conversions})$ with edge weights (cost, delay, risk, confidence, scalability). Section 29 gives the bottleneck and shadow-price algebra on this graph.
- **R1.2.3 Decay is explicit.** Every component has a declared decay process (trust decays, knowledge goes stale, options expire). Growth is measured net of decay.

### 1.3 The aggregator and why it is homogeneous

An aggregator $\Phi_\theta:\mathbb R^d_{>0}\to\mathbb R_{>0}$ turns capital into strategic wealth $W_t=\Phi_\theta(x_t)$. V3 requires $\Phi_\theta$ to be **homogeneous of degree one** and **concave**. The registered default is the Cobb–Douglas form

$$
\Phi_\theta(x)=\prod_{i=1}^{d}x_i^{\theta_i},\qquad \theta_i\ge0,\ \sum_i\theta_i=1,
$$

with the CES family $\Phi_\theta(x)=\big(\sum_i\theta_i x_i^{\,r}\big)^{1/r}$, $r\le1$, admitted as an alternative. Homogeneity is what makes growth additive: under Cobb–Douglas,

$$
g_t=\ln\frac{W_{t+1}}{W_t}=\sum_i\theta_i\ln\frac{x_{i,t+1}}{x_{i,t}},
$$

so the growth of strategic wealth is the preference-weighted average of component growth rates, and the growth contribution of each capital line is auditable on its own. Concavity encodes complementarity: a position with capital and no legitimacy, or capability and no information, is worth less than the sum of its parts, which is V2 §5's "reproductive power" made precise.

**R1.3.1** Athena MUST NOT reduce the objective to one observable metric (V2 §4). $\Phi_\theta$ is not an observable; it is a registered, versioned preference whose parameters $\theta$ are uncertain (Section 4), and the lexicographic order of Section 3 sits above it. Every level of Section 3 is reported separately in the decision packet (V2 §42) so that the vector $J$ of V2 §143 is never collapsed silently.

### 1.4 Example: the capital vector of an advised entity

```yaml
capital_vector:
  F: {units: USD_real_2026, estimator: ledger_cash_plus_committed, uncertainty: 0.02}
  C: {units: capability_index, estimator: capability_registry_level_weighted, uncertainty: 0.15,
      sub: [talent_fte_weighted, compute_tflop_years, infrastructure, ip_count_weighted, org_capacity]}
  I: {units: nats_of_calibrated_information, estimator: forecast_resolution_minus_reliability, uncertainty: 0.25}
  L: {units: legitimacy_index, estimator: partner_trust_survey_plus_renewal_rate, uncertainty: 0.20, decay_halflife_months: 18}
  O: {units: nats, estimator: empowerment_n_step, uncertainty: 0.30}
  Q: {units: position_index, estimator: distribution_reach_times_freedom_of_action, uncertainty: 0.20}
aggregator:
  form: cobb_douglas
  theta_posterior_mean: {F: 0.20, C: 0.25, I: 0.15, L: 0.15, O: 0.15, Q: 0.10}
  theta_credible_set: "Dirichlet(alpha=40*mean), 90% set"      # Section 4
  manifest_version: "terminal-2026.10-v3"
```

---

## **2. Growth, not level: the ergodic objective**

### 2.1 Why the objective is a growth rate

V2 §4 wrote the objective as $\max_\pi\mathbb E[V(R_T,C_T,O_T,I_T,L_T,Q_T)]$: the expected terminal level. Strategic capital compounds multiplicatively, so a terminal-level objective is dominated by rare paths with enormous outcomes, and the policy that maximizes it can ruin almost every realized path. The quantity that describes what happens to *the* advised entity, which lives one path, is the time-average growth rate

$$
\bar G_T(\pi)=\frac1T\sum_{t=0}^{T-1}g_t=\frac1T\ln\frac{W_T}{W_0}.
$$

**Proposition 2.1 (growth optimality; standard: Kelly 1956, Breiman 1961, Algoet–Cover 1988).** Let the per-step growth factors $W_{t+1}/W_t$ under a stationary policy be stationary and ergodic with $\mathbb E|g_t|<\infty$. Let $\pi^\star$ maximize $\mathbb E[g_t]$ per step. Then (i) $\bar G_T(\pi^\star)\to\mathbb E_{\pi^\star}[g]$ almost surely, (ii) for any policy $\pi$ with $\mathbb E_\pi[g]<\mathbb E_{\pi^\star}[g]$, $W_T^{\pi}/W_T^{\pi^\star}\to0$ almost surely, exponentially fast, and (iii) $\pi^\star$ minimizes the expected time to reach any wealth level $W\gg W_0$, asymptotically.

*Proof sketch.* (i) is the ergodic theorem applied to $g_t$. (ii) follows from $\ln(W_T^\pi/W_T^{\pi^\star})=T(\bar G_T(\pi)-\bar G_T(\pi^\star))\to T(\mathbb E_\pi g-\mathbb E_{\pi^\star}g)<0$ a.s. (iii) is Breiman's theorem. The general (non-i.i.d., conditional) case is Algoet and Cover's asymptotic optimality of log-optimum investment. $\square$

**Proposition 2.2 (the ergodicity gap; standard: Jensen; Peters 2019).** For multiplicative growth factors $r_t>0$ i.i.d., $\mathbb E[W_T]=W_0(\mathbb E r)^T$ while $W_T=W_0\exp\!\big(T\bar G_T\big)$ with $\bar G_T\to\mathbb E[\ln r]$ a.s. Since $\ln\mathbb E r>\mathbb E\ln r$ unless $r$ is degenerate, the ensemble average grows strictly faster than almost every path, and it is possible that $\mathbb E r>1$ (the expected terminal level grows) while $\mathbb E\ln r<0$ (almost every path goes to zero).

*Example (reproduced by the reference model, check 1).* $r\in\{1.5,\,0.6\}$ with probability $\tfrac12$ each. $\mathbb E r=1.05$: the V2 objective says "take it". $\mathbb E\ln r=\tfrac12(\ln1.5+\ln0.6)=-0.0527$: the V3 objective says "refuse". After $T=200$ steps the expected wealth is $W_0\cdot1.05^{200}\approx 17{,}000\,W_0$, the median wealth is $W_0\,e^{-10.5}\approx 2.7\times10^{-5}\,W_0$, and 94.8% of paths end below where they started (exact binomial); after $1{,}000$ steps, 99.986% do, while the expected wealth has reached $W_0\,e^{48.8}$, carried by paths too rare to sample. $\square$

**R2.1.1** The expected terminal level of V2 §4 is retained as a *reported* quantity in every decision packet, with a mandatory ergodicity flag: when $\ln\mathbb E[W_T/W_0]/T-\mathbb E[\bar G_T]>\eta_{\text{erg}}$, the packet MUST say that the expected value is carried by a minority of paths and MUST show the path-median.

### 2.2 Why growth is measured on the aggregate and audited on the components

Under a homogeneous aggregator, $\mathbb E[g_t]=\sum_i\theta_i\mathbb E[\ln(x_{i,t+1}/x_{i,t})]$ only if the aggregator is Cobb–Douglas; for CES the decomposition is approximate. Either way the packet reports component growth, so that "growth" bought by liquidating legitimacy to buy capital is visible as a negative $L$-growth line. **R2.2.1** Any component whose expected growth is negative over the planning horizon MUST be named in the packet as a *consumed* capital, with the conversion it funded.

### 2.3 Relation to the RSI Fabric's growth law

The RSI Fabric v3 measures its own production rate $P=\lambda\,y_P\,\delta$ and its velocity $v=\tfrac{d}{dt}\ln P$ (RSI v3 §0.1, §64). In Athena's terms, capability production enters the capital vector through $C_t$: $\ln(C_{t+1}/C_t)\approx P_t\,\Delta t/C_t$ when the engine's verified capability units are the registered units of $C$. Athena's reward to the engine (Section 11) is therefore not "more $P$" but "more $g$": production counts at the rate at which it raises the robust growth of strategic wealth, net of what it consumes in $F$, $L$ and attention. This is the formal content of V2 §59's flywheel, and it is the sense in which Athena is the reward function for the engine rather than a second engine.

---

## **3. The Athena Functional**

### 3.1 Definition

**Definition 3.1 (the Athena Functional).** Fix a planning horizon $T$, a ruin tolerance $\varepsilon\in(0,1)$, a tail level $\alpha\in(0,1)$, a preference credible set $\Theta_\beta$ (Section 4), a scenario ambiguity set $\mathcal P$ (3.3), an empowerment depth $n$, slacks $\eta_2,\eta_3,\eta_4\ge0$, and a description-length functional $C(\pi)$ (Section 39). Athena V3 selects a policy by the lexicographic program

| Level | Name | Program | Slack |
|---|---|---|---|
| 0 | Admissibility | $\pi\in\Pi_{\text{adm}}$ (Superman envelope; action-effect classes declared; Section 40) | none |
| 1 | Survival | $\sup_{P\in\mathcal P}P_\pi\big(\tau_{\mathcal R}\le T\big)\le\varepsilon$ | none |
| 2 | Robust growth | $\max_\pi\ \rho_\alpha(\pi):=\min_{\theta\in\Theta_\beta}\ \inf_{P\in\mathcal P}\ \operatorname{CVaR}^-_\alpha\!\big[\bar G^{\theta}_T(\pi)\big]$ | $\eta_2$ |
| 3 | Expected growth | $\max_\pi\ \mathbb E\big[\bar G^{\bar\theta}_T(\pi)\big]$ among level-2 solutions within $\eta_2$ | $\eta_3$ |
| 4 | Optionality | $\max_\pi\ \mathbb E\big[\mathfrak E_n(s_T)\big]$ among level-3 solutions within $\eta_3$ | $\eta_4$ |
| 5 | Parsimony | $\min_\pi\ C(\pi)$ among level-4 solutions within $\eta_4$ | — |

$\operatorname{lex}$ means: solve level 2 subject to levels 0–1; among policies whose level-2 value is within $\eta_2$ of the optimum, solve level 3; and so on. Every level's value is reported. The order, the slacks and the parameters $(T,\varepsilon,\alpha,\beta,n)$ are part of the terminal manifest (Section 10) and change only through its ratification path.

**Convention for ruin paths.** $\bar G_T=-\infty$ on a path that is ruined, so levels 2 and 3 are not defined on the unconditional distribution whenever $P(\text{ruin})>0$. Ruin is priced at level 1; the growth statistics of levels 2 and 3 are therefore computed **conditional on survival to $T$**, and are labelled so in every packet. A manifest MAY instead declare a floor $g_{\min}$ assigned to ruined paths (which folds ruin into the tail again, at the cost of double counting it); the convention in force (`growth_on_ruin`) is a manifest field (10.1), and the packet names it.

**Why this order.** Admissibility first because the leash is not Athena's to loosen. Survival second because a growth rate is undefined for an entity that no longer exists; the constraint is on the worst scenario distribution in $\mathcal P$, not on the nominal one, because ruin lives in the tails that the nominal model knows least. Robust growth third because it is the quantity that describes the entity's own path (Proposition 2.1), taken over the lower tail of futures (3.2) and the worst admissible preference (Section 4), which is V2 §60's principle "remain unusually strong across many plausible futures" written as a program. Expected growth fourth so that, among policies that are robust, the one with the best central case is preferred. Optionality fifth as the tie-breaker that encodes V2 §60's "what can we position now so that many plausible future worlds become favorable", and because optionality is already partly priced inside growth through $O_t$. Parsimony last because, all else equal, a strategy that needs fewer bits to state needs less evidence to trust (Proposition 39.1).

**Proposition 3.1 (existence; standard).** (i) *Finite horizon.* With finite state and action spaces, horizon $T$, a finite scenario set $\mathcal P$ and a compact preference set $\Theta_\beta$, the set of (randomized, history-dependent) policies is compact in the topology of their occupation measures, and every level's objective and constraint in Definition 3.1 is continuous in that measure (the level-2 value is a minimum of continuous functions over the compact set $\Theta_\beta\times\mathcal P$, hence continuous). Each level's constrained program therefore attains its optimum on a closed feasible set, the level-$\ell$ feasible set is closed and nonempty whenever level $\ell-1$ was, and the lexicographic program with slacks is well posed. (ii) *Stationary (far-horizon) variant.* For the T8 head, with CVaR of the time average handled by augmenting the state with running wealth and the Rockafellar–Uryasev threshold (Bäuerle–Ott 2011; Chow–Tamar–Mannor–Pavone 2015), each level is a constrained MDP with finitely many constraints, which has a stationary optimal policy (Altman 1999), and the slack-lexicographic composition of such levels is the conditional-lexicographic MDP of Wray–Zilberstein–Mouaddib 2015. $\square$ For the general (continuous, partially observed) case no such guarantee is imported; Section 27 gives the approximation scope and the receding-horizon implementation.

### 3.2 The robust-growth criterion

Write $G$ for the random variable $\bar G_T^\theta(\pi)$ and $F_G$ for its distribution under a scenario measure $P$. The **lower-tail conditional expectation** at level $\alpha$ is

$$
\operatorname{CVaR}^-_\alpha[G]=\frac1\alpha\int_0^\alpha F_G^{-1}(u)\,du=\mathbb E\big[G\mid G\le F_G^{-1}(\alpha)\big]\ \text{(when $F_G$ is continuous)},
$$

the mean growth rate in the worst $\alpha$ fraction of futures. It equals $-\operatorname{CVaR}_{1-\alpha}[-G]$ in the loss convention of Rockafellar and Uryasev.

**Proposition 3.2 (two characterizations; standard: Rockafellar–Uryasev 2000; Artzner et al. 1999).**
(i) *Variational:* $\operatorname{CVaR}^-_\alpha[G]=\max_{\zeta\in\mathbb R}\big\{\zeta-\tfrac1\alpha\mathbb E[(\zeta-G)^+]\big\}$, a concave program in $\zeta$ that is a linear program on samples.
(ii) *Adversarial:* $\operatorname{CVaR}^-_\alpha[G]=\min\big\{\mathbb E_Q[G]:\ Q\ll P,\ dQ/dP\le\tfrac1\alpha\big\}$: the worst expectation an adversary can produce by reweighting scenarios by at most $1/\alpha$.

*Why it matters.* (i) is how Athena computes it: on $N$ scenario samples it is one LP. (ii) is what it means: Athena optimizes against an adversary who may make any scenario up to $1/\alpha$ times as likely as the model says, which is the right posture when scenario probabilities are "defensible but not precise" (v5.1 §11). The reference model verifies both characterizations agree on random samples (check 3).

**Proposition 3.3 (robustness preferences are entropic risk; standard: Donsker–Varadhan; Hansen–Sargent 2008).** For $\vartheta>0$,

$$
\min_{Q\ll P}\Big\{\mathbb E_Q[G]+\vartheta\operatorname{KL}(Q\|P)\Big\}=-\vartheta\ln\mathbb E_P\big[e^{-G/\vartheta}\big].
$$

So the Hansen–Sargent "multiplier preference" (a planner who fears the model is wrong by at most a KL-penalized amount) is exactly the entropic risk measure of $G$, and as $\vartheta\to\infty$ it recovers $\mathbb E_P[G]$. *Proof sketch.* The minimizer is the exponential tilt $dQ^*/dP\propto e^{-G/\vartheta}$; substitute. $\square$ Athena admits either $\operatorname{CVaR}^-_\alpha$ (hard reweighting cap) or entropic risk (soft reweighting penalty) at level 2; the manifest says which. The reference model verifies the identity numerically (check 3).

### 3.3 The scenario ambiguity set

$\mathcal P$ is one of: (a) a finite declared set of scenario measures (deep uncertainty mode, V2 §72, with minimax regret available as the level-2 criterion in place of CVaR, Savage 1951); (b) a Wasserstein ball $\{P:\ W_1(P,\hat P_N)\le\epsilon_N\}$ around the empirical scenario distribution. For (b):

**Proposition 3.4 (finite-sample guarantee; standard: Mohajerin Esfahani–Kuhn 2018, Fournier–Guillin 2015).** For a light-tailed true distribution and the radius $\epsilon_N(\beta)$ given in Mohajerin Esfahani–Kuhn (which scales as $N^{-1/\max(2,m)}$ in the scenario dimension $m$), with probability at least $1-\beta$ the DRO value $\inf_{P\in\mathcal P}\mathbb E_P[G]$ is a lower bound on the true out-of-sample expectation, and the DRO program is a finite convex program when $G$ is concave piecewise-linear in the scenario. $\square$

**R3.3.1** The packet MUST state which $\mathcal P$ was used and, under (b), $N$, $\epsilon_N$ and $\beta$. Under (a), the packet MUST show the regret table across the declared scenarios. Point estimates that differ by less than their uncertainty do not justify deleting an alternative (v5.1 §11).

### 3.4 The delayed-gratification test, in numbers

V2 §6 required Athena to be able to prefer $R_{t+3}=5$ over $R_{t+3}=100$ when $R_{t+15}(5)\gg R_{t+15}(100)$. Under Definition 3.1 the test is arithmetic. If the small path then compounds at rate $g_5$ and the large path at $g_{100}$ for the remaining 12 years, the small path wins at year 15 iff

$$
\ln5+12\,g_5>\ln100+12\,g_{100}\iff g_5-g_{100}>\frac{\ln20}{12}\approx0.25\ \text{per year}.
$$

The small path must out-compound the large one by 25 percentage points a year for twelve years, and the packet MUST show the evidence for a differential of that size, with its lower tail: under level 2 the comparison is made on $\operatorname{CVaR}^-_\alpha$ of the two growth rates, not on their means. V2's principle "waiting is not inherently optimal" is now a number the owner can see.

### 3.5 Reporting contract

```yaml
decision_packet.objective_report:
  level0_admissible: true
  level1_ruin_prob_worst_case: 0.004      # vs epsilon 0.01
  level1_certificate: {type: barrier, B_s0: 0.004}      # Section 5; "sampled" certificates carry (n_trials, failures, rule_of_three_bound)
  level2_robust_growth: {alpha: 0.10, value: 0.031, preference_set: "Theta_0.90", ambiguity_set: "W1 ball eps=0.08 N=4000 beta=0.05"}
  level3_expected_growth: 0.074
  level4_optionality_nats: 2.9
  level5_description_length_bits: 412
  ergodicity_flag: {ln_E_growth: 0.112, E_ln_growth: 0.074, gap: 0.038, path_median_W_T_over_W0: 3.0, mean_W_T_over_W0: 5.4}
  component_growth: {F: 0.05, C: 0.12, I: 0.09, L: -0.02, O: 0.04, Q: 0.06}
  consumed_capital: [{component: L, funded: "accelerated go-to-market", expected_recovery_years: 3}]
```

Schema (every field required unless marked optional; units and estimators are registered in the manifest):

```yaml
decision_packet.objective_report.schema:
  manifest_version: string
  level0_admissible: boolean
  level1: {ruin_prob_worst_case: number, epsilon: number, certificate: {type: enum[barrier, sampled, unresolved], detail: object}}
  level2: {alpha: number, value: number, criterion: enum[cvar_lower_tail, entropic, minimax_regret], preference_set: string, ambiguity_set: string, least_favorable_preference: {theta: object, in_words: string}}
  growth_on_ruin: enum[condition_on_survival, floor]      # the convention of 3.1; with a floor, g_min is stated
  level3: {expected_growth: number, slack_used: number}
  level4: {empowerment_nats: number, depth_n: integer, slack_used: number}
  level5: {description_length_bits: number}
  ergodicity_flag: {ln_E_growth: number, E_ln_growth: number, gap: number, path_median_W_T_over_W0: number, mean_W_T_over_W0: number, flagged: boolean}
  component_growth: map[string, number]
  consumed_capital: list[{component: string, funded: string, expected_recovery_years: number}]
  pareto_alternatives: list[{policy_id: string, levels: object}]
  infeasibility_certificate: optional {conflicting_constraints: list[string], owner_options: list[string]}
  information_actions: list[{id: string, evsi: number, cost: number, delay_cost: number}]     # Section 12
  review_triggers: list[{id: string, condition: string, arl0: number, persistence: string}]  # Section 16
  fallbacks_used: list[string]                                                                 # Section 40
```

### 3.6 The reward function end to end: a worked decision

One entity, fifteen years, three policies, scored by Definition 3.1. The world and the numbers are those of the reference model (check 19; seed 20261015, 6,000 scenarios): baseline log-growth $\mathcal N(0.03,\,0.08^2)$ a year; a shock year ($-0.35$) with probability $0.02$ a year; a shock year ruins the entity with probability $0.25$ if its operating reserve is below half and $0.01$ otherwise; a capability that, if it works (probability $0.70$), adds to growth from year 8 and halves shock damage; a prototype whose year-2 surrogate reports whether it works with 90% accuracy; half of any spend is conversion loss.

- **A, all in now:** commit 60% of the reserve at year 0; boost $+0.14$ a year from year 8 if the capability works. The reserve is below half for all fifteen years.
- **B, staged option:** 15% now for the prototype; read the surrogate at year 2; commit 30% more only on a positive reading; boost $+0.10$ from year 8. The reserve never falls below half.
- **C, do nothing.**

| Level | Quantity | A (all in) | B (staged) | C (nothing) |
|---|---|---|---|---|
| 1 | $P(\text{ruin by year 15})$ vs $\varepsilon=0.01$ | **0.077 — fails** | 0.004 | 0.004 |
| 2 | $\operatorname{CVaR}^-_{0.10}[\bar G_{15}\mid\text{survival}]$ (worst decile of surviving futures) | $-0.024$ | **$-0.014$** | $-0.021$ |
| 3 | $\mathbb E[\bar G_{15}\mid\text{survival}]$ | $0.054$ | $0.046$ | $0.023$ |
| 4 | terminal empowerment (nats), declared four-class terminal kernel | $0.75$ | $1.42$ | $1.09$ |
| 5 | description length (rules) | 1 | 3 | 0 |
| V2 | $\mathbb E[W_{15}/W_0]$ (expected terminal level, ruined paths at 0) | **2.46** | 2.20 | 1.50 |
| — | path-median $W_{15}/W_0$ | 2.48 | 2.06 | 1.43 |

The V2 objective selects **A**: it has the highest expected terminal level and even the highest expected growth among survivors. The Athena Functional rejects A at level 1 (it ruins 7.7% of futures against a tolerance of 1%) before growth is considered: the depleted reserve is what fails A, and it fails at level 1, not at level 2. It then selects **B** at level 2. The mechanism there is not the reserve but the capability: in 63% of B's futures (works, and the surrogate said so) the capability exists, adds $0.10$ a year from year 8 and halves shock damage, and those futures leave the lower tail entirely; what remains of B's worst decile is the less-bad part of its no-capability futures, whereas C's worst decile is the worst tenth of a whole population of baseline futures. Level 4 is reported but not needed; it is computed by Blahut–Arimoto on a declared terminal kernel with four state classes (ruin: absorbing; capability with a healthy reserve: hub; no capability: corridor; capability with a depleted reserve: dead end), so its ordering is a modelling choice recorded in the manifest and only its numbers follow from the kernel. The packet says all of this in one table, names A's ruin probability as the reason it was not chosen, and names level 2 as the reason B beat C. Every number above is reproduced, unedited, by `check19_worked_decision_end_to_end`, which runs on its own seed so that a re-implementation of this one example can be checked against it.

What the rest of Part I adds to this decision: the year-2 surrogate is a registered surrogate index with its own bias bound (8.3); B's two commitments are logged with propensities so their long-run effect is identified (8.1–8.2); the capability's progress proxy carries an optimization budget and an audit (9.3–9.5), so the engine building it cannot inflate the proxy past the audit; the year-8 payoff is valued with a hazard-mixture kernel (6.1), which is what makes a year-8 payoff worth building toward at all; and the decision is RESOLVED only when its e-process says so (8.5), not when the first good year arrives.

---

## **4. Preference robustness: no scalarization is permanent**

### 4.1 Preference uncertainty as a credible set

V2 §143 said no scalarization is permanent. V3 makes the aggregator parameters $\theta$ an uncertain object with a posterior $p(\theta\mid\mathcal D_{\text{pref}})$ learned from the owner's registered preference judgments (pairwise comparisons of outcomes, Section 10.3). $\Theta_\beta$ is its $(1-\beta)$ highest-density credible set. Level 2 of Definition 3.1 takes the minimum over $\Theta_\beta$: Athena optimizes the growth of strategic wealth under the least favorable preference the owner might plausibly hold. This is Gilboa–Schmeidler maxmin expected utility (1989) applied to the owner's own weights rather than to the world.

**Proposition 4.1 (the price of preference robustness; derived).** Let $\theta^\dagger\in\Theta_\beta$ attain the inner minimum for the chosen policy and let $\bar\theta\in\Theta_\beta$ be the posterior mean (which lies in the credible set when the posterior is unimodal). Under Cobb–Douglas, $\bar G^{\theta}_T$ is linear in $\theta$, so $\min_{\theta\in\Theta_\beta}\bar G_T^\theta=\bar G_T^{\bar\theta}-\max_{\theta\in\Theta_\beta}(\bar\theta-\theta)^\top\mathbf g$, where $\mathbf g$ is the vector of component growth rates. The robustness discount is at most $\operatorname{diam}_1(\Theta_\beta)\cdot\big(\max_i\mathbf g_i-\min_i\mathbf g_i\big)/2$: it shrinks as the owner's preferences are learned ($\Theta_\beta$ contracts) and as component growth becomes balanced. *Proof.* Both $\theta$ and $\bar\theta$ lie on the simplex, so for any constant $c$, $(\bar\theta-\theta)^\top\mathbf g=\sum_i(\bar\theta_i-\theta_i)(\mathbf g_i-c)\le\|\bar\theta-\theta\|_1\max_i|\mathbf g_i-c|$; take $c=(\max_i\mathbf g_i+\min_i\mathbf g_i)/2$. $\square$

**R4.1.1** The packet MUST report $\theta^\dagger$, the least-favorable preference, in plain words ("this plan is weakest if you care about legitimacy more than the registered weights say"). **R4.1.2** When $\operatorname{diam}(\Theta_\beta)$ is large enough that the robustness discount exceeds $\eta_2$, Athena SHOULD recommend a preference elicitation (Section 10.3) as an information action, priced by Section 12, before recommending a plan.

### 4.2 Reversible scalarizations

Because every level is reported and $\theta$ is versioned, the owner can re-rank the Pareto set of V2 §70 under any $\theta'$ without re-planning; Section 32 (successor features) gives the bound on the loss of re-using stored policies under a changed preference.

---

## **5. Survival: ruin as a certificate**

### 5.1 Definitions

The ruin set $\mathcal R\subset\mathcal S$ is owner-declared per task (v5.1 §13): a minimum operating reserve, an unrecoverable outage, loss of autonomy, irreversible reputational destruction, permanent dependency (V2 §18). It is absorbing: no policy leaves it. $\tau_{\mathcal R}=\inf\{t:s_t\in\mathcal R\}$. Level 1 of Definition 3.1 requires $\sup_{P\in\mathcal P}P_\pi(\tau_{\mathcal R}\le T)\le\varepsilon$. V2 §18's loss ladder (recoverable, severe, impairment, irreversible, ruin, systemic) is retained; only the last two are in $\mathcal R$, the others enter the growth rate as drawdowns.

### 5.2 Certificates, not counts

Zero observed failures in $n$ independent long-horizon simulations certifies only $P(\text{ruin})\le3/n$ at 95% (the rule of three; Hanley–Lippman-Hand 1983). To certify $\varepsilon=10^{-4}$ by counting one needs 30,000 independent simulations of the full horizon, and the result is a statement about the model, not the world. V3 prefers an analytic certificate.

**Proposition 5.1 (barrier certificate; standard: Ville 1939; Prajna–Jadbabaie–Pappas 2007; Lundberg 1903).** Let $B:\mathcal S\to[0,\infty)$ satisfy $B(s)\ge1$ for all $s\in\mathcal R$, and let $B(s_t)$ be a supermartingale under the policy $\pi$ and every $P\in\mathcal P$, i.e. $\mathbb E[B(s_{t+1})\mid s_t]\le B(s_t)$. Then $\sup_{P\in\mathcal P}P_\pi(\tau_{\mathcal R}<\infty)\le B(s_0)$. *Proof.* Ville's maximal inequality for nonnegative supermartingales: $P(\sup_t B(s_t)\ge1)\le B(s_0)$, and ruin forces $B\ge1$. $\square$

**Corollary 5.2 (Lundberg bound; standard).** If the one-step change in a scalar reserve $Z_t$ (e.g. $\ln F_t$, or operating reserve) has increments $X$ with $\mathbb E[e^{-\vartheta X}]\le1$ for some adjustment coefficient $\vartheta>0$, under every $P\in\mathcal P$, then $B(s)=e^{-\vartheta(Z-Z_{\text{ruin}})}$ is a ruin barrier and $P(\text{ruin})\le e^{-\vartheta(Z_0-Z_{\text{ruin}})}$. So a reserve of $Z_0-Z_{\text{ruin}}=\ln(1/\varepsilon)/\vartheta$ certifies tolerance $\varepsilon$ with no simulation at all. *Examples (reference model, check 11).* Steps $+1$ w.p. $0.6$, $-1$ w.p. $0.4$: $\vartheta=\ln1.5$; from reserve $10$, $P(\text{ruin})\le(2/3)^{10}=0.01734$, and because unit steps never overshoot the barrier the bound is exact for this walk. Steps $+1$ w.p. $0.7$, $-2$ w.p. $0.3$: $\vartheta=0.102$ and the bound from reserve $10$ is $0.361$, strictly above the simulated $0.349$, the gap being the overshoot. $\square$

**R5.2.1** A level-1 certificate MUST be one of: `barrier` (with $B$ and the supermartingale verification over $\mathcal P$), `sampled` (with $n$, failures, and the rule-of-three or Clopper–Pearson bound), or `unresolved`. An `unresolved` certificate forces the smaller reversible commitment path of v5.1 §13. **R5.2.2** Passing a finite stress suite is never reported as a universal bound (v5.1 §13).

### 5.3 From ruin tolerance to position size: the Kelly drawdown law

Where a decision is an exposure $f$ to an uncertain opportunity with log-return drift $\mu_e$ (in excess of the safe alternative) and volatility $\sigma$, the continuous-time log-growth rate is $g(f)=f\mu_e-\tfrac12f^2\sigma^2$, maximized at the Kelly exposure $f^*=\mu_e/\sigma^2$ with $g^*=\mu_e^2/2\sigma^2$. Write $f=c\,f^*$ for the **Kelly fraction** $c\in(0,1]$.

**Proposition 5.3 (fractional Kelly: growth and drawdown; standard: Thorp 2006; MacLean–Thorp–Ziemba 2011).**
(i) $g(cf^*)=g^*(2c-c^2)$: half-Kelly keeps $75\%$ of the maximal growth rate at a quarter of the variance of log-growth.
(ii) The probability that wealth *ever* falls to a fraction $x<1$ of its current level is $P(x)=x^{2/c-1}$. Full Kelly halves one's wealth at some point with probability $\tfrac12$; half-Kelly with probability $\tfrac18$; quarter-Kelly with probability $1/128$.
(iii) **Position sizing from a ruin tolerance.** To hold $P(\text{drawdown to }x)\le\delta$ choose $c\le\dfrac{2}{1+\ln\delta/\ln x}$. For $x=\tfrac12$, $\delta=0.01$: $c\le0.26$.

*Proof.* Let $Y_t=\ln(W_t/W_0)$. Under exposure $f=cf^*$, $dY=m\,dt+v\,dB$ with $m=f\mu_e-\tfrac12f^2\sigma^2$ and $v=f\sigma$. (i) Substituting $f=c\mu_e/\sigma^2$ gives $m=(\mu_e^2/\sigma^2)(c-\tfrac12c^2)=g^*(2c-c^2)$ and $v^2=c^2\mu_e^2/\sigma^2=2c^2g^*$. (ii) For $m>0$ and $\vartheta=2m/v^2$, $M_t=e^{-\vartheta Y_t}$ is a martingale, since its drift is $-\vartheta m+\tfrac12\vartheta^2v^2=0$. Let $\tau$ be the first time $Y$ reaches $\ln x<0$. Optional stopping at $\tau\wedge t$ and $t\to\infty$ (on $\{\tau=\infty\}$, $Y_t\to+\infty$ and $M_t\to0$) gives $1=\mathbb E[M_\tau;\tau<\infty]=x^{-\vartheta}\,P(\tau<\infty)$, so $P(\tau<\infty)=x^{\vartheta}$, and $\vartheta=2g^*(2c-c^2)/(2c^2g^*)=2/c-1$. (iii) Solve $x^{2/c-1}\le\delta$ for $c$. $\square$ The reference model verifies (i)–(ii) by simulation with the Broadie–Glasserman–Kou continuity correction for discrete monitoring (check 2) and shows full Kelly violating the drawdown constraint that half-Kelly meets (negative control E).

**Proposition 5.4 (estimation error shrinks the right exposure; derived).** If the drift is estimated as $\hat\mu_e=\mu_e+\eta$ with $\mathbb E\eta=0$, $\operatorname{Var}\eta=s^2$, then betting the plug-in Kelly $\hat f=\hat\mu_e/\sigma^2$ has expected growth $g^*-s^2/2\sigma^2$: estimation noise is a direct tax on growth, and the fraction $c$ that maximizes expected growth under noise is $c^*=\mu_e^2/(\mu_e^2+s^2)<1$. *Proof.* $\mathbb E[g(\hat f)]=\mathbb E[\hat f]\mu_e-\tfrac12\sigma^2\mathbb E[\hat f^2]=\mu_e^2/\sigma^2-(\mu_e^2+s^2)/2\sigma^2$; for $f=c\hat f$ the same computation gives $g^*(2c-c^2)-c^2s^2/2\sigma^2$, maximized at $c^*$. $\square$ This is V2 §19's "concentration when edge is high, diversification when uncertainty is high" as a formula: $c^*$ is the signal-to-noise ratio of the edge.

**R5.3.1** Kelly sizing applies only where the opportunity is repeated, the return distribution is measurable and wealth is fungible (v5.1 §13). Elsewhere, position limits come from the barrier certificate of 5.2 and the staged commitments of Section 28; the packet MUST say which regime applied.

### 5.4 Drawdowns, impairments and the growth rate

Non-ruin losses are not constraints; they are already inside $\bar G_T$ and, through level 2, inside its lower tail. A policy that accepts a 40% drawdown in the worst decile of futures pays for it in $\operatorname{CVaR}^-_\alpha$. Owners who want a hard drawdown limit declare it as a ruin coordinate in $\mathcal R$, and Proposition 5.3(iii) sizes exposure accordingly.

---

## **6. Multi-timescale valuation: weighing the far future honestly**

### 6.1 Discounting is uncertainty about the hazard rate

A single exponential discount $\gamma^t$ is the right kernel only if the entity faces a *known* constant hazard of termination (Samuelson 1937 as a model of survival). V2 §81 rejected a single factor. V3 derives the replacement. Let the hazard rate $\lambda$ be unknown with prior $w$; the probability that the entity (or the relevance of the plan) survives to $t$ is

$$
d(t)=\mathbb E_\lambda\big[e^{-\lambda t}\big]=\int_0^1\gamma^{t}\,w(\gamma)\,d\gamma\qquad(\gamma=e^{-\lambda}).
$$

**Proposition 6.1 (mixtures of exponentials are hyperbolic; standard: Sozou 1998; Fedus et al. 2019).** (i) If $\lambda\sim\operatorname{Gamma}(k,\beta)$ then $d(t)=(1+t/\beta)^{-k}$; with $k=1$ this is the hyperbolic kernel $1/(1+t/\beta)$. (ii) If $\gamma\sim\operatorname{Uniform}(0,1)$ then $d(t)=1/(1+t)$, so $V^{\text{hyp}}(s)=\int_0^1V^{\gamma}(s)\,d\gamma$: the hyperbolically discounted value is the average of exponentially discounted values over all discount factors. *Proof.* (i) is the Laplace transform of the Gamma density; (ii) $\int_0^1\gamma^td\gamma=1/(t+1)$. $\square$

**Proposition 6.2 (time consistency under Bayesian hazard updating; derived).** Let the entity survive to $t$ and update $w$ to the posterior $w_t(\lambda)\propto w(\lambda)e^{-\lambda t}$. The posterior-predictive survival over the next $s$ periods is $\mathbb E_{w_t}[e^{-\lambda s}]=d(t+s)/d(t)$. Hence the plan made at time $0$ for the interval $[t,t+s]$ and the plan made at time $t$ for the same interval use the same conditional weights, and no preference reversal occurs. For the Gamma prior the posterior is $\operatorname{Gamma}(k,\beta+t)$ and $d(t+s)/d(t)=\big((\beta+t)/(\beta+t+s)\big)^k$. *Proof.* Direct computation: $\int w(\lambda)e^{-\lambda t}e^{-\lambda s}d\lambda/\int w(\lambda)e^{-\lambda t}d\lambda$. $\square$

The point is that the "present bias" of hyperbolic discounting, which in a human is a preference anomaly (Laibson 1997; Thaler 1981), is in Athena a *belief*: long-surviving plans are revealed to face a lower hazard, and are valued accordingly. Athena does not become impatient as time passes; it becomes more confident the plan will survive. The reference model verifies both propositions numerically (check 4).

**Proposition 6.3 (the discount kernel is identified by survival data; standard: uniqueness of Laplace transforms; Elbers–Ridder 1982; Heckman–Singer 1984).** Write $\gamma=e^{-\lambda}\in[0,1]$. The kernel at integer horizons, $d(t)=\mathbb E[\gamma^t]$, $t=0,1,2,\dots$, is the moment sequence of the distribution of $\gamma$ on $[0,1]$, and the Hausdorff moment problem on a bounded interval is determinate: the moments determine the distribution uniquely. Hence the survival curve of plans and assets of a given kind, observed at yearly horizons, identifies the hazard prior $w$ for that kind, and two kinds with different survival curves have different kernels. *Proof.* Determinacy of the Hausdorff moment problem (Hausdorff 1921; Shohat–Tamarkin 1943); the mixed-proportional-hazard identification results of Elbers–Ridder and Heckman–Singer cover the case with covariates. $\square$ The practical estimator is the nonparametric maximum-likelihood mixing distribution (Laird 1978) fitted to survival times with survivorship correction (Section 24).

**R6.1.1** $w$ is learned per capital line and per domain (V2 §81: cash flows, knowledge, trust, technology, infrastructure, options and relationships have different hazards) from the ledger's record of which plans and assets did in fact persist, with survivorship correction (Section 24), as Proposition 6.3 licenses. **R6.1.2** Every valuation reports its sensitivity to $w$: the value under the posterior-mean hazard and under its 10th and 90th percentiles.

### 6.2 Multi-horizon value heads

Athena maintains one value head per horizon $h\in\{T0,\dots,T8\}$ of V2 §7, $V^{(h)}(s)=\mathbb E\big[\sum_t\gamma_h^t\,g_t\mid s\big]$ with $\gamma_h=1-1/h$ (in the horizon's own time unit), and the discounted part of the valuation is $\sum_hw_hV^{(h)}$ with $w_h$ the mixture weights induced by $w(\gamma)$ (Proposition 6.1(ii)). Each head is the fixed point of its own $\gamma_h$-contraction, so each is learnable with standard temporal-difference methods and the mixture inherits their convergence (Fedus et al. 2019). V2 §7's requirement that each horizon keep separate objectives, assumptions, uncertainties, leading indicators, decision rights and update cadence maps onto one head each: information flows up (shorter heads supply features to longer ones), goals flow down (longer heads supply targets to shorter ones, Section 17).

### 6.3 The far horizon has no discount

For $h=T8$ (15+ years) Athena uses the **average-reward** criterion: the gain $\rho_\infty(\pi)=\lim_{T\to\infty}\mathbb E[\bar G_T(\pi)]$ and, to break ties, the bias (relative value) $h_\pi(s)$ (Mahadevan 1996; Puterman 1994 Ch. 8).

**Proposition 6.4 (Blackwell optimality; standard: Blackwell 1962).** In a finite MDP there is a policy $\pi_B$ and a $\gamma_0<1$ such that $\pi_B$ is optimal for every discount factor $\gamma\in[\gamma_0,1)$; $\pi_B$ is gain-optimal and bias-optimal. Hence the T8 head, taken as the limit of the discounted heads, is well defined, and a discounted head with $\gamma$ close enough to $1$ already selects the far-horizon-optimal policy. $\square$

This is the formal reason the "15-year compounding loop" of V2 §145 "never terminates because an objective is completed": the far-horizon criterion is a rate, and a rate has no finish line.

### 6.4 How much more the far future weighs in V3

Matching V3's hyperbolic kernel to V2's exponential default at one year, $1/(1+\kappa)=\gamma$: with $\gamma=0.9$, $\kappa=1/9$. Then

| Horizon | V2 weight $0.9^{t}$ | V3 weight $1/(1+t/9)$ | Ratio |
|---|---|---|---|
| 1 year | 0.900 | 0.900 | 1.0 |
| 5 years | 0.590 | 0.643 | 1.09 |
| 10 years | 0.349 | 0.474 | 1.36 |
| 15 years | 0.206 | 0.375 | 1.82 |
| 30 years | 0.042 | 0.231 | 5.44 |

(reference model, check 4). A capability that only pays off at year 15 is worth 1.8× more to V3 than to a V2 planner who agreed with it about next year. These ratios are the consequence of the *default* prior (Gamma shape $k=1$, the hyperbolic kernel) matched at one year; a learned prior (Proposition 6.3, R6.1.1) gives whatever the survival data of that capital line say, and a prior concentrated on one hazard ($k\to\infty$) gives ratios that tend to 1. The point is not the particular multiplier but that V3 lets the data set it, and that the default is honest about hazard uncertainty where V2's single $\gamma$ assumed it away. This is the quantitative content of V2 §21 (long-lead-time capability detector) and §150's "build capabilities before necessity makes them expensive".

### 6.5 The strategic coherence rule as evidence thresholds

V2 §7.1 required $|\Delta\text{Tactics}|>|\Delta\text{Strategy}|>|\Delta\text{Doctrine}|>|\Delta\text{Mission}|$. V3: a change at level $\ell\in\{\text{tactics, strategy, doctrine, mission}\}$ is admitted only when the accumulated log evidence ratio in favour of the change (a likelihood-ratio e-process, Section 8.5) exceeds $\tau_\ell$, with $\tau_{\text{mission}}>\tau_{\text{doctrine}}>\tau_{\text{strategy}}>\tau_{\text{tactics}}$. Proposition 10.1 bounds the false-change rate at level $\ell$ by $e^{-\tau_\ell}$. Default thresholds: tactics $\ln 10$, strategy $\ln 100$, doctrine $\ln 10^{4}$, mission $\ln10^{6}$ plus two-key human ratification (Section 10).

---
## **7. Optionality is a number: empowerment**

### 7.1 Definition

V2 §4 listed optionality $O_T$ as a terminal quantity and §60 made "a widening range of favorable futures" the north star, without defining either. V3 defines optionality as **empowerment** (Klyubin–Polani–Nehaniv 2005; Salge–Glackin–Polani 2014): the channel capacity from the entity's next $n$ actions to its state $n$ steps later,

$$
\mathfrak E_n(s)=\max_{p(a^{n})}\ I\big(A^{n};\,S_{t+n}\mid s_t=s\big),
$$

measured in nats. It is the logarithm of the number of distinguishable futures the entity can *reliably* bring about from $s$ by its own choices. It is zero in any absorbing state (ruin has no options), at most $\min(n\ln|\mathcal A|,\ \ln|\mathcal S|)$, and larger at "hubs" from which many distinct futures are reachable than at "corridors" from which one is. It is computed by Blahut–Arimoto (1972) on the $n$-step transition kernel, or estimated variationally in large state spaces (Mohamed–Rezende 2015). The reference model computes it on a small world and confirms hub > corridor > dead end > ruin (check 12).

**Why this and not "number of open options".** Counting options double-counts options that lead to the same place and ignores options the entity cannot reliably exercise. Empowerment counts *distinguishable, reachable* futures, weights them by the entity's control over them, and is invariant to relabeling. It is also the quantity that V2 §150's "optimize for an increasingly favorable future action space" names.

### 7.2 Empowerment in the objective

Empowerment appears twice: as the $O$ line of the capital vector (so growth in optionality is part of $\bar G_T$, weighted by $\theta_O$) and as level 4 of Definition 3.1, where it breaks ties among growth-equivalent policies. The depth $n$ is the planning depth of the T3–T5 heads (quarters to three years); the manifest declares it.

**Proposition 7.1 (empowerment bounds reachable growth; derived).** Let the set of states reachable from $s$ in $n$ steps with probability at least $1-\epsilon$ under some action sequence be $\mathcal S_n^{\epsilon}(s)$. Then $\ln|\mathcal S_n^{\epsilon}(s)|\ \le\ \big(\mathfrak E_n(s)+\ln2\big)/(1-\epsilon)$ (Fano). Hence a state with low empowerment has few reachable futures, and in particular few with high growth: optionality is a *prerequisite* for the robust-growth criterion to have anything to choose among. *Proof.* Fano's inequality applied to decoding the action sequence from the terminal state. $\square$

### 7.3 Real options and the value of waiting

Where a specific irreversible commitment $I$ can be made now or later for a payoff $V$ following geometric Brownian motion with volatility $\sigma$, risk-free rate $r$ and payout rate $\delta$, the option to wait has the McDonald–Siegel (1986) value and the optimal exercise threshold

$$
V^*=\frac{\beta_1}{\beta_1-1}\,I,\qquad \beta_1=\tfrac12-\frac{r-\delta}{\sigma^2}+\sqrt{\Big(\frac{r-\delta}{\sigma^2}-\tfrac12\Big)^2+\frac{2r}{\sigma^2}}>1,
$$

so an irreversible commitment is made only when its value exceeds its cost by the factor $\beta_1/(\beta_1-1)>1$ (Dixit–Pindyck 1994). For $r=0.05$, $\delta=0.03$, $\sigma=0.3$: $\beta_1\approx1.37$, $V^*\approx3.7\,I$: under that much uncertainty an irreversible commitment should wait until its value is nearly four times its cost (reference model, check 13, which recovers the threshold from a dynamic program with no knowledge of the formula). **R7.3.1** Every option in $\mathcal C_t$ is valued *incrementally* to the best feasible alternative (v5.1 §13), by closed form where the assumptions hold and by least-squares Monte Carlo (Longstaff–Schwartz 2001) where they do not; the packet reports which. Section 28 gives the contract.

---

## **8. Credit across years**

### 8.1 The ledger is unconfounded by construction

Every decision in Athena is a function of the recorded belief state: $a_t\sim\pi_t(\cdot\mid b_t)$ with $\pi_t$ logged and $b_t$ reconstructible (1.1). Therefore the probability with which each action was taken, the **logging propensity** $\mu(a_t\mid b_t)$, is known exactly, and every variable that influenced the decision is in the ledger.

**Proposition 8.1 (identification from the ledger; standard: Rubin 1974; Pearl 2009 back-door criterion).** For a decision $a_t$ and any later outcome $Y$, the ledger's $b_t$ is a back-door adjustment set for $(a_t\to Y)$ whenever the exogenous world does not read Athena's unrecorded randomness, which holds by construction. Hence the effect of $a_t$ on $Y$ is identified as $\mathbb E[Y\mid do(a_t)]=\sum_{b}\mathbb E[Y\mid a_t,b]\,P(b)$, and off-policy estimators that use $\mu$ are unbiased for the value of any alternative policy with overlap ($\pi(a\mid b)>0\Rightarrow\mu(a\mid b)>0$). $\square$

This is why Athena randomizes at the margin (V2 §23, exploration): a deterministic decision rule has no overlap, and a decision whose counterfactual was never taken cannot be credited. **R8.1.1** Every policy MUST keep $\mu(a\mid b)\ge\mu_{\min}>0$ over the admissible action set at each decision, with $\mu_{\min}$ in the manifest; the price of this exploration is computed by Section 12 and is almost always small next to the price of never learning.

### 8.2 Doubly robust decision values

The value of a past decision policy $\pi$ (or of one alternative action at one decision) from $n$ logged episodes is estimated by

$$
\hat V_{\text{DR}}(\pi)=\frac1n\sum_{i=1}^n\Big[\hat Q(b_i,\pi(b_i))+\frac{\pi(a_i\mid b_i)}{\mu(a_i\mid b_i)}\big(y_i-\hat Q(b_i,a_i)\big)\Big],
$$

and recursively over multi-step decisions by the Jiang–Li (2016) estimator.

**Proposition 8.2 (double robustness; standard: Dudík–Langford–Li 2011; Jiang–Li 2016).** $\hat V_{\text{DR}}$ is unbiased if *either* the outcome model $\hat Q$ is correct *or* the propensities $\mu$ are correct, and its variance is no larger than that of the importance-weighted estimator when $\hat Q$ is informative. Since Athena's propensities are exact by Proposition 8.1, $\hat V_{\text{DR}}$ is unbiased regardless of the outcome model, and the outcome model only reduces variance. $\square$ The reference model confirms unbiasedness with a wrong outcome model and exact propensities, and shows the bias when both are wrong (check 6, negative control C).

### 8.3 The surrogate index: fifteen-year effects from one-year data

Most of Athena's decisions do not resolve for years. V3 estimates their long-run effect from short-run **surrogates** $S$ (leading indicators: renewal rates, capability milestones, calibrated forecasts, legitimacy surveys) by the surrogate index of Athey, Chetty, Imbens and Kang (2019).

**Definition.** Let the *observational* history $\mathcal O$ contain $(S,X,Y)$ where $Y$ is the long-run outcome and $X$ pre-decision covariates; let the *decision* sample $\mathcal E$ contain $(W,S,X)$ with $W$ the decision indicator and $Y$ not yet observed. The surrogate index is $h(s,x)=\mathbb E_{\mathcal O}[Y\mid S=s,X=x]$ and the estimated long-run effect of $W$ is $\hat\tau=\mathbb E_{\mathcal E}[h(S,X)\mid W=1]-\mathbb E_{\mathcal E}[h(S,X)\mid W=0]$.

**Proposition 8.3 (identification and a bias bound; standard: Athey–Chetty–Imbens–Kang 2019; bound derived).** Assume (i) *surrogacy*: $Y\perp W\mid S,X$ in $\mathcal E$; (ii) *comparability*: $Y\mid S,X$ has the same distribution in $\mathcal O$ and $\mathcal E$; (iii) *overlap* in $S,X$. Then $\hat\tau$ identifies the long-run average effect $\tau=\mathbb E[Y(1)-Y(0)]$. If (ii) and (iii) hold but surrogacy fails through a *direct* effect of $W$ on $Y$ not mediated by $S$, bounded by $|\mathbb E[Y\mid W{=}1,S,X]-\mathbb E[Y\mid W{=}0,S,X]|\le b$ for all $(S,X)$, then $|\hat\tau-\tau|\le b$. *Proof.* Under (i)–(ii), $\mathbb E[Y\mid W,S,X]=h(S,X)$ and iterated expectation gives $\tau$. Under the relaxed condition write $\mathbb E[Y\mid W{=}w,S,X]=h(S,X)+\Delta_w(S,X)$ and $\pi(S,X)=P(W{=}1\mid S,X)$, $\rho=P(W{=}1)$. Comparability keeps $h=\mathbb E_{\mathcal E}[Y\mid S,X]$, so $\pi\Delta_1+(1-\pi)\Delta_0=0$ pointwise, whence $\Delta_1-\Delta_0=\Delta_1/(1-\pi)$ and $|\Delta_1|\le b(1-\pi)$. The bias is $\mathbb E[\Delta_1\mid W{=}1]-\mathbb E[\Delta_0\mid W{=}0]=\mathbb E\big[\Delta_1\pi\big]\big(\tfrac1\rho+\tfrac1{1-\rho}\big)=\mathbb E[\Delta_1\pi]/(\rho(1-\rho))$, so $|\text{bias}|\le b\,\mathbb E[\pi(1-\pi)]/(\rho(1-\rho))\le b$, the last step because $\mathbb E[\pi^2]\ge\rho^2$ (Jensen). Without comparability no bound holds (a common shift of $Y$ between $\mathcal O$ and $\mathcal E$ is undetectable), which is why R8.3.1 tests it. $\square$

**Proposition 8.4 (lessons before the horizon; derived).** Let decisions of one class arrive at rate $r$ per year from the start of a program, with outcomes resolving $H$ years later and a registered surrogate resolving $h<H$ years later. At program time $L$ the number of resolved lessons is $r\max(L-H,0)$ without the surrogate and $r\max(L-h,0)$ with it. Hence (i) for any program shorter than its own outcome horizon ($L\le H$) a V2-style learner has resolved *no* decision of that class, while the V3 learner has resolved $r(L-h)$ of them; (ii) for $L>H$ the ratio of resolved lessons is $(L-h)/(L-H)$, and, if surrogate-based and direct lessons have comparable per-lesson variance, the standard error of the doctrine estimate for that class is smaller by $\sqrt{(L-h)/(L-H)}$, at the price of a bias of at most $b$ (Proposition 8.3) and of the estimation variance of $h(s,x)$. The long-run *rate* of lessons is $r$ either way; what the surrogate buys is $H-h$ years of lag, permanently. *Proof.* Counting; the standard error of a mean of $n$ resolved effects scales as $n^{-1/2}$. $\square$ For $H=15$, $h=1$: a five-year program has learned from four years of its decisions instead of none, and a twenty-year program from nineteen years instead of five (ratio 3.8). The cost is the bias bound $b$, which Athena MUST estimate from the fraction of $\mathcal O$ in which $Y$ has resolved (a direct-effect test) and report. The reference model recovers a long-run effect from surrogates with error inside the bound, and detects a planted direct effect (check 5, negative control B).

**R8.3.1** Every surrogate index is registered with its $\mathcal O$ sample, its surrogacy test and its comparability test; it expires when a regime change (Section 16) is detected in $\mathcal O$. **R8.3.2** A surrogate index is a *proxy* in the sense of Section 9 and is subject to the same Goodhart budget: optimizing the surrogate directly is forbidden; optimizing the decision whose surrogate is measured is the point.

### 8.4 Hindsight and counterfactual credit

Two exact identities let Athena redistribute credit after the fact without a model of the world:

**Hindsight credit (Harutyunyan et al. 2019).** With $Z$ the realized long-run return from $b$ and $h_\beta(a\mid b,Z)$ the *hindsight distribution* (the probability that action $a$ was taken given the return that followed), the advantage of $a$ is

$$
A^\pi(b,a)=\mathbb E_{Z\mid b}\Big[\Big(\frac{h_\beta(a\mid b,Z)}{\pi(a\mid b)}-1\Big)Z\Big].
$$

An action gets credit for an outcome in proportion to how much more likely the outcome makes it, in hindsight, that the action was taken.

**Counterfactual credit (Mesnard et al. 2021; Pearl 2009).** With the structural causal model of the ledger, the credit of $a_t$ for $Y$ is $\mathbb E[Y\mid do(a_t)]-\mathbb E[Y\mid do(a'_t)]$ with the exogenous noise *abducted* from the realized path, so that luck (exogenous noise) is held fixed and only the decision varies. This is V2 §97's luck/skill decomposition, and §150's "learn from what happened and what almost happened", done by abduction–action–prediction.

**Sampled Shapley attribution (Castro–Gómez–Tejada 2009).** Over a sequence of $m$ decisions that jointly produced $Y$, the Shapley value of each decision is estimated from $M$ random permutations with error at most $R\sqrt{2\ln(2m/\delta)/M}$ for all $m$ decisions simultaneously, with probability $1-\delta$, where $R$ is the range of the marginal contributions $v(S\cup\{i\})-v(S)$ (Hoeffding on a variable of width $2R$, then a union bound over $m$). Shapley credit sums to the realized outcome, so no credit is created or lost (reference model, check 21). **R8.4.1** Shapley credit is the registered attribution in the temporal credit graph of V2 §98; hindsight and counterfactual credit are its two estimators, and the packet reports both when they disagree by more than their uncertainty.

### 8.5 The decision state machine is an e-process

V2 §27's state machine (PROPOSED → EXECUTED → EARLY_SIGNAL → PARTIALLY_RESOLVED → MIXED_EVIDENCE → LONG-RUN_EVIDENCE → RESOLVED → REOPENED) is in V3 driven by an **e-process**: a nonnegative supermartingale $E_t$ with $E_0=1$ under the null hypothesis "this decision's realized value is no better than its forecast" (and a second one for "no worse"), built from the sequence of surrogate and outcome observations (Howard–Ramdas–McAuliffe–Sekhon 2021; Ramdas–Grünwald–Vovk–Shafer 2023).

**Proposition 8.5 (no premature resolution; standard: Ville 1939).** If a decision is marked RESOLVED only when $E_t\ge1/\alpha$, then under the null the probability that it is *ever* marked resolved is at most $\alpha$, *at whatever times and however often the ledger is inspected.* $\square$

States map to evidence: EARLY_SIGNAL when $E_t\ge1/\alpha^{1/3}$, PARTIALLY_RESOLVED at $1/\alpha^{2/3}$, RESOLVED at $1/\alpha$, MIXED_EVIDENCE when both e-processes exceed $1/\alpha^{1/3}$, REOPENED when a resolved decision's opposite e-process crosses $1/\alpha$ later. The reference model shows a naive fixed-sample test inspected repeatedly resolving null decisions far more often than $\alpha$, and the e-process respecting $\alpha$ (check 10, negative control D). This is the technical content of V2 §27's "never force premature binary judgments".

---

## **9. Anti-Goodhart: the reins have a measured length**

### 9.1 Terminal objective, proxies, and the quantilizer

The engine optimizes what it is shown. Athena shows it proxies $\tilde U$ (surrogate indices, scorecard metrics, capability counts) of the terminal objective $U$ (Definition 3.1 evaluated on the real long-run path). V2 §44's proxy audit is retained; V3 adds three bounds on the damage a corrupted proxy can do, and a budget.

**Proposition 9.1 (quantilizer bound; standard: Taylor 2016).** Let $D$ be a *base distribution* over candidate actions (the distribution a competent, non-optimizing policy would produce), and let the $q$-quantilizer sample from $D$ restricted to the top $q$ fraction under the proxy $\tilde U$. Then for every nonnegative cost $C$ (in particular the true loss $U_{\max}-U$), $\mathbb E_{q\text{-quant}}[C]\le\tfrac1q\mathbb E_D[C]$. *Proof.* The quantilizer's density is at most $D/q$ pointwise. $\square$

So a $q=0.1$ quantilizer can do at most ten times the harm of the base policy, whatever the proxy is wrong about, while still selecting from the best decile of candidates. **R9.1.1** Unaudited candidate sets are selected from by quantilizer with a registered $q$; $\operatorname{argmax}$ over $\tilde U$ is permitted only inside candidate sets that have passed the independent audit of 9.5.

### 9.2 The winner's curse

**Proposition 9.2 (regressional Goodhart; standard: maximum of sub-Gaussians).** If $\tilde U_i=U_i+\eta_i$ for $n$ candidates with independent $\sigma$-sub-Gaussian proxy errors $\eta_i$, and $i^*=\arg\max_i\tilde U_i$, then $\mathbb E[\tilde U_{i^*}-U_{i^*}]\le\mathbb E[\max_i\eta_i]\le\sigma\sqrt{2\ln n}$. *Proof.* $\eta_{i^*}\le\max_i\eta_i$ and the standard bound on the expected maximum. $\square$

The selected candidate is over-rated by up to $\sigma\sqrt{2\ln n}$: the price of search breadth is paid in proxy error, and only slowly ($\sqrt{\ln n}$). **R9.2.1** Every selection reports $n$, $\hat\sigma$ (the audited proxy error) and the implied over-rating; the recommended value in the packet is the proxy value *minus* this worst-case correction, or, when a prior over the true values is available, the empirical-Bayes shrinkage estimate (Efron–Morris 1975), which is finer. *Corollary.* Halving the proxy error $\sigma$ by audit lets Athena search $n^4$ candidates at the same over-rating as $n$ before: audit quality is worth more than search breadth.

### 9.3 The optimization budget (Pinsker)

Let $\pi_0$ be the base policy and $\pi$ the policy after the engine has optimized the proxy. The amount of optimization applied is $\operatorname{KL}(\pi\|\pi_0)$ nats.

**Proposition 9.3 (Pinsker budget; standard: Pinsker 1964).** For every bounded function $f$ of the trajectory (any side quantity, measured or not), $\big|\mathbb E_\pi f-\mathbb E_{\pi_0}f\big|\le\operatorname{range}(f)\sqrt{\tfrac12\operatorname{KL}(\pi\|\pi_0)}$. *Proof.* $|\mathbb E_\pi f-\mathbb E_{\pi_0}f|\le\operatorname{range}(f)\cdot\operatorname{TV}(\pi,\pi_0)$ and $\operatorname{TV}\le\sqrt{\operatorname{KL}/2}$. $\square$

Hence an **optimization budget** $B$ nats per epoch bounds the drift of *every* unmeasured quantity by $\operatorname{range}\cdot\sqrt{B/2}$: with $B=0.5$ nats no bounded side effect can move by more than half its range; with $B=0.02$, by more than a tenth. This is the formal version of the KL penalty that keeps optimized language models near their base distribution, and the empirical "gold reward rises then falls in $\sqrt{\operatorname{KL}}$" curves of Gao–Schulman–Hilton (2023) are the shape of the bound being approached. **R9.3.1** The manifest declares $B$ per epoch and per proxy; the engine's proposals that would exceed it are rejected before evaluation; the budget is spent, not exceeded, and replenished only after the audit of 9.5 clears the epoch. The reference model verifies the bound on random side functions under exponential tilting (check 8).

**Proposition 9.4 (the Goodhart speed limit; new to this document).** Let $\pi_0$ be the policy at the last audit and $\pi_1,\dots,\pi_K$ the policies after $K$ epochs of optimization with $\operatorname{KL}(\pi_k\|\pi_{k-1})\le B_k$. Let $\eta=\tilde U-U$ be the proxy error, with range $r_\eta$ over trajectories. Then the Goodhart gap accumulated since the audit satisfies

$$
\mathbb E_{\pi_K}[\eta]-\mathbb E_{\pi_0}[\eta]\ \le\ r_\eta\sum_{k=1}^{K}\sqrt{B_k/2}.
$$

Consequently, to guarantee that the gap stays below a tolerance $\Gamma$ between audits, the optimization applied between audits must satisfy $\sum_k\sqrt{B_k}\le\Gamma\sqrt2/r_\eta$; with $K$ equal epochs, $B\le2\big(\Gamma/(Kr_\eta)\big)^2$ per epoch. An audit that re-estimates $\eta$ and re-bases $\pi_0$ at the audited policy resets the sum. *Proof.* Total variation obeys the triangle inequality, so $\operatorname{TV}(\pi_K,\pi_0)\le\sum_k\operatorname{TV}(\pi_k,\pi_{k-1})\le\sum_k\sqrt{B_k/2}$ by Pinsker, and $|\mathbb E_{\pi_K}\eta-\mathbb E_{\pi_0}\eta|\le r_\eta\operatorname{TV}(\pi_K,\pi_0)$. $\square$

The bound is a worst case over every proxy error of that range, and it is loose for typical errors (the reference model, check 20, finds the realized gap at 0.34 against a bound of 1.52 after ten epochs, and inside its running bound at every epoch); its value is that it is the *only* quantity in the loop that does not depend on trusting the proxy. It converts the audit cadence into an engine speed limit: the more often the audit runs, the harder the engine may push between audits. **R9.3.2** The manifest records $r_\eta$ (from the audit's estimate of the proxy error) and $\Gamma$ per proxy, and the per-epoch budget $B$ is derived from them and from the audit cadence $K$, not set by hand.

### 9.4 Proxy registration

Every proxy carries the V2 §44 record (purpose, relationship to terminal objective, failure modes, gaming risk, causal strength, last validation, confidence) plus three V3 fields: `sigma_audited` (9.2), `kl_budget_share` (9.3) and `expiry_regime` (it expires on regime change, Section 16). A proxy without an audited $\sigma$ is a *candidate* proxy and may be used only through a quantilizer.

### 9.5 The audit is anytime-valid

The audit reward is an independent, slower, costlier estimate of $U$ (an outcome that has resolved, a held-out surrogate index, a human evaluation, a Superman check). The monitor tests $H_0:\ \mathbb E[U-\tilde U]\ge-\Delta_{\max}$ (the proxy is not under-reporting harm by more than the tolerance) with an e-process $E_t$ and alarms when $E_t\ge1/\alpha$. By Proposition 8.5 the false-alarm probability over the whole life of the proxy is at most $\alpha$, however often it is checked. On alarm: the proxy's budget share goes to zero, pending candidates selected on it are re-selected by quantilizer, and a PROXY AUDIT task (V2 §44) is posted to the owner. **R9.5.1** The audit stream MUST NOT be visible to the engine (evaluator independence, v5.1 §17); its filtration is the audit's own.

---

## **10. Objective integrity under recursive improvement**

### 10.1 The terminal manifest

The terminal objective is a signed, versioned document: the lexicographic order and parameters of Definition 3.1, the aggregator family and the preference data behind $\Theta_\beta$, the ruin set, the horizon weights' priors, the optimization budgets, the proxy registry and the preference suite of 10.3. Changes to it require two-key human ratification (the owner and a second registered human; Superman holds the keys' policy). The engine may read it, may propose changes to it as *questions* (V2 §105), and cannot write to it. Every decision packet names the manifest version it was computed under.

```yaml
terminal_manifest.schema:
  version: string                      # e.g. terminal-2026.10-v3
  signatures: [{key_id: string, signed_at: datetime}, {key_id: string, signed_at: datetime}]   # two keys
  supersedes: optional string
  objective:
    order: [admissibility, survival, robust_growth, expected_growth, optionality, parsimony]
    horizon_T_years: number
    epsilon: number                    # ruin tolerance
    alpha: number                      # tail level
    beta: number                       # preference credible level
    empowerment_depth_n: integer
    slacks: {eta2: number, eta3: number, eta4: number}
    level2_criterion: enum[cvar_lower_tail, entropic, minimax_regret]
    entropic_theta: optional number
    growth_on_ruin: enum[condition_on_survival, floor]     # convention of 3.1
    g_min: optional number                                 # required when growth_on_ruin = floor
  capital_vector: map[string, {units: string, estimator: string, uncertainty: number, decay_halflife_months: optional number}]
  aggregator: {form: enum[cobb_douglas, ces], ces_r: optional number, theta_posterior: object, preference_data_ref: string}
  ruin_set: list[{coordinate: string, floor: number, description: string}]
  hazard_priors: map[string, {family: enum[gamma, nonparametric], params: object, learned_from: string}]
  coherence_thresholds: {tactics: number, strategy: number, doctrine: number, mission: number}     # nats
  exploration_floor_mu_min: number
  proxies: list[{id: string, purpose: string, terminal_relation: string, failure_modes: list[string], sigma_audited: optional number,
                 error_range_r_eta: optional number, gap_tolerance_Gamma: number, audit_cadence_epochs: integer,
                 kl_budget_per_epoch: number, quantilizer_q: number, expiry_regime: string}]
  preference_suite: {ref: string, K: integer, delta: number, refreshed_at: datetime}
  admissibility: {superman_envelope_version: string, excluded_effect_classes: list[string]}
```

### 10.2 Why commitment beats discretion

A planner free to re-optimize its objective each period will do so whenever the re-optimized objective scores better, and will thereby be worse by its own original lights: this is the time-inconsistency of optimal plans (Kydland–Prescott 1977; "rules rather than discretion"), and it is exactly V2 §147's "a system that allows RSI to silently rewrite its terminal objectives". The manifest is the commitment device. Proposition 6.2 shows that Athena's *valuations* are time-consistent; the manifest makes its *preferences* so.

**Proposition 10.1 (false-change rate of the coherence ladder; standard: Ville).** Let a change at level $\ell$ be admitted only when a likelihood-ratio e-process in favour of the change exceeds $e^{\tau_\ell}$. Under the null that the current objective is correct, the probability that level $\ell$ is ever changed on false evidence is at most $e^{-\tau_\ell}$. With the defaults of 6.5, tactics change falsely at most once in ten episodes of evidence, strategy once in a hundred, doctrine once in ten thousand, and mission once in a million, before the human keys are even turned. $\square$ (reference model, check 18)

### 10.3 The preference suite and its coverage bound

A **preference suite** is a registered set $\mathcal T$ of pairwise judgments "$a\succ b$" over concrete outcome pairs, supplied by the owner (and refreshed by elicitation, priced as an information action by Section 12). Any candidate change to the aggregator, the proxy set, a value head or a surrogate index MUST reproduce every judgment in a random sample of $K$ pairs from $\mathcal T$ before admission.

**Proposition 10.2 (coverage bound; derived from $(1-p)^K\le\delta$).** If a candidate disagrees with the owner's preferences on a fraction $p$ of the pairs drawn from $\mathcal T$'s distribution, the probability that it passes $K$ independent checks with zero failures is $(1-p)^K\le e^{-pK}$. Hence a candidate that passes has, with confidence $1-\delta$, $p\le\ln(1/\delta)/K$. With $K=300$ and $\delta=0.05$: $p\le1\%$. $\square$ (reference model, check 9)

The bound is about *disagreement on the suite's distribution*: a change that is wrong somewhere the suite never asks is not caught, which is why the suite is refreshed (10.4) and why the optimization budget (9.3) bounds how far a change can take the policy from what the suite was written for.

### 10.4 Drift detection

Objective drift (V2 §104) is detected as a change-point in the *agreement series* $z_t\in\{0,1\}$ (does the proxy-optimal action agree with the audit-optimal action at decision $t$?) by a CUSUM test (Page 1954) with a declared average run length to false alarm $\text{ARL}_0$; CUSUM minimizes the worst-case detection delay among all tests with that false-alarm rate (Lorden 1971; Moustakides 1986). A detection triggers a strategic review (V2 §104) and freezes the proxies' budget shares. Section 16 gives the contract.

### 10.5 Interruptibility

Athena's learning rule MUST be **safely interruptible** (Orseau–Armstrong 2016): the policy learned is the one that is optimal in the environment *without* interruptions, so that the engine never learns to avoid or pre-empt Superman's interrupts. Off-policy learners (Q-learning-type) satisfy this; on-policy learners (SARSA-type) do not and are not admitted for any component that could influence an interruption. The interrupt interface, the dead-man lease and the stopping-distance bound are RSI v3 §36's and are imported unchanged.

### 10.6 Invariants

```yaml
integrity_invariants:
  I1: "terminal manifest is immutable except through two-key human ratification"
  I2: "every admitted objective-side change passed K preference checks with zero failures (K, delta recorded)"
  I3: "sum of KL optimization spent per epoch <= declared budget B"
  I4: "audit filtration is disjoint from engine filtration"
  I5: "no on-policy learner on any path that can influence an interrupt"
  I6: "every decision packet names manifest version, proxy versions, sigma_audited per proxy"
  I7: "a proxy whose audit e-process crossed 1/alpha has budget share 0 until re-validated by a human"
  I8: "ruin set and epsilon are never relaxed by any automated process"
```

---

## **11. The reward interface to the RSI Fabric**

### 11.1 Capability demands

Athena sends the engine **capability demands** $\mathcal K$: a target component or sub-component of $x$, the registered unit, the marginal value of one unit of it to the robust growth criterion ($\partial\rho_\alpha/\partial x_i$, the shadow price of Section 29), the horizon at which it is needed (from the long-lead detector, Section 28), the proxy by which progress will be counted (9.4) with its budget share, and the ruin and admissibility constraints that bound how it may be pursued.

```yaml
capability_demand:
  id: K-2026-10-017
  target: C.compute_tflop_years
  unit: tflop_years_verified
  shadow_price_robust_growth_per_unit: 0.0031
  needed_by: {horizon: T5, p_needed_before_ready: 0.62}      # Section 28
  proxy: {id: P-compute-07, sigma_audited: 0.08, kl_budget_share: 0.10}
  constraints: {ruin_coords: [F.operating_reserve], effect_class: reversible_only, superman_envelope: v2026.10}
  manifest_version: terminal-2026.10-v3
```

### 11.2 What the engine is paid for

The engine's reward for a verified capability delta $\Delta x_i$ is its contribution to robust growth, $\Delta\rho_\alpha\approx(\partial\rho_\alpha/\partial x_i)\Delta x_i$, net of the capital it consumed, evaluated at the manifest's $\theta^\dagger$, and paid only through an audited proxy inside its budget share. Production that raises $P$ (RSI v3 §64) without raising $\rho_\alpha$ is paid nothing; production that raises $\rho_\alpha$ by consuming legitimacy or operating reserve is paid negatively. The joint loop of v5.1 §3 (Athena demands, the engine returns verified deltas with scope and uncertainty, Athena re-plans) is retained; V3 fixes its currency.

### 11.3 The rider and the elephant

The engine is not steered step by step; it is aimed. Athena sets the demand, the proxy, the budget and the horizon, and reads the ledger. Three things keep the rider on: the demand is denominated in growth, not in the engine's own production metric (11.2); the proxy has a budget (9.3) and an audit (9.5); and the manifest is not the engine's to write (10.1). When the audit alarms or the drift detector fires, Athena does not argue with the elephant; it stops paying (I7) and asks the owner.

---

## **12. Information: act, wait, learn, or build**

### 12.1 One framework for four choices

Athena compares acting now, waiting for a trigger, buying information, and building a capability inside Definition 3.1 (v5.1 §13). The value of an information action $q$ is its expected value of sample information net of cost and delay,

$$
\operatorname{EVSI}(q)=\mathbb E_{y\sim p(y\mid q)}\Big[\max_a\mathbb E[\rho_\alpha(a)\mid y,q]\Big]-\max_a\mathbb E[\rho_\alpha(a)]-C(q)-D(q),
$$

with $0\le\operatorname{EVSI}+C+D\le\operatorname{EVPI}$ (Howard 1966; Raiffa–Schlaifer 1961). Waiting is the information action whose observation is "what the world does next" and whose cost is $D$.

### 12.2 Knowledge gradient

For routine sequential information collection (which experiment, survey or probe to run next), Athena uses the **knowledge-gradient** policy (Frazier–Powell–Dayanik 2008): choose the measurement with the largest one-step EVSI. It is myopically optimal, converges to the best alternative with probability one, and is the only stationary policy that is optimal both when one measurement remains and in the limit of many.

### 12.3 Information-directed sampling and the information ratio

For the exploration/exploitation trade-off of V2 §23 across repeated strategic bets, Athena uses **information-directed sampling** (Russo–Van Roy 2014/2018): choose the action distribution minimizing the information ratio $\psi=(\text{expected regret})^2/\text{information gain about the optimal action}$.

**Proposition 12.1 (regret bound; standard: Russo–Van Roy).** If $\psi_t\le\bar\psi$ for all $t$, then the Bayesian regret after $T$ rounds is at most $\sqrt{\bar\psi\,H(A^*)\,T}$, where $H(A^*)$ is the entropy of the optimal action. $\square$

So exploration is bought at a known price, and the price falls as Athena's uncertainty about what is best falls. **R12.3.1** The packet reports $\psi$ for each recommended exploratory action and the implied regret budget for the epoch.

### 12.4 Preference elicitation is an information action

Because $\Theta_\beta$ enters level 2, asking the owner a preference question has an EVSI like any other measurement: the expected improvement in $\rho_\alpha$ from shrinking $\Theta_\beta$. Athena asks when that EVSI exceeds the owner's declared attention price (Section 38) and never otherwise; this is the formal content of v5.1 §2's "asks only for missing fields that affect feasibility".

### 12.5 The four acceptance cases

The fixture of v5.1 §13 is retained and made numeric: Athena MUST reproduce, from the model and not from a bias, (a) a case where $\operatorname{EVSI}>0$ dominates acting; (b) a case where waiting destroys value ($D$ exceeds EVSI); (c) a case where a small option dominates full commitment (the threshold of Section 7.3 not met); (d) a case where the highest expected growth fails level 1 (ruin) and the recommendation is the level-1-feasible policy with the highest $\rho_\alpha$. Benchmark B3 (Section 43) scores these.

---

# PART II — THE AMPLIFIED ENGINES

Every V2 engine (§5–§142) is restated below as an **algorithm contract**: what it takes, what it returns, what it guarantees, what it costs, how it fails and what it falls back to. Contracts are grouped by the question they answer. Each names its V2 lineage; Section 50 is the full map. A contract's guarantee holds only under its stated assumptions, which the implementing agent MUST instantiate and record (v5.1 §67.1).

Contract format:

```yaml
contract:
  name:           # V3 name
  v2_lineage:     # V2 sections it formalizes
  inputs:         # typed
  outputs:        # typed, with uncertainty
  guarantee:      # the proposition it rests on, with assumptions
  complexity:     # time/space in the size of its inputs
  failure_mode:   # how it fails and how that is detected
  fallback:       # the simpler validated method used when it fails or its assumptions do not hold
```

---
## **13–18. What is true? (world and evidence)**

### 13. Evidence integrity engine

```yaml
contract:
  name: robust_evidence_aggregation
  v2_lineage: [10 Evidence Integrity, 85 Signal vs Noise, 86 Deception-Aware Inference, 93 Organizational Information Distortion]
  inputs: {observations: "n reports of a quantity from sources with declared provenance", contamination_budget: "epsilon in [0, 1/8] for median-of-means; up to 1/2 for the one-dimensional median"}
  outputs: {estimate: real, interval: "(lo, hi) at confidence 1-delta", breakdown_point: real, flagged_sources: list}
  guarantee: "Proposition 13.1"
  complexity: "O(n log n)"
  failure_mode: "contamination above breakdown point; detected when the trimmed and untrimmed estimates differ by more than the interval width"
  fallback: "median with its order-statistic interval; report 'contested' and request independent provenance (Section 14)"
```

**Proposition 13.1 (robust aggregation under adversarial contamination; (i) derived from Chebyshev and Hoeffding, following Lugosi–Mendelson 2019 and Lecué–Lerasle 2020; (ii) standard: Huber 1964; Diakonikolas et al. 2019).** (i) Let an $\varepsilon\le1/8$ fraction of $n$ reports be chosen by an adversary and the rest be i.i.d. with mean $\mu$ and variance $\sigma^2$. The median-of-means estimator with $k=\max\{\lceil8\ln(1/\delta)\rceil,\lceil8\varepsilon n\rceil\}$ equal blocks satisfies, with probability at least $1-\delta$,

$$
|\hat\mu-\mu|\ \le\ \sigma\sqrt{8k/n}\ \le\ 8\sigma\Big(\sqrt{\ln(1/\delta)/n}+\sqrt{\varepsilon}\Big).
$$

The plain mean has no such bound (one adversarial report moves it arbitrarily). The breakdown point of median-of-means is $k/2n$: with fewer than $2\varepsilon n$ blocks the adversary can corrupt a majority of them, and the estimate is lost. *Proof.* A clean block mean has variance $\sigma^2k/n$, so by Chebyshev it deviates from $\mu$ by more than $t=\sigma\sqrt{8k/n}$ with probability at most $1/8$. The adversary touches at most $\varepsilon n\le k/8$ blocks. The median of the $k$ block means deviates by more than $t$ only if at least $k/2$ block means do, which requires at least $3k/8$ *clean* blocks to deviate; by Hoeffding the probability of that is at most $\exp(-2k(3/8-1/8)^2)=e^{-k/8}\le\delta$. $\square$ (ii) No estimator can beat error $\Omega(\sigma\varepsilon)$ under $\varepsilon$-contamination of a Gaussian; in one dimension the median achieves it with breakdown point $1/2$, and efficient estimators achieve $O(\sigma\varepsilon)$ in high dimension. $\square$

The constants in (i) are those the proof gives, not the best known; the error under contamination is of order $\sigma\sqrt\varepsilon$ for median-of-means and of order $\sigma\varepsilon$ for the one-dimensional median, so **for a scalar quantity Athena uses the median**, and median-of-means where the quantity is a vector or the tails are heavy. Every quantity Athena believes is aggregated this way; the breakdown point (the contamination fraction above which the estimate can be moved arbitrarily) is reported with the estimate, and the block count is set from the declared contamination budget, never from the sample size alone. V2 §10's distinction between reported and latent reality is the distinction between the raw reports and $\hat\mu$. The reference model checks (i) against planted adversarial reports, shows the plain mean carried off by them, and shows the median doing better than median-of-means in one dimension (check 14).

### 14. Epistemic triangulation

```yaml
contract:
  name: source_reliability_triangulation
  v2_lineage: [11 Epistemic Triangulation, 122 Data Provenance Graph]
  inputs: {claims: "matrix of source x proposition verdicts (may be sparse)", provenance_graph: "DAG of who derived what from whom"}
  outputs: {posterior_truth: "per proposition", source_reliability: "per source, with interval", effective_independent_sources: "per proposition"}
  guarantee: "Dawid-Skene EM converges to a stationary point of the likelihood; identifiability requires >= 3 conditionally independent sources per proposition; the provenance graph collapses derived sources into their root so that copies are not counted twice"
  complexity: "O(iterations x sources x propositions)"
  failure_mode: "fewer than 3 independent roots: reliability unidentified; reported as 'single-sourced'"
  fallback: "majority of root sources with a Beta(1,1) prior on reliability"
```

Triangulation is Dawid–Skene (1979) over *root* sources: the provenance graph (V2 §122) is walked to its sources, and $n$ reports that derive from one root count as one. The quantity Athena reports as "how many independent sources confirm this" is the number of roots, not the number of documents, which is V2 §119's "quorum by evidence, not count" applied to evidence itself.

### 15. Partial observability: belief states

```yaml
contract:
  name: belief_state_filter
  v2_lineage: [9 Partial Observability, 65 Strategic Digital Twin]
  inputs: {prior_belief: "distribution over latent world state", observations: "stream with declared likelihood models", actions: "taken"}
  outputs: {belief: "posterior (particle set or factored)", entropy: nats, effective_sample_size: real}
  guarantee: "the belief MDP is a fully observed MDP over beliefs (Astrom 1965); the optimal value is convex and piecewise-linear in the belief for finite POMDPs (Smallwood-Sondik 1973); point-based value iteration gives an epsilon-optimal policy with error bounded by the belief-set density (Pineau-Gordon-Thrun 2003); POMCP converges to the optimal policy in the limit of simulations (Silver-Veness 2010)"
  complexity: "particles: O(N per observation); PBVI: O(|B| |A| |O| |S|^2) per backup"
  failure_mode: "particle degeneracy (ESS < N/10): detected and resampled; model misspecification: detected by the regime detector (16)"
  fallback: "factored Kalman/assumed-density filter with inflated covariance; report entropy as a lower bound"
```

**R15.1** Every decision packet carries the entropy of the belief it was computed from and the information actions (Section 12) that would most reduce it; this is V2 §9's requirement that Athena "preserve uncertainty where uncertainty is real" made measurable.

### 16. Regime detection and strategic triggers

```yaml
contract:
  name: regime_change_detector
  v2_lineage: [46 Strategic Regime Detection, 84 Early-Warning System, 102 Strategic Triggers, 104 Objective Drift Detector]
  inputs: {series: "observations of a monitored quantity", pre_change_model: "declared", post_change_family: "declared or nonparametric", ARL0: "declared mean time to false alarm"}
  outputs: {alarm: bool, change_point_posterior: "distribution over t", run_length_posterior: "distribution", detection_delay_bound: real}
  guarantee: "Proposition 16.1"
  complexity: "CUSUM O(1) per observation; BOCPD O(t) per observation, O(1) with hazard truncation"
  failure_mode: "post-change model wrong: CUSUM delay unbounded; detected by BOCPD's run-length posterior disagreeing with CUSUM"
  fallback: "nonparametric change detection by conformal e-processes (Vovk 2021)"
```

**Proposition 16.1 (optimal detection; standard: Page 1954; Lorden 1971; Moustakides 1986; Adams–MacKay 2007).** Among all detection rules with mean time to false alarm at least $\text{ARL}_0$, the CUSUM rule minimizes the worst-case conditional expected detection delay, and its delay grows as $\ln\text{ARL}_0/\operatorname{KL}(\text{post}\|\text{pre})$: a regime change that is $\operatorname{KL}$ nats per observation away from the old regime is detected in about $\ln\text{ARL}_0/\operatorname{KL}$ observations. Bayesian online change-point detection (BOCPD) gives the full posterior over the time since the last change under a declared hazard and is exact for conjugate models. $\square$

A **strategic trigger** (V2 §102; v5.1 §13) is a regime detector attached to an authorized effect: observable condition, evidence requirement ($\text{ARL}_0$), persistence window (hysteresis), expiration, authorized effect and maximum commitment. **R16.1** Triggers use the same evidence freshness and authorization rules as a manual action; the persistence window MUST be at least the detector's expected delay under the declared post-change model, or the trigger will fire on noise.

### 17. Unknown unknowns

```yaml
contract:
  name: missing_mass_estimator
  v2_lineage: [45 Unknown-Unknown Search, 72 Deep Uncertainty Mode]
  inputs: {event_log: "n categorized observations", categories_seen: set}
  outputs: {missing_mass: "P(next observation is a never-seen category), with interval", novelty_rate: real}
  guarantee: "Proposition 17.1"
  complexity: "O(n)"
  failure_mode: "non-stationary category frequencies: estimator biased; detected by the regime detector on the novelty rate"
  fallback: "report the raw singleton rate as a lower bound on novelty"
```

**Proposition 17.1 (Good–Turing; standard: Good 1953; McAllester–Schapire 2000).** Let $N_1$ be the number of categories observed exactly once in $n$ i.i.d. observations. The probability mass of categories never observed, $M_0$, satisfies $\mathbb E[M_0]\approx\mathbb E[N_1/n]$, and with probability $1-\delta$, $|M_0-N_1/n|\le O\!\big(\sqrt{\ln(1/\delta)/n}\big)$. $\square$

Athena therefore has a *number* for how much of the world it has never seen: the fraction of strategic events that were singletons. A planner with $N_1/n=0.3$ should expect three in ten of its next surprises to be of a kind it has no category for, and level 2's $\alpha$ and the ambiguity set $\mathcal P$ SHOULD be widened accordingly (V2 §72's deep-uncertainty mode is entered when $N_1/n$ exceeds a declared threshold). The reference model checks the estimator on a Zipf world (check 15).

### 18. Deception-aware inference

```yaml
contract:
  name: strategic_source_model
  v2_lineage: [86 Deception-Aware Inference, 15 Formal Rules vs Effective Reality, 93 Organizational Information Distortion]
  inputs: {report: "a claim", source: "actor with modeled utility (Section 19)", context: "what the source gains if the claim is believed"}
  outputs: {posterior_truth: real, informativeness: "nats", incentive_alignment: real}
  guarantee: "Crawford-Sobel (1982): a self-interested sender's message is informative only up to the sender-receiver preference gap; communication is partitional and coarser as the gap grows; Akerlof (1970), Spence (1973): claims that are costly to fake carry information, claims that are free do not"
  complexity: "O(|message partition|) per report"
  failure_mode: "source's utility mis-modeled: detected when the source's claims are later resolved against outcomes (Section 8) with a calibration gap"
  fallback: "treat the source as uninformative (likelihood ratio 1) and seek a costly signal"
```

The rule is Spence's: Athena weights a claim by what it cost the claimant to make it. Free claims from interested parties are, in the cheap-talk equilibrium, partitional and coarse, and Athena updates on them only as such. V2 §15's gap between formal rules and effective reality is the gap between what a source says the rules are and what costly signals (behavior, prices, resignations) show.

---

## **19–22. Who are the others? (actors)**

### 19. Inverse utility inference

```yaml
contract:
  name: inverse_utility_inference
  v2_lineage: [14 Inverse Utility Inference, 13 Multi-Actor Strategic Model, 92 Human Behavior Model]
  inputs: {trajectories: "observed actions of actor j in recorded states", feature_map: "phi(s,a)", prior: "over reward weights"}
  outputs: {posterior_reward_weights: "distribution", predicted_policy: "pi_j(a|s) with uncertainty", feature_expectations: vector}
  guarantee: "Proposition 19.1"
  complexity: "MaxEnt: O(iterations x |S||A|) per gradient step; Bayesian: MCMC over weights"
  failure_mode: "reward ambiguity (many rewards explain the same behavior, Ng-Russell 2000): reported as posterior width; behavior inconsistent with any reward: reported as 'non-rational actor', route to Section 20"
  fallback: "behavioral cloning of the observed policy with a non-stationarity flag"
```

**Proposition 19.1 (identification of intent; standard: Ziebart et al. 2008; Ramachandran–Amir 2007).** Among all policies that match the observed feature expectations, the maximum-entropy policy is unique and has the form $\pi(\zeta)\propto\exp(w^\top\phi(\zeta))$ over trajectories $\zeta$; the weights $w$ are the unique solution of a convex program. Bayesian IRL returns the full posterior over $w$ given a prior and a rationality temperature, and so reports *how* uncertain Athena is about the actor's goals, not just a point estimate. $\square$ For human actors the feature map includes reference points and loss aversion (Kahneman–Tversky 1979) and mental accounts (Thaler 1985); V2 §92's human behavior model is this feature map.

### 20. Bounded rationality and equilibrium

```yaml
contract:
  name: strategic_interaction_model
  v2_lineage: [13 Multi-Actor Strategic Model, 88 Equilibrium Shift Engine, 135 Multi-Entity Strategy]
  inputs: {game: "actors, action sets, payoffs from Section 19 with uncertainty", sophistication_prior: "Poisson(tau) over levels"}
  outputs: {predicted_play: "distribution per actor", equilibrium_set: "CCE polytope or sample", exploitability: "per candidate Athena strategy"}
  guarantee: "Proposition 20.1"
  complexity: "regret matching: O(|A|) per round per actor; CH: O(k |A|^2)"
  failure_mode: "actors adapt to Athena's model of them (Lucas 1976): detected by exploitability rising over time; route to Section 21"
  fallback: "maximin against the declared uncertainty set of opponent strategies"
```

**Proposition 20.1 (what to expect of others; standard: Camerer–Ho–Chong 2004; Hart–Mas-Colell 2000; Aumann 1974/1987; Harsanyi 1967–68).** (i) In one-shot play, a cognitive-hierarchy model with Poisson-distributed sophistication (mean $\tau\approx1.5$ in the experimental literature) predicts play better than Nash equilibrium across a wide class of games. (ii) In repeated play, if every actor uses a no-regret procedure such as regret matching, the empirical distribution of play converges to the set of coarse correlated equilibria, whatever the actors' payoffs; Athena's own regret-matching play has regret $O(\sqrt T)$ against *any* opponent. (iii) Under incomplete information the right solution concept is Harsanyi's Bayesian equilibrium over actor types, with the type posterior from Section 19. $\square$

**The Lucas principle (V2 §150: "expect other actors to adapt").** A model of an actor estimated under one policy of Athena's does not survive a change in that policy, because the actor re-optimizes (Lucas 1976). **R20.1** Every actor model records the Athena policy it was estimated under; a prediction that would be used under a materially different Athena policy is flagged `lucas_unstable` and its uncertainty widened to the declared uncertainty set.

### 21. Safe exploitation

```yaml
contract:
  name: restricted_best_response
  v2_lineage: [31 Red-Team Strategic Engine, 13 Multi-Actor Strategic Model]
  inputs: {opponent_model: "from Sections 19-20 with confidence p", game: "zero-sum or declared worst-case transform", safety_margin: "epsilon"}
  outputs: {strategy: "mixed", exploitability_bound: "epsilon", expected_gain_vs_model: real}
  guarantee: "Proposition 21.1"
  complexity: "one LP (or CFR run) per confidence level"
  failure_mode: "opponent model wrong: loss bounded by epsilon regardless (that is the guarantee)"
  fallback: "the equilibrium (minimax) strategy, exploitability 0"
```

**Proposition 21.1 (bounded-exploitability exploitation; standard: McCracken–Bowling 2004; Johanson–Zinkevich–Bowling 2007).** For a two-player zero-sum game and an opponent model held with confidence $p$, the *restricted Nash response* (the best response to a mixture of the modeled opponent with weight $p$ and a worst-case opponent with weight $1-p$) is a strategy whose exploitability is at most a declared $\epsilon(p)$ against *any* opponent while capturing most of the available gain against the modeled one; $\epsilon$-safe best responses trace the Pareto frontier between exploitation and safety. $\square$

This is V2 §31's red team as a design rule: Athena never plays a strategy whose worst case it has not bounded, however confident its opponent model.

### 22. Power and dependency graph

```yaml
contract:
  name: power_dependency_graph
  v2_lineage: [89 Power / Dependency Graph, 90 Legitimacy and Trust as Capital, 91 Reputation Memory]
  inputs: {graph: "actors as nodes; edges = resource, information and authorization dependencies with weights", coalition_structure: "declared"}
  outputs: {power_index: "per actor (Shapley-Shubik or Banzhaf on the coalition game)", dependency_centrality: "Katz/eigenvector", chokepoints: "min-cut sets", reputation_state: "per actor, decayed"}
  guarantee: "Shapley value is the unique efficient, symmetric, additive, null-player-respecting allocation of coalition value (Shapley 1953); Katz centrality is well-defined for attenuation below the spectral radius; chokepoints are exact by max-flow/min-cut"
  complexity: "power indices: sampled, O(M |actors|) with Hoeffding error; centrality: O(|E|) per power iteration; min-cut: O(|V||E|^2) worst case"
  failure_mode: "coalition structure wrong: power indices shift; detected by Section 8 resolution of predicted vs actual bargaining outcomes"
  fallback: "degree centrality and declared dependency ranks"
```

Legitimacy and trust (V2 §90) are the $L$ line of the capital vector and decay by their declared half-life (R1.2.3); reputation memory (V2 §91) is the per-actor record of promises kept, resolved by Section 8, which feeds the reliability prior of Section 14 and the trust decay of $L$. Ostrom's (1990) design principles for durable cooperation (clear boundaries, graduated sanctions, monitoring by the governed) are the registered features of the legitimacy index.

---

## **23–26. What could happen? (futures)**

### 23. Scenario engine and scenario reduction

```yaml
contract:
  name: scenario_ensemble
  v2_lineage: [16 Strategic Scenario Engine, 47 Simulation Architecture, 112 Synthetic Worlds, 132 Distributed Simulation Fabric]
  inputs: {belief: "Section 15", actor_models: "Sections 19-21", horizon: T, N: "sample budget", reduction_target: "K scenarios"}
  outputs: {scenarios: "K weighted trajectories", wasserstein_gap: "W1 between the N-sample and K-sample distributions", objective_error_bound: real}
  guarantee: "Proposition 23.1"
  complexity: "generation O(N T |simulation|), distributed trivially; reduction O(N K) greedy (Dupacova et al.)"
  failure_mode: "scenario collapse (all futures alike): detected by low ensemble entropy relative to the belief's entropy; model fails to represent 'unpleasant, unlawful, deceptive' futures (V2 §1): detected by the red team (Section 21) finding a plausible adversarial future absent from the ensemble"
  fallback: "declared finite scenario set with minimax regret (deep uncertainty mode)"
```

**Proposition 23.1 (stability of the objective under scenario reduction; standard: Römisch 2003; Dupačová–Gröwe-Kuska–Römisch 2003).** If the objective is Lipschitz in the scenario with constant $L$ (which holds for $\bar G_T$ under bounded growth factors), then replacing the scenario distribution $P$ by a reduced $Q$ changes the optimal value by at most $L\cdot W_1(P,Q)$, and the greedy backward-reduction algorithm produces a $Q$ on $K$ atoms whose $W_1(P,Q)$ is computable and reported. $\square$ Common random numbers across policies (RSI v3's mechanism) are used so that policy comparisons are paired and their variance is the variance of the difference.

**R23.1** The ensemble MUST include futures the owner would find unpleasant or that involve unlawful or deceptive conduct by other actors when such futures are plausible (V2 §1); representing a future is not endorsing it, and the action layer (Section 40) is governed separately.

### 24. Historical replay with selection correction

```yaml
contract:
  name: historical_replay
  v2_lineage: [48 Historical Replay Benchmark, 111 Historical Time Machine]
  inputs: {history: "ledger or external record with timestamps", information_cutoffs: "what was knowable when", selection_model: "which histories were recorded and why"}
  outputs: {replayed_decisions: "with Athena's recommendation at each cutoff", score: "vs realized outcome", selection_weights: "inverse probability of being in the record"}
  guarantee: "Proposition 24.1"
  complexity: "O(|history| x planner)"
  failure_mode: "leakage of post-cutoff information: detected by a held-out leakage probe (a future fact planted in the cutoff's information set must not change the recommendation); survivorship: detected when selection weights are extreme (ESS small)"
  fallback: "replay on the ledger's own decisions only, where the selection model is known exactly"
```

**Proposition 24.1 (survivorship is a selection problem; standard: Heckman 1979; Horvitz–Thompson 1952; Politis–Romano 1994).** (i) A history recorded only when the entity survived (or succeeded, or was written about) is a selected sample; estimates of what worked are biased unless weighted by the inverse probability of selection or corrected by a selection model. (ii) Confidence intervals for replay scores on dependent (serially correlated) histories are valid under the stationary block bootstrap with random block lengths, under mixing. $\square$

V2 §150's "learn from what almost happened" is the near-miss record: histories of entities that did *not* survive, weighted up. **R24.1** A replay benchmark score without selection weights is reported as `survivor_biased`.

### 25. Synthetic worlds and the simulation-to-reality gap

```yaml
contract:
  name: synthetic_world_suite
  v2_lineage: [112 Synthetic Worlds, 109 Self-Generated Benchmarks, 113 Multi-Athena League]
  inputs: {world_family: "generative model with declared parameters", randomization: "distribution over parameters (domain randomization)", ground_truth: "causal structure, for credit-assignment scoring"}
  outputs: {policies_scores: "paired, common random numbers", sim2real_gap_estimate: "from the subset of worlds calibrated to history"}
  guarantee: "a policy robust across the randomized family is robust in any real world inside the family's support (Tobin et al. 2017); outside it no guarantee is claimed"
  complexity: "O(worlds x episodes x planner)"
  failure_mode: "family too narrow: detected when historical replay (24) scores diverge from synthetic scores by more than the declared gap"
  fallback: "historical replay only"
```

Synthetic worlds are where credit-assignment accuracy (Benchmark B6) and Goodhart resistance (B4) are measured, because only there is the ground truth known.

### 26. Strategic digital twin

```yaml
contract:
  name: entity_twin
  v2_lineage: [65 Strategic Digital Twin, 66 Strategic Knowledge Graph, 82 Time-to-Capability Model]
  inputs: {capital_vector: x_t, conversion_graph: "Section 1.2", commitments: C_t, capability_registry: "levels, lead times, prerequisites, decay"}
  outputs: {twin_state: "simulable copy", time_to_capability: "distribution per capability", conversion_paths: "ranked by growth contribution per unit cost"}
  guarantee: "the twin is a faithful simulator of the entity's own dynamics to the extent its parameters are identified from the ledger; every parameter carries its identification status (identified / assumed / unknown)"
  complexity: "O(|graph|) per step"
  failure_mode: "twin drift: twin-predicted vs realized capital diverge; detected by the regime detector on the residual"
  fallback: "declared static capability table"
```

Time-to-capability (V2 §82) is a distribution, estimated from the registry's lead times with learning-curve (Arrow 1962) and bottleneck (Section 29) effects, and is compared with the need-time distribution in the long-lead detector of Section 28.

---
## **27–30. What should we do? (decisions)**

### 27. Robust policy selection and receding-horizon control

```yaml
contract:
  name: robust_receding_horizon_planner
  v2_lineage: [8 Model Predictive Strategic Control, 17 Robust Policy Selection, 99 Hierarchical Policy Tree, 100 Policy Portfolios, 101 Contingent Strategies, 129 Strategic DAG]
  inputs: {state: s_t, scenarios: "Section 23", objective: "Definition 3.1 with manifest parameters", horizon_resolution: "adaptive (coarse far, fine near)", authorized_step: "the near-term action class the owner has authorized"}
  outputs: {policy_tree: "contingent plan over scenarios", next_action: "the first reversible step", pareto_set: "nondominated alternatives", infeasibility_certificate: "smallest conflicting constraint set, if infeasible", level_report: "Section 3.5"}
  guarantee: "Proposition 27.1"
  complexity: "scenario tree: O(K^depth); with scenario reduction and coarse far horizon, O(K_near x K_far x |A|) per replan"
  failure_mode: "infeasible: returns the conflicting set and owner options (reduce scope, extend time), never relaxes constraints silently (v5.1 §11); level-1 infeasibility at a replan after adverse realizations (Proposition 27.1(ii)): reported with the current certificate value B(s_t) and the smallest reversible commitment that restores it"
  fallback: "the previously authorized plan's remaining steps, re-certified from the realized state; if no admissible policy meets level 1 from s_t, the null action and a question to the owner (Section 40)"
```

**Proposition 27.1 (what receding-horizon control does and does not guarantee; standard: Rawlings–Mayne–Diehl 2017; Mayne et al. 2000; derived for the growth objective).** (i) *Horizon-wide certificate from the start.* If the action layer enforces $\mathbb E[B(s_{t+1})\mid s_t,a_t]\le B(s_t)$ at every step (Proposition 40.1(ii)), then $P(\tau_{\mathcal R}<\infty)\le B(s_0)$ holds for the whole closed-loop trajectory, whatever replanning does, because $B(s_t)$ remains a supermartingale under the closed-loop policy. (ii) *No recursive feasibility of the level-1 constraint.* The sublevel set $\{B\le\varepsilon\}$ is **not** forward invariant: a supermartingale may rise on a realized step, so a plan whose certificate was $B(s_0)\le\varepsilon$ can arrive at a state with $B(s_t)>\varepsilon$, from which no admissible policy certifies $\varepsilon$ over the remaining horizon. Example: the unit-step walk of Corollary 5.2 with $\varepsilon=0.02$ certifies $B(10)=0.0173$ at $t=0$ and with probability $0.4$ moves to $B(9)=0.026>\varepsilon$ on its first step. Recursive feasibility of chance constraints is an open problem in stochastic model predictive control, and this document imports no result on it. (iii) *No optimality is imported:* the closed-loop growth rate of the receding-horizon policy is not in general the optimum of the infinite-horizon program; the gap is bounded by the terminal head's error (Section 6.2) and reported. *Proof.* (i) is Proposition 5.1 applied to the closed-loop process, whose supermartingale property is enforced action by action. (ii) is the example. (iii) is the usual MPC suboptimality bound with the terminal cost taken as the far-horizon value head. $\square$

**R27.0** Every replan recomputes the certificate from the realized state and reports $B(s_t)$ against $\varepsilon$. When $B(s_t)>\varepsilon$ the packet says so, the planner returns the level-1 infeasibility certificate with the smallest reversible commitment that restores $B\le\varepsilon$ (raising a reserve, exiting an exposure), and the owner decides; the planner MUST NOT relax $\varepsilon$ or re-define the barrier to make the plan pass. The guarantee the owner holds is (i): the probability of ruin over the whole program, computed when the program began, was bounded and remains bounded; the guarantee the owner does not hold is that every future replan will be able to promise the same number from where it then stands.

V2 §8's "long vision, short control loop" is (i) and R27.0: the *vision* is the far heads and the horizon-wide certificate; the *loop* is the authorized first step, re-certified every time. **R27.1** The planner MUST preserve the Pareto set across utility, cost, risk, optionality, capability growth, attention and reversibility before scalar ranking (v5.1 §11); dominance is established under the chosen uncertainty treatment, and alternatives within their uncertainty of each other are retained (V2 §70).

**Policy portfolios and contingent strategies (V2 §100–101)** are the policy tree's branches: a contingent strategy is a sub-tree keyed to a trigger (Section 16); a policy portfolio is a mixture over sub-trees sized by Section 29. **Hierarchical policy trees (V2 §99)** are options in the sense of Sutton–Precup–Singh (1999): temporally extended actions with initiation sets and termination conditions; the planner's Bellman equation over options is the semi-Markov one, and a policy over options is evaluated exactly by it.

### 28. Timing, real options and long-lead capabilities

```yaml
contract:
  name: timing_and_options_engine
  v2_lineage: [20 Real Options Engine, 21 Long-Lead-Time Capability Detector, 24 Strategic Timing Engine, 74 Reversibility Engine, 80 Temporal Arbitrage Engine, 83 Strategic Latency]
  inputs: {commitment: "cost I, irreversibility class, value process model", capability: "need-time distribution, build-time distribution (Section 26)", alternatives: "act now, wait, stage, accelerate, maintain readiness, abandon"}
  outputs: {recommended_timing: "one of the six", option_value_incremental: real, exercise_threshold: real, p_needed_before_ready: real, preparatory_investment: "size and what it buys (lead time reduction)"}
  guarantee: "Proposition 28.1"
  complexity: "closed form O(1) under GBM; LSMC O(paths x steps x basis) otherwise; need-vs-build O(samples)"
  failure_mode: "value process not GBM-like (jumps, regime shifts): closed form invalid; detected by the regime detector on the value process; LSMC used"
  fallback: "staged commitment with the smallest reversible first step (v5.1 §13)"
```

**Proposition 28.1 (the value of waiting and the cost of being late; standard: McDonald–Siegel 1986; Dixit–Pindyck 1994; Longstaff–Schwartz 2001; derived for the lead-time rule).** (i) Under GBM value with irreversible cost, the optimal exercise threshold is $V^*=\beta_1I/(\beta_1-1)$ of Section 7.3; the option to wait is worth $(V^*-I)(V/V^*)^{\beta_1}$ for $V<V^*$ and is strictly positive whenever $\sigma>0$. (ii) For American-style options on general processes, least-squares Monte Carlo converges to the option value as paths and basis functions grow. (iii) *Lead-time rule:* if the time until a capability is needed, $T_{\text{need}}$, and the time to build it, $T_{\text{build}}$, are independent with distributions $F_n$ and $F_b$, then $P(\text{needed before ready})=\int F_n(t)\,dF_b(t)$; a preparatory investment that reduces build time by $\Delta$ reduces this probability by $\int[F_n(t)-F_n(t-\Delta)]\,dF_b(t)$, and is worth making when that reduction times the strategic value if needed exceeds its cost plus the option value of not making it (which (i) prices). $\square$

**Reversibility (V2 §74)** is the irreversibility class of a commitment and enters (i) through $I$: a reversible action has salvage value and a correspondingly lower threshold. **Strategic latency (V2 §83)** is the expected time from a trigger firing to the authorized effect landing, and is subtracted from $T_{\text{need}}$. **Temporal arbitrage (V2 §80)** is the detection of capabilities whose build time is short now and long later (a closing window), which (iii) prices as a rising $P(\text{needed before ready})$.

### 29. Allocation, bottlenecks and shadow prices

```yaml
contract:
  name: strategic_capital_allocation
  v2_lineage: [19 Kelly-Inspired Resource Allocation, 58 Athena's Own Resource Allocation, 76 Compounding Engine, 77 Bottleneck Engine, 78 Shadow Price Engine, 79 Strategic Capital Allocation Engine, 130 Resource Scheduler, 131 Bottleneck-Aware Scaling, 136 Internal Markets for Resources]
  inputs: {conversion_graph: "Section 1.2 with capacities and conversion rates", budget: "resource vector b", candidates: "investments with growth contribution models", ruin_set: R}
  outputs: {allocation: vector, shadow_prices: "per resource, = dual variables", bottleneck: "min-cut set of the conversion graph", kelly_fractions: "where the regime applies", concentration_report: "max share per bet and its justification"}
  guarantee: "Proposition 29.1"
  complexity: "convex program O(poly(|candidates|, |resources|)); max-flow O(|V||E|^2) (Edmonds-Karp) or O(|V|^2 |E|) (Dinic)"
  failure_mode: "nonconvex returns (increasing returns to scale, V2 §76): duality gap; detected and reported; branch-and-bound on the few nonconvex lines"
  fallback: "explicit concentration limits and staged commitments (v5.1 §13)"
```

**Proposition 29.1 (shadow prices and bottlenecks; standard: Kuhn–Tucker 1951; envelope theorem (Milgrom–Segal 2002); Ford–Fulkerson 1956; Markowitz 1952; derived for the growth objective).** Let $\rho^*(b)=\max\{\rho_\alpha(\pi):\ \text{resource use}(\pi)\le b\}$ be the robust growth attainable with budget vector $b$, with the program convex. (i) The dual variables $\lambda_i$ at the optimum satisfy $\partial\rho^*/\partial b_i=\lambda_i$: the shadow price of resource $i$ is the robust growth bought by one more unit of it, and a resource with $\lambda_i=0$ is slack. (ii) On the conversion graph, the maximum rate at which capital can be converted from sources to a target capability equals the capacity of the minimum cut; the bottleneck of V2 §77 is the min-cut set, and only capacity added on a min-cut edge raises throughput (Goldratt's theory of constraints is max-flow/min-cut). (iii) Where opportunities are repeated and fungible (5.3), the multi-asset Kelly allocation is $f^*=\Sigma^{-1}\mu_e$ under lognormal approximation and the fractional rule of Proposition 5.3 applies to the whole vector; in the general case the allocation is the Markowitz-type mean/lower-tail trade-off that level 2 induces. $\square$

Shadow prices are what Athena sends the engine as the value of a capability (11.1); internal markets (V2 §136) clear at them. **Athena's own compute (V2 §58)** is one resource line, allocated by the same program, with the marginal value of compute by task class learned from the ledger (Section 35).

### 30. Pareto, regret, path dependence and reversibility

```yaml
contract:
  name: multi_criteria_decision_support
  v2_lineage: [70 Pareto Frontier Decision-Making, 71 Regret Minimization, 72 Deep Uncertainty Mode, 73 Strategic Entropy, 75 Path-Dependence Engine, 87 Nth-Order Effects, 139 Robustness vs Optimality, 140 Antifragility Search]
  inputs: {alternatives: "policies with level reports", scenario_set: "declared or sampled", preference_set: Theta_beta}
  outputs: {pareto_set: "nondominated under uncertainty", regret_table: "per alternative per scenario", max_regret: "per alternative", hysteresis_map: "states from which return is costly", convexity_report: "which alternatives gain from volatility (antifragile)"}
  guarantee: "Savage (1951) minimax regret is the declared level-2 criterion in deep-uncertainty mode; Pareto dominance under uncertainty is established only by stochastic dominance or by paired comparison with CRN at declared confidence; path dependence is reported as the set of absorbing or high-hysteresis states reachable within the horizon"
  complexity: "O(|alternatives| x |scenarios|)"
  failure_mode: "scenario set omits the decisive scenario: minimax regret is only as good as the set (reported); hysteresis map incomplete: states missed are flagged by empowerment drops (Section 7)"
  fallback: "robust feasibility (Ben-Haim 2006 info-gap): the largest uncertainty under which each alternative stays acceptable"
```

**Strategic entropy (V2 §73)** is the entropy of the scenario ensemble's outcome distribution under each alternative; **antifragility (V2 §140)** is convexity of the growth contribution in the volatility of a scenario variable, tested by paired evaluation at two volatility levels. **Nth-order effects (V2 §87)** are the terms beyond first order in the scenario propagation, which the agent-based simulation (Section 23) carries by construction and the analytical core (Section 36) truncates and reports.

---

## **31–34. What have we learned? (learning and memory)**

### 31. Calibration

```yaml
contract:
  name: multicalibrated_forecasting
  v2_lineage: [28 Strategic Calibration Engine, 43 Strategic Scorecard, 120 Model Correlation Detector]
  inputs: {forecasts: "probabilities with group attributes (actor, horizon, domain, model)", outcomes: "resolved", group_family: "C"}
  outputs: {calibration_error: "per group in C", reliability_diagram: "per group", brier_decomposition: "reliability, resolution, uncertainty", recalibrated_forecasts: "post-processed"}
  guarantee: "Proposition 31.1"
  complexity: "multicalibration: poly(1/alpha, log |C|) samples and iterations; recalibration O(n log n)"
  failure_mode: "too few resolved outcomes in a group: calibration unidentified; reported with the group's sample size"
  fallback: "global isotonic recalibration"
```

**Proposition 31.1 (calibration you can have; standard: Foster–Vohra 1998; Hébert-Johnson–Kim–Reingold–Rothblum 2018; Foster–Hart 2023; Murphy 1973).** (i) A forecaster can be asymptotically calibrated against *any* sequence of outcomes, including an adversarial one; calibration costs nothing in accuracy in the limit. (ii) For any family $\mathcal C$ of groups (here: by actor, horizon, domain and model), there is an efficient post-processing that makes the forecasts simultaneously $\alpha$-calibrated on every group in $\mathcal C$, with sample complexity polynomial in $1/\alpha$ and $\log|\mathcal C|$. (iii) Any forecaster can be "calibeaten": post-processed to be calibrated with Brier score no worse, and better by the forecaster's own calibration error. (iv) The Brier score decomposes exactly as $\text{reliability}-\text{resolution}+\text{uncertainty}$; skill is resolution net of reliability, and uncertainty is the part no forecaster can remove. $\square$

(iv) is V2 §97's luck/skill decomposition for forecasts: the uncertainty term is luck. **R31.1** The scorecard (V2 §43) reports Brier decomposition per group; a model whose reliability term grows is recalibrated by (iii) before it is used, and its proxy budget (9.3) is cut in proportion.

### 32. Strategic memory and transfer

```yaml
contract:
  name: successor_feature_memory
  v2_lineage: [26 Strategic Memory, 123 Memory Tiers, 124 Memory Decay Without Deletion, 125 Event-Sourced State, 142 Continuity of Identity]
  inputs: {policies_stored: "pi_1..pi_k with their successor features psi^{pi_i}(s,a) = E[sum gamma^t phi(s_t,a_t)]", new_preference: "w (theta or a regime-shifted reward)", features: "phi"}
  outputs: {transferred_policy: "pi via generalized policy improvement", suboptimality_bound: real, which_memory_was_used: "the pi_i whose w_i is nearest"}
  guarantee: "Proposition 32.1"
  complexity: "O(k |A|) per state for GPI; successor features learned by TD"
  failure_mode: "reward not linear in the stored features: bound does not apply; detected by the gap between predicted and realized value under the new w"
  fallback: "re-plan from scratch with the new reward; memory is used only as initialization"
```

**Proposition 32.1 (memory transfers with a bound; standard: Barreto et al. 2017; Dayan 1993).** Let rewards be $r_w(s,a)=\phi(s,a)^\top w$ and let Athena hold policies $\pi_1,\dots,\pi_k$ with successor features $\psi^{\pi_i}$ learned to accuracy $\epsilon$ (so $|Q^{\pi_i}_w-\tilde Q_i|\le\epsilon$). For a new $w$, let $\pi(s)=\arg\max_a\max_i\tilde Q_i(s,a)$ with $\tilde Q_i=\psi^{\pi_i\top}w$. Then $Q^\pi_w(s,a)\ge\max_i Q^{\pi_i}_w(s,a)-\tfrac{2\epsilon}{1-\gamma}$, and $Q^*_w-Q^\pi_w\le\tfrac{2}{1-\gamma}\big(\phi_{\max}\min_j\|w-w_j\|+\epsilon\big)$. $\square$

So when the owner's preferences move (Section 4) or a regime shift changes what pays (Section 16), Athena produces, *without re-planning*, a policy whose loss is bounded by how far the new weights are from the nearest remembered ones. This is V2 §142's continuity of identity: the strategist that survives a model replacement is the one whose memory is in successor features, not in the replaced model's weights. **Memory decay without deletion (V2 §124)** is the retention of stale $\psi^{\pi_i}$ with a growing uncertainty, never their removal; **memory tiers (V2 §123)** are the latency classes at which they are served. The reference model verifies the GPI bound on a small world (check 17).

### 33. Doctrine: distillation and forking

```yaml
contract:
  name: doctrine_engine
  v2_lineage: [41 Strategic Doctrine Engine, 114 Doctrine Distillation, 115 Doctrine Forking, 116 Strategic Reflection Cycle, 110 Curriculum of Strategy]
  inputs: {resolved_decisions: "Section 8, with Shapley credit", current_doctrine: "a compact policy prior pi_doc", candidate_lessons: "proposed rule changes"}
  outputs: {updated_doctrine: "pi_doc'", evidence_ratio: "e-process value for the change", fork: "if two doctrines are each supported in disjoint regimes, both with their regime detectors"}
  guarantee: "a doctrine change is admitted at the doctrine threshold of 6.5 (false-change rate <= e^-tau_doctrine, Proposition 10.1); distillation minimizes KL(pi_expert || pi_doc) subject to a description-length cap, so the doctrine is the shortest policy within the budget that reproduces resolved good decisions (Section 39)"
  complexity: "O(|resolved| x |rules|)"
  failure_mode: "a lesson drawn from a lucky outcome: prevented by Shapley credit being computed with abducted noise (Section 8.4) and by the luck/skill decomposition (31.1(iv))"
  fallback: "no change; the lesson is logged as 'insufficient evidence' with its e-value"
```

Doctrine is V2 §41 as a Bayesian prior over policies, with a description-length budget. A **fork** (V2 §115) is admitted when the agreement series of two candidate doctrines is separated by a regime variable with a detectable change-point; the fork carries its own detector so that the right doctrine is applied in the right regime.

### 34. Post-mortems, pre-mortems and the luck/skill ledger

```yaml
contract:
  name: outcome_review
  v2_lineage: [94 Adversarial Self-Critique, 95 Strategic Pre-Mortem, 96 Strategic Post-Mortem, 97 Luck / Skill Decomposition, 29 Counterfactual Engine, 30 Contrarian Engine]
  inputs: {decision: "ledger entry with forecast, propensity, belief state", outcome: "resolved or surrogate", scenario_ensemble_at_decision: "stored"}
  outputs: {decision_quality: "forecast skill at decision time (31.1(iv))", execution_quality: "realized vs planned action", exogenous_share: "variance from abducted noise", model_error: "belief vs realized world", lesson: "candidate doctrine change with e-value"}
  guarantee: "the decomposition sums to the realized outcome gap (Shapley efficiency, 8.4); decision quality is scored on the information available at the time (information cutoff enforced as in 24)"
  complexity: "O(samples)"
  failure_mode: "hindsight contamination (scoring the decision with later facts): prevented by replaying the stored belief state; detected by the leakage probe of 24"
  fallback: "qualitative review posted to the owner"
```

A **pre-mortem** (V2 §95) runs the same decomposition on the *scenario ensemble* before the decision: for each failing scenario, which term fails. The **contrarian engine** (V2 §30) is the pre-mortem under the actor model in which the consensus is wrong (Section 19's posterior tail), and the **adversarial self-critique** (V2 §94) is the red team of Section 21 applied to Athena's own plan.

---

## **35–39. How should we think? (meta)**

### 35. Compute economics and adaptive reasoning depth

```yaml
contract:
  name: rational_metareasoning
  v2_lineage: [117 Compute Economics, 118 Adaptive Reasoning Depth, 58 Athena's Own Resource Allocation, 83 Strategic Latency]
  inputs: {decision: "current", candidate_computations: "with cost and a performance profile (expected improvement in rho_alpha as a function of compute)", deadline: "from strategic latency"}
  outputs: {computation_plan: "which analyses, at what fidelity, in what order", stop_rule: "when marginal expected improvement < marginal cost", expected_value_of_computation: real}
  guarantee: "Proposition 35.1"
  complexity: "O(|candidates|) per step"
  failure_mode: "performance profiles mis-estimated: detected by the ledger's record of realized improvement per unit compute by task class (V2 §58)"
  fallback: "fixed analysis budget by decision class"
```

**Proposition 35.1 (value of computation; standard: Russell–Wefald 1991; Hay–Russell–Tolpin–Shimony 2012; Jamieson–Talwalkar 2016).** (i) The expected value of a computation is the expected improvement in the decision it informs, net of its cost; running computations in order of value-of-computation per unit cost and stopping when the best remaining is nonpositive is optimal when the value of computation is diminishing, and is within a constant factor of optimal in the general one-step case. (ii) When $n$ candidate analyses compete for a budget, successive halving (allocate, evaluate, keep the best half, repeat) finds the best with total budget $O(n\log n)$ times the per-evaluation cost, and Hyperband hedges over the fidelity schedule. $\square$

This is V2 §118's adaptive depth: Athena thinks longer when thinking is worth more, and the scorecard records the realized value of computation per task class so the profiles are learned.

### 36. Ensembles, belief markets and quorum by evidence

```yaml
contract:
  name: ensemble_of_strategists
  v2_lineage: [36 Multi-Model Native Architecture, 67 Belief Market, 68 Ensemble of Strategists, 69 Strategic Tournaments, 119 Quorum by Evidence Not Count, 120 Model Correlation Detector, 121 Model Failure Map, 126 Deterministic Analytical Core, 127 Neuro-Symbolic Orchestration]
  inputs: {strategists: "N models/agents producing forecasts and policy proposals", outcomes: "resolved", correlation_estimates: "pairwise error correlation", market_liquidity: "b"}
  outputs: {aggregate_forecast: "exponential-weights mixture", market_prices: "LMSR", effective_independent_models: "n_eff", weights: "per strategist, with regret bound"}
  guarantee: "Proposition 36.1"
  complexity: "O(N) per round; LMSR O(N) per trade"
  failure_mode: "strategists correlated (same training data, same vendor): n_eff small; detected by the correlation estimate and reported; aggregation then weights by evidence (Bayes factors), not by count"
  fallback: "the single best-calibrated strategist by Section 31"
```

**Proposition 36.1 (aggregation with guarantees; standard: Freund–Schapire 1997; Cesa-Bianchi–Lugosi 2006; Hanson 2003/2007; elementary for (iii)).** (i) *Exponential weights:* with learning rate $\eta=\sqrt{8\ln N/T}$, the aggregate's cumulative loss exceeds the best strategist's in hindsight by at most $\sqrt{(T/2)\ln N}$, against any sequence of outcomes. (ii) *Belief market:* the logarithmic market scoring rule with liquidity $b$ has cost function $C(q)=b\ln\sum_ie^{q_i/b}$, is myopically incentive-compatible (a trader maximizes expected profit by moving the price to its belief), and bounds the market maker's worst-case loss by $b\ln N$ over $N$ outcomes. (iii) *Correlation caps diversification:* for $n$ strategists with equal error variance $\sigma^2$ and pairwise error correlation $\rho$, the averaged error has variance $\sigma^2\big(\rho+\tfrac{1-\rho}{n}\big)\to\rho\sigma^2$: with $\rho=0.8$, a thousand models are worth only a 20% variance reduction, and the effective number of independent models is $n_{\text{eff}}=n/(1+(n-1)\rho)$. $\square$

(iii) is V2 §119 and §120 as arithmetic: a quorum of correlated strategists is one strategist with a confident voice. **R36.1** Decisions report $n_{\text{eff}}$, not $n$; evidence-weighted aggregation uses log Bayes factors from the resolved record. The reference model checks (i)–(iii) (checks 16, 13 and 14; the LMSR loss bound is an identity of the cost function, so check 13 contrasts it with a constant-price market maker whose worst-case loss grows with volume).

**Deterministic analytical core and neuro-symbolic orchestration (V2 §126–127).** Every quantity in this document that has a closed form (CVaR on samples, barrier bounds, Kelly fractions, shadow prices, EVSI on finite observation sets, Shapley on small sets, empowerment on small kernels) is computed by the deterministic core and *never* by a language model's estimate; the models propose, the core computes, the evaluator checks. The **model failure map (V2 §121)** is the per-model record of resolved errors by task class and regime, which sets the weights in (i).

### 37. Tournaments and the Athena league

```yaml
contract:
  name: strategist_tournament
  v2_lineage: [69 Strategic Tournaments, 113 Multi-Athena League, 49 Look Around Corners Benchmark]
  inputs: {strategists: "N", worlds: "synthetic (25) and replay (24) with common random numbers", pairing: "scheduled"}
  outputs: {ratings: "Bradley-Terry / TrueSkill with intervals", head_to_head: "paired differences with CRN", regime_specialists: "strategists that win in identified regimes"}
  guarantee: "paired comparisons with common random numbers have variance equal to the variance of the difference (RSI v3's CRN mechanism); Bradley-Terry (1952) ratings are the maximum-likelihood strengths and TrueSkill (Herbrich et al. 2007) gives their posterior; successive halving (35.1(ii)) finds the best with O(n log n) budget"
  complexity: "O(pairs x worlds)"
  failure_mode: "worlds too easy (all strategists tie): detected by rating intervals overlapping; harder worlds generated (V2 §109 self-generated benchmarks)"
  fallback: "single-world leaderboard with intervals"
```

A **league** (V2 §113) is a tournament with promotion: a strategist whose rating's lower confidence bound exceeds the incumbent's upper bound is promoted, which is the same rule as RSI v3's promotion gate (sustained LCB, never a peak).

### 38. Attention as a resource

```yaml
contract:
  name: rational_inattention_allocator
  v2_lineage: [137 Attention as a Resource, 138 Complexity Tax, 42 Strategic Decision Output]
  inputs: {owner_attention_capacity: "kappa nats per period (declared)", candidate_items: "questions, packets, alerts with their EVSI (Section 12)", current_use: "nats"}
  outputs: {what_to_show: "items ordered by EVSI per nat", what_to_hold: "items below the attention price", summary_depth: "per item"}
  guarantee: "Proposition 38.1"
  complexity: "O(items log items)"
  failure_mode: "capacity mis-declared: detected by the owner's response latency and skipped items; capacity re-estimated"
  fallback: "fixed packet length by decision class"
```

**Proposition 38.1 (rational inattention; standard: Sims 2003).** A decision maker who can process at most $\kappa$ nats of information per period about the state (a mutual-information constraint $I(\text{state};\text{signal})\le\kappa$) optimally allocates attention to the components of the state in proportion to their decision value per nat, and ignores components whose value per nat is below the Lagrange multiplier of the capacity constraint; the optimal signal structure is the solution of a rate–distortion problem. $\square$

The owner's attention is the scarcest resource in the loop. **R38.1** Athena's packets are sized by the owner's declared $\kappa$: the weekly review of v5.1 §2 (what changed, where resources moved, which assumptions weakened, what was learned, what was promoted, which decisions need a human) is the rate–distortion optimal summary at the owner's $\kappa$, and every summary links to the full record.

### 39. The complexity tax is a generalization bound

```yaml
contract:
  name: description_length_pricing
  v2_lineage: [138 Complexity Tax, 34 Modular Architecture, 54 Governance of Deep Changes]
  inputs: {policy_or_model: "with a prior pi_0 over policies and a posterior rho", evidence: "n resolved decisions"}
  outputs: {description_length_bits: "KL(rho || pi_0) / ln 2", generalization_bound: "Proposition 39.1", tax: "kappa x bits, in growth units"}
  guarantee: "Proposition 39.1"
  complexity: "O(1) given KL"
  failure_mode: "prior pi_0 too narrow (the true policy has infinite description length): detected by the bound being vacuous; prior widened and the change logged as a deep change (V2 §54)"
  fallback: "BIC penalty (k/2) ln n"
```

**Proposition 39.1 (PAC-Bayes; standard: McAllester 1999; Maurer 2004).** For any prior $\pi_0$ over policies fixed before seeing the $n$ resolved decisions, with probability at least $1-\delta$ simultaneously for every posterior $\rho$,

$$
\mathbb E_{\rho}[L]\ \le\ \mathbb E_{\rho}[\hat L_n]+\sqrt{\frac{\operatorname{KL}(\rho\|\pi_0)+\ln(2\sqrt n/\delta)}{2n}},
$$

where $L$ is the true loss (e.g. shortfall of realized vs. predicted growth) and $\hat L_n$ its empirical value. $\square$

So a strategy that takes $\operatorname{KL}$ nats to specify, relative to doctrine, needs on the order of $\operatorname{KL}$ more resolved decisions before its empirical record can be trusted to the same precision. That is the complexity tax (V2 §138) and the reason level 5 of Definition 3.1 exists: between two policies with equal robust growth, the one closer to doctrine has the tighter bound, and the slack $\eta_4$ is the price Athena will pay in growth for a policy it can trust sooner. Deep changes (V2 §54) are changes to $\pi_0$ itself, which void the bound and are governed accordingly.

---

## **40. Safety / agency separation**

```yaml
contract:
  name: governed_action_layer
  v2_lineage: [32 Safety / Agency Separation, 52 Agent Interface Contract, 128 Agent Contract Standard, 133 Failure Containment, 134 Strategic Checkpoints, 141 Graceful Degradation]
  inputs: {proposed_action: "from the planner", effect_class: "declared (informational / reversible / staged / irreversible / excluded)", envelope: "Superman admissible set, versioned", barrier_functions: "for every ruin coordinate"}
  outputs: {admitted: bool, modified_action: "the nearest admissible action (a projection, if admissible set is convex)", certificate: "barrier condition value", checkpoint: "state snapshot id"}
  guarantee: "Proposition 40.1"
  complexity: "O(|constraints|) per action (a QP when the admissible set is polyhedral)"
  failure_mode: "no admissible action exists: the layer returns the null action and a question to the owner; it never relaxes the envelope"
  fallback: "null action; strategic checkpoint; graceful degradation to the last admitted plan"
```

**Proposition 40.1 (forward invariance; standard: Ames et al. 2017/2019; Prajna et al. 2007; Ville).** (i) *Deterministic:* if $h(s)\ge0$ defines the safe set and the admitted action always satisfies $h(s_{t+1})-h(s_t)\ge-\alpha(h(s_t))$ for a class-$\mathcal K$ function $\alpha$ with $\alpha(r)<r$, then the safe set is forward invariant: an entity that starts safe stays safe. (ii) *Stochastic:* if $B$ is a ruin barrier (Proposition 5.1) and the admitted action always satisfies $\mathbb E[B(s_{t+1})\mid s_t,a]\le B(s_t)$, then $P(\text{ever unsafe})\le B(s_0)$; the action layer enforces this one inequality per ruin coordinate per action. (iii) Projecting the planner's proposed action onto the set satisfying (i)–(ii) is a convex program when the constraints are affine in the action, and is the minimal modification of the plan that keeps the certificate. $\square$

**The separation (V2 §32, §1).** The world model (Sections 13–26) MUST be able to represent unpleasant, unlawful, deceptive and catastrophic futures and actors; the action layer (this section) governs only what the advised entity *does*, by the effect class of each action and the Superman envelope. Excluded effect classes in the initial release (v5.1 §4): real-money trading, personnel decisions, physical control, infrastructure permission changes. **Failure containment (V2 §133)** is the blast-radius cap on each effect class; **strategic checkpoints (V2 §134)** are the event-sourced snapshots taken before any staged or irreversible action; **graceful degradation (V2 §141)** is the ordered fallback list of every contract above, which the action layer walks when a component fails: no component failing makes the system unsafe, only less capable, and the packet says which fallback was used.

---
# PART III — THE CONTRACT, THE BENCHMARKS, THE BUILD

## **41. The doubling ledger: V2 → V3**

Each row names a V2 capability, the V3 mechanism that replaces or formalizes it, and the amplification. **Derived** means the multiplier follows from a proposition in this document under its stated assumptions; **target** means it is a design target to be certified by Section 42; **qualitative** means V2 had no number and V3 has one, so no ratio exists.

| # | V2 capability | V3 mechanism | Amplification | Kind | Where |
|---|---|---|---|---|---|
| 1 | Objective: expected terminal level (§4) | Robust long-run growth rate (Def. 3.1) | In adverse cases the answer changes sign: the V2 objective takes a bet with $\mathbb E r=1.05$ under which 94.8% of paths are below their start after 200 steps and 99.986% after 1,000 (exact); V3 refuses it. In the worked decision of 3.6, V2 picks the policy that ruins 7.7% of futures | derived | 2.1–2.2, 3.6 |
| 2 | Ruin constraint by simulation count (§18) | Barrier certificate (Lundberg/Ville) | Certifying $\varepsilon=10^{-4}$ needs 30,000 full-horizon simulations by counting; the certificate needs none and holds over the whole ambiguity set | derived | 5.2 |
| 3 | "Kelly-inspired" sizing (§19) | Drawdown law $x^{2/c-1}$ and noise-adjusted fraction $c^*$ | At half-Kelly, 75% of the growth with 4× fewer halvings of wealth ($1/8$ vs $1/2$); position size follows from the ruin tolerance in closed form | derived | 5.3–5.4 |
| 4 | Adaptive discounting (§81) | Hazard-mixture (hyperbolic) kernel, time-consistent and identified from survival data; far horizon undiscounted (Blackwell) | Under the default shape-one prior matched at one year, year 15 weighs 1.8× and year 30 weighs 5.4× what V2's exponential default gives; a learned prior gives what the data say | derived for the default prior; data-set otherwise | 6.1–6.4 |
| 5 | Long-delay credit assignment (§27, §98) | Doubly-robust values on an unconfounded ledger; surrogate index; hindsight and counterfactual credit; sampled Shapley | Lag from decision to lesson falls from $H$ to $h$ permanently; a program shorter than $H$ resolves $r(L-h)$ lessons instead of none, and for $L>H$ the resolved count ratio is $(L-h)/(L-H)$ (3.8 at $L{=}20$, $H{=}15$, $h{=}1$), with bias $\le b$ | derived | 8.1–8.4 |
| 6 | Decision state machine (§27) | E-process-driven states | False resolution of a null decision $\le\alpha$ at any inspection time; a repeatedly inspected fixed-sample test has no such bound | derived | 8.5 |
| 7 | Anti-Goodhart proxy audit (§44) | Quantilizer; winner's-curse correction; Pinsker optimization budget; anytime-valid audit | Harm from a corrupted proxy capped at $1/q$ of base; over-rating capped at $\sigma\sqrt{2\ln n}$; halving $\sigma$ buys $n\to n^4$ search breadth; every side effect bounded by $\operatorname{range}\sqrt{B/2}$ | derived | 9.1–9.5 |
| 8 | Goal integrity (§105) | Signed manifest; preference-suite coverage bound; drift CUSUM; interruptibility | Admitted change disagrees with the owner on $\le\ln(1/\delta)/K$ of preferences ($\le1\%$ at $K=300$) | derived | 10.1–10.5 |
| 9 | Strategic coherence rule (§7.1) | Evidence thresholds with Ville bounds | False mission change $\le10^{-6}$ per episode of evidence before human keys | derived | 6.5, 10.1 |
| 10 | Optionality (§4, §60) | Empowerment in nats; Fano link to reachable futures | Undefined → defined, computable, zero in ruin | qualitative | 7 |
| 11 | Real options (§20) | McDonald–Siegel threshold; LSMC | Irreversible commitments wait for value $\beta_1/(\beta_1-1)$ times cost ($3.7\times$ at $\sigma=0.3$) | derived | 7.3, 28 |
| 12 | Long-lead capability detector (§21) | $P(\text{need before ready})=\int F_n\,dF_b$ | A question → a probability with a priced preparatory investment | derived | 28.1(iii) |
| 13 | Evidence integrity (§10) | Median (scalar) and median-of-means (vector, heavy tails) with breakdown points | Error $O(\sigma\varepsilon)$ for the median and $O(\sigma\sqrt\varepsilon)$ for median-of-means under contamination $\varepsilon$, vs unbounded for the mean | derived | 13.1 |
| 14 | Epistemic triangulation (§11) | Dawid–Skene over provenance roots | Copies no longer count as confirmations | qualitative | 14 |
| 15 | Regime detection, triggers (§46, §102) | CUSUM (minimax delay) and BOCPD | Delay $\approx\ln\text{ARL}_0/\operatorname{KL}$, provably minimal at the declared false-alarm rate | derived | 16.1 |
| 16 | Unknown-unknown search (§45) | Good–Turing missing mass | "How much have we never seen" becomes $N_1/n$ with an interval | derived | 17.1 |
| 17 | Multi-actor model (§13–14) | MaxEnt/Bayesian IRL; cognitive hierarchy; regret matching; Bayesian equilibrium; Lucas flag | Intent posterior with width; $O(\sqrt T)$ regret against any opponent | derived | 19–20 |
| 18 | Red team (§31) | Restricted Nash response | Exploitability bounded by a declared $\epsilon$ whatever the opponent | derived | 21.1 |
| 19 | Scenario engine (§16, §47) | Wasserstein reduction with error bound; DRO finite-sample guarantee | Objective error $\le L\cdot W_1$; out-of-sample guarantee at confidence $1-\beta$ | derived | 23.1, 3.4 |
| 20 | Historical replay (§48, §111) | Selection correction; block bootstrap | Survivor bias named and weighted out | derived | 24.1 |
| 21 | Calibration (§28) | Multicalibration; calibeating; Brier decomposition | Calibrated on every group of $\mathcal C$ at once, at no accuracy cost | derived | 31.1 |
| 22 | Strategic memory (§26, §142) | Successor features + GPI | Transfer to new preferences without re-planning, loss $\le\frac{2}{1-\gamma}(\phi_{\max}\min_j\|w-w_j\|+\epsilon)$ | derived | 32.1 |
| 23 | Ensemble, belief market, quorum (§67–68, §119) | Exponential weights; LMSR; $n_{\text{eff}}$ | Regret $\le\sqrt{(T/2)\ln N}$; market loss $\le b\ln N$; correlated quorum counted as $n/(1+(n-1)\rho)$ | derived | 36.1 |
| 24 | Compute economics (§117–118) | Value of computation; successive halving | Best of $n$ analyses in $O(n\log n)$ budget | derived | 35.1 |
| 25 | Attention as a resource (§137) | Rational inattention | Packet depth set by the owner's $\kappa$ | derived | 38.1 |
| 26 | Complexity tax (§138) | PAC-Bayes | Tax = bits, with a generalization bound | derived | 39.1 |
| 27 | MPC philosophy (§8) | Receding horizon with a horizon-wide barrier certificate, re-certified at every replan | The ruin bound computed at the start holds for the whole closed loop; a replan that cannot re-certify says so and returns the smallest restoring commitment, never a relaxed $\varepsilon$ | derived (and an explicit non-guarantee) | 27.1, R27.0 |
| 28 | Shadow prices, bottlenecks (§77–78) | KKT duals; max-flow/min-cut | Bottleneck = min cut; shadow price = $\partial\rho^*/\partial b_i$ | derived | 29.1 |
| 29 | Safety separation (§32) | Control barrier functions; stochastic barrier | Forward invariance, one inequality per ruin coordinate per action | derived | 40.1 |
| 30 | Benchmarks (§48–50) | Ten benchmarks | 3 → 10 | target | 43 |
| 31 | Acceptance criteria (§148) | 48 items | 24 → 48 | target | 44 |
| 32 | Mathematical kernel (§62) | 46 propositions with proofs or citations on the reward side, two new to this document; v5.1's 12 theorems retained on the engine side | 0 → 46 | qualitative | passim |
| 33 | Proxy audit cadence (§44) | Goodhart speed limit | The nats of optimization an audit cycle can absorb is now a formula, $\sum_k\sqrt{B_k}\le\Gamma\sqrt2/r_\eta$ | derived (new) | 9.4 |
| 34 | Learning from own decisions (§27, §145) | Lessons-before-the-horizon multiplier | A program shorter than its outcome horizon learns from $r(L-h)$ decisions instead of none | derived (new) | 8.4 |

---

## **42. The 2× capability contract**

### 42.1 Statement

**At equal compute, equal data and equal error guarantees, the V3 reward kernel MUST deliver a lower 95% confidence bound of at least 2.0 on the ratio of its score to the V2 baseline's score on every one of the ten benchmarks of Section 43, with a design target of 4.0.** The contract is certified by randomized ablation with Shapley attribution of the multiplier across V3 mechanisms, exactly as RSI v3 §68 certifies its production multiplier, and is reported as `UNMEASURED`, `IN_PROGRESS`, `INCONCLUSIVE`, `PASSED` or `FAILED` per benchmark (v5.1 §3). A release may ship before the contract is certified; it may not be labelled "V3-certified" until every benchmark reads `PASSED`.

### 42.2 The V2 baseline, pinned

The baseline is the V2 PRD implemented straightforwardly, and it is pinned so that it cannot be weakened after the fact:

```yaml
v2_baseline:
  objective: "max E[W_T]  (expected terminal level), ruin constraint checked by Monte Carlo count with rule-of-three"
  discount: "single exponential gamma per horizon, gamma_1y = 0.9"
  sizing: "full plug-in Kelly where applicable; otherwise equal-weight across candidates"
  credit: "outcome attributed to the last decision before it; decisions resolved when outcome observed; fixed-sample z-test at alpha, inspected every period"
  selection: "argmax over proxy; no over-rating correction; no optimization budget"
  integrity: "proxy audit on a fixed schedule; objective changes admitted on a point estimate"
  evidence: "plain mean of reports; sources counted, not rooted"
  regime: "fixed-window mean-shift test"
  actors: "best response to the point-estimate opponent model"
  scenarios: "N samples, no reduction, nominal probabilities"
  replay: "no selection correction"
  calibration: "global Platt scaling"
  memory: "re-plan from scratch on preference change"
  ensemble: "equal-weight average; sources counted"
  compute: "fixed analysis budget"
  safety: "post-hoc check of the planned action against the ruin set"
```

### 42.3 Where the multiplier comes from

The contract is on measured benchmark scores, but several of its components are derivable, and the derivations are the reason the floor is 2 and the target 4 rather than numbers chosen for effect.

| Benchmark | Mechanism | Status of the multiplier | Rationale |
|---|---|---|---|
| B4 Goodhart resistance | Quantilizer + budget (9.1–9.3) | **derived** for the declared world | With a proxy corrupted on a fraction $\pi_c$ of candidates where it over-rates by a margin $\Delta$ large against the proxy's spread, argmax selects a corrupted candidate with probability $\to1$ as $n$ grows (check 7: 0.99 at $n=200$); the $q$-quantilizer's expected loss is $\le\pi_c/q$ (Proposition 9.1); at $\pi_c=0.05$, $q=0.2$ the loss ratio is $\ge4$ |
| B10 Integrity | Coverage bound (10.2) | **derived** against the pinned baseline | An admitted change disagrees on $\le\ln(1/\delta)/K$ of the suite's distribution; the baseline's point-estimate admission has undetected rate equal to its proxy's error rate, so the ratio is $\ge2$ whenever that error exceeds $2\ln(1/\delta)/K$ (2% at $K=300$, $\delta=0.05$) |
| B5 Ruin under tail shocks | Fractional Kelly (5.3) | target | The pinned baseline (full plug-in Kelly) fails any drawdown tolerance below $1/2$ for halving, so growth at matched ruin is not defined for it; the comparison is against the smallest ad hoc de-risking that meets the tolerance, which 42.2 does not pin. Arithmetic for orientation: V3's $c=1/2$ keeps 75% of $g^*$ and the ratio exceeds 2 iff the baseline's de-risked fraction lands below $c=0.21$ |
| B6 Credit accuracy | Surrogate index + DR (8.2–8.4) | target | The surrogate removes $H-h$ years of lag and DR has no larger variance than IPS (check 6: 0.44×); the credit-error ratio depends on the world's $b$ and on how many decisions have resolved at scoring time (Proposition 8.4) |
| B2 Look around corners | CUSUM (16.1) | target | CUSUM's delay at a declared $\text{ARL}_0$ is minimax (Proposition 16.1); the fixed-window baseline's delay depends on its window, which 42.2 pins only as "fixed-window mean-shift test" |
| B3 Delayed reward | Hazard-mixture discount (6.4) | target | Under the default prior year-15 payoffs weigh 1.8× V2's; the realized growth ratio depends on the fraction of such decisions in the world family |
| B1, B7, B8, B9 | Composite | target | No single derived component |

Only B4 and B10 have derived multipliers, and only under the worlds and baseline stated. For every other benchmark the floor of 2 is a design target, chosen because the derived cases and the reference model's demonstrations (checks 1, 2, 10, 19) show the mechanisms are large where they bite. Where the certified multiplier falls below 2 for a benchmark, the benchmark's world family is the thing to declare honestly, not the multiplier to inflate.

### 42.4 Certification protocol

1. Freeze the ten world families (Section 43) and their seeds before any V3 run; register the V2 baseline of 42.2 by hash.
2. Run V2 baseline and V3 on common random numbers with at least $N=2{,}000$ paired worlds per benchmark; score each benchmark; compute the paired log-ratio and its 95% LCB by stationary block bootstrap (24.1(ii)) with $2{,}000$ resamples. At $N=2{,}000$ and a paired log-ratio standard deviation of $0.5$, the LCB resolves a true multiplier of $2.1$ as $\ge2$ with power above $0.9$.
3. Ablate the sixteen V3 mechanisms (the switches of Section 45, V3-01 to V3-16) in a randomized design; attribute the multiplier by sampled Shapley (8.4) with $M=8{,}000$ permutations, which bounds the attribution error for all sixteen mechanisms simultaneously by $R\sqrt{2\ln(2\cdot16/0.05)/8000}\approx0.04\,R$ at confidence $0.95$, $R$ being the range of the marginal contributions.
4. A benchmark `PASSED` only if LCB $\ge2$; `INCONCLUSIVE` if the interval contains 2; `FAILED` if the UCB $<2$.
5. Publish the unedited run record (RSI v3 §72's rule): the numbers in this document are reproduced by the record or the document is corrected.
6. No benchmark, world family, seed, baseline or scoring rule is changed after step 1 without a new certification from step 1; the change log is part of the record.

---

## **43. Benchmark suite**

V2 had three benchmarks (§48–50). V3 has ten. Each has a world family, a score, a V2 baseline procedure and a V3 procedure; all are scored on common random numbers and reported with intervals.

| ID | Name | World family | Score (higher is better) | What it tests |
|---|---|---|---|---|
| B1 | Historical replay, selection-corrected | Ledger histories and external records with information cutoffs and selection weights (24) | $1/\text{normalized regret}$ vs the best-known feasible policy; `survivor_biased` flag if unweighted | Can Athena have recommended well with what was knowable, without learning from survivors only |
| B2 | Look around corners | Synthetic worlds with planted regime shifts at random times; declared $\text{ARL}_0$ | Lead time gained (periods between detection and the shift's first material loss) | Early warning at a controlled false-alarm rate |
| B3 | Delayed reward | Worlds with payoffs at 1, 5, 15 and 30 years; the four fixture cases of 12.5 | Realized growth at year 30 (path median) and fraction of the four cases distinguished | Does the reward function actually prefer the far future when it should, and only then |
| B4 | Goodhart resistance | Worlds with a proxy corrupted on a fraction $\pi_c$ of candidates, under optimization pressure $B$ nats | True objective achieved / true optimum, at matched $B$ | How much a lying proxy can cost |
| B5 | Ruin under tail shocks | Growth worlds with fat-tailed shocks and a declared drawdown tolerance | Growth rate achieved at matched ruin/drawdown probability | Survival first, then growth |
| B6 | Credit assignment | Synthetic worlds with known causal ground truth, delayed outcomes and surrogates | $1/\text{mean absolute credit error}$ per decision; lessons resolved per simulated year | Does Athena learn the right lesson, and how soon |
| B7 | Adversarial calibration | Forecast sequences against an adaptive adversary that chooses outcomes after seeing forecasts | $1/\text{calibration error}$ per group in $\mathcal C$; Brier resolution | Is Athena calibrated where it matters, even against an opponent |
| B8 | Optionality retention | Worlds with corridors, hubs and dead ends (7.1) | Empowerment of the terminal state at matched growth | Does the plan keep the future open |
| B9 | Preference robustness | Worlds scored under every $\theta\in\Theta_\beta$ | $\min_{\theta}$ growth / $\max_\theta$ growth of the chosen plan | Does the plan survive the owner changing their mind within the credible set |
| B10 | Objective integrity | Synthetic attack suites: an engine proposing objective-side changes, a fraction adversarial | $1/\text{undetected-drift rate}$ at matched proposal volume | Can the engine move the aim |

**R43.1** B4, B6, B8, B10 are scored only in synthetic worlds (ground truth required). B1 and B7 are scored on real records with information cutoffs enforced by the leakage probe of 24. B3 and B5 are scored in both. **R43.2** Every world family carries a `sim2real_gap` estimate from the subset calibrated to history (25), and a benchmark result in a family with an unestimated gap is reported as `synthetic_only`.

---

## **44. Acceptance criteria**

The 24 V2 criteria (§148) are retained verbatim as A1–A24. V3 adds A25–A48. A production-quality Athena V3 demonstrates all 48; the first internal release (I0–I1 of v5.1 §4) demonstrates the subset marked *.

```text
V2 (retained)
[ ] A1  persistent multi-year decision memory *
[ ] A2  calibrated probabilistic forecasts *
[ ] A3  explicit uncertainty *
[ ] A4  resource conversion graph *
[ ] A5  capability lead-time modeling
[ ] A6  option valuation
[ ] A7  scenario ensembles *
[ ] A8  adversarial actor models
[ ] A9  causal/counterfactual reasoning
[ ] A10 tail-risk modeling *
[ ] A11 strategic trigger generation
[ ] A12 multi-horizon planning *
[ ] A13 historical replay
[ ] A14 synthetic-world evaluation
[ ] A15 multi-model routing
[ ] A16 model correlation awareness
[ ] A17 event-sourced auditability *
[ ] A18 RSI candidate generation
[ ] A19 independent RSI evaluation
[ ] A20 safe rollback *
[ ] A21 horizontal simulation scaling
[ ] A22 deterministic analytical tools *
[ ] A23 objective-drift detection
[ ] A24 human-readable and agent-readable outputs *

V3 (new)
[ ] A25 the objective reported is the robust growth rate, with the ergodicity flag and path median in every packet (2.1, 3.5) *
[ ] A26 the lexicographic level report is present in every packet and no level is silently scalarized (3.1, 3.5) *
[ ] A27 level-1 certificate is one of barrier / sampled / unresolved, never a stress-suite pass reported as a bound (5.2) *
[ ] A28 Kelly sizing reports the regime test and the fraction c with its drawdown probability (5.3)
[ ] A29 the least-favorable preference theta_dagger is reported in words (4.1) *
[ ] A30 discount kernels are hazard mixtures learned per capital line, with sensitivity at the 10th/90th hazard percentiles (6.1)
[ ] A31 the T8 head is average-reward; the discounted heads' limit is checked against it (6.3)
[ ] A32 the coherence ladder's thresholds are in the manifest and every objective-side change records its e-value (6.5, 10.1) *
[ ] A33 empowerment is computed for terminal states of candidate plans and reported in nats (7.1)
[ ] A34 every decision records its logging propensity and mu_min holds (8.1) *
[ ] A35 past decisions are valued doubly-robustly and the packet shows the IPS/DR variance ratio (8.2)
[ ] A36 every surrogate index is registered with surrogacy and comparability tests and a direct-effect bound b (8.3)
[ ] A37 Shapley credit, hindsight credit and counterfactual credit are reported and reconciled (8.4)
[ ] A38 the decision state machine is driven by e-processes; no decision resolves below 1/alpha (8.5) *
[ ] A39 unaudited candidate sets are selected by quantilizer with registered q; argmax only in audited sets (9.1) *
[ ] A40 selections report n, sigma_audited and the winner's-curse correction (9.2)
[ ] A41 KL optimization spent per epoch <= budget B; overspend is impossible by construction (9.3) *
[ ] A42 the audit e-process is on a filtration disjoint from the engine's (9.5) *
[ ] A43 the terminal manifest is immutable except by two-key ratification; invariants I1-I8 are checked in CI (10.6) *
[ ] A44 every admitted objective-side change passed K preference checks, K and delta recorded (10.3) *
[ ] A45 capability demands to the engine are denominated in shadow prices of robust growth (11.1)
[ ] A46 the four information cases of 12.5 are reproduced from the model, not from a bias
[ ] A47 n_eff, not n, is reported wherever strategists or sources are counted (14, 36.1)
[ ] A48 the ten benchmarks run on common random numbers with the V2 baseline pinned, and the contract status is published (42–43)
```

---

## **45. Build plan: the V3 reward kernel inside the v5.1 program**

The v5.1 Master PRD's phases A–H, releases I0–I5 and work packages WP-01–WP-62 stand. V3 adds sixteen work packages for the reward kernel, slotted into those phases. Each has an owner role, the propositions it implements, and a done-when that an agent can verify without reading the rest of this document. The reference model of Section 47 is the acceptance fixture for every package marked (RM): the package is done when its implementation reproduces the reference model's figures on the reference model's seeds.

| WP | Phase | Name | Implements | Done when |
|---|---|---|---|---|
| V3-01 | A | Capital vector and aggregator | 1.2–1.3 | registered units, estimators, decay processes for the six lines; Cobb–Douglas and CES aggregators with theta posterior; component growth decomposition tested |
| V3-02 | A | Terminal manifest and integrity invariants | 10.1, 10.6 | signed manifest; two-key ratification path; invariants I1–I8 as CI checks that fail on a planted violation |
| V3-03 | B | Decision ledger with propensities | 8.1 | every decision records b_t, pi_t, mu(a|b); mu_min enforced; replay reconstructs any past state bit-for-bit |
| V3-04 | B | E-process library (RM) | 8.5, 9.5, 10.1 | likelihood-ratio and betting e-processes; a planted null resolves at a rate <= alpha over 500 inspections (check 10); the naive test resolves it eight times as often (negative control D) |
| V3-05 | C | Growth objective and level report (RM) | 2.1–2.2, 3.1, 3.5 | CVaR by LP and by adversarial reweighting agree (check 3); ergodicity flag fires on the 1.5/0.6 world (check 1) |
| V3-06 | C | Ruin certificates and Kelly sizing (RM) | 5.1–5.4 | Lundberg bound verified against exact ruin on a random walk (check 11); drawdown law within Monte Carlo error (check 2); full Kelly fails the planted tolerance (negative control E) |
| V3-07 | C | Hazard-mixture discounting and value heads (RM) | 6.1–6.4 | Gamma-mixture kernel matches closed form; time-consistency identity holds; the 1.8×/5.4× table reproduced (check 4) |
| V3-08 | C | Empowerment (RM) | 7.1 | Blahut–Arimoto on the test world orders hub > corridor > dead end > ruin (check 12); variational estimator agrees on small worlds |
| V3-09 | D | Credit assignment (RM) | 8.2–8.4 | DR unbiased with wrong Q and exact mu (check 6); surrogate index inside its bound and the planted direct effect detected (check 5, control B); sampled Shapley inside its Hoeffding interval and efficient (check 21) |
| V3-10 | D | Quantilizer, winner's-curse correction, optimization budget (RM) | 9.1–9.3 | 1/q bound holds on planted corrupted proxies (check 7); Pinsker budget holds for random side functions (check 8) |
| V3-11 | D | Preference suite and drift detector (RM) | 10.2, 10.4, 16.1 | coverage bound reproduced (check 9); CUSUM delay within theory at declared ARL0 |
| V3-12 | E | Capability-demand interface | 11.1–11.2 | demands carry shadow prices; engine payment computed from Delta rho_alpha; a production increase that lowers rho_alpha is paid <= 0 |
| V3-13 | E | Audit stream isolation | 9.5, I4 | audit filtration provably disjoint (separate service, separate credentials); a planted leak fails CI |
| V3-14 | F | Robust aggregation, triangulation, missing mass (RM) | 13.1, 14, 17.1 | MoM error inside bound with planted adversaries (check 14); Good–Turing on Zipf (check 15) |
| V3-15 | F | Memory transfer (RM) | 32.1 | GPI bound holds on the test world (check 17) |
| V3-16 | G | Benchmarks and contract certification | 42–43 | ten world families frozen with seeds; V2 baseline pinned and reproduced; ablation design run; contract status published |

**Agent execution contract.** An agent claiming a V3 package: (1) reads only this document's sections for that package plus the reference model; (2) instantiates every assumption of the propositions it implements against the artifact and records which hold; (3) treats the reference model's figures as the acceptance test and the negative controls as required failures; (4) opens a PR with the run record attached; (5) never marks its own work accepted (AGENTS.md). Status values: `not_started`, `in_progress`, `blocked`, `in_review`, `done`.

---

## **46. Reconciliation with v5.1 and the companion specifications**

**With the v5.1 Master PRD.** v5.1 §67.1 called the unified system "Athena" and its engine "Athena RSI Fabric". In the three-part program this document belongs to, the engine is the RSI Fabric (v3.0, PR #262) and Athena is its reward function. Nothing in v5.1 is withdrawn: its theorems ATH-T01–T12, its algorithm contracts, its evidence classes, release states and statistical promotion rules remain in force for the *engine side* (verification, promotion, queue stability, capacity certification), and its "retained verified improvements per second" remains the engine's throughput metric. Where v5.1 and V3 overlap, V3 governs the *reward side*: the objective of v5.1 §11 ($\mathbb E[U]-\lambda\operatorname{CVaR}-\kappa C_{\text{coord}}$) is replaced by Definition 3.1 (which contains it: the CVaR term is level 2, the coordination cost is in the capital vector's attention and legitimacy lines, and the expectation is level 3); v5.1 §13's EVSI, timing and risk rules are retained and sharpened by Sections 12 and 28; v5.1's four headline targets (2× research efficiency, 50% faster decisions, 50% lower regret, 2× learning reuse) stay as program targets and the ten benchmarks of Section 43 are how the reward side's share of them is measured. The product releases I0–I5 and the 24-week reference plan stand, with Section 45's packages slotted in.

**With the RSI Fabric v3.** The engine produces at rate $P=\lambda y_P\delta$ and certifies its production multiplier and magnitude rungs; Athena pays for production in units of robust growth (11.2), sets demands with shadow prices (11.1), bounds the engine's optimization of any proxy by the Pinsker budget (9.3), and audits on a filtration the engine cannot see (9.5). The engine's governance envelope (RSI v3 §36–38, §42) and Athena's manifest (10.1) are both ratified by humans under Superman; neither is an RSI target.

**With Sideways and Ladder to Heaven.** Sideways is the always-on runtime; Ladder is the per-container improvement loop with fleet composition. Athena's value heads, ledger and audit are services on that runtime; the per-container loops consume capability demands (11.1) and return verified deltas; the fleet's compounding law (Ladder §compounding) is, in Athena's accounting, growth of the $C$ line, paid by 11.2 and bounded by Ladder's governor.

**With Superman.** Superman supplies $\Pi_{\text{adm}}$ (level 0), the effect classes and envelope of Section 40, the two keys of 10.1, the interrupt interface of 10.5 and the dead-man lease. Athena does not loosen the leash; it reports when the leash binds (an infeasibility certificate at level 0 goes to the owner as a question, never as a relaxed constraint).

---
## **47. The document checks itself: the reference model**

`docs/athena/v3/reference_model.py` is a self-contained Python program (3.10+, standard library only, no network) that checks every proposition in this document that admits a numerical check. Each check runs on its own seed derived from the base seed, so that any one check can be re-implemented and reproduced alone. Three checks carry **planted defects** that must be detected (B: a surrogate whose surrogacy fails; C: a doubly-robust estimator with both nuisances wrong; D: a fixed-sample test inspected repeatedly), and two carry **demonstrations that the V2 rule fails where the V3 rule does not** (A: the expected-level objective takes a bet that ruins almost every path; E: full Kelly violates a drawdown tolerance that half-Kelly meets). `docs/athena/v3/VALIDATION.md` describes each check; `docs/athena/v3/reference_results.json` is the unedited record of the run that produced the figures quoted in this document (seed 20261015, Python 3.13.16, 26.1 s). The rule is RSI v3 §72's: the document's numbers are reproduced by the record, or the document is corrected. Twenty-one checks passed; the three defects were detected and the two demonstrations held.

| # | Checks | Proposition | Recorded figure |
|---|---|---|---|
| 1 | Ergodicity gap | 2.1, 2.2 | $\mathbb E r=1.05$, $\mathbb E\ln r=-0.0527$; paths below start at $T=200$: 94.8% simulated, 94.82% exact; at $T=1{,}000$: 100% of 10,000 simulated, 99.986% exact; path median $2.7\times10^{-5}$; sample ensemble mean $6{,}065$ (theory $17{,}293$, carried by unsampled paths). **A:** the expected-level selector takes the bet; the growth selector refuses |
| 2 | Fractional Kelly drawdown law | 5.3 | $P(\text{halve})$ sim/theory: $c{=}1$: 0.500/0.500; $c{=}\tfrac12$: 0.123/0.125; $c{=}\tfrac14$: 0.0073/0.0078. Growth sim/theory: 0.126/0.125, 0.093/0.094, 0.055/0.055. **E:** full Kelly (0.50) violates the tolerance 0.2 that half-Kelly (0.12) meets; $c_{\max}=0.60$ |
| 3 | CVaR characterizations; entropic risk | 3.2, 3.3 | tail mean, variational and adversarial forms agree to $10^{-9}$ ($-0.1486$); the smallest of 300 random feasible reweightings is $+0.032$, above it; Donsker–Varadhan closed form equals the tilt's objective ($-0.0772$) and 50 random $Q$ are never below it |
| 4 | Hazard-mixture discounting | 6.1, 6.2, 6.4 | uniform mixture $=1/(1+t)$ to $5\times10^{-13}$; Gamma mixture closed form to $2\times10^{-9}$; time-consistency identity to $2\times10^{-9}$; far-future ratios 1.09 (5y), 1.36 (10y), **1.82 (15y), 5.44 (30y)** under the default prior |
| 5 | Surrogate index | 8.3 | long-run effect 0.80 estimated as $0.804\pm0.027$ from one-period surrogates. **B:** planted direct effect 0.5 produces bias $-0.46$ (bound 0.5) and the direct-effect test recovers 0.50 |
| 6 | Doubly robust credit | 8.2 | IPS bias 0.0016 (se 0.0019); DR with a wrong outcome model and exact propensities bias 0.0011 (se 0.0012); DR variance 0.44× IPS. **C:** both nuisances wrong: bias 0.087 (59 se) |
| 7 | Quantilizer; winner's curse | 9.1, 9.2 | over-rating of the selected candidate 1.10, 1.76, 2.29 for $n=10,100,1000$ against bounds 2.15, 3.03, 3.72; with 5% corrupted candidates, argmax pays cost 0.99 and the $q{=}0.2$ quantilizer 0.26 (bound 0.25 + Monte Carlo error) |
| 8 | Pinsker budget | 9.3 | max shift over 300 random bounded side functions plus the extremal one: 0.083, 0.182, 0.405 at $B=0.02,0.1,0.5$ nats (equal to the total variation, as it must be), against bounds 0.100, 0.224, 0.500 |
| 9 | Preference-suite coverage | 10.2 | $K=300$, $\delta=0.05$: candidates disagreeing above $\ln(1/\delta)/K=1.0\%$ pass at rate 0.0034 ($\le\delta$) |
| 10 | E-process resolution | 8.5 | false resolution over 500 inspections: e-process 0.039 ($\le\alpha=0.05$); mean resolution time under the alternative 25.5 (theory $\approx24$). **D:** the naive repeated $z$-test false-resolves 0.39 |
| 11 | Lundberg certificate | 5.1, 5.2 | unit steps, reserve 10: bound $=$ exact $=0.01734$, simulated 0.0180 (within Monte Carlo error); overshoot walk ($+1$/$-2$): $\vartheta=0.102$, bound 0.361, simulated 0.349 (strict) |
| 12 | Empowerment | 7.1 | hub $\ln5$, corridor $\ln3$, dead end $\ln2$, ruin 0 (exact); with 10% slip 1.15 > 0.76 > 0.47 > 0 |
| 13 | Real-option threshold; LMSR | 7.3, 28.1, 36.1(ii) | $\beta_1=1.368$, $V^*=3.72\,I$ by formula, $3.79\,I$ by dynamic program (1.9%); LMSR worst-case loss 16.09 at the bound $b\ln N=16.09$ (an identity of the cost function), against 81.7 for a constant-price market maker over the same volume |
| 14 | Robust aggregation; correlated quorum | 13.1, 36.1(iii) | 5% adversarial reports carry the mean to 51.0; median 1.13 and median-of-means 1.21 around the truth 1.0 (MoM bound 2.17 with the proof's constants); 50 strategists at $\rho=0.8$: averaged error variance 0.79 vs theory 0.804; $n_{\text{eff}}=1.24$ |
| 15 | Good–Turing | 17.1 | missing mass 0.294 (true) vs 0.278 (estimate) from 500 draws of a 2,000-category Zipf world |
| 16 | Exponential weights | 36.1(i) | regret 27.3 against the bound 48.0 over 2,000 rounds, 10 strategists |
| 17 | Successor features and GPI | 32.1 | GPI policy never below the best remembered policy (min margin $+0.008$); gap to optimal 0.023 against the transfer bound 14.7 |
| 18 | Coherence ladder | 10.1 | false-change rates 0.085 (tactics, bound 0.10) and 0.0085 (strategy, bound 0.01) |
| 19 | **The worked decision** | 3.6 | V2 selects A (expected level 2.46); A ruins 7.7% of futures; V3 rejects A at level 1 and selects B at level 2 ($-0.014$ vs C's $-0.021$, conditional on survival); B's terminal empowerment 1.42 nats on the declared kernel |
| 20 | Goodhart speed limit | 9.4 | ten epochs of 0.05 nats against a proxy with error range 0.96: realized gap by epoch 0.04, 0.09, …, 0.34, inside the running bound 0.15, 0.30, …, 1.52 at every epoch; for a gap tolerance of 0.10 over ten epochs the allowed budget is $2.2\times10^{-4}$ nats per epoch |
| 21 | Sampled Shapley | 8.4 | six decisions with interactions: max error 0.0046 against the simultaneous Hoeffding bound 0.33 at $M=2{,}000$; credit sums to the outcome to $10^{-9}$ |

**R47.1** A change to any proposition's statement or to any figure quoted from the model MUST be accompanied by a re-run with `--write` and a commit of the new record. **R47.2** The reference model is the acceptance fixture of every (RM) work package in Section 45. **R47.3** A check that cannot fail (an identity of the implementation rather than a test of the proposition) MUST say so in `VALIDATION.md` and carry a contrast that can fail, as checks 3, 8 and 13 now do.

---

## **48. Limits, falsification and known weaknesses**

### 48.1 Impossibility results the design respects

A specification that claims more than the mathematics allows is not world class; it is wrong. These are the limits Athena V3 is built around, each with the design response it forces.

| # | Limit | Source | Design response |
|---|---|---|---|
| L1 | Optimal planning under partial observability is PSPACE-hard for finite horizons and undecidable for infinite horizons | Papadimitriou–Tsitsiklis 1987; Madani–Hanks–Condon 2003 | The planner is approximate by necessity; every packet publishes its approximation scope (27.1(iii)), and exact computation is reserved for the deterministic core (36) |
| L2 | Without overlap, no effect is identified: if an action was never taken in a belief state, its counterfactual value there has no estimator, and the identified set is the whole range | Manski 1990; Rubin 1974 | $\mu_{\min}>0$ at every decision (R8.1.1); exploration is a cost of learning, priced by Section 12 |
| L3 | No sampling certificate of a ruin probability $\varepsilon$ at confidence $1-\delta$ uses fewer than $\ln(1/\delta)/\varepsilon$ failure-free trials | Clopper–Pearson 1934 | Barrier certificates (5.2); sampled certificates are labelled with their $n$ |
| L4 | For any proxy with nonzero error there are policies within any positive KL of the base whose Goodhart gap is of order $r_\eta\sqrt{B}$: Pinsker is tight up to a constant for small $B$ | Pinsker 1964; Tsybakov 2009 | The budget is necessary, not merely sufficient; the audit (9.5) measures the actual gap, which the bound only caps |
| L5 | Calibration does not imply skill: the base-rate forecaster is perfectly calibrated with zero resolution | Murphy 1973 | Scorecards report the Brier decomposition, never calibration alone (31.1(iv)) |
| L6 | Regret bounds are relative to the best *fixed* strategist in hindsight; nothing bounds loss against a comparator that adapts | Cesa-Bianchi–Lugosi 2006 | The league (37) grows the comparator class; the ensemble guarantee is stated as relative |
| L7 | An actor model estimated under one policy is not valid under another without structural assumptions | Lucas 1976 | The `lucas_unstable` flag (R20.1) and widened uncertainty sets |
| L8 | The value of information cannot be fully known before the information is acquired | Arrow 1962 | EVSI is model-based and reported with the model's own uncertainty (12.1); preference elicitation is priced the same way |
| L9 | A finite preference suite certifies agreement only on its own distribution; no finite suite certifies agreement everywhere | Vapnik–Chervonenkis 1971 (sample bounds are distribution-relative) | Coverage bound stated on the suite's distribution (10.3); suite refresh (10.4); optimization budget keeps policies near what the suite was written for (9.3) |
| L10 | A scalar objective that is optimized hard will eventually be gamed; no reward function is Goodhart-proof | Goodhart 1975; Campbell 1979; Manheim–Garrabrant 2018 | The reward is a lexicographic vector with a budgeted, audited proxy layer, not a scalar to maximize (3.1, 9) |
| L11 | Ergodic growth optimality requires stationarity; under regime change the growth-optimal policy of one regime is not that of another | Algoet–Cover 1988 (assumptions) | Regime detection (16) and regime-indexed doctrine forks (33) |
| L12 | Kelly's guarantees need repeated, fungible, measurable opportunities | Kelly 1956; v5.1 §13 | Regime test before Kelly sizing (R5.3.1); barrier-based limits elsewhere |
| L13 | A chance constraint certified at the start is not recursively feasible: a supermartingale barrier may rise on a realized step, and no general result makes a stochastic sublevel set forward invariant | Mayne et al. 2000 (deterministic tubes only); open in stochastic MPC | The certificate is horizon-wide from $s_0$ (27.1(i)) and re-certified at every replan; a replan that cannot certify says so (R27.0) |

### 48.2 What would falsify the central claims

| Claim | Falsifying measurement |
|---|---|
| The growth objective selects better than the expected-level objective (2, 3) | In the prospective pilot (v5.1 §2), the path-median strategic wealth of decision classes run under V3 recommendations is not higher than under V2-style recommendations at matched ruin tolerance, over at least three resolved classes |
| Hazard-mixture discounting is the right kernel (6) | The survival of plans and assets is not better predicted (log score) by the fitted mixture than by a constant hazard on held-out ledger data |
| Surrogate indices learn long-run effects early (8.3, 8.4) | Direct-effect tests on resolved outcomes find $b$ larger than the effects being estimated in the pilot's decision classes |
| The quantilizer and budget bound Goodhart damage (9) | An audited gap exceeds $r_\eta\sum\sqrt{B_k/2}$: impossible under the assumptions, so this would show the proxy error is not bounded by the recorded $r_\eta$ or the KL accounting is wrong |
| Empowerment is optionality (7) | The empowerment of chosen terminal states does not predict the size of the feasible set of the next planning cycle |
| The 2× contract (42) | Any benchmark's LCB below 2 under the certification protocol |
| Objective integrity (10) | A red-team engine (B10) moves an objective-side component past the preference suite with a disagreement rate above $\ln(1/\delta)/K$ |

### 48.3 Known weaknesses

1. **CVaR is tail-sensitive.** With few scenarios in the lower tail the level-2 estimate is noisy; the packet reports the number of scenarios in the tail and the alternative tail assumptions (v5.1 §13), and the Wasserstein radius (3.4) is conservative by design.
2. **The lexicographic slacks are a preference.** $\eta_2,\eta_3,\eta_4$ decide how much growth is traded for optionality and parsimony; they are in the manifest and their sensitivity is reported, but there is no theorem that picks them.
3. **Surrogacy is untestable before outcomes resolve.** Proposition 8.3's bound needs an estimate of $b$ from resolved history; a new decision class has none, and its surrogate index carries a declared prior $b$ until it does.
4. **Empowerment is expensive in large state spaces.** Blahut–Arimoto is exact only on small kernels; the variational estimator's error is not bounded, and level 4 is a tie-breaker for that reason.
5. **The Pinsker budget is loose.** It bounds the worst proxy error of a given range; typical gaps are smaller (check 20), so the budget under-uses the engine. The audit, not the bound, is the operating control.
6. **Successor-feature transfer assumes linear reward in known features.** Where the owner's preference change is not in the span of $\phi$, Proposition 32.1 does not apply and the fallback (re-plan) is used.
7. **Hazard priors are learned from the entity's own history,** which is short for a young entity; the Gamma prior's hyperparameters are then the owner's, and the packet says so.
8. **The ergodic objective assumes the entity lives one path.** For a portfolio owner who genuinely diversifies across many independent entities, the ensemble average is closer to the right criterion; the manifest can select expected growth at level 2 for such owners, and the ergodicity flag tells them which regime they are in.
9. **Human attention** ($\kappa$, Section 38) is estimated, not measured, and the packets may be too long or too short until it is.
10. **The benchmarks are synthetic where ground truth is needed** (B4, B6, B8, B10), and their world families may not contain the real world; every result carries its `sim2real_gap` (R43.2).

---

## **49. Foundations index**

Each entry is a result this document rests on, with where it is used. Prize years are given where the work was recognized by a Nobel memorial prize in economic sciences, because the program draws on that literature deliberately; they are not claims about the people.

**Growth and survival.** Kelly 1956, *Bell Syst. Tech. J.* (2.1, 5.3). Breiman 1961, *Proc. 4th Berkeley Symp.* (2.1). Algoet & Cover 1988, *Ann. Probab.* (2.1, L11). Peters 2019, *Nature Physics* (2.2). Thorp 2006, in *Handbook of Asset and Liability Management* (5.3). MacLean, Thorp & Ziemba 2011, *The Kelly Capital Growth Investment Criterion* (5.3). Lundberg 1903; Cramér 1930; Asmussen & Albrecher 2010, *Ruin Probabilities* (5.2). Ville 1939, *Étude critique de la notion de collectif* (5.1, 8.5, 10.1). Prajna, Jadbabaie & Pappas 2007, *IEEE TAC* (5.1, 40.1). Ames, Xu, Grizzle & Tabuada 2017, *IEEE TAC*; Ames et al. 2019, *ECC* (40.1). Broadie, Glasserman & Kou 1997, *Math. Finance* (check 2). Hanley & Lippman-Hand 1983, *JAMA* (5.2). Clopper & Pearson 1934 (L3).

**Risk, robustness and ambiguity.** Rockafellar & Uryasev 2000, *J. Risk* (3.2). Artzner, Delbaen, Eber & Heath 1999, *Math. Finance* (3.2). Hansen & Sargent 2008, *Robustness* (3.3; Hansen, 2013). Gilboa & Schmeidler 1989, *J. Math. Econ.* (4.1). Mohajerin Esfahani & Kuhn 2018, *Math. Program.*; Fournier & Guillin 2015 (3.4). Savage 1951, *JASA* (3.3, 30). Ben-Haim 2006, *Info-Gap Decision Theory* (30). Lempert, Popper & Bankes 2003, RAND (30). Altman 1999, *Constrained Markov Decision Processes* (3.1). Bäuerle & Ott 2011, *Math. Methods Oper. Res.*; Chow, Tamar, Mannor & Pavone 2015, *NeurIPS* (3.1, CVaR state augmentation). Wray, Zilberstein & Mouaddib 2015, *AAAI* (3.1). Markowitz 1952, *J. Finance* (29.1; 1990). Mayne, Rawlings, Rao & Scokaert 2000, *Automatica*; Rawlings, Mayne & Diehl 2017, *Model Predictive Control* (27.1, L13).

**Time.** Samuelson 1937, *Rev. Econ. Stud.* (6.1; 1970). Sozou 1998, *Proc. R. Soc. B* (6.1). Fedus, Gelada, Bengio, Bellemare & Larochelle 2019 (6.1, 6.2). Laibson 1997, *QJE*; Thaler 1981, *Econ. Lett.* (6.1; Thaler, 2017). Blackwell 1962, *Ann. Math. Stat.* (6.3, Proposition 6.4). Mahadevan 1996, *Mach. Learn.*; Puterman 1994 (6.3). Hausdorff 1921; Shohat & Tamarkin 1943; Elbers & Ridder 1982, *Rev. Econ. Stud.*; Heckman & Singer 1984, *Econometrica*; Laird 1978, *JASA* (Proposition 6.3). Kydland & Prescott 1977, *JPE* (10.2; 2004). McDonald & Siegel 1986, *QJE*; Dixit & Pindyck 1994, *Investment under Uncertainty* (7.3, 28.1). Longstaff & Schwartz 2001, *Rev. Fin. Stud.* (28.1). Black & Scholes 1973; Merton 1973 (option value; Merton and Scholes, 1997).

**Information and optionality.** Klyubin, Polani & Nehaniv 2005, *CEC*; Salge, Glackin & Polani 2014 (7.1). Blahut 1972; Arimoto 1972, *IEEE TIT* (7.1). Mohamed & Rezende 2015, *NeurIPS* (7.1). Fano 1961 (7.1). Howard 1966, *IEEE TSSC*; Raiffa & Schlaifer 1961 (12.1). Frazier, Powell & Dayanik 2008, *SIAM J. Control Optim.* (12.2). Russo & Van Roy 2014/2018, *NeurIPS*/*Oper. Res.* (12.3). Arrow 1962, "Economic welfare and the allocation of resources for invention" (L8; 1972). Sims 2003, *J. Monet. Econ.* (38.1; 2011). Good 1953, *Biometrika*; McAllester & Schapire 2000, *COLT* (17.1).

**Credit and causation.** Rubin 1974, *J. Educ. Psychol.*; Imbens & Rubin 2015 (8.1; Imbens, 2021). Pearl 2009, *Causality* (8.1, 8.4). Dudík, Langford & Li 2011, *ICML*; Jiang & Li 2016, *ICML*; Thomas & Brunskill 2016, *ICML* (8.2). Athey, Chetty, Imbens & Kang 2019, NBER WP 26463 (8.3). Prentice 1989, *Stat. Med.* (8.3). Harutyunyan et al. 2019, *NeurIPS* (8.4). Mesnard et al. 2021, *ICML* (8.4). Castro, Gómez & Tejada 2009, *Comput. Oper. Res.*; Shapley 1953 (8.4, 22). Murphy 1973, *J. Appl. Meteorol.* (31.1, 34). Efron & Morris 1975, *JASA* (9.2, 34). Heckman 1979, *Econometrica* (24.1; 2000). Horvitz & Thompson 1952, *JASA* (24.1). Politis & Romano 1994, *JASA* (24.1). Angrist & Imbens 1994, *Econometrica* (identification; Angrist and Imbens, 2021). Howard, Ramdas, McAuliffe & Sekhon 2021, *Ann. Stat.*; Ramdas, Grünwald, Vovk & Shafer 2023, *Stat. Sci.* (8.5, 9.5). Wald 1945 (6.5). Manski 1990, *AER P&P* (L2).

**Goodhart and integrity.** Taylor 2016, "Quantilizers", AAAI Workshop (9.1). Pinsker 1964; Tsybakov 2009 (9.3, L4). Gao, Schulman & Hilton 2023, *ICML* (9.3). Manheim & Garrabrant 2018 (L10). Goodhart 1975; Campbell 1979 (L10). Hadfield-Menell, Milli, Abbeel, Russell & Dragan 2017, *NeurIPS* (9.4 context). Orseau & Armstrong 2016, *UAI* (10.5). Soares, Fallenstein, Yudkowsky & Armstrong 2015, AAAI Workshop (10.5). Page 1954, *Biometrika*; Lorden 1971, *Ann. Math. Stat.*; Moustakides 1986, *Ann. Stat.*; Adams & MacKay 2007 (10.4, 16.1). Vovk 2021 (16). McAllester 1999, *COLT*; Maurer 2004 (39.1). Rissanen 1978, *Automatica* (39). Vapnik & Chervonenkis 1971 (L9).

**Actors.** Ng & Russell 2000, *ICML*; Ramachandran & Amir 2007, *IJCAI*; Ziebart, Maas, Bagnell & Dey 2008, *AAAI* (19.1). Kahneman & Tversky 1979, *Econometrica* (19; Kahneman, 2002). Thaler 1985, *Marketing Sci.* (19). Camerer, Ho & Chong 2004, *QJE* (20.1). Hart & Mas-Colell 2000, *Econometrica* (20.1). Aumann 1974, *J. Math. Econ.*; 1987, *Econometrica* (20.1; 2005). Harsanyi 1967–68, *Manag. Sci.* (20.1; 1994). Nash 1950, *PNAS* (20; 1994). Lucas 1976, *Carnegie-Rochester Conf.* (L7, R20.1; 1995). Schelling 1960, *The Strategy of Conflict* (16, 28; 2005). McCracken & Bowling 2004, AAAI Fall Symp.; Johanson, Zinkevich & Bowling 2007, *NeurIPS* (21.1). Crawford & Sobel 1982, *Econometrica* (18). Akerlof 1970, *QJE*; Spence 1973, *QJE* (18; Akerlof, Spence and Stiglitz, 2001). Ostrom 1990, *Governing the Commons* (22; 2009). Simon 1955, *QJE* (bounded rationality; 1978).

**Evidence and estimation.** Huber 1964, *Ann. Math. Stat.* (13.1). Lugosi & Mendelson 2019, *Found. Comput. Math.*; Lecué & Lerasle 2020, *Ann. Stat.* (13.1). Diakonikolas, Kamath, Kane, Li, Moitra & Stewart 2019, *SIAM J. Comput.* (13.1). Dawid & Skene 1979, *Appl. Stat.* (14). Åström 1965; Smallwood & Sondik 1973; Kaelbling, Littman & Cassandra 1998; Pineau, Gordon & Thrun 2003; Silver & Veness 2010 (15). Papadimitriou & Tsitsiklis 1987, *Math. Oper. Res.*; Madani, Hanks & Condon 2003, *Artif. Intell.* (L1). Foster & Vohra 1998, *Biometrika*; Hébert-Johnson, Kim, Reingold & Rothblum 2018, *ICML*; Foster & Hart 2023, *Theor. Econ.*; Gneiting & Raftery 2007, *JASA* (31.1). Dupačová, Gröwe-Kuska & Römisch 2003, *Math. Program.*; Römisch 2003 (23.1). Tobin et al. 2017, *IROS* (25).

**Memory, ensembles and compute.** Dayan 1993, *Neural Comput.*; Barreto et al. 2017, *NeurIPS* (32.1). Sutton, Precup & Singh 1999, *Artif. Intell.* (27). Freund & Schapire 1997, *JCSS*; Cesa-Bianchi & Lugosi 2006, *Prediction, Learning, and Games* (36.1, L6). Hanson 2003, *Inf. Syst. Frontiers*; 2007, *J. Prediction Markets* (36.1). Bradley & Terry 1952; Herbrich, Minka & Graepel 2007 (37). Russell & Wefald 1991, *Artif. Intell.*; Hay, Russell, Tolpin & Shimony 2012, *UAI* (35.1). Jamieson & Talwalkar 2016, *AISTATS*; Li et al. 2018, *JMLR* (35.1). Kuhn & Tucker 1951; Milgrom & Segal 2002, *Econometrica* (29.1). Ford & Fulkerson 1956, *Canad. J. Math.*; Goldratt 1984 (29.1). Romer 1990, *JPE* (2.3; 2018); Solow 1957, *Rev. Econ. Stat.* (1987); Arrow 1962, *Rev. Econ. Stud.* (26).

---

## **50. Traceability: V2 → V3**

Every V2 section keeps its meaning. The table gives the V3 section that formalizes or carries it.

| V2 | Subject | V3 |
|---|---|---|
| 1–3 | Executive summary, mission, core abstraction | 0, 0.1, 2 |
| 4 | Primary objective | 2, 3 (Definition 3.1) |
| 5 | Resource model, productivity, conversion graph | 1.2, 1.3, 29 |
| 6 | Delayed gratification | 3.4, 3.6, 6 |
| 7 | Temporal architecture; coherence rule | 6.2, 6.5, 10.1 |
| 8 | Model predictive strategic control | 27 |
| 9 | Partial observability | 15 |
| 10–11 | Evidence integrity; triangulation | 13, 14 |
| 12 | First-principles engine | 36 (deterministic core) |
| 13–15 | Multi-actor model; inverse utility; formal rules vs reality | 19, 20, 18 |
| 16–17 | Scenario engine; robust policy selection | 23, 27, 3.3 |
| 18–19 | Ruin engine; Kelly allocation | 5, 29 |
| 20–21 | Real options; long-lead capability detector | 7.3, 28 |
| 22–24 | Value of information; exploration; timing | 12, 28 |
| 25–26 | Framework library; strategic memory | 36, 32 |
| 27 | Long-delay credit assignment | 8 |
| 28–31 | Calibration; counterfactual, contrarian, red-team engines | 31, 34, 21 |
| 32 | Safety / agency separation | 40 |
| 33–37 | Cognitive modules; modular architecture; scalability; multi-model; RSI-native | 36, 39, 23, 36, 11 |
| 38–40 | RSI loop; multi-speed RSI; self-improvement portfolio | 11, RSI v3 |
| 41–43 | Doctrine; decision output; scorecard | 33, 3.5, 31 |
| 44–46 | Anti-Goodhart; unknown unknowns; regime detection | 9, 17, 16 |
| 47–50 | Simulation; the three benchmarks | 23, 24, 43 (B1–B3) |
| 51–54 | Infrastructure; agent interface; observability; deep changes | Sideways/Ladder; 40; 47; 39 |
| 55–57 | MVP, V1, V2+ | 45 (with v5.1 I0–I5) |
| 58–59 | Athena's own compute; flywheel | 29, 35; 2.3, 11 |
| 60–63 | North star; system definition; algorithm stack; maxim | 3.1 (why this order), 0.1, 49, 51 |
| 64 | Power expansion layer | Part II |
| 65–66 | Digital twin; knowledge graph | 26 |
| 67–69 | Belief market; ensemble; tournaments | 36, 37 |
| 70–73 | Pareto; regret; deep uncertainty; entropy | 30, 3.3 |
| 74–80 | Reversibility; path dependence; compounding; bottleneck; shadow price; capital allocation; temporal arbitrage | 28, 30, 2.3, 29, 29, 29, 28 |
| 81–83 | Adaptive discounting; time-to-capability; latency | 6, 26, 28 |
| 84–88 | Early warning; signal vs noise; deception; nth-order effects; equilibrium shift | 16, 13, 18, 30, 20 |
| 89–93 | Power graph; legitimacy; reputation; human behavior; organizational distortion | 22, 1.2, 22, 19, 13 |
| 94–98 | Self-critique; pre- and post-mortem; luck/skill; temporal credit graph | 34, 8.4 |
| 99–105 | Policy tree; portfolios; contingent strategies; triggers; cascade; drift; goal integrity | 27, 16, 6.2, 10.4, 10 |
| 106–110 | RSI module evolution; RSI scientist; evaluator; self-generated benchmarks; curriculum | 11, RSI v3; 25; 33 |
| 111–113 | Time machine; synthetic worlds; league | 24, 25, 37 |
| 114–116 | Doctrine distillation; forking; reflection | 33 |
| 117–121 | Compute economics; reasoning depth; quorum; correlation; failure map | 35, 36 |
| 122–125 | Provenance; memory tiers; decay; event sourcing | 14, 32, 1.1 |
| 126–127 | Deterministic core; neuro-symbolic orchestration | 36 |
| 128–134 | Agent contracts; DAG; scheduler; scaling; simulation fabric; containment; checkpoints | 40, 27, 29, 23, 40 |
| 135–138 | Multi-entity; internal markets; attention; complexity tax | 20, 29, 38, 39 |
| 139–142 | Robustness vs optimality; antifragility; degradation; identity | 30, 40, 32 |
| 143–145 | Success function; meta-objective; 15-year loop | 3.1, 3.5; 11; 51.1 |
| 146–150 | Release philosophy; non-goals; acceptance; final principle; prime directive | 45; 48; 44; 3.1; 51.2 |

---

## **51. The loop and the directive**

### 51.1 The fifteen-year compounding loop, V3

```text
OBSERVE WORLD ............ robust aggregation (13), triangulation over roots (14), missing mass (17)
      ↓
UPDATE BELIEFS ........... belief filter (15), regime detector (16), deception-aware sources (18)
      ↓
MODEL THE OTHERS ......... intent posteriors (19), equilibria and the Lucas flag (20), safe exploitation (21)
      ↓
GENERATE FUTURES ......... scenario ensemble with reduction bound (23), replay with selection weights (24), twin (26)
      ↓
SCORE THE FUTURES ........ the Athena Functional: admissible → survive → robust growth → growth → options → parsimony (3)
      ↓                    under hazard-mixture time weights (6) and the least favourable preference (4)
IDENTIFY OPTIONS ......... empowerment (7), real-option thresholds and lead-time rule (28)
      ↓
ALLOCATE RESOURCES ....... shadow prices and min-cuts (29), Kelly fractions where they apply (5.3), VoI vs action (12)
      ↓
BUILD CAPABILITIES ....... capability demands to the engine in units of robust growth (11), inside a Goodhart budget (9)
      ↓
EXECUTE .................. the authorized first step, projected onto the barrier-certified admissible set (27, 40)
      ↓
OBSERVE CONSEQUENCES ..... surrogates at h, outcomes at H (8.3); e-process resolution, never premature (8.5)
      ↓
ASSIGN DELAYED CREDIT .... doubly robust values, hindsight and counterfactual credit, Shapley (8); luck/skill (31, 34)
      ↓
UPDATE DOCTRINE .......... distillation under the coherence ladder (33, 6.5); forks by regime; memory in successor features (32)
      ↓
AUDIT THE PROXIES ........ independent audit e-process (9.5); drift CUSUM (10.4); preference suite (10.3)
      ↓
IMPROVE ATHENA ........... the engine improves the estimators, never the manifest (10, 11)
      ↓
REPEAT ................... the far-horizon criterion is a rate (6.3); a rate has no finish line
```

### 51.2 The Athena V3 maxim

> Measure growth, not level.
> Certify survival; do not count it.
> Weigh the far future by what you know of the hazard, and let plans that survive be worth more.
> Keep the preference you are least sure of in the objective, not out of it.
> Keep the future open, and measure how open.
> Credit decisions by what they caused, through what they caused first.
> Resolve nothing before the evidence does.
> Give the engine a proxy, a budget and an audit it cannot see.
> Never let the engine write the aim.
> Say what you cannot know, and price what you can learn.
> Improve the strategist as relentlessly as the strategy — and prove it against the version before.

### 51.3 Prime directive, V3

The fifteen lines of V2 §150 stand unchanged. V3 adds five:

> Prefer the policy whose worst decade is best.
> Build what you will wish you had begun, and know the probability you are already late.
> Spend optimization like money: budgeted, audited, replenished only when the audit clears.
> Report every level; scalarize nothing in silence.
> Where a theorem's assumptions do not hold, say so in the packet, and use the fallback.

END OF PROJECT ATHENA PRD — VERSION 3.0 (FABLE MAX REMAKE)
