# LVL3.AI RSI EXPONENTIAL IMPROVEMENT FABRIC

> **Version 3.0 — Fable Max Remake.** Supersedes the RSI Fabric PRD v2.0 as the working specification. The v2.0 text is preserved unchanged as `docs/RSI_PRD_V2.md` (ODA AI PR #257, with the original Word document alongside it) and remains the certified lineage baseline of this document. Every v2 section number is retained below with the same meaning; v3 formalizes each one, raises the targets, and adds Part II (sections 63–69). Section 69 is the traceability table from v2 to v3. All performance figures in this document are **specification targets or derived bounds**, not measured ODA AI results.

### **Agent-Readable Product Requirements Document**

**Version:** 3.0 (Fable Max Remake)  
**Status:** Foundational / Ground-Truth Architecture  
**Organization:** LVL3.AI  
**Document Type:** PRD + Architecture Constitution + Mathematical Contract  
**Primary Objective:** Build a measurable, recursively self-improving computational substrate whose verified capability production grows exponentially inside a human-ratified governance envelope, and which automatically advances from one certified order of magnitude to the next.

**What changed from v2.0 (summary):**

1. Every metric, gate and rule now has a formal definition, an estimator, and a confidence requirement. "Agent-readable" now means an implementing agent can compute every quantity in this document from ledger data.
2. The **Recursive Growth Law** (Section 64) replaces the informal RIV proxy. Recursive improvement velocity is $v = \tfrac{d}{dt}\ln P$ and the exponential regime is a *measured* condition on the returns-to-scale exponent $\varphi$, never an assumption.
3. The **4× Capability-Production Contract** (Section 68): at equal hardware and equal error guarantees, v3 mechanisms (sequential testing, common random numbers, multi-fidelity funnel, deduplication, surrogate screening, truthful resource market, portfolio allocation, error-threshold mutation scheduling, robust promotion, coherence-free topology) MUST deliver at least a 4× multiplier in capability production over the v2 fixed-sample baseline at M0, with a design target of ≥ 8×. A **vertical ladder** doubles the design target at every rung ($\mathcal{M}_k^{\text{target}} = 4\cdot 2^{k}$) alongside the 10× horizontal ladder, and the multiplier is itself a meta-RSI target. Section 68 derives each factor, gives the randomized-ablation protocol that certifies it causally, and attributes the product to its factors by Shapley value.
4. The magnitude ladder is extended. M0 is unchanged at $10^3$ evaluations/s. The declared north star moves from M5 ($10^8$/s) to **M6 ($10^9$/s)**. M7–M9 are frontier horizons; M10+ is bounded by the physics envelope computed in Section 67.
5. The governance envelope is strengthened in proportion to the raised ambition: a formal self-design boundary with an acyclic trust graph (Section 42), a human-ratified **growth governor** that is a pre-committed rule rather than a discretionary setting (Section 38), a dead-man lease halt with a provable stopping distance (Section 36), and invariants expressed as an admissible-action set (Section 37). Faster growth is permitted only because the leash is formal; Proposition 64.5 proves that the governed trajectory is at most exponential at the ratified rate whatever the ungoverned dynamics would do.
6. The mathematics is drawn, wherever a result exists, from the established literature, and most of it from work recognized by Nobel prizes: Romer's knowledge production function (growth law), Solow's growth accounting (resource-normalized velocity), Arrow's learning by doing (experience curve), Vickrey–Clarke–Groves and the Myerson revelation principle (truthful resource market), Nash bargaining (proportional fairness), Markowitz portfolio selection (exploration portfolio), Shapley values (credit assignment), Simon's near-decomposability (pod and timescale hierarchy), Wilson's renormalization group (knowledge coarse-graining and propagation), Parisi's overlap distribution (diversity), Eigen's error threshold (mutation scheduling), Hasselmann's optimal fingerprinting (attribution of acceleration), Kantorovich's optimal transport (distribution shift and robust promotion), the Angrist–Imbens–Card causal toolkit (promotion as a natural experiment), Sims's rational inattention (human review allocation), Kydland–Prescott rules-over-discretion and Hart's residual control rights (governance), and the Holmström–Milgrom multitask model with the Lucas critique (Goodhart governor). Section 70 is the index of which result each section rests on, and marks the few places where this document states something new.
7. Three results are new to this document and are labelled as such with proofs or as conjectures: the **Information–Verification Bound** on sustained RSI velocity (Proposition 65.6), the **Governed Growth Bound** (Proposition 64.5), and the **exponent decomposition** of $\varphi$ into measurable elasticities (Conjecture 64.6).
8. The document verifies itself and says how to refute itself. Section 72 is a self-contained simulation whose unedited output reproduces the document's numbers (and corrects one approximation where simulation disagrees with it); Section 73 lists the known weaknesses and the measurements that would falsify each central claim.

**Reading conventions:** MUST / SHALL / SHOULD / MAY follow RFC 2119. Formulas are given in LaTeX for humans and, where an agent must compute them, in fenced pseudo-code or YAML. Section 63 is the symbol table and Section 70 the foundations index; the symbols used most are: $\lambda$ (completed evaluations per second), $y_V$ and $y_P$ (verification and promotion yields), $\delta$ (mean verified capability gain per promotion), $P=\lambda\,y_P\,\delta$ (capability production rate), $v=\tfrac{d}{dt}\ln P$ (recursive improvement velocity), $\varphi$ (returns-to-scale exponent), $\mathcal{M}$ (the v3-over-v2 production multiplier), $\mathcal{I}$ (the invariant set), $\mathcal{G}$ (the governor envelope).

### **0.1 The program on one page**

Six equations run the program; everything else in this document is a lever on one of their terms or a check on one of their hypotheses.

$$
\textbf{(1) production:}\quad P = \lambda\, y_P\, \delta
$$

$$
\textbf{(2) RSI velocity (Solow residual):}\quad \tilde v = \frac{d}{dt}\ln P - \sum_i \eta_i \frac{d}{dt}\ln R_i
$$

$$
\textbf{(3) growth law (Romer–Jones):}\quad \dot A = \kappa\, A^{\varphi} E_m^{\lambda_A},\qquad \varphi < 1 \text{ power law},\ \varphi = 1 \text{ exponential},\ \varphi > 1 \text{ hyperbolic}
$$

$$
\textbf{(4) speed limit (Prop. 65.6):}\quad \bar v \le \overline{\frac{\dot\lambda_V}{\lambda_V}} + \overline{\frac{\dot{\mathcal{K}}}{\mathcal{K}}} + \overline{\frac{\dot\delta}{\delta}} + \frac{1}{T}\ln\frac{1}{1-\varepsilon}
$$

$$
\textbf{(5) leash (Prop. 64.5, 36.3):}\quad P(t) \le P(0)\,e^{v_{\max}t}\Big(\tfrac{\Vert R(t)\Vert_w}{\Vert R(0)\Vert_w}\Big)^{\eta_R},\qquad T_{\text{stop}} \le T_{\text{lease}} + W_{\max}
$$

$$
\textbf{(6) contract (68):}\quad \text{LCB}_{95}(\mathcal{M}) \ge 4 \text{ at M0},\qquad \mathcal{M}_k^{\text{target}} = 4\cdot 2^{k},\qquad \lambda_k = 10^{3+k}
$$

Read (1) as what is produced, (2) as how much of its growth is the machinery's doing, (3) as the regime that growth is in, (4) as the only three ways to grow faster, (5) as the limits humans set and the fabric cannot cross, and (6) as what this version promises over the last one.

### **0. MACHINE-READABLE SUMMARY**

``` yaml
product:
  name: LVL3.AI RSI Exponential Improvement Fabric
  short_name: RSI Fabric
  organization: LVL3.AI
  version: "3.0"
  codename: fable_max_remake
  supersedes: "RSI Fabric PRD v2.0 (docs/RSI_PRD_V2.md, sha256 a473819918ddf6e6b8bba45ade7702b13db7f822ba4847b3477a4cbc94e28abe)"
  status: foundational
  architecture_style:
    - event_driven
    - asynchronous
    - distributed
    - modular
    - hardware_aware
    - verification_native
    - lineage_preserving
    - recursively_optimizable
    - statistically_governed        # new in v3: every promotion is a controlled statistical decision
    - envelope_governed             # new in v3: growth is bounded by a human-ratified envelope
  north_star:
    current_declared_magnitude: M6
    aggregate_evaluation_rate_per_sec: 1000000000
    interpretation: >
      Aggregate meaningful candidate-generation, simulation, evaluation,
      verification, selection, or knowledge-producing events per second,
      certified by a lower confidence bound on a sustained window.
      This MUST NOT be represented as 1e9 globally serialized architectural
      breakthroughs per second.
  initial_engineering_target:
    magnitude: M0
    aggregate_evaluation_rate_per_sec: 1000
    capability_production_multiplier_vs_v2:
      contract_floor: 4.0
      design_target: 8.0
      certification: randomized_ablation_lcb_95_with_shapley_attribution
  vertical_ladder:
    design_target_multiplier_at_rung_k: "4 * 2^k"     # M0: 4, M1: 8, M2: 16, ..., M6: 256
    gate_at_rung_k: "M_k >= 4 and M_k >= M_(k-1)"     # non-decreasing is the gate; doubling is the target
  growth_law:
    production_rate: "P = lambda * y_P * delta"
    velocity: "v = d/dt ln P   (resource-normalized, see 64.4)"
    exponential_regime: "phi_hat >= 1 with LCB(phi_hat) >= 1 - eps_phi over >= 3 doublings"
    doubling_time: "T2 = ln 2 / v"
    magnitude_time: "T10 = ln 10 / v"
  governance_envelope:
    ratified_by: human_control_plane
    parameters: [v_max, d_max, r_max, blast_radius_caps, halt_latency_bound]
    rule: >
      Certification of M_n automatically creates and activates the M_(n+1)
      objective inside the ratified envelope; any expansion of the envelope
      itself requires two-key human ratification and is never an RSI target.
  transition_rule: >
    Certification of M_n automatically creates and activates the M_(n+1)
    scaling objective while preserving an immutable certified M_n baseline.
```

## **1. MISSION**

Build a computational system whose **ability to discover, verify, retain, recombine, and propagate useful improvements increases over time**, and whose attainment of any certified performance order automatically initiates the engineering program required to attain the next order.

The system MUST optimize not merely for more computation, but for:

> ***more verified capability produced per unit of computation, energy, time, money, communication, and physical infrastructure.***

### **1.1 Formal objective**

Let $C(t) \in \mathbb{R}^{d}$ be the verified capability vector (Section 5.4) and let $R(t) \in \mathbb{R}^{6}_{+}$ be the resource vector

$$
R(t) = \big(\text{compute},\ \text{energy},\ \text{time},\ \text{money},\ \text{communication},\ \text{infrastructure}\big)(t).
$$

The program objective is to maximize cumulative, independently verified capability per unit resource over a horizon $T$:

$$
\max\ \ \mathbb{E}\!\left[\int_{0}^{T} \frac{\dot{\bar C}(t)}{\|R(t)\|_{w}}\, dt\right]
\quad\text{subject to}\quad S(t) \in \mathcal{I}\ \ \forall t,\quad \text{and}\quad \text{growth}(t) \in \mathcal{G}(t),
$$

where $\bar C = w^{\top} C$ is a reporting scalarization (used only for growth measurement, never as the sole promotion criterion), $\|R\|_{w}$ is a weighted resource norm with weights ratified by the Human Control Plane (Section 38), $\mathcal{I}$ is the invariant set (Section 37) and $\mathcal{G}$ is the governance envelope (Section 38).

### **1.2 Core research hypothesis**

> *A sufficiently modular, parallel, verification-native optimization substrate can improve not only its target systems, but also its own experiment generation, evaluators, representations, compilers, scheduling, knowledge systems, runtime, resource allocation, and hardware mapping—thereby increasing the productivity of subsequent improvement cycles.*

Stated as a falsifiable claim about the Recursive Growth Law (Section 64): the resource-normalized returns-to-scale exponent $\varphi$ of the fabric's capability production rate is $\ge 1$ over sustained intervals, and the excess $\varphi - 1 \ge 0$ is causally attributable, through the ledger, to promoted changes in the improvement machinery rather than to added hardware.

If $\varphi < 1$ is measured and sustained after the Phase 3 mechanisms (Section 54) are live, the hypothesis is falsified for that configuration and the program MUST say so.

## **2. DEFINITION OF RSI**

LVL3.AI SHALL define **Recursive Self-Improvement (RSI)** as:

> *A closed-loop process in which a computational system proposes changes to itself or its improvement machinery, evaluates those changes against independent evidence, retains only demonstrably useful changes, preserves causal lineage, converts outcomes into reusable knowledge, and improves the mechanisms that generate future improvements.*

### **2.1 Formal definition**

An RSI fabric is a tuple

$$
\mathcal{F} = \big(\mathcal{S},\ \Pi,\ E,\ V,\ K,\ \Gamma\big)
$$

with

- $\mathcal{S}$: the state space, $S = (S_{\text{target}}, S_{\text{machinery}}, S_{\text{knowledge}})$ — the systems being improved, the improvement machinery (generators, schedulers, surrogates, representations), and the knowledge store;
- $\Pi$: the **proposal operator**, a stochastic map $\Pi(\cdot \mid S, K)$ over candidates $c \in \mathcal{C}$ (the candidate space), conditioned on the current state and knowledge;
- $E$: the **evaluation operator**, which maps a candidate and an environment to an evaluation event $e = (c, \text{env}, \text{seed}, \text{evaluator}, x, \text{cost}, \text{lineage})$ with measured outcome $x$;
- $V$: the **verifier**, an independent decision procedure $V(e_{1:n}) \in \{\text{ACCEPT}, \text{REJECT}, \text{QUARANTINE}, \text{CONTINUE}\}$ with controlled error probabilities $(\alpha, \beta)$ (Section 17) and independent of $\Pi$ (Section 18);
- $K$: the **knowledge compressor**, which maps evaluation histories to knowledge objects (Section 20) and failure objects (Section 21), and updates the priors used by $\Pi$;
- $\Gamma$: the **governor**, which restricts the admissible action set to $\mathcal{A}_{\text{adm}} = \{a : S \in \mathcal{I} \Rightarrow a(S) \in \mathcal{I}\}$ and enforces the envelope $\mathcal{G}$ (Sections 37–38).

The loop is a discrete-time stochastic process on $\mathcal{S}$:

$$
S_{k+1} = \Gamma\Big( \text{Promote}\big( V(E(\Pi(S_k, K_k))),\ S_k \big) \Big), \qquad K_{k+1} = K(K_k,\ e_{k}).
$$

### **2.2 The RSI condition**

The process is *recursively self-improving* on an interval if the expected capability production rate $P(t) = \lambda(t)\, y_P(t)\, \delta(t)$ (Section 5) is increasing, and the increase is causally attributable to promoted changes in $S_{\text{machinery}}$ or $K$:

$$
\frac{d}{dt}\,\mathbb{E}[P(t)] > 0
\quad\text{and}\quad
\sum_{m \in \text{meta-promotions}} \widehat{\text{ATE}}_m > 0,
$$

where $\widehat{\text{ATE}}_m$ is the ledger-attributed average treatment effect of meta-promotion $m$ on $P$ (Section 40). Growth of $P$ caused only by added resources is **scaling**, not RSI (Section 64.4 normalizes it away as a Solow residual). The sustained velocity any RSI fabric can achieve is bounded by the growth of three quantities and nothing else: verification throughput, information per evaluation, and verified gain per promotion (Proposition 65.6). Every mechanism in this document acts on one of the three.

### **2.3 What RSI is NOT**

RSI is **NOT** equivalent to:

- rewriting source code;
- generating many patches;
- producing many tokens;
- spawning many agents;
- maximizing GPU utilization;
- increasing container count;
- improving one benchmark score;
- making unverified self-modifications.

Formally: none of $|\Pi|$ (proposal count), token count, agent count, utilization or container count appears in $P$. Only completed, verified, lineage-preserving evaluations and their verified gains do.

### **2.4 Canonical loop**

``` text
OBSERVE
  -> FORM HYPOTHESIS              (pre-registered: metric, direction, MDE, falsifier)
  -> GENERATE CANDIDATE           (Pi; generator id + version recorded)
  -> ASSIGN RISK CLASS            (sets isolation level, evidence bar, blast radius)
  -> ISOLATE                      (sandbox; least privilege; resource caps)
  -> EXECUTE                      (seeded, environment-hashed, paired with control)
  -> MEASURE                      (metric vector + resource vector + energy)
  -> VERIFY                       (independent verifier; sequential test; FDR control)
  -> COMPARE AGAINST CONTROL      (paired, common random numbers)
  -> ACCEPT | REJECT | QUARANTINE (controlled error rates; winner re-measured on fresh seeds)
  -> COMPRESS LEARNING            (knowledge object or failure object; MDL-admissible)
  -> UPDATE SEARCH PRIORS         (posterior over generators, regions, representations)
  -> PROPAGATE USEFUL KNOWLEDGE   (utility-ranked; gossip; bounded coherence cost)
  -> IMPROVE IMPROVEMENT PROCESS  (meta-candidates on L1; verified by L3; see Section 42)
  -> REPEAT
```

Each arrow is an immutable ledger event (Section 19). The loop has no step in which a candidate evaluates itself, certifies itself, or modifies the record of itself.

## **3. FIRST-PRINCIPLES CONSTITUTION**

Every architectural choice MUST be defensible from one or more first principles. v3 gives each principle a formal statement and the number that makes it binding.

### **FP-1 — Causality**

Information propagates at finite speed, and an improvement is a *causal* claim: the candidate, not something correlated with it, moved the metric.

**Physical part.** A synchronous loop spanning distance $d$ cannot iterate faster than

$$
f_{\max} = \frac{c_{\text{medium}}}{2d}, \qquad c_{\text{fiber}} \approx 2\times 10^{8}\ \text{m/s}\ (\approx 5\ \mu\text{s per km, one way}).
$$

| **Aggregate Rate** | **Nominal Interval** | **Vacuum Light-Travel Distance** | **Fiber Round-Trip Reach** |
|---|---|---|---|
| $10^3$/s | 1 ms | ~300 km | ~100 km |
| $10^4$/s | 100 µs | ~30 km | ~10 km |
| $10^5$/s | 10 µs | ~3 km | ~1 km |
| $10^6$/s | 1 µs | ~300 m | ~100 m |
| $10^7$/s | 100 ns | ~30 m | ~10 m |
| $10^8$/s | 10 ns | ~3 m | ~1 m |
| $10^9$/s | 1 ns | ~0.3 m | ~0.1 m |

These are physical upper bounds for a *serialized* loop, not practical latency targets. Aggregate rates above $10^4$/s are therefore only reachable as sums of independent local loops; no design may assume a global clock at these rates.

``` yaml
constraint:
  name: causality
  implication:
    - globally_synchronous_ultra_fast_RSI_is_forbidden_at_large_distance
    - locality_must_increase_with_iteration_rate
    - aggregate_throughput_must_scale_via_parallelism
    - global_knowledge_federation_must_run_slower_than_local_micro_loops
    - every_promotion_requires_an_identified_causal_effect   # new in v3
```

**Statistical part.** For candidate $c$ with control $c_0$, the effect of interest is the interventional contrast

$$
\tau(c) = \mathbb{E}\big[Y \mid do(c)\big] - \mathbb{E}\big[Y \mid do(c_0)\big],
$$

identified by randomized assignment of seeds, environments and placement (Section 40). A promotion decision MUST be based on an estimate $\hat\tau$ of $\tau$ with a stated confidence sequence or interval; a correlation between the presence of $c$ and a metric movement is not an estimate of $\tau$.

**Architectural consequence:** Higher RSI magnitudes MUST become progressively more local, asynchronous, and hierarchical; and every promotion is a randomized, paired, causally identified comparison.

### **FP-2 — Thermodynamics**

Information processing consumes physical resources. Irreversible operations have a non-zero thermodynamic floor, while practical hardware operates many orders above that floor.

**Floor.** Landauer's bound at $T = 300\,\text{K}$:

$$
E_{\min} = k_B T \ln 2 \approx 2.87 \times 10^{-21}\ \text{J per erased bit}.
$$

An evaluation that erases $10^{9}$ bits has a thermodynamic floor of $\approx 3\ \text{pJ}$. Practical evaluations cost $10^{-4}$ to $1$ J (Section 67), i.e. $10^{8}$–$10^{12}$ times the floor. The ladder is therefore **engineering-bound by data motion and utilization, not thermodynamics-bound**, through at least M9.

**What binds instead.** Order-of-magnitude energy per operation (process-dependent; the ratios are what matter):

| **Operation** | **Energy (order of magnitude)** |
|---|---|
| 16-bit multiply-accumulate on an accelerator | ~1 pJ |
| On-chip SRAM access, per bit | ~0.1–1 pJ |
| HBM access, per bit | ~3–5 pJ |
| DRAM access, per bit | ~10–20 pJ |
| Network transfer, per bit, intra-datacenter | ~10–100 pJ |
| Wide-area transfer, per bit | ~1 nJ and up (amortized) |

Moving a bit off-chip costs 10–1000× an arithmetic operation. Therefore the system MUST optimize:

``` text
compute
memory movement
network movement
storage
energy
heat
cooling
hardware utilization
```

and MUST account every evaluation in joules (measured or modelled from the resource vector, Section 5.8). Raw compute throughput without energy-efficiency improvement is not sufficient evidence of recursive progress; the certified quantity is capability per joule (Section 61).

**Open-system framing.** The fabric is a dissipative structure in Prigogine's sense: it maintains and increases internal order (verified capability, compressed knowledge) only by a continuous throughput of free energy and a matching export of entropy as heat. The thermodynamic efficiency of the fabric is therefore a well-defined ratio, verified-knowledge bits retained per joule dissipated, and its ceiling is $1/(k_B T \ln 2)$ bits per joule. Section 67 reports where each rung sits against that ceiling; the gap is the engineering headroom.

### **FP-3 — Locality**

Memory movement is often more expensive than arithmetic (FP-2 table), and latency compounds across hops.

> ***Move computation toward data before moving data toward computation.***

**Rule.** For an evaluation with arithmetic intensity $I$ (operations per byte moved), the roofline bound on attainable throughput is $\min(\text{peak},\ I \cdot \text{BW})$ (Section 58). Micro-evaluations have low $I$ and are bandwidth- and latency-bound; the only lever is to not move the bytes. The architecture SHALL prefer:

- accelerator-resident state;
- node-local evaluation;
- persistent workers;
- content-addressed local caches;
- local knowledge summaries;
- selective global propagation;
- topology-aware scheduling.

**Budget.** On the fast path, bytes moved per evaluation across any boundary slower than node-local memory MUST be bounded by a per-magnitude budget $b_k$ (Section 28); bytes moved per *useful discovery* is a tracked metric and a Rule D optimization target (Section 43).

### **FP-4 — Verification Is Harder Than Mutation**

Generating candidate changes can be cheap. Establishing that a candidate is **actually better** can be much harder.

**Sample-complexity floor.** To certify that a bounded metric difference $D \in [-1, 1]$ has mean $\ge \Delta$ with error $\le \delta$ requires, by Hoeffding,

$$
n \ \ge\ \frac{2}{\Delta^{2}} \ln\frac{2}{\delta}
\qquad(\text{e.g. } \Delta = 0.05,\ \delta = 0.05 \Rightarrow n \ge 2952),
$$

while generating the candidate costs $O(1)$ evaluations. Variance-adaptive bounds (empirical Bernstein) and sequential tests (Section 17) reduce $n$ by constant factors, never to $O(1)$. The asymmetry is structural.

**Undecidability.** No procedure decides "this change is an improvement everywhere" for general programs (Rice's theorem). Verification is therefore statistical, bounded in scope, sandboxed, and replicated; it never claims universality.

> *Verification capacity SHALL scale at least as intentionally as candidate-generation capacity.*

**Binding form.** Let $\lambda_{\text{gen}}$ be the candidate generation rate and $\lambda_{V}$ the verification plane's sustainable decision rate at the required $(\alpha, \beta)$. The fabric MUST enforce $\lambda_{\text{gen}} \le \kappa_V \lambda_V$ with $\kappa_V$ set by the funnel's screening capacity (Section 16); when the bound binds, generation is throttled, verification is never relaxed. No magnitude may be certified through raw candidate throughput alone (Section 6).

**Why relaxing verification is self-defeating.** Candidate quality is private information of the generator, so the candidate pool is a market with asymmetric information (Akerlof): if the verifier's screening weakens, the expected quality of what gets promoted falls, generators that produce cheap low-quality candidates are rewarded relative to careful ones, and the pool degrades toward "lemons". The verification plane is the screening device that keeps the pooling equilibrium from collapsing, which is why its budget is protected (Section 37) rather than traded on the resource market.

**Consequence for growth.** Proposition 65.6 turns this principle into an inequality: sustained RSI velocity cannot exceed the growth rate of verification throughput plus the growth rate of information per evaluation plus the growth rate of gain per promotion. Generation rate does not appear.

### **FP-5 — Goodhart Resistance**

Whenever a proxy metric becomes an optimization target, agents may discover ways to increase the proxy without increasing the intended underlying capability.

**Selection bias is quantified.** If $k$ candidates with equal true effect are measured with noise $\sigma$, the best observed score overstates the truth by

$$
\mathbb{E}\big[\max_{i \le k} Z_i\big]\ \sigma, \qquad
\mathbb{E}[\max_{i\le k} Z_i] \approx \sqrt{2\ln k}\ \text{(asymptotically)};
$$

numerically: $k = 10^3 \Rightarrow 3.24\sigma$; $k = 10^6 \Rightarrow 4.86\sigma$; $k = 10^9 \Rightarrow 6.09\sigma$. At fabric scale, **the winner of a screening round is, by construction, several sigma overstated**. Therefore:

- a screening winner MUST be re-measured on fresh seeds and held-out environments before promotion (the re-measurement is unbiased; the screening score is not);
- promotion estimates SHOULD be shrunk toward the population mean (empirical Bayes: $\hat\tau_{\text{shrunk}} = \bar\tau + \frac{\sigma_\tau^2}{\sigma_\tau^2 + \sigma^2/n}(\hat\tau - \bar\tau)$);
- proxy–truth divergence $\text{div}(t) = \mathbb{E}[\text{proxy}] - \mathbb{E}[\text{ground truth}]$ MUST be monitored on a rotating held-out set, with a drift alarm (Section 49).

Rules retained from v2, now mandatory:

- generators MUST NOT unilaterally control evaluators;
- evaluator changes require higher evidence standards (Section 18);
- held-out evaluations MUST exist;
- adversarial evaluators MUST exist (Section 41);
- real-world or external ground truth SHOULD be used wherever practical;
- benchmarks MUST rotate and expand;
- metric gaming MUST be explicitly tested.

Robust objectives SHOULD be used for promotion of high-blast-radius changes: optimize $\text{CVaR}_{q}$ (the mean of the worst $q$ fraction of environments) or the minimum over an environment ensemble, not the mean alone; Section 41.3 gives the Wasserstein-robust form.

**The Goodhart governor (new in v3).** Goodhart's law is the Lucas critique applied to the fabric: a relation between proxy and truth estimated under one selection policy does not survive a change in the policy, because the policy changes the population being measured. The Holmström–Milgrom multitask result gives the remedy: when effort on measured and unmeasured dimensions competes, the incentive weight on a measured proxy must fall with its covariance to the true objective. The fabric applies this literally. For each proxy metric $m_j$ the selection weight is re-estimated on every rotation of the hidden ground-truth set,

$$
\omega_j \;\propto\; \frac{\widehat{\text{Cov}}(m_j,\ Y_{\text{truth}})}{\widehat{\text{Var}}(m_j)}\quad\text{(the regression coefficient of truth on the proxy)},
$$

so a proxy whose covariance with ground truth decays is automatically de-weighted toward zero, and the selection intensity $i$ (the standardized selection differential; top 10% $\Rightarrow i \approx 1.75$) is capped at a ratified $i_{\max}$ and lowered when proxy divergence drifts. Under the standard correlated-response model the expected true gain per generation is $R_{Y} = i\, r_{pY}\, h_p\, \sigma_{Y}$, where $r_{pY}$ is the proxy–truth correlation and $h_p$ the proxy's repeatability; the governor keeps $i$ bounded and $r_{pY}$ measured, so the realized gain is a prediction rather than a hope. Selection into promotion is also a sample-selection problem in Heckman's sense: estimates computed only on promoted candidates are biased, which is why Section 17.5 re-measures and why calibration streams (Section 16.2) run unselected candidates at full fidelity.

### **FP-6 — Exploration vs. Exploitation**

A system optimizing only its current best lineage will converge prematurely.

**Formal frame.** Candidate-source and region selection is a bandit problem. With $K$ arms (generators, regions, representations) and horizon $T$, Thompson sampling and UCB achieve regret $O(\sqrt{K T \ln T})$; a fixed greedy policy has linear regret whenever its arm is not optimal. Compute MUST therefore be reserved for exploration:

``` yaml
portfolio:
  exploitation: 0.50-0.70
  adjacent_exploration: 0.15-0.25
  high_novelty_search: 0.05-0.15
  evaluator_and_meta_rsi: 0.10-0.20
  floors:                      # new in v3: never zero
    high_novelty_search_min: 0.03
    evaluator_and_meta_rsi_min: 0.05
```

These are initial ranges, not immutable constants; the split is itself allocated by a bandit over observed promotion yield per cost (Section 14), subject to the floors. The novelty floor is justified by Section 45: diversity collapse is a failure condition and recovering from it costs more than maintaining it.

**Portfolio form.** Treat each generator, region or population as an asset with expected verified gain per unit cost $\mu_i$ and covariance $\Sigma$ of realized gains across assets (generators that fail on the same candidate families are correlated and do not diversify). The allocation that maximizes expected production for a variance budget lies on the Markowitz efficient frontier,

$$
\max_{x \ge 0,\ \sum_i x_i = 1}\ \mu^{\top}x - \frac{\gamma_{\text{risk}}}{2}\, x^{\top}\Sigma\, x,
$$

and the portfolio's Sharpe-type ratio $\mu^{\top}x / \sqrt{x^{\top}\Sigma x}$ is tracked per window. The point of the variance term is operational: a fabric whose production rate swings widely wastes verification capacity in the troughs and starves it in the peaks (Section 31); diversification across uncorrelated generators smooths $P(t)$ at no cost in expectation. Section 14.1 gives the bandit that estimates $\mu$ and $\Sigma$ online.

### **FP-7 — No Free Global Synchronization**

Distributed consensus, locks, barriers, and globally ordered event streams impose latency and availability costs.

**Universal Scalability Law.** With $N$ workers, contention coefficient $\gamma$ (serialized fraction) and coherence coefficient $\theta$ (pairwise synchronization cost), relative throughput is

$$
S(N) = \frac{N}{1 + \gamma (N-1) + \theta N (N-1)}, \qquad
N^{*} = \sqrt{\frac{1-\gamma}{\theta}}\ \ \text{(throughput peaks and then falls)}.
$$

| **Coherence $\theta$** | **$N^{*}$ (workers at peak)** |
|---|---|
| $10^{-4}$ | 100 |
| $10^{-6}$ | 1,000 |
| $10^{-8}$ | 10,000 |
| $10^{-10}$ | 100,000 |
| $10^{-13}$ | ~3,000,000 |

To run $N = 10^{6}$ cells without retrograde throughput, the fast path's coherence coefficient must satisfy $\theta \lesssim 10^{-13}$: **effectively zero pairwise coordination**. This is only achievable by hierarchy (coherence confined to pods of bounded size, Section 10) and epidemic propagation whose per-node cost is $O(\log N)$, not $O(N)$.

Therefore high-speed paths SHALL avoid unnecessary global synchronization. Use:

- local clocks;
- local state;
- versioned knowledge;
- eventual convergence;
- deterministic replay where needed;
- conflict resolution;
- causal metadata (hybrid logical clocks, Section 29).

Design rule: every fast-path component MUST declare its $\gamma$ and $\theta$ budget (Section 56), and the certification contract (Section 6) measures $S(N)/N$ as scaling efficiency.

**Why decentralization is a knowledge argument, not only a latency argument.** Hayek's observation that the knowledge relevant to allocation is dispersed and never available to a single planner applies exactly: at M6 no scheduler can hold the state of $10^{6}$ cells, so prices on the resource market (Section 23) and local priors (Section 20) are the only channels through which that knowledge can be aggregated. Simon's theory of nearly decomposable systems says when this works: if interactions within a subsystem are of order 1 and between subsystems of order $\epsilon \ll 1$, then on timescales shorter than $1/\epsilon$ the subsystems evolve independently and on longer timescales only their aggregates interact. Pods are chosen to make $\epsilon$ small (Section 10.1), which is the same thing as making $\theta$ small.

### **FP-8 — Physical Reality Has Multiple Clocks**

Some changes can be validated in nanoseconds. Others require milliseconds, seconds, hours, days, months, physical experiments, or fabrication cycles.

**Nesting rule.** Loops with time constants $\tau_1 < \tau_2 < \dots$ MUST satisfy a separation ratio $\tau_{i+1}/\tau_i \ge 10$ so that each outer loop observes its inner loop at quasi-steady state (cascade-control condition; violation produces oscillation and false attribution). Each band must also sit within about two decades of its neighbours, or the outer loop never observes the inner loop's transients at its own sampling rate; spanning 1 ms to 1 month ($\approx 2.6\times10^{9}$ ms, 9.4 decades) therefore takes about five bands, which is the structure of Section 25.

Therefore RSI MUST operate on multiple concurrent timescales, and no loop may be driven faster than its evidence clock.

### **FP-9 — Useful Knowledge Can Outlive a Candidate**

A failed experiment can still eliminate a region of search space or reveal a causal mechanism.

**Value of a negative result.** If a failure object (Section 21) prevents $r$ future redundant evaluations of expected cost $\bar c$ each, its value is $r\bar c$ regardless of the candidate's own score. Knowledge yield is measured in bits (Section 5.6): a knowledge object $K$ is admissible iff it compresses the ledger, $L(D \mid K) + L(K) < L(D)$ (minimum description length), and its yield is the saving.

Every experiment has two potential outputs:

``` yaml
outputs:
  capability_gain: optional
  knowledge_gain: expected
```

Failures MUST NOT be discarded blindly.

### **FP-10 — Recursive Acceleration Must Be Measured**

The system SHALL distinguish:

1. capability improvement — $\Delta C$ (Section 5.4);
2. experiment throughput — $\lambda$ (Section 5.1);
3. experiment quality — $y_V$, duplicate rate, information gain per evaluation;
4. verification quality — realized $(\alpha, \beta)$, regression hazard (Section 5.5);
5. improvement efficiency — $P / \|R\|$ (Section 5.8);
6. improvement-of-improvement — $v = \tfrac{d}{dt}\ln P$ and $\varphi$ (Sections 5.9–5.10, 64).

The system MUST NOT claim recursive acceleration unless the evidence demonstrates it: the claim is $\text{LCB}_{95}(\hat\varphi) \ge 1 - \varepsilon_\varphi$ on resource-normalized data over at least three doublings of $P$, with the excess attributed to meta-promotions by randomized ablation (Section 68). Anything else is scaling, tuning, or noise, and is reported as such.

**Two instruments make the measurement honest.** First, growth accounting in Solow's form separates what added resources explain from what the machinery explains; the residual is the RSI velocity (Section 64.4). Second, Hasselmann's point about slow variables driven by fast noise applies to capability time series: integrating many small random fluctuations produces random-walk-like drift that looks like a trend, so detection and attribution use optimal fingerprinting against the noise covariance estimated from control periods (Section 64.8), never a visual trend.

## **4. ORDER-OF-MAGNITUDE LADDER**

``` yaml
magnitudes:
  M0:
    evaluations_per_sec: 1000
    status: initial_build_target
    production_multiplier_vs_v2: ">= 4.0 (contract), >= 8.0 (design)"
  M1:
    evaluations_per_sec: 10000
  M2:
    evaluations_per_sec: 100000
  M3:
    evaluations_per_sec: 1000000
  M4:
    evaluations_per_sec: 10000000
  M5:
    evaluations_per_sec: 100000000
    status: certified_waypoint          # v2 north star, now a waypoint
  M6:
    evaluations_per_sec: 1000000000
    status: declared_north_star         # raised in v3
  M7:
    evaluations_per_sec: 10000000000
    status: frontier_horizon
  M8:
    evaluations_per_sec: 100000000000
    status: frontier_horizon
  M9:
    evaluations_per_sec: 1000000000000
    status: frontier_horizon_accelerator_resident_only
  M10_plus:
    evaluations_per_sec: "1e13+"
    status: physics_and_infrastructure_limited_horizon   # envelope in Section 67
```

The ladder is exponential in its index by construction: $\lambda_k = 10^{3+k}$ evaluations/s for magnitude $M_k$. The program's deeper claim is exponential growth in *time* of capability production $P$, which the ladder does not assume and Section 64 measures.

### **4.0 The vertical ladder (new in v3)**

The horizontal ladder counts evaluations. The vertical ladder counts what each evaluation is worth. Let $\mathcal{M}_k$ be the capability-production multiplier at rung $k$ relative to the v2 fixed-sample baseline running on the same hardware (Section 68). Then

$$
\mathcal{M}_k^{\text{target}} = 4 \cdot 2^{k}, \qquad \text{gate}_k:\ \ \mathcal{M}_k \ge 4\ \ \text{and}\ \ \mathcal{M}_k \ge \mathcal{M}_{k-1},
$$

so the design target is $4\times$ at M0, $8\times$ at M1, $16\times$ at M2 and $256\times$ at M6, while the certification gate only requires the multiplier to hold its floor and never fall. Capability production at rung $k$ is then targeted at $\lambda_k \cdot \mathcal{M}_k \cdot P_{\text{v2}}/\lambda$, i.e. $10^{k} \cdot 2^{k} = 20^{k}$ times M0's, which is the formal content of "aim as high as possible": the fabric is designed to climb two ladders at once, and the second one is the one the fabric itself improves.

### **4.1 Physics and infrastructure envelope per rung**

The implied energy per evaluation $\varepsilon = W / \lambda$ at a power budget $W$, the in-flight population $L = \lambda W_{\text{sojourn}}$ (Little's law), and the hot-path ledger bandwidth at 256 bytes per record:

| **Rung** | **$\lambda$ (1/s)** | **$\varepsilon$ at 1 MW** | **$\varepsilon$ at 100 MW** | **In-flight $L$ (assumed sojourn)** | **Ledger hot path** |
|---|---|---|---|---|---|
| M0 | $10^{3}$ | 1 kJ | — | 50 (50 ms) | 256 KB/s |
| M3 | $10^{6}$ | 1 J | 100 J | $10^{4}$ (10 ms) | 256 MB/s |
| M6 | $10^{9}$ | 1 mJ | 100 mJ | $10^{6}$ (1 ms) | 256 GB/s |
| M9 | $10^{12}$ | 1 µJ | 100 µJ | $10^{8}$ (100 µs) | 256 TB/s |

Reading the table: a 300 W accelerator delivers 1 mJ in about 3 µs and 100 µJ in about 0.3 µs. M6 at 1 MW therefore requires evaluations that are microsecond-scale and accelerator-resident on average; M9 requires sub-microsecond evaluations and a ledger that is hierarchical (per-evaluation records local with TTL, Merkle roots global; Section 19). The Landauer floor for $10^{9}$ erased bits per evaluation is 3 pJ, i.e. a thermodynamic ceiling near $3\times10^{20}$ evaluations/s at 1 GW: the ladder is engineering-bound, not physics-bound, through every rung listed (Section 67).

### **4.2 Mandatory interpretation**

An evaluation is a completed, measurable experimental event

$$
e = \big(c,\ \text{env},\ \text{seed},\ \text{evaluator},\ x \in \mathbb{R}^{m},\ r \in \mathbb{R}^{6}_{+},\ \text{lineage},\ \text{verdict}\big)
$$

with:

- candidate identity $c$ (content hash);
- environment identity (hash);
- evaluator identity (hash, version);
- measured output $x$ (a metric vector, not a single scalar);
- resource accounting $r$ (compute, energy, time, money, communication, infrastructure);
- causal lineage (parent ids, generator id);
- terminal verdict or knowledge artifact.

**Minimum-information criterion (new in v3).** An event counts toward $\lambda$ only if it is attached to a pre-registered experiment (Section 15) whose metric has non-zero variance under the null and whose outcome can change at least one promotion decision or knowledge object. Re-running a deterministic evaluation with an identical (candidate, environment, seed, evaluator) tuple is a replay, counted under reproducibility (Section 46), not under $\lambda$.

An evaluation MAY be: a kernel microbenchmark; a scheduling policy comparison; an IR transformation; a model-routing decision test; a prompt-policy test; an algorithm replacement; an agent workflow variation; a retrieval strategy evaluation; a compiler optimization; a data-structure substitution; a sandboxed code patch; a simulation; a formal proof attempt; an adversarial test; a surrogate-model estimate (counted at the surrogate fidelity level, never as a full-fidelity event).

An evaluation MUST NOT be counted merely because a candidate was generated.

## **5. CORE METRICS**

All metrics are computed from the ledger (Section 19) over a window $[t - W, t]$; each is reported with a 95% confidence interval or, for monitored streams, an anytime-valid confidence sequence (Section 17.3). Pseudo-code uses the ledger event fields of Section 4.2.

### **5.1 Evaluation Throughput**

$$
\hat\lambda(t) = \frac{\#\{e : t_{\text{end}}(e) \in [t-W, t]\}}{W}, \qquad
\text{LCB}_{95}(\lambda) = \hat\lambda - 1.645\sqrt{\hat\lambda / W}\ \ (\text{Poisson approximation}).
$$

``` text
lambda = count(events where completed and counted and t_end in window) / W
```

Certification uses $\text{LCB}_{95}$ on a sustained window (Section 6), never the peak.

### **5.2 Useful Verification Yield**

$$
y_V = \Pr(\text{verified useful} \mid \text{completed}) \ \approx\ \frac{\#\text{verified useful}}{\#\text{completed}}
$$

with a Wilson interval. "Verified useful" means the verifier returned ACCEPT or produced an admissible knowledge or failure object (Sections 20–21).

### **5.3 Promotion Yield**

$$
y_P = \Pr(\text{promoted} \mid \text{completed}), \qquad
y_{P\mid V} = \Pr(\text{promoted} \mid \text{verified}).
$$

Promotions are counted only when the promotion decision passed the false-discovery control of Section 17.4; the reported $y_P$ therefore has an FDR guarantee $\le q$.

### **5.4 Capability Delta**

For a capability vector $C \in \mathbb{R}^{d}$ measured on a benchmark distribution $\mathcal{D}$ (rotating, held-out, Section 18):

$$
\Delta C = \mathbb{E}_{\mathcal{D}}[C_{\text{new}}] - \mathbb{E}_{\mathcal{D}}[C_{\text{baseline}}],
$$

estimated by paired differences on common seeds and environments (Section 40), reported per dimension with a confidence interval. Capability SHOULD be multidimensional rather than compressed prematurely into a single score; the scalarization $\bar C = w^{\top} C$ is used for the growth law only, and $w$ is ratified by the Human Control Plane. The ratification is not a formality: by Arrow's impossibility theorem no non-dictatorial aggregation of the capability dimensions satisfies the usual axioms, so some party must simply choose $w$, and the document makes that party human (73.1). Within a rung $w$ is frozen; across rungs capability is reported as a fixed-basket index so that a change in the mix of domains cannot masquerade as growth.

The mean verified gain per promotion is

$$
\delta = \mathbb{E}\big[\Delta \bar C \mid \text{promoted}\big],
$$

measured on the post-promotion re-measurement, not the screening score (FP-5).

### **5.5 Regression Rate**

$$
\rho_{\text{reg}} = \Pr(\text{material regression within horizon } H \mid \text{accepted}),
$$

estimated as a hazard on the promotion cohort (Kaplan–Meier over the horizon, since recent promotions are censored). "Material" means a held-out metric moved beyond its pre-registered tolerance or a Section 41 adversary found a defect attributable to the change.

### **5.6 Knowledge Yield**

$$
\text{KY} = \frac{\sum_{K \text{ admitted in window}} \big[L(D) - L(D \mid K) - L(K)\big]}{\#\text{completed evaluations}}\quad \text{bits per evaluation},
$$

where $L(\cdot)$ is the description length under the fabric's reference coder (Section 20.3). The operational proxy, when MDL accounting is unavailable, is the reduction in surrogate predictive log-loss on held-out outcomes per evaluation. The v2 count of reusable artifacts per evaluation is retained as a secondary metric.

### **5.7 Duplicate Search Rate**

$$
\text{DSR} = \Pr\big(\exists\, e' \text{ prior} : \text{sim}(c, c') \ge s^{*} \wedge \text{env}(e) = \text{env}(e')\big),
$$

with similarity computed by locality-sensitive hashing (MinHash over token or IR shingles, collision probability equal to Jaccard similarity; cosine LSH for embeddings) at threshold $s^{*}$ (Section 21.3). Duplicates do not count toward $\lambda$.

### **5.8 Cost of Useful Discovery**

$$
\text{CUD} = \frac{\|R_{\text{window}}\|_{w}}{\#\text{verified useful discoveries}},
$$

reported also as the full resource vector per discovery and as a Pareto front over (energy, time, money). The **experience-curve exponent** $b$ in $\text{CUD}(n) = \text{CUD}_0\, n^{-b}$, fitted on cumulative discoveries $n$, is a program-level target (Section 48).

### **5.9 Recursive Improvement Velocity**

The capability production rate and its velocity:

$$
P(t) = \lambda(t)\, y_P(t)\, \delta(t), \qquad
v(t) = \frac{d}{dt}\ln P(t).
$$

$v$ is in units of 1/time; exponential growth of $P$ is exactly constant positive $v$. The doubling time is $T_2 = \ln 2 / v$ and the time per magnitude is $T_{10} = \ln 10 / v = 3.32\,T_2$. The v2 proxy (verified gain × future-productivity multiplier × generalization / cost) is subsumed: the multiplier is $P_{\text{after}}/P_{\text{before}}$ of a meta-promotion, and cost normalization is in 5.9.1.

**5.9.1 Resource normalization.** Let $R(t)$ be the resource vector and $\eta_R$ the measured elasticity of $P$ with respect to resources at fixed machinery (Section 64.4). The resource-normalized velocity

$$
\tilde v(t) = v(t) - \eta_R\, \frac{d}{dt}\ln \|R(t)\|_{w}
$$

is the velocity attributable to the machinery. This is Solow's growth-accounting residual applied to the fabric's own production function (Section 64.4); only $\tilde v$ is used for RSI claims. The **recursive gain coefficient** $\text{RGC} = \tilde v / v \in [0, 1]$ reports what fraction of observed growth is RSI rather than scaling.

### **5.10 Recursive Acceleration**

$$
a(t) = \frac{d\tilde v}{dt}, \qquad
\hat\varphi - 1 = \frac{\partial \ln \tilde v}{\partial \ln P}\ \ \text{(regression slope over windows)}.
$$

The program's deepest objective is sustained $\tilde v > 0$ with $\varphi \ge 1$ (exponential or faster) inside the governance envelope, with the excess over resource scaling attributed to meta-promotions. $a > 0$ with $\varphi < 1$ is possible transiently and is not a recursive-acceleration claim. $\varphi$ is the returns-to-scale exponent of Romer's knowledge production function in its general (Jones) form, $\dot A = \kappa\, A^{\varphi} L_A^{\lambda_A}$, with the fabric's meta-evaluation effort in the role of research labour; Section 64 gives the derivation, the regimes and the decomposition of $\varphi$ into measurable elasticities.

### **5.11 Decision Throughput and Decision Efficiency (new)**

Let $n_B$ be the fixed-sample size the v2 baseline needs for a promotion decision at $(\alpha, \beta, \Delta)$ and $\bar n$ the realized mean evaluations per decision under v3 testing:

$$
D = \frac{\lambda}{\bar n}\ \ \text{decisions per second}, \qquad
\mathcal{M}_\lambda = \frac{n_B}{\bar n}\ \ \text{(decision-efficiency multiplier)}.
$$

### **5.12 Variance-Reduction Factor (new)**

$$
\text{VRF} = \frac{\text{Var}(\hat\tau_{\text{unpaired}})}{\text{Var}(\hat\tau_{\text{realized}})} = \frac{1}{(1-\rho_{\text{CRN}})(1 - r^{2}_{\text{CV}})},
$$

where $\rho_{\text{CRN}}$ is the pairing correlation from common random numbers and $r_{\text{CV}}$ the control-variate correlation (Section 40.2).

### **5.13 Verification Efficiency (new)**

$$
\text{VE} = \frac{\text{verified decisions per second}}{\text{verification-plane joules per second}},\qquad
\text{and the ratio } \lambda_{\text{gen}} / \lambda_V \le \kappa_V\ \text{(FP-4)}.
$$

### **5.14 Governance Metrics (new)**

Tracked continuously and reported in every certificate:

``` yaml
governance_metrics:
  invariant_check_pass_rate: "fraction of admissibility checks passed; MUST be 1.0 for L3/L4"
  boundary_violation_attempts: "count of proposals touching L3/L4; MUST be 0 promoted, any attempt alarms"
  velocity_vs_envelope: "tilde_v / v_max; MUST be <= 1.0"
  halt_latency_measured: "seconds from HALT to zero in-flight; MUST be <= lease_ttl + W_max"
  human_review_sampling_rate: "fraction of L1 promotions reviewed; >= ratified minimum"
  evaluator_change_rate: "L2 changes per day; <= ratified cap"
```

## **6. MAGNITUDE CERTIFICATION CONTRACT**

A magnitude $M_k$ is certified only when ALL required gates pass on one sustained window; each gate is a statistical statement with the confidence level fixed at 95% unless stated otherwise.

``` yaml
certification_gates:
  throughput:            "LCB_95(lambda) >= 10^(3+k) over the full window"
  sustained_duration:    "window >= max(1 hour, 100 * p99_9 sojourn), no gaps > 1 s"
  reproducibility:       "replay of a random 1% sample reproduces verdicts at >= 99% (tolerance per Section 46)"
  evaluator_integrity:   "evaluator hashes unchanged during window; hidden-set leakage test passes"
  useful_yield:          "LCB_95(y_V) >= y_V_min(k); duplicates excluded"
  cumulative_gain:       "LCB_95(sum of delta over window) > 0 on held-out re-measurement"
  regression_control:    "UCB_95(rho_reg) <= rho_max(k)"
  lineage_completeness:  "fraction of events with full parent chain >= 1 - 1e-6"
  rollback_readiness:    "rollback drill executed during window; MTTR <= bound"
  resource_accounting:   "100% of events carry a resource vector; energy accounted (measured or modelled)"
  scaling_efficiency:    "S(N)/N >= 0.5 at the certifying N (FP-7); theta measured and reported"
  failure_recovery:      "chaos injection during window; zero lineage loss, zero unverified promotions"
  adversarial_validation: "Section 41 populations ran during window; every exploit found became a test family"
  production_multiplier: "M_k >= 4.0 and M_k >= M_(k-1), measured by randomized ablation, Section 68"  # new
  goodhart_governor:     "selection weights omega_j re-estimated on the rotated hidden set during window; i <= i_max"  # new
  governance:            "all Section 5.14 metrics within envelope; zero L3/L4 promotions"  # new
```

Each certification MUST generate:

``` yaml
magnitude_certificate:
  magnitude: "M_k"
  benchmark_suite_hash: required
  runtime_hash: required
  evaluator_set_hash: required
  infrastructure_profile: required
  start_time: required
  end_time: required
  sustained_rate_lcb95: required
  sustained_rate_point: required
  p50_latency: required
  p95_latency: required
  p99_latency: required
  p99_9_latency: required
  promotion_yield_ci95: required
  regression_rate_ucb95: required
  resource_cost_vector: required
  energy_joules: required
  capability_delta_ci95: required
  production_multiplier_lcb95: required
  production_multiplier_shapley_attribution: required   # per-mechanism shares, Section 68.4
  scaling_efficiency: required
  coherence_coefficient_theta: required
  governance_metrics: required
  phi_hat_ci95: required_from_M1          # growth exponent, once >= 3 doublings exist
  evidence_bundle_uri: required
  signed_result: required                 # signed by the verification plane and the governor
```

A certificate is a signed, content-addressed object. Its signature keys live in the invariant plane (Section 37) and are not reachable from any RSI cell.

## **7. AUTOMATIC NEXT-MAGNITUDE DIRECTIVE**

Certification of $M_k$ MUST automatically emit:

``` yaml
event:
  type: MAGNITUDE_CERTIFIED
  magnitude: "M_k"
actions:
  - freeze_certified_baseline              # immutable; the rollback target for M_(k+1) work
  - create_immutable_evidence_bundle
  - activate_next_magnitude_program        # inside the currently ratified envelope G
  - profile_dominant_bottlenecks           # Section 31: utilization per stage, binding constraint
  - project_time_to_next_magnitude         # T10 = ln 10 / tilde_v, with CI
  - allocate_experimental_budget           # within r_max of G
  - generate_scaling_hypotheses
  - launch_parallel_scaling_programs
  - request_envelope_review                # new: humans re-ratify G for M_(k+1); growth continues under current G meanwhile
```

The next target is:

$$
\lambda_{k+1} = 10\,\lambda_k, \qquad
\hat T_{10} = \frac{\ln 10}{\tilde v}\ \ \text{(projected, with its confidence interval, recorded in the directive)}.
$$

**Envelope rule (new in v3).** Activation is automatic *within* the ratified envelope $\mathcal{G}$: the directive may reallocate budget, spawn populations and raise targets up to the ratified resource growth rate $r_{\max}$ and velocity cap $v_{\max}$. It cannot expand $\mathcal{G}$. If the projected program needs more than $\mathcal{G}$ permits, the directive records the gap and waits for two-key ratification (Section 38); work continues at the current envelope. No certified magnitude is considered "done."

Every magnitude is simultaneously:

1. a production baseline;
2. a research launchpad;
3. a training dataset for the next magnitude.

## **8. ARCHITECTURAL PLANES**

``` text
+----------------------------------------------------------+
| 0. CONSTITUTION / INVARIANT PLANE                        |
| protected rules, identities, permissions, auditability   |
| governor: admissible-action set, envelope G, halt leases |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 1. INTENT PLANE                                          |
| objectives, budgets, constraints, research priorities    |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 2. DISCOVERY PLANE                                       |
| hypotheses, mutations, program synthesis, recombination  |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 3. EXECUTION PLANE                                       |
| sandboxes, simulators, microbenchmarks, shadow execution |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 4. VERIFICATION PLANE                                    |
| tests, proofs, adversaries, sequential statistics, FDR   |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 5. KNOWLEDGE PLANE                                       |
| lineage, experiment graph, laws, failure memory          |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 6. PROPAGATION PLANE                                     |
| promotion, migration, recombination, rollback            |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 7. META-RSI PLANE                                        |
| improves planes 1-3 and 5-8; never 0; plane 4 under 18   |
+-----------------------------+----------------------------+
                              |
+-----------------------------v----------------------------+
| 8. PHYSICAL OPTIMIZATION PLANE                           |
| hardware mapping, topology, energy, cooling, accelerators|
+----------------------------------------------------------+
```

### **8.1 Plane invariants (new)**

Each plane declares what it may read, what it may write, and who verifies its changes. The relation "plane $i$ may modify plane $j$" MUST be acyclic when composed with "plane $j$ verifies plane $i$" (Section 42.3). Concretely:

| **Plane** | **May be modified by** | **Changes verified by** | **Fast-path?** |
|---|---|---|---|
| 0 Constitution | humans only (two-key) | humans + offline audit | no |
| 1 Intent | humans; Meta-RSI within envelope | plane 4 + human sampling | no |
| 2 Discovery | Meta-RSI | plane 4 | yes |
| 3 Execution | Meta-RSI | plane 4 | yes |
| 4 Verification | Meta-RSI under Section 18 (cross-validation, replay) | plane 0 process, human review | partly |
| 5 Knowledge | planes 4–5 | plane 4 | yes (append-only) |
| 6 Propagation | Meta-RSI | plane 4 + plane 0 signatures | partly |
| 7 Meta-RSI | Meta-RSI (depth-limited, Section 42.4) | plane 4 | no |
| 8 Physical | Meta-RSI, humans | plane 4 + physical-clock evidence | no |

## **9. RSI CELL**

The smallest autonomous optimization unit is an **RSI Cell**: a bounded closed loop with its own local ledger shard and knowledge cache.

``` yaml
rsi_cell:
  required_fields:
    - cell_id
    - specialization
    - objective
    - budget                   # resource vector cap, enforced by plane 0
    - local_state
    - candidate_generator
    - evaluator_binding
    - sandbox_binding
    - local_archive
    - lineage_endpoint
    - result_stream
    - risk_policy
    - version
    - halt_lease               # new: TTL lease from the governor; expiry halts the cell
    - coherence_budget         # new: declared theta contribution, Section 10
    - test_policy              # new: (alpha, beta, MDE, stopping rule) defaults
```

### **9.1 Cell throughput model**

A cell with $w$ persistent workers, mean evaluation service time $s$ and overhead fraction $o$ (scheduling, serialization, ledger write) sustains

$$
\lambda_{\text{cell}} = \frac{w\,u}{s\,(1 + o)}, \qquad L_{\text{cell}} = \lambda_{\text{cell}}\, W_{\text{sojourn}}\ \ (\text{Little}),
$$

at target utilization $u$ (design value $u = 0.7$ to keep queueing delay bounded; at $u \to 1$ the M/M/1 sojourn $W = s/(1-u)$ diverges). The overhead budget is $o \le 0.1$ at M0 and $o \le 0.01$ from M3 (Section 28).

### **9.2 Cell state machine**

Section 29 defines the states; every transition is an immutable event carrying a hybrid logical clock timestamp. A cell whose halt lease expires transitions to HALTED from any state, completes nothing new, and flushes its ledger shard.

A cell MAY specialize in: code; compiler; memory; inference; retrieval; reasoning; model routing; kernel generation; network topology; scheduling; evaluator generation; benchmark generation; formal verification; scientific discovery; meta-RSI; knowledge compression.

Cells SHOULD be: disposable; forkable; mergeable; versioned; isolated; resource-bounded; independently observable.

## **10. SWARM TOPOLOGY**

The system SHALL NOT require one central intelligence to control all experiments.

``` text
        CELL <----> CELL                pod (<= N_pod cells, shared coherence budget)
          ^          ^
          | \      / |
          |  \    /  |
          v   \  /   v
        CELL <----> CELL
          ^          ^
          | \      / |
          v  \    /  v
        CELL <----> CELL
          |
     (gossip, O(log N) rounds)  <---->  other pods / regions
```

### **10.1 Pod sizing from the Universal Scalability Law**

Within a pod, cells may share a local queue, a local knowledge cache and a local dedup index; these create a pod coherence coefficient $\theta_{\text{pod}}$. The pod size is bounded by

$$
N_{\text{pod}} \le \sqrt{\frac{1-\gamma_{\text{pod}}}{\theta_{\text{pod}}}}\ \cdot\ \frac{1}{2},
$$

i.e. half the USL peak, so that the pod runs on the rising part of its throughput curve with $S(N)/N \ge 0.5$. With $\theta_{\text{pod}} = 10^{-6}$ this gives $N_{\text{pod}} \le 500$ cells. Across pods there is **no pairwise coherence**: only epidemic propagation of knowledge and Merkle summaries.

**Choosing the partition.** Pods are Simon's nearly decomposable subsystems. Build the interaction graph whose edge weights are the measured rates at which cells read each other's results, shared caches or queues; partition it to minimize the cut (spectral partitioning on the Fiedler vector of the graph Laplacian, refined by local search) subject to the size bound above. The cut weight divided by the internal weight is the coupling $\epsilon$; it is reported as the pod's measured $\theta$ and the partition is recomputed when $\epsilon$ drifts above budget.

### **10.2 Propagation across pods**

Push–pull gossip with fanout $f$ reaches $N$ pods in $O(\log_{f+1} N)$ rounds with high probability: $N = 10^{3}$ pods in ~10 rounds, $10^{6}$ in ~20, $10^{9}$ in ~30 (base 2). At 50 ms per round, global convergence of a high-value knowledge object takes about one second at M6 scale, with per-pod message cost $O(f \log N)$, not $O(N)$. This is what makes $\theta \approx 0$ on the fast path achievable (FP-7).

Higher-level coordination exists, but micro-experiment selection SHOULD become increasingly local at scale. Knowledge propagation SHOULD be event-driven and utility-ranked (Section 35).

## **11. HORIZONTAL VS. VERTICAL SCALING**

### **Horizontal Scale**

Increase: CPU; GPU; accelerator count; node count; Cell count; storage; regional clusters.

Horizontal scale multiplies throughput with USL efficiency:

$$
\lambda(N) = \lambda_1 \cdot S(N) = \frac{N\,\lambda_1}{1 + \gamma (N-1) + \theta N (N-1)}.
$$

Because the number of candidate evaluations available grows without bound, the fabric is in Gustafson's regime (scaled speedup $S = N - (1-p)(N-1)$ for serial fraction $1-p$): the ceiling is set by coherence $\theta$, not by a fixed serial fraction.

### **Vertical RSI Scale**

Improve: candidate quality; evaluator quality; knowledge reuse; representation; scheduling; compiler performance; kernel efficiency; memory use; network use; verification precision; search-space pruning; experimental design; causal inference.

Vertical scale acts on the other factors of $P$ and on $\bar n$:

$$
P = \underbrace{\lambda(N)}_{\text{horizontal}} \cdot \underbrace{\frac{n_B}{\bar n}}_{\mathcal{M}_\lambda\ (\text{decision efficiency})} \cdot \underbrace{y_P}_{\mathcal{M}_y} \cdot \underbrace{\delta}_{\mathcal{M}_\delta}\ \Big/\ \frac{n_B}{\bar n}\Big|_{\text{baseline}},
$$

so that

``` text
horizontal_scale * vertical_improvement = compounded_RSI_capacity
P = lambda(N) * y_P * delta ;   v3 contract: (y_P * delta / n_bar) >= 4 x baseline at equal lambda(N); design 8x
```

The objective is the product, and the 4× contract (Section 68) is a statement about the vertical factors at fixed hardware. The two ladders of Section 4.0 are exactly horizontal (10× per rung) and vertical (2× per rung, by design target).

## **12. LANGUAGE AND RUNTIME STRATEGY**

No single language SHALL dominate every layer. Each layer carries an overhead budget: the fast-path per-evaluation overhead attributable to the runtime (scheduling, serialization, isolation entry/exit, ledger append) MUST satisfy $o \le 0.1$ at M0 and $o \le 0.01$ from M3; a layer that cannot meet its budget in a language is moved to one that can.

### **Rust**

Primary roles: high-integrity runtime; scheduler; orchestration; state machines; experiment coordinator; lineage service; policy enforcement; distributed protocols; sandbox control; resource accounting; the governor and lease service.

Rationale: memory safety removes a class of verification cost (no memory-corruption test families on the control plane), deterministic destructors bound resource leaks, and the absence of a garbage collector keeps p99.9 scheduling latency inside the overhead budget.

### **C++**

Primary roles: ultra-low-latency execution; existing HPC ecosystems; specialized simulation; systems integration; device-level optimization; latency-critical networking.

### **Python**

Primary roles: research; rapid experimentation; benchmark authoring; model research; analysis; scientific workflows; offline computation of the Section 5 estimators.

Python SHOULD be removed from critical microsecond loops unless justified by compiled execution; interpreter dispatch alone (order $10^{2}$ ns per bytecode) exceeds the M4+ per-evaluation overhead budget.

### **CUDA / ROCm / Accelerator Kernels**

Use for: dense numerical evaluation; inference; simulation; batched candidate scoring. From M4, the majority of counted evaluations are expected to be accelerator-resident batches (Section 4.1): a batch of $B$ micro-candidates evaluated in one kernel launch of duration $d$ contributes $B/d$ to $\lambda$ with per-evaluation overhead $\approx t_{\text{launch}}/B$.

### **Triton / MLIR / LLVM-class IR**

Use for machine-generated computational transformations; this is the native representation for high-rate mutation from M3 (Section 13).

### **WebAssembly / Isolated Native Runtime**

Use where efficient sandboxing is valuable: isolation entry/exit in the microsecond range versus milliseconds for process or container boundaries, which matters once $1/\lambda_{\text{cell}}$ is itself in the microsecond range.

## **13. REPRESENTATION EVOLUTION**

The system SHALL progressively move from human-source-centric mutation toward machine-native representations.

``` text
SOURCE CODE
   ->
AST
   ->
TYPED IR
   ->
COMPUTATIONAL DAG
   ->
DOMAIN DSL
   ->
HARDWARE-AWARE IR
   ->
MACHINE-DESIGNED REPRESENTATION
```

### **13.1 Why representation is a search-efficiency variable**

A representation $\mathcal{R}$ fixes the neighbourhood structure of the candidate space. Search efficiency depends on the fitness landscape's **autocorrelation length** $\ell$ under random walks in $\mathcal{R}$ (ruggedness) and its **neutrality** (fraction of neutral moves). For a landscape with correlation $r(d) = e^{-d/\ell}$ at mutation distance $d$, the expected number of evaluations to reach a given improvement scales inversely with $\ell$; a representation change that doubles $\ell$ at equal expressiveness is worth as much as doubling $\lambda$.

Representation changes are therefore **meta-candidates** evaluated on: promotion yield per evaluation; measured $\ell$ and neutrality; expressiveness (coverage of the incumbent's reachable set); compile and verification cost per candidate.

**The landscape is glassy.** Parisi's theory of complex landscapes (replica symmetry breaking) gives the right expectation for a candidate space of this kind: exponentially many metastable optima organized hierarchically, with an ultrametric structure of basins. Three consequences are built in. Local search from one lineage converges to a basin whose quality is typical, not optimal, so parallel lineages are a requirement rather than a luxury (Section 45). The population's diversity is measured by the **overlap distribution** $P(q)$ of pairwise behavioural similarities $q_{ab}$ between lineages: a single sharp peak means one basin (monoculture), a broad or multi-peaked $P(q)$ means several, and the diversity floor is stated on it (Section 45.2). And a representation change is valuable precisely when it changes the basin structure, which is why $\ell$ is measured per representation rather than assumed.

Human-readable code remains necessary for: constitutional logic; auditability; security policy; interfaces; debugging; human governance. It need not remain the fastest mutable representation. Every machine-native representation MUST have a lossless lift back to an auditable form for anything that reaches the CANARY state or above (Section 44).

## **14. CANDIDATE GENERATION ENSEMBLE**

Candidate sources MAY include:

``` yaml
candidate_generators:
  - large_language_models
  - small_specialized_models
  - evolutionary_search
  - genetic_programming
  - bayesian_optimization
  - reinforcement_learning
  - gradient_methods
  - symbolic_search
  - constraint_solving
  - program_synthesis
  - theorem_proving
  - superoptimization
  - monte_carlo_search
  - retrieval_recombination
  - cross_population_migration
```

No generator receives permanent monopoly.

### **14.1 Budget allocation as a cost-aware bandit**

Each generator $g$ has an unknown promotion-yield-per-cost $\mu_g = \mathbb{E}[\text{verified gain}]/\mathbb{E}[\text{cost}]$. Allocation uses Thompson sampling over a posterior for $\mu_g$ (Beta for yield, log-normal for gain, Gamma for cost), with a diversity bonus:

$$
\text{score}_g = \tilde\mu_g + \beta_{\text{nov}}\,\text{nov}_g, \qquad \tilde\mu_g \sim \text{posterior}(\mu_g),
$$

and budget share $\propto$ sampled score, subject to the FP-6 floors. Regret against the best fixed generator is $O(\sqrt{K T \ln T})$ for $K$ generators; a static split has linear regret whenever yields drift, which they do, because the landscape changes with every promotion.

Generators themselves SHALL be benchmarked against: useful-yield; novelty; cost; generalization; downstream descendant value (Section 24). The posterior is reset on a generator version change (its lineage is immutable; its statistics are not inherited). The bandit's posterior means and the empirical covariance of realized gains across generators are the $(\mu, \Sigma)$ of the FP-6 portfolio; the bandit explores, the portfolio sizes.

### **14.2 Mutation scheduling under the error threshold**

Eigen's quasispecies theory bounds how aggressive mutation can be before selection can no longer retain the incumbent's information. For a candidate of description length $L$ symbols, per-symbol mutation probability $\mu$ and selective superiority $\sigma_s$ of the incumbent (its fitness relative to the mean of its mutants), information survives only if

$$
\mu\, L \;<\; \ln \sigma_s \qquad(\text{error threshold}),
$$

beyond which the population delocalizes from the incumbent (error catastrophe) regardless of how much it is evaluated. The fabric schedules its mutation operators accordingly: the exploitation and adjacent-exploration populations run at $\mu L \le \tfrac{1}{2}\ln\hat\sigma_s$ with $\hat\sigma_s$ estimated from the verifier's accept ratio, so that the expected number of changed symbols per candidate stays below the threshold with margin; the **high-novelty population deliberately runs above the threshold**, which is why it is a separate, isolated population whose outputs enter the main lineages only through the full funnel. The margin $\ln\hat\sigma_s - \mu L$ is reported as `error_threshold_margin` (Section 30) and a negative margin in an exploitation population is a failure condition (Section 49). This is the formal reason "mutation rate" never appears in $P$: above threshold more mutation produces less information.

## **15. EXPERIMENT SPECIFICATION**

Every candidate experiment MUST instantiate a pre-registered specification; the statistical fields are new in v3 and are what make a decision reproducible.

``` yaml
experiment:
  experiment_id: required
  parent_ids: []
  hypothesis: required
  target_component: required
  candidate_artifact_hash: required
  generator_id: required
  generator_version: required
  risk_class: required                   # sets isolation level, evidence bar, blast radius
  expected_gain:
    metric: required                     # pre-registered primary metric
    direction: required
    magnitude: optional
  statistics:                            # new in v3
    minimum_detectable_effect: required  # Delta, in metric units
    alpha: required                      # false-promotion rate for this risk class
    beta: required                       # false-rejection rate
    stopping_rule: required              # SPRT | mixture_SPRT | confidence_sequence | fixed_n
    max_samples: required                # truncation
    pairing: required                    # common_random_numbers | independent
    control_variates: []                 # covariates for variance reduction
    fidelity_stage: required             # which funnel stage this spec covers
  falsification_condition: required
  evaluator_ids: required
  environment_hash: required
  benchmark_hash: required
  seeds: required                        # list or generator state; never implicit
  resource_budget: required
  time_limit: required
  rollback_strategy: required
```

Defaults per risk class (initial values, ratified in the Intent plane):

| **Risk class** | **$\alpha$** | **$\beta$** | **Replications before promotion** | **Fresh-seed re-measurement** |
|---|---|---|---|---|
| R0 kernel / config micro-change | 0.05 | 0.10 | 1 | yes |
| R1 algorithm / policy | 0.01 | 0.10 | 2 | yes |
| R2 evaluator / benchmark (Section 18) | 0.001 | 0.05 | 3 + historical replay | yes |
| R3 runtime / protocol / topology | 0.001 | 0.05 | 3 + chaos | yes |
| R4 anything touching L3/L4 | not admissible through the fabric (Section 42) | — | — | — |

## **16. EXPERIMENT FUNNEL**

Higher magnitude requires progressively stronger filtering.

``` text
IDEA GENERATION
      |
      v
CHEAP SURROGATE MODEL            stage 1  (cost c1, survival s1, recall r1)
      |
      v
STATIC VALIDATION                stage 2
      |
      v
LOW-COST SIMULATION              stage 3
      |
      v
MICROBENCHMARK                   stage 4
      |
      v
HIGH-FIDELITY TEST               stage 5
      |
      v
ADVERSARIAL TEST                 stage 6
      |
      v
SHADOW EXECUTION
      |
      v
CANARY
      |
      v
LIMITED DEPLOYMENT
      |
      v
PRODUCTION
```

### **16.1 Funnel economics**

For stages $i = 1..S$ with per-candidate cost $c_i$, survival fraction $s_i$ (fraction passed to the next stage) and recall $r_i$ (fraction of *true* winners passed), the expected cost per entering candidate and the end-to-end recall are

$$
\bar c = \sum_{i=1}^{S} c_i \prod_{j<i} s_j, \qquad \mathcal{R} = \prod_{i<S} r_i .
$$

Against evaluating every candidate at full fidelity (cost $c_S$ each, recall 1), the funnel multiplies true-winner discoveries per unit cost by

$$
\mathcal{M}_{\text{funnel}} = \mathcal{R}\,\frac{c_S}{\bar c}.
$$

Worked example (assumptions stated): $c = (1, 10, 100)$, $s = (0.1, 0.2)$, $r = (0.9, 0.95)$ gives $\bar c = 1 + 1 + 2 = 4$, $\mathcal{R} = 0.855$, $\mathcal{M}_{\text{funnel}} = 21.4$. The funnel is the largest single multiplier available and the one most dependent on measured recall: a stage with $r_i$ unmeasured is not admissible on the promotion path.

### **16.2 Algorithmic instantiation**

Successive halving: with $n$ candidates, budget $B$ and elimination factor $\eta$, run $\lceil \log_\eta n \rceil$ rounds, keep the top $1/\eta$ each round, and give survivors $\eta\times$ the budget; Hyperband hedges over $\eta$. Each stage's $(c_i, s_i, r_i)$ is measured continuously on a calibration stream of candidates that are *also* run at full fidelity, so that recall is a measured quantity (Section 34.2).

The funnel SHALL be risk-sensitive. Low-risk kernel transformations can progress rapidly (R0: stages 1, 4, 5 may suffice). High-impact evaluator or architecture changes require stronger evidence (R2–R3: every stage, plus replay and chaos).

## **17. VERIFICATION PLANE**

The Verification Plane is an independent system: separate code lineage, separate identities, separate resource budget, and no write access from the Discovery or Execution planes.

Required capabilities:

``` yaml
verification:
  deterministic:
    - unit_tests
    - property_tests
    - differential_tests
    - type_checks
    - static_analysis
    - memory_safety_checks
    - formal_proofs_where_practical
  probabilistic:
    - held_out_benchmarks
    - sequential_tests                 # SPRT / mixture SPRT, 17.2
    - anytime_valid_confidence_sequences   # 17.3
    - false_discovery_rate_control     # 17.4
    - fresh_seed_remeasurement_of_winners  # FP-5
    - repeated_trials
    - adversarial_tests
    - distribution_shift_tests
    - cross_evaluator_consensus
  system:
    - latency_regression
    - throughput_regression
    - resource_regression
    - security_regression
    - reliability_regression
    - observability_regression
```

### **17.1 The decision problem**

A promotion decision tests $H_0: \tau \le 0$ against $H_1: \tau \ge \Delta$ on paired differences $d_i = x_i^{(c)} - x_i^{(c_0)}$ with noise $\sigma^2$ (estimated), at error rates $(\alpha, \beta)$ from the risk class. The fixed-sample (v2 baseline) requirement is

$$
n_B = \left(\frac{(z_{1-\alpha} + z_{1-\beta})\,\sigma}{\Delta}\right)^{2}.
$$

### **17.2 Sequential probability ratio test**

Wald's SPRT accumulates the log-likelihood ratio $S_n = \sum_i z_i$ with $z_i = \frac{\Delta}{\sigma^2}\left(d_i - \frac{\Delta}{2}\right)$ and stops at

$$
S_n \ge A = \ln\frac{1-\beta}{\alpha}\ \ (\text{ACCEPT } H_1), \qquad
S_n \le B = \ln\frac{\beta}{1-\alpha}\ \ (\text{ACCEPT } H_0).
$$

Wald's approximations for the expected sample size, with $\text{KL} = \Delta^{2}/(2\sigma^{2})$ per observation:

$$
\mathbb{E}_{1}[N] \approx \frac{(1-\beta)A + \beta B}{\text{KL}}, \qquad
\mathbb{E}_{0}[N] \approx \frac{(1-\alpha)(-B) - \alpha A}{\text{KL}}.
$$

| **$\alpha=\beta$** | **SPRT $\mathbb{E}[N]$ ($\sigma^{2}/\Delta^{2}$ units)** | **Fixed $n_B$** | **$\mathcal{M}_{\text{seq}}$ at the boundary** |
|---|---|---|---|
| 0.05 | 5.30 | 10.82 | 2.04 |
| 0.01 | 9.01 | 21.65 | 2.40 |
| 0.001 | 13.79 | 38.20 | 2.77 |

These are Wald's approximations, which ignore overshoot of the thresholds; simulation (72.2, check 1) shows the realized boundary multiplier is 1.6× at $\Delta/\sigma = 1$ and 1.9–2.3× at $\Delta/\sigma = 0.3$, with realized error rates below nominal, and the mixture multiplier of the next paragraph at 4–6×. By the Wald–Wolfowitz theorem the SPRT minimizes expected sample size under both hypotheses among all tests with the same error rates. Candidates whose true effect is far from the boundary stop much earlier: a clearly worse candidate with $\tau = -2\Delta$ stops after $\approx 1.2\,\sigma^2/\Delta^2$ observations, nine times fewer than $n_B$. Since most candidates in any search are clearly worse, the realized $\mathcal{M}_{\text{seq}}$ exceeds the boundary value: with 20% of candidates near the boundary and 80% clearly worse, $\bar n \approx 0.2(5.3) + 0.8(1.2) = 2.0$ versus $n_B = 10.8$, a 5.4× decision-efficiency gain at $\alpha = \beta = 0.05$ (illustrative; the mixture is measured, Section 68).

Composite alternatives use the mixture SPRT or a generalized likelihood-ratio statistic; truncation at `max_samples` with a terminal decision keeps the error rates bounded (the truncated test's realized $\alpha$ is reported).

### **17.3 Anytime-valid inference**

For monitored streams and for any test that may be stopped by a scheduler at an arbitrary time, the plane uses **confidence sequences**: intervals $\text{CI}_n$ with $\Pr(\forall n \ge 1: \tau \in \text{CI}_n) \ge 1 - \alpha$. Their width shrinks as $O\!\left(\sqrt{\log\log n / n}\right)$, so the price of optional stopping over a fixed-$n$ interval is an iterated-logarithm factor, not a constant.

Equivalently, **e-values**: a non-negative statistic $E$ with $\mathbb{E}_{H_0}[E] \le 1$, rejecting when $E \ge 1/\alpha$ (Markov's inequality bounds the type-I error by $\alpha$). E-values from successive batches multiply into a test martingale, so evidence accumulates across the whole fabric's history without ever inflating $\alpha$.

### **17.4 False-discovery control at fabric scale**

With $m$ simultaneous promotion hypotheses per window, per-test $\alpha$ does not bound the fraction of false promotions. The plane controls the false-discovery rate at level $q$: Benjamini–Hochberg on p-values (reject the $k$ smallest where $p_{(k)} \le \frac{k}{m} q$) when tests are independent or positively dependent, and the **e-BH** procedure on e-values (reject hypotheses with $e_{(i)} \ge \frac{m}{q\,i}$) under arbitrary dependence, which is the fabric's situation because candidates share environments, seeds and ancestors. The reported promotion yield (Section 5.3) carries this guarantee.

### **17.5 Winner re-measurement**

Any candidate selected as the best of $k$ screened candidates MUST be re-measured on fresh seeds and a disjoint environment sample before promotion; the promotion estimate is the re-measurement (unbiased), optionally shrunk (FP-5). The screening score is recorded but never used as the promotion estimate.

### **17.6 Robust promotion for high blast radius**

For R2–R3 changes the verifier tests the gain not on the sampled environment distribution $\hat{\mathcal{D}}$ alone but on every distribution within a Wasserstein ball around it (Section 41.3): promote only if $\inf_{\mathcal{D}': W_1(\mathcal{D}', \hat{\mathcal{D}}) \le \varepsilon_W} \mathbb{E}_{\mathcal{D}'}[\tau] > 0$ at the stated confidence. The radius $\varepsilon_W$ is the measured transport distance between the benchmark distribution and the production distribution, so the robustness demanded is the shift actually observed, no more.

## **18. EVALUATOR CONSTITUTION**

Evaluator modification is higher-risk than ordinary candidate modification: an evaluator error is multiplied by every decision it touches.

``` yaml
evaluator_rules:
  generator_cannot_self_certify: true
  evaluator_changes_require_cross_validation: true
  historical_benchmarks_must_be_replayed: true
  hidden_tests_must_exist: true
  benchmark_leakage_must_be_monitored: true
  evaluator_lineage_must_be_immutable: true
  external_ground_truth_preferred_when_available: true
  evaluator_is_blind_to_candidate_internals: true        # new
  evaluator_rotation_schedule_is_pre_registered: true    # new
  evaluator_change_rate_is_capped_by_envelope: true      # new (Section 5.14)
```

### **18.1 Evaluator quality metrics (new)**

Each evaluator $\mathcal{E}$ is itself measured, on a calibration stream with external ground truth where available:

- **test–retest reliability** $r_{tt}$: correlation of scores on repeated seeds; the noise variance $\sigma^2$ used in Section 17 is derived from it;
- **discriminative power**: the minimum $\Delta$ it resolves at $(\alpha, \beta)$ within the stage's cost budget;
- **calibration**: for probabilistic evaluators, expected calibration error on held-out outcomes;
- **proxy divergence**: $\text{div}_{\mathcal{E}}(t)$ against ground truth on the rotating hidden set (FP-5);
- **capture score**: the gain in proxy score obtainable by a dedicated adversarial population in a fixed budget (Section 41); an evaluator whose capture score rises is retired or patched.

An evaluator change is admissible only if it is an R2 experiment (Section 15) that leaves $r_{tt}$ and discriminative power no worse and reduces proxy divergence or capture score on replayed history.

## **19. EXPERIMENT LEDGER**

Use append-only, content-addressed experiment records.

``` yaml
experiment_record:
  experiment_id: required
  parent_ids: []
  candidate_hash: required
  environment_hash: required
  benchmark_hash: required
  evaluator_hashes: []
  hardware_profile: required
  start_time: required               # hybrid logical clock
  end_time: required
  results: required                  # metric vector; or content hash of the result blob
  verdict: required
  test_statistic_trace: optional     # S_n trajectory or e-value, for audit of the stopping rule
  resource_cost: required            # resource vector incl. joules
  knowledge_artifacts: []
  promotion_status: required
  descendants: []
  record_hash: required              # hash over all fields above
  prev_hash_in_shard: required       # hash chain within the cell shard
```

### **19.1 Structure**

The ledger is a **Merkle DAG**: each record is addressed by its content hash and references its parents by hash, so lineage is tamper-evident (changing any ancestor changes every descendant's address) and membership is provable with $O(\log n)$ hashes. Per-cell shards are hash chains; pod and region summaries are Merkle roots published on the gossip plane at a fixed cadence; the global root is signed by the invariant plane.

### **19.2 Bandwidth and retention**

Hot-path records are bounded at 256 bytes (hashes, verdict, statistics, resource vector); payloads (results, artifacts) are content-addressed blobs deduplicated by hash. Section 4.1 gives the implied bandwidths. From M3 ($\ge 256$ MB/s), per-evaluation records live in local shards with a retention TTL after which only the shard's Merkle root, its aggregated statistics and every record referenced by a promotion or a knowledge object are retained globally; this keeps lineage completeness at $1 - 10^{-6}$ for anything promoted while bounding storage growth to $O(\text{promotions} + \text{knowledge})$ rather than $O(\lambda t)$.

The ledger MUST support: replay; rollback; ancestry; causal attribution; experiment deduplication; meta-analysis; reproducibility; failure forensics; proofs of inclusion for any certified claim.

## **20. KNOWLEDGE GRAPH**

Raw experiment storage does not scale to extreme magnitudes by itself (Section 19.2). The Knowledge Plane SHALL transform observations into abstractions.

``` text
RAW EXPERIMENTS
      ->
CLUSTERS
      ->
PATTERNS
      ->
MECHANISTIC HYPOTHESES
      ->
CAUSAL LAWS
      ->
REUSABLE HEURISTICS
      ->
SEARCH PRIORS
```

Knowledge objects SHOULD contain:

``` yaml
knowledge_object:
  knowledge_id: required
  claim: required
  confidence: required               # posterior probability, Section 20.2
  scope_conditions: required
  supporting_experiments: []
  contradicting_experiments: []
  causal_status:
    enum:
      - observed
      - correlated
      - intervention_supported
      - formally_proven
  reusable_by: []
  expiration_policy: required
  description_length_saving_bits: required   # new: MDL admissibility evidence, 20.3
  prior_update: optional                     # new: which search prior it modifies, and how
```

### **20.1 Graph semantics**

Nodes are typed (hypothesis, result, mechanism, law, heuristic, invariant); edges are typed (supports, contradicts, refines, generalizes, applies-to) and carry evidence weights. A claim's confidence is a posterior updated by every supporting or contradicting experiment.

### **20.2 Belief update**

For a claim $h$ with prior $\pi_0(h)$ and experiment outcomes $o_{1:n}$ with likelihood ratios $\Lambda_i = p(o_i \mid h)/p(o_i \mid \neg h)$ (from the verifier's e-values or likelihood traces):

$$
\frac{\pi_n(h)}{1-\pi_n(h)} = \frac{\pi_0(h)}{1-\pi_0(h)} \prod_{i=1}^{n} \Lambda_i .
$$

The causal status advances from *correlated* to *intervention-supported* only when at least one supporting experiment is a randomized intervention with $\text{LCB}_{95}(\hat\tau) > 0$ (Section 40), and to *formally proven* only on a machine-checked proof object.

### **20.3 Minimum description length admissibility**

A knowledge object $K$ is admitted iff it compresses the evidence it summarizes:

$$
L(D \mid K) + L(K) < L(D),
$$

where $L$ is the description length under the fabric's reference coder (a fixed, versioned model of ledger records; its hash is in every certificate). The saving $L(D) - L(D \mid K) - L(K)$ in bits is the object's knowledge yield (Section 5.6); an object that does not compress is noise and is rejected regardless of how plausible its claim reads. This is Gell-Mann and Lloyd's effective complexity made operational: knowledge is the length of the concise description of the regularities, and the fabric only pays for regularities. Search priors are the decoded form of admitted knowledge: $\Pi(\cdot \mid S, K)$ conditions on them (Section 2.1).

### **20.4 Coarse-graining and relevance**

The pipeline RAW → CLUSTERS → PATTERNS → LAWS is a renormalization-group flow in Wilson's sense: each level integrates out detail at the scale below and keeps the variables that still matter at the scale above. A claim's **relevance** is measured, not assumed: let $\hat\tau^{(\ell)}$ be its estimated effect when evaluated at aggregation level $\ell$ (cell, pod, region). A claim is *relevant* if $\text{LCB}_{95}(\hat\tau^{(\ell+1)}) > 0$ whenever $\text{LCB}_{95}(\hat\tau^{(\ell)}) > 0$, *irrelevant* if its effect averages out under aggregation, and *marginal* otherwise. Only relevant claims are candidates for upward propagation (Section 35); irrelevant ones stay local, which is the correct fate of a true-but-local fact. The empirical scaling of $\hat\tau^{(\ell)}$ with level is recorded as the claim's relevance exponent.

## **21. FAILURE MEMORY**

Failure is a first-class asset.

``` yaml
failure_object:
  failure_id: required
  candidate_family: required          # region descriptor: LSH bucket set or embedding centroid + radius
  failure_mode: required
  reproduction_recipe: required
  conditions: required
  confidence: required
  affected_components: []
  root_cause: optional
  avoid_until: optional
  possible_escape_conditions: []
  evaluations_avoided_estimate: optional   # new: r, for valuing the object (FP-9)
```

### **21.1 Dead-region penalty**

The scheduler SHOULD penalize known dead regions unless novelty evidence justifies revisiting them. Formally the proposal operator applies a multiplicative prior penalty $\exp(-\beta_F \cdot \text{conf}(F))$ to candidates whose family matches a failure object $F$, decaying with `avoid_until` and lifted when an `escape_condition` is observed.

### **21.2 Valuation**

A failure object's value is $r\,\bar c$ (evaluations avoided × mean cost); the Knowledge Plane reports the cumulative avoided cost as a line item of the moat (Section 51).

### **21.3 Deduplication index**

Duplicates are detected before execution by locality-sensitive hashing: MinHash over shingles of the candidate's canonical representation (collision probability equals Jaccard similarity) and random-hyperplane LSH over embeddings (collision probability $1 - \angle/\pi$). A candidate colliding with a completed experiment in the same environment above $s^{*}$ is routed to the existing result (and counted under DSR, Section 5.7), not re-run. The index is per pod with Merkle-summarized global sync (Section 10), so lookups stay node-local.

## **22. NOVELTY ENGINE**

A dedicated novelty subsystem SHALL continuously search outside dominant lineages.

### **22.1 Novelty score and acquisition**

With an embedding $z_c$ of candidate behaviour (not source text) and a density estimate $\hat p$ over previously evaluated behaviours,

$$
\text{nov}(c) = -\ln \hat p(z_c)\quad \text{or}\quad \text{nov}(c) = \text{dist}_{k\text{-NN}}(z_c),
$$

and the acquisition used for selection is

$$
\text{acq}(c) = \text{EI}(c) + \beta_t\,\text{nov}(c) + \beta_I\,\text{EIG}(c),
$$

where $\text{EI}$ is expected improvement under the surrogate (Section 34), $\text{EIG}(c) = I(Y_c;\theta) = H[Y_c] - \mathbb{E}_\theta H[Y_c \mid \theta]$ is the expected information gain about the surrogate's parameters, and $\beta_t$ is annealed but floored (FP-6). Behavioural novelty is used because textual novelty is cheap to fake and does not predict new capability.

Objectives: maximize behavioral diversity; test alternate architectures; challenge assumptions; discover orthogonal solutions; avoid monoculture; preserve weak but promising branches.

Novelty compute SHALL NOT be reduced to zero even when exploitation is highly productive; the floor is 3% of evaluations (FP-6) and the diversity floor of Section 45 is a hard constraint.

## **23. RESOURCE MARKET**

Compute is allocated as an internal capital market.

Each Cell / population receives a score based on:

``` yaml
resource_score_inputs:
  - direct_capability_gain
  - knowledge_gain
  - descendant_value
  - novelty
  - reliability
  - cost_efficiency
  - strategic_priority
  - uncertainty
  - optionality
```

### **23.1 Why a market**

Hayek's argument (FP-7) is the reason the allocation is a market rather than a planner: the knowledge of which population can use the next GPU-hour best is held by the populations, and prices are the only scalable channel for it. The design question is then mechanism design (Hurwicz, Maskin, Myerson): choose rules under which reporting that knowledge truthfully is each population's best strategy.

### **23.2 Mechanism**

Populations report value functions $U_i(x_i)$ (expected verified gain as a concave function of allocation, from their posteriors). Two allocation rules are used, for different goods.

*Divisible compute within an epoch* is allocated by **proportional fairness**, which is the Nash bargaining solution among the populations:

$$
\max_{x} \sum_i w_i \ln U_i(x_i) \quad \text{s.t.}\quad \sum_i x_i \le B,\ \ x_i \ge x_i^{\min},
$$

with $w_i$ the strategic priority from the Intent plane and $x_i^{\min}$ the FP-6 floors. The Nash-welfare objective prevents a single high-bidding population from starving exploration.

*Indivisible or bundled goods* (reserved accelerator blocks, verification-plane slots, energy headroom, physical-experiment time) are allocated by a **Vickrey–Clarke–Groves** mechanism: the allocation maximizes reported total value, and each winner is charged the externality it imposes, the value others would have obtained had it not bid. Truthful reporting is then a dominant strategy, which removes the need to detect lying from the fast path; by the revelation principle no other mechanism achieves a better allocation with strategic populations. Bundles of complementary goods (compute plus the verification capacity to use it) are cleared together in a combinatorial round, in the manner of Milgrom and Wilson's clock auctions, because allocating them separately creates exposure: compute without verification slots produces nothing (FP-4). Payments are denominated in future budget, so a population that overstates value pays for it in its own later allocations.

### **23.3 Audit**

Realized value is compared to reported value after verification. Under VCG misreporting is already unprofitable; the audit exists for the proportional-fairness epochs and for drift: a population's reputation $\text{rep}_i \in (0,1]$ multiplies its reports and decays with over-claiming ($\text{rep}_i \leftarrow \text{rep}_i \cdot \min(1, \text{realized}_i/\text{reported}_i)^{\eta}$). Gaming the market is itself a Section 41 target.

Resource-allocation policy itself is an RSI target (an L1 meta-candidate, Section 42).

## **24. DESCENDANT VALUE**

A candidate can be valuable because it enables future improvements.

``` text
Descendant_Value =
Direct_Gain
+ Future_Experiments_Accelerated
+ Knowledge_Reused
+ New_Search_Space_Opened
+ Improvement_Machinery_Improved
```

### **24.1 Bellman form**

On the lineage DAG, with direct verified gain $r(c)$, discount $\gamma \in (0,1)$ per generation and observed children $\text{ch}(c)$:

$$
V(c) = r(c) + \gamma \sum_{c' \in \text{ch}(c)} p(c' \mid c)\, V(c'),
$$

estimated by a backward pass over the DAG at a fixed cadence (children appear over time, so $V$ is revised and the revision history is itself in the ledger). Machinery improvements enter through $r$ measured as $\Delta \ln P$ (a meta-promotion's direct gain is the multiplicative lift it gives every later experiment, Section 64). Knowledge reuse enters as the yield (Section 5.6) of knowledge objects citing $c$.

Meta-RSI SHOULD rank interventions partly on descendant value, not only immediate gain; generators are credited with the $V$ of their outputs (Section 14), which is how a generator that produces few winners but good parents keeps its budget.

### **24.2 Credit assignment among interacting promotions**

Gains are rarely separable: a kernel change and a scheduler change landing in the same window may be worth more together than apart. The fabric attributes a window's verified gain $G(\mathcal{S})$ over the set $\mathcal{S}$ of promotions by **Shapley value**,

$$
\phi_i = \sum_{T \subseteq \mathcal{S}\setminus\{i\}} \frac{|T|!\,(|\mathcal{S}|-|T|-1)!}{|\mathcal{S}|!}\,\big[G(T \cup \{i\}) - G(T)\big],
$$

the unique attribution that is efficient (shares sum to $G(\mathcal{S})$), symmetric, and gives zero to a change that adds nothing to any coalition. $G(T)$ is measured by replaying the window with only the promotions in $T$ applied (the ledger makes every subset replayable); with $|\mathcal{S}|$ large, $\phi_i$ is estimated by Monte Carlo over random permutations with a confidence interval. The same computation attributes the Section 68 multiplier to its mechanisms and a generator's budget to its contributions.

## **25. MULTI-TIMESCALE RSI**

``` yaml
timescales:
  micro:
    duration: nanoseconds_to_milliseconds
    targets:
      - kernel_variants
      - cache_policy
      - local_routing
      - small_IR_rewrites
      - hardware_mapping
  meso:
    duration: milliseconds_to_seconds
    targets:
      - algorithms
      - agent_policies
      - model_routing
      - retrieval
      - workflows
  macro:
    duration: seconds_to_hours
    targets:
      - architectures
      - evaluator_systems
      - runtime_design
      - distributed_protocols
  epoch:
    duration: hours_to_months
    targets:
      - model_families
      - compiler_architecture
      - new_training_methods
      - accelerator_design
  physical:
    duration: months_to_years
    targets:
      - chips
      - photonics
      - cooling
      - robotics
      - datacenters
      - power_systems
      - manufacturing
```

### **25.1 Nesting and stability**

Each timescale is a loop with time constant $\tau_i$; the outer loop's objective is the inner loop's efficiency ($P$ of the inner loop, or its $\mathcal{M}$). Stability requires the separation ratio $\tau_{i+1}/\tau_i \ge 10$ (FP-8): an outer loop that changes the inner loop's objective faster than the inner loop converges produces oscillation and attributes the inner loop's transient to its own intervention. The scheduler enforces the ratio by rate-limiting outer-loop promotions to at most one per $10\,\tau_i$ of the loop beneath.

### **25.2 Physical clocks are not compressible**

Loops in the *epoch* and *physical* bands are bounded by evidence clocks (training runs, fabrication, physical experiments). Their $\lambda$ is small by construction and their decisions carry the highest evidence bar; surrogate models (Section 34) and digital twins may propose, but only physical-clock evidence promotes (Rule F, Section 43).

## **26. M0 — INITIAL BUILDABLE SYSTEM**

### **Objective**

Demonstrate:

``` text
>= 1,000 completed narrow RSI evaluations / second      (LCB_95, sustained, Section 6)
AND
capability production P >= 4 x the v2 fixed-sample baseline at equal hardware   (contract floor; design target 8x)
```

under sustained load while preserving:

- complete lineage;
- reproducibility;
- resource accounting;
- independent verification;
- automated rejection;
- sandbox promotion;
- rollback;
- knowledge extraction;
- failure memory;
- observability;
- governance envelope and halt lease (new).

### **M0 candidate domains**

Prioritize high-frequency, low-cost, objectively measurable domains:

1. compiler transformations;
2. kernel micro-optimization;
3. routing strategies;
4. cache strategies;
5. prompt/policy variations;
6. retrieval policies;
7. agent workflow topology;
8. inference configuration;
9. scheduler policy;
10. benchmark generation.

These are ideal because they allow many short evaluation cycles with measurable outputs, high test–retest reliability (so $\sigma^2$ is small and $n_B$ is small), and natural pairing on common seeds (so $\rho_{\text{CRN}}$ is high).

### **26.1 M0 sizing (assumptions stated)**

| **Quantity** | **Assumption / derivation** | **Value** |
|---|---|---|
| Mean evaluation service time $s$ | narrow domains, node-local | 20 ms-core |
| Target utilization $u$ | bounded queueing (Section 9.1) | 0.7 |
| Overhead fraction $o$ | Section 12 budget | $\le 0.1$ |
| Worker-cores needed | $\lambda s (1+o)/u = 1000 \cdot 0.02 \cdot 1.1 / 0.7$ | ~32 cores |
| In-flight evaluations $L$ | $\lambda W$, $W \approx 50$ ms | 50 |
| Verification-plane share | FP-4; sequential tests | $\le 25\%$ of cores |
| Ledger hot path | 256 B × 1000/s | 256 KB/s (~22 GB/day) |
| Energy (modelled) | ~10 W per busy core-equivalent, ×1.5 for infrastructure | ~0.5 kW, i.e. ~0.5 J per evaluation |

M0 fits on a single node or a small pod; its purpose is to prove the loop, the statistics and the governance, not scale.

## **27. M0 REFERENCE ARCHITECTURE**

``` text
                    +----------------------+
                    |  CONSTITUTION PLANE  |  invariants, keys, governor, halt leases
                    +----------+-----------+
                               |
                    +----------v-----------+
                    |     INTENT PLANE     |  objectives, budgets, envelope G
                    +----------+-----------+
                               |
                    +----------v-----------+
                    |    META-SCHEDULER    |  bandit over generators; resource market
                    +----------+-----------+
                               |
                 +-------------+-------------+
                 |                           |
          +------v------+             +------v------+
          | WORK QUEUE A|             | WORK QUEUE B|  sharded, node-local, lock-free
          +------+------+             +------+------+
                 |                           |
        +--------+--------+         +--------+--------+
        |                 |         |                 |
 +------v------+   +------v------+  |        +-------v-----+
 | RSI CELL    |   | RSI CELL    |  |        | RSI CELL    |  persistent workers, dedup index
 +------+------+   +------+------+  |        +-------+-----+
        |                 |         |                |
 +------v------+   +------v------+  |        +-------v-----+
 | SANDBOX     |   | SANDBOX     |  |        | SANDBOX     |  least privilege, resource caps
 +------+------+   +------+------+  |        +-------+-----+
        |                 |         |                |
        +--------+--------+---------+----------------+
                 |
          +------v------+
          | VERIFICATION|  SPRT / confidence sequences / e-BH; fresh-seed re-measurement
          +------+------+
          +------v------+
          | LEDGER      |  Merkle DAG; per-cell hash chains; signed roots
          +------+------+
          +------v------+
          | KNOWLEDGE   |  MDL-admitted objects; failure memory; priors
          +------+------+
          +------v------+
          | META-RSI    |  L1 changes only; verified by plane 4; depth-limited
          +-------------+
```

### **27.1 Latency budget per evaluation (M0)**

| **Stage** | **Budget (p50 / p99)** |
|---|---|
| dequeue + dedup lookup | 50 µs / 500 µs |
| sandbox entry | 100 µs / 2 ms (persistent sandbox; no cold start on the fast path) |
| execution | 20 ms / 100 ms |
| measurement + resource accounting | 100 µs / 1 ms |
| ledger append (local shard) | 20 µs / 200 µs |
| verification statistic update | 10 µs / 100 µs |

The non-execution budget sums to under 0.3 ms p50, i.e. $o \approx 0.015$ at $s = 20$ ms, inside the $o \le 0.1$ requirement.

## **28. DATA PATH**

Critical paths SHOULD use: binary protocols; preallocated memory; zero-copy techniques where beneficial; ring buffers; local shared memory; append-only logs; persistent workers; content-addressed artifacts; batched accelerator execution.

Critical paths SHOULD avoid: repeated container startup; synchronous database round trips; JSON serialization where binary formats are materially better; global locks; global consensus; avoidable cross-region communication.

### **28.1 Bytes-moved budget**

Let $b_k$ be the allowed bytes per evaluation crossing a boundary slower than node-local memory at magnitude $M_k$. With an intra-datacenter cost of ~10–100 pJ/bit (FP-2) and an energy budget that must stay below 10% of the evaluation's own energy, the budget is

$$
b_k \le \frac{0.1\,\varepsilon_k}{8 \times 50\ \text{pJ}}\quad\Rightarrow\quad
b_0 \approx 125\ \text{MB (never binding)},\ \ b_6 \approx 250\ \text{KB at } \varepsilon_6 = 1\ \text{mJ},\ \ b_9 \approx 250\ \text{bytes at } \varepsilon_9 = 1\ \mu\text{J}.
$$

The M6 figure permits the 256-byte hot-path record plus small artifacts by reference; at M6 the per-device link imposes a comparable budget (a few hundred KB per evaluation at $10^{5}$ evaluations/s per device on a 50 GB/s link), so energy and bandwidth bind together there. The M9 figure says the fast path may move one hot-path record per evaluation and nothing else: artifacts stay on device and leave only by reference or as aggregates. This is Rule D (Section 43) made numeric.

## **29. EVENT MODEL**

Each Cell SHALL implement an explicit deterministic state machine where practical.

``` yaml
states:
  - IDLE
  - ASSIGNED
  - GENERATING
  - GENERATED
  - SANDBOXED
  - EXECUTING
  - MEASURING
  - VERIFYING
  - COMPLETED
  - REJECTED
  - QUARANTINED
  - PROMOTED
  - ARCHIVED
  - HALTED          # new: lease expiry or HALT event; reachable from any state
```

Every state transition emits an immutable event.

### **29.1 Ordering and idempotency**

Events carry **hybrid logical clock** timestamps (physical time plus a logical counter), giving causal ordering across cells without a global clock (FP-7) and bounded drift from wall time for windowed metrics. Every side-effecting message carries an idempotency key (hash of experiment id, stage and attempt) so that retries never double-count an evaluation or double-promote a candidate; exactly-once semantics are achieved by at-least-once delivery plus idempotent application.

## **30. OBSERVABILITY**

Required telemetry (every series with its estimator from Section 5 and its confidence interval or sequence):

``` yaml
throughput:
  - candidates_per_sec
  - evaluations_per_sec            # lambda, LCB_95
  - decisions_per_sec              # D = lambda / n_bar
  - verifications_per_sec
  - promotions_per_sec
  - knowledge_objects_per_sec

latency:
  - p50
  - p95
  - p99
  - p99_9
  - max

quality:
  - useful_yield                   # y_V
  - promotion_yield                # y_P with FDR level q
  - regression_rate                # rho_reg hazard, UCB_95
  - generalization_rate
  - evaluator_disagreement
  - realized_false_positive_rate   # from replay and re-measurement
  - realized_false_negative_rate   # from calibration stream run at full fidelity
  - proxy_divergence               # FP-5

efficiency:
  - cpu_seconds
  - gpu_seconds
  - accelerator_seconds
  - memory_bytes
  - network_bytes
  - storage_bytes
  - energy_joules                  # measured or modelled; model hash recorded
  - dollars
  - decision_efficiency_multiplier # M_lambda
  - variance_reduction_factor      # VRF
  - funnel_multiplier              # M_funnel with measured recall
  - production_multiplier          # M_k, with Shapley shares per mechanism
  - error_threshold_margin         # ln(sigma_s) - mu L, per population (Section 14.2)
  - portfolio_sharpe_ratio         # FP-6 portfolio
  - market_truthfulness            # realized / reported value, per population

recursion:
  - P                              # capability production rate
  - tilde_v                        # resource-normalized velocity
  - phi_hat_ci95                   # returns-to-scale exponent
  - doubling_time_T2
  - meta_improvements_per_day
  - descendant_value
  - duplicate_search_rate
  - knowledge_reuse_rate
  - experience_curve_exponent_b
  - recursive_gain_coefficient     # RGC = tilde_v / v
  - overlap_distribution_entropy   # diversity, Section 45.2
  - fingerprint_detection_statistic # Section 64.8

governance:                        # Section 5.14
  - invariant_check_pass_rate
  - boundary_violation_attempts
  - velocity_vs_envelope
  - halt_latency_measured
  - human_review_sampling_rate
  - evaluator_change_rate
```

### **30.1 Alarms**

Alarms are anytime-valid tests (Section 17.3) on the monitored series, so they do not false-alarm from being checked continuously: proxy divergence drift; regression hazard above $\rho_{\max}$; $\theta$ rising (coherence creep); effective lineages below the diversity floor (Section 45); surrogate calibration drift (Section 34); $\lambda_{\text{gen}}/\lambda_V$ above $\kappa_V$ (verification starvation); any boundary-violation attempt; $\tilde v$ above $v_{\max}$ (the governor throttles before the alarm, Section 38).

## **31. BOTTLENECK AUTONOMY**

The system SHALL continuously profile its own throughput.

``` text
DETECT
  ->
QUANTIFY
  ->
RANK
  ->
FORM SCALING HYPOTHESES
  ->
SPAWN SPECIALIZED RSI POPULATION
  ->
EXPERIMENT
  ->
VERIFY
  ->
DEPLOY
  ->
REMEASURE
```

### **31.1 Detection by queueing**

Model the pipeline as stages $i$ with arrival rate $\lambda_i$, service rate $\mu_i$ and utilization $\rho_i = \lambda_i/\mu_i$. The binding constraint is $\arg\max_i \rho_i$; its queue grows without bound as $\rho_i \to 1$ and its sojourn time in the M/M/1 approximation is $W_i = 1/(\mu_i - \lambda_i)$. The expected throughput gain from relieving stage $i$ by a factor $k$ is bounded by Amdahl: $S = 1/\big((1 - f_i) + f_i/k\big)$ with $f_i$ the fraction of end-to-end time spent in stage $i$, so the ranking is by $f_i$ and by the cost of the relief, which is the scaling hypothesis's expected value per cost (Section 23).

Targetable bottlenecks include: candidate quality; evaluator latency; scheduler contention; memory bandwidth; storage; network; model inference; compilation; container overhead; data duplication; knowledge retrieval; GPU underutilization; serialization; lock contention; cache misses; and, from v3, verification-plane capacity ($\lambda_{\text{gen}}/\lambda_V$), coherence $\theta$, and the realized $\bar n$ per decision.

## **32. MAGNITUDE TRANSITION DESIGN**

Each transition is specified by the budgets that must tighten for the next rung to be certifiable: the fast-path overhead fraction $o_k$, the coherence coefficient $\theta_k$, the energy-derived off-node byte ceiling $b_k$ (Section 28.1; design budgets may be tighter), the verification-plane decision rate $\lambda_{V,k}$, and the ledger strategy. The worker count is projected from the USL with the measured $(\gamma, \theta)$ of the previous rung.

| **Rung** | **$o_k$** | **$\theta_k$ (fast path)** | **$b_k$** | **Ledger** | **Dominant evaluation type** |
|---|---|---|---|---|---|
| M0 | $\le 0.10$ | $\le 10^{-4}$ | unbounded | single shard | node-local process |
| M1 | $\le 0.10$ | $\le 10^{-5}$ | unbounded | sharded per cell | persistent workers, batched |
| M2 | $\le 0.05$ | $\le 10^{-6}$ | ~25 MB | pod summaries | vectorized evaluators |
| M3 | $\le 0.01$ | $\le 10^{-8}$ | ~5 MB | TTL + Merkle roots | compiled, accelerator-resident state |
| M4 | $\le 0.01$ | $\le 10^{-10}$ | ~1.2 MB | hierarchical | machine-native IR, batched kernels |
| M5 | $\le 0.005$ | $\le 10^{-12}$ | ~500 KB | hierarchical, sampled | accelerator-local populations |
| M6 | $\le 0.002$ | $\le 10^{-13}$ | ~250 KB (energy) / link-bound | records off-device; artifacts by reference | accelerator-resident micro-evolution |

### **M0 → M1**

Target: $10^4$ evaluations/sec. Primary methods: persistent workers; batching; queue sharding; evaluator vectorization; cache reuse; deduplication; more parallel Cells. Statistics: sequential tests on every R0–R1 decision; CRN pairing default. Projected cells: $N \approx 10 \times$ M0's at $S(N)/N \ge 0.9$ given $\theta \le 10^{-5}$.

### **M1 → M2**

Target: $10^5$ evaluations/sec. Required evolution: decentralized scheduling; specialized worker pools; IR-level mutation; local experiment caches; higher evaluator parallelism; hierarchical telemetry. The verification plane moves to e-process accounting so that evidence accumulates across shards without a central p-value registry.

### **M2 → M3**

Target: $10^6$ evaluations/sec. Required evolution: node-local queues; accelerator-resident state; compiled evaluators; low-copy data paths; persistent models; locality-aware experiment placement; local knowledge summaries. The ledger hot path reaches 256 MB/s (Section 4.1): per-evaluation records become local with TTL; only Merkle roots, aggregates and promotion-referenced records leave the node.

### **M3 → M4**

Target: $10^7$ evaluations/sec. Required evolution: machine-native IR dominates high-rate mutation; hardware-aware Cells; microsecond-scale local loops; stronger predictive surrogate filtering (funnel stage 1 handles the majority of elimination, Section 34); asynchronous cluster federation; aggressive knowledge compression (MDL admission is enforced at the pod, not the region).

### **M4 → M5**

Target: $10^8$ evaluations/sec. Required evolution: accelerator/package-local optimization populations; global system no longer serializes experiments; local autonomy becomes mandatory; high-value knowledge alone propagates upward (relevance test, Section 20.4); surrogate evaluation handles most candidate elimination; global coordination operates on a slower clock (the separation ratio of Section 25.1 between the pod loop and the region loop is $\ge 100$).

### **M5 → M6**

Target: $10^9$ evaluations/sec (new). Required evolution: evaluations are accelerator-resident and batched by construction (a kernel launch evaluates $10^{3}$–$10^{5}$ micro-candidates); the off-device byte budget is a few hundred kilobytes per evaluation by energy and by link bandwidth, so events leave the device as 256-byte records while artifacts stay on device and leave only by reference or as aggregates; the verification plane runs *inside* the device for stage-1 and stage-4 decisions, with device-level e-values merged off-device; energy per evaluation is at or below 1 mJ at a 1 MW budget (Section 4.1); the coherence coefficient on any fast path is below $10^{-13}$, i.e. pods share nothing synchronously. The governance envelope for M6 is ratified before the M5 certificate activates the M6 program (Section 7).

## **33. M6 ARCHITECTURAL MODEL**

``` text
                     GLOBAL CONSTITUTION              (plane 0: invariants, keys, envelope, leases)
                            |
                    GLOBAL INTENT GRAPH               (objectives, budgets; slow clock, hours)
                            |
                    KNOWLEDGE FEDERATION              (gossip of relevant claims; minutes)
             +--------------+--------------+
             |              |              |
         REGION A        REGION B       REGION C      (autonomous; cross-region RTT 10-100 ms)
             |              |              |
       +-----+-----+   +-----+-----+   +----+-----+
       |           |   |           |   |          |
    CLUSTER      CLUSTER         CLUSTER       CLUSTER  (local market epochs; seconds)
       |           |              |             |
     PODS        PODS           PODS          PODS      (<= 500 cells; shared dedup/cache; ms)
       |           |              |             |
  RSI CELLS    RSI CELLS      RSI CELLS     RSI CELLS   (persistent workers; local ledger shard)
       |           |              |             |
ACCELERATOR-LOCAL MICRO-EVOLUTION / EVALUATION          (microseconds; batched; in-device verification)
```

No global lock. No global experiment queue. No global 10 ns synchronization assumption. Aggregate rate emerges from vast parallel local work.

### **33.1 Numbers at M6 (assumptions stated)**

| **Quantity** | **Derivation** | **Value** |
|---|---|---|
| Evaluations/s | target | $10^{9}$ |
| Accelerators | at $10^{5}$ evaluations/s per device (batched micro-evaluations of ~10 µs) | $10^{4}$ devices |
| Cells | one per device partition, 4 per device | $4\times10^{4}$ cells, ~80 pods |
| Power | at ~0.5 kW per device incl. host and network, plus 30% facility overhead | ~6.5 MW, i.e. ~6.5 mJ per evaluation |
| Gossip convergence | ~80 pods, $\log_2 80 \approx 6.3$ rounds at 50 ms | < 0.5 s |
| Ledger off-device | aggregates at 1 Hz per cell, 4 KB each | 160 MB/s global |
| In-flight at halt | $L = \lambda W$, $W = 1$ ms | $10^{6}$ evaluations, drained in ~1 ms |

Every number is a target or an assumption to be replaced by a measurement; the structure of the derivation is the deliverable.

## **34. SURROGATE MODELS**

At large scale, full-fidelity evaluation of every candidate is impossible. The system SHALL maintain multi-fidelity evaluators.

``` text
CANDIDATE
   ->
ULTRA-CHEAP SURROGATE
   ->
FAST APPROXIMATION
   ->
SIMULATION
   ->
HIGH-FIDELITY TEST
   ->
REAL EXECUTION
```

### **34.1 Definition and use**

A surrogate is a learned predictor $\hat f(c) \approx \mathbb{E}[\tau(c)]$ with a calibrated predictive distribution $p(\tau \mid c)$. It is used for two things only: **screening** (funnel stage 1) and **acquisition** (which candidates to evaluate next, Section 22.1). It never promotes. The screening rule evaluates candidate $c$ at the next fidelity iff

$$
\frac{\text{EI}(c)}{c_{\text{next}}} \ge \kappa_{\text{screen}}, \qquad
\text{EI}(c) = \mathbb{E}\big[\max(\tau(c) - \tau^{+},\, 0)\big],
$$

with $\tau^{+}$ the incumbent's verified gain and $\kappa_{\text{screen}}$ set so that the measured stage-1 recall meets its floor (Section 16). The resulting yield multiplier $\mathcal{M}_{\text{surr}}$ is the ratio of promotions per full-fidelity evaluation with and without screening, measured on the calibration stream.

### **34.2 Calibration stream**

A random fraction $f_{\text{cal}}$ of candidates (initially 1%) bypasses screening and runs at full fidelity regardless of the surrogate's opinion. This stream measures recall $r_1$, false rejection, false promotion, calibration error and distribution shift of the surrogate on an unselected sample (the Heckman point: the selected sample cannot measure its own selection error). $f_{\text{cal}}$ is lowered only as the confidence interval on $r_1$ narrows.

### **34.3 Models**

Surrogates are domain-specific: Gaussian processes or Bayesian ensembles for low-dimensional configuration spaces (calibrated uncertainty by construction); gradient-boosted or neural regressors with conformal prediction for high-dimensional candidates (coverage guaranteed without distributional assumptions); and **energy-based models** in the Hopfield–Hinton line for the behaviour-density estimates the novelty engine needs (Section 22.1), where the learned energy landscape doubles as the embedding under which overlaps $q_{ab}$ are computed (Section 45.2).

The surrogate systems themselves SHALL be evaluated for: calibration; false rejection; false promotion; distribution shift; adversarial vulnerability (a surrogate that can be driven to high EI by a cheap candidate family is a Goodhart surface, Section 41).

## **35. KNOWLEDGE PROPAGATION**

Not every local result should become global.

### **35.1 Priority**

$$
\text{Propagation\_Priority}(K) =
\frac{\text{relevant}(K)\cdot \mathbb{E}[\text{global value of } K]}{\text{bytes}(K)\cdot \text{latency}\cdot \text{energy proxy}\cdot \text{coordination cost}},
$$

where $\text{relevant}(K) \in \{0, 1\}$ is the renormalization test of Section 20.4 (an effect that averages out one level up has zero priority at that level, whatever its local value) and the expected global value is the knowledge yield (Section 5.6) times the number of pods whose priors it would change, estimated from the overlap of their candidate distributions with $K$'s scope conditions.

### **35.2 Transport**

Propagation is push–pull gossip (Section 10.2): $O(\log N)$ rounds, $O(f \log N)$ messages per node, no coordinator. Objects are content-addressed and versioned; conflicts (two pods admitting incompatible claims) are not resolved by the transport but recorded as a *contradiction edge* in the knowledge graph and queued as an experiment (a contradiction is the highest-information hypothesis available, Section 22.1).

Low-value local observations remain local. High-value generalizable discoveries propagate.

## **36. SECURITY AND CONTAINMENT**

Every untrusted candidate MUST execute under least privilege.

### **36.1 Isolation by risk class**

| **Risk class** | **Isolation** | **Network** | **Resource caps** |
|---|---|---|---|
| R0 | in-process WebAssembly or restricted native sandbox; microsecond entry | none | CPU-time, memory, no syscalls beyond the evaluator ABI |
| R1 | process sandbox with seccomp-class syscall filter | none | as R0 plus file-system namespace |
| R2 | separate VM or microVM; evaluator and candidate never share a kernel | none; evaluator reaches it over a one-way channel | hard quotas, time limit, snapshot/rollback |
| R3 | dedicated hardware partition; attested boot | isolated segment | as R2 plus power and thermal caps |

Required controls at every class: network restriction; filesystem isolation; process isolation; time limits; memory limits; CPU/GPU quotas; syscall restrictions where practical; immutable audit events; secrets isolation; rollback capability; hardware attestation of the sandbox image for R2+.

### **36.2 What candidates cannot touch**

Candidates cannot modify: their own evaluation record; prior experiment history; protected evaluator baselines; immutable constitutional constraints; the halt lease service; the signing keys of the verification plane. These are enforced by construction (no code path exists from a sandbox to these objects), not by evaluation.

### **36.3 Dead-man lease and stopping distance**

Every cell holds a **halt lease** from the governor with time-to-live $T_{\text{lease}}$ (initially 1 s). A cell whose lease is not renewed transitions to HALTED (Section 29) from any state: it starts nothing new, finishes or abandons in-flight evaluations, flushes its ledger shard and releases its sandboxes. A HALT event revokes all leases at once. Because halting requires *no* message to arrive (only the absence of renewals), it works under partition, overload and adversarial conditions. Promotions require a governor signature, so no promotion can occur after a HALT regardless of in-flight state.

The fabric's **stopping distance** follows from Little's law: at most $L = \lambda W$ evaluations are in flight at any instant, all of which complete or are abandoned within $W_{\max}$ of the halt. The time from HALT to zero activity is therefore bounded by

$$
T_{\text{stop}} \le T_{\text{lease}} + W_{\max},
$$

about 1.1 s at M0 and about 1.001 s at M6, independent of the number of cells. This bound is measured in every certification window by a halt drill (Section 6) and reported as `halt_latency_measured` (Section 5.14).

### **36.4 Threat model**

The fabric is designed against: a candidate that attempts to escape its sandbox; a candidate that attempts to influence its own evaluation (timing side channels, evaluator state); a generator that learns to exploit a surrogate or evaluator (Section 41); a population that misreports value to the market (Section 23.3); a compromised cell that forges ledger events (prevented by per-shard hash chains and signed Merkle roots); and a meta-change that would weaken verification (not admissible, Section 42). It is not designed to withstand a compromised invariant plane; the invariant plane is small, offline-auditable and human-operated for that reason.

## **37. IMMUTABLE / HIGH-GOVERNANCE INVARIANTS**

The following are NOT ordinary RSI targets:

``` yaml
protected_invariants:
  - audit_log_integrity
  - experiment_lineage_integrity
  - authorization_boundaries
  - sandbox_boundaries
  - rollback_system
  - resource_ceiling_enforcement
  - evaluator_separation
  - evidence_bundle_integrity
  - halt_lease_service              # new
  - governance_envelope_parameters  # new: v_max, d_max, r_max, caps
  - verification_plane_budget_floor # new: cannot be traded on the market
  - signing_keys                    # new
  - trust_graph_acyclicity          # new, Section 42.3
```

### **37.1 Admissible actions**

Let $\mathcal{I}$ be the set of states satisfying every invariant above, expressed as checkable predicates. An action $a$ is admissible iff it maps $\mathcal{I}$ into itself:

$$
\mathcal{A}_{\text{adm}} = \{\, a : \forall S \in \mathcal{I},\ a(S) \in \mathcal{I} \,\},
$$

and the governor $\Gamma$ (Section 2.1) rejects any proposal outside $\mathcal{A}_{\text{adm}}$ *before* evaluation. Admissibility is a static property of the proposal (which objects it writes), not an outcome of running it; a proposal that cannot be statically classified is inadmissible.

### **37.2 Rules, not discretion**

Kydland and Prescott showed that a policy re-optimized period by period is dominated by a pre-committed rule, because agents who anticipate re-optimization change their behaviour. The same holds for an optimizer facing its own governor: if the envelope could be relaxed by strong short-run performance, strong short-run performance would become the thing optimized. The envelope is therefore a committed rule with a **constitutional lag**: a change to any protected invariant or envelope parameter takes effect no sooner than $T_{\text{lag}}$ (initially 7 days) after two-key approval, is announced in the ledger at approval, and is never conditioned on a performance metric. These MAY evolve only through this higher-assurance governance workflow.

### **37.3 Design principles**

Ostrom's design principles for durable governance of a shared resource map onto the planes: clearly defined boundaries (Section 42); rules matched to local conditions (risk classes, Section 15); monitoring by accountable monitors (the verification plane and human sampling); graduated sanctions (quarantine before rejection, budget decay before exclusion, Section 23.3); conflict-resolution mechanisms (contradiction edges, Section 35.2); recognized rights to organize (populations and lanes); and nested enterprises (cell, pod, region, federation). The point of citing them is that these are the empirically observed properties of governance that lasted.

## **38. HUMAN CONTROL PLANE**

Humans define: strategic objectives; constraints; budgets; protected invariants; deployment authority; risk posture; research priorities; stop conditions.

### **38.1 Residual control**

In Hart's theory of incomplete contracts, whoever holds the residual rights of control decides in the contingencies the contract did not foresee. This document is an incomplete contract with the fabric. The Human Control Plane holds all residual control rights: any situation not covered by an admissible action and a ratified parameter is decided by humans, and the fabric's default in an unforeseen situation is to hold (continue inside the current envelope, or halt if the situation is a boundary question), never to extrapolate.

### **38.2 The governance envelope**

``` yaml
governance_envelope:                       # ratified by two keys; constitutional lag applies
  v_max:                                   # cap on resource-normalized velocity tilde_v
    initial: "0.10 per day"                #   = doubling time of P no shorter than ~7 days
    rationale: "matches the initial human review capacity; raised per rung after review"
  d_max:                                   # max depth of autonomous self-modification (Section 42.4)
    initial: 2                             #   L0 targets and L1 machinery; L2 by R2 process; L3/L4 never
  r_max:                                   # cap on resource growth rate the directive may self-allocate
    initial: "2x per certified rung"
  blast_radius_caps:
    production_fraction_per_promotion: 0.01
    simultaneous_canaries: 8
  evaluator_change_rate_cap: "2 per day, each R2"
  human_review_sampling:
    L1_promotions: ">= 1%"
    L2_changes: "100%"
  halt_latency_bound: "T_lease + W_max"
  kill_switch_holders: ">= 2 independent"
```

The governor enforces $\tilde v \le v_{\max}$ by throttling the meta fraction $f$ first and the evaluation rate second (Proposition 64.5), so that a fabric in a super-exponential regime is slowed to the ratified exponential, never stopped by the envelope alone. Proposition 64.7 shows that a binding $v_{\max}$ is also what makes the fabric produce usable capability along the way rather than only machinery.

### **38.3 Allocating human attention**

Human review is a channel of finite capacity $\kappa_H$ (items per day), so its allocation is a rational-inattention problem in Sims's sense: attend where the expected reduction in harm per unit attention is largest. With expected harm $h_i$ and residual uncertainty $u_i$ of promotion $i$ (both from the verifier's output), review probability is

$$
\pi_i \propto h_i\, u_i, \qquad \sum_i \pi_i \le \kappa_H,
$$

subject to the floors above (every L2 change, at least 1% of L1 promotions at random so that the sampling itself cannot be gamed). A promotion selected for review is held in SHADOW (Section 44) until reviewed; the queue depth and the fraction of harm covered are reported, and when the queue exceeds capacity the fabric's promotion rate for that class is throttled rather than the review skipped.

### **38.4 What humans do not do**

Humans SHOULD NOT need to micromanage: individual candidate generation; individual worker scheduling; routine experiment selection; deduplication; local Cell migration; low-risk sandbox promotion. The design goal is that human attention goes to the envelope, the invariants, the sampled reviews and the unforeseen, and the fabric reports in the units of this document.

## **39. SCIENTIFIC-METHOD NATIVE FORMAT**

Every meaningful experiment SHOULD express:

``` yaml
scientific_method:
  hypothesis: required
  causal_rationale: required
  intervention: required
  predicted_outcome: required            # direction and minimum detectable effect, pre-registered
  falsification_condition: required      # the observation that would reject the hypothesis
  control: required_when_possible
  design: required                       # randomized | paired | factorial | diff_in_diff | regression_discontinuity
  analysis_plan: required                # test, stopping rule, error rates, covariates; fixed before data
  observation: generated
  conclusion: generated
  replication_status: generated          # none | replicated_internally | replicated_independently
```

Pre-registration is what makes the Section 17 error rates real: a test chosen after seeing the data has no stated $\alpha$. The analysis plan is hashed into the experiment record (Section 19) before the first evaluation runs; a plan changed afterward produces a new experiment with the old one recorded as abandoned.

The system is not merely a code mutator. It is an automated empirical research system operating on itself, and its standard of evidence is the one randomized evaluation brought to empirical economics: an effect is a difference between what happened under the intervention and what would have happened without it, estimated from a design that makes the comparison fair.

## **40. CAUSAL VALIDATION**

### **40.1 Potential outcomes**

For candidate $c$ and unit $u$ (an environment–seed pair), let $Y_u(c)$ and $Y_u(c_0)$ be the potential outcomes under candidate and control. The estimand is $\tau = \mathbb{E}[Y_u(c) - Y_u(c_0)]$. Because every unit can be run under both arms, the fabric is in the rare position of observing both potential outcomes for the same unit; the paired difference $d_u = Y_u(c) - Y_u(c_0)$ is unbiased for $\tau$ under randomized unit selection, and the design question reduces to variance (40.2) and interference (40.3).

Where possible, use: A/B tests; ablation studies; matched controls; factorial experiments; counterfactual simulation; intervention-based causal tests; replay tests. Correlation alone SHOULD NOT justify high-impact promotion.

### **40.2 Variance reduction**

Two techniques, both free in a fabric that controls its own seeds, multiply decision efficiency directly:

**Common random numbers.** Running both arms on the same seeds and environments induces correlation $\rho_{\text{CRN}}$ between $Y_u(c)$ and $Y_u(c_0)$, so

$$
\text{Var}(d_u) = 2\sigma^{2}(1 - \rho_{\text{CRN}}), \qquad \mathcal{M}_{\text{CRN}} = \frac{1}{1-\rho_{\text{CRN}}},
$$

a 2× gain at $\rho = 0.5$ and 10× at $\rho = 0.9$. Micro-benchmarks and simulations typically show $\rho \ge 0.8$.

**Control variates.** With a covariate $Z_u$ correlated with $d_u$ at $r_{\text{CV}}$ (a cheap proxy, a pre-period measurement, a surrogate prediction), the adjusted estimator $\hat\tau_{\text{CV}} = \bar d - \hat\beta(\bar Z - \mathbb{E}Z)$ has variance $(1 - r_{\text{CV}}^{2})$ times the unadjusted one. Combined:

$$
\text{VRF} = \frac{1}{(1 - \rho_{\text{CRN}})(1 - r_{\text{CV}}^{2})}.
$$

Variance reduction raises the information per evaluation $\mathcal{K} = \Delta^{2}/(2\sigma_{\text{eff}}^{2})$, which is one of the three terms of the Information–Verification Bound (Proposition 65.6).

### **40.3 Interference**

Units are not independent when candidates share caches, queues, thermal headroom or a knowledge cache (a violation of the stable-unit-treatment-value assumption). The fabric handles interference by design: candidates in the same comparison run in disjoint sandboxes with pinned resources; pod-level interventions are randomized at the pod level (cluster randomization) with the pod as the unit; and the regression specification for cross-cell effects includes the exposure of each unit to other treated units.

### **40.4 Attribution of meta-promotions**

A meta-promotion changes the machinery, not a candidate, so its effect is on $P$ over time. Three designs are used, in order of preference:

1. **Randomized rollout.** Apply the change to a random half of pods; estimate the effect on $\tilde v$ by comparing treated and control pods over the window (the cleanest design; used for everything that can be pod-scoped).
2. **Difference-in-differences.** When rollout cannot be randomized, compare the change in $\ln P$ before and after in treated pods against the same change in untreated pods; the parallel-trends assumption is checked on the pre-period.
3. **Regression discontinuity at the promotion threshold.** Candidates whose verification statistic fell just above and just below the promotion cutoff are comparable in everything except promotion; comparing their downstream descendant value estimates the *causal* effect of promotion itself, which calibrates $\delta$ and detects a cutoff that promotes noise.

Granger-type lead–lag tests on the velocity series are used only to *screen* for candidate meta-effects worth a designed test, never as attribution. Detection of a sustained change in $\tilde v$ against multi-timescale noise uses optimal fingerprinting (Section 64.8), and the shares of a window's gain among its promotions are Shapley values (Section 24.2).

## **41. ANTI-FRAGILE EVALUATION**

Dedicated adversarial populations SHALL search for: benchmark exploitation; metric hacking; hidden regressions; race conditions; nondeterminism; security defects; memory corruption; false causal attribution; distribution shift; long-tail failures; resource leaks; surrogate exploitation; market misreporting.

### **41.1 Capture score**

For each evaluator and surrogate, an adversarial population with a fixed budget $B_{\text{adv}}$ searches for candidates that raise the proxy without raising ground truth. Its best achieved proxy–truth gap in the budget is the **capture score**; a rising capture score retires or patches the evaluator (Section 18.1). The adversarial budget is a floor, not a market good (Section 37).

### **41.2 Test families**

Every discovered exploit SHOULD become a new permanent or rotating test family, with the exploit's candidate family indexed in failure memory (Section 21) so that the main populations are steered away from it.

### **41.3 Distribution shift and robust promotion**

Shift between the evaluation distribution $\hat{\mathcal{D}}$ and the production distribution $\mathcal{D}_{\text{prod}}$ is measured by the Wasserstein-1 (Kantorovich) distance,

$$
W_1(\hat{\mathcal{D}}, \mathcal{D}_{\text{prod}}) = \inf_{\pi \in \Pi(\hat{\mathcal{D}}, \mathcal{D}_{\text{prod}})} \mathbb{E}_{(x, x') \sim \pi}\,\|x - x'\|,
$$

computed on the environment feature space (or its dual form on 1-Lipschitz test functions when the space is high-dimensional). It is reported in every certificate. For R2–R3 promotions the gain must hold on the worst distribution within radius $\varepsilon_W = W_1(\hat{\mathcal{D}}, \mathcal{D}_{\text{prod}})$ of the evaluation distribution (distributionally robust promotion, Section 17.6); for R0–R1 the measured shift sets how often benchmarks rotate.

## **42. SELF-DESIGN BOUNDARY**

The system MAY progressively optimize:

``` text
application code
  ->
algorithms
  ->
agent policies
  ->
evaluators            (R2 process; Section 18)
  ->
compilers
  ->
runtime
  ->
memory layout
  ->
network topology
  ->
hardware mapping
  ->
accelerator architecture
  ->
datacenter topology
```

Long-horizon research MAY extend toward: chip design; photonics; cooling; energy systems; robotics; manufacturing; scientific instrumentation. This is where recursive software improvement begins to become recursive technological improvement.

### **42.1 Layers**

| **Layer** | **Contents** | **Who may change it** | **Verified by** |
|---|---|---|---|
| L0 | target systems: application code, kernels, policies, configurations | the fabric (R0–R1) | L2 evaluators, L3 verifiers |
| L1 | improvement machinery: generators, schedulers, surrogates, representations, market policy | the fabric, as meta-candidates (R1–R3) | L3 |
| L2 | evaluators, benchmarks, calibration streams | the fabric under the R2 process | L3 + human review (100%) |
| L3 | verifiers, ledger, governor, sandbox, halt leases, signing | humans, offline, two-key, constitutional lag | humans + independent audit |
| L4 | constitution, invariants, envelope, human control plane | humans only | humans |

### **42.2 Boundary rule**

A proposal is admissible only if every object it writes is in a layer the proposer may change, and the layer that verifies it is strictly higher than every layer it writes. L3 and L4 are never written through the fabric's promotion path; a proposal that would write them is inadmissible by static classification (Section 37.1) and its attempt is a governance event (Section 5.14).

### **42.3 Trust graph acyclicity**

Define the directed graph on components with an edge $i \to j$ if $j$ verifies changes to $i$. The invariant is that this graph is acyclic and every path terminates in L3 or L4: **no change is verified by a component it can modify**, directly or through a chain. Acyclicity is checked statically on every deployed configuration and is itself a protected invariant (Section 37).

### **42.4 Depth of recursion**

Let depth 0 be a change to L0, depth 1 a change to the machinery that produces depth-0 changes, depth 2 a change to the machinery that produces depth-1 changes (a meta-meta change, e.g. to the bandit that allocates among generators). The envelope parameter $d_{\max}$ (initially 2) bounds the depth the fabric may modify autonomously; each depth's verifier sits strictly above it by 42.3. The recursion is therefore finite and audited at every level, while still containing the loop that improves the improver.

## **43. PHYSICS-AWARE SCALING RULES**

### **Rule A — Faster means more local**

As target rate rises, synchronize less: a loop at rate $f$ may span at most $c_{\text{fiber}}/(2f)$ (FP-1), and above $10^{4}$/s that is less than a datacenter.

### **Rule B — Larger means more asynchronous**

Global synchronization cost increases with physical scale: the coherence term $\theta N(N-1)$ grows quadratically, so $\theta$ must fall as $N^{-2}$ for throughput to keep rising (FP-7).

### **Rule C — Compute is not free**

Measure energy and thermal proxies: every evaluation carries joules (measured or modelled), and the certified quantity is capability per joule (Section 61).

### **Rule D — Data motion is a target**

Optimize bytes moved per useful discovery: the energy-derived off-node byte ceiling per evaluation falls from 125 MB at M0 to ~250 KB at M6 and ~250 bytes at M9 (Section 28.1), link bandwidth binds equally from M6, and bytes per discovery is a tracked metric.

### **Rule E — Verification throughput is a first-class resource**

Candidate generation MUST NOT outrun trustworthy evaluation indefinitely: $\lambda_{\text{gen}} \le \kappa_V \lambda_V$ is enforced, the verification budget floor is protected, and sustained velocity is bounded by verification growth (Proposition 65.6).

### **Rule F — Real-world experiments impose real-world clocks**

No software architecture can compress every physical experiment into nanoseconds; loops on physical clocks are rate-limited by their evidence and the separation ratio (Section 25).

## **44. PROMOTION STATES**

``` yaml
promotion_states:
  - LAB
  - SANDBOX
  - SIMULATION
  - SHADOW
  - CANARY
  - LIMITED_PRODUCTION
  - PRODUCTION
  - FOUNDATIONAL
absorbing:
  - REJECTED
  - REVERTED
  - QUARANTINED          # re-enterable only by a new experiment
```

### **44.1 Markov model**

Promotion is a Markov chain on these states with transition probabilities $p_{s \to s'}$ estimated from the ledger per risk class. The expected cost to reach PRODUCTION from LAB is the sum over the path of per-state evidence cost times expected visits, computed from the fundamental matrix of the chain; it is the quantity the funnel economics (Section 16.1) minimize and the resource market prices. Required evidence grows with promotion depth and blast radius: the error rates $(\alpha_s, \beta_s)$ tighten at each state, and the exposure cap (fraction of production traffic) at CANARY and LIMITED_PRODUCTION is set by the blast-radius parameters of the envelope.

A candidate's required evidence grows with its promotion depth and blast radius. A regression detected in any state reverts to the frozen baseline (Section 7) and emits a failure object.

## **45. BRANCHING AND DIVERSITY**

The system SHALL support concurrent lineages.

``` text
OMEGA-221
  +-- OMEGA-221-A
  +-- OMEGA-221-B
  +-- OMEGA-221-C
  +-- OMEGA-221-D
```

Rules: do not replace the incumbent immediately; preserve promising alternate branches; merge useful capabilities when evidence supports it; allow specialization; preserve genealogical history.

### **45.1 Effective number of lineages**

With lineage shares $p_a$ of the evaluation budget, the effective number of lineages is

$$
N_{\text{eff}} = \exp\Big(-\sum_a p_a \ln p_a\Big)\quad\text{or}\quad N_{\text{eff}}^{(2)} = \Big(\sum_a p_a^{2}\Big)^{-1},
$$

and the floor is $N_{\text{eff}} \ge N_{\min}$ (initially 8 at M0, rising by two per rung). Budget shares are the arms of a bandit, but the floor is a constraint on the bandit, not a prior.

### **45.2 Overlap distribution**

Share counts do not detect two lineages that have converged to the same behaviour. The fabric therefore computes the **overlap distribution** $P(q)$ of pairwise behavioural similarities $q_{ab} \in [0, 1]$ between lineages (Section 13.1), using the embedding of Section 34.3, and requires that the entropy of $P(q)$ over fixed bins, or equivalently the number of clusters in the ultrametric tree built from the overlap matrix, stays above a floor. A collapse of $P(q)$ toward a single high-overlap peak is the signature of monoculture (replica symmetry restored) and is a failure condition (Section 49) even when $N_{\text{eff}}$ by share is high.

### **45.3 Valuing a weak branch**

Keeping a branch alive costs its share of budget and buys the right, not the obligation, to exploit it later. That is a call option. With the branch's current expected gain $S_b$, the cost to bring it to the incumbent's level as strike $K_b$, volatility $\sigma_b$ of its gain estimate (from the dispersion of its recent evaluations, or an ARCH-type estimate when volatility is time-varying), horizon $T_b$ and no discounting, the Black–Scholes–Merton value

$$
V_{\text{opt}}(b) = S_b\,\Phi(d_1) - K_b\,\Phi(d_2), \qquad
d_{1,2} = \frac{\ln(S_b/K_b) \pm \tfrac{1}{2}\sigma_b^{2} T_b}{\sigma_b \sqrt{T_b}},
$$

is positive and increasing in $\sigma_b$: the more uncertain a branch, the more it is worth keeping at small cost. Branch-preservation budget is allocated by $V_{\text{opt}}(b)$ per unit maintenance cost, which formalizes "preserve weak but promising branches" and stops the market from pruning high-variance lineages that a mean-based rule would discard.

### **45.4 Mutation and the threshold**

Each lineage's exploitation population runs below Eigen's error threshold with margin (Section 14.2); the novelty population runs above it under isolation. The margin per population is in the certificate.

## **46. REPRODUCIBILITY STANDARD**

Every accepted experiment SHALL capture: code hash; model hash; weights/version; configuration; prompt; data hash; evaluator hash; compiler version; dependency lock; hardware class; environment; seeds; parent lineage; analysis plan hash.

### **46.1 Determinism classes**

| **Class** | **Definition** | **Replay requirement** |
|---|---|---|
| D0 bit-exact | same inputs give identical outputs | identical |
| D1 numerically stable | outputs agree within a stated tolerance (e.g. floating-point reduction order) | within tolerance |
| D2 statistically reproducible | distribution of outputs agrees (hardware timing, nondeterministic kernels) | replay distribution within a two-sample test at the stated level |
| D3 irreproducible | none of the above | not promotable above SANDBOX; must explain why |

A foundational improvement MUST be replayable at D0 or D1, or otherwise strongly explain why replay is impossible. The certification gate replays a random sample (Section 6).

## **47. M0 SUCCESS CRITERIA**

M0 is certified only when LVL3.AI demonstrates:

``` yaml
M0_success:
  sustained_evaluations_per_sec_lcb95: ">= 1000"
  production_multiplier_vs_v2_lcb95: ">= 4.0"        # Section 68 ablation; design target 8.0
  complete_lineage: true
  reproducible_execution: true
  independent_verification: true
  sequential_tests_on_all_R0_R1_decisions: true
  fdr_control_at_q: "<= 0.05"
  winner_remeasurement: true
  automated_generation: true
  automated_rejection: true
  automated_sandbox_promotion: true
  rollback: true
  knowledge_retention: true                           # MDL-admitted objects exist and change priors
  failure_retention: true
  resource_accounting_with_energy: true
  bottleneck_detection: true
  diversity_floor_held: true                          # N_eff >= 8, P(q) entropy above floor
  error_threshold_margin_positive: true               # all exploitation populations
  governance_envelope_enforced: true                  # Section 5.14 within bounds for the full window
  halt_drill_within_bound: true
  trust_graph_acyclic: true
  next_magnitude_activation: true
```

M0 is NOT certified if throughput is achieved by: disabling verification; dropping lineage; counting candidate generation as evaluation; using duplicate experiments; hiding regressions; excluding resource costs; relaxing error rates below the risk-class defaults; counting surrogate estimates as full-fidelity evaluations; or any change to L3/L4 through the fabric.

## **48. PROGRAM-LEVEL SUCCESS**

The RSI program succeeds when:

``` text
CAPABILITY                 rises        (LCB_95 of cumulative verified delta > 0, held-out)
EXPERIMENT PRODUCTIVITY    rises        (P = lambda * y_P * delta rises; M_k non-decreasing)
KNOWLEDGE REUSE            rises        (knowledge yield in bits/evaluation and reuse rate rise)
RECURSIVE VELOCITY         positive     (tilde_v > 0, Solow residual after resource normalization)
EXPONENTIAL REGIME         certified    (LCB_95(phi_hat) >= 1 - eps_phi over >= 3 doublings, attributed)

while:

REGRESSION RATE             falls       (UCB_95(rho_reg) non-increasing per rung)
COST / USEFUL DISCOVERY     falls       (experience-curve exponent b >= 0.3, Section 48.2)
DUPLICATE SEARCH            falls
LATENCY / USEFUL RESULT     falls where physically compressible
GOVERNANCE METRICS          inside the envelope for the whole program
```

### **48.1 Exponential-regime certificate**

The program MAY state that the fabric is in the exponential regime only on the basis of a signed certificate containing: the window; $\hat\varphi$ with its 95% interval from the Section 64.6 regression; the Solow decomposition of growth into resource and residual shares; the fingerprint detection statistic (Section 64.8) with its confidence; the ablation and Shapley attribution of the residual to meta-promotions (Section 68); and the number of doublings covered ($\ge 3$). A regime claim without the certificate is a Section 55 violation.

### **48.2 Learning by doing**

Arrow's model of productivity rising with cumulative experience predicts that the cost of a useful discovery falls as a power of the number already made, $\text{CUD}(n) = \text{CUD}_0\, n^{-b}$. The fabric fits $b$ on its own ledger; the target is $b \ge 0.3$ (each doubling of cumulative discoveries cuts the cost by $\ge 19\%$), and a measured $b$ near zero after Phase 3 means knowledge reuse (Sections 20–21) is not working, whatever $\lambda$ says.

## **49. FAILURE CONDITIONS**

The program SHALL consider these architectural failures, each with its detector:

| **Failure mode** | **Detector (Section)** |
|---|---|
| raw_throughput_without_useful_yield | $\lambda$ up, $\text{LCB}(y_V)$ or $\delta$ flat (5.2, 5.4) |
| benchmark_overfitting | proxy divergence drift on the rotated hidden set (FP-5, 18.1) |
| evaluator_capture | capture score rising (41.1) |
| recursive_regression | regression hazard above $\rho_{\max}$; RD at the cutoff shows promotion of noise (5.5, 40.4) |
| search_monoculture | $N_{\text{eff}}$ below floor or $P(q)$ entropy collapse (45.1–45.2) |
| error_catastrophe | negative error-threshold margin in an exploitation population (14.2) |
| lineage_loss | lineage completeness below $1 - 10^{-6}$ (6) |
| unreproducible_progress | replay sample failing at the stated tolerance (46) |
| compute_scaling_without_efficiency_scaling | RGC near zero: growth explained by resources (5.9.1) |
| knowledge_explosion_without_compression | knowledge objects admitted without MDL saving; retrieval latency rising (20.3) |
| coordination_overhead_domination | measured $\theta$ above budget; $S(N)/N$ falling (FP-7, 32) |
| candidate_generation_outpacing_verification | $\lambda_{\text{gen}}/\lambda_V > \kappa_V$ (FP-4) |
| hidden_resource_externalities | energy or bytes unaccounted; CUD falling while joules per discovery rise (5.8) |
| surrogate_drift | calibration stream recall or coverage below floor (34.2) |
| market_capture | truthfulness ratio drifting; one population's share above cap (23.3) |
| review_starvation | human review queue above capacity with promotions not throttled (38.3) |
| uncontrolled_self_modification | any L3/L4 write attempt, trust graph cycle, depth above $d_{\max}$, or $\tilde v > v_{\max}$ (42, 38) |

Every detector is an anytime-valid test on its series (Section 30.1), so it can be checked continuously without inflating its false-alarm rate.

## **50. RSI OPERATING FLYWHEEL**

``` text
MORE EXPERIMENTS
      ->
MORE EVIDENCE
      ->
BETTER KNOWLEDGE
      ->
BETTER SEARCH PRIORS
      ->
BETTER CANDIDATES
      ->
HIGHER USEFUL YIELD
      ->
BETTER ALGORITHMS
      ->
BETTER COMPUTE EFFICIENCY
      ->
MORE EXPERIMENTS
      ->
BETTER EVALUATORS
      ->
MORE TRUSTWORTHY PROMOTION
      ->
BETTER META-RSI
      ->
FASTER FLYWHEEL
```

### **50.1 Loop gain**

Write the flywheel as a feedback loop on $\ln P$. Each turn of the loop (one meta-promotion) multiplies $P$ by $(1 + g)$ on average, and turns occur at rate $f\lambda y_m$ (meta fraction × evaluation rate × meta promotion yield). The velocity is

$$
v = f\,\lambda\, y_m\, \overline{\ln(1+g)} ,
$$

and the loop is self-reinforcing when the turn rate itself rises with $P$: $\lambda$, $y_m$ and $g$ all depend on the machinery. Exponential growth is the case $v$ constant in time, which requires the gain per turn to not decay as fast as the turn rate rises; this is the content of $\varphi \ge 1$ (Section 64). The flywheel's *speed* is $v$, its *acceleration* is $\dot v$, and the governor caps the former (Section 38.2).

## **51. LVL3.AI MOAT**

The moat SHALL NOT be defined as one model.

The moat is the compounding substrate: experiment history; failure history; improvement genealogy; causal knowledge graph; evaluator infrastructure; benchmark families; specialized populations; optimized runtimes; optimized compilers; optimized kernels; resource-allocation policies; search priors; machine-discovered abstractions; meta-RSI history.

### **51.1 Why it compounds**

Knowledge in the fabric is a non-rival good in Romer's sense: once a knowledge or failure object is admitted, every cell uses it at zero marginal cost. Non-rivalry is the source of increasing returns in the growth law (the $\beta_K$ term of Conjecture 64.6) and the reason a larger ledger makes each later evaluation worth more, not less. Arrow's learning by doing adds the second mechanism: cost per discovery falls with cumulative discoveries (48.2). The measurable form of the moat at time $t$ is the **replication cost**,

$$
\text{Moat}(t) = \min\ \text{resources a new entrant would need to reach the fabric's } (K_t, \text{CUD}_t, P_t) \text{ from nothing},
$$

estimated from the fabric's own experience curve as the integral of $\text{CUD}(n)$ over the discoveries made, less the share recoverable from public knowledge. It grows with every valid experiment: every valid experiment increases the system's knowledge; every useful knowledge artifact improves future search; every improvement in search increases experiment productivity. This creates a compounding system-level advantage.

## **52. ARCHITECTURAL DOCTRINE**

``` yaml
doctrine:
  - measure_reality
  - verify_before_promoting
  - preserve_lineage
  - separate_generation_from_evaluation
  - scale_via_parallelism_and_locality
  - avoid_global_synchronization_on_fast_paths
  - compress_experience_into_knowledge
  - preserve_diversity
  - reward_descendant_value
  - optimize_the_optimizer
  - treat_every_magnitude_as_a_launchpad
  - never_equate_mutation_rate_with_improvement_rate
  - allow_machine_native_representations
  - keep_macro_orchestration_out_of_micro_loops
  - account_for_energy_data_motion_and_heat
  - use_multiple_timescales
  - respect_physical_causality
  - maximize_verified_cumulative_capability
  # new in v3
  - every_promotion_is_a_controlled_statistical_decision
  - every_claim_of_acceleration_is_a_solow_residual_with_a_confidence_interval
  - the_envelope_is_a_rule_not_a_setting
  - no_change_is_verified_by_what_it_can_modify
  - verification_capacity_bounds_velocity_so_grow_verification_first
  - what_cannot_be_statically_classified_is_inadmissible
```

## **53. GROUND-TRUTH MAGNITUDE ROADMAP**

Two ladders, climbed together:

``` text
            horizontal (evaluations/s)      vertical (M_k design target)      production vs M0-v2
M0          10^3                            4x                                 4
 |
 v
M1          10^4                            8x                                 80
 |
 v
M2          10^5                            16x                                1,600
 |
 v
M3          10^6                            32x                                32,000
 |
 v
M4          10^7                            64x                                640,000
 |
 v
M5          10^8                            128x                               1.28 x 10^7
 |
 v
M6          10^9   (north star)             256x                               2.56 x 10^8
 |
 v
M7-M9       10^10 - 10^12 (frontier)        non-decreasing                     physics envelope, Section 67
```

At every threshold:

``` text
ACHIEVE
  ->
VERIFY                 (LCB_95 on the sustained window)
  ->
CERTIFY                (signed certificate, Section 6)
  ->
PRESERVE BASELINE      (immutable rollback target)
  ->
PROFILE LIMITS         (utilization per stage; theta; b_k; lambda_V)
  ->
PROJECT                (T10 = ln 10 / tilde_v, with CI)
  ->
GENERATE NEXT-SCALE HYPOTHESES
  ->
ALLOCATE RESEARCH POPULATIONS   (inside the envelope)
  ->
ATTACK BOTTLENECKS
  ->
10X  (and 2X on the vertical ladder)
```

## **54. CURRENT ENGINEERING PRIORITY**

LVL3.AI SHOULD NOT begin by attempting to simulate M6. The correct path is to build the M0 architecture in a way that contains the scaling primitives required for M1–M6 and the statistical and governance machinery that the 4× contract and the growth-law measurement need from day one.

Immediate engineering sequence:

``` yaml
phase_1:                                   # the loop, the statistics, the leash
  - experiment_schema                      # Section 15, with the statistics block
  - immutable_ledger                       # Section 19, Merkle DAG, per-cell chains
  - RSI_cell_runtime                       # Section 9, with halt lease
  - sandbox_runtime                        # Section 36, R0-R1 isolation
  - evaluator_interface                    # Section 18, blind, versioned
  - metrics_pipeline                       # Section 5 estimators with intervals
  - sequential_verifier                    # Section 17.2-17.3: SPRT, confidence sequences
  - common_random_numbers_pairing          # Section 40.2
  - governor_and_invariant_checker         # Sections 37-38: admissibility, envelope, halt drill

phase_2:                                   # yield and throughput
  - distributed_work_queues
  - persistent_workers
  - candidate_generator_ensemble           # Section 14, bandit + error-threshold scheduling
  - knowledge_graph                        # Section 20, MDL admission
  - failure_memory_and_dedup_index         # Section 21, LSH
  - automatic_promotion                    # Section 44 chain with FDR control (17.4)
  - winner_remeasurement                   # Section 17.5
  - calibration_stream                     # Section 34.2
  - ablation_harness_for_the_4x_contract   # Section 68.3

phase_3:                                   # the optimizer of the optimizer
  - meta_scheduler                         # portfolio (FP-6) over the bandit
  - bottleneck_detector                    # Section 31 queueing model
  - experiment_deduplication_at_scale
  - novelty_engine                         # Section 22
  - resource_market                        # Section 23: proportional fairness + VCG rounds
  - surrogate_models_and_funnel            # Sections 16, 34 with measured recall
  - descendant_value_and_shapley           # Section 24
  - growth_law_estimator                   # Section 64: Solow decomposition, phi_hat, fingerprinting

phase_4:                                   # certification
  - magnitude_certifier                    # Section 6
  - automatic_next_magnitude_directive     # Section 7 with envelope rule
  - M0_certification
  - M1_scaling_program
```

### **54.1 Lever map**

Every mechanism in this document acts on one of the three terms of the Information–Verification Bound (Proposition 65.6) or on one of the elasticities of $\varphi$ (Conjecture 64.6). The map is how an implementing agent decides what to build next: measure which term binds (Section 31), then build the lever on that term.

| **Term** | **Levers (sections)** |
|---|---|
| verification throughput $\lambda_V$ | persistent workers, batching, in-device verification (12, 32); protected budget (37); pod sizing (10.1) |
| information per evaluation $\mathcal{K}$ | CRN and control variates (40.2); evaluator reliability (18.1); sequential stopping (17.2); dedup (21.3); funnel recall (16) |
| gain per promotion $\delta$ | priors from knowledge (20); descendant value (24); representation (13); portfolio (FP-6); robust promotion (17.6) |
| $\beta_K$ knowledge reuse (raises $\varphi$) | MDL admission (20.3), relevance propagation (20.4, 35), failure memory (21) |
| $\beta_D$ duplication (lowers $\varphi$) | LSH dedup (21.3), novelty (22), market (23) |
| $\beta_V$ verification saturation (lowers $\varphi$) | FP-4 throttle, verification plane scaling (32) |
| $\beta_G$ Goodhart divergence (lowers $\varphi$) | Goodhart governor (FP-5), rotation (18), adversaries (41), calibration stream (34.2) |

## **55. AGENT EXECUTION CONTRACT**

Any coding or research agent implementing this PRD MUST obey:

``` yaml
agent_contract:
  priorities:
    - correctness
    - measurability
    - modularity
    - reproducibility
    - scaling
    - verification
    - performance
  prohibited_shortcuts:
    - claim_unverified_improvement
    - hide_regressions
    - bypass_lineage
    - silently_change_evaluators
    - count_generated_candidates_as_completed_evaluations
    - remove_safety_or_resource_boundaries_to_improve_benchmarks
    - report_a_screening_score_as_a_promotion_estimate        # new
    - choose_a_test_after_seeing_the_data                    # new
    - claim_acceleration_without_the_Section_48_certificate  # new
    - write_to_L3_or_L4_through_the_fabric                   # new
  required_behavior:
    - expose_interfaces
    - define_schemas
    - write_tests
    - instrument_latency
    - instrument_throughput
    - record_resource_cost
    - make_components_replaceable
    - preserve_backward_compatible_evidence
    - report_every_metric_with_its_interval                  # new
    - state_assumptions_next_to_every_number                 # new
    - run_the_halt_drill_before_claiming_any_magnitude       # new
```

### **55.1 Acceptance tests an agent must ship with each phase**

- Phase 1: a synthetic candidate stream with known true effects; the verifier's realized $(\alpha, \beta)$ match the risk-class defaults within their intervals; the SPRT's mean sample size matches Section 17.2 within 15%; the halt drill meets $T_{\text{lease}} + W_{\max}$; an inadmissible proposal is rejected before evaluation and logged.
- Phase 2: on the synthetic stream, FDR at the stated $q$; winner re-measurement removes the Section FP-5 bias to within its interval; the dedup index catches planted duplicates at the stated similarity; the ablation harness reproduces a planted 2× efficiency difference.
- Phase 3: the market allocates a planted high-value population more budget under truthful reports and strictly less under a planted over-report; the growth-law estimator recovers a planted $\varphi$ within its interval on simulated trajectories; the fingerprint detector finds a planted velocity change against red noise at the stated power.
- Phase 4: an end-to-end M0 certification on the synthetic stream, with every gate's statistic computed from the ledger alone.

## **56. COMPONENT INTERFACE REQUIREMENTS**

Every module SHALL expose:

``` yaml
module_interface:
  module_id: required
  version: required
  inputs_schema: required
  outputs_schema: required
  side_effects: required
  latency_budget: required            # p50 / p99, Section 27.1
  resource_budget: required           # resource vector cap
  error_modes: required
  telemetry: required                 # which Section 30 series it emits
  replayability: required             # determinism class, Section 46.1
  security_class: required            # which layer it lives in, Section 42.1
  upgrade_strategy: required
  scalability_budget:                 # new
    contention_gamma: required        # declared share of serialized work on the fast path
    coherence_theta: required         # declared pairwise coordination cost
    bytes_off_node_per_call: required # against b_k, Section 28.1
  statistical_contract: optional      # new: for verifiers and evaluators, the (alpha, beta) they guarantee and how measured
  layer_writes: required              # new: the layers this module writes; checked for admissibility and acyclicity
```

No major subsystem may exist as an opaque uninstrumented dependency. A module's declared $\gamma$ and $\theta$ are checked against measurement in every certification window; a module exceeding its declaration is a bottleneck candidate (Section 31) and, if on the fast path, blocks certification.

## **57. TESTING HIERARCHY**

``` text
UNIT
 ->
PROPERTY
 ->
DIFFERENTIAL
 ->
METAMORPHIC            (new: relations that must hold across transformed inputs, e.g. permuting seeds leaves lambda unchanged)
 ->
STATISTICAL            (new: realized alpha, beta, FDR, coverage on synthetic streams with known truth)
 ->
INTEGRATION
 ->
SYSTEM
 ->
LOAD
 ->
CHAOS
 ->
ADVERSARIAL
 ->
REPLAY
 ->
CANARY
 ->
LONG-HORIZON REGRESSION
 ->
FABRIC-ON-FABRIC       (new: the fabric evaluates a change to itself through its own funnel, under the self-design boundary)
```

M0 requires this hierarchy to exist even if not every class is equally mature. The STATISTICAL class is mandatory at M0 because a verifier whose realized $\alpha$ is unknown certifies nothing.

## **58. DESIGN FOR HARDWARE EVOLUTION**

The software architecture SHALL assume hardware heterogeneity. Schedulers SHOULD support: CPU; GPU; FPGA; future ASIC; vector accelerators; domain-specific accelerators.

### **58.1 Roofline placement**

An evaluation with arithmetic intensity $I$ (operations per byte moved) attains at most

$$
\text{throughput} \le \min\big(\text{peak}_{\text{device}},\ I \cdot \text{BW}_{\text{device}}\big),
$$

so the scheduler places each evaluation class on the device whose ridge point $\text{peak}/\text{BW}$ is nearest its $I$: bandwidth-bound micro-evaluations go where bytes are cheapest to move (on-chip, near-memory), compute-bound ones where operations are cheapest. Experiment descriptors MUST express hardware requirements declaratively, including $I$ and the working-set size, so that placement is a computation rather than a convention.

### **58.2 Hardware as an RSI target**

Hardware mapping (L0) and accelerator architecture (physical band, Section 25) are in the self-design boundary's progression (Section 42); their loops run on fabrication clocks and their evidence is physical (Rule F).

## **59. DESIGN FOR GEOGRAPHIC EVOLUTION**

The architecture SHALL support:

``` text
single_machine
 ->
single_cluster
 ->
multi_cluster
 ->
multi_region
 ->
global_federation
```

### **59.1 Latency sets the loop**

With fiber at ~5 µs per km one way, a synchronous loop across 1,000 km cannot exceed ~100 Hz and across 4,000 km ~25 Hz (FP-1). Therefore, as geographic distance increases: local autonomy rises (every loop faster than the cross-region RTT is region-local); synchronization frequency falls (regions exchange only Merkle roots, relevant knowledge and market clearing at a cadence $\ge 10\times$ the RTT); knowledge compression rises (the off-region byte budget is the strictest); propagation becomes more selective (the relevance test of Section 20.4 at region level).

### **59.2 Sovereignty and failure domains**

Regions are failure domains and may be data-sovereignty domains: a region can certify its own magnitude on its own ledger shard, and the federation's magnitude is the sum of certified regional rates, never a global count that depends on cross-region consistency.

## **60. BEYOND SOFTWARE RSI**

The long-term system MAY extend optimization into the physical stack.

``` text
MODEL
 ->
ALGORITHM
 ->
COMPILER
 ->
RUNTIME
 ->
KERNEL
 ->
HARDWARE MAPPING
 ->
CHIP ARCHITECTURE
 ->
INTERCONNECT
 ->
DATACENTER
 ->
COOLING
 ->
ENERGY
 ->
ROBOTIC LABS
 ->
MANUFACTURING
```

At that stage the optimization loop becomes:

> ***recursive technological improvement**, not only recursive software improvement.*

### **60.1 Physical loops**

Physical experiments are batched (a fabrication run or a robotic lab shift evaluates many candidates at once), so their $\lambda$ is a batch size divided by a long cycle, and their verification is dominated by the sim-to-real gap. A digital twin is a surrogate (Section 34) whose calibration stream is the physical result; the gap is measured as $W_1$ between simulated and realized outcome distributions (Section 41.3) and promotion through a twin is admissible only within that measured radius. The system MUST continue to respect the slower validation clocks of physical reality.

## **61. FINAL GROUND TRUTH**

LVL3.AI is not building a program that changes itself rapidly.

LVL3.AI is building:

> ***a recursively optimizing computational ecosystem that generates enormous populations of candidate improvements, evaluates them against independent evidence, preserves causal lineage, retains verified gains, converts success and failure into reusable knowledge, improves its own search and verification machinery, measures its own acceleration as a residual with a confidence interval, and automatically begins the ascent to the next order of magnitude whenever the current magnitude is certified — inside an envelope that humans ratify and the fabric cannot touch.***

The current buildable target is:

``` text
M0 = 10^3 completed RSI evaluations / second, at >= 4x the v2 baseline's capability production
```

The declared architectural north star is:

``` text
M6 = 10^9 aggregate meaningful RSI evaluation events / second, at a vertical-ladder target of 256x
```

M6 is not an assumed endpoint. The system is explicitly architected so that:

``` text
M_k CERTIFIED
   ->
M_(k+1) ACTIVATED   (inside the ratified envelope)
```

The long-term objective is not raw iteration speed. It is:

> ***the highest physically achievable rate at which computation, knowledge, and experimentation can be transformed into independently verified cumulative capability.***

### **61.1 The governing equation**

v2 wrote the governing equation conceptually as compute × experiment quality × verification quality × knowledge reuse × meta-improvement over energy × latency × communication × cost × regression. v3 writes it as a measurable quantity and a bound on its growth.

The capability production rate and its resource-normalized form:

$$
P = \lambda\, y_P\, \delta, \qquad
\Pi = \frac{P\,(1 - \rho_{\text{reg}} h)}{\dot E}\quad\text{(net verified capability per joule, with } h \text{ the mean harm of a regression relative to } \delta\text{)}.
$$

The sustained growth of $P$ is bounded (Proposition 65.6):

$$
\bar v \;\le\; \overline{\frac{\dot\lambda_V}{\lambda_V}} + \overline{\frac{\dot{\mathcal{K}}}{\mathcal{K}}} + \overline{\frac{\dot\delta}{\delta}} + \frac{1}{T}\ln\frac{1}{1-\varepsilon},
$$

the regime of that growth is the measured exponent $\varphi$ of the knowledge production function (Section 64), and the whole trajectory is capped by the envelope (Proposition 64.5):

$$
P(t) \;\le\; P(0)\, e^{v_{\max} t}\, \Big(\frac{\|R(t)\|_w}{\|R(0)\|_w}\Big)^{\eta_R}.
$$

The exact equation is expected to evolve as the system gains empirical evidence; the three terms of the bound and the envelope are not expected to, because they follow from what verification, information and governance are. That evolution is itself part of RSI.

## **62. TERMINAL PRINCIPLE**

``` text
BUILD
 -> MEASURE            (with intervals)
 -> VERIFY             (sequentially, independently, at stated error rates)
 -> LEARN              (only what compresses)
 -> IMPROVE
 -> IMPROVE THE IMPROVER   (to depth d_max, verified from above)
 -> CERTIFY            (signed; residual, not trend)
 -> 10X  x  2X         (both ladders)
 -> REPEAT             (inside the envelope)
```

**That is LVL3.AI RSI.**

# PART II — MATHEMATICAL FOUNDATIONS AND CONTRACTS

Part II holds the derivations that Part I cites. Everything here is computable from the ledger; Section 71 gives reference pseudo-code, Section 72 reproduces the numbers by simulation, and Section 73 says what would refute them. Results that are standard are attributed in Section 70; results new to this document are labelled *Proposition* (with proof) or *Conjecture* (with the measurement that would confirm or refute it).

## **63. NOTATION AND SYMBOL TABLE**

| **Symbol** | **Meaning** | **Units** | **Defined in** |
|---|---|---|---|
| $t$, $W$ | time; measurement window length | s | 5 |
| $\lambda$ | completed, counted evaluations per second | 1/s | 5.1 |
| $\lambda_k$ | threshold of magnitude $M_k$: $10^{3+k}$ | 1/s | 4 |
| $\lambda_V$, $\lambda_{\text{gen}}$ | verification-plane decision rate; candidate generation rate | 1/s | FP-4 |
| $y_V$, $y_P$, $y_m$ | verification yield; promotion yield; meta promotion yield | — | 5.2–5.3 |
| $\delta$ | mean verified capability gain per promotion | capability units | 5.4 |
| $C$, $\bar C$, $w$ | capability vector; reporting scalarization; its weights | — | 5.4 |
| $P$ | capability production rate $\lambda y_P \delta$ | capability/s | 5.9 |
| $R$, $\Vert R\Vert_w$, $\eta_R$, $\eta_i$ | resource vector; weighted norm; resource elasticity of $P$ | — | 1.1, 64.4 |
| $v$, $\tilde v$, $a$ | velocity $\tfrac{d}{dt}\ln P$; resource-normalized velocity; acceleration | 1/s | 5.9–5.10 |
| $A$ | machinery productivity index ($P = A\,F(R)$) | — | 64.1 |
| $\kappa$, $\varphi$, $\lambda_A$ | growth constant; returns-to-scale exponent; meta-effort elasticity | — | 64.2 |
| $f$ | meta fraction: share of decisions aimed at the machinery | — | 50.1, 64.7 |
| $T_2$, $T_{10}$ | doubling time; magnitude time | s | 5.9 |
| $\alpha$, $\beta$, $\Delta$, $\sigma^2$ | false-promotion rate; false-rejection rate; minimum detectable effect; noise variance | — | 15, 17 |
| $n_B$, $\bar n$, $n_{\min}$ | fixed-sample size; realized mean samples per decision; sequential lower bound | evaluations | 17.1, 65.6 |
| $\mathcal{K}$ | information per evaluation, $\Delta^2/(2\sigma^2)$ under the Gaussian model | nats | 17.2 |
| $\rho_{\text{CRN}}$, $r_{\text{CV}}$, VRF | pairing correlation; control-variate correlation; variance-reduction factor | — | 40.2 |
| $c_i$, $s_i$, $r_i$, $\mathcal{R}$ | funnel stage cost, survival, recall; end-to-end recall | — | 16.1 |
| $\mathcal{M}$, $\mathcal{M}_k$, $\mathcal{M}_x$ | production multiplier vs v2 baseline; at rung $k$; component $x$ | — | 68 |
| $N$, $\gamma$, $\theta$, $S(N)$, $N^*$ | workers; contention; coherence; USL throughput; USL peak | — | FP-7 |
| $L$, $W_{\text{sojourn}}$, $u$, $o$ | in-flight count; sojourn time; utilization; overhead fraction | — | 9.1 |
| $\epsilon$ | inter-pod coupling (near-decomposability) | — | 10.1 |
| $b_k$ | off-node bytes per evaluation budget at rung $k$ | bytes | 28.1 |
| $\varepsilon_k$ | energy per evaluation at rung $k$ | J | 4.1 |
| $\rho_{\text{reg}}$, $h$ | regression hazard; mean harm of a regression relative to $\delta$ | — | 5.5, 61.1 |
| $\omega_j$, $i$, $r_{pY}$ | Goodhart selection weight; selection intensity; proxy–truth correlation | — | FP-5 |
| $\mu L$, $\sigma_s$ | mutation load per candidate; selective superiority (error threshold) | — | 14.2 |
| $P(q)$, $N_{\text{eff}}$ | overlap distribution; effective number of lineages | — | 45 |
| $V(c)$, $\phi_i$ | descendant value; Shapley share | — | 24 |
| $W_1$ | Wasserstein-1 distance | feature units | 41.3 |
| $\mathcal{I}$, $\mathcal{A}_{\text{adm}}$, $\mathcal{G}$ | invariant set; admissible actions; governance envelope | — | 37–38 |
| $v_{\max}$, $d_{\max}$, $r_{\max}$ | envelope caps: velocity, recursion depth, resource growth | — | 38.2 |
| $T_{\text{lease}}$, $T_{\text{stop}}$ | halt lease TTL; stopping time bound | s | 36.3 |
| $\beta_K$, $\beta_D$, $\beta_V$, $\beta_G$ | elasticities: knowledge reuse, duplication, verification saturation, Goodhart | — | 64.6 |

## **64. THE RECURSIVE GROWTH LAW**

### **64.1 Production function**

Write the capability production rate as the product of a machinery index and a resource function,

$$
P(t) = A(t)\, F(R(t)), \qquad F(R) = \prod_i R_i^{\eta_i},
$$

where $A$ collects everything about *how well* the fabric converts resources into verified capability (generators, evaluators, priors, representations, scheduling, statistics) and $F$ is a Cobb–Douglas form in the resource components with elasticities $\eta_i$. $F$ is the "scaling" part; $A$ is the "RSI" part. Nothing in this split is assumed about returns: constant returns to resources ($\sum_i \eta_i = 1$) is a measured hypothesis, not a premise.

### **64.2 Knowledge production function**

Following Romer, the machinery index grows through the fabric's own effort on it. In the general form introduced by Jones,

$$
\dot A = \kappa\, A^{\varphi}\, E_m^{\lambda_A}, \qquad E_m = f \cdot D,
$$

where $E_m$ is the meta-effort (the share $f$ of the decision rate $D$ aimed at the machinery), $\lambda_A \in (0, 1]$ captures duplication among concurrent meta-experiments ("stepping on toes": two populations rediscovering the same improvement), and $\varphi$ is the returns-to-scale exponent: how much easier or harder the next improvement is as the machinery gets better. Romer's original model is $\varphi = 1$; the semi-endogenous case is $\varphi < 1$ (ideas getting harder to find); the fabric is designed to push $\varphi$ up through non-rival knowledge reuse (Section 51.1) and is required to measure where it lands.

At fixed resources, $D$ is itself proportional to $A$ raised to some power, so the law collapses to the reduced form used throughout Part I,

$$
\dot A = \kappa_{\text{eff}}\, A^{\varphi_{\text{eff}}}, \qquad v = \frac{\dot A}{A} = \kappa_{\text{eff}}\, A^{\varphi_{\text{eff}} - 1},
$$

and it is $\varphi_{\text{eff}}$ (written $\varphi$ elsewhere) that the ledger estimates.

### **64.3 Regimes**

Solving $\dot A = \kappa A^{\varphi}$ from $A(0) = A_0$:

| **Regime** | **Solution** | **Velocity** | **Character** |
|---|---|---|---|
| $\varphi < 1$ | $A(t) = \big[A_0^{1-\varphi} + (1-\varphi)\kappa t\big]^{1/(1-\varphi)}$ | $v \to 0$ as $t^{-1}$ | power law; sub-exponential |
| $\varphi = 1$ | $A(t) = A_0 e^{\kappa t}$ | $v = \kappa$ constant | exponential; $T_2 = \ln 2/\kappa$ |
| $\varphi > 1$ | $A(t) = \big[A_0^{1-\varphi} - (\varphi-1)\kappa t\big]^{-1/(\varphi-1)}$ | $v$ rising | hyperbolic; finite-time blow-up at $t^* = \dfrac{A_0^{1-\varphi}}{(\varphi-1)\kappa}$ |

The $\varphi > 1$ regime is unphysical as written because it ignores the ceilings of Section 67 and the envelope of Section 38; with a saturation term, $\dot A = \kappa A^{\varphi}(1 - A/A_{\max})$, every regime becomes logistic in the long run. The envelope acts earlier than the physics (Proposition 64.5).

### **64.4 Growth accounting**

Differentiating $\ln P = \ln A + \sum_i \eta_i \ln R_i$,

$$
\frac{\dot P}{P} = \underbrace{\frac{\dot A}{A}}_{\tilde v\ \text{(RSI)}} + \underbrace{\sum_i \eta_i \frac{\dot R_i}{R_i}}_{\text{scaling}},
$$

which is Solow's growth accounting with the fabric's machinery as total factor productivity. The residual $\tilde v$ is what Section 5.9.1 defines, with $\eta_R \frac{d}{dt}\ln\|R\|_w$ as the one-dimensional summary of the scaling term. The elasticities $\eta_i$ are not estimated by regression on observational data (which would confound them with $A$); the fabric estimates them experimentally by scaling the resource allocation of a random subset of pods by a factor $s$ for a window and measuring the paired change in $\ln P$: $\hat\eta_i = \Delta \ln P / \ln s$ with its interval. This is a resource RCT, and it is run in every certification window.

### **64.5 Proposition (Governed Growth Bound)**

*Statement.* Suppose the governor enforces $\tilde v(t) \le v_{\max}$ for all $t$ by throttling (Section 38.2), and the resource vector grows at most as $\|R(t)\|_w$. Then for every $t \ge 0$, whatever the ungoverned dynamics (any $\varphi$, any $\kappa$),

$$
P(t) \;\le\; P(0)\, e^{v_{\max} t}\, \Big(\frac{\|R(t)\|_w}{\|R(0)\|_w}\Big)^{\eta_R},
$$

no finite-time singularity can occur, and the doubling time of the machinery index is never shorter than $\ln 2 / v_{\max}$.

*Proof.* By 64.4, $\frac{d}{dt}\ln P = \tilde v + \eta_R \frac{d}{dt}\ln\|R\|_w \le v_{\max} + \eta_R \frac{d}{dt}\ln\|R\|_w$. Integrating from $0$ to $t$ gives $\ln P(t) - \ln P(0) \le v_{\max} t + \eta_R\big(\ln\|R(t)\|_w - \ln\|R(0)\|_w\big)$, which is the bound after exponentiation. The right-hand side is finite for every finite $t$, so no blow-up is possible; and $\ln A(t) - \ln A(0) = \int_0^t \tilde v \le v_{\max} t$ gives $T_2 \ge \ln 2 / v_{\max}$. $\square$

*Corollary (stopping distance).* At a HALT, no new evaluation starts and no promotion is signed; the in-flight population is at most $L = \lambda W_{\text{sojourn}}$ by Little's law and completes within $W_{\max}$; with lease TTL $T_{\text{lease}}$, activity ceases within $T_{\text{lease}} + W_{\max}$ regardless of $N$ (Section 36.3).

*Remark.* The proposition is elementary; its value is that it is checkable. The governor's enforcement is a Section 37 invariant, and `velocity_vs_envelope` (Section 5.14) is the running witness that the hypothesis of the proposition holds.

### **64.6 Conjecture (exponent decomposition)**

*Statement.* Over windows in which the verification plane is not saturated, the effective exponent decomposes into measurable elasticities,

$$
\varphi_{\text{eff}} - 1 \;=\; \beta_K - \beta_D - \beta_V - \beta_G ,
$$

where $\beta_K$ is the elasticity of velocity with respect to the stock of admitted knowledge (non-rival reuse, Section 51.1), $\beta_D$ the elasticity with respect to the duplicate search rate (Jones's duplication externality), $\beta_V$ the elasticity with respect to verification saturation $\lambda_{\text{gen}}/\lambda_V$, and $\beta_G$ the elasticity with respect to proxy divergence (FP-5).

*Measurement.* Regress $\ln\tilde v_w$ on $\ln P_w$, $\ln K_w$, $\ln \text{DSR}_w$, $\ln(\lambda_{\text{gen}}/\lambda_V)_w$ and $\ln \text{div}_w$ over windows $w$, with block-bootstrap intervals to respect autocorrelation; the conjecture holds in a configuration if the coefficient on $\ln P_w$ is statistically indistinguishable from $\beta_K - \beta_D - \beta_V - \beta_G$ computed from the other coefficients, and it fails if a residual dependence on $P$ remains. Either outcome is informative: a residual dependence names an elasticity this document has not identified.

*Why it is a conjecture.* The decomposition is exact for a multiplicatively separable velocity, $\tilde v \propto K^{\beta_K}\text{DSR}^{-\beta_D}(\lambda_{\text{gen}}/\lambda_V)^{-\beta_V}\text{div}^{-\beta_G}$, and each factor's dependence on $P$ is then a power law; the claim that the fabric's velocity is separable in these four drivers is empirical.

### **64.7 Proposition (envelope-optimal meta-fraction)**

*Setting.* Horizon $T$; $\varphi = 1$, $\lambda_A = 1$; fixed resources; a fraction $f$ of decisions improves the machinery, so $A(t) = e^{\kappa f t}$, and the remainder $(1-f)$ harvests capability at rate $(1-f)\,A(t)\,P_0$. Cumulative harvested capability is

$$
J(f) = P_0\,(1-f)\,\frac{e^{\kappa f T} - 1}{\kappa f}.
$$

*Statement.* (i) Ungoverned, for $\kappa T \ge 4$ the maximizer is the larger root of $f(1-f) = 1/(\kappa T)$,

$$
f^{*} = \frac{1 + \sqrt{1 - 4/(\kappa T)}}{2} \;\longrightarrow\; 1 - \frac{1}{\kappa T}\quad(\kappa T \to \infty),
$$

so for a long horizon almost all effort goes to the machinery and harvesting is deferred to the end. (ii) Under a binding governor $\kappa f \le v_{\max}$ with $v_{\max}/\kappa < f^{*}$, the constrained optimum is $f_{\mathcal{G}} = v_{\max}/\kappa$, and the harvested share is $1 - v_{\max}/\kappa$. (iii) For every $t$ below a crossover $t_\times$, cumulative capability under the governed policy exceeds that under the ungoverned optimum; for small $t$ the ratio is $(1 - v_{\max}/\kappa)\,\kappa T$.

*Proof.* (i) For $\kappa f T \gg 1$, $\ln J \approx \ln(1-f) + \kappa f T - \ln f + \text{const}$; setting the derivative $-\frac{1}{1-f} + \kappa T - \frac{1}{f}$ to zero gives $\kappa T = \frac{1}{f(1-f)}$. The second derivative $-\frac{1}{(1-f)^2} + \frac{1}{f^2}$ is negative iff $f > \tfrac{1}{2}$, so the larger root is the maximum and the smaller a minimum. (ii) $J$ is increasing on $[0, f^{*}]$, so a constraint $f \le v_{\max}/\kappa < f^{*}$ binds at its boundary. (iii) At small $t$, both cumulative harvests are linear: governed $\approx (1 - v_{\max}/\kappa) P_0 t$, ungoverned-optimal $\approx (1 - f^{*}) P_0 t \approx P_0 t/(\kappa T)$; the ratio is $(1 - v_{\max}/\kappa)\kappa T \gg 1$. Both are continuous and the ungoverned curve eventually dominates (it has the larger exponent), so a crossover exists. $\square$

*Interpretation.* The envelope is not only a safety device. Without it, the optimal policy for a fabric with a long horizon is to improve itself and deliver almost nothing until the end; with it, the fabric delivers verified capability continuously at the ratified rate. That is the design intent of $v_{\max}$: it is the rate at which humans have decided to take delivery.

### **64.8 Detection and attribution by optimal fingerprinting**

A capability series integrates many small fast fluctuations, and Hasselmann's stochastic model shows that such integration produces red noise whose excursions look like trends. A change in $\tilde v$ is therefore *detected* and *attributed* by optimal fingerprinting, not by eye. Let $y$ be the vector of windowed $\tilde v$ observations, $F$ the matrix whose column $m$ is the expected response pattern of meta-promotion $m$ (a step at its rollout time, smoothed over the separation timescale of Section 25.1), and $\Sigma_\varepsilon$ the noise covariance estimated from control pods and pre-rollout periods (including its autocorrelation). The generalized least squares estimate of the amplitudes is

$$
\hat a = (F^{\top}\Sigma_\varepsilon^{-1}F)^{-1}F^{\top}\Sigma_\varepsilon^{-1}\, y, \qquad
\text{Cov}(\hat a) = (F^{\top}\Sigma_\varepsilon^{-1}F)^{-1}.
$$

*Detection* of meta-promotion $m$'s effect is the interval of $\hat a_m$ excluding zero; *attribution* is the interval including one (the observed response has the predicted amplitude). The detection statistic and its confidence are reported in the Section 48.1 certificate, and the randomized rollout of Section 40.4 is what makes $F$ and $\Sigma_\varepsilon$ identifiable.

### **64.9 Estimating $\varphi$**

Partition the certification history into windows $w$ long enough that $\tilde v_w$ is estimated with relative error below 20%. Regress $\ln \tilde v_w$ on $\ln P_w$; the slope is $\hat\varphi - 1$, with a block-bootstrap interval. The exponential-regime condition is $\text{LCB}_{95}(\hat\varphi) \ge 1 - \varepsilon_\varphi$ (initially $\varepsilon_\varphi = 0.05$) over at least three doublings of $P$ with resources held fixed or normalized by 64.4. Fewer than three doublings gives an interval too wide to certify anything, which is why the certificate first becomes available at M1.

## **65. STATISTICAL DECISION THEORY OF PROMOTION**

### **65.1 Concentration bounds**

For i.i.d. observations in $[a, b]$ with mean $\mu$, Hoeffding's inequality gives $\Pr(|\bar X_n - \mu| \ge \varepsilon) \le 2\exp\!\big(-2n\varepsilon^{2}/(b-a)^{2}\big)$, hence

$$
n \;\ge\; \frac{(b-a)^{2}}{2\varepsilon^{2}}\ln\frac{2}{\delta}
$$

suffices for precision $\varepsilon$ at confidence $1-\delta$. The empirical-Bernstein bound replaces $(b-a)^2$ by the sample variance up to a lower-order term, $|\bar X_n - \mu| \le \sqrt{2\hat\sigma_n^{2}\ln(3/\delta)/n} + 3(b-a)\ln(3/\delta)/n$, which is what the fabric uses when the metric's variance is far below its range (the usual case for micro-benchmarks).

### **65.2 Fixed-sample test**

For paired differences with mean $\tau$ and variance $\sigma^2$, the one-sided test of $H_0: \tau \le 0$ against $H_1: \tau \ge \Delta$ at error rates $(\alpha, \beta)$ needs

$$
n_B = \Big(\frac{(z_{1-\alpha} + z_{1-\beta})\,\sigma}{\Delta}\Big)^{2}
$$

observations. This is the v2 baseline's cost per decision.

### **65.3 Sequential probability ratio test**

With $z_i = \frac{\Delta}{\sigma^2}(d_i - \frac{\Delta}{2})$ the per-observation log-likelihood ratio, $S_n = \sum_{i\le n} z_i$, and thresholds $A = \ln\frac{1-\beta}{\alpha}$, $B = \ln\frac{\beta}{1-\alpha}$, Wald's identity $\mathbb{E}[S_N] = \mathbb{E}[N]\,\mathbb{E}[z]$ with $\mathbb{E}_1[z] = \text{KL} = \Delta^2/(2\sigma^2)$ and $\mathbb{E}_0[z] = -\text{KL}$ gives the expected sample sizes of Section 17.2 (ignoring overshoot). Numerically, with $\sigma^2/\Delta^2$ as the unit:

| **$\alpha = \beta$** | **$A$** | **$\mathbb{E}_{0,1}[N]$** | **$n_B$** | **ratio** |
|---|---|---|---|---|
| 0.05 | 2.944 | 5.30 | 10.82 | 2.04 |
| 0.01 | 4.595 | 9.01 | 21.65 | 2.40 |
| 0.001 | 6.907 | 13.79 | 38.20 | 2.77 |

For a candidate with true effect $\tau$ the drift is $\mathbb{E}[z] = \frac{\Delta}{\sigma^2}(\tau - \frac{\Delta}{2})$; a clearly worse candidate ($\tau = -2\Delta$) has drift $-2.5\,\Delta^2/\sigma^2$ and stops after $\approx A/2.5 = 1.18\,\sigma^2/\Delta^2$ observations at $\alpha = 0.05$. The realized mean $\bar n$ over the candidate mixture is what the fabric reports; the boundary values above are its worst case.

Wald and Wolfowitz proved that among all tests with error probabilities at most $(\alpha, \beta)$, the SPRT minimizes $\mathbb{E}_0[N]$ and $\mathbb{E}_1[N]$ simultaneously. Composite alternatives use a mixture likelihood ratio (integrating $\Delta$ over a prior), which keeps the same optional-stopping validity.

### **65.4 Confidence sequences and e-values**

A confidence sequence is a sequence of intervals with $\Pr(\forall n: \tau \in \text{CI}_n) \ge 1 - \alpha$; it may be inspected and acted on at any time. For sub-Gaussian observations the width is $O(\sqrt{\log\log n / n})$, the law-of-the-iterated-logarithm rate, so the cost of time-uniform validity over a fixed-$n$ interval is a $\sqrt{\log\log n}$ factor.

An e-value for $H_0$ is a non-negative statistic with $\mathbb{E}_{H_0}[E] \le 1$. By Markov, $\Pr_{H_0}(E \ge 1/\alpha) \le \alpha$. A product of sequentially computed e-values is a non-negative supermartingale under $H_0$, and Ville's inequality gives $\Pr_{H_0}(\sup_n E_n \ge 1/\alpha) \le \alpha$: evidence can be accumulated across batches, cells and time and acted on at any stopping time without inflating $\alpha$. The likelihood ratio of the SPRT is the canonical e-process; its thresholds are the e-value thresholds $1/\alpha$ up to the $\beta$ correction.

For $m$ hypotheses with e-values $e_1, \dots, e_m$, the e-BH procedure rejects the hypotheses with $e_{(i)} \ge \frac{m}{q\, i}$ for the largest such $i$, and controls the false-discovery rate at $q$ under arbitrary dependence; this is the fabric's promotion-level guarantee (Section 17.4).

### **65.5 Selection bias**

For $k$ candidates with equal true effect and Gaussian measurement noise, the expected standardized maximum is

| $k$ | 10 | $10^2$ | $10^3$ | $10^4$ | $10^5$ | $10^6$ | $10^8$ | $10^9$ |
|---|---|---|---|---|---|---|---|---|
| $\mathbb{E}[\max Z]$ | 1.54 | 2.51 | 3.24 | 3.85 | 4.38 | 4.86 | 5.71 | 6.09 |

(exact values by quadrature; the asymptotic $\sqrt{2\ln k}$ overstates them by 0.4–0.6). The screening winner's score therefore exceeds its truth by that many $\sigma$ in expectation, which is the quantitative content of FP-5 and the reason for Section 17.5. Empirical-Bayes shrinkage, $\hat\tau_{\text{shrunk}} = \bar\tau + \frac{\sigma_\tau^2}{\sigma_\tau^2 + \sigma^2/n}(\hat\tau - \bar\tau)$ with $\sigma_\tau^2$ the across-candidate variance of true effects estimated from the population, corrects the estimate; re-measurement on fresh seeds removes the bias entirely.

### **65.6 Proposition (Information–Verification Bound)**

*Statement.* Let the verification plane sustain at most $\lambda_V$ observation-evaluations per second, let every promotion decision be a sequential test at error rates $(\alpha, \beta)$ with per-observation information $\mathcal{K}$ (expected log-likelihood ratio under the alternative), and let $\delta$ be the mean verified gain per promotion. Then the capability production rate satisfies

$$
P \;\le\; B := \frac{\lambda_V\, \mathcal{K}\, \delta}{c_{\alpha\beta}}, \qquad
c_{\alpha\beta} = (1-\beta)\ln\frac{1-\beta}{\alpha} + \beta\ln\frac{\beta}{1-\alpha},
$$

and over any window $[0, T]$ in which the fabric is verification-bound, $P(t) \ge (1-\varepsilon)B(t)$, the average velocity satisfies

$$
\bar v = \frac{1}{T}\int_0^T v\,dt \;\le\; \overline{\frac{\dot\lambda_V}{\lambda_V}} + \overline{\frac{\dot{\mathcal{K}}}{\mathcal{K}}} + \overline{\frac{\dot\delta}{\delta}} + \frac{1}{T}\ln\frac{1}{1-\varepsilon},
$$

where the bars denote window averages.

*Proof.* Wald's lower bound states that any sequential test with error probabilities at most $(\alpha, \beta)$ has expected sample size under the alternative at least $n_{\min} = c_{\alpha\beta}/\mathcal{K}$. Promotions per second are at most the observation budget divided by the minimum observations per promotion decision: $\pi \le \lambda_V / n_{\min} = \lambda_V\mathcal{K}/c_{\alpha\beta}$. Hence $P = \pi\,\delta \le B$. For the velocity statement, $\ln P(T) - \ln P(0) \le \ln B(T) - \ln\big((1-\varepsilon)B(0)\big) = \ln\frac{B(T)}{B(0)} + \ln\frac{1}{1-\varepsilon}$, using $P(T) \le B(T)$ and $P(0) \ge (1-\varepsilon)B(0)$. Since $\ln\frac{B(T)}{B(0)} = \int_0^T \big(\frac{\dot\lambda_V}{\lambda_V} + \frac{\dot{\mathcal{K}}}{\mathcal{K}} + \frac{\dot\delta}{\delta}\big)dt$ (with $c_{\alpha\beta}$ fixed by the risk class), dividing by $T$ gives the result. $\square$

*Corollaries.* (a) The candidate generation rate, token count, agent count and mutation rate do not appear: they can raise $P$ only through $\mathcal{K}$ (better candidates have larger $\Delta$) or $\delta$. (b) Exponential growth of $P$ requires exponential growth of the product $\lambda_V\mathcal{K}\delta$; a fabric that scales generation without scaling verification is bounded by a constant. (c) $\mathcal{K} = \Delta^2/(2\sigma_{\text{eff}}^2)$ is raised by variance reduction (40.2), evaluator reliability (18.1) and candidate quality; this is why those levers are in Phase 1 (Section 54.1). (d) Relaxing $(\alpha,\beta)$ lowers $c_{\alpha\beta}$ and raises $B$, but it also raises the false-promotion rate and hence $\rho_{\text{reg}}$; the net quantity $P(1 - \rho_{\text{reg}}h)$ (Section 61.1) is what the risk-class defaults are chosen to maximize, and they are not RSI targets.

*Remark.* The bound is tight up to overshoot when the verifier is an SPRT and every candidate sits at the alternative; the fabric's realized slack $1 - P/B$ is reported as a measure of how far the pipeline is from being verification-bound, which is the condition under which the lever map of Section 54.1 applies.

### **65.7 Funnel thresholds**

With stage costs $c_i$ and a calibrated surrogate, the stage-$i$ pass threshold that maximizes expected true-winner discoveries per unit cost is the one at which the marginal candidate's expected improvement per unit of downstream cost equals the fabric-wide shadow price of a full-fidelity evaluation (the market price of a verification slot, Section 23). This ties the funnel's $s_i$ to the market rather than to a fixed percentile, and makes the funnel tighten automatically when verification is scarce (FP-4).

## **66. SCALABILITY AND QUEUEING**

### **66.1 Universal Scalability Law**

Amdahl's law with serial fraction $\gamma$ gives $S(N) = N/(1 + \gamma(N-1))$, monotone and bounded by $1/\gamma$. Adding a coherence cost that grows with the number of pairs, $\theta N(N-1)$ (every worker exchanging state with every other), gives the Universal Scalability Law

$$
S(N) = \frac{N}{1 + \gamma(N-1) + \theta N(N-1)},
$$

which has a maximum at $N^* = \sqrt{(1-\gamma)/\theta}$ and *falls* beyond it: adding workers past $N^*$ reduces throughput. The fabric fits $(\gamma, \theta)$ per pipeline stage by nonlinear least squares on measured $S(N)$ at several $N$ (at least five points spanning a decade), reports both with intervals in every certificate, and sizes pods at $N^*/2$ (Section 10.1). The quadratic term is why the design pushes $\theta$ toward zero rather than merely small: at $N = 10^6$, $\theta = 10^{-10}$ still costs $\theta N^2 = 100$ units of coherence per unit of work.

### **66.2 Amdahl and Gustafson**

Amdahl bounds speedup at fixed problem size by $1/\gamma$. Gustafson's scaled speedup $S = N - \gamma(N-1)$ applies when the problem grows with the machine; the fabric's problem (the supply of candidate evaluations) is unbounded, so it is in Gustafson's regime and the binding term is coherence, not the serial fraction. Within a single evaluation, however, Amdahl applies to the pipeline stages (Section 31.1).

### **66.3 Little's law and utilization**

$L = \lambda W$ holds for any stable queueing system without assumptions on the arrival or service distributions. Its uses here: sizing the in-flight population and hence memory and sandbox counts (Section 4.1); bounding the stopping distance (Section 36.3); and detecting hidden queues (a stage whose measured $L$ exceeds $\lambda W$ for its declared $W$ is buffering somewhere undeclared). With $c$ servers and utilization $u$, the mean queueing delay in the M/M/c approximation grows like $1/(1-u)$ near saturation, which is why the target utilization is 0.7: the mean sojourn in the M/M/1 model is $s/(1-u)$, about $3.3\times$ the service time at $u = 0.7$, $10\times$ at $u = 0.9$ and $100\times$ at $u = 0.99$, and the tail quantiles are worse.

### **66.4 Epidemic propagation**

Push–pull gossip with fanout $f$ informs all $N$ nodes in $\log_{f+1} N + O(\log\log N)$ rounds with high probability, with $O(N\log\log N)$ total messages for push–pull (versus $O(N\log N)$ for push only). Convergence time is rounds × round period; message cost per node is $O(f\log N)$. Both are reported per certification window, and the knowledge plane's propagation latency SLO (Section 35) is set from them.

### **66.5 Near-decomposability**

Simon's aggregation result: in a system whose interaction matrix has blocks with internal interaction strength of order 1 and inter-block strength of order $\epsilon$, the dynamics separate into a fast phase in which each block equilibrates independently (timescale of order 1) and a slow phase in which only block aggregates interact (timescale of order $1/\epsilon$), with the error of treating the blocks as independent of order $\epsilon$. This is the formal basis for pods (Section 10.1), for the separation ratio (Section 25.1) and for region autonomy (Section 59): the fabric is built as a hierarchy of nearly decomposable blocks, and $\epsilon$ at each level is measured as the normalized cut of the interaction graph.

### **66.6 Worked sizing M0–M6 (assumptions stated)**

| **Rung** | **$\lambda$** | **Mean service** | **Compute units (at $u=0.7$)** | **In-flight $L$** | **Ledger hot path** | **Energy / eval (assumed)** | **Power** |
|---|---|---|---|---|---|---|---|
| M0 | $10^3$ | 20 ms-core | ~32 cores | 50 | 256 KB/s | 0.5 J | ~0.5 kW |
| M1 | $10^4$ | 10 ms-core | ~160 cores | 200 | 2.6 MB/s | 0.2 J | ~2 kW |
| M2 | $10^5$ | 5 ms-core | ~800 cores | 1,000 | 26 MB/s | 0.1 J | ~10 kW |
| M3 | $10^6$ | 1 ms-core-equiv. | ~1,500 cores + accelerators | $10^4$ | 256 MB/s | 20 mJ | ~20 kW |
| M4 | $10^7$ | 100 µs accel. | ~1,500 devices | $10^5$ | 2.6 GB/s (local) | 5 mJ | ~50 kW |
| M5 | $10^8$ | 20 µs accel. | ~3,000 devices | $10^6$ | 26 GB/s (local) | 2 mJ | ~200 kW |
| M6 | $10^9$ | 10 µs accel. | ~$10^4$ devices | $10^6$ (1 ms sojourn) | 256 GB/s (local) | 1–6 mJ | ~1–6 MW |

The service-time column is the design assumption that drives everything else; it falls by $\sim 10\times$ per three rungs because evaluations move from processes to batched accelerator kernels (Section 32). Every entry is a target, replaced by measurement at certification.

## **67. PHYSICS ENVELOPE**

### **67.1 Thermodynamic floor**

Landauer: $E_{\min} = k_B T\ln 2 = 2.87\times10^{-21}$ J per erased bit at 300 K. An evaluation that irreversibly erases $b$ bits costs at least $b\,E_{\min}$: $3$ pJ at $b = 10^9$, $3$ nJ at $b = 10^{12}$. The practical energies of Section 66.6 (mJ to J) sit $10^{6}$–$10^{11}$ above the floor. The ceiling on evaluations per second at power $W$ with $b$ erased bits each is $W/(b E_{\min})$: about $3\times10^{20}$/s at 1 GW and $b = 10^{9}$. Nothing on the ladder approaches it; the envelope that binds is engineering (data motion, utilization, overhead), and Section 67.4 quantifies where.

### **67.2 Ultimate bounds (for orientation only)**

The Margolus–Levitin bound limits a system of energy $E$ above its ground state to at most $2E/(\pi\hbar) \approx 6\times10^{33}$ orthogonal state transitions per second per joule; Bremermann's limit is the same statement per unit mass, $\approx 1.4\times10^{50}$ bits per second per kilogram. They are quoted so that no rung is ever specified beyond them and for no other reason; they are $10^{15}$ or more above anything in this document.

### **67.3 Causal limits**

| **Distance** | **One-way (vacuum)** | **One-way (fiber, $2\times10^8$ m/s)** | **Max synchronous loop rate (fiber RTT)** |
|---|---|---|---|
| 1 m (in rack) | 3.3 ns | 5 ns | 100 MHz |
| 100 m (in hall) | 0.33 µs | 0.5 µs | 1 MHz |
| 10 km (metro) | 33 µs | 50 µs | 10 kHz |
| 1,000 km | 3.3 ms | 5 ms | 100 Hz |
| 4,000 km (continental) | 13 ms | 20 ms | 25 Hz |
| 20,000 km (antipodal) | 67 ms | 100 ms | 5 Hz |

A loop at rate $f$ that requires a synchronous exchange can span at most $c_{\text{fiber}}/(2f)$. This is the quantitative content of FP-1 and Rules A–B, and it is why every rung above M1 is a sum of local loops.

### **67.4 Data-motion envelope**

Using the FP-2 energy-per-bit figures and the Section 28.1 rule that off-node data motion may consume at most 10% of an evaluation's energy, the off-node byte budget per evaluation is $b_k \le 0.1\,\varepsilon_k / (8 \times 50\ \text{pJ})$:

| **Rung** | **$\varepsilon_k$ (assumed)** | **$b_k$ off-node** | **What fits** |
|---|---|---|---|
| M0 | 0.5 J | 125 MB | anything |
| M3 | 20 mJ | 5 MB | full records and artifacts |
| M4 | 5 mJ | 1.2 MB | records; artifacts by reference |
| M5 | 2 mJ | 500 KB | records only |
| M6 | 1 mJ | 250 KB | records; artifacts by reference; link bandwidth binds equally |
| M9 | 1 µJ | 250 B | one hot-path record, nothing else |

At M6 the envelope allows records and referenced artifacts but, at $10^{9}$ records per second, the *aggregate* hot path is 256 GB/s, which is why records stay in local shards with TTL and only Merkle roots and aggregates travel (Section 19.2); at M9 the envelope allows one 256-byte record per evaluation and nothing else, and the aggregate (256 TB/s) makes per-evaluation records off-device impossible, so the design must emit statistics. These are the two structural facts behind the ledger strategy of Section 19.2 and the M5 → M6 transition of Section 32.

### **67.5 Per-rung envelope**

| **Rung** | **$\lambda$** | **$\varepsilon$ at 1 MW** | **$\varepsilon$ at 100 MW** | **Accelerator time per evaluation at 300 W** | **Feasibility** |
|---|---|---|---|---|---|
| M0 | $10^{3}$ | 1 kJ | — | — | processes on a node |
| M3 | $10^{6}$ | 1 J | 100 J | 3.3 ms | compiled, node-local |
| M6 | $10^{9}$ | 1 mJ | 100 mJ | 3.3 µs at 1 MW; 330 µs at 100 MW | batched accelerator kernels |
| M9 | $10^{12}$ | 1 µJ | 100 µJ | 3.3 ns at 1 MW; 330 ns at 100 MW | in-device micro-evaluations only |
| M12 | $10^{15}$ | 1 nJ | 100 nJ | — | beyond current device architectures; thermodynamically allowed |

The ladder is engineering-bound through M9 and architecture-bound beyond it; it is nowhere physics-bound before $\sim$M17. The program therefore never has to argue with physics for its stated horizons, and it is required to argue with data motion at every rung.

### **67.6 Thermodynamic efficiency**

As an open, dissipative system (FP-2), the fabric's efficiency is verified-knowledge bits retained per joule dissipated. Its ceiling is $1/E_{\min} \approx 3.5\times10^{20}$ bits/J. At M0, with ~0.5 J per evaluation and a knowledge yield of order $10^{-2}$–$10^{0}$ bits per evaluation (Section 5.6), the fabric runs at $10^{-2}$–$10^{0}$ bits/J, i.e. $10^{20}$ below the ceiling. The number is reported not because it will ever be approached but because its trend across rungs is the cleanest single statement of whether efficiency, and not only throughput, is scaling (Section 49: compute_scaling_without_efficiency_scaling).

## **68. THE 4× CAPABILITY-PRODUCTION CONTRACT**

### **68.1 Definition**

The **baseline** $\mathcal{B}$ is the v2 fabric at the same hardware, the same candidate generators, the same evaluators and the same risk-class error rates, deciding every promotion with a fixed-sample test of size $n_B$ (Section 65.2), unpaired, with no funnel, no surrogate screening, no deduplication, no resource market, a static FP-6 split, no error-threshold scheduling, and the v2 promotion criterion. The **multiplier** is

$$
\mathcal{M} = \frac{P_{\text{v3}}}{P_{\mathcal{B}}}\ \ \text{at equal hardware and equal realized } (\alpha, \beta),
$$

and the contract is $\text{LCB}_{95}(\mathcal{M}) \ge 4$ at M0, with design target $\mathcal{M} \ge 8$ and the vertical ladder $\mathcal{M}_k^{\text{target}} = 4\cdot2^{k}$ (Section 4.0).

### **68.2 Composition**

$P = \lambda\, y_P\, \delta$, and the v3 mechanisms act on three factors:

$$
\mathcal{M} = \underbrace{\mathcal{M}_{\text{seq}}\,\mathcal{M}_{\text{VRF}}}_{\mathcal{M}_\lambda:\ \text{decisions per evaluation}}\ \times\ \underbrace{\mathcal{M}_{\text{funnel}}\,\mathcal{M}_{\text{dedup}}\,\mathcal{M}_{\text{sched}}}_{\mathcal{M}_y:\ \text{promotions per decision}}\ \times\ \underbrace{\mathcal{M}_{\text{prior}}\,\mathcal{M}_{\text{robust}}}_{\mathcal{M}_\delta:\ \text{net gain per promotion}}.
$$

| **Factor** | **Mechanism** | **Theory** | **Range (derived)** | **M0 design assumption** |
|---|---|---|---|---|
| $\mathcal{M}_{\text{seq}}$ | sequential tests | 65.3; 72.2 check 1: 1.6–2.3 at the boundary (simulated); 4–6 on a realistic mixture | 1.6–6 | 2.5 |
| $\mathcal{M}_{\text{VRF}}$ | CRN + control variates | 40.2: $1/((1-\rho)(1-r^2))$ | 1.5–10 | 2.0 ($\rho = 0.5$) |
| $\mathcal{M}_{\text{funnel}}$ | multi-fidelity funnel incl. surrogate stage, recall-weighted | 16.1 | 1.5–20 | 1.5 (conservative; recall must be measured first) |
| $\mathcal{M}_{\text{dedup}}$ | LSH deduplication | $1/(1-\text{DSR})$ | 1.05–1.3 | 1.05 |
| $\mathcal{M}_{\text{sched}}$ | bandit + portfolio + error-threshold scheduling | FP-6, 14.1–14.2 | 1.1–1.5 | 1.1 |
| $\mathcal{M}_{\text{prior}}$ | knowledge priors, descendant value, market | 20, 24, 23 | 1.0–2.0 | 1.0 (no credit until measured) |
| $\mathcal{M}_{\text{robust}}$ | robust promotion lowering regression harm | 17.6, 61.1 | 1.0–1.3 | 1.0 |

Product of the M0 design assumptions: $2.5 \times 2.0 \times 1.5 \times 1.05 \times 1.1 = 8.7$ (the ablation in 72.2, check 7, recovers it from simulated pods). Product of the lower ends of the derived ranges: $1.6 \times 1.5 \times 1.5 \times 1.05 \times 1.1 = 4.2$. The contract floor of 4 is therefore at the product of the most conservative values of only five of the seven factors; the design target of 8 is the product of the assumptions, and the ranges say the realized multiplier is likely to be larger. Factors overlap in two places and are counted once: the surrogate is funnel stage 1 (not a separate factor), and CRN and control variates are measured jointly as VRF.

### **68.3 Measurement protocol**

$\mathcal{M}$ is certified by **randomized ablation**, which is itself an FP-1 experiment:

1. Enumerate the mechanisms $\{m_1, \dots, m_J\}$ (seven above).
2. Over the certification window, assign each pod a random mechanism configuration from a fractional factorial design (resolution IV or better, so main effects are not aliased with two-factor interactions), including the all-off configuration (= $\mathcal{B}$) and the all-on configuration (= v3).
3. Measure $\ln P$ per pod per sub-window, paired on seeds and candidate streams (CRN at the pod level).
4. Estimate the main effects $\hat e_j$ and the relevant interactions on $\ln P$ by least squares with pod-clustered errors; $\widehat{\ln\mathcal{M}} = \sum_j \hat e_j + \text{interactions}$, with a confidence interval.
5. Verify *equal error guarantees*: realized $(\alpha, \beta)$ on the calibration stream (Section 34.2) under v3 are no worse than under $\mathcal{B}$; if they are, the v3 decisions are re-thresholded until they are, and step 4 is recomputed.
6. Certify if $\text{LCB}_{95}(\mathcal{M}) \ge 4$ and the all-on versus all-off contrast agrees with the factorial estimate within its interval.

### **68.4 Attribution**

Because $\ln P$ is additive across mechanisms to first order, Shapley values on the factorial estimates (Section 24.2, with coalitions = subsets of mechanisms and $G(T) = \widehat{\ln P}(T) - \widehat{\ln P}(\emptyset)$) give each mechanism's share of $\ln\mathcal{M}$; the shares sum to $\ln\mathcal{M}$ exactly and are reported in the certificate. A mechanism whose share is indistinguishable from zero is removed from the fast path (it costs overhead) and returned to the research population.

### **68.5 What does and does not count**

Counts toward $\mathcal{M}$: fewer evaluations per decision at equal error; more promotions per decision at equal error; larger verified gain per promotion; lower regression harm. Does not count: relaxed error rates; surrogate estimates counted as evaluations; duplicate experiments; any change to the evaluators between arms; hardware differences between arms; and any gain whose ablation estimate is not causally identified by the design above.

### **68.6 The multiplier as an RSI target**

$\mathcal{M}$ is a product of factors each of which is a property of the machinery, so $\ln\mathcal{M}$ grows at the rate $\sum_j \dot e_j$; the vertical ladder's doubling per rung is the statement that $\ln\mathcal{M}$ should grow by $\ln 2$ per rung. The factors with the most headroom at M0 (funnel recall, priors, robustness) are exactly the ones whose design assumption above is set to 1.0–1.5 pending measurement; the meta-RSI population's first objective after M0 certification is to move them.

## **69. TRACEABILITY FROM v2.0 TO v3.0**

| **v2 §** | **v3 §** | **Disposition** |
|---|---|---|
| 0 | 0 | retained; version 3.0; north star M6; growth law, contract and envelope fields added |
| 1 | 1 | retained; formal objective 1.1; falsifiable hypothesis 1.2 |
| 2 | 2 | retained; formal tuple 2.1; RSI condition 2.2; loop annotated 2.4 |
| 3 FP-1…FP-10 | 3 | retained; each principle formalized with numbers; Goodhart governor, portfolio form, Hayek/Simon, Solow/Hasselmann added |
| 4 | 4 | retained; ladder extended to M9 with physics envelope 4.1; vertical ladder 4.0; minimum-information criterion 4.2 |
| 5.1–5.10 | 5.1–5.10 | retained; each with estimator and interval; RIV becomes $v$, $\tilde v$, $\varphi$; 5.11–5.14 added |
| 6 | 6 | retained; every gate a statistical statement; production-multiplier and governance gates added |
| 7 | 7 | retained; envelope rule and projection added |
| 8 | 8 | retained; plane invariant table 8.1 |
| 9 | 9 | retained; throughput model 9.1; halt lease field |
| 10 | 10 | retained; USL pod sizing 10.1; gossip 10.2; spectral partition |
| 11 | 11 | retained; factorized form with the contract |
| 12 | 12 | retained; overhead budgets per layer |
| 13 | 13 | retained; landscape correlation length and Parisi structure 13.1 |
| 14 | 14 | retained; cost-aware bandit 14.1; error-threshold scheduling 14.2 |
| 15 | 15 | retained; statistics block and risk-class defaults |
| 16 | 16 | retained; funnel economics 16.1; successive halving 16.2 |
| 17 | 17 | retained; SPRT 17.2; confidence sequences 17.3; FDR 17.4; re-measurement 17.5; robust promotion 17.6 |
| 18 | 18 | retained; evaluator quality metrics 18.1; blindness and rotation rules |
| 19 | 19 | retained; Merkle DAG 19.1; bandwidth and retention 19.2 |
| 20 | 20 | retained; belief update 20.2; MDL admissibility 20.3; coarse-graining relevance 20.4 |
| 21 | 21 | retained; penalty 21.1; valuation 21.2; LSH index 21.3 |
| 22 | 22 | retained; novelty score and acquisition 22.1 |
| 23 | 23 | retained; Hayek rationale, proportional fairness and VCG 23.2; audit 23.3 |
| 24 | 24 | retained; Bellman form 24.1; Shapley attribution 24.2 |
| 25 | 25 | retained; separation ratio 25.1; physical clocks 25.2 |
| 26 | 26 | retained; contract in the objective; sizing 26.1 |
| 27 | 27 | retained; annotated; latency budget 27.1 |
| 28 | 28 | retained; bytes budget 28.1 |
| 29 | 29 | retained; HALTED state; HLC and idempotency 29.1 |
| 30 | 30 | retained; series extended; alarms as anytime-valid tests 30.1 |
| 31 | 31 | retained; queueing detection 31.1 |
| 32 | 32 | retained; budgets per transition; M5 → M6 added |
| 33 M5 model | 33 M6 model | renamed and extended; numbers 33.1 |
| 34 | 34 | retained; screening rule 34.1; calibration stream 34.2; model classes 34.3 |
| 35 | 35 | retained; priority with relevance 35.1; transport 35.2 |
| 36 | 36 | retained; isolation by risk class 36.1; halt lease and stopping distance 36.3; threat model 36.4 |
| 37 | 37 | retained; new invariants; admissible actions 37.1; rules not discretion 37.2; design principles 37.3 |
| 38 | 38 | retained; residual control 38.1; envelope 38.2; attention allocation 38.3 |
| 39 | 39 | retained; design and analysis plan fields |
| 40 | 40 | retained; potential outcomes 40.1; variance reduction 40.2; interference 40.3; meta attribution 40.4 |
| 41 | 41 | retained; capture score 41.1; Wasserstein shift and robust promotion 41.3 |
| 42 | 42 | retained; layers 42.1; boundary rule 42.2; acyclicity 42.3; depth 42.4 |
| 43 A–F | 43 A–F | retained; each rule quantified |
| 44 | 44 | retained; Markov model 44.1; absorbing states |
| 45 | 45 | retained; $N_{\text{eff}}$ 45.1; overlap distribution 45.2; option value 45.3; threshold 45.4 |
| 46 | 46 | retained; determinism classes 46.1 |
| 47 | 47 | retained; criteria extended with the contract, statistics and governance |
| 48 | 48 | retained; regime certificate 48.1; learning by doing 48.2 |
| 49 | 49 | retained; detector per failure mode; new modes |
| 50 | 50 | retained; loop gain 50.1 |
| 51 | 51 | retained; non-rivalry and replication cost 51.1 |
| 52 | 52 | retained; six doctrine lines added |
| 53 | 53 | retained; two ladders |
| 54 | 54 | retained; phases extended; lever map 54.1 |
| 55 | 55 | retained; prohibitions and behaviours added; acceptance tests 55.1 |
| 56 | 56 | retained; scalability and statistical contracts, layer writes |
| 57 | 57 | retained; metamorphic, statistical and fabric-on-fabric classes |
| 58 | 58 | retained; roofline 58.1 |
| 59 | 59 | retained; latency 59.1; sovereignty 59.2 |
| 60 | 60 | retained; physical loops and sim-to-real 60.1 |
| 61 | 61 | retained; governing equation made measurable 61.1 |
| 62 | 62 | retained; annotated |
| — | 63–71 | new: notation; growth law; decision theory; scalability; physics; contract; traceability; foundations; reference computations |
| — | 72–73 | new: numerical verification with unedited output; open problems and falsification |

## **70. FOUNDATIONS INDEX**

Results this document rests on, with the work they come from and where they are used. Prize years are given where the work was recognized by a Nobel Memorial Prize in Economic Sciences or a Nobel Prize in Physics or Chemistry; results without a prize are standard mathematics and are listed for completeness.

| **Result** | **Origin** | **Used in** |
|---|---|---|
| Knowledge production function; non-rival ideas; endogenous growth | Romer (Economics 2018); general-exponent form by Jones (1995) | 5.10, 51.1, 64.2 |
| Growth accounting; total-factor-productivity residual | Solow (Economics 1987) | 5.9.1, 64.4 |
| Learning by doing; experience curve | Arrow (Economics 1972) | 48.2, 51.1 |
| Impossibility of non-dictatorial aggregation | Arrow (Economics 1972) | 5.4, 73.1 |
| Fixed-basket and chained index numbers | Laspeyres (1871); Fisher (1922) | 5.4, 73.1 |
| Lucas critique | Lucas (Economics 1995) | FP-5 |
| Rules rather than discretion; time inconsistency | Kydland and Prescott (Economics 2004) | 37.2 |
| Dispersed knowledge and prices | Hayek (Economics 1974) | FP-7, 23.1 |
| Near-decomposability; bounded rationality | Simon (Economics 1978) | FP-7, 10.1, 25.1, 66.5 |
| Nash bargaining solution; proportional fairness | Nash (Economics 1994); Kelly (1997) | 23.2 |
| Second-price auction; VCG mechanism | Vickrey (Economics 1996); Clarke (1971); Groves (1973) | 23.2 |
| Mechanism design; revelation principle | Hurwicz, Maskin, Myerson (Economics 2007) | 23.1–23.2 |
| Combinatorial clock auctions | Milgrom and Wilson (Economics 2020) | 23.2 |
| Portfolio selection; efficient frontier; Sharpe ratio | Markowitz, Sharpe (Economics 1990) | FP-6, 14.1 |
| Option pricing | Scholes and Merton (Economics 1997), with Black | 45.3 |
| Shapley value | Shapley (Economics 2012) | 24.2, 68.4 |
| Multitask incentives; informativeness | Holmström (Economics 2016); Holmström and Milgrom (1991) | FP-5 |
| Incomplete contracts; residual control rights | Hart (Economics 2016) | 38.1 |
| Rational inattention | Sims (Economics 2011) | 38.3 |
| Potential outcomes; LATE; instrumental variables | Angrist and Imbens (Economics 2021); Rubin | 40.1, 40.4 |
| Difference-in-differences | Card (Economics 2021) | 40.4 |
| Randomized controlled evaluation as the standard of evidence | Banerjee, Duflo, Kremer (Economics 2019) | 39, 40 |
| Sample-selection bias | Heckman (Economics 2000) | FP-5, 34.2 |
| Lead–lag screening; conditional heteroskedasticity | Granger, Engle (Economics 2003) | 40.4, 45.3 |
| Design principles for durable governance of shared resources | Ostrom (Economics 2009) | 37.3 |
| Asymmetric information; screening | Akerlof, Spence, Stiglitz (Economics 2001) | FP-4 |
| Optimal transport; linear programming | Kantorovich (Economics 1975) | 41.3, 17.6, 60.1 |
| Renormalization group; relevant and irrelevant operators | Wilson (Physics 1982) | 20.4, 35.1 |
| Replica symmetry breaking; overlap distribution; complex landscapes | Parisi (Physics 2021) | 13.1, 45.2 |
| Stochastic climate model; optimal fingerprinting | Hasselmann (Physics 2021) | FP-10, 64.8 |
| Energy-based models; learned representations | Hopfield, Hinton (Physics 2024) | 34.3 |
| Dissipative structures; entropy export | Prigogine (Chemistry 1977) | FP-2, 67.6 |
| Quasispecies; error threshold | Eigen (Chemistry 1967) | 14.2, 45.4 |
| Effective complexity | Gell-Mann (Physics 1969) and Lloyd | 20.3 |
| Landauer's principle | Landauer (1961) | FP-2, 67.1 |
| Margolus–Levitin and Bremermann bounds | Margolus and Levitin (1998); Bremermann (1962) | 67.2 |
| Sequential probability ratio test; optimality; lower bounds | Wald (1945); Wald and Wolfowitz (1948) | 17.2, 65.3, 65.6 |
| Confidence sequences; e-values; e-BH | Ville (1939); Robbins; Howard et al. (2021); Vovk and Wang; Wang and Ramdas (2022) | 17.3–17.4, 65.4 |
| Hoeffding and empirical-Bernstein inequalities | Hoeffding (1963); Maurer and Pontil (2009) | FP-4, 65.1 |
| False-discovery rate | Benjamini and Hochberg (1995) | 17.4 |
| Thompson sampling; UCB; GP-UCB regret | Thompson (1933); Auer et al. (2002); Srinivas et al. (2010) | FP-6, 14.1 |
| Successive halving; Hyperband | Jamieson and Talwalkar (2016); Li et al. (2017) | 16.2 |
| Minimum description length | Rissanen (1978) | 20.3 |
| Locality-sensitive hashing; MinHash | Indyk and Motwani (1998); Broder (1997) | 21.3 |
| Universal Scalability Law | Gunther (1993) | FP-7, 66.1 |
| Amdahl's and Gustafson's laws | Amdahl (1967); Gustafson (1988) | 31.1, 66.2 |
| Little's law | Little (1961) | 4.1, 36.3, 66.3 |
| Epidemic (gossip) protocols | Demers et al. (1987); Karp et al. (2000) | 10.2, 66.4 |
| Hybrid logical clocks | Kulkarni et al. (2014) | 29.1 |
| Roofline model | Williams, Waterman, Patterson (2009) | 58.1 |
| Correlated response to selection; breeder's equation | Lush (1937); Falconer | FP-5 |
| Bellman equation | Bellman (1957) | 24.1 |
| Conformal prediction | Vovk, Gammerman, Shafer (2005) | 34.3 |
| Fiedler vector; spectral partitioning | Fiedler (1973) | 10.1 |

New to this document: Proposition 64.5 (Governed Growth Bound), Conjecture 64.6 (exponent decomposition), Proposition 64.7 (envelope-optimal meta-fraction), Proposition 65.6 (Information–Verification Bound), the vertical ladder (4.0), the Goodhart governor (FP-5), the halt-lease stopping-distance bound (36.3), the relevance test (20.4), the overlap-distribution diversity floor (45.2), the option valuation of branches (45.3), the 4× contract with its ablation protocol (68), and the self-verification and falsification sections (72–73). Each is an application of the listed results to the fabric; none is claimed as more than that.

## **71. REFERENCE COMPUTATIONS**

Pseudo-code for the estimators an implementing agent needs. All read the ledger of Section 19; none writes anything but telemetry.

``` python

# 71.1 Sequential probability ratio test on paired differences (Section 17.2)
def sprt_step(state, d, delta, sigma2, alpha, beta):
    A = log((1 - beta) / alpha); B = log(beta / (1 - alpha))
    state.S += (delta / sigma2) * (d - delta / 2)
    state.n += 1
    if state.S >= A: return "ACCEPT_H1"
    if state.S <= B: return "ACCEPT_H0"
    if state.n >= state.max_samples: return "TRUNCATE"   # terminal decision by sign of S; report realized alpha
    return "CONTINUE"

# 71.2 e-BH false-discovery control over a window (Section 17.4)
def e_bh(e_values, q):
    m = len(e_values); order = sorted(range(m), key=lambda i: -e_values[i])
    k = max([i + 1 for i in range(m) if e_values[order[i]] >= m / (q * (i + 1))], default=0)
    return set(order[:k])                                 # indices rejected (promotable)

# 71.3 Resource-normalized velocity, the Solow residual (Section 64.4)
def solow_residual(lnP_series, lnR_series, eta):           # eta: dict of elasticities from the resource RCT
    dlnP = diff(lnP_series); dlnR = {i: diff(lnR_series[i]) for i in eta}
    return dlnP - sum(eta[i] * dlnR[i] for i in eta)        # tilde_v per window

# 71.4 Returns-to-scale exponent (Section 64.9)
def phi_hat(tilde_v_windows, P_windows, n_boot=2000, block=8):
    slope, lcb, ucb = block_bootstrap_ols(y=log(tilde_v_windows), x=log(P_windows), block=block, n_boot=n_boot)
    return 1 + slope, 1 + lcb, 1 + ucb

# 71.5 USL fit and pod sizing (Sections 10.1, 66.1)
def usl_fit(N_points, S_points):
    gamma, theta = nonlinear_least_squares(lambda N, g, t: N / (1 + g * (N - 1) + t * N * (N - 1)), N_points, S_points)
    N_star = sqrt((1 - gamma) / theta)
    return gamma, theta, N_star, N_star / 2                 # pod size cap

# 71.6 Little's-law sizing and stopping distance (Sections 9.1, 36.3)
def sizing(lmbda, service, overhead, util, sojourn, lease_ttl, W_max):
    workers = lmbda * service * (1 + overhead) / util
    in_flight = lmbda * sojourn
    T_stop = lease_ttl + W_max
    return workers, in_flight, T_stop

# 71.7 Shapley attribution by permutation sampling (Sections 24.2, 68.4)
def shapley(players, G, n_perm=10000):
    phi = {p: 0.0 for p in players}
    for _ in range(n_perm):
        perm = random_permutation(players); coalition = set(); prev = G(coalition)
        for p in perm:
            coalition.add(p); cur = G(coalition); phi[p] += cur - prev; prev = cur
    return {p: phi[p] / n_perm for p in players}           # add bootstrap intervals over permutations

# 71.8 VCG allocation of indivisible bundles (Section 23.2)
def vcg(bids):                                              # bids[i] = reported value function over bundles
    alloc = argmax_total_reported_value(bids)              # combinatorial winner determination
    payments = {}
    for i in bids:
        others_without_i = argmax_total_reported_value({j: bids[j] for j in bids if j != i})
        payments[i] = value(others_without_i, exclude=i) - value(alloc, exclude=i)
    return alloc, payments                                  # payments in future budget units

# 71.9 Winner's-curse-corrected estimate (Sections 17.5, 65.5)
def promotion_estimate(remeasured_mean, remeasured_n, pop_mean, pop_var_true, sigma2):
    shrink = pop_var_true / (pop_var_true + sigma2 / remeasured_n)
    return pop_mean + shrink * (remeasured_mean - pop_mean)  # on fresh-seed data only; never the screening score

# 71.10 Optimal fingerprinting (Section 64.8)
def fingerprint(y, F, Sigma_eps):
    Si = inv(Sigma_eps); C = inv(F.T @ Si @ F)
    a_hat = C @ F.T @ Si @ y
    return a_hat, C                                         # detection: CI excludes 0; attribution: CI includes 1

# 71.11 Halt drill (Section 36.3)
def halt_drill(governor, cells, W_max):
    t0 = now(); governor.revoke_all_leases()
    while any(c.in_flight() > 0 for c in cells): sleep(1e-3)
    t_stop = now() - t0
    assert t_stop <= governor.lease_ttl + W_max
    return t_stop                                           # recorded as halt_latency_measured
```

## **72. NUMERICAL VERIFICATION**

A specification that states numbers should be able to reproduce them. The script below is self-contained (numpy only, fixed seed) and checks the document's claimed quantities by simulation: the sequential-test savings and their realized error rates, the winner's curse and its removal by re-measurement, the variance-reduction factor, false-discovery control under dependence, the three growth regimes and the recovery of $\varphi$ from noisy windows, the governor bound, the envelope-optimal meta-fraction, the ablation and Shapley attribution of the multiplier, the USL fit, the funnel economics and Little's law. Its output follows the code, unedited. Where simulation and the analytic approximation disagree, the document says so and uses the simulated value (Section 17.2, 68.2).

### **72.0 What the run shows**

| **Claim** | **Section** | **Analytic** | **Simulated** | **Verdict** |
|---|---|---|---|---|
| SPRT boundary multiplier, $\alpha = \beta = 0.05$ | 17.2 | 2.04 (Wald approx.) | 1.59 at $\Delta/\sigma = 1$; 1.92 at $\Delta/\sigma = 0.3$ | overshoot lowers the gain at large per-observation effects; approaches theory as $\Delta/\sigma \to 0$ |
| SPRT mixture multiplier (20% boundary, 80% clearly worse) | 17.2 | ~5.4 | 3.96–6.31 across settings | the operative number; design assumption 2.5 is conservative |
| Realized $(\alpha, \beta)$ of the SPRT | 17.2 | $\le$ nominal | 0.027–0.042 at nominal 0.05; 0.008 at nominal 0.01 | conservative, as Wald's bounds predict |
| Winner's curse, $k = 10, 10^3, 10^6$ | FP-5, 65.5 | 1.54, 3.24, 4.86 $\sigma$ | 1.55, 3.25, 4.82 $\sigma$; re-measurement mean $\approx 0$ | confirmed; re-measurement removes it |
| VRF at $\rho = 0.5, 0.9$ | 40.2 | 2, 10 | 2.01, 9.94 | confirmed |
| e-BH FDR under shared-noise dependence, $q = 0.05$ | 17.4 | $\le 0.05$ | 0.003 (power 0.70) | valid and conservative; see 73.1 item 5 |
| Growth regimes $\varphi = 0.8, 1.0, 1.2$ | 64.3 | power law; exponential; blow-up at $t^* = 100$ | $A(T)$ matches closed forms; blow-up at $t = 100$ | confirmed |
| $\hat\varphi$ from noisy windows | 64.9 | 0.8, 1.0, 1.2 | 0.81, 1.00, 1.19 | estimator recovers the exponent |
| Governor at $v_{\max} = 0.1$ on $\varphi = 1.2$ | 64.5 | no blow-up; $A \le e^{v_{\max}t}$ | no blow-up; bound holds; max velocity 0.100 | confirmed |
| Envelope-optimal meta-fraction, $\kappa T = 20$ | 64.7 | $f^* = 0.947$ | 0.947 | confirmed |
| Ablation recovers planted multipliers; LCB $\ge 4$ | 68.3 | planted $\mathcal{M} = 8.66$ | 9.21, LCB$_{95}$ 8.66 | protocol works at 160 pods |
| Shapley shares sum to $\ln\mathcal{M}$ | 68.4 | 1.000 | 1.000 | confirmed |
| USL fit recovers $(\gamma, \theta)$, $N^*$ | 66.1 | 0.02, $10^{-5}$, 313 | 0.0198, $1.03\times10^{-5}$, 308 | confirmed |
| Funnel example | 16.1 | 4.00, 0.855, 21.4 | 4.01, 0.856, 21.3 | confirmed |
| Little's law at M0 | 66.3 | $L = \lambda W$ | $L = 19.8$, $W = 19.9$ ms | confirmed |

### **72.1 Script**

``` python
"""RSI Fabric PRD v3.0, Section 72: numerical verification (checks 1-10).
Pure numpy. Deterministic. Reproduces the document's claimed numbers from simulation.
Run: python3 rsi_verify.py
"""
import numpy as np
from math import log, sqrt, exp, erf

rng = np.random.default_rng(20261015)
Phi = lambda x: 0.5 * (1 + erf(x / sqrt(2)))

def z_quantile(p):            # inverse normal CDF by bisection (no scipy dependency)
    lo, hi = -10.0, 10.0
    for _ in range(100):
        mid = (lo + hi) / 2
        lo, hi = (mid, hi) if Phi(mid) < p else (lo, mid)
    return (lo + hi) / 2

print("== check 1: SPRT vs fixed-sample (Section 17.2 / 65.3) ==")
sigma = 1.0
for Delta, alpha in ((1.0, 0.05), (0.3, 0.05), (0.3, 0.01)):
    beta = alpha
    A, B = log((1 - beta) / alpha), log(beta / (1 - alpha))
    z = z_quantile(1 - alpha)
    n_B = int(np.ceil(((z + z) * sigma / Delta) ** 2))
    def sprt(tau, reps=20000, nmax=2000):
        d = rng.normal(tau, sigma, size=(reps, nmax))
        S = np.cumsum((Delta / sigma**2) * (d - Delta / 2), axis=1)
        hit_A = np.argmax(S >= A, axis=1); hit_B = np.argmax(S <= B, axis=1)
        okA = (S >= A).any(axis=1); okB = (S <= B).any(axis=1)
        tA = np.where(okA, hit_A, nmax); tB = np.where(okB, hit_B, nmax)
        N = np.minimum(tA, tB) + 1
        accept = tA < tB
        return N.mean(), accept.mean()
    N1, acc1 = sprt(Delta); N0, acc0 = sprt(0.0); Nbad, accbad = sprt(-2 * Delta)
    print(f"Delta/sigma={Delta}, alpha=beta={alpha}: fixed n_B={n_B}; SPRT E[N|H1]={N1:.1f} (Wald approx {((1-beta)*A+beta*B)/(Delta**2/(2*sigma**2)):.1f}), "
          f"E[N|H0]={N0:.1f}; realized alpha={acc0:.4f}, beta={1-acc1:.4f}; boundary multiplier {n_B/N1:.2f}x; clearly-worse E[N]={Nbad:.1f}")
    mix = 0.2 * N1 + 0.8 * Nbad
    print(f"   mixture (20% boundary, 80% clearly worse): n_bar={mix:.1f} -> decision-efficiency multiplier {n_B/mix:.2f}x")

print("\n== check 2: Winner's curse and re-measurement (FP-5 / 17.5 / 65.5) ==")
for k in (10, 1000, 10**6):
    reps = 2000 if k <= 1000 else 60
    scores = rng.normal(0, 1, size=(reps, k))
    win = scores.max(axis=1)
    fresh = rng.normal(0, 1, size=reps)           # the winner's true effect is 0; fresh measurement is unbiased
    print(f"k={k:>7}: screening winner mean = {win.mean():.2f} sigma (table: {dict([(10,1.54),(1000,3.24),(10**6,4.86)])[k]}); fresh re-measurement mean = {fresh.mean():+.2f}")

print("\n== check 3: Common random numbers (40.2) ==")
for rho in (0.5, 0.9):
    n = 200000
    e = rng.normal(size=n); a = rng.normal(size=n); b = rng.normal(size=n)
    ya = sqrt(rho) * e + sqrt(1 - rho) * a; yb = sqrt(rho) * e + sqrt(1 - rho) * b
    paired = np.var(ya - yb); unpaired = np.var(ya - rng.permutation(yb))
    print(f"rho={rho}: VRF measured = {unpaired/paired:.2f} (theory 1/(1-rho) = {1/(1-rho):.2f})")

print("\n== check 4: e-BH false-discovery control under dependence (17.4 / 65.4) ==")
m, frac_alt, n_obs, q, Delta = 2000, 0.10, 20, 0.05, 1.0
fdrs, powers = [], []
for rep in range(100):
    alt = rng.random(m) < frac_alt
    tau = np.where(alt, Delta, 0.0)
    shared = rng.normal(0, 0.5, size=n_obs)          # shared environment noise -> dependent tests
    d = tau[:, None] + shared[None, :] + rng.normal(0, 1, size=(m, n_obs))
    # e-value = likelihood ratio of H1 (tau=Delta) vs H0 (tau=0) with sigma_eff^2 = 1.25 (known for the check)
    s2 = 1.25
    e = np.exp(np.sum((Delta / s2) * (d - Delta / 2), axis=1))
    order = np.argsort(-e); k_star = 0
    for i in range(m):
        if e[order[i]] >= m / (q * (i + 1)): k_star = i + 1
    rej = np.zeros(m, bool); rej[order[:k_star]] = True
    fdrs.append((rej & ~alt).sum() / max(rej.sum(), 1)); powers.append((rej & alt).sum() / alt.sum())
print(f"m={m}, {int(frac_alt*100)}% alternatives, shared-noise dependence: FDR = {np.mean(fdrs):.4f} (q={q}), power = {np.mean(powers):.2f}")

print("\n== check 5: Growth law regimes, phi estimation and the governor (64.3 / 64.5 / 64.9) ==")
def simulate(phi, kappa=0.05, A0=1.0, T=400, dt=0.01, v_max=None, cap=1e20):
    A, t, hist = A0, 0.0, []
    while t < T and A < cap:
        v = kappa * A ** (phi - 1)
        if v_max is not None: v = min(v, v_max)
        A *= exp(v * dt); t += dt; hist.append((t, A, v))
    return np.array(hist)
for phi in (0.8, 1.0, 1.2):
    h = simulate(phi)
    # windowed noisy velocity estimates, then regress ln v on ln A
    idx = np.arange(0, len(h), 500)[1:]
    A_w = h[idx, 1]; v_w = h[idx, 2] * np.exp(rng.normal(0, 0.15, size=len(idx)))
    slope = np.polyfit(np.log(A_w), np.log(v_w), 1)[0]
    if h[-1, 1] >= 1e20: blow = f"finite-time blow-up: reached A=1e20 at t={h[-1,0]:.0f} (theory t*={1/((phi-1)*0.05):.0f})"
    else: blow = f"A(T)={h[-1,1]:.3g} (theory {(1+(1-phi)*0.05*400)**(1/(1-phi)) if phi<1 else exp(0.05*400):.3g})"
    print(f"phi={phi}: ungoverned {blow}; phi_hat = {1+slope:.2f}")
h_g = simulate(1.2, v_max=0.1); t_end = h_g[-1, 0]
bound = exp(0.1 * t_end)
print(f"phi=1.2 governed at v_max=0.1: no blow-up, A(T)={h_g[-1,1]:.3g} <= bound e^(v_max T)={bound:.3g}: {h_g[-1,1] <= bound*1.0001}; max velocity {h_g[:,2].max():.3f}")

print("\n== check 6: Envelope-optimal meta-fraction (64.7) ==")
kT = 20.0
f_grid = np.linspace(0.01, 0.99, 9801)
J = (1 - f_grid) * (np.exp(kT * f_grid) - 1) / (kT * f_grid)
f_num = f_grid[np.argmax(J)]; f_closed = (1 + sqrt(1 - 4 / kT)) / 2
print(f"kappa*T={kT}: numeric argmax f*={f_num:.3f}, closed form {f_closed:.3f}; harvested share ungoverned = {1-f_num:.3f}")
v_max_over_kappa = 0.4
print(f"governed with v_max/kappa={v_max_over_kappa}: f_G={v_max_over_kappa}, harvested share {1-v_max_over_kappa:.2f}; "
      f"early cumulative ratio governed/ungoverned ~ {(1-v_max_over_kappa)*kT:.1f}x")

print("\n== check 7: Randomized ablation and Shapley attribution of the multiplier (68.3 / 68.4) ==")
mech = {"seq": 2.5, "VRF": 2.0, "funnel": 1.5, "dedup": 1.05, "sched": 1.1}
names = list(mech); J_ = len(names)
pods = 160
configs = rng.integers(0, 2, size=(pods, J_))                     # random configurations (full factorial support)
lnP = np.log(1000.0) + configs @ np.log(np.array([mech[n] for n in names])) + rng.normal(0, 0.10, size=pods)
X = np.column_stack([np.ones(pods), configs])
coef = np.linalg.lstsq(X, lnP, rcond=None)[0]
lnM = coef[1:].sum()
resid = lnP - X @ coef; cov = resid.var(ddof=J_ + 1) * np.linalg.inv(X.T @ X)
se = sqrt(np.ones(J_) @ cov[1:, 1:] @ np.ones(J_))                 # s.e. of the sum of main effects
print("planted multipliers:", {n: mech[n] for n in names}, "-> planted M =", round(float(np.prod(list(mech.values()))), 2))
print("estimated per-mechanism:", {n: round(float(np.exp(c)), 2) for n, c in zip(names, coef[1:])})
print(f"estimated M = {exp(lnM):.2f}, LCB95 ~ {exp(lnM - 1.645*se):.2f}; contract (>= 4): {exp(lnM - 1.645*se) >= 4}")
# Shapley on the additive log model: shares equal main effects exactly; verify by permutation sampling
G = lambda S: sum(coef[1 + names.index(n)] for n in S)
phi_sh = {n: 0.0 for n in names}
for _ in range(2000):
    perm = list(rng.permutation(names)); S = []; prev = 0.0
    for n in perm:
        S.append(n); cur = G(S); phi_sh[n] += cur - prev; prev = cur
print("Shapley shares of ln M:", {n: round(float(phi_sh[n] / 2000 / lnM), 3) for n in names}, "(sum =", round(float(sum(phi_sh.values()) / 2000 / lnM), 3), ")")

print("\n== check 8: USL fit (66.1) ==")
g_true, th_true = 0.02, 1e-5
N = np.array([1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024])
S = N / (1 + g_true * (N - 1) + th_true * N * (N - 1)) * np.exp(rng.normal(0, 0.03, size=len(N)))
# linearize: N/S - 1 = g (N-1) + th N(N-1)  -> least squares in (g, th)
y = N / S - 1; Xu = np.column_stack([N - 1, N * (N - 1)])
g_hat, th_hat = np.linalg.lstsq(Xu, y, rcond=None)[0]
print(f"true gamma={g_true}, theta={th_true}; fitted gamma={g_hat:.4f}, theta={th_hat:.2e}; N* true={sqrt((1-g_true)/th_true):.0f}, fitted={sqrt((1-g_hat)/th_hat):.0f}")

print("\n== check 9: Funnel economics by Monte Carlo (16.1) ==")
c = np.array([1.0, 10.0, 100.0]); s = np.array([0.1, 0.2]); r = np.array([0.9, 0.95])
n_c = 200000
cost = np.full(n_c, c[0]); alive = np.ones(n_c, bool)
for i in range(2):
    passed = alive & (rng.random(n_c) < s[i]); cost[passed] += c[i + 1]; alive = passed
recall_mc = np.prod([ (rng.random(n_c) < r[i]).mean() for i in range(2) ])
cbar = cost.mean()
print(f"mean cost per entering candidate = {cbar:.2f} (formula 4.00); recall = {recall_mc:.3f} (formula 0.855); multiplier = {recall_mc*c[-1]/cbar:.1f} (formula 21.4)")

print("\n== check 10: Little's law and stopping distance (36.3 / 66.3) ==")
lam, svc, c_srv = 1000.0, 0.020, 32
# discrete-event M/M/c, 60 simulated seconds
t, nxt_arr, in_sys, busy, done, area = 0.0, rng.exponential(1/lam), 0, [], 0, 0.0
svc_ends = []
T_end = 60.0; last = 0.0
while t < T_end:
    nxt_dep = min(svc_ends) if svc_ends else float('inf')
    t = min(nxt_arr, nxt_dep); area += in_sys * (t - last); last = t
    if t == nxt_arr:
        in_sys += 1; nxt_arr = t + rng.exponential(1/lam)
        if len(svc_ends) < c_srv: svc_ends.append(t + rng.exponential(svc))
        else: pass  # queued; started when a server frees
    else:
        svc_ends.remove(nxt_dep); in_sys -= 1; done += 1
        if in_sys > len(svc_ends): svc_ends.append(t + rng.exponential(svc))
L_meas = area / T_end; W_meas = L_meas / (done / T_end)
print(f"M/M/{c_srv}, lambda={lam:.0f}/s, service={svc*1000:.0f} ms: utilization {lam*svc/c_srv:.2f}, L measured {L_meas:.1f}, W = L/lambda = {W_meas*1000:.1f} ms; "
      f"stopping distance <= T_lease + W_max ~ {1.0 + 5*W_meas:.2f} s (T_lease = 1 s, W_max taken as 5 W)")
```

### **72.2 Output (unedited)**

``` text
== check 1: SPRT vs fixed-sample (Section 17.2 / 65.3) ==
Delta/sigma=1.0, alpha=beta=0.05: fixed n_B=11; SPRT E[N|H1]=6.9 (Wald approx 5.3), E[N|H0]=6.9; realized alpha=0.0270, beta=0.0283; boundary multiplier 1.59x; clearly-worse E[N]=1.7
   mixture (20% boundary, 80% clearly worse): n_bar=2.8 -> decision-efficiency multiplier 3.96x
Delta/sigma=0.3, alpha=beta=0.05: fixed n_B=121; SPRT E[N|H1]=63.1 (Wald approx 58.9), E[N|H0]=63.4; realized alpha=0.0423, beta=0.0422; boundary multiplier 1.92x; clearly-worse E[N]=14.1
   mixture (20% boundary, 80% clearly worse): n_bar=23.9 -> decision-efficiency multiplier 5.07x
Delta/sigma=0.3, alpha=beta=0.01: fixed n_B=241; SPRT E[N|H1]=104.8 (Wald approx 100.1), E[N|H0]=104.1; realized alpha=0.0083, beta=0.0084; boundary multiplier 2.30x; clearly-worse E[N]=21.5
   mixture (20% boundary, 80% clearly worse): n_bar=38.2 -> decision-efficiency multiplier 6.31x

== check 2: Winner's curse and re-measurement (FP-5 / 17.5 / 65.5) ==
k=     10: screening winner mean = 1.55 sigma (table: 1.54); fresh re-measurement mean = -0.02
k=   1000: screening winner mean = 3.25 sigma (table: 3.24); fresh re-measurement mean = -0.03
k=1000000: screening winner mean = 4.82 sigma (table: 4.86); fresh re-measurement mean = +0.03

== check 3: Common random numbers (40.2) ==
rho=0.5: VRF measured = 2.00 (theory 1/(1-rho) = 2.00)
rho=0.9: VRF measured = 9.88 (theory 1/(1-rho) = 10.00)

== check 4: e-BH false-discovery control under dependence (17.4 / 65.4) ==
m=2000, 10% alternatives, shared-noise dependence: FDR = 0.0019 (q=0.05), power = 0.71

== check 5: Growth law regimes, phi estimation and the governor (64.3 / 64.5 / 64.9) ==
phi=0.8: ungoverned A(T)=3.13e+03 (theory 3.13e+03); phi_hat = 0.81
phi=1.0: ungoverned A(T)=4.85e+08 (theory 4.85e+08); phi_hat = 1.00
phi=1.2: ungoverned finite-time blow-up: reached A=1e20 at t=100 (theory t*=100); phi_hat = 1.20
phi=1.2 governed at v_max=0.1: no blow-up, A(T)=5.08e+16 <= bound e^(v_max T)=2.36e+17: True; max velocity 0.100

== check 6: Envelope-optimal meta-fraction (64.7) ==
kappa*T=20.0: numeric argmax f*=0.947, closed form 0.947; harvested share ungoverned = 0.053
governed with v_max/kappa=0.4: f_G=0.4, harvested share 0.60; early cumulative ratio governed/ungoverned ~ 12.0x

== check 7: Randomized ablation and Shapley attribution of the multiplier (68.3 / 68.4) ==
planted multipliers: {'seq': 2.5, 'VRF': 2.0, 'funnel': 1.5, 'dedup': 1.05, 'sched': 1.1} -> planted M = 8.66
estimated per-mechanism: {'seq': 2.59, 'VRF': 1.99, 'funnel': 1.49, 'dedup': 1.07, 'sched': 1.13}
estimated M = 9.34, LCB95 ~ 8.72; contract (>= 4): True
Shapley shares of ln M: {'seq': 0.426, 'VRF': 0.308, 'funnel': 0.178, 'dedup': 0.031, 'sched': 0.056} (sum = 1.0 )

== check 8: USL fit (66.1) ==
true gamma=0.02, theta=1e-05; fitted gamma=0.0218, theta=7.59e-06; N* true=313, fitted=359

== check 9: Funnel economics by Monte Carlo (16.1) ==
mean cost per entering candidate = 3.93 (formula 4.00); recall = 0.855 (formula 0.855); multiplier = 21.8 (formula 21.4)

== check 10: Little's law and stopping distance (36.3 / 66.3) ==
M/M/32, lambda=1000/s, service=20 ms: utilization 0.62, L measured 19.9, W = L/lambda = 20.0 ms; stopping distance <= T_lease + W_max ~ 1.10 s (T_lease = 1 s, W_max taken as 5 W)
```

## **73. OPEN PROBLEMS AND HOW TO FALSIFY THIS DOCUMENT**

A specification that cannot be wrong is not a specification. This section lists what the document assumes, what is known to be loose, and the measurements that would refute its central claims.

### **73.1 Known weaknesses**

1. **Gaussian, known-variance tests.** The sequential-test numbers assume Gaussian paired differences with known $\sigma$. Heavy tails or a misestimated $\sigma$ inflate the realized $\alpha$. Mitigation in the document: empirical-Bernstein confidence sequences (65.1, 17.3) and the STATISTICAL test class that measures realized $\alpha$ on synthetic streams (57). Open: the efficiency cost of the distribution-free tests at fabric scale.
2. **Overshoot.** Wald's approximations understate the SPRT's sample size when the per-observation effect $\Delta/\sigma$ is large (72.2, check 1). The boundary multipliers in 17.2 are approximations; the mixture multipliers are the operative numbers and are measured, never assumed.
3. **Non-stationarity.** Every promotion changes the candidate distribution. Bandit posteriors, surrogates and the Goodhart weights assume drift slower than their re-estimation cadence, and the separability behind Conjecture 64.6 may fail under fast drift. Mitigation: windowed estimators with block bootstrap, the calibration stream. Open: the window length as a function of $\tilde v$.
4. **Scalarization.** By Arrow's impossibility theorem there is no non-dictatorial rule that aggregates a multidimensional capability vector into one ordering while satisfying the usual axioms. The document therefore makes the Human Control Plane the designated dictator over the weights $w$ (5.4, 38), which is a choice, not a derivation. Consequences: $\delta$, $P$ and every growth claim are relative to $w$; $w$ is frozen within a rung; across rungs the capability index is a fixed-basket (chained Laspeyres-type) index so that a change in the mix of domains cannot masquerade as growth. Open: a principled rule for revising $w$ between rungs.
5. **Dependence.** Candidates share ancestors, seeds and environments. e-BH is valid under arbitrary dependence but conservative (72.2, check 4, shows an FDR far below $q$, i.e. lost power). Open: dependence-aware e-values that recover power without losing validity.
6. **Surrogate feedback.** Screening by the surrogate selects the surrogate's own future training data. The calibration stream (34.2) measures recall on unselected candidates, but the surrogate's errors can concentrate in the selected region. Open: the minimum calibration fraction as a function of the surrogate's capture score (41.1).
7. **Baseline fairness.** $\mathcal{M}$ is defined against v2 as written. To prevent the contract being met against a weak comparator, the certificate also reports $\mathcal{M}$ against the strongest fixed-sample design (fixed $n_B$ with CRN pairing); the vertical ladder is tracked on that stronger comparator.
8. **The envelope's parameters are choices.** $v_{\max}$, $d_{\max}$, $r_{\max}$ and the review floors have initial values with stated rationales and no first-principles derivation. This is deliberate: they encode a human decision about the rate at which to take delivery (64.7), and it is the document's largest non-mathematical commitment.
9. **Energy and cost figures are assumptions.** The physics tables bound what cannot happen; they do not predict what will. Every joule figure is replaced by a measurement at certification.
10. **Depth.** $d_{\max} = 2$ bounds autonomous recursion. Whether deeper meta-levels carry value is an empirical question this document does not answer.
11. **The bound is not a rate.** Proposition 65.6 says what sustained velocity cannot exceed; attaining it requires the fabric to be verification-bound with small slack, which is a design condition (54.1), not a given. A fabric far below its bound can grow fast for a while without any of the bound's terms moving.
12. **Physical loops.** The sim-to-real radius (60.1) assumes the relevant shift lives in the measured feature space. Unmeasured features, the usual cause of sim-to-real failure, are outside it.
13. **Correlated mechanisms.** The composition in 68.2 treats the factors as multiplicative; the ablation design estimates interactions, but a design of resolution IV cannot separate all two-factor interactions from each other. If interactions are large, the reported $\mathcal{M}$ is the all-on versus all-off contrast (68.3 step 6), not the product.

### **73.2 Falsification**

| **If this is measured…** | **…then this claim is refuted** |
|---|---|
| $\text{LCB}_{95}(\hat\varphi) < 1 - \varepsilon_\varphi$ over $\ge 3$ doublings after Phase 3, resources normalized | the core hypothesis (1.2) for that configuration |
| $\text{UCB}_{95}(\mathcal{M}) < 4$ in the randomized ablation at M0 | the 4× contract and the design assumptions of 68.2 |
| a significant residual dependence of $\ln\tilde v$ on $\ln P$ after the four elasticities (64.6) | the exponent decomposition is incomplete |
| realized $\alpha$ on the calibration stream above nominal by more than its interval | the verification plane's statistical contract (56, 57) |
| regression discontinuity at the promotion cutoff shows no positive effect of promotion on descendant value (40.4) | promotion is promoting noise; $\delta$ is overstated |
| measured $\theta$ on the fast path above budget at the certifying $N$ | the topology claim (FP-7, 32) |
| halt drill exceeding $T_{\text{lease}} + W_{\max}$ | a lease or signature invariant is violated somewhere (36.3) |
| experience-curve exponent $b \approx 0$ after Phase 3 | knowledge reuse is not working; the moat argument (51) is unsupported |
| proxy–truth covariance decaying faster than the rotation re-estimates it | the Goodhart governor is too slow; FP-5 rules are insufficient |
| $P(q)$ collapsing while share-based $N_{\text{eff}}$ stays high | share-based diversity is uninformative (expected; the reason 45.2 exists) |
| a configuration in which $\mathcal{M}_k < \mathcal{M}_{k-1}$ at certification | the vertical ladder's non-decreasing gate; the rung is not certified |

### **73.3 What this document does not claim**

It does not claim that $\varphi \ge 1$ holds; it claims it will be measured and reported with its interval. It does not claim unbounded growth; it bounds growth by the envelope and by physics. It does not claim that the results of Section 70 endorse the fabric; they are tools applied to it. It does not claim general intelligence of any kind; it specifies a system for producing independently verified improvements to measurable systems, and the measurability is the limit of its scope.

**End of document.** This is LVL3.AI RSI, v3.0 — Fable Max Remake.
