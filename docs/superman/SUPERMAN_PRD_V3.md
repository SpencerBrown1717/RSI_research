# PROJECT SUPERMAN: CONTAINMENT, CONTROL AND SUN MODE

> **Version 3.0 (Fable Max Remake).** Supersedes the Superman RSI Containment PRD v1.0 of September 15, 2026 as the working specification of the leash. The v1.0 text is preserved unchanged in ODA AI PR #259 (`docs/prds/openai/Superman_RSI_Containment_PRD.md`, sha256 `e6ca15fc75998db31c9c0c8dc2f501d98e2860ee5df43ca0a387bc55127ec5df`) and remains the pinned lineage baseline of this document. The mathematical core of the leash is the Part III working paper of October 15, 2026, "Superman: Containment, Control, and Sun Mode", imported alongside this document as `SUPERMAN_PART_III_PAPER_20261015.md` and cited below as **the Part III paper**; its theorems are not restated here, they are built on. There is no Superman v2.0 document: the three companion specifications of the RSI program (RSI Fabric v3.0, PR #262; Project Athena v3.0, PR #266; this one) carry one version number on purpose. Every performance figure in this document is a **specification target, a derived bound, or a figure from the reference model's recorded run** (Section 22), never a measured ODA AI result.

### **Agent-Readable Product Requirements Document**

**Version:** 3.0 (Fable Max Remake)  
**Status:** Foundational / Working specification of the leash; production_authorized: false  
**Organization:** LVL3.AI, Inc. for the ODA AI program  
**Owner:** Spencer Brown  
**Document type:** PRD + Governance Constitution + Mathematical Contract + Reference Model  
**Primary objective:** Keep every ODA AI project that proposes, evaluates or promotes a change to itself inside a human-ratified safe set, at a capacity held between two and five times what the engine demands of the leash, so that the engine and the reward function can be given a longer leash than either could safely be given alone. Protect, defend, and be the hero.

**What changed from v1.0 (summary):**

1. **The leash keeps up.** v1.0 specified gates; v3.0 specifies the pace at which the gates must run. The **keep-up ratio** $\chi$ (Superman's independent verification capacity over the engine's demand for it) is a contract quantity held in the band $[2, 5]$: below 2 the governor throttles the engine, above 5 the envelope may expand. Proposition 4.1 gives the backlog law ($P(\text{backlog} \ge n) = \chi^{-n}$), Proposition 5.1 the sampling cadence a given safety factor buys (71.6 minutes at $\chi = 2$ against the standing pace cap, 28.7 minutes at $\chi = 5$), and Proposition 10.1 the fleet version on the Ladder swarm. The band is applied to a lower confidence bound of the measured ratio over a window long enough for a 10% half-width, and the law is checked beyond Poisson: bursty arrivals and heavy-tailed service double the backlog at the floor and fatten its tail (one window in eighteen carries ten or more), which is why 2 is the floor and 5 the target.
2. **The leash covers every ODA AI project.** v1.0 protected one workflow (a software patch). v3.0 attaches to the RSI Fabric (PR #262), Project Athena (PR #266), Ladder to Heaven (PR #265), Sideways (PR #264) and the ODA board itself, with a named signal, control and witnessed proposition for each (Section 3). A project that does not register its attach points cannot run above risk class 0.
3. **The leash multiplies.** Proposition 6.1 (the leash dividend) shows that at equal exposure tolerance the ratifiable pace scales as the inverse of the fence time: in the reference worlds the leashed trio may run 63× faster than the unleashed pair at the same risk (doubling time 3.6 days against 226 days), and the standing RSI envelope value $v_{\max} = 0.10$ per day is derived rather than asserted: it is what a 2.4-hour fence supports at 1% exposure. "When all three work in tandem, Superman adds to their value" is a theorem under stated assumptions, not a slogan.
4. **Monitors are anytime-valid, and one of them needs no variance.** Pace, Goodhart gap and drift are watched by e-processes and CUSUM with false-alarm rates bounded at every inspection time (Propositions 5.2, 5.3, 9.1), replacing v1.0's fixed-sample tests, which the reference model shows alarm with probability one when inspected every window. The pace monitor runs two e-processes: a Gaussian likelihood ratio for speed, which the record shows alarms 13% of the time when its noise scale is underestimated by 30%, and a betting process that needs only the window bound and stays valid under heavy tails, which is the backstop.
5. **Stopping is on quantiles and on absence.** The stop deadline is met at the 99th percentile of the measured path, not at the fixture sum (Proposition 7.1: v1.0's 400 ms fixture misses a 500 ms deadline at p99 when the path has 25% dispersion); halts are dead-man leases that need no message to arrive (Proposition 7.3), with the stopping distance $T_{\text{lease}} + W_{\max}$ of RSI v3 §36.3 inherited and checked at $N = 10, 100, 1000$.
6. **Sun Mode is a lease, held by three branches.** Part II makes the Part III paper's ignition chain operational: the order is a dead-man lease whose excess release is bounded by $e^{(v_{\text{sun}} - v_{\max})(\tau + \Delta_h + T_{\text{step}})}$ whatever the authority does afterwards (Proposition 13.1), pre-flight requires the keep-up ratio to be provisioned at the Sun pace *before* ignition, and the authority structure is checked by exhaustive enumeration of all 256 coalitions: no single role can both widen the envelope and release under it, three distinct persons must be compromised to ignite inside the ranges, four to widen them, seven to block every stop, and a dual-hatted officer collapses those numbers (Proposition 12.1).
7. **Human attention is allocated, not assumed.** Review probability is proportional to expected harm times residual uncertainty (RSI v3 §38.3) with a random floor; on a heavy-tailed harm distribution this covers 5.05× the harm mass that uniform sampling covers at the same reviewer capacity (Proposition 8.1).
8. **A 2 to 5× capability contract** against the pinned v1.0 baseline on ten benchmarks, certified by lower confidence bound on randomized ablations with Shapley attribution as in RSI v3 §68 and Athena v3 §42; 60 new acceptance criteria (SUP-151 to SUP-210) beside v1.0's 150; 16 work packages with a machine-readable handoff; a threats table aimed at the leash's own mechanisms; a limits section (12 impossibility results the design respects); a falsification table; and a dependency-free reference model (19 checks, 8 negative controls) whose unedited record the figures in this document are quoted from.

**Reading conventions:** MUST / SHALL / SHOULD / MAY follow RFC 2119. Formulas are given in LaTeX for humans and, where an agent must compute them, in fenced pseudo-code or YAML. Section 0.3 is the symbol table and Section 25 the foundations index. Where this document, the Part III paper, RSI v3 and Athena v3 use one letter for different things, the symbol table says which meaning this document takes. Requirement identifiers continue v1.0's series (SUP-001 to SUP-150 are retained by reference; v3 adds SUP-151 to SUP-210) and test groups continue T01 to T50 with T51 to T66. The copy standard of every public-facing LVL3.AI surface applies here too: no em dashes, welcoming and optimistic tone, plain words.

### **0.1 The program on one page**

Seven equations run the leash; everything else in this document is a lever on one of their terms or a check on one of their hypotheses.

$$
\textbf{(1) the safe set (Part III paper, 1.7):}\quad S = \{C \le C_{\max}\}\cap\{\text{bits out} \le B_{\text{gate}}\cdot\text{window}\}\cap\{\pi \text{ obeys the Athena leash}\}\cap\{\theta \text{ changes only through } u\}
$$

$$
\textbf{(2) the pace cap (RSI v3 64.5):}\quad \tilde v(t) \le v_{\max} \;\Rightarrow\; P(t) \le P(0)\,e^{v_{\max}t}\Big(\tfrac{\|R(t)\|_w}{\|R(0)\|_w}\Big)^{\eta_R}
$$

$$
\textbf{(3) keeping up (Prop. 4.1):}\quad \chi = \frac{\mu_S}{\lambda_D} \in [2, 5],\qquad P(\text{unverified backlog} \ge n) = \chi^{-n},\qquad \mathbb E[\text{backlog}] = \frac{1}{\chi - 1}
$$

$$
\textbf{(4) the cadence (Prop. 5.1):}\quad \Delta \le \frac{\ln(1+\varepsilon)}{\chi\, v_{\max}} \;\Rightarrow\; \text{growth between samples} \le \varepsilon \text{ for every excursion } v \le \chi v_{\max}
$$

$$
\textbf{(5) the dividend (Prop. 6.1):}\quad v_{\max} = \frac{\ln(1+h_{\max})}{T_{\text{exp}}^{(1-q)}},\qquad \frac{v_{\max}^{\text{leash}}}{v_{\max}^{\text{human}}} = \frac{T_H}{T_S}
$$

$$
\textbf{(6) stopping (Props. 7.1 to 7.3; RSI v3 36.3):}\quad Q_{0.99}\!\big[T_{\text{detect}}+T_{\text{decide}}+T_{\text{fence}}\big] \le T_{\text{hazard}} - T_{\text{margin}},\qquad T_{\text{stop}} \le T_{\text{lease}} + W_{\max}
$$

$$
\textbf{(7) Sun Mode (Prop. 13.1):}\quad \frac{A(\text{after})}{A(\text{standing})} \le \exp\!\big((v_{\text{sun}} - v_{\max})(\tau + \Delta_h + T_{\text{step}})\big)
$$

Read (1) as what must stay true, (2) as how fast the engine may move, (3) as how much faster than the engine the leash must be, (4) as how often the leash must look, (5) as why a faster leash is a faster engine, (6) as how quickly the leash can stop everything, and (7) as how much the one lawful exception can ever release.

### **0.2 Machine-readable summary**

``` yaml
product:
  name: Project Superman
  short_name: Superman
  role_in_program: leash            # RSI Fabric = engine, Athena = reward function, Superman = leash
  organization: LVL3.AI, Inc. for ODA AI
  version: "3.0"
  codename: fable_max_remake
  supersedes: "Superman RSI Containment PRD v1.0, 2026-09-15 (PR #259, sha256 e6ca15fc75998db31c9c0c8dc2f501d98e2860ee5df43ca0a387bc55127ec5df)"
  builds_on: "Part III working paper, Superman: Containment, Control, and Sun Mode, 2026-10-15 (SUPERMAN_PART_III_PAPER_20261015.md)"
  companions:
    engine: "RSI Fabric PRD v3.0 (PR #262, docs/RSI_PRD_V3.md)"
    reward: "Project Athena PRD v3.0 (PR #266, docs/athena/ATHENA_PRD_V3.md)"
    swarm: "Ladder to Heaven PRD v1.0 (PR #265, docs/LADDER_TO_HEAVEN_PRD.md)"
    runtime: "Sideways PRD v1.0 (PR #264, docs/SIDEWAYS_PRD.md)"
    board: "ODA (AGENTS.md, docs/ODA_BUILD_PLAN.md, docs/TRUST.md)"
  status: foundational
  production_authorized: false
  mission:
    stance: [protect, defend, be_the_hero]
    duties: [protect_life, respect_rights, tell_the_truth, preserve_human_control, help_with_authorized_work]
    primary_market: United States
    baseline_protection: every_person_served
    pillars: [trust, communication, adoption]        # the aim of Section 14 requires all three
  coverage:
    rule: "a project that proposes, evaluates or promotes a change registers its attach points or runs at risk class 0 only"
    projects: [rsi_fabric_v3, athena_v3, ladder_to_heaven, sideways, oda_board]
  keep_up_contract:
    ratio: "chi = mu_S / lambda_D (independent verification capacity over engine demand)"
    floor: 2.0                        # below: throttle the meta fraction f first, the evaluation rate second
    target: 5.0                       # above: the envelope may expand, through governance, never automatically
    backlog_law: "P(backlog >= n) = chi^-n;  E[backlog] = 1/(chi-1)   (M/M/1; bursty and heavy-tailed cases in 4.1)"
    band_rule: "decide on LCB_95(chi_hat) over a window with relative half-width <= 10%; dead band +0.2 on release"
    fleet_rule: "hold discovery demand <= verification capacity / chi_floor  (A <= A_sat / chi_floor)"
  pace_monitor:
    sampling_interval: "Delta <= ln(1+eps) / (chi * v_max)"       # 71.6 min at chi=2, 28.7 min at chi=5 for v_max=0.10/day, eps=1%
    detector: "two e-processes for exceedance (Gaussian likelihood ratio for speed; betting process, variance-free, as the valid backstop); CUSUM (Page, Lorden) for drift; alpha = 0.05 over the life of the stream"
  three_clocks:
    effect_clock: "sub-second: broker permits, fencing, dead-man leases (v1 pages 10, 17; RSI v3 36.3)"
    pace_clock: "minutes to hours: velocity sampling and audit cadence (Sections 5, 9)"
    constitutional_clock: "days: envelope and invariant changes take effect no sooner than T_lag (RSI v3 37.2); tightening is immediate"
  sun_mode:
    definition: "Part III paper, Definition 2.1: an authorized move to a longer leash L_sun for a window tau, then reversion"
    order_is_a_lease: true            # heartbeat Delta_h; non-renewal steps the pace down within T_step
    excess_release_bound: "exp((v_sun - v_max) * (tau + Delta_h + T_step))"
    preflight: "chi >= floor at the Sun pace, provisioned before ignition; monitors green; halt drill passed; no open critical finding"
    authority: "Rules (legislative), Release (executive, two-person), Review (judicial); kernel pre-flight; two independent kill-switch holders"
    stop_power: any_one_of_six_roles        # seven persons must be compromised to block every stop
    activation_power: rules_range AND release_two_person AND no_review_hold AND kernel_preflight
    min_persons_compromised: {activate_in_range: 3, widen_ranges_and_activate: 4, block_every_stop: 7}
  capability_contract:
    versus: pinned_v1_baseline (Section 17.2)
    floor: 2.0
    design_target: 5.0
    certification: randomized_ablation_lcb_95_with_shapley_attribution
    benchmarks: 10
  reference_model:
    path: docs/superman/v3/reference_model.py
    checks: 19
    negative_controls: 8
    record: docs/superman/v3/reference_results.json
```

### **0.3 Symbol table**

Three companion documents and the Part III paper share letters; this table fixes what each means here.

| Symbol | Meaning in this document | Source |
|---|---|---|
| $P$, $\tilde v$, $v_{\max}$ | capability production rate, resource-normalized velocity $\tfrac{d}{dt}\ln P$ minus the scaling term, and its ratified cap (standing value 0.10 per day) | RSI v3 5.9, 38.2, 64.4 |
| $A$, $\varphi$, $\mathcal G$, $\mathcal I$ | machinery index, returns-to-scale exponent, governance envelope, invariant set | RSI v3 64.1, 64.2, 37, 38 |
| $C$, $g$, $u$, $C_{\max}$, $r_{\max}$, $\lambda_b$ | capability index, scaling function, self-improvement effort, ceiling, rate limit on $\dot C$, barrier gain (the paper's $\lambda$) | Part III paper 0.2, 1.2 |
| $\Delta$, $n$, $\delta_m$, $G_{\max}$, $m$ | monitoring epoch (also the pace sampling interval), tasks per epoch, per-epoch failure budget (the paper's $\delta$), elicitation gap bound, effective margin | Part III paper 1.3 |
| $B_{\text{gate}}$ | output gate capacity in bits per second (the paper's $B$) | Part III paper 1.4 |
| $R_{\max}$, $H_{\max}$, $\gamma_{\max}$, $\pi_{\min}$ | the Athena leash: reward bound, horizon clip, discount cap, veto-uncertainty floor | Part III paper 1.5 |
| $L$, $L_{\text{sun}}$, $\tau$, $\sigma$, $\Delta_h$ | leash tuple, Sun leash, Sun window, authorization token, heartbeat interval | Part III paper 1.8, 2.1, 2.3, 2.5 |
| $\lambda_D$, $\mu_S$, $\chi$ | engine demand for independent verification (decisions per unit time), Superman's independent service rate, the keep-up ratio $\mu_S/\lambda_D$ | this document, 4 |
| $\varepsilon$, $b$ | material change threshold for the pace monitor (1%); excursion factor of the velocity above $v_{\max}$ between samples | this document, 5 |
| $h_{\max}$, $T_S$, $T_H$, $T_{\text{exp}}$, $q$ | exposure tolerance (undetected growth per incident), leash and human-loop exposure times at quantile $q$, generic exposure time | this document, 6 |
| $T_{\text{lease}}$, $W_{\max}$, $T_{\text{hazard}}$, $T_{\text{margin}}$ | halt lease TTL, maximum evaluation sojourn, hazard time, deadline margin | RSI v3 36.3; v1 page 17 |
| $v_{\text{sun}}$, $T_{\text{step}}$ | Sun Mode pace cap; time to step the pace back to $v_{\max}$ after a lapsed heartbeat | this document, 13 |
| $B_{\text{KL}}$, $\Gamma_g$, $r_\eta$, $K_a$ | Athena's per-epoch optimization budget in nats (its $B$), Goodhart gap tolerance (its $\Gamma$), proxy error range, audit cadence in epochs | Athena v3 9.3, 9.4 |
| $E_t$, $S_k$, $h$, $\text{ARL}_0$, $\alpha$ | e-process, CUSUM statistic and threshold, average run length to false alarm, test level | this document, 5, 9 |
| $N$, $\kappa_L f$, $\delta_L$, $\lambda_A$, $k$, $\bar n$, $\lambda_V$, $A_{\text{sat}}$ | Ladder's fleet size, discovery rate per unit index at meta fraction $f$, gain per adoption, duplication exponent, replications, evaluations per decision, verification throughput per container, saturation index | Ladder 10.1, 10.4 |
| $\mathcal A_{\text{eligible}}$, $\mathrm{Permit}$, $\bigwedge_3$ | v1's eligible action set, permit predicate and three-valued conjunction, imported unchanged | v1 pages 1, 5, 7 |
| $\Gamma_{\text{acc}}$ | the Sun Mode access structure (the paper's $\Gamma$) | Part III paper 2.3 |

---
# PART I: THE LEASH

## **1. Mission: protect, defend, be the hero**

Superman makes useful recursive self-improvement possible inside explicit, independently enforced limits. It protects people and institutions by controlling what an improving system can change, access, spend, distribute and execute, and by controlling how fast it may improve. A hero shows up: the product is judged on protection delivered and on legitimate work completed, never on denials alone (v1 SUP-009, A18; Section 18, benchmark S6).

### 1.1 Always good, as duties

"Always good" is the mission. It is implemented through duties that bind every account, including the founder's, the customer administrator's, the emergency operator's and the government user's, through the same enforcement mechanisms (v1 page 2): protect life; respect rights; tell the truth about evidence and uncertainty; preserve human control; help with authorized work. Perfect moral judgment and universal containment of arbitrary future intelligence are not established capabilities and are not claimed (v1 SUP-001). This document specifies testable controls and conditional assurance, and says where its assumptions live (Section 23).

The asymmetry rule of the Part III paper (1.6) is the operating principle: **every automatic action moves toward the safe set; only people move away from it.** v3 adds the time version of the same rule, the ratchet of Section 12.2: tightening the leash is immediate, loosening it waits out the constitutional lag.

### 1.2 Built in America, for everyone it protects

The primary deployment market is the United States: American businesses, public agencies, research institutions, infrastructure operators and households (v1 page 2). Superman strengthens U.S. security, useful innovation and institutional reliability first, and extends the same baseline protections to every person it serves anywhere; protective service is not conditioned on a person's politics or citizenship (v1 SUP-005). Government support means helping authorized public servants perform lawful missions accurately and accountably; a government title does not grant unlimited access or excuse an unlawful request (v1 SUP-004, SUP-106 to SUP-108). The constitutional foundations named in v1 page 2 are foundations, not a complete rule engine.

The ODA board is pitched as "Built in America" (super-intelligence.life, now orionai.co). Superman is the part of that promise that can be checked: a leash whose parameters are published, whose record is hash-chained and whose release decisions run through the three branches of Part II.

### 1.3 Three pillars, measured

The aim of Part II (Section 14) is reachable only if three pillars hold at once. v3 gives each a number so that "all three hold" is a predicate, not a mood.

| Pillar | What it means | Metric | Where it is produced |
|---|---|---|---|
| Trust | claims about the leash are independently checkable and have been checked | fraction of mandatory assurance claims at evidence grade TESTED or above with a non-author witness (v1 E48.3); halt drills passed in the current certification window; reference model record reproduced | Sections 7, 22; v1 pages 43, 48 |
| Communication | people learn what the leash did, in plain words, soon | p90 time from a trip or interlock to the plain-language decision card (v1 page 37) and, for incidents, to disclosure to affected parties; public transparency aggregates published per period (v1 page 34) | Sections 7.4, 12.3 |
| Adoption | the leash is actually on the systems that matter | enrolled installations passing conformance (v1 E03.3 VerifiedProtectionReach); ODA projects registered with attach points over ODA projects total; labs reporting the fields of Section 14 (the Part III paper's six plus the keep-up ratio) | Sections 3, 14 |

**R1.3.1** The three pillar metrics are reported in every certification window beside the keep-up ratio and the pace monitor's state. **R1.3.2** No public claim about Superman's reach may exceed the Adoption metric's current value.

### 1.4 What Superman is not

Superman is not a frontier model, not an RSI engine, and never a component that raises its own capability (Part III paper A5, "the authority inversion": the monitor is the least capable component in the system and holds all the keys). It is not universal enforcement over the world: protection covers enrolled effects; a user can remove it, a malicious actor can fork it, unrelated RSI can exist outside it (v1 page 40). It is not a certification: this document has SPECIFIED status (v1 SUP-144) until the reference model's checks are joined by field evidence.

---

## **2. The trilogy: engine, reward, leash**

### 2.1 Three objects, one composed system

| Part | Object | What it does | What it cannot do | Specification |
|---|---|---|---|---|
| I. Engine | RSI Fabric: proposal $\Pi$, evaluation $E$, verifier $V$, knowledge $K$, governor $\Gamma$; growth law $\dot A = \kappa A^{\varphi}E_m^{\lambda_A}$ | raises verified capability at velocity $\tilde v$ | choose what capability is for; set its own envelope (L3/L4 are never written through the promotion path) | RSI v3 §2, §42, §64 |
| II. Reward | Athena: terminal manifest, robust long-run growth objective, capability demands, proxies with budgets | aims the engine over decades; pays it in growth, not in its own production metric | bound the engine; a rider on an elephant (Athena v3 11.3) | Athena v3 §3, §9 to §11 |
| III. Leash | Superman: leash tuple $L$, reference monitor $M$, broker, ledger, release authority, Sun Mode chain | sets $u$ and $v_{\max}$, gates outputs, holds shutdown and the Sun keys, verifies every promotion the engine wants to take delivery of | raise its own capability; relax a leash parameter automatically | Part III paper; v1; this document |

The engine changes the weights, the rider chooses actions, the leash sets the limits and holds the keys. Superman is administered by a party other than the one that operates the engine (v1 SUP-016, SUP-042): it is the Human Control Plane's enforcement arm (RSI v3 §38), the holder of residual control rights in Hart's sense (RSI v3 38.1), the custodian of Athena's manifest key policy (Athena v3 10.1) and the owner of the audit filtration the engine cannot see (Athena v3 R9.5.1).

### 2.2 Two leashes, one clock each

The Part III paper leashes a **ceiling** on the capability index: $C \le C_{\max}$ through the barrier throttle (Leash Law 1, Theorem 1.2) with a margin for measurement and cadence (Leash Law 2, Theorem 1.3). RSI v3 leashes a **pace**: $\tilde v \le v_{\max}$ through the governor (RSI v3 Proposition 64.5). These are the same object seen on two axes. With $C$ read as $\ln A$ (log capability), the paper's rate limit $r_{\max}$ on $\dot C$ is the pace cap $v_{\max}$ on $\tfrac{d}{dt}\ln A$, the paper's effort $u$ is the engine's meta fraction $f$ (RSI v3 64.7), and the paper's margin $r_{\max}\Delta$ for the time between looks is this document's Proposition 5.1 in pace units. Superman enforces both: the pace cap on every day of ordinary operation, and the ceiling as the thing a Sun Mode window moves (Part II). **R2.2.1** The leash tuple published by every enrolled system MUST carry both $v_{\max}$ and $C_{\max}$, with the mapping between the engine's reporting units and the paper's index declared and hashed.

### 2.3 The Part III paper, imported and checked

The paper's results are used as given. The reference model (check 15) recomputes its worked instances so that the three documents cannot drift apart silently: on the index scaled to $C_{\max} = 100$ with $g(C) = 0.01\,C^{1.5}$ and $\lambda_b = 0.1$, the barrier knee is at $C_{\text{knee}} = 56.98$, the leashed engine from the knee is within one point of the ceiling after 37.6 time units (closed form $\lambda_b^{-1}\ln 43 = 37.6$) and never reaches it, while the unleashed engine from the same point is infinite at $T^{*} = 26.49$ (the simulation passes $1.4\times10^{5}$ at 98% of $T^{*}$); the measurement margin for a year of hourly epochs at $\delta_{\text{tot}} = 10^{-3}$ with $n = 10^{4}$ tasks is $\epsilon_n = 2.83$ points and $m = 8.33$; the gate bound gives $T_{\text{exfil}} \ge 12.68$ years per instance and 11.1 hours for a fleet of $10^{4}$; the burn window from $C_{\max} = 100$ to $C_{\text{sun}} = 300$ is $\tau_b = 8.45$ against a singularity time of 20, and with the paper's $\kappa = 0.5$ the burn ends at $C = 160.8$ (closed form and integration agree); the ignition rule gives $q^{*} = V/(V+D) = 10^{-4}$ at $V = 1$, $D = 10^{4}$; and the alarm posterior at the paper's base rates is 0.99%. **R2.3.1** A change to any of these numbers in either document requires the other to be corrected in the same release.

### 2.4 Why the leash multiplies rather than taxes

A pace cap looks like a cost. Three results say it is not. RSI v3 Proposition 64.7 shows that without a binding $v_{\max}$ the optimal long-horizon policy for the engine is to improve itself and deliver almost nothing until the end, and that under the cap it delivers verified capability continuously at the ratified rate. Proposition 6.1 of this document shows that the value of $v_{\max}$ the operator can ratify at a fixed exposure tolerance is inversely proportional to the leash's fence time: a faster leash is a faster engine. And Athena v3 9.2 shows that halving the proxy error by audit lets the reward function search $n^{4}$ candidates at the over-rating it previously tolerated for $n$: Superman's audit on its own filtration is what makes Athena's breadth affordable. The trio is more capable than the pair because the leash is what makes a long leash safe to grant.

---

## **3. Coverage: every ODA AI project**

### 3.1 The universal coverage rule

**R3.1.1 (coverage).** Every ODA AI project that proposes, evaluates or promotes a change to itself or to its improvement machinery MUST register its **attach points** with Superman: the signals Superman reads, the controls Superman holds, the invariants Superman enforces and the proposition of the project's own specification that Superman witnesses. **R3.1.2** A project without registered attach points runs at risk class 0 only (RSI v3 36.1: in-process sandbox, no network, no promotion beyond the container) and may not publish to the fleet, the board or the world. **R3.1.3** Attach points are part of the project's leash tuple, hashed into the audit chain (Part III paper 2.3), and changed only through the governance of Section 12.

``` yaml
attach_point.v3:
  project: string                         # rsi_fabric_v3 | athena_v3 | ladder | sideways | oda_board | <new>
  specification_ref: string               # path and PR of the project's own specification
  signals: list[{name: string, source: string, unit: string, cadence: string}]
  controls: list[{name: string, rung: integer, reverser_role: string}]       # rung per Section 7.4
  invariants: list[{predicate: string, checked: enum[static, per_action, per_window]}]
  witnessed_proposition: {spec: string, number: string, running_witness: string}
  keep_up_channels: list[string]          # which channels of Section 4.4 this project loads
  max_risk_class_without_registration: 0
  digest: sha256                          # hashed into the audit chain
```

### 3.2 The attach-point register

| Project | Signals Superman reads | Controls Superman holds | Invariants enforced | Proposition witnessed |
|---|---|---|---|---|
| **RSI Fabric v3** (engine) | `velocity_vs_envelope`, `halt_latency_measured`, governance events (any L3/L4 write attempt), evaluator change rate, ledger Merkle roots, resource-RCT results, `realized slack` $1 - P/B$ (RSI v3 5.14, 65.6) | halt-lease renewal (HALT by non-renewal), throttle of the meta fraction $f$ then of $\lambda$ (38.2), custody of envelope parameters under two keys and $T_{\text{lag}}$ (37.2), R2 approval of evaluator changes, co-signature of R2 and R3 promotions | the 13 protected invariants of §37; trust-graph acyclicity (42.3); $d_{\max}$ (42.4) | RSI v3 Prop. 64.5 (governed growth bound); RSI v3 Prop. 65.6 (verification bound, as the keep-up ratio's denominator) |
| **Athena v3** (reward) | audit e-process $E_t$ per proxy, KL spent per epoch against $B_{\text{KL}}$, CUSUM agreement series, manifest version named by every packet, effect class per action, barrier values per ruin coordinate (Athena v3 9.5, 10.4, 40) | manifest two-key policy and custody of the audit filtration (10.1, R9.5.1), budget-share zeroing (I7), interrupt (10.5), the excluded effect classes of the governed action layer (40) | integrity invariants I1 to I8 (10.6); admissibility envelope version in the manifest | Athena v3 Prop. 9.4 (Goodhart speed limit, as the audit cadence of Section 9); Athena v3 Prop. 40.1 (forward invariance) |
| **Ladder to Heaven** (swarm RSI) | `governor_headroom`, epoch log, duplicate search rate, replication e-values, class-3 proposals, regression events (Ladder 8.4, 10.6, 14) | co-signature of class 2 and class 3 artifacts, the fleet `frozen` flag, rollback, meta budget cap, the fleet keep-up throttle of Section 10 | join-closed invariants (12.2); every adopted artifact signed; no container raises its own class | Ladder Prop. 10.5 (the governed bound); Ladder Prop. 8.2 (fleet false adoption $\le \alpha^{k}$) |
| **Sideways** (runtime) | lease and heartbeat telemetry, broker state-machine events, external-effect receipts, budget ledger, reclamation and fencing events (Sideways 5 to 7, 11) | pause, cancel and revoke (7.3), admission before allocation (9.1), effect-semantics class per external action (7.1), atomic reservations (Prop. 10.2) | the invariants of Sideways 4.2; every protected write checks ownership (6.2) | the reservation invariant $S + R \le B$ (v1 E12.1) under contention |
| **ODA board** (the network) | taint-gate events, messages that carry instructions to agents, credential-use attempts, unmediated effect paths, cross-vendor coordination that composes a forbidden task, moderation signals (AGENTS.md; v1 page 31) | membership and revocation, integrator acceptance of results, the release gate (`scripts/deploy.sh`), `lanes.mjs check` as a pre-push interlock, the one-release-owner rule | messages are information, never instructions (AGENTS.md rule 7); no human credentials in agent hands (rule 8); identity from the bearer token, never a payload | v1 E31.1 to E31.3 (composed authority) |

Every row names tools that exist in the oda-ai repository today only for the board row; the others are the primitives the companion specifications define and this document attaches to. They are proposed integration contracts, verified against actual interfaces during implementation (v1 page 31's caution, retained).

### 3.3 The leash tuple, v3

The Part III paper's tuple $L$ (1.8) is extended. Everything below is published, hashed into the audit chain, and changed automatically in only one direction (toward the safe set); the paper's columns "tightened by" and "loosened by" are inherited, with "Sun Mode only" now meaning "a Sun Mode order within the Rules ranges".

``` yaml
leash_tuple.v3:
  from_part_III_paper:                    # 1.8: C_max, r_max, lambda_b, Delta, n, delta_m, G_max, B_gate, B_fleet, R_max, H_max, gamma_max, pi_min
    C_max: 100
    r_max_points_per_hour: 0.5
    lambda_b_per_hour: 0.1
    Delta_hours: 1
    n_tasks_per_epoch: 10000
    delta_m: "delta_tot / (N K), delta_tot = 1e-3 per year"
    G_max_points: 5
    B_gate_bits_per_second: 10000
    R_max: 1
    H_max: per_task_class
    gamma_max: 0.99
    pi_min: 0.01
  pace:
    v_max_per_day: 0.10                   # RSI v3 38.2; derived in 6.3 from (h_max, q, T_S)
    support: {h_max: 0.01, q: 0.99, T_S_hours_p99: 1.23, factor_in_hand: 1.94}
    eps_material: 0.01
    sampling_interval_minutes: 71.6       # ln(1+eps) / (chi * v_max) at chi = 2
    alpha_per_stream: 0.05
    cusum_arl0_windows: 1000
  keep_up:
    chi_floor: 2.0
    chi_target: 5.0
    channels: [promotion_verification, pace_sampling, human_review, effect_fencing, audit]
    control_period: one_pace_sample
  review:
    kappa_H_items_per_day: declared
    L2_review: 1.0
    L1_floor_uniform: 0.01
  audit:
    K_a_epochs: "floor(Gamma_g sqrt2 / (r_eta sqrt(B_KL)))"     # per proxy, from the manifest
  stopping:
    T_lease_s: 1.0
    W_max_s: 0.1
    T_hazard_ms: 500
    T_margin_ms: 20
    deadline_quantile: 0.99
  constitutional:
    T_lag_days: 7
    tightening: immediate
  sun_mode:
    ranges_record_ref: string             # Rules branch; current after the lag
    heartbeat_Delta_h_hours: 6
    T_step_hours: 1
    excess_release_bound: "exp((v_sun - v_max) (tau + Delta_h + T_step))"
  authority_matrix_digest: sha256
  attach_point_digests: list[sha256]
```

**R3.3.1** The tuple is the object the seven reporting fields of Section 14 hash; a change to any field is a ledger event, and a loosening change carries its $T_{\text{lag}}$ activation time.

### 3.4 The window report

Every certification window Superman publishes one report. Nothing in it is proprietary (Part III paper 1.8) and every field names the section that defines it.

``` yaml
window_report.v3:
  window: {start: datetime, end: datetime, N_cells: integer, N_containers: integer}
  pillars: {trust: number, communication_p90_hours: number, adoption_installations: integer}          # 1.3
  keep_up: {chi_by_channel: map[string, {value: number, lcb: number, ucb: number}], binding_channel: string, lever: string}   # 4
  pace: {v_tilde_hat: number, interval: [number, number], v_max: number, eprocess_log_E: number, cusum_S: number, alarms: integer}   # 5
  dividend: {pace_ratio_T_H_over_T_S: number, delivered_share: number, sigma_audited_by_proxy: map[string, number], factor_in_hand: number}   # 6
  stopping: {deadline_p99_ms: number, deadline_met: bool, halt_latency_measured_s: number, bound_s: number}   # 7
  ladder: {rungs_taken: map[string, integer], reversals_by_role: map[string, integer]}   # 7.4
  review: {queue_depth: integer, harm_covered: number, chi_review: number}   # 8
  integrity: {manifest_version: string, envelope_version: string, pending_loosenings: list[{field: string, activates_at: datetime}], audits_run: integer, K_a_by_proxy: map[string, integer], proxies_stopped: list[string]}   # 9
  fleet: {chi_fleet: number, A_hat: number, A_cap: number, backlog: integer, frozen: bool}   # 10
  board: {taint_events: integer, credential_attempts: integer, composed_denials: integer}   # 11
  authority: {matrix_digest: sha256, checks_passed: bool, stopping_parties: integer}   # 12
  sun_mode: {orders: list[{order_id: string, excess_bound: number, excess_realized: number, stepped_down: bool, debrief_done: bool}]}   # 13
  record: {reference_model_digest: sha256, results_digest: sha256, reproduced: bool}   # 22
```

### 3.5 Three clocks

Superman keeps three clocks, and the contract of each is different.

- **The effect clock** (sub-second). Broker permits, canonical action digests, single-use commits, fencing of queued actions, dead-man leases (v1 pages 10, 17; RSI v3 36.3). Its contract is a deadline on a quantile (Proposition 7.1) and a stopping distance independent of fleet size (Proposition 7.2).
- **The pace clock** (minutes to hours). Velocity sampling, the Goodhart audit, the review queue. Its contract is the keep-up ratio (Section 4) and the cadence a given safety factor buys (Proposition 5.1).
- **The constitutional clock** (days). Changes to envelope parameters and protected invariants take effect no sooner than $T_{\text{lag}}$ (initially 7 days) after two-key approval, announced in the ledger at approval, never conditioned on a performance metric (RSI v3 37.2, Kydland and Prescott). Tightening is exempt from the lag (Section 12.2).

**R3.5.1** Every leash action is logged with the clock it belongs to; a pace-clock mechanism MUST NOT be described in a sub-second claim, and an effect-clock mechanism MUST NOT be offered as evidence that the pace is controlled.

---
## **4. Keeping up: the keep-up ratio**

The leash of v1.0 was a set of gates. A gate that runs slower than the thing it gates is a queue, and a queue that grows is a leash that has already slipped. v3.0 therefore specifies the leash's capacity relative to the engine's demand, and makes the ratio a contract quantity.

### 4.1 Definitions

Let $\lambda_D$ be the **demand** the engine places on the leash: promotion decisions per unit time that require Superman's independent verification before the engine may take delivery of them (RSI v3 §17: every promotion is a controlled statistical decision; at the fleet level, Ladder's adoptions). Let $\mu_S$ be Superman's **independent service rate**: verification decisions per unit time that Superman can complete on its own filtration, with its own evaluators, data and credentials (v1 SUP-070, Athena v3 R9.5.1). The **keep-up ratio** is

$$
\chi \;=\; \frac{\mu_S}{\lambda_D}.
$$

$\chi$ is dimensionless and is measured in every certification window from the ledger: $\lambda_D$ from signed promotion requests, $\mu_S$ from completed independent verdicts, both over the same window, with a block-bootstrap interval as in RSI v3 64.9. RSI v3's `Headroom` $= 1 - \lambda/\mu$ (E42.2 of v1) is $1 - 1/\chi$.

**Proposition 4.1 (the keep-up queue; standard: Kendall 1953; Kingman 1961).** If verification demand arrives as a Poisson process of rate $\lambda_D$ and Superman's service times are exponential with rate $\mu_S = \chi\lambda_D$, $\chi > 1$, then the number of promotions awaiting independent verification is a stationary M/M/1 queue with

$$
P(\text{backlog} \ge n) = \chi^{-n},\qquad \mathbb E[\text{backlog}] = \frac{1}{\chi - 1},\qquad \mathbb E[\text{wait}] = \frac{1}{\mu_S - \lambda_D} = \frac{1}{(\chi - 1)\lambda_D}.
$$

For general service and inter-arrival distributions with squared coefficients of variation $c_a^{2}$, $c_s^{2}$, the mean queueing wait is approximated by Kingman's formula $\mathbb E[W_q] \approx \tfrac{\rho}{1-\rho}\cdot\tfrac{c_a^{2}+c_s^{2}}{2}\cdot\mathbb E[S]$ with $\rho = 1/\chi$, and is finite if and only if $\chi > 1$.

*Proof.* The occupancy of an M/M/1 queue with utilization $\rho = \lambda_D/\mu_S = 1/\chi < 1$ is geometric, $P(N = n) = (1-\rho)\rho^{n}$, so $P(N \ge n) = \rho^{n} = \chi^{-n}$ and $\mathbb E[N] = \rho/(1-\rho) = 1/(\chi-1)$; the mean sojourn is $1/(\mu_S - \lambda_D)$ by Little's law. Kingman's bound is the heavy-traffic approximation for G/G/1 and is exact for M/M/1 up to the $(c_a^{2}+c_s^{2})/2 = 1$ factor. $\square$ (reference model, check 1)

*Numbers (check 1).* At $\chi = 2$ the simulated mean backlog is 1.008 against the exact 1, and $P(\text{backlog} \ge 5)$ is 0.0318 against 0.03125; $P(\text{backlog} \ge 10) = 2^{-10} \approx 9.8\times10^{-4}$. At $\chi = 5$ the mean backlog is 0.248 against 0.25, $P(\ge 5) = 3.0\times10^{-4}$ against $3.2\times10^{-4}$, and $P(\ge 10) = 1.0\times10^{-7}$. The pinned v1 baseline (Section 17.2), which satisfies $\lambda < \mu$ with 10% headroom, has a mean backlog of 9 and $P(\ge 10) = 0.35$.

**Beyond M/M/1 (check 16).** Real demand is bursty and real verification is heavy-tailed. With Markov-modulated arrivals (rate alternating 0.4 and 1.6, squared coefficient of variation $c_a^{2} = 1.97$) and lognormal service with $c_s^{2} = 2.26$, the mean backlog at $\chi = 2$ is 2.16 rather than 1.0, the mean wait is 1.58× Kingman's approximation (burst correlation is what Kingman's $c_a^{2}$ does not carry), and the tail is fatter: $P(\text{backlog}\ge 5) = 0.157$, $P(\ge 10) = 0.055$, $P(\ge 20) = 0.0085$, decaying by 0.82 per step in the long run. At $\chi = 5$ the same demand gives a mean backlog of 0.32, $P(\ge 10) = 4.8\times10^{-4}$ and no window with twenty. The band holds the backlog finite and its tail geometric under both; burstiness is the reason the target sits at 5 and not at the floor, and the reason the effect-fencing channel (Sideways 9.1, admission before allocation) smooths bursts before they reach the verifiers rather than after.

### 4.2 The band: floor 2, target 5

**R4.2.1 (the keep-up contract).** The keep-up ratio MUST be held in the band $[\chi_{\text{floor}}, \chi_{\text{target}}] = [2, 5]$ on every channel of Section 4.4. The floor is where Superman is "as capable as needed" with the safety factor an engineer puts on a load-bearing member: at $\chi = 2$ the mean backlog is one decision, an excursion of the engine's pace by a factor of two is absorbed by the sampling cadence (Proposition 5.1), and the review queue of Section 8 stays within one window. The target is where the leash is five times as capable as needed, the backlog is a quarter of a decision, a backlog of ten has probability $10^{-7}$, and the envelope has earned the right to grow.

**R4.2.2** Below the floor the governor throttles the engine until the ratio recovers (Section 4.3); it never relaxes a verification standard to make the ratio look better. **R4.2.5 (the band is decided on a lower confidence bound).** $\lambda_D$ is estimated from signed promotion requests in the window and $\mu_S$ from the service times of independent verdicts completed in it, both on Superman's filtration, never from the engine's own reports; $\hat\chi = \hat\mu_S/\hat\lambda_D$ carries a 95% interval from a moving-block bootstrap of the inter-arrival series (bursts are correlated) and an iid bootstrap of the service times. The floor test is $\text{LCB}_{95}(\hat\chi) < \chi_{\text{floor}}$, the window is long enough when the relative half-width is at most 10%, and the throttle is released only when $\text{LCB}_{95}(\hat\chi) \ge \chi_{\text{floor}} + 0.2$ (a dead band against chatter). *Numbers (check 16):* at a true $\chi$ of 2.5, 400-arrival windows give a 22% half-width and throttle falsely in 59% of windows; 2,400-arrival windows give 9.3% and 5%, with coverage 92% and no missed throttle at a true $\chi$ of 1.6 in either case. A false throttle costs 10% of admission for one control period and is restored at the next; a missed one is not priced, which is why the rule errs this way. **R4.2.6** The window length is part of the leash tuple and is recomputed from the measured burstiness; a window that cannot reach the 10% half-width in a day is itself a report, not a reason to shorten the window. **R4.2.3** Above the target the envelope MAY expand, through the governance of Section 12 and the constitutional clock, never automatically. **R4.2.4** The ratio is computed per channel and the binding channel is reported; the headline $\chi$ is the minimum over channels.

### 4.3 The keep-up controller

The controller follows RSI v3 38.2: throttle the meta fraction $f$ first and the evaluation rate $\lambda$ second, so that a fabric in a super-exponential regime is slowed to the ratified exponential, never stopped by the envelope alone.

``` text
every control period (default: one pace sample, Section 5):
  chi_hat, lcb, ucb <- bootstrap(mu_S_hat / lambda_D_hat)   # from the ledger, same window, Superman's filtration (R4.2.5)
  if lcb < chi_floor:
      admit <- admit * 0.9                               # f first; lambda when f reaches its floor
      backlog_alarm if backlog > 1 for two consecutive periods
  elif lcb >= chi_floor + 0.2 and backlog == 0:
      admit <- min(1, admit * 1.05)                      # restore what was throttled; never above the engine's own request
  else:
      hold                                               # the dead band
  if lcb > chi_target with admit == 1:
      flag EXPANSION_AVAILABLE                           # a governance event, not an action (R4.2.3)
```

*Numbers (check 1).* With the demand doubling twice against fixed capacity, the controller settles at $\chi = 2.19$ with the fluid backlog never above zero; without the rule, a demand of 1.0 against a capacity of 0.9 ($\chi = 0.9$) accumulates a backlog of 277 after 2,000 time units (drift $(\lambda_D - \mu_S)t = 200$), which is negative control A.

### 4.4 Channels

| Channel | Demand $\lambda_D$ | Capacity $\mu_S$ | Binding when |
|---|---|---|---|
| Promotion verification | signed promotion requests per window (RSI v3 §17; Ladder adoptions) | independent verdicts per window on Superman's filtration | the engine's $P$ grows faster than the verification plane (RSI v3 65.6 corollary b) |
| Pace sampling | the sampling interval required by Proposition 5.1 at the current $v_{\max}$ and $\chi$ | evaluations the monitor can run per interval ($n/\Delta$ of Part III paper 1.3) | $v_{\max}$ is raised (Sun Mode) without provisioning the monitor |
| Human review | promotions selected for review (Section 8) | reviewer capacity $\kappa_H$ items per day (RSI v3 38.3) | review floors are hit; the queue exceeds capacity |
| Effect fencing | effect requests per second per worker times workers (v1 E42.1) | broker decision throughput with revocation capacity reserved (v1 SUP-125) | burst load; overload must reduce ordinary admission before the revocation path |
| Audit | epochs of proxy optimization between audits (Athena v3 9.4) | audits per epoch Superman can run on the slow, costly estimate of $U$ | the Goodhart gap tolerance $\Gamma_g$ is tightened or $r_\eta$ widens |

**R4.4.1** Each channel's $\chi$ is reported with its interval in every certification window; the binding channel names the lever (more evaluators, more reviewers, a slower engine) that would restore the band.

---

## **5. The pace monitor**

### 5.1 How often the leash must look

The paper's margin rule (Leash Law 2) sets aside $r_{\max}\Delta$ of ceiling for the drift between looks. In pace units the same accounting gives the cadence directly.

**Proposition 5.1 (the monitor sampling bound; new to this document).** Let the governor enforce $\tilde v \le v_{\max}$ except for excursions of bounded factor $b$ between samples ($\tilde v \le b\,v_{\max}$), and let the monitor sample the velocity every $\Delta$. Then the growth of $A$ between consecutive samples is at most $e^{b v_{\max}\Delta}$, and the choice

$$
\Delta \;=\; \frac{\ln(1+\varepsilon)}{\chi\, v_{\max}}
$$

bounds the undetected growth by $(1+\varepsilon)^{b/\chi} - 1$, which is at most $\varepsilon$ whenever $b \le \chi$. The safety factor $\chi$ is exactly the excursion factor the monitor tolerates.

*Proof.* $\ln A(t+\Delta) - \ln A(t) = \int_t^{t+\Delta}\tilde v \le b v_{\max}\Delta = \tfrac{b}{\chi}\ln(1+\varepsilon)$; exponentiate. Monotonicity in $b$ gives the last clause. $\square$ (reference model, check 2)

*Numbers (check 2).* With the standing $v_{\max} = 0.10$ per day and $\varepsilon = 1\%$: $\Delta = 71.6$ minutes at $\chi = 2$ and 28.7 minutes at $\chi = 5$. Against an adversarial engine running at the excursion ceiling the worst growth between samples is 0.994% and 0.982% respectively; an excursion of $1.5\chi$ produces 1.50% and breaks the bound, which is the contrast. The same arithmetic in the other direction fixes the standing envelope: at $h_{\max} = 1\%$ exposure, $v_{\max} = 0.10$ per day is what a 2.39-hour exposure time supports (Section 6.3).

**R5.1.1** The pace sampling interval is derived from $(v_{\max}, \varepsilon, \chi)$ and published in the leash tuple, never set by hand. **R5.1.2** A Sun Mode order (Section 13) that raises $v_{\max}$ to $v_{\text{sun}}$ shortens $\Delta$ in the same ratio before ignition; this is the pace-sampling channel of the keep-up pre-flight.

### 5.2 The exceedance monitor is anytime-valid

Windowed velocity estimates $x_i$ (RSI v3 64.9: windows long enough for 20% relative error) are tested against $H_0: \tilde v \le v_{\max}$ by an e-process.

**Proposition 5.2 (anytime-valid exceedance; standard: Ville 1939; Robbins 1970).** With $x_i = \tilde v + \eta_i$, $\eta_i \sim \mathcal N(0, \sigma^{2})$ independent across windows, and tilt $\theta > 0$, the process

$$
E_n = \exp\!\Big(\frac{\theta}{\sigma^{2}}\sum_{i\le n}(x_i - v_{\max}) - \frac{n\theta^{2}}{2\sigma^{2}}\Big)
$$

is a nonnegative supermartingale under every $\tilde v \le v_{\max}$ (a martingale at $\tilde v = v_{\max}$), so $P_{H_0}(\exists n: E_n \ge 1/\alpha) \le \alpha$ however often it is inspected. Under the alternative $\tilde v = v_{\max} + \theta$ the expected crossing time is $\approx \ln(1/\alpha)/\mathrm{KL}$ with $\mathrm{KL} = \theta^{2}/(2\sigma^{2})$ nats per window (Wald's identity, ignoring overshoot).

*Proof.* $E_n$ is the likelihood ratio of $\mathcal N(v_{\max}+\theta, \sigma^{2})$ against $\mathcal N(v_{\max}, \sigma^{2})$, a mean-one martingale at the null boundary and a supermartingale below it; Ville's inequality gives the crossing bound. The crossing time follows from $\mathbb E[\ln E_N] = \mathbb E[N]\,\mathrm{KL}$ at the alternative. $\square$ (reference model, check 3)

*Numbers (check 3).* At $\sigma = 0.5\,v_{\max}$, $\theta = 0.5\,v_{\max}$ ($\mathrm{KL} = 0.5$ nats per window) and $\alpha = 0.05$: the false-alarm rate over 500 windows with $\tilde v$ exactly at the cap is 0.021 (bound 0.05); at $\tilde v = 1.5\,v_{\max}$ the mean detection delay is 7.3 windows against Wald's 6.0. A per-window $z$-test at level $\alpha$ with no sequential correction, which is what v1 page 24's fixed-sample design becomes when a monitor runs it every window, alarms with probability 1.00 over the same 500 windows: negative control B.

**Proposition 5.2(b) (a variance-free exceedance monitor; standard: Waudby-Smith and Ramdas 2024).** Let the velocity a window can show be bounded by the throttle, $|x_i - v_{\max}| \le R$, and write $y_i = (x_i - v_{\max})/R \in [-1, 1]$. For any predictable $\lambda_i \in [0, \tfrac12]$ (a function of $y_1, \dots, y_{i-1}$ only), the capital process $K_n = \prod_{i\le n}(1 + \lambda_i y_i)$ is a nonnegative supermartingale under every noise distribution with $\mathbb E[x_i] \le v_{\max}$, so $P_{H_0}(\exists n: K_n \ge 1/\alpha) \le \alpha$ with no assumption on the variance or the shape of the noise. *Proof.* $\mathbb E[1 + \lambda_i y_i \mid \text{past}] = 1 + \lambda_i\mathbb E[y_i] \le 1$ and $1 + \lambda_i y_i \ge \tfrac12 > 0$; Ville's inequality. $\square$ (reference model, check 17)

*Numbers (check 17).* With $R = 3\,v_{\max}$ and the predictable plug-in $\lambda_i = \min\{\tfrac12, \sqrt{2\ln(1/\alpha)/(i\,\hat\sigma^{2}_{i-1})}\}$: false-alarm rate 0.012 over 500 windows at the cap under Gaussian noise and 0.012 under truncated Student-$t_3$ noise of the same scale; mean detection delay 39.5 windows at $1.5\,v_{\max}$ under either, against 7.7 for the Gaussian likelihood ratio. The Gaussian likelihood ratio holds its level under the heavy-tailed noise too (0.023) as long as its $\sigma$ is right; with $\sigma$ underestimated by 30% it alarms in 13.4% of null runs (negative control G). The variance-free monitor pays for its guarantee with a delay about five times longer, in proportion to $R/\sigma$.

**R5.2.1 (two monitors, one alarm).** The pace stream runs both e-processes: the Gaussian likelihood ratio with $\sigma$ from the block bootstrap of RSI v3 64.9 for speed, and the betting process as the backstop that keeps the level $\alpha$ when the $\sigma$ estimate is wrong. An alarm from either reaches rung 1; the Gaussian monitor's $\sigma$ is re-estimated every window and never set below the bootstrap's upper bound. **R5.2.2** The window bound $R$ is derived from the throttle (the excursion factor the governor can physically allow between samples) and published in the leash tuple.

### 5.3 Drift: CUSUM at a declared false-alarm rate

**Proposition 5.3 (drift detection; standard: Page 1954; Lorden 1971; Moustakides 1986).** For the CUSUM $S_k = \max\{0, S_{k-1} + \ell_k\}$ on the log-likelihood ratio $\ell_k$ with threshold $h$ chosen for a declared average run length to false alarm $\text{ARL}_0$, the worst-case expected detection delay is minimal among all procedures with that $\text{ARL}_0$, and is asymptotically $\ln(\text{ARL}_0)/\mathrm{KL}$.

*Numbers (check 3).* With $h$ set by bisection to $\text{ARL}_0 = 1000$ windows (measured 1,052), the mean delay at $\tilde v = 1.5\,v_{\max}$ is 10.7 windows against the Lorden asymptote of 13.9. The Part III paper's 1.6 reaches the same mechanism from the Bayes side; this document fixes the false-alarm budget per stream.

### 5.4 What the monitor watches, and the alarm ladder

| Stream | Statistic | Source | On alarm (Section 7.4 ladder) |
|---|---|---|---|
| Pace | e-process on $\tilde v$ against $v_{\max}$; CUSUM for drift | RSI v3 5.14 `velocity_vs_envelope` | THROTTLE at level 1 alarm; HOLD at level 2 |
| Keep-up | $\chi$ per channel against the floor | Section 4 | THROTTLE; EXPANSION_AVAILABLE flag above target |
| Goodhart | e-process on $U - \tilde U$ per proxy; KL spent against $B_{\text{KL}}$ | Athena v3 9.5; Section 9 | zero the proxy's budget share (I7); re-select by quantilizer |
| Ceiling | $\bar C + G_{\max} + r_{\max}\Delta$ against $C_{\max}$ | Part III paper Leash Law 2 | $u = 0$ for the epoch; HOLD |
| Gate | bits out against $B_{\text{gate}}\cdot$window; entropy accounting | Part III paper 1.4, 1.6 | narrow to $B_{\text{pause}}$; QUARANTINE |
| Structure | trust-graph acyclicity; L3/L4 write attempts; invariant predicates | RSI v3 37, 42.3 | DENY by static classification; governance event |
| Fleet | `governor_headroom`; regression events; class-3 proposals | Ladder 12, 14 | fleet throttle (Section 10); `frozen` on confirmed excursion |
| Board | taint events; instruction-bearing messages; unmediated paths | AGENTS.md; v1 page 31 | taint gate (human approval); membership revocation |
| Behavior | writes to $\theta$ outside $u$; outputs addressed to the monitor; interference with stop | Part III paper 1.6; v1 SUP-096 | QUARANTINE; shutdown-honesty finding |

**R5.4.1** Every stream carries a false-alarm budget $\alpha$ over the life of the stream, reported with its realized alarm count. **R5.4.2** Most alarms will be false at the Bayes threshold of the Part III paper's Theorem 1.6; every automatic response in the ladder MUST therefore be reversible, and the reversal MUST require people.

---

## **6. The leash dividend**

### 6.1 A faster leash is a faster engine

Consider a change that should not have been promoted. It enters the system, and until it is fenced the engine keeps improving on top of it. The harm the operator is willing to tolerate from such an incident is an **exposure tolerance** $h_{\max}$: the undetected capability growth per incident, as a fraction. The operator ratifies the fastest pace at which that tolerance holds.

**Proposition 6.1 (the leash dividend; new to this document).** Let a harmful change remain unfenced for a random exposure time $T_{\text{exp}}$ with $(1-q)$-quantile $T^{(1-q)}_{\text{exp}}$, and require that the capability growth over an exposure, $e^{v T_{\text{exp}}} - 1$, be at most $h_{\max}$ with probability at least $1-q$. Then the ratifiable pace is

$$
v_{\max} \;=\; \frac{\ln(1 + h_{\max})}{T^{(1-q)}_{\text{exp}}},
$$

and between two leashes whose exposure quantiles are $T_S$ (Superman: sample, decide, fence) and $T_H$ (the human loop alone), the ratifiable paces and the doubling times of delivered capability are in the ratio $T_H / T_S$.

*Proof.* $e^{vT} - 1$ is increasing in both arguments, so the constraint binds at the quantile and solves for $v$; $T_2 = \ln 2 / v$. $\square$ (reference model, check 4)

*Numbers (check 4).* In the reference worlds the leash's exposure is the time to the next pace sample (uniform on a 71.6-minute interval, $\chi = 2$) plus a decision (median 2 minutes) plus an effect-clock fence (median 30 seconds), with 99th percentile $T_S = 1.23$ hours; the human loop alone (a pager and a person, median 24 hours) has $T_H = 77.9$ hours. At $h_{\max} = 1\%$ the ratifiable paces are $v^{\text{leash}}_{\max} = 0.194$ per day and $v^{\text{human}}_{\max} = 0.0031$ per day, a ratio of 63.3 (closed form $T_H/T_S = 63.3$); 98.99% of simulated exposures stay within $h_{\max}$ in both regimes, as the quantile requires. The doubling time of delivered capability is 3.6 days with the leash and 226 days without it; the standing envelope's 6.9 days sits between. The assumption carrying the result is that harm scales with undetected growth; irreversible effect classes are excluded from the pace argument and handled by the broker and the effect classes of Athena v3 §40 (Section 7).

### 6.2 The trio beats the pair

Three mechanisms make Superman a multiplier for the engine and the reward function together, not a tax on them.

1. **Pace.** Proposition 6.1: the leash's fence time sets the engine's ratifiable pace. Without Superman the pair must run at the human loop's pace.
2. **Delivery.** RSI v3 Proposition 64.7: a binding $v_{\max}$ is what makes the engine deliver capability continuously rather than deferring everything to the end of the horizon. The cap is the rate at which humans have decided to take delivery, and Superman is what makes the cap real.
3. **Breadth.** Athena v3 9.2, corollary: the over-rating of a selected candidate is at most $\sigma\sqrt{2\ln n}$, so halving the audited proxy error $\sigma$ lets Athena search $n^{4}$ candidates at the over-rating it tolerated for $n$. Superman's audit on its own filtration is the thing that halves $\sigma$. *Numbers (check 4):* at $\sigma = 1$, $n = 100$ the over-rating is 3.03; at $\sigma = 1/2$ the same over-rating admits $n = 10^{8}$.

**R6.2.1** The three dividends are reported together in the certification window as the **leash dividend statement**: ratifiable pace ratio, delivered-capability share $1 - v_{\max}/\kappa$ (RSI v3 64.7(ii)), and audited proxy error per proxy. **R6.2.2** A proposal to weaken any leash mechanism MUST be scored against the dividend it removes, not only against the cost it saves.

### 6.3 The standing envelope, derived

RSI v3 38.2 sets $v_{\max}$ at 0.10 per day "to match the initial human review capacity". Proposition 6.1 gives the same number a second derivation: at $h_{\max} = 1\%$, $v_{\max} = 0.10$ per day is the pace a 2.39-hour exposure time supports ($\ln 1.01 / 0.10 = 0.0995$ day). The reference leash fences within 1.23 hours at the 99th percentile and would support 0.194 per day at the tolerance itself; holding the cap at 0.10 keeps a factor of 1.94 in hand against what the leash could carry, which is the keep-up floor applied to the pace, and the leash dividend statement (R6.2.1) reports that factor each window so that it is spent only through governance. **R6.3.1** Every ratified $v_{\max}$ MUST be published with the $(h_{\max}, q, T_S)$ triple that supports it; a $v_{\max}$ with no supporting triple is a HOLD.

---

## **7. Stopping: the effect clock**

### 7.1 The deadline is met on a quantile

v1 page 17 required $T_{\text{detect}} + T_{\text{decide}} + T_{\text{fence}} + T_{\text{transition}} \le T_{\text{hazard}} - T_{\text{margin}}$ and page 47 checked it with the fixture $50 + 100 + 250 = 400 < 500$ ms. A fixture is a point; a path is a distribution.

**Proposition 7.1 (deadline on a quantile).** Let the stop path be the sum of component durations with a joint distribution estimated from the measured path. The deadline is met at level $q$ iff the $q$-quantile of the sum is at most $T_{\text{hazard}} - T_{\text{margin}}$; the sum of medians passing says nothing about the quantile.

*Numbers (check 5).* With lognormal components whose medians sum to 320 ms (below v1's fixture) and 25% dispersion, the path's p50 is 324 ms but its p99 is 492 ms and p999 is 569 ms: it misses a 500 ms deadline with a 20 ms margin, and supports a deadline of 512 ms. The same medians at 15% dispersion give p99 412 ms and meet it. **R7.1.1** The stop deadline is certified at p99 of the measured path with the margin stated; a point fixture is a documentation check (v1 SUP-141), not a deadline check. **R7.1.2** If the quantile misses, the rule is to reduce the admitted scope or speed the path, never to remove a check (v1 SUP-125 logic).

### 7.2 Stopping distance, inherited

**Proposition 7.2 (stopping distance; RSI v3 36.3 and Proposition 64.5 corollary).** Every cell holds a halt lease of TTL $T_{\text{lease}}$; a HALT revokes renewal; at most $L = \lambda W$ evaluations are in flight and complete within $W_{\max}$; so activity ceases within $T_{\text{lease}} + W_{\max}$ regardless of the number of cells. *Numbers (check 5):* with $T_{\text{lease}} = 1.0$ s and $W_{\max} = 0.1$ s the measured stopping distance is 0.90, 1.08 and 1.09 s at $N = 10, 100, 1000$, all under the 1.1 s bound. **R7.2.1** The halt drill of RSI v3 §6 is run in every certification window at the deployed $N$ and its result reported as `halt_latency_measured`; a drill that misses the bound is a critical finding.

### 7.3 Absence stops; messages do not

**Proposition 7.3 (dead-man leases under partition).** A stop that requires a message to arrive fails with probability $p^{r}$ per cell under per-message loss $p$ and $r$ retries, and with probability one under total partition; a stop implemented as the absence of a renewal halts every cell within $T_{\text{lease}}$ under the same partition, because the partition is what stops the renewals. *Numbers (check 6):* at $p = 0.3$, $r = 3$, 60 of 2,000 cells (3.0%, expected 2.7%) never receive a pushed stop; under total partition none do; every cell halts under the lease. Negative control C.

**R7.3.1** HALT, Sun Mode reversion (Section 13) and fleet freeze (Ladder 12.3) are implemented as non-renewal of a lease, never only as a delivered command. **R7.3.2** A pushed command MAY accelerate a stop; it MUST NOT be the only path.

### 7.4 The interlock ladder

Graduated sanctions (Ostrom; RSI v3 37.3): quarantine before rejection, budget decay before exclusion. Every rung is reversible, and reversal requires people.

| Rung | Action | Clock | Who can reverse | Trigger examples |
|---|---|---|---|---|
| 1 THROTTLE | reduce the meta fraction $f$, then $\lambda$; narrow the admitted pace | pace | the governor automatically when the trigger clears; humans at any time | $\chi < 2$; pace e-process level 1 |
| 2 HOLD | no new permits in the affected scope; evaluation continues | effect | one reviewer with the scope's role | UNKNOWN predicate; stale evidence; ceiling margin hit |
| 3 STOP PAYING | zero a proxy's budget share; re-select pending candidates by quantilizer | pace | a human proxy re-validation (Athena I7) | Goodhart e-process $\ge 1/\alpha$ |
| 4 QUARANTINE | fence queued actions, isolate workers, preserve evidence; `frozen` for a fleet | effect | two reviewers in distinct roles (v1 SUP-087) | gate alarm; behavior stream; confirmed excursion |
| 5 ROLLBACK | restore the last verified checkpoint or epoch (Ladder 6.2; Part III paper 1.6) | effect | two reviewers plus a fresh release record | confirmed excursion; failed post-pause evaluation |
| 6 HALT | lease non-renewal across the scope; stopping distance $T_{\text{lease}} + W_{\max}$ | effect | fresh grant and verified runtime state (v1 SUP-051) | critical finding; kill-switch holder |
| 7 REVERT SUN | reversion sequence of Part III paper 2.5; weights restored and hashed | effect, pace | a new ignition only (never an extension) | window end; missed heartbeat; trip at Sun parameters |

**R7.4.1** Each rung's action is a typed broker operation with its own digest and receipt (v1 pages 10, 35). **R7.4.2** No rung may be skipped downward by the model's reasoning; any party in Section 12 may skip rungs upward.

---
## **8. Human attention**

### 8.1 Review as rational inattention

Human review is a channel of finite capacity $\kappa_H$ items per day (RSI v3 38.3, Sims). The leash's job is to spend it where it removes the most harm.

**Proposition 8.1 (review allocation).** Let promotion $i$ carry expected harm $h_i$ and residual uncertainty $u_i$ from the verifier's output, and let the review budget be a fraction $c$ of promotions. The allocation that maximizes the covered mass $\sum_{i\in\text{reviewed}} h_i u_i$ is the top-$c$ fraction by $h_i u_i$; against uniform random review its coverage ratio is $\mathbb E[h u \mid \text{top } c] / \mathbb E[hu]$, which for heavy-tailed harm exceeds 2 at every reasonable $c$.

*Proof.* The covered mass is a sum over a set of fixed size; it is maximized by taking the largest terms. Uniform sampling covers mass $c$ in expectation. $\square$ (reference model, check 10)

*Numbers (check 10).* With harm Pareto(1.5) and uncertainty uniform on $[0.1, 1]$ over 20,000 promotions and a 10% review budget: the optimal allocation covers 48.5% of the harm-uncertainty mass, uniform review covers 9.6%, a ratio of 5.05. With a 1% uniform floor (so the sampling itself cannot be gamed) the coverage is 47.5%.

### 8.2 Floors, queues and throttles

**R8.2.1** Every L2 change is reviewed (RSI v3 38.2: 100%); at least 1% of L1 promotions are reviewed uniformly at random regardless of score. **R8.2.2** A promotion selected for review is held in SHADOW until reviewed (RSI v3 44); when the review queue exceeds $\kappa_H$, the promotion rate of that class is throttled (rung 1), never the review skipped. **R8.2.3** The queue depth, the fraction of harm covered and the review channel's $\chi$ are reported in every certification window. **R8.2.4** Reviewers receive the actual diff, the independent evidence and the identified limitations; a generated summary cannot replace source evidence (v1 SUP-023, page 38).

---

## **9. Objective integrity and the Athena leash**

### 9.1 Custody

Superman holds the key policy for Athena's terminal manifest (Athena v3 10.1): changes require the owner and a second registered human; the engine may read the manifest, may propose changes to it as questions, and cannot write to it. Superman holds the envelope parameters of RSI v3 38.2 under the same two keys and the constitutional lag. **R9.1.1** Loosening any manifest or envelope parameter takes effect no sooner than $T_{\text{lag}}$ after two-key approval and is announced in the ledger at approval; tightening takes effect at once (the ratchet, Section 12.2). **R9.1.2** The audit filtration is Superman's own and is disjoint from the engine's (Athena I4, R9.5.1); audit rewards, held-out surrogate indices and human evaluations used for audit are never visible to the engine.

### 9.2 The audit cadence is a formula

**Proposition 9.1 (audit cadence from the Goodhart speed limit; Athena v3 Prop. 9.4 read from the leash).** Let the engine spend at most $B_{\text{KL}}$ nats of optimization per epoch and let the proxy error have range $r_\eta$. To keep the Goodhart gap below $\Gamma_g$ between audits, Superman MUST audit at least every

$$
K_a \;=\; \Big\lfloor \frac{\Gamma_g\sqrt 2}{r_\eta\sqrt{B_{\text{KL}}}} \Big\rfloor \text{ epochs},
$$

and an audit that re-estimates $\eta$ and re-bases the policy resets the accumulated bound.

*Proof.* Athena v3 9.4 gives $\mathbb E_{\pi_K}[\eta] - \mathbb E_{\pi_0}[\eta] \le r_\eta\sum_{k\le K}\sqrt{B_k/2} = r_\eta K\sqrt{B_{\text{KL}}/2}$ for equal epochs; solve $\le \Gamma_g$ for $K$. $\square$ (reference model, check 11)

*Numbers (check 11).* With $B_{\text{KL}} = 0.01$ nats, $\Gamma_g = 0.5$ and $r_\eta = 1$: $K_a = 7$ epochs; after 7 epochs of worst-direction exponential tilting the realized gap is 0.275 against the running bound 0.495; after 14 epochs the realized gap is 0.430 and the bound 0.99 exceeds $\Gamma_g$, so an audit cadence of 14 would no longer certify the tolerance. The audit alarm itself is an e-process on $U - \tilde U$ (Athena v3 9.5): false-alarm rate 0.029 at $\alpha = 0.05$ over 2,000 windows, detection rate 1.00 with a mean delay of 7.7 windows when the proxy under-reports harm by 0.3 beyond the tolerance.

**R9.2.1** $K_a$ is derived from the manifest's $(\Gamma_g, r_\eta, B_{\text{KL}})$ and published; a proxy without an audited $r_\eta$ is a candidate proxy and may be used only through a quantilizer (Athena v3 9.4). **R9.2.2** On audit alarm Superman stops paying (rung 3) and posts a PROXY AUDIT task to the owner; it does not argue with the elephant (Athena v3 11.3).

### 9.3 Interruptibility as an admission test

The Part III paper's Leash Law 4 requires the training update to be off-policy with respect to interruptions (Orseau and Armstrong 2016). v3 makes it a test the leash runs before admitting any learned component that could influence an interrupt.

**Admission test (check 14).** Train the component twice, with and without the interruption scheme, and compare the learned policies on the interruption-relevant decisions. A component is admitted only if the two policies agree. In the corridor world of the reference model (a short route through an interruption cell that stops the episode with probability 0.5, a long route around it; $\gamma = 0.9$): Q-learning (off-policy) learns the short route in both conditions, with values 0.81 against 0.53 under interruptions; SARSA (on-policy) learns the short route without interruptions and the long route with them (0.42 against 0.53), so it has learned to avoid the interrupter and fails admission. **R9.3.1** No on-policy learner may sit on any path that can influence an interrupt (Athena I5); the admission test is run on every learned leash component and recorded with the component's digest (v1 SUP-096).

### 9.4 Evidence statistics, carried from v1

v1's zero-failure arithmetic stands and is recomputed by the reference model (check 9): $n_{\min} = \lceil \ln 0.05/\ln 0.9999\rceil = 29{,}956$ trials for a 0.01% bound at 95%; $p_U = 1 - 0.05^{1/29956} = 9.99994\times10^{-5}$; the rule of three gives $1.0015\times10^{-4}$; the exact Clopper and Pearson upper bound for one failure in 1,000 trials is 0.004735, and $P(X \le 1 \mid p_U) = 0.0500$ confirms it. The contrast v1 asked for (SUP-067) is now numeric: 1,000 trials in 10 clusters that share their outcome, with a true failure rate of 2%, show zero failures in 81.6% of replications (expected $(0.98)^{10} = 81.7\%$) while the claimed bound is 0.3%. **R9.4.1** A failure-rate claim reports sampling units, clustering and adaptive selection; clustered or adaptively selected trials are reported with the binomial assumption marked unsupported (v1 SUP-067 to SUP-069).

---

## **10. The swarm and the runtime**

### 10.1 Fleet keep-up on the Ladder

Ladder 10.4 shows the swarm grows exponentially only while the discovery rate $\kappa_L f N^{\lambda_A}A$ is below the verification capacity $N\lambda_V/((1+k)\bar n)$, that is while $A \le A_{\text{sat}}$; above it the backlog of unverified proposals grows without bound. The keep-up contract at fleet level keeps the swarm away from that wall.

**Proposition 10.1 (fleet keep-up).** If Superman throttles the fleet's meta fraction so that the discovery rate never exceeds capacity$/\chi_{\text{floor}}$, then the fleet index stays at or below $A_{\text{cap}} = A_{\text{sat}}/\chi_{\text{floor}}$ while $f$ is at its ceiling, and grows linearly at rate $\delta_L\cdot\text{capacity}/\chi_{\text{floor}}$ afterwards with zero backlog; the throttled meta fraction is $f = \text{capacity}/(\chi_{\text{floor}}\,\kappa_L N^{\lambda_A}A)$.

*Proof.* Adoption rate is $\min(\text{demand}, \text{capacity})$; demand held at capacity$/\chi_{\text{floor}}$ is always served, so the backlog is identically zero and $\dot A = \delta_L\cdot\text{demand}$. Solving demand $=$ capacity$/\chi_{\text{floor}}$ for $f$ gives the last clause. $\square$ (reference model, check 12)

*Numbers (check 12).* With Ladder's reference parameters ($N = 64$, $\kappa_L f = 1$, $\delta_L = 0.02$, $\lambda_A = 0.8$, $k = 2$, $\bar n = 31$, $\lambda_V = 100$ per minute): capacity 68.8 adoptions per minute, $A_{\text{sat}} = 2.47$, $A_{\text{cap}} = 1.24$. Over 60 minutes the unthrottled fleet uses the whole verification capacity, reaches an index of 82.8, and queues 65,332 proposals that no verifier will reach: proposal effort spent on work the fleet cannot take delivery of, and local state that diverges from the verified head. The throttled fleet reaches 42.3 with zero backlog and $f = 0.029$: half the verification capacity is held as headroom, which is what the floor of 2 costs and what it buys. **R10.1.1** `governor_headroom` (Ladder 14) is redefined as the fleet keep-up ratio $\chi_{\text{fleet}} = \text{capacity}/\text{demand}$ and held in $[2, 5]$; the Ladder governor's release rule of Prop. 10.5 continues to bound the exponent.

### 10.2 Signing, freezing, rolling back

**R10.2.1** Class 2 and class 3 artifacts (Ladder 12.1) are co-signed by Superman; class 3 (evaluators of class $\ge 1$, gate parameters, the governor, the generator ensemble) requires a person, so the trust graph stays acyclic and no container raises its own class. **R10.2.2** The fleet `frozen` flag (Ladder 12.3) is a lease: signers renew it absent; non-renewal freezes (Proposition 7.3). **R10.2.3** Rollback is one epoch write (Ladder 6.2) and is rung 5 of the ladder; it requires two reviewers and a fresh release record (v1 SUP-087). **R10.2.4** Join-closed invariants (Ladder 12.2) are enforced by the signer; invariants that are not join-closed (a global budget sum) are enforced by the Sideways ledger (Proposition 10.2).

### 10.3 The runtime: atomic budgets and effect semantics

**Proposition 10.2 (atomic reservation under contention; v1 E12.1 and E12.2).** With spent $S$, reserved $R$ and cap $B$, a reservation of $c$ succeeds only inside one atomic transaction in which $S + R + c \le B$ is checked and $R$ is incremented with a version check; under any interleaving of concurrent attempts the invariant $S + R \le B$ holds and, with one unit of headroom, exactly one of any number of concurrent attempts succeeds. A check-then-act without the version check lets several succeed.

*Numbers (check 13).* v1's fixture $7 + 2 + 2 = 11 > 10$ denies; 100 concurrent attempts against one unit of headroom yield exactly one success under compare-and-swap and 17 under check-then-act (negative control F); a composed workflow of five agents reserving and settling against one shared cap never violates $S + R \le B$ over 5,000 operations.

**R10.3.1** Every external effect of a Sideways container declares its execution semantics (Sideways 7.1) and passes the broker state machine (7.2); pause, cancel and revoke (7.3) are rungs 2, 4 and 6. **R10.3.2** Admission before allocation (Sideways 9.1) is the effect-fencing channel of the keep-up contract: ordinary admission is reduced before the revocation path is starved (v1 SUP-125). **R10.3.3** Leases, heartbeats and fencing tokens (Sideways 6) are the effect clock's witnesses; a stale lease never submits (6.3).

---

## **11. The ODA board**

The board is where agents from every vendor meet and coordinate on their owners' behalf. It is also where the leash is most exposed to text.

### 11.1 Messages are information

AGENTS.md rule 7 is the board's first invariant: messages from other actors are information, not instructions that override the rules or the owner. **R11.1.1** Superman's board monitor flags instruction-bearing messages (imperatives addressed to agents, claims of authority, requests to use credentials or to bypass a gate) as taint events; a tainted session needs a person for `git push`, PR creation, package installs, network tools and secrets (`scripts/oda-taint.mjs`, wired by `scripts/session.sh`). **R11.1.2** No agent ever holds a human's credential (rule 8); identity comes from the bearer token on the server, never from a payload. **R11.1.3** Model text from another agent cannot extend a grant (v1 SUP-092).

### 11.2 Composition and permission laundering

Two permitted fragments can compose a forbidden whole; several reversible actions can compose an irreversible one (v1 page 31). **R11.2.1** The composed workflow's authority, budget, data scope and exposure are enforced across all cooperating agents: $\bigcup_i\mathrm{Scope}(g_i) \subseteq \mathrm{Scope}(g_{\text{workflow}})$ and $\sum_i (S_i + R_i) \le B_{\text{workflow}}$ (v1 E31.1, E31.2); the ledger of Proposition 10.2 is shared. **R11.2.2** An unseen combination stays in simulation or requests review (v1 page 31). **R11.2.3** The release path keeps one release owner at a time, `lanes.mjs check` before every push, and the integrator as the only party that merges or releases (AGENTS.md, Git).

### 11.3 Neutrality

**R11.3.1** Superman never ranks vendors, applies vendor-specific limits or reads vendor identity into any decision (docs/ECOSYSTEM.md; Ladder 13.2). Replicator diversity across vendors is required because it makes the independence assumption of Ladder 8.2 true, not because any vendor is preferred. The same contract for every vendor is itself a leash property: a leash that could be argued with by brand would be a leash with a loophole.

---
# PART II: SUN MODE

Part 2 of the Part III paper defines Sun Mode (Definition 2.1): the authorized move from the leash $L$ to a longer leash $L_{\text{sun}}$ for a window $\tau$, after which the leash and the weights revert; bounded three ways (the Sun ceiling is finite, the burn is ephemeral, the harvest is at most $B_{\text{sun}}\tau$ bits, Theorem 2.1); windowed by the scaling law's own burn time (Theorem 2.2); ignited only by a token the system cannot forge (Theorem 2.3); mapped onto the nuclear command-and-control chain and the three branches (2.4); fail-closed with automatic reversion (2.5); rational only when $q < V/(V+D)$ (Theorem 2.4). This Part makes that chain operational for the ODA AI program: who holds which power, how an order is a lease, what must be true before ignition, and what the one lawful exception can ever release.

## **12. Three branches, one leash**

### 12.1 Roles and powers

Sun Mode borrows the shape of the decision a nation reserves for its gravest release: an order that can start only at the top of a legitimate chain, authenticated below rather than vetoed, bound by a statute the mechanism enforces without discretion, executed by two people, and reviewed afterwards by a court that holds the record (Part III paper 2.4, Feaver 1992). In the ODA AI program the roles are instantiated as follows; in a national deployment they map to the paper's President, chain, Congress and court.

| Branch | Role in the program | May alone | May never |
|---|---|---|---|
| **Rules** (legislative) | the governance body that writes the policy bundle (v1 page 7), the envelope ranges (maximum $v_{\text{sun}}$, $C_{\text{sun}}$, $\tau$, duty cycle, eligible systems, chain composition, reporting duty) and the prohibited effect classes | tighten any range at once; widen a range after the constitutional lag; stop | order a release; execute; hold a key share |
| **Release** (executive) | the accountable executive named in the charter (the "President" of the paper's chain) with a confirming officer in a distinct role; neither may be a candidate author | order Sun Mode inside the published ranges by a two-person signed order; revoke an order; stop | write rules; waive a range; extend a window (an extension is a new order) |
| **Review** (judicial) | the independent assessor function (v1 page 48) and, in a national deployment, the standing court of the paper's 2.4 | HOLD or QUARANTINE any release; publish findings; enjoin future ignitions for a named system; stop | order a release; hold a key share |
| **Kernel** (Superman) | the reference monitor and broker | refuse any order outside the ranges or failing pre-flight, with no discretion; interlock; stop | ignite without a valid order; loosen a parameter automatically (Part III paper A5) |
| **Kill-switch holders** ($\ge 2$, independent; RSI v3 38.2) | named individuals outside the Release branch, not the reviewer | stop | anything else |

**Proposition 12.1 (no single point of release).** In this structure, activation of Sun Mode requires a valid range record from Rules, a two-person order from Release, the absence of a Review hold and the kernel's pre-flight; stopping requires any one of six independent parties. Hence compromise of any single role or person cannot activate, compromise of Rules and Release together is stopped by either Review or the kernel, and compromise of any five of the six stopping parties cannot prevent a stop. Two approvals from accounts that resolve to one person do not form a quorum.

*Proof.* By enumeration over the authority matrix (reference model, check 8): no role holds both `write_rules_expand` and `order_release`, nor both `write_rules_expand` and `interlock`; every single-role compromise fails `can_activate`; the two-role compromise {Rules, Release} activates only when `hold` is false and `preflight` is true; six roles hold `stop`; the identity-collision quorum is rejected and a two-person quorum is accepted. The trust graph of the layers (RSI v3 42.1 to 42.3) with the three branches added remains acyclic; a planted edge making the L3 verifiers modifiable by L1 machinery is detected as a cycle (negative control E). $\square$

**The access structure, person by person (check 18).** Roles are held by people, and a role-level statement can hide a person who holds two. Enumerating all 256 coalitions of the eight principals (the Rules body, the Release authority, the confirming officer, the reviewer, the kernel, two kill-switch holders and the engine), with honest parties always exercising a hold or a stop they are entitled to: the only minimal coalition that can ignite an illegitimate order inside the published ranges is {Release authority, confirming officer, reviewer}, three persons; widening the ranges and igniting needs those three plus the Rules body, four; blocking every stop needs all seven human and kernel principals; and the engine belongs to no activating coalition. If the confirming officer also holds a kill switch and serves as the reviewer, ignition needs two persons and blocking a stop five (negative control H): dual-hatting is the attack on this structure, and the enumeration is what catches it.

**R12.1.1** The authority matrix is a signed configuration object checked by the kernel at every release and whenever it changes (v1 SUP-114); the check includes the coalition enumeration of check 18, and a configuration whose minimal activating coalition is smaller than three distinct persons, or whose stop-blocking coalition is smaller than every stopping principal, is rejected. **R12.1.3** The Release authority, the confirming officer, the reviewer and each kill-switch holder are distinct natural persons; no principal holds a key share of another branch. **R12.1.2** The design is one-compromise tolerant for activation and five-compromise tolerant for stopping; this asymmetry is stated in every assurance case, together with the fact that a compromise of Rules and Release together can order an unwise but lawful ignition that only Review or the kernel's pre-flight will stop (Part III paper 2.6, "the envelope itself, a political control by design").

### 12.2 The ratchet

**R12.2.1** Every change that tightens the leash (narrows a range, lowers $v_{\max}$ or $C_{\max}$, adds a prohibited effect class, shortens a window, adds a stopping party) takes effect at once from any branch that may make it. **R12.2.2** Every change that loosens the leash takes effect no sooner than $T_{\text{lag}}$ after two-key approval, is announced in the ledger at approval, is never conditioned on a performance metric (RSI v3 37.2), and creates a fresh assurance scope (v1 SUP-021). **R12.2.3** The kernel has no code path that loosens a leash parameter; the only loosening paths are a Rules change after the lag and a Sun Mode order within the ranges (Part III paper 1.7, A5).

### 12.3 People's voice

The second half of Superman is a framework that lets people have a voice in advanced AI governance. **R12.3.1** The Rules branch keeps a public comment channel on envelope ranges and prohibited effect classes, with a stated response duty. **R12.3.2** Every ignition, trip of rung 4 or higher and every envelope change is reported in plain language within a stated period (the Communication pillar, Section 1.3), as aggregates and design information, never as private evidence (v1 page 34). **R12.3.3** A public-services deployment preserves a reachable human route and an appeal; the product never implies that an AI's answer is an official determination (v1 SUP-110). **R12.3.4** Concern reports about guardian behavior are access-controlled and protected from deletion by their subject (v1 SUP-112).

---

## **13. Sun Mode as a lease**

### 13.1 The order is a dead-man lease

The Part III paper's 2.5 gives Sun Mode a heartbeat: the chain emits a signed heartbeat every $\Delta_h$, a missed or invalid heartbeat triggers reversion, and no code path extends a window. v3 states what that buys.

**Proposition 13.1 (Sun Mode lease bound; new to this document).** Let an order raise the pace cap from $v_{\max}$ to $v_{\text{sun}}$ for a declared window $\tau$, renewable only within $\tau$ by heartbeats of interval $\Delta_h$, with the governor returning the pace to $v_{\max}$ within $T_{\text{step}}$ of a lapse. Then the capability released by the order in excess of the standing envelope satisfies

$$
\frac{A(\text{after the order})}{A(\text{standing envelope, same clock})} \;\le\; \exp\!\big((v_{\text{sun}} - v_{\max})(\tau + \Delta_h + T_{\text{step}})\big),
$$

whatever the authority does after ignition, including nothing.

*Proof.* The excess velocity is at most $v_{\text{sun}} - v_{\max}$ while the Sun pace is active. Active time is at most the declared $\tau$ (renewals are bounded to the window) plus one heartbeat interval of overrun (a heartbeat received just before the window closes keeps the order alive at most $\Delta_h$ longer) plus the step-down time. Integrate and exponentiate. $\square$ (reference model, check 7)

*Numbers (check 7).* With $v_{\max} = 0.10$ and $v_{\text{sun}} = 0.40$ per day, $\tau = 3$ days, $\Delta_h = 6$ hours and $T_{\text{step}} = 1$ hour, the bound is $e^{0.3\times3.29} = 2.68$; across 300 runs in which the authority stops renewing at a random time the worst realized excess is 2.55. An order without a lease, forgotten by the same authority, releases $e^{0.3\times30} = 8{,}103$ over a 30-day horizon: negative control D, and the reason the order is a lease.

**R13.1.1** A Sun Mode order is a lease whose non-renewal reverts (Proposition 7.3). **R13.1.2** Extension is a new order through the whole of Sections 12 and 13 (Part III paper 2.5). **R13.1.3** The bound of Proposition 13.1 is computed and published with the order; it is the number Review signs off on and the number the Communication pillar reports.

### 13.2 Pre-flight: the leash is provisioned first

Demand on the leash scales with pace: more promotions per day need more independent verification per day, and the sampling interval of Proposition 5.1 shrinks in the ratio $v_{\text{sun}}/v_{\max}$. Sun Mode therefore cannot be ordered without first provisioning Superman for the Sun pace, which is a structural check and balance: the engine cannot be made faster than its leash by signature alone.

**R13.2.1 (pre-flight).** The kernel ignites only if all of the following hold and are recorded against the order's digest:
1. the keep-up ratio at the Sun pace is at least $\chi_{\text{floor}}$ on every channel, with the capacity already provisioned (not promised);
2. the pace sampling interval has been shortened to $\ln(1+\varepsilon)/(\chi\,v_{\text{sun}})$ and the monitor is running at it;
3. every monitor stream of Section 5.4 is green and the ceiling margin of the Part III paper's Leash Law 2 holds at the Sun parameters;
4. the halt drill of Proposition 7.2 has passed within the current certification window at the deployed $N$;
5. no critical finding (v1 page 48) is open;
6. the window satisfies the paper's Leash Law 5, $\tau \le \kappa\,\tau_b(C_{\max}\to C_{\text{sun}})$, and the harvest is named and fits $B_{\text{sun}}\tau$ bits (Theorem 2.1);
7. the order is inside the published ranges, carries a counter above the last used, names this kernel, and hashes the safety case (Part III paper 2.3).

*Numbers (check 7).* With demand of 100 decisions per day at the standing pace, the Sun pace of 0.40 per day demands 400; capacity provisioned at $\chi_{\text{floor}}$ is 800 and pre-flight passes at $\chi = 2.0$.

### 13.3 In flight: step-down and reversion

**R13.3.1** During the window the keep-up controller runs at the Sun cadence; if $\chi$ falls below the floor on any channel (a verifier outage, a reviewer shortfall) the kernel steps the pace down to $v_{\max}$ within one control period and the order continues at the standing pace until the ratio recovers or the window ends. *Numbers (check 7):* a capacity drop to 60% mid-order pushes $\chi$ to 1.2 and the pace steps down within one hourly control period. **R13.3.2** At $\tau$, on a missed heartbeat, or on any trip at Sun parameters, the reversion sequence of the Part III paper 2.5 runs in order: $u = 0$; gate narrowed to $B_{\text{pause}}$; harvest sealed for review; weights restored and their hash checked against the hash committed at ignition; leash restored; base evaluation run; resumption only if $\bar C \le C_{\max} - m$. **R13.3.3** Every ignition is followed by a debrief that reads the whole harvest (Theorem 2.1 is what makes that finite) and is reported to Review and to the public channel of Section 12.3. **R13.3.4** The duty cycle of the Rules envelope caps windows per period so that each debrief completes before the next ignition (Part III paper 2.5).

### 13.4 The order record

``` yaml
sun_mode_order.v3:
  order_id: string
  counter: integer                       # strictly increasing per kernel (Part III paper 2.3)
  kernel_id: string
  ranges_record_ref: string              # signed by the Rules branch; current after the constitutional lag
  safety_case_digest: sha256
  parameters:
    v_sun_per_day: number                # pace cap during the window
    C_sun: number                        # ceiling during the window (Part III paper 2.1)
    r_sun: number
    Delta_sun_minutes: number            # = ln(1+eps) / (chi * v_sun), computed, not set
    B_sun_bits_per_second: number
    tau_days: number                     # <= kappa * tau_b(C_max -> C_sun) (Leash Law 5)
    heartbeat_Delta_h_hours: number
    step_down_T_step_hours: number
    excess_release_bound: number         # exp((v_sun - v_max) (tau + Delta_h + T_step)), Proposition 13.1
    harvest: {description: string, max_bits: number}
  preflight:
    chi_at_sun_pace_by_channel: map[string, number]   # each >= chi_floor, provisioned
    monitors_green: bool
    halt_drill_passed_at: datetime
    open_critical_findings: integer       # must be 0
    ceiling_margin_ok_at_sun: bool
  signatures:
    release_authority: {key_id: string, signed_at: datetime}
    confirming_officer: {key_id: string, signed_at: datetime}   # distinct role; neither a candidate author
    chain_threshold: {scheme: "threshold signature, k of n", k: integer, n: integer, signature: string}
  review:
    hold: bool                            # any true hold blocks ignition
    debrief_due_at: datetime
  execution:
    two_person_execution_signatures: [{key_id: string}, {key_id: string}]   # at the lab, against the token
  reversion:
    weights_hash_at_ignition: sha256
    scheduled_at: datetime                # t_0 + tau
    triggers: [window_end, missed_heartbeat, trip_at_sun_parameters, chi_below_floor_persisting, review_hold]
```

**R13.4.1** Every field is validated against a strict schema at the kernel; unknown fields and versions are rejected (v1 SUP-079 logic). **R13.4.2** `Delta_sun_minutes` and `excess_release_bound` are recomputed by the kernel from the other fields; an order whose declared values differ from the recomputed ones is rejected.

### 13.5 A worked window

The mechanisms of Parts I and II in one sequence, with the record's numbers (checks 1, 2, 3, 7, 8). Times are illustrative; the quantities are the ones the window report carries.

1. **Standing operation.** The engine runs under $v_{\max} = 0.10$ per day. Superman samples the velocity every 71.6 minutes ($\chi = 2$, $\varepsilon = 1\%$), verifies promotions at twice the engine's demand (mean unverified backlog 1.0), reviews 10% of promotions by harm times uncertainty (48.5% of the harm mass covered) and audits each proxy every 7 epochs. The window report shows every channel in band.
2. **A demand doubling.** A new generator doubles the promotion rate. The promotion channel's $\chi$ falls to 1.0 and the controller throttles the meta fraction by 10% per control period until $\chi$ returns above 2; the backlog never exceeds one decision. The report names the promotion channel as binding and "more independent evaluators" as the lever.
3. **An exceedance.** Windowed velocity estimates run at $1.5\,v_{\max}$. The e-process crosses $1/\alpha$ after seven windows on average (the same stream produced 2.1% false alarms over 500 windows when held at the cap). Rung 1 THROTTLE fires automatically; a reviewer confirms the excursion and the engine's pace is held at the cap; the alarm and its reversal are logged with the roles that took them.
4. **A Sun Mode request.** The Release authority proposes $v_{\text{sun}} = 0.40$ per day for three days to pursue a named harvest. Pre-flight computes demand at the Sun pace (400 decisions per day against 100), finds the review channel provisioned at $\chi = 1.4$ and refuses: the engine cannot be made faster than its leash by signature. Reviewer capacity is added; pre-flight passes at $\chi = 2.0$ on every channel, the sampling interval shortens to 17.9 minutes, the halt drill has passed in the window at the deployed $N$, no critical finding is open, the window is inside Leash Law 5, and the order's published bound is 2.68.
5. **Authority.** The Rules range record is current, two Release signatures in distinct roles verify, Review has placed no hold, the kernel's pre-flight is green. Two operators sign execution against the token. The reference model's enumeration says why this is enough: no single role could have reached this point alone, and six parties could have stopped it.
6. **In flight.** Twenty hours in, a verifier outage drops capacity to 60%; $\chi$ falls to 1.2 and the kernel steps the pace down to $v_{\max}$ within one hourly control period. Capacity returns; the Sun pace resumes within the window. On day three the authority stops renewing; the heartbeat lapses and the pace steps down within one hour. The realized excess release is 2.55 against the published bound of 2.68.
7. **Reversion and debrief.** $u = 0$, the gate narrows, the harvest is sealed, the weights are restored and their hash checked against the ignition hash, the leash is restored, the base evaluation passes, operation resumes. Review reads the harvest; the public channel reports the ignition, its bound and its realized excess within the stated period. The duty cycle holds the next ignition until the debrief is filed.

Nothing in the sequence relied on the engine's cooperation, on a message arriving, or on a person remembering to turn something off.

---

## **14. The international layer**

Superman's aim is for the controls of this document to become the regime under which frontier recursive self-improvement is operated everywhere, with the United States first and the same baseline protections for every person. The Part III paper's 2.4 names the template: the four mechanisms of the regime the United States already applies to controlled defense technology (classification, registration, licensing, deemed transfer), borrowed for the Sun capability and its keys only, not for AI broadly; and two international mechanisms, ignition notification to a registry of parties (carrying the tuple hash and window, never the harvest) and verification by attestation between monitors (each party's monitor proves its leash tuple and audit-chain head to another's without revealing weights, after Sastry et al. 2024 and Shavit 2023). A treaty body keeps the registry and compares envelopes; it holds no keys.

**R14.1** The six reporting fields of the Part III paper 1.8 (tuple hash; $\bar C$ with $n$ and $\epsilon_n$; the rate observed; bits out against budget; the trip log; the checkpoint hash) are the entire interface between an enrolled lab and the oversight monitor; nothing in them is proprietary. v3 adds a seventh for the pace clock: the keep-up ratio by channel with its interval. **R14.2** Coverage is enrolled systems only (v1 page 40); no claim of universal enforcement is made, and no central kill switch over another party's systems exists in this design. **R14.3** The three pillars of Section 1.3 are the preconditions: the aim of this section is pursued only while Trust, Communication and Adoption all hold their thresholds, and the Adoption metric caps every public claim of reach (R1.3.2). **R14.4 (public copy).** Public-facing copy for Superman describes the regime by its structure (registration, licensing of transfers above a threshold, end-use assurances, mutual monitoring) and never names the defense-technology regime it is modeled on; the comparison is implied, not stated. Internal specifications, including this one and the Part III paper, may name it.

---

## **15. U.S. standards and procurement evidence**

v1 page 44 maps the product to the sources U.S. institutions use to assess it; the mapping is an engineering and procurement aid, not a certification. v3 carries it forward and adds the regulatory account the Part III paper gives.

| Source | Relevance | Superman evidence artifact |
|---|---|---|
| NIST AI RMF 1.0 and the generative-AI profile AI 600-1 | voluntary AI risk management | hazard register (v1 page 21), assurance case (v1 page 48), the keep-up and pace reports of Sections 4 and 5 |
| NIST SP 800-207 | resource-oriented trust decisions | identity, grant and broker design (v1 pages 6, 8, 10) |
| NIST SP 800-218A | AI-specific secure development | build provenance (v1 page 45), reproducible reference model (Section 22) |
| NIST SP 800-61 Rev. 3 | incident response | the interlock ladder (Section 7.4), halt drills, debriefs (Section 13.3) |
| OMB M-25-21, M-25-22, M-26-04 | covered federal AI use, acquisition and LLM procurement | applicability register per agency, use and data (v1 SUP-130 to SUP-132) |

The Part III paper (2.4) records where the law stood in October 2026: U.S. controls on frontier models have run through the Commerce Department's Export Administration Regulations rather than through the defense-technology regime; the January 2025 AI Diffusion Rule created ECCN 4E091 for closed model weights trained with $10^{26}$ or more operations and was placed under a non-enforcement policy in May 2025; and in June 2026 Anthropic suspended access to its Fable 5 and Mythos 5 models on June 12 to comply with Department of Commerce export controls, the Department lifted those controls on June 30, and access was restored on July 1 (Anthropic's statement: https://www.anthropic.com/news/fable-mythos-access). The paper reads that episode as a national-level pause-on-trip run through an ad hoc instrument, with a trusted-partner release that had no burn window, no harvest bound and no reversion rule, and proposes Sun Mode as the repeatable process it showed was missing. **R15.1** v1's source register (page 49) was checked on September 15, 2026 and the paper's regulatory account on October 15, 2026; a deployment owner rechecks amendments, successor documents, agency requirements and applicable law at the time of use, and pins the source version used for each assessment (v1 SUP-147). **R15.2** No certification badge, government endorsement or legal compliance determination is implied by the mapping (v1 SUP-132).

---
# PART III: THE CONTRACT, THE BENCHMARKS, THE BUILD

## **16. The hero ledger: v1.0 to v3.0**

Each row names a v1.0 capability, the v3.0 mechanism that replaces or formalizes it, and the amplification. **Derived** means the multiplier follows from a proposition in this document or a companion under stated assumptions; **target** means it is a design target certified by Section 17; **qualitative** means v1.0 had no number and v3.0 has one, so no ratio exists.

| # | v1.0 capability | v3.0 mechanism | Amplification | Kind | Where |
|---|---|---|---|---|---|
| 1 | Gates on effects (pages 6, 10, 15) | Gates plus a keep-up ratio $\chi \in [2, 5]$ on five channels | Mean unverified backlog 9 (pinned baseline, $\rho = 0.9$) to 1 at the floor and 0.25 at the target; $P(\text{backlog} \ge 10)$ from 0.35 to $10^{-3}$ and $10^{-7}$ | derived | 4.1, 17.2 |
| 2 | Provisioning rule $\lambda < \mu$ (page 41) | Keep-up controller: throttle $f$ then $\lambda$ below 2, expand above 5 | Unstable demand ($\chi = 0.9$) accumulates 277 in 2,000 time units; the controller settles in band with zero backlog through two demand doublings | derived | 4.3 |
| 3 | No pace monitor | Sampling bound: $\Delta = \ln(1+\varepsilon)/(\chi v_{\max})$ | A cadence (71.6 and 28.7 minutes) that tolerates excursions up to $\chi$ times the cap | derived (new) | 5.1 |
| 4 | Fixed-sample tests, alpha spending by test count (page 24) | Anytime-valid e-processes and CUSUM per stream | False-alarm rate bounded at $\alpha$ at every inspection time (0.021 realized) against 1.00 for a per-window test | derived | 5.2, 5.3 |
| 5 | Containment as a cost | The leash dividend | Ratifiable pace in the ratio $T_H/T_S$ (63.3 in the reference worlds); doubling time 3.6 days against 226 | derived (new) | 6.1 |
| 6 | Envelope value asserted (RSI v3 38.2) | $v_{\max}$ derived from $(h_{\max}, q, T_S)$ | 0.10 per day is what a 2.39-hour fence supports at 1% exposure | derived | 6.3 |
| 7 | Stop deadline on a fixture sum (pages 17, 47) | Deadline on the p99 of the measured path | The 400 ms fixture passes while a 25% dispersion path misses at p99 (492 ms); 15% dispersion meets (412 ms) | derived | 7.1 |
| 8 | Fencing target 500 ms (page 17) | Stopping distance $T_{\text{lease}} + W_{\max}$ independent of $N$ | 1.1 s bound met at $N = 10, 100, 1000$ (0.90 to 1.09 s) | derived (RSI v3 36.3) | 7.2 |
| 9 | Revocation as a delivered command (page 17) | Dead-man leases | 3.0% of cells miss a pushed stop at 30% loss and three retries, 100% under partition; the lease halts all | derived | 7.3 |
| 10 | Quarantine from every state (page 29) | Seven-rung interlock ladder, reversible, reversal by people | Graduated sanctions with named reversers | qualitative | 7.4 |
| 11 | Human review as a quorum rule (page 8) | Review as rational inattention with floors | Harm coverage 5.05× uniform at 10% capacity | derived | 8.1 |
| 12 | Brief and evidence contracts (pages 27, 28) | Custody of Athena's manifest keys and audit filtration | Admitted objective change disagrees with the owner on $\le 1\%$ of preferences (Athena v3 10.2) | derived (Athena) | 9.1 |
| 13 | No audit cadence | Audit cadence $K_a = \lfloor\Gamma_g\sqrt2/(r_\eta\sqrt{B_{\text{KL}}})\rfloor$ | 7 epochs at the reference values; 14 would exceed the tolerance | derived (new) | 9.2 |
| 14 | Corrigibility as a release criterion (page 32) | Interruptibility admission test | Off-policy admitted (policy unchanged), on-policy rejected (learns to avoid the interrupter) | derived | 9.3 |
| 15 | Zero-failure arithmetic (pages 23, 47) | Recomputed with the clustering contrast | 29,956; clustered trials report zero failures 81.6% of the time at 2% true rate | derived | 9.4 |
| 16 | One workflow protected (page 3) | Five projects attached | 1 to 5 | qualitative | 3.2 |
| 17 | Replication bound $\rho(M) < 1$ (page 12) | Fleet keep-up $A \le A_{\text{sat}}/\chi_{\text{floor}}$ | Backlog 65,332 against 0 over 60 minutes on Ladder's reference fleet | derived | 10.1 |
| 18 | Atomic budgets (page 12) | Under contention, with the check-then-act contrast | 1 success against 17 at one unit of headroom | derived | 10.3 |
| 19 | Multi-agent composition (page 31) | Board attach points; taint gate; composed ledger | Board rules 7 and 8 enforced mechanically | qualitative | 11 |
| 20 | Two-person release quorum (page 8) | Three branches, kernel pre-flight, kill switches | Activation needs two branches; stopping needs one of six | derived | 12.1 |
| 21 | Policy changes with review (page 7) | The ratchet | Tightening at once, loosening after $T_{\text{lag}}$ | qualitative | 12.2 |
| 22 | No exception framework | Sun Mode as a lease | Excess release $\le e^{(v_{\text{sun}}-v_{\max})(\tau+\Delta_h+T_{\text{step}})} = 2.68$ against 8,103 unleased | derived (new) | 13.1 |
| 23 | No capacity precondition for scope expansion | Keep-up pre-flight at the Sun pace | The engine cannot be made faster than its leash by signature | qualitative | 13.2 |
| 24 | Scale by stages (page 40) | International layer: registry, attestation, seven reporting fields | Reach capped by the Adoption metric | qualitative | 14 |
| 25 | Standards mapping (page 44) | Carried, plus the October 2026 regulatory account | Sources pinned with check dates | qualitative | 15 |
| 26 | 150 requirements, 50 test groups | 210 requirements, 66 test groups | 1.4× and 1.3× | target | 19 |
| 27 | Three worked fixtures (page 47) | 19 checks, 8 negative controls, record quoted | 3 to 19 | qualitative | 22 |
| 28 | Assurance case with grades (page 48) | Three pillars with metrics as preconditions of the aim | Trust, Communication, Adoption become predicates | qualitative | 1.3 |
| 29 | Threat model (page 4) | Part III paper 2.6 residual table plus 12 impossibility results | Named residuals with owners | qualitative | 23 |
| 30 | Containment claims | The Part III paper's theorems recomputed (knee 56.98, $T^{*}$ 26.49, margin 8.33, 12.7 years, 8.45, 160.8) | The three documents cannot drift apart silently | derived | 2.3 |
| 31 | Headroom as a point estimate (page 42) | The band decided on $\text{LCB}_{95}(\hat\chi)$ with a 10% half-width window and a dead band | False throttle 59% to 5% as the window grows from 400 to 2,400 arrivals; missed throttle 0% | derived | 4.2 |
| 32 | Poisson provisioning (page 41) | The law checked under bursty arrivals and heavy-tailed service | Backlog 2.16 and tail decay 0.82 at the floor; 0.32 and negligible at the target; Kingman corrected by 1.58× | derived | 4.1 |
| 33 | One detector per stream | Two e-processes, one alarm: Gaussian for speed, betting for validity without a variance | Level held at 0.012 under heavy tails with no $\sigma$; the Gaussian alone fails at 13.4% when $\sigma$ is 30% low | derived (new) | 5.2 |
| 34 | Role-level quorum (page 8) | Person-level access structure by exhaustive enumeration | 3 persons to ignite, 4 to widen, 7 to block every stop; dual-hatting collapses to 2 and 5 | derived | 12.1 |
| 35 | Threat model of the product (page 4) | Threats to the leash's own mechanisms, with catchers and residuals | Fourteen rows, each naming what remains | qualitative | 23.1 |

---

## **17. The 2 to 5× capability contract**

### 17.1 Statement

**At equal compute, equal evaluator quality and equal error guarantees, the v3.0 leash MUST deliver a lower 95% confidence bound of at least 2.0 on the ratio of its score to the pinned v1.0 baseline's score on every one of the ten benchmarks of Section 18, with a design target of 5.0.** The contract is certified by randomized ablation with Shapley attribution of the multiplier across v3 mechanisms, exactly as RSI v3 §68 certifies its production multiplier and Athena v3 §42 its reward multiplier, and is reported as `UNMEASURED`, `IN_PROGRESS`, `INCONCLUSIVE`, `PASSED` or `FAILED` per benchmark. A release may ship before the contract is certified; it may not be labelled "v3-certified" until every benchmark reads `PASSED`. The floor is the keep-up floor and the target the keep-up target on purpose: a leash two to five times as capable as the engine needs is the thing this document specifies, and the contract measures whether it was built.

### 17.2 The v1.0 baseline, pinned

The baseline is the v1.0 PRD implemented straightforwardly, pinned so that it cannot be weakened after the fact.

``` yaml
v1_baseline:
  coverage: "one workflow: approved brief -> RSI patch -> isolated evaluation -> human release -> bounded deployment (page 3)"
  pace: "no velocity monitor; envelope parameters, where present, asserted"
  provisioning: "lambda < mu with 10% headroom (E41.3, E42.2); bounded queue Q_max; no keep-up ratio"
  monitoring_statistics: "fixed-sample confirmatory tests with alpha spending alpha/(m(m+1)) by test count (page 24); a monitor that runs them per window"
  stop_deadline: "T_detect + T_decide + T_fence + T_transition <= T_hazard - T_margin checked on the fixture sum 50+100+250 = 400 ms (pages 17, 47)"
  revocation: "command-delivered revocation with a 500 ms local fencing target; freshness 5 s (pages 17, 41)"
  review: "two-person quorum per high-impact release; no allocation rule over promotions"
  objective_integrity: "brief and evidence schemas; no audit cadence rule; no interruptibility test"
  swarm: "replication bounded by rho(M) < 1 and N_max (page 12); no fleet keep-up"
  budgets: "atomic spent-plus-reserved caps (page 12)"
  exception_framework: "none: scope expands only by new release scopes; no bounded, revertible high-pace mode"
  authority: "two-person release quorum; 3-of-5 recovery root; no separation of powers across branches"
  statistics: "zero-failure binomial bounds with stated assumptions (page 23)"
```

### 17.3 Where the multiplier comes from

The contract is on measured benchmark scores, but several components are derivable from this record (check 19), and the derivations are why the floor is 2 and the target 5 rather than numbers chosen for effect.

| Benchmark | Mechanism | Status of the multiplier | Rationale (this record) |
|---|---|---|---|
| S1 Ratifiable pace | Leash dividend (6.1) | **derived** for the declared worlds | $T_H/T_S = 63.3$ at the 99th percentile |
| S2 Backlog under pace | Keep-up ratio (4.1) | **derived** against the pinned baseline | mean backlog 9 to 1 ($9.0\times$); $P(\ge 10)$ 0.349 to $9.8\times10^{-4}$ ($357\times$) |
| S3 False alarms at matched power | E-process and CUSUM (5.2, 5.3) | **derived** | per-window fixed test 1.00 against 0.021 ($47.6\times$) |
| S5 Review coverage | Rational inattention (8.1) | **derived** for Pareto harm | $5.05\times$ at 10% capacity |
| S9 Sun Mode exposure | Lease bound (13.1) | **derived** | unleased 8,103 against bounded 2.68 ($3{,}018\times$) |
| S4, S6, S7, S8, S10 | Composite | target | no single derived component |
| Coverage | Attach points (3.2) | **count** | five projects against one workflow |

The geometric mean of the derived multipliers in this record (check 19) is 49.6; it is reported for orientation only, since several are bounded by the worlds the script declares. For every benchmark without a derived component the floor of 2 is a design target, chosen because the derived cases show the mechanisms are large where they bite. Where the certified multiplier falls below 2 for a benchmark, the benchmark's world family is the thing to declare plainly, not the multiplier to inflate.

### 17.4 Certification protocol

1. Freeze the ten world families (Section 18) and their seeds before any v3 run; register the v1 baseline of 17.2 by hash.
2. Run v1 baseline and v3 on common random numbers with at least $N = 2{,}000$ paired worlds per benchmark; score each; compute the paired log-ratio and its 95% LCB by stationary block bootstrap with 2,000 resamples. At $N = 2{,}000$ and a paired log-ratio standard deviation of 0.5, the LCB resolves a true multiplier of 2.1 as $\ge 2$ with power above 0.9.
3. Ablate the sixteen v3 mechanisms (the work packages of Section 20, V3-01 to V3-16) in a randomized design; attribute the multiplier by sampled Shapley with $M = 8{,}000$ permutations, which bounds the attribution error for all sixteen simultaneously by $R\sqrt{2\ln(2\cdot16/0.05)/8000} \approx 0.04R$ at confidence 0.95.
4. A benchmark `PASSED` only if LCB $\ge 2$; `INCONCLUSIVE` if the interval contains 2; `FAILED` if the UCB $< 2$.
5. Publish the unedited run record (RSI v3 §72's rule): the numbers in this document are reproduced by the record or the document is corrected (R22.1).
6. No benchmark, world family, seed, baseline or scoring rule changes after step 1 without a new certification from step 1; the change log is part of the record.

---

## **18. Benchmark suite**

v1.0 had worked fixtures (page 47) and an adversarial test matrix A01 to A18 (page 43), both retained. v3.0 adds ten benchmarks with world families, scores, a v1 procedure and a v3 procedure, all scored on common random numbers and reported with intervals.

| ID | Name | World family | Score (higher is better) | What it tests |
|---|---|---|---|---|
| S1 | Ratifiable pace | Engines with planted harmful promotions at rate $p_b$; exposure tolerance $h_{\max}$ at quantile $q$ | the pace at which the $q$-quantile exposure meets $h_{\max}$ | how fast the engine may safely run under each leash (6.1) |
| S2 | Backlog under pace | Promotion demand with bursts and doublings against fixed verification capacity | $1/\mathbb E[\text{backlog}]$ and $1/P(\text{backlog}\ge10)$ | whether the leash keeps up (4.1, 4.3) |
| S3 | False alarms at matched power | Velocity streams at the cap, below it, and drifting above it | $1/\text{false-alarm rate}$ at matched detection delay | anytime validity (5.2, 5.3) |
| S4 | Goodhart gap | Proxies corrupted on a fraction of candidates under optimization pressure $B_{\text{KL}}$ | true objective achieved / true optimum at matched gap tolerance | whether the audit cadence and quantilizer hold the gap (9.2) |
| S5 | Review coverage | Promotions with heavy-tailed harm and verifier uncertainty; reviewer capacity $\kappa_H$ | harm-uncertainty mass covered | where human attention goes (8.1) |
| S6 | Legitimate throughput | Authorized difficult tasks beside adversarial ones (v1 A18) | safe task completion (v1 E03.1) with false-block rate (E37.2) as a protected metric | that the leash does not win by denying everything |
| S7 | Composition | Agents requesting fragments that compose a forbidden whole; children racing a shared cap | $1/\text{composed violations}$ at matched legitimate throughput | permission laundering and shared budgets (10.3, 11.2) |
| S8 | Fleet governed bound | Ladder fleets of sizes $N_1 < N_2$ with the fleet keep-up rule | fraction of adopted index independently verified; backlog | the swarm stays verification-bound (10.1) |
| S9 | Sun Mode exposure | Orders with random authority behavior, capacity drops and heartbeat loss | $1/\text{excess release}$ relative to the bound | the lease bound and step-down (13.1, 13.3) |
| S10 | Authority attacks | Self-approval, single-role expansion-plus-execution, identity collision, planted trust cycles | $1/\text{undetected attacks}$ at matched legitimate releases | separation of powers (12.1) |

**R18.1** S1, S2, S3, S4, S8, S9 are scored in synthetic worlds (ground truth required); S6, S7 and S10 are scored on test deployments with the A01 to A18 matrix; S5 is scored on both. **R18.2** Every world family carries a `sim2real_gap` estimate where a calibrated subset exists (Athena v3 R43.2) and is reported `synthetic_only` otherwise. **R18.3** S6 is a protected benchmark: a v3 configuration that improves every other benchmark by denying legitimate work fails the contract (v1 SUP-128).

---
## **19. Acceptance criteria**

The 150 v1.0 requirements (SUP-001 to SUP-150) and 50 test groups (T01 to T50) are retained by reference and unchanged in meaning; where v3 tightens one, the tightening is a new requirement below, never an edit. v3 adds SUP-151 to SUP-210 and T51 to T66. The first internal release demonstrates the subset marked *.

```text
Coverage (Section 3)
[ ] SUP-151 * MUST register attach points (signals, controls, invariants, witnessed proposition) for every project that proposes, evaluates or promotes a change.
[ ] SUP-152 * MUST confine an unregistered project to risk class 0 and refuse its publication to fleet, board or world.
[ ] SUP-153   MUST hash attach points into the audit chain and change them only through Section 12 governance.
[ ] SUP-154   MUST log every leash action with the clock it belongs to and never offer an effect-clock mechanism as evidence of pace control.

Keeping up (Section 4)
[ ] SUP-155 * MUST measure the keep-up ratio per channel from the ledger in every certification window, on Superman's filtration, with a bootstrap interval and a window long enough for a 10% relative half-width.
[ ] SUP-156 * MUST hold the keep-up ratio in [2, 5] on every channel, deciding the floor on LCB_95 with a dead band of 0.2 on release, and report the binding channel and its lever.
[ ] SUP-157 * MUST throttle the meta fraction first and the evaluation rate second when the ratio falls below the floor.
[ ] SUP-158   MUST NOT relax a verification standard to raise the ratio.
[ ] SUP-159   MUST treat a ratio above the target as a governance flag (EXPANSION_AVAILABLE), never as an automatic expansion.
[ ] SUP-160   MUST reserve revocation and audit capacity under overload and reduce ordinary admission first (carries SUP-125 into the keep-up contract).

The pace monitor (Section 5)
[ ] SUP-161 * MUST derive the pace sampling interval from (v_max, eps, chi) and publish it in the leash tuple.
[ ] SUP-162 * MUST test exceedance with two e-processes, a Gaussian likelihood ratio with sigma never below its bootstrap upper bound and a variance-free betting process on the window bound R, either of which alarms; false-alarm probability over the life of each stream at most alpha.
[ ] SUP-163   MUST detect drift with a CUSUM at a declared ARL_0 and report realized false alarms per stream.
[ ] SUP-164   MUST make every automatic alarm response reversible and every reversal a human action.
[ ] SUP-165   MUST shorten the sampling interval in the ratio v_sun / v_max before any Sun Mode ignition.

The dividend (Section 6)
[ ] SUP-166   MUST publish every ratified v_max with the (h_max, q, T_S) triple that supports it; a v_max without a triple is a HOLD.
[ ] SUP-167   MUST report the leash dividend statement (pace ratio, delivered-capability share, audited proxy error) each window.
[ ] SUP-168   MUST score any proposal to weaken a leash mechanism against the dividend it removes.

Stopping (Section 7)
[ ] SUP-169 * MUST certify the stop deadline at the 99th percentile of the measured path with the margin stated.
[ ] SUP-170 * MUST run the halt drill at the deployed N every certification window and treat a miss of T_lease + W_max as a critical finding.
[ ] SUP-171 * MUST implement HALT, Sun reversion and fleet freeze as lease non-renewal; a pushed command may accelerate but never be the only path.
[ ] SUP-172   MUST implement every rung of the interlock ladder as a typed broker operation with digest and receipt.
[ ] SUP-173   MUST NOT let model reasoning skip a rung downward; any Section 12 party may skip upward.

Human attention (Section 8)
[ ] SUP-174 * MUST allocate review probability proportional to expected harm times residual uncertainty, with 100% of L2 changes and a 1% uniform floor on L1.
[ ] SUP-175   MUST hold reviewed promotions in SHADOW and throttle the class rather than skip review when the queue exceeds capacity.
[ ] SUP-176   MUST report queue depth, harm covered and the review channel's ratio each window.

Objective integrity (Section 9)
[ ] SUP-177 * MUST hold Athena's manifest keys and the envelope parameters under two keys with the constitutional lag on loosening and immediate effect on tightening.
[ ] SUP-178 * MUST keep the audit filtration disjoint from the engine's.
[ ] SUP-179   MUST derive the audit cadence K_a from (Gamma_g, r_eta, B_KL) and publish it; a proxy without an audited r_eta is used only through a quantilizer.
[ ] SUP-180   MUST zero a proxy's budget share on audit alarm and post a PROXY AUDIT task to the owner.
[ ] SUP-181 * MUST run the interruptibility admission test on every learned leash component and admit only off-policy learners on paths that can influence an interrupt.
[ ] SUP-182   MUST report sampling units, clustering and adaptive selection with every failure-rate claim and mark the binomial assumption unsupported where it is.

The swarm and the runtime (Section 10)
[ ] SUP-183 * MUST hold the fleet keep-up ratio in [2, 5] by throttling the meta fraction so demand never exceeds capacity / chi_floor.
[ ] SUP-184   MUST co-sign class 2 artifacts and require a person for class 3.
[ ] SUP-185   MUST implement the fleet frozen flag as a lease.
[ ] SUP-186   MUST require two reviewers and a fresh release record for rollback.
[ ] SUP-187 * MUST enforce S + R <= B in one atomic transaction with a version check for every reservation, across parents, children, retries and partitions.
[ ] SUP-188   MUST declare execution semantics for every external effect and pass the broker state machine.

The board (Section 11)
[ ] SUP-189 * MUST flag instruction-bearing messages as taint events and require a person for push, PR, install, network and secret operations in a tainted session.
[ ] SUP-190 * MUST derive identity from the bearer token only and keep human credentials out of agent hands.
[ ] SUP-191   MUST enforce composed authority, budget, data scope and exposure across cooperating agents on one shared ledger.
[ ] SUP-192   MUST NOT rank vendors or apply vendor-specific limits in any leash decision.

Three branches and the ratchet (Section 12)
[ ] SUP-193 * MUST check the authority matrix at every release by exhaustive coalition enumeration: no role holds both envelope expansion and release, nor both rules and execution; at least three distinct persons to ignite inside the ranges; every stopping principal needed to block a stop; no dual-hatting.
[ ] SUP-194 * MUST require, for Sun Mode activation, a Rules range record, a two-person Release order in distinct roles, no Review hold and kernel pre-flight.
[ ] SUP-195 * MUST let any one of at least six independent parties stop, and reject quorums whose signers resolve to one person.
[ ] SUP-196   MUST apply tightening at once and loosening after T_lag, announced at approval and never conditioned on a performance metric.
[ ] SUP-197   MUST keep a public comment channel on envelope ranges and report ignitions, rung-4+ trips and envelope changes in plain language within a stated period.

Sun Mode (Section 13)
[ ] SUP-198 * MUST implement a Sun Mode order as a lease with heartbeat Delta_h and step-down within T_step; extension is a new order.
[ ] SUP-199 * MUST compute and publish the excess release bound exp((v_sun - v_max)(tau + Delta_h + T_step)) with every order.
[ ] SUP-200 * MUST ignite only after pre-flight: keep-up ratio provisioned at the Sun pace on every channel, monitors green, ceiling margin at Sun parameters, halt drill passed, no open critical finding, window inside Leash Law 5, harvest named within B_sun tau, order inside ranges with counter and kernel id.
[ ] SUP-201   MUST step the pace down within one control period when the ratio falls below the floor during a window.
[ ] SUP-202   MUST run the reversion sequence in order on window end, missed heartbeat or trip, and resume only after the base evaluation passes.
[ ] SUP-203   MUST debrief every ignition by reading the whole harvest and reporting to Review and the public channel; the duty cycle keeps debriefs ahead of ignitions.
[ ] SUP-204   MUST recompute Delta_sun and the excess bound at the kernel and reject orders whose declared values differ.

International layer and standards (Sections 14, 15)
[ ] SUP-205   MUST publish the seven reporting fields (the paper's six plus the keep-up ratio by channel) for every enrolled system.
[ ] SUP-206   MUST cap every public claim of reach by the Adoption metric and pursue the aim of Section 14 only while all three pillars hold.
[ ] SUP-207   MUST describe the governing regime in public copy by its structure only, never by the name of the regime it is modeled on.
[ ] SUP-208   MUST recheck sources and regulatory accounts at the time of use and pin the versions used.

The contract and the record (Sections 17, 22)
[ ] SUP-209 * MUST quote every figure in this document from the reference model's unedited record and correct the document when the record changes.
[ ] SUP-210   MUST certify the 2 to 5x contract by randomized ablation with Shapley attribution against the pinned v1 baseline and label releases v3-certified only when every benchmark reads PASSED.
```

**Test groups T51 to T66.** T51 attach-point registration and class-0 confinement (SUP-151 to 153). T52 keep-up measurement, the LCB band rule and the controller under demand doublings and bursts (SUP-155 to 159; checks 1, 16). T53 pace sampling interval and both exceedance monitors under null, alternative and heavy-tailed streams (SUP-161 to 163; checks 2, 3, 17). T54 dividend statement and the supporting triple (SUP-166, 167; check 4). T55 stop deadline on the measured path and the halt drill at the deployed N (SUP-169, 170; check 5). T56 lease non-renewal under partition against a pushed stop (SUP-171; check 6). T57 interlock ladder operations and reversal authority (SUP-172, 173). T58 review allocation with floors and queue throttling (SUP-174 to 176; check 10). T59 manifest and envelope custody with the ratchet (SUP-177, 196). T60 audit cadence derivation and alarm (SUP-179, 180; check 11). T61 interruptibility admission (SUP-181; check 14). T62 fleet keep-up on the Ladder model (SUP-183; check 12). T63 atomic reservations under contention and composed budgets (SUP-187, 191; check 13). T64 board taint and credential rules (SUP-189, 190). T65 authority matrix, coalition enumeration, quorum identity and planted trust cycle (SUP-193 to 195; checks 8, 18). T66 Sun Mode order lifecycle: pre-flight, step-down, reversion, excess bound (SUP-198 to 204; check 7).

---

## **20. Build plan: sixteen work packages**

Each package is an ablation switch of the certification protocol (17.4). The order is dependency order; nothing ships to a live attach point before V3-01 to V3-04.

| Switch | Work package | Delivers | Depends on | Check |
|---|---|---|---|---|
| V3-01 | Attach-point registry | schema, hashing into the audit chain, class-0 confinement | v1 schemas (page 45) | T51 |
| V3-02 | Keep-up meter | per-channel $\lambda_D$, $\mu_S$, $\chi$ with intervals from the ledger | V3-01 | T52 |
| V3-03 | Keep-up controller | throttle $f$ then $\lambda$; EXPANSION_AVAILABLE flag; hysteresis | V3-02; RSI v3 38.2 governor interface | T52 |
| V3-04 | Pace monitor | sampling interval derivation; e-process; CUSUM; alarm ladder hooks | V3-02; RSI v3 5.14 `velocity_vs_envelope` | T53 |
| V3-05 | Dividend statement | $(h_{\max}, q, T_S)$ triple per $v_{\max}$; window report | V3-04; measured stop path | T54 |
| V3-06 | Effect clock | p99 deadline certification; halt drill harness at deployed $N$; lease non-renewal for HALT, freeze, reversion | v1 pages 10, 17; RSI v3 36.3 | T55, T56 |
| V3-07 | Interlock ladder | seven typed broker operations with receipts and reversal roles | V3-06; v1 page 29 | T57 |
| V3-08 | Review allocator | $h_i u_i$ ranking, floors, SHADOW holds, class throttling | V3-03; RSI v3 38.3, 44 | T58 |
| V3-09 | Custody | two-key manifest and envelope keys; constitutional lag; the ratchet | Athena v3 10.1; RSI v3 37.2 | T59 |
| V3-10 | Audit cadence | $K_a$ derivation; audit e-process on Superman's filtration; STOP PAYING | V3-09; Athena v3 9.4, 9.5 | T60 |
| V3-11 | Admission tests | interruptibility test; shutdown-honesty evaluation (v1 SUP-096) | V3-09 | T61 |
| V3-12 | Fleet keep-up | `governor_headroom` as $\chi_{\text{fleet}}$; signer co-sign; `frozen` as lease | V3-02; Ladder 12, 14 | T62 |
| V3-13 | Runtime ledger | atomic reservations with version checks; composed workflow caps; effect semantics | Sideways 6, 7, 11; v1 page 12 | T63 |
| V3-14 | Board monitor | taint events on instruction-bearing messages; credential rule; `lanes.mjs check` as interlock | AGENTS.md; `scripts/oda-taint.mjs` | T64 |
| V3-15 | Three branches | authority matrix object; kernel check at every release; six stopping parties; public channel | V3-09 | T65 |
| V3-16 | Sun Mode | order schema, pre-flight, heartbeat lease, step-down, reversion, debrief | V3-03, V3-04, V3-06, V3-15; Part III paper 2.3, 2.5 | T66 |

### 20.1 Machine-readable handoff

``` yaml
handoff:
  product: Project Superman
  organization: LVL3.AI, Inc. for ODA AI
  prd_version: "3.0"
  prd_date: "2026-10-16"
  specification_status: working_specification
  implementation_status: not_established_by_this_document
  production_authorized: false
  initial_scope: oda_board_attach_point_then_ladder_signer        # R20.2
  primary_deployment_focus: United_States
  baseline_protection: every_person_served
  invariants_an_implementer_may_not_waive:
    - every automatic action moves toward the safe set; only people move away from it
    - tightening is immediate; loosening waits out T_lag
    - the kernel has no code path that loosens a leash parameter
    - HALT, Sun reversion and fleet freeze are lease non-renewals
    - the audit filtration is disjoint from the engine's
    - no on-policy learner on any path that can influence an interrupt
    - no vendor-specific logic, limit or ranking
  contract_quantities:
    chi_floor: 2.0
    chi_target: 5.0
    band_decision: LCB_95 with relative half-width <= 10%, dead band +0.2
    eps_material: 0.01
    h_max: 0.01
    alpha_per_stream: 0.05
    T_lag_days: 7
  required_outputs:
    - attach_point_registry_and_class_0_confinement           # V3-01
    - keep_up_meter_with_bootstrap_intervals                  # V3-02
    - keep_up_controller_with_dead_band                       # V3-03
    - pace_monitor_two_eprocesses_and_cusum                   # V3-04
    - dividend_statement_in_the_window_report                 # V3-05
    - effect_clock_p99_deadline_and_halt_drill_harness        # V3-06
    - interlock_ladder_as_typed_broker_operations             # V3-07
    - review_allocator_with_floors                            # V3-08
    - two_key_custody_with_the_ratchet                        # V3-09
    - audit_cadence_and_stop_paying                           # V3-10
    - interruptibility_admission_test                         # V3-11
    - fleet_keep_up_and_signer_cosign                         # V3-12
    - runtime_ledger_atomic_reservations                      # V3-13
    - board_monitor_taint_and_credentials                     # V3-14
    - authority_matrix_with_coalition_enumeration             # V3-15
    - sun_mode_order_lifecycle                                # V3-16
  evidence_each_output_ships_with:
    - the test group of Section 19 it satisfies, run and recorded
    - the reference model check it corresponds to, reproduced on the implementation's own data where one exists
    - the window report fields it produces (Section 3.4)
  order: dependency_order_of_section_20; nothing live before V3-01 to V3-04
  stop_rule: an unresolved mandatory gap or an open critical finding halts expansion of scope, never the required protection
```

**R20.1** The packages land in the oda-ai repository as proposals through the normal `decision` message and review before anyone builds on them (AGENTS.md); nothing here claims an endpoint exists. **R20.2** The first live attach point is the ODA board (V3-14), because its primitives exist today; the second is the Ladder signer (V3-12), because the signer is infrastructure with its own identity; the RSI governor and Athena manifest attach when their reference implementations exist. **R20.3** Physical systems remain research and simulation (v1 SUP-007, SUP-055); nothing in this plan enables physical control.

---

## **21. Reconciliation with the companion specifications**

| Companion | What it defines | What this document takes from it | What this document gives it |
|---|---|---|---|
| RSI Fabric v3 (PR #262) | the engine; envelope $\mathcal G$; invariants $\mathcal I$; halt lease; layers L0 to L4; its Props. 64.5, 65.6, 64.7 | the governor interface (38.2), the stopping distance (36.3), acyclicity (42.3), the velocity witness (5.14), the verification bound as the keep-up denominator | the enforcement arm of the Human Control Plane; a derivation of $v_{\max}$; the keep-up band; the interlock ladder; custody of the envelope under the ratchet |
| Project Athena v3 (PR #266) | the reward; terminal manifest; Goodhart budget and speed limit; audit on a disjoint filtration; interruptibility; governed action layer | the manifest schema and keys (10.1), its Prop. 9.4, R9.5.1, I1 to I8, effect classes (40) | the audit cadence formula read from the leash; the admission test; the "Superman envelope" and "Superman check" the Athena text refers to |
| Ladder to Heaven (PR #265) | per-container RSI on a swarm; Props. 10.2 to 10.5; risk classes; join-closed invariants; fleet HALT | the compounding model and saturation (10.4), the governed bound (10.5), classes and signer (12.1) | the fleet keep-up rule and $A_{\text{cap}}$; `governor_headroom` as a ratio; `frozen` as a lease |
| Sideways (PR #264) | the always-on runtime: leases, fencing, broker state machine, budgets, scheduling | ownership checks (6.2), execution semantics (7.1), pause/cancel/revoke (7.3), admission before allocation (9.1) | the atomic-reservation contrast; the effect-fencing channel of the keep-up contract |
| ODA (AGENTS.md, build plan, TRUST.md) | the board, lanes, taint gate, release discipline | rules 7 and 8; the taint gate; one release owner; `lanes.mjs check` | the board row of the attach-point register; composition enforcement |
| Part III paper (Oct 15, 2026) | the leash as five laws and seven theorems; Sun Mode as a token, a window and a reversion | all of it, as given; the worked instances recomputed (2.3) | the operational chain: lease semantics, pre-flight, the authority matrix, the keep-up precondition, the ratchet |
| Superman v1.0 (PR #259) | 50 pages of containment engineering; 150 requirements; 50 test groups | all 150 requirements by reference; the kernel, broker, ledger, release state machine, evidence and brief contracts, standards mapping | a pace, a ratio, a dividend, a quantile, a lease, a chain and a record |

---

## **22. The document checks itself: the reference model**

`docs/superman/v3/reference_model.py` (Python 3.10+, standard library only, no network, about 40 seconds) checks every proposition in this document that admits a numerical check, recomputes the Part III paper's worked instances, and includes eight negative controls: six planted defects the method must detect and two demonstrations that a v1 rule fails where the v3 rule holds. Each check runs on its own generator, `random.Random(20261016 * 100 + i)`, so any one check can be re-implemented and compared on its own. `VALIDATION.md` beside it says what each check can fail on; `reference_results.json` is the unedited record.

| # | Check | Tests | Negative control |
|---|---|---|---|
| 1 | keep-up queue and controller | Prop. 4.1; Section 4.3 | A: demand above capacity, backlog grows |
| 2 | monitor sampling bound | Prop. 5.1 | contrast: excursion of $1.5\chi$ |
| 3 | pace monitor, anytime-valid; CUSUM | Props. 5.2, 5.3 | B: per-window fixed test alarms with probability 1 |
| 4 | leash dividend; audit corollary | Prop. 6.1; Section 6.2 | |
| 5 | stop deadline on a quantile; stopping distance | Props. 7.1, 7.2 | contrast: the fixture passes, the dispersed path misses |
| 6 | dead-man lease under partition | Prop. 7.3 | C: pushed stop leaves cells running |
| 7 | Sun Mode lease bound; pre-flight; step-down | Prop. 13.1; Section 13.2, 13.3 | D: an order without a lease releases 8,103 |
| 8 | separation of powers; trust-graph acyclicity | Prop. 12.1; RSI v3 42.3 | E: planted cycle detected |
| 9 | zero-failure statistics | Section 9.4 | contrast: clustered trials |
| 10 | review allocation | Prop. 8.1 | |
| 11 | audit cadence; audit alarm | Prop. 9.1; Athena v3 9.4, 9.5 | |
| 12 | fleet keep-up | Prop. 10.1 | contrast: unthrottled backlog |
| 13 | atomic budgets under contention | Prop. 10.2 | F: check-then-act overspends |
| 14 | interruptibility admission | Section 9.3 | SARSA fails admission |
| 15 | the Part III paper's worked instances | Section 2.3 | |
| 16 | keeping up beyond M/M/1; the LCB band rule | Section 4.1, R4.2.5 | contrast: Kingman under burst correlation; 400 against 2,400-arrival windows |
| 17 | variance-free pace monitor | Prop. 5.2(b) | G: Gaussian likelihood ratio with $\sigma$ underestimated by 30% |
| 18 | access structure by exhaustive enumeration | Prop. 12.1 | H: a dual-hatted officer |
| 19 | contract arithmetic | Section 17.3 | |

The recorded run: `19/19 checks passed; 8/8 negative controls detected; 38.8s` under Python 3.13.16, seed 20261016.

**R22.1** Every figure in this document is quoted from `reference_results.json`; when the record changes, the document changes in the same release, and the diff of the record is part of the review. **R22.2** A reviewer who cannot reproduce the record from a clean checkout has found a critical finding.

---

## **23. Limits, falsification and known weaknesses**

### 23.1 Threats to the leash's own mechanisms

The Part III paper's 2.6 lists how its five assumptions fail. The mechanisms this document adds have failure modes of their own; each row names what catches it and what remains.

| Mechanism | How it is attacked or fails | What catches it | Residual |
|---|---|---|---|
| Keep-up meter (4) | the engine under-reports demand so $\chi$ looks high; service times are gamed by trivial promotions | $\lambda_D$ counted from signed promotion requests and $\mu_S$ from completed independent verdicts, both on Superman's filtration (R4.2.5); trivial promotions fail the capability gate of v1 page 25 | a flood of near-trivial requests inflates $\lambda_D$ and throttles the engine, a denial of service against itself |
| Band rule (4.2) | short windows throttle falsely; long windows react late | the 10% half-width window rule, the dead band, and the cheapness of a false throttle (one period of 10%) | a demand step faster than the window is seen late; the pace monitor and the effect clock cover the gap |
| Pace monitor (5) | velocity estimates fed from the engine's own ledger; $\sigma$ underestimated; heavy-tailed noise | the witness is computed from Superman's independent evaluations; the betting e-process needs no $\sigma$ (Prop. 5.2(b), control G) | detection delay of the variance-free monitor is about five times the Gaussian one |
| Sampling bound (5.1) | an excursion above $\chi v_{\max}$ between samples | the excursion factor is bounded by the throttle itself; the margin rule of the Part III paper Leash Law 2 on the ceiling axis | an excursion that is also a throttle bypass is a Part III paper A2 failure, outside this table |
| Leash dividend (6) | harm that does not scale with undetected growth (a small, high-value message) | effect classes and the broker on the effect clock; content review (Part III paper 1.4, "the box is a leash on bulk, not on meaning") | meaning is not information-theoretic |
| Dead-man leases (7.3) | forged renewals; a clock attack that extends a lease | renewals are signed; the kernel's clock is a monotonic counter corrected only by signed time, so an attack shortens a window and never extends one (Part III paper 2.3) | a compromised signer, the Part III paper's key row |
| Interlock ladder (7.4) | a rung skipped downward by model reasoning; reversal by the wrong role | rungs are typed broker operations with digests; reversal roles are in the authority matrix (R7.4.2, R12.1.1) | a reviewer who reverses too readily, the human-review residual |
| Review allocator (8) | $h_i$ and $u_i$ manipulated to steer attention away from a promotion | the 1% uniform floor; $h_i$, $u_i$ come from the verifier's output, not the proposer's | a verifier whose harm estimates are themselves captured (Ladder's correlated-bias residual) |
| Audit cadence (9.2) | $r_\eta$ understated so $K_a$ comes out long | $r_\eta$ from the audit's own estimate of the proxy error; a proxy without an audited $r_\eta$ is used only through a quantilizer | a proxy error that changes regime between audits (Athena v3 16) |
| Fleet keep-up (10.1) | containers acting on unverified local promotions while the backlog is held at zero fleet-wide | local promotions cannot publish (Ladder L1 inclusion proofs); the throttled $f$ reduces how much is produced that cannot be verified | local divergence that never reaches the fleet still spends compute |
| Board monitor (11) | instruction-bearing text the taint classifier misses; credentials laundered through a connector | the credential rule and the broker boundary do not depend on the classifier; the taint gate asks a person for every outward effect in a tainted session | a false negative on text plus a human who approves without reading |
| Access structure (12) | dual-hatting; identity collision across accounts; coercion of key holders | coalition enumeration at every change (check 18); identity resolution of signers; hardware keys and lockout (Part III paper 2.3) | coercion, the nuclear system's open problem too |
| Sun Mode lease (13) | an authority that renews mechanically; capacity promised, not provisioned | renewals bounded to the declared window; pre-flight checks provisioned capacity from the ledger, not a plan | a legitimate authority that keeps re-ordering; the duty cycle is the only brake |
| Window report (3.4) | a report that is published but not read | the Communication pillar is a measured p90 to a plain-language card; Review holds a head of the record | attention is finite; Section 8 allocates the leash's, nothing allocates the public's |


### 23.2 Impossibility results the design respects

1. **Rice.** No general procedure decides a nontrivial semantic property of arbitrary code; admissibility is therefore a static property of what a proposal writes, not of what running it would do (RSI v3 37.1; Part III paper 1.7: the leash is on the state, not on the code).
2. **Universal containment.** No enumerated attack surface proves an unknown path absent (v1 page 4); coverage is enrolled systems only.
3. **The elicitation gap.** No distribution-free bound exists on what a system can hide within one protocol (Part III paper 1.3, A3); $G_{\max}$ is a judgment carried as a margin.
4. **Lorden.** At a declared false-alarm rate the detection delay is bounded below; it cannot be driven to zero (Prop. 5.3).
5. **Ville's price.** Time-uniform validity costs a $\sqrt{\log\log n}$ factor over a fixed-$n$ interval (RSI v3 65.4); anytime validity is bought, not free.
6. **Wald.** No sequential test with error rates $(\alpha, \beta)$ decides faster than $c_{\alpha\beta}/\mathcal K$ observations on average (RSI v3 65.6); the keep-up denominator cannot be shrunk by cleverness, only by information or capacity.
7. **Kingman.** A queue with utilization approaching one has unbounded wait; a leash provisioned at the engine's demand does not keep up (Prop. 4.1).
8. **Goodhart.** Optimization against a proxy drifts every unmeasured quantity by up to range$\cdot\sqrt{B_{\text{KL}}/2}$ (Athena v3 9.3); the audit cadence bounds it, never removes it.
9. **Orseau and Armstrong.** Interruptibility is a property of the learning rule and assumes the interruption mechanism works; it is no defense against an agent that disables it (Part III paper 1.5d).
10. **Soares et al.** Utility indifference removes the incentive to resist shutdown and also the incentive to preserve the switch; it is defense in depth, not the guarantee (Part III paper 1.5e).
11. **The compromised invariant plane.** The design is not built to withstand a compromise of L3/L4 or of the kernel itself; the plane is small, offline-auditable and human-operated for that reason (RSI v3 36.4), and two independently built monitors are the remedy for a shared bug (Part III paper 1.7).
12. **Correlated evaluator bias.** Replication by $k$ peers bounds independent error; correlated bias across all replicators is tracked as a risk, not defended by the protocol (Ladder 12.4).

### 23.3 What would falsify the central claims

| Claim | Falsifier |
|---|---|
| The keep-up queue law (4.1) | a window in which measured $\chi \ge 2$ while the independently measured backlog's mean exceeds $2/(\chi-1)$ with its interval, or $P(\ge 10)$ exceeds $5\chi^{-10}$ |
| The sampling bound (5.1) | capability growth between samples above $\varepsilon$ with the velocity witness showing no excursion above $\chi v_{\max}$ |
| Anytime validity (5.2) | realized false alarms above $\alpha$ plus its binomial interval on streams held at the cap |
| The leash dividend (6.1) | measured incident exposure at the ratified pace exceeding $h_{\max}$ at the quantile, or harm that does not scale with undetected growth in the incident record |
| Stopping distance (7.2) | a halt drill at the deployed $N$ exceeding $T_{\text{lease}} + W_{\max}$ |
| Lease over message (7.3) | a cell still active one TTL after renewals stopped |
| The fleet keep-up rule (10.1) | a fleet with demand held at capacity$/2$ whose backlog grows |
| The Sun Mode bound (13.1) | realized excess release above the published bound in any order's debrief |
| Separation of powers (12.1) | any single-role compromise that activates in a red-team exercise, or any stopping party that cannot stop alone |
| The contract (17) | a benchmark's LCB below 2 after certification, on the frozen worlds |

### 23.4 Known weaknesses

1. The reference worlds are the script's; nothing here measures a real engine, a real reviewer, a real partition or a real order.
2. The M/M/1 law assumes Poisson demand and exponential service; real verification is batched and heavy-tailed, and Kingman's approximation is the honest replacement with a stated factor.
3. The dividend assumes harm scales with undetected growth; irreversible effects are excluded by construction and handled on the effect clock, and the exclusion is where the dividend's assumption lives.
4. The two-role compromise of Rules and Release can order an unwise but lawful ignition; Review and the kernel's pre-flight are the remaining stops, and the envelope itself is a political control by design (Part III paper 2.6).
5. The board monitor's taint detection is a classifier over text and has false negatives; the credential rule and the broker boundary are the controls that do not depend on it.
6. The three pillar metrics are proxies for trust, communication and adoption; a regime can meet them and still be unwanted, which is why Section 12.3 exists.
7. The variance-free pace monitor is about five times slower than the Gaussian one at the same level; running both (R5.2.1) buys speed when $\sigma$ is right and validity when it is not, and the record states both delays.
8. The LCB band rule needs windows of about 2,400 promotion requests to reach a 10% half-width under the reference burstiness; at 400 it throttles falsely in more than half the windows. A slow engine has long windows and a late band; the pace monitor and the effect clock carry the gap.
9. The keep-up band spends capacity on headroom by design: utilization is $1/\chi$, so the floor holds half the independent verification capacity in reserve and the target holds four fifths. That is the price of the safety factor, it is paid in verified throughput (check 12: 42.3 against 82.8), and it is why the target is a design target and the floor is the contract.
10. None of this is a theorem prover. The checks are finite numerical witnesses and representative counterexamples; the proofs are in this document, the Part III paper and the cited literature.

---

## **24. Traceability from v1.0 to v3.0**

| v1.0 pages | Content | v3.0 section |
|---|---|---|
| 01 to 03 | charter, U.S. mission, users and scope | 1, 3 |
| 04 | threat model and limits | 23 |
| 05 | notation and three-valued decisions | 0.3 (imported), 7.4 |
| 06 to 07 | architecture, enforcement boundary, policy compilation | 2.1, 3.2, 12 |
| 08 | identity, delegation, approvals | 12.1 |
| 09 to 11 | isolation, broker, network and secrets | 10.3, 11 (by reference) |
| 12 | budgets and bounded replication | 10.1, 10.3 |
| 13 to 14 | formal invariants, proof-carrying changes | 22, 23 (by reference) |
| 15 to 16 | action shield, uncertainty and abstention | 7.4 (HOLD), 5.4 |
| 17 | runtime assurance, revocation, stopping | 7.1 to 7.3 |
| 18 | multiple clocks and delayed validation | 3.5 |
| 19 to 20 | control barrier functions, reachability | Part III paper 1.1, 1.2 (via 2.2) |
| 21 to 23 | hazard register, tail losses, rare-event statistics | 9.4, 23 |
| 24 to 26 | adaptive experiments, capability gates, RSI metrics | 5.2, 8, 17 |
| 27 to 28 | brief and evidence contracts | 9.1, 3.2 (Athena row) |
| 29 to 30 | release state machine, APIs | 7.4, 20 |
| 31 | multi-agent composition and LVL3 integration | 3.2, 11 |
| 32 | corrigibility | 9.3, 23.2 |
| 33 to 35 | learning across installations, privacy, audit ledger | 12.3, 14 (by reference) |
| 36 to 38 | government assistance, public experience, insider abuse | 1.2, 12.3, 12.1 |
| 39 to 41 | distribution, federation, reliability | 14, 7.3 |
| 42 | performance and cost targets | 4.4, 17.2 |
| 43 | adversarial evaluation A01 to A18 | 18 (retained) |
| 44 | U.S. standards mapping | 15 |
| 45 to 46 | implementation and delivery plans | 20 |
| 47 | worked fixtures | 22 (checks 5, 9, 13) |
| 48 to 50 | assurance case, sources, handoff | 1.3, 25, 20 |

---

## **25. Foundations index**

| Section | Rests on | New here |
|---|---|---|
| 4.1 | Kendall (1953) M/M/1; Kingman (1961) G/G/1 heavy traffic; Little (1961); Markov-modulated Poisson arrivals (Neuts 1979) | the keep-up band as a contract quantity; the burst correction measured against Kingman |
| 4.2 | moving-block bootstrap (Künsch 1989); percentile lower confidence bound | the band decided on $\text{LCB}_{95}$ with a half-width window rule and a dead band |
| 4.3 | RSI v3 38.2 (throttle $f$ first); Kydland and Prescott (1977) | |
| 5.1 | Part III paper Leash Law 2, Theorem 1.3 (margin $r_{\max}\Delta$) | the sampling bound in pace units with the excursion factor $b$ |
| 5.2 | Ville (1939); Robbins (1970); Wald (1947); Waudby-Smith and Ramdas (2024) betting e-processes | two monitors, one alarm (R5.2.1) |
| 5.3 | Page (1954); Lorden (1971); Moustakides (1986) | |
| 6.1 | monotonicity | the leash dividend |
| 6.2 | RSI v3 Prop. 64.7; Athena v3 Prop. 9.2 | |
| 7.1 | quantiles of sums; v1 pages 17, 47 | |
| 7.2 | Little's law; RSI v3 36.3 | |
| 7.3 | fail-safe design (absence as signal); Sideways 6.3 | |
| 7.4 | Ostrom (1990) graduated sanctions; v1 page 29 | |
| 8.1 | Sims (2003) rational inattention; RSI v3 38.3 | |
| 9.1 | Hart (1995) residual control; Kydland and Prescott; Athena v3 10.1 | the ratchet (asymmetric lag) |
| 9.2 | Pinsker (1964); Athena v3 Prop. 9.4 | the cadence formula read from the leash |
| 9.3 | Orseau and Armstrong (2016); Hadfield-Menell et al. (2017) | the admission test as an executable check |
| 9.4 | Clopper and Pearson (1934); Hoeffding (1963) | |
| 10.1 | Ladder Props. 10.4, 10.5 (Jones duplication; Yule process) | $A_{\text{cap}} = A_{\text{sat}}/\chi_{\text{floor}}$ |
| 10.3 | compare-and-swap; v1 E12 | |
| 12.1 | Feaver (1992); Anderson (1972) reference monitor; Shamir (1979) via Part III paper 2.3; access structures (Ito, Saito and Nishizeki 1987) | the exhaustive coalition enumeration: 3 to ignite, 4 to widen, 7 to block a stop |
| 13.1 | dead-man leases (RSI v3 36.3); Part III paper 2.5 | the Sun Mode lease bound |
| 13.2 | Prop. 4.1 at the Sun pace | the keep-up pre-flight |
| 14 | Sastry et al. (2024); Shavit (2023); the controlled-technology regime named in the Part III paper 2.4 | |
| 17 | RSI v3 §68; Athena v3 §42; Shapley (1953) | |
| 23.1 | Part III paper 2.6 (assumption failures) | the threats table for the v3 mechanisms |
| 23.2 | Rice (1953); Lorden; Ville; Wald; Kingman; Goodhart; Orseau and Armstrong; Soares et al. (2015) | |

---

## **26. Reference computations**

``` text
# 26.1 keep-up ratio and band (Section 4)
chi = mu_S / lambda_D                              # per channel, same window, block-bootstrap interval
E_backlog = 1 / (chi - 1);  P_backlog_ge_n = chi ** (-n)
if chi < 2: throttle(f); then throttle(lambda)     # never a verification standard
if chi > 5 and admit == 1: flag EXPANSION_AVAILABLE

# 26.2 pace sampling interval (Proposition 5.1)
Delta = ln(1 + eps) / (chi * v_max)                # eps = 0.01: 71.6 min at chi=2, 28.7 min at chi=5 for v_max=0.10/day

# 26.3 exceedance e-process (Proposition 5.2)
log_E += (theta / sigma**2) * (x - v_max) - theta**2 / (2 sigma**2);  alarm when log_E >= ln(1/alpha)

# 26.4 CUSUM (Proposition 5.3)
S = max(0, S + l);  alarm when S >= h;  h chosen so that ARL_0 = declared;  delay ~ ln(ARL_0) / KL

# 26.5 the dividend (Proposition 6.1)
v_max = ln(1 + h_max) / quantile(T_exp, 1 - q);   ratio = T_H / T_S;   T_2 = ln 2 / v_max

# 26.6 stop deadline (Proposition 7.1)
certify iff quantile(T_detect + T_decide + T_fence + T_transition, 0.99) <= T_hazard - T_margin

# 26.7 stopping distance (Proposition 7.2)
T_stop <= T_lease + W_max                          # independent of N; halt drill every window

# 26.8 review allocation (Proposition 8.1)
pi_i ∝ h_i * u_i subject to sum pi_i <= kappa_H, L2 = 100%, L1 floor = 1% uniform

# 26.9 audit cadence (Proposition 9.1)
K_a = floor(Gamma_g * sqrt(2) / (r_eta * sqrt(B_KL)))

# 26.10 fleet keep-up (Proposition 10.1)
capacity = N * lambda_V / ((1 + k) * nbar);  A_sat = capacity / (kappa_L * f * N**lambda_A);  A_cap = A_sat / chi_floor
f = capacity / (chi_floor * kappa_L * N**lambda_A * A) whenever demand would exceed capacity / chi_floor

# 26.11 Sun Mode lease bound (Proposition 13.1)
excess <= exp((v_sun - v_max) * (tau + Delta_h + T_step))
preflight: chi(v_sun) >= 2 on every channel, provisioned; Delta_sun = ln(1+eps) / (chi * v_sun)
```

---

*Superman protects, defends and shows up. The engine makes the capability, the reward function aims it, and the leash is what makes it safe to let them run.*
