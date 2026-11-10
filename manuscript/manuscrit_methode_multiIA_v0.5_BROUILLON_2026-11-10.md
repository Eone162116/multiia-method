# A preregistered multi-agent framework for empirical inference under degeneracy

**Working draft v0.5 — 10 November 2026**  
**Status:** methods manuscript. v0.5 adds F15 and F16 (§3.4). v0.4 aligned the text with protocol v2.3 DRAFT (merge of the 29 July amendment). v0.3 added the ledger of all applications (§1.2), the failure-mode catalogue (§3.0), the development cases (§8.1–8.2), refutation criteria (§9.7) and declarations. Items in [TO CONFIRM / TO INSERT / TO DECIDE] need the author's decision or data.  
**Scope:** methods paper; not a claim of new astrophysical or particle-physics discovery

---

## Abstract

Empirical research increasingly combines public data, complex analysis pipelines, simulation, and multiple AI systems used for code generation, criticism, verification, and synthesis. This combination can accelerate analysis, but it also expands researcher degrees of freedom and creates distinctive failure modes: post-null pivots disguised as robustness checks, divergence between frozen and executed code, circular benchmarks whose truth is conditioned on the classifier being evaluated, and provenance failures discovered only after a scientific conclusion has been reached.

We present a preregistered multi-agent workflow designed to control these risks. The framework separates generation from validation, requires an exogenous verification path where possible, enforces identical-code forward modelling for estimator-degeneracy tests, prioritizes paired comparisons, and includes explicit stopping rules that forbid reopening a closed claim through new post hoc tests. Executable reproducibility is treated as part of the inferential object: archived code, inputs, seeds, commands, environments, outputs, and hashes must correspond to the path that generated the reported decision.

The framework was stress-tested in four principal settings with deliberately different logical roles; further development, illustrative and ongoing applications are listed in Section 1.2 and reported in Section 8 for completeness. In MaNGA stellar kinematics, a statistic initially interpreted as an intrinsic radial gradient was shown to be non-identifiable because ordinary non-circular kinematics passed through the observational operator reached the observed regime; the astrophysical claim was closed rather than rescued. In a controlled CMS dimuon benchmark, an initial circular benchmark was rejected before blind analysis, while a corrected exogenous construction passed all three preregistered constraints. In TESS, a real candidate was selected mechanically before light-curve access and assigned a frozen `SURVIVE` verdict that remains pending future TFOPWG adjudication. Finally, a heavier blind GWOSC benchmark using public O4b strain, a fixed PyCBC matched-filter pipeline, and time-slide backgrounds failed its preregistered transfer criterion: the time-shift null was rejected correctly, but a borderline real event was rejected and a strong real event reached only `GRAY`. No post hoc rescue analysis was allowed.

The resulting evidence does not support the claim that one analysis method transfers successfully across scientific domains. It supports a narrower methodological claim: a multi-agent workflow can be structured so that survival, rejection, ambiguity, non-identifiability, provenance failure, and classifier failure remain auditable terminal outcomes rather than triggers for adaptive rescue.

---

## 1. Introduction

The limiting factor in many modern empirical projects is no longer access to data or computational power. Public archives, mature scientific Python ecosystems, and generative AI systems can now compress weeks of coding and exploratory analysis into hours. The resulting gain in speed is real. So is the accompanying increase in researcher degrees of freedom.

This problem becomes particularly acute when several AI systems are used in parallel. One model may generate code, another may critique an interpretation, a third may suggest a robustness test, and a fourth may summarize the result. Each contribution can be locally reasonable while the overall workflow drifts into a form of adaptive inference in which the effective hypothesis, statistic, null, and stopping rule change after the data have been seen.

The methodological difficulty is therefore not merely hallucination or coding error. A more subtle failure occurs when a workflow remains technically competent while becoming logically non-prospective. A new test can be introduced only after a previous test fails. A null result can trigger a new statistic whose purpose is implicitly to recover the original claim. A benchmark can appear blind while its cases were selected using the same classifier that is later evaluated. A result can be scientifically stable while the archived script no longer matches the code that actually generated the numbers.

The framework presented here was developed to address this class of problems. It is based on a simple principle:

> A scientific result is not fully specified by its estimate and uncertainty. It also depends on the provenance of the executable path that produced it and on the rule governing what is allowed to happen after the result is known.

We therefore treat generation, validation, degeneracy testing, stopping, provenance, and external adjudication as separate objects.

The protocol emerged from a galaxy-kinematics project in which an initially compelling empirical signal failed an explicit forward-model identifiability test. Instead of replacing the statistic after the failure, the project was closed under a preregistered degeneracy rule. Subsequent confirmatory controls were then used only to characterize the closed result, not to reopen it. The same protocol was later transferred to a controlled particle-physics benchmark, a prospective exoplanet-candidate analysis, and a blind gravitational-wave benchmark.

The motivation overlaps with the broader literature on researcher degrees of freedom, preregistration, and reproducible science (Simmons et al. 2011; Munafò et al. 2017; Nosek et al. 2018), but the present framework focuses on a narrower problem that becomes acute in AI-assisted work: once generating another analysis becomes nearly frictionless, the scientific workflow needs explicit rules governing which future analyses are no longer allowed to change a frozen conclusion.

This paper describes the framework, the failure modes revealed during its development, and what four principal case studies do—and do not—show about transferability. Section 1.2 lists every application of the protocol to date, including those not retained as principal cases.


### 1.1 Logical role of the empirical cases

The case studies are not pooled as if they were repeated measurements of one performance parameter. Each was chosen to exercise a different failure regime.

| Case | Scientific object | Frozen outcome | Logical role in protocol evaluation |
|---|---|---|---|
| MaNGA | stellar-kinematic residual statistic \(n_g\) | **CLOSED / non-identifiable** | tests whether an attractive scientific claim is allowed to die after a forward-model degeneracy criterion |
| CMS dimuon | controlled invariant-mass benchmark | **PASS 3/3** | tests blind construction, exogenous truth, null design, and pre-reveal hashing |
| TESS TOI 7698.01 | real transit candidate | **SURVIVE / PENDING** | tests prospective freezing before a future external disposition |
| GWOSC O4b | blind H1/L1 matched-filter benchmark | **FAIL** | tests whether a cross-domain implementation failure is accepted without post hoc rescue |
| Solar flare | future NOAA/GOES adjudication | **REJECT / PENDING** | parked prospective registration; not used as active evidence in this draft |

The evidential target is therefore **workflow behavior under heterogeneous outcomes**, not a domain-averaged accuracy score.

### 1.2 Ledger of all applications of the protocol

Every application of the protocol to date is listed below, whatever its outcome. The four principal cases (§§4–7) are those developed in detail.

| Application | Domain | Status in this paper | Outcome | Changed the protocol? |
|---|---|---|---|---|
| MaNGA \(n_g\) | galaxy kinematics | principal case (§4) | closed, non-identifiable (B2) | origin of the protocol (v1.0 derived retrospectively from it; v2.0 added the pre-committed stopping rule after its closure) |
| RV exoplanets (HD 41248, HD 219134 b) | stellar activity vs. planets | development application (§8.1) | partial: 1/3 at v1, 2/3 at v2; v3 specified, not executed | lessons recorded in a 29 July amendment (P10, P11, accessible verifier, F14), merged into protocol v2.3 DRAFT on 9 November 2026, after the principal cases |
| Moser's circle problem | experimental mathematics | illustrative demonstration (§8.2) | naive prediction (32) refuted; true value 31 | no change recorded |
| CMS dimuon | particle physics | principal case (§5) | first benchmark rejected under F13 before analysis; second PASS 3/3 | yes: F13 |
| TESS TOI 7698.01 | exoplanet candidate | principal case (§6) | SURVIVE, adjudication pending | no |
| GWOSC O4b | gravitational waves | principal case (§7) | FAIL (strict) | no |
| Solar flare, 1 Sep 2026 | space weather | parked (§8.3) | REJECT, outcome pending | no |
| RAR / SPARC | galaxy dynamics | development application on real data (§8.4.1) | registered prediction (M/L degeneracy of the residual–gas-fraction correlation) refuted on its own terms; the later gas explanation is exploratory and untested | first use of the prediction-registration mode on a live question [TO CONFIRM] |
| Case-control omics, simulated | high-dimensional biology | illustrative demonstration on simulated data (§8.4.2) | pure-noise hits removed by multiple-comparison correction; a perfect batch confound survives Bonferroni and naive permutation and is removed only by the batch control (P6) | no change recorded [TO CONFIRM] |
| Quantitative backtest, simulated | finance | illustrative demonstration on simulated data (§8.4.3) | best Sharpe 1.37 among 5000 random strategies; naive p = 9×10⁻⁴, corrected p = 0.89 | no change recorded [TO CONFIRM] |
| HYDRO prospective streamflow forecast | hydrology | prospective, paused (§8.4.4) | v8 paused on 7 October 2026; preregistration freeze deadline 10 January 2027 | [TO CONFIRM] |
| wbt-gaia wide binaries | astrophysics | prospective, pending (§8.4.4) | frozen by annotated tag on 9 November 2026; Gaia DR4 release on 2 December 2026 | no |

Freeze dates (file timestamps, closure notes and protocol v2.2 FINAL, local time): MaNGA 28 July 2026 (m≥3 closure) and 27–31 August 2026 (B2, C1–C3); RV test 28–29 July 2026; CMS (v1 and v2), TESS and GWOSC all on 31 August 2026, between 17:14 (first CMS preregistration) and 21:32 (GWOSC closure note). [TO CONFIRM: the dates of the Moser, omics, finance and RAR/SPARC applications (the Moser, omics and finance demonstrations were run in a late-July 2026 working session), and any application still missing from this table.]

**Selection of the principal cases.** The RV test was the protocol's first transfer to a foreign domain; the mathematical case is a didactic example with a known answer. The lessons of the RV test were recorded in an amendment dated 29 July 2026 (P10, P11, an accessible-verifier requirement and F14), headed "to be merged" into the v2.0 protocol, and they were never merged: protocol v2.1 and v2.2 FINAL, both of 31 August 2026, list nine principles and do not mention that test. The principal cases of §§5–7 were frozen and closed on 31 August 2026, after v2.2 FINAL was finalised (17:04, ten minutes before the first CMS preregistration), so they were governed by v2.2 FINAL and not by the amended protocol. The amendment was merged afterwards, on 9 November 2026, into protocol v2.3 DRAFT (`protocol/` in this repository). [TO CONFIRM: whether the lessons of the RV test were nevertheless applied to §§5–7 by hand, and that neither development application was left out because of its outcome.]


---

## 2. Design principles

### 2.1 Separation of generation and validation

The first principle is organizational rather than statistical. The process that proposes a hypothesis, statistic, or model should be separated from the process that decides whether the resulting claim survives.

In a multi-agent setting, this means assigning explicit roles. A generator may propose a statistic or code path. A calculator may implement the frozen analysis. A critic may search for failure modes. An arbitrator may decide whether a preregistered criterion is satisfied. These roles need not correspond to permanently distinct models, but the information flow must preserve their logical separation.

The key constraint is that validation cannot silently inherit the objective of rescuing the generated claim.

### 2.2 Exogenous verification

Whenever possible, the ultimate verifier should be external to the inferential loop.

Examples include:

- an independent future classification;
- a public catalogue maintained by another collaboration;
- a physically distinct measurement channel;
- a known generative mechanism in a controlled benchmark;
- a forward model whose inputs are fixed independently of the observed decision statistic.

An apparent verifier that is generated from the same classifier being evaluated is not exogenous, even if the labels are hidden from the analyst.

### 2.3 Identical-code forward modelling

When testing whether an observed statistic is identifiable, mocks must pass through the same estimator as the observations.

If an observed statistic is
\[
S = \mathcal{E}(\mathcal{O}(X)),
\]
where \(\mathcal{O}\) is the observational operator and \(\mathcal{E}\) is the estimator, then a physically plausible alternative model \(X_0\) must be evaluated as
\[
S_0 = \mathcal{E}(\mathcal{O}(X_0)).
\]

Comparing an observed estimator to a simplified analytic expectation that bypasses the observational operator is insufficient for identifying estimator-induced degeneracy.

### 2.4 Joint degeneracy rather than additive channel budgets

Instrumental and astrophysical effects often interact nonlinearly. Point-spread functions, spatial binning, noise, coherent residual structure, and estimator choices do not generally contribute independent additive offsets.

The protocol therefore avoids statements of the form
\[
S_{\rm obs} = S_{\rm intrinsic} + S_{\rm instrument}
\]
unless such additivity has itself been demonstrated.

The relevant question is instead whether an ordinary alternative model passed through the full operator can occupy the same decision region as the observations.

### 2.5 Paired statistics

Whenever a mock can be associated with the same object as an observation, the preferred comparison is paired.

For object \(i\),
\[
\Delta_i = S^{\rm obs}_i - \bar S^{\rm mock}_i.
\]

This retains object-specific information that is lost in comparisons of two marginal population distributions.

### 2.6 Retraction and non-identifiability are valid outcomes

A protocol that only rewards survival is not a validation protocol.

A previously interesting signal may become non-identifiable. A forward model may show that the estimator cannot separate the target effect from an ordinary nuisance process. A prospective target may remain ambiguous.

These are accepted terminal outcomes.

### 2.7 Precommitted stopping

The most important protection against post-null pivoting is a stopping rule.

Once a preregistered closure criterion is satisfied, the original claim is closed. Additional analyses may characterize the estimator, quantify sensitivity, or document limitations, but they may not function as a new decisive route to resurrect the closed claim.

This rule is stronger than merely labelling a new analysis “exploratory.” It constrains interpretation.

### 2.8 Executable reproducibility

A table is not reproducible merely because its method is described correctly.

For a result to be archive-clean, the following must be frozen and verified:

- exact code executed;
- exact inputs;
- random seeds;
- runtime commands;
- relevant package versions;
- outputs and logs;
- hashes of archived artifacts.

The archived execution path must regenerate the reported decision quantities.

---

## 3. Failure modes discovered during protocol development

The protocol was not designed perfectly in advance. Several of its strongest rules were added after concrete failures.

### 3.0 Catalogue of failure modes and numbering

The failure modes observed during development are catalogued below; §§3.1–3.3 describe the three most recent in detail. F1–F10 are taken from protocol v2.0, F11 (v2.1, 31 August 2026) and F12 (v2.2 FINAL, 31 August 2026) from the governing protocol, and F13 was introduced after v2.2 FINAL (CMS case) and added to v2.3 DRAFT. F14 comes from an amendment of 29 July 2026 that was merged into the protocol only on 9 November 2026 (v2.3 DRAFT), where it was labelled F11. F15 and F16 come from the reference audit of 9 November 2026 (§3.4) and are proposed for the next protocol version.

| Code | Failure mode |
|---|---|
| F1 | Confabulated references together with their attached claims |
| F2 | Censoring artefact disguised as signal (clipped negatives plus radially growing errors fabricate a positive gradient; three occurrences) |
| F3 | Instrumental trend that was a sample confound (removed by partial correlation on redshift and mass) |
| F4 | Systematics budget correct channel by channel but wrong in total (the dominant PSF × non-circular term was in no channel) |
| F5 | Geometric contamination of a "clean" fallback probe |
| F6 | Garden of forking paths: successive statistics after failures, sequence neither preregistered nor disclosed |
| F7 | Multi-AI self-validation loop: cross-audits recycling the project's own risk register as external findings |
| F8 | Data hygiene: duplicate files silently inflating N |
| F9 | Lost provenance of sample-selection choices |
| F10 | Public-archive integrity defect: a superseded analysis output published with a DOI as the "frozen sample", contradicting the fiducial result; public and indexed for six weeks |
| F11 | Post-null pivot disguised as robustness (v2.1; §3.1): after a closure criterion has been met, a new test is proposed as "decisive"; a specialisation of F6 |
| F12 | Executed code differs from frozen or archived code (§3.2) |
| F13 | Endogenous verifier or circular benchmark (§3.3) |
| F15 | Verifier false negative by registry mismatch: a valid DOI is declared unresolvable because it was queried in the wrong registration agency, for example a DataCite DOI queried at CrossRef (§3.4) |
| F16 | Citation that resolves but does not support its claim: the DOI exists but its metadata differ from the citation, or the attached claim is stronger than the source's own conclusion (§3.4) |
| F14 | Erroneous self-diagnosis applied without test (29 July 2026 amendment, merged into v2.3 DRAFT on 9 November 2026, where it was labelled F11): a predicted fix tightened the null instead of widening it |

[TO CONFIRM: the status of F10. Proposed wording for F10: the corrected archive was prepared but not deposited, and the original public record remains online with the defect described above.]

### 3.1 F11: post-null pivot disguised as robustness

After a degeneracy criterion had already closed the original astrophysical claim, a new injection-recovery test was proposed as potentially “decisive.”

This was rejected because it would have changed the logical role of a post-null sensitivity analysis. Once closure has occurred, a later test may characterize estimator performance, but it cannot become a new gate for reopening the astrophysical claim.

F11 is therefore defined as:

> a new post-null analysis whose practical role is to create another path to the original positive claim after the preregistered closure condition has already been met.

The countermeasure is an explicit non-resurrection clause.

### 3.2 F12: executed code differs from frozen or archived code

A later audit found that several confirmatory controls had been executed through code paths that differed from the nominal frozen scripts.

The discrepancies were not changes to the scientific thresholds. They included a duplicate-row fix, cleaning of sentinel values before secondary regressions, a branch-selection mismatch in one control, and an unseeded bootstrap used for confidence intervals.

None of these changed the central scientific conclusion. They nevertheless constituted a provenance failure.

The entire confirmatory chain was therefore rerun through canonical scripts. The final archive reported:

- `STATUS = PASS`;
- zero validation errors;
- 195/195 MaNGA MAPS inputs hashed;
- 17 source artifacts hashed;
- 17 archived copies hashed;
- the exact confirmatory preregistration recovered and verified.

The recovered preregistration,
`PREREG_controls_L0_v1.md`, has SHA256

`2a64a52aa20fc92669681a182ad2f16325daf2c109f3e56886527e61bddc6104`.

Protocol v2.2 FINAL, finalised on 31 August 2026 at 17:04, still records this artefact as unrecovered (status `EXECUTION_PASS_PREREG_MISSING`, 16 source artifacts) and treats its absence as a permanent provenance exception. The archive described here (17 source artifacts, `STATUS = PASS`) is the later one, in which the preregistration was found and verified by hash. The recovered files carry last-modified times of 27 August 2026 (14:24 to 14:26), before the first C1 output file (31 August, 11:39); file timestamps support the prospective ordering but do not prove it. The recovered copies were created on 31 August 2026 at 18:24, eighty minutes after v2.2 FINAL, so the protocol note was accurate when written and became outdated that evening. The protocol note was updated on 9 November 2026 (v2.3 DRAFT, section 5, "Mise à jour de provenance").

This incident motivated a stronger definition of reproducibility: the code in the archive must be the code that actually regenerated the published numbers.

### 3.3 F13: endogenous verifier or circular benchmark

The first cross-domain CMS benchmark contained a more subtle flaw.

Its constructor used the same classifier later used in the blinded analysis to select:

- a positive case that already produced `SURVIVE`;
- a null case resampled until it produced `REJECT`;
- a weak case whose mixture fraction was chosen to produce `GRAY`.

The labels were hidden, but the truth had been conditioned on the classifier. A three-of-three success would therefore have measured self-consistency rather than transferability.

The benchmark was stopped before analysis.

A corrected version prohibited all classifier calls during construction. The builder did not import the analysis kernel, did not calculate the decision statistic, and did not resample cases conditionally on their future verdict.

F13 is therefore:

> a benchmark whose nominal truth or case admission rule depends on the classifier or decision rule that the benchmark is supposed to evaluate.


### 3.4 F15 and F16: reference-audit failures (9 November 2026)

Two failures of the reference check itself were found while auditing the twelve references of the v0.2 manuscript. An exogenous check can be wrong in either direction: F15 flagged a valid reference as broken, and F16 passed an inexact one as clean.

**F15.** An earlier audit (October 2026) had declared the GWOSC O4b data-release DOI (10.7935/8emv-ag54) unresolvable. On 9 November 2026 it resolved by three independent routes: the DataCite API, the doi.org redirect, and the GWOSC page itself, which prints it as its dataset DOI. CrossRef returns 404 for this DOI because the prefix 10.7935 is registered with DataCite, so the earlier check most plausibly queried the wrong agency; the method it actually used is not documented. [TO CONFIRM] On 8 November an AI assistant repeated the "unresolvable" status from an earlier note into a task and a status page, before re-verifying it. Counter-measure: determine the registration agency first (`doi.org/doiRA`), query that agency, and confirm with a second route before any DOI is declared broken.

**F16.** Two kinds of citation resolved but did not support what was attached to them. First, the STScI/MAST entry for the TESS products resolved, but the resolved titles, authors and year (TESS-SPOC: Caldwell, Jenkins and Ting, 2020; QLP: Huang, 2020) differed from the citation text ("TESS mission data products", author "STScI/MAST", 2026), and one product actually used, the 2-minute SPOC light curves, had no DOI at all. Second, in the radial-velocity development application (§8.1), the 29 July amendment stated the reference verdicts of the phantoms more strongly than their sources: it described α Cen Bb as having the cleanest possible ground truth and as conceded by its discoverer, whereas Rajpaul et al. (2016) show that the signal almost certainly arises from the window function of the data; and it described HD 41248 as having a definitive ground truth, whereas Faria et al. (2020) conclude that the variations can be explained by stellar activity and that the data do not provide enough evidence for a planet. Both were corrected on 9 November 2026. Counter-measure: compare the resolved metadata with the citation field by field, and the attached claim with the source's own conclusion, not only the existence of the reference.

---

## 4. Case study I: MaNGA stellar kinematics and closure by non-identifiability

### 4.1 Initial statistic

The originating project used the final SDSS-IV MaNGA release in DR17 (Abdurro’uf et al. 2022), which contains the complete MaNGA survey. It studied a radial statistic \(n_g\) derived from the logarithmic slope of the residual stellar-velocity variance after subtraction of an azimuthal first-order model and correction for diagonal noise.

Across 195 usable MaNGA disk galaxies, the observed median was approximately

\[
n_g^{\rm obs} \simeq 0.766.
\]

The initial astrophysical interpretation treated the positive slope as potentially intrinsic.

### 4.2 Forward-model degeneracy test

A forward model injected ordinary non-circular kinematic structure with a radial variance envelope

\[
{\rm env}(R)
=
A\,\sigma_{\rm ref}
\left(\frac{R}{R_{\rm med}}\right)^{s_{\rm in}/2}
\]

into coherent azimuthal modes and an incoherent component. The simulated field was then passed through the observational operator, including the point-spread function, real spatial tessellation, and paired noise treatment, before being evaluated with the same \(n_g\) estimator.

The preregistered closure logic contained three regimes. The decisive condition was B2:

> if any ordinary baseline with non-positive intrinsic slope reaches the decision region \(n_g^{\rm out}\ge0.50\), the statistic is considered non-separable with respect to the intrinsic interpretation, and no replacement statistic is introduced to rescue the claim.

At \(A=1.144\), the amplitude calibrated for \(f_{\rm coh}=0.7\) and used for the reference run, and flat intrinsic variance \(s_{\rm in}=0\), the forward model produced:

\[
n_g^{\rm out}=0.752
\]
for \(f_{\rm coh}=0.3\), with an interval approximately \([0.586,0.923]\), and

\[
n_g^{\rm out}=0.863
\]
for \(f_{\rm coh}=0.7\).

These values occupy the same regime as the observed statistic.

The correct conclusion is not that “the instrument creates the signal from nothing,” and not that there exists an additive “instrumental floor.” The result is instead:

> \(n_g\) is non-identifiable as a unique tracer of an intrinsic positive radial variance gradient under the tested ordinary non-circular baselines.

B2 therefore closed the original astrophysical claim.

### 4.3 Confirmatory controls

Three controls had been frozen before the closure package was finalized.

#### C1: amplitude sweep

For \(s_{\rm in}=0\), amplitudes
\[
A=\{0.8,0.9,1.0,1.061,1.144\}
\]
were evaluated for \(f_{\rm coh}=0.3\) and \(0.7\).

The amplitude \(A\) is calibrated beforehand on the 195 real galaxies so that the injected residual variance matches the observed one: the median ratio of injected to observed variance is 0.889 for \(f_{\rm coh}=0.3\) and 0.764 for \(f_{\rm coh}=0.7\), which gives \(A=1/\sqrt{\rm ratio}=1.061\) and \(A=1.144\) respectively. The calibration therefore concerns the variance level (an amplitude), whereas the tested quantity is a radial slope; the sweep was nevertheless frozen to remove any suspicion of tuning. The preregistered criteria were: (i) B2 holds (\(n_g^{\rm out}(s_{\rm in}=0)\ge+0.50\) for at least one \(f_{\rm coh}\)) for all \(A\ge1.0\); and (ii) \(n_g^{\rm out}(s_{\rm in}=0)\ge+0.65\) from \(A=1.061\) onwards.

The reference run uses \(A=1.144\) for both branches. For the \(f_{\rm coh}=0.3\) branch, whose own calibration is \(A=1.061\), this over-injects variance by about 16% (\((1.144/1.061)^2\approx1.16\)); the preregistration flagged this mismatch. The headline cell (0.752) is therefore not the exactly calibrated one for that branch, which gives about 0.732, and both values are reported below. The word "conservative", used for \(A=1.144\) in earlier drafts, is not retained: a larger \(A\) raises \(n_g^{\rm out}\) and thus favours the degeneracy verdict, so the choice is not conservative with respect to that verdict. [TO DISCUSS: confirm this reading.]

At \(A=1.061\), the two branches yielded approximately 0.732 and 0.819. At \(A=1.144\), they yielded approximately 0.752 and 0.863.

Table C1 gives \(n_g^{\rm out}\) at \(s_{\rm in}=0\) (flat intrinsic variance) for the five amplitudes, with 95% bootstrap intervals and the number of galaxies \(N\) entering the median.

| \(A\) | \(n_g^{\rm out}\), \(f_{\rm coh}=0.3\) | 95% interval | \(N\) | \(n_g^{\rm out}\), \(f_{\rm coh}=0.7\) | 95% interval | \(N\) |
|---|---:|---|---:|---:|---|---:|
| 0.8 | 0.696 | [0.466, 0.856] | 183 | 0.790 | [0.637, 0.917] | 185 |
| 0.9 | 0.725 | [0.544, 0.869] | 183 | 0.817 | [0.662, 0.956] | 185 |
| 1.0 | 0.717 | [0.560, 0.910] | 183 | 0.808 | [0.690, 0.938] | 186 |
| 1.061 | 0.732 | [0.568, 0.935] | 184 | 0.819 | [0.720, 0.945] | 187 |
| 1.144 | 0.752 | [0.586, 0.923] | 187 | 0.863 | [0.757, 0.986] | 188 |

Criterion (i) holds at every amplitude tested, including those below 1.0 where it was not required (0.696 to 0.863), and criterion (ii) holds at \(A=1.061\) and \(A=1.144\) (0.732 to 0.863). Across the whole range \(A=0.8\)–\(1.144\), \(n_g^{\rm out}(s_{\rm in}=0)\) varies by only 0.056 for \(f_{\rm coh}=0.3\) and 0.073 for \(f_{\rm coh}=0.7\), so the mismatch discussed above changes the headline cell by about 0.02 (0.732 against 0.752).

The same grid shows how weakly the estimator responds to the injected intrinsic slope. At \(A=1.144\) and \(f_{\rm coh}=0.3\), \(n_g^{\rm out}\) is 0.425 [0.244, 0.584] for \(s_{\rm in}=-1\), then 0.761, 0.752, 0.798 and 0.847 for \(s_{\rm in}=-0.5\), 0, \(+0.5\) and \(+1.0\), with intervals 0.3 to 0.4 wide; for \(f_{\rm coh}=0.7\) it is 0.537, 0.746, 0.863, 1.014 and 0.957. The observed value 0.766 lies inside the 95% interval of every cell with \(s_{\rm in}\) between \(-0.5\) and \(+1.0\) for \(f_{\rm coh}=0.3\), and between \(-0.5\) and 0 for \(f_{\rm coh}=0.7\). Only the strongly negative slope \(s_{\rm in}=-1\) falls below the 0.50 decision region. For \(f_{\rm coh}=0.3\) the response is flat within the interval widths over \(-0.5\le s_{\rm in}\le+1.0\); for \(f_{\rm coh}=0.7\) it rises by about 0.27.

One caveat applies to this comparison: \(N\) is not constant. It is 183 to 188 at \(s_{\rm in}=0\) but only 159 to 168 at \(s_{\rm in}=+0.5\) and \(+1.0\), against 195 usable galaxies, so the medians at different slopes are taken over different subsets of galaxies. [TO CONFIRM: why \(N\) depends on \(s_{\rm in}\) (undefined slopes in some mock realisations?), and whether that selection could bias the flat response.]

The full 50-cell grid is archived in `control_C1_Asweep_reconciled.csv` (SHA-256 `FE7634BDB71D3D6413EF420B2473A688A2551F1DF1B28EFF38E25ADA4D8D9D73`). An earlier file, `control_C1_Asweep.csv` (SHA-256 `4329E120929E3CA0DF308494364E90120C99454B312A6654F50C98B357BE6193`), has identical point estimates but slightly different intervals (for example [0.215, 0.605] against [0.216, 0.611] at \(A=0.8\), \(s_{\rm in}=-1\), \(f_{\rm coh}=0.3\)), consistent with the F12 correction of an unseeded bootstrap [TO CONFIRM]. The reconciled file is the one cited here.

#### C2: paired observed-minus-mock offsets

For each galaxy,
\[
\Delta n_{g,i}
=
n^{\rm obs}_{g,i}
-
\bar n^{\rm mock}_{g,i}.
\]

The primary branch \(f_{\rm coh}=0.3\) gave

\[
{\rm median}(\Delta n_g)=+0.093970,
\]
with 95% bootstrap interval
\[
[-0.066478,+0.255219].
\]

The secondary branch gave

\[
+0.037175,
\]
with interval
\[
[-0.202638,+0.149402].
\]

No median offset was detected, but strict equivalence within \(\pm0.10\) was not demonstrated. This distinction is important. The primary interval remains compatible with a paired positive excess approaching +0.25.

The result therefore does not justify the statement that “the mock reproduces every galaxy.” It supports the narrower conclusion that the preregistered formal insufficiency criterion was not triggered.

#### C3: resolution hierarchy

Galaxies were divided into fixed terciles of \(R_e/{\rm PSF}\), and

\[
D =
{\rm median}(n_g|t_0)
-
{\rm median}(n_g|t_2)
\]

was evaluated.

For the primary \(f_{\rm coh}=0.3\) branch:

\[
D_{\rm obs}=+0.576100,
\]
with 95% interval
\[
[+0.129771,+0.944107],
\]

and

\[
D_{\rm mock}=+0.539419,
\]
with interval
\[
[+0.236584,+0.764644].
\]

The positive resolution hierarchy therefore appears in both observations and the forward model.

The difference \(D_{\rm obs}-D_{\rm mock}\) was retained as descriptive only; no post hoc equivalence threshold was introduced.

### 4.4 Methodological outcome

The MaNGA case is a negative scientific result but a positive protocol result.

The framework succeeded by preventing an initially interesting interpretation from surviving an explicit identifiability failure. Subsequent work improved provenance and characterization without reopening the closed claim.

---

## 5. Case study II: controlled cross-domain transfer with CMS dimuon data

### 5.1 Purpose

The MaNGA case alone cannot establish transferability because the protocol was developed within that project.

A second-domain benchmark was therefore constructed using public CMS dimuon data released through the CERN Open Data Portal. The underlying educational release contains 100,000 dimuon events derived from the Run2010B public Mu dataset and explicitly warns that the derived selection is not suitable for a full CMS physics analysis (McCauley 2014). This limitation is useful here because the benchmark objective is methodological rather than a new particle-physics measurement. The objective was not to make a new particle-physics measurement. It was to test whether the workflow could distinguish a known correlated signal from a destroyed-correlation null while preserving blind construction and preregistered stopping.

### 5.2 Correction of the first benchmark

The first benchmark version was rejected under F13 before analysis because its constructor selected cases conditional on the same classifier later being evaluated.

A second version removed this circularity.

The constructor made zero calls to the classifier.

Three disjoint samples of 8000 events were generated:

- `POSITIVE`: real CMS dimuon pairs;
- `NULL`: a single event-mixing of the second muon, with no retry;
- `WEAK`: a single event-mixing with 1% of the original real pairs restored.

The admissible outcomes were fixed before analysis:

- POSITIVE → `SURVIVE`;
- NULL → `REJECT`;
- WEAK → `REJECT` or `GRAY`, but never `SURVIVE`.

### 5.3 Frozen classifier

The primary statistic counted events in the mass window

\[
86 \le M_{\mu\mu} < 96~{\rm GeV}.
\]

A null distribution was generated by 999 charge-stratified event-mixings.

The classifier used the permutation probability, relative excess, and the location of the maximum histogram excess.

No rule was changed after case construction.

### 5.4 Blind results

Before reveal, the three frozen verdicts were:

- `case_73879439` → `REJECT`;
- `case_a22e176c` → `REJECT`;
- `case_d9ce21ef` → `SURVIVE`.

The corresponding result files were hashed before the truth key was opened.

The reveal showed:

- `case_a22e176c` = NULL → `REJECT`;
- `case_73879439` = WEAK → `REJECT`;
- `case_d9ce21ef` = POSITIVE → `SURVIVE`.

The benchmark therefore passed all three preregistered constraints.

The positive case was strong: \(T_{\rm obs}=364\) against a null median of 18, permutation \(p=0.001\), relative excess \(+19.22\), and a peak at 91 GeV.

The controlled benchmark verdict was:

\[
\texttt{PASS\_3\_CONSTRAINTS\_OF\_3}.
\]

### 5.5 What this benchmark does and does not establish

The CMS exercise demonstrates controlled cross-domain transfer of several protocol components:

- blind analysis;
- truth construction independent of the classifier;
- null design;
- preregistered decision rules;
- frozen results before reveal;
- provenance checks.

It does not establish validity on an unresolved scientific question. The cases were deliberately constructed from known mechanisms.

The `WEAK` case also produced `REJECT`, not `GRAY`. The prospective handling of a genuinely ambiguous external case therefore remained untested at this stage. No fourth case was added to manufacture a gray result.

Two of the three constraints were weakly discriminating by design: the positive case is the Z-boson peak (\(T_{\rm obs}=364\) against a null median of 18), and the admissible set for `WEAK` includes the verdict of `NULL` (`REJECT`). The PASS 3/3 should therefore be read as evidence that the construction, blinding and hashing mechanics worked, not as evidence of classifier sensitivity.

---

## 6. Case study III: prospective TESS candidate with future adjudication

### 6.1 Why TESS adds a different test

A controlled benchmark can test logic, but its truth is still known to the benchmark constructor.

The TESS case was designed so that final adjudication is not known at analysis time.

The target was selected mechanically from the NASA Exoplanet Archive (2025-2026) TOI table before any light-curve access. The Archive documents TFOPWG dispositions including `PC`, `APC`, `CP`, `KP`, `FP`, and `FA`, and notes that the TOI table is periodically synchronized from ExoFOP. The TESS mission and its public photometric products are described by Ricker et al. (2015); mission-produced and high-level light curves are distributed through MAST (TESS Team 2021; Caldwell et al. 2020; Huang 2020).

### 6.2 Frozen target selection

The selector used a tiered rule based only on public metadata such as TOI disposition, creation date, TESS magnitude, orbital period, catalog transit depth, candidate radius, and duration.

No light curve was accessed during selection.

The selected target was:

\[
\text{TOI 7698.01}
\]
(TIC 241577487),

with snapshot disposition `PC`, period 4.5701356 days, catalog depth approximately 341 ppm, candidate radius approximately \(1.67\,R_\oplus\), and TESS magnitude 9.82.

The target JSON and the catalogue snapshot were hashed before photometric analysis.

### 6.3 Frozen photometric path

Light curves were then acquired under a product-selection rule fixed before flux inspection.

The canonical light curve contained 48,678 cadences from sectors 3, 30, 70, and 97 and was frozen under SHA256 before the decision statistic was calculated.

The primary event estimator used the catalog ephemeris, local sideband detrending, and median in-transit depth. The null consisted of 999 phase shifts evaluated with the identical event estimator.

Additional frozen vetoes tested odd/even depth differences and a possible phase-0.5 secondary signal.

### 6.4 Prospective verdict

The analysis produced 26 usable transit events with median depth

\[
353.6~{\rm ppm},
\]

close to the catalog value.

The phase-null probability was

\[
p=0.001,
\]

the minimum accessible value under 999 null realizations and exactly the preregistered survival threshold.

The fraction of events with positive depth was 0.885.

The odd/even comparison was non-significant:
\[
p=0.503,
\]
with relative difference approximately 0.154.

The secondary-depth ratio was zero under the frozen estimator.

The preregistered verdict was therefore

\[
\boxed{\texttt{SURVIVE}}.
\]

This result was immediately hashed.

The meaning of `SURVIVE` is deliberately limited:

> the archived TESS photometry supports a coherent transit-like signal at the frozen ephemeris without a preregistered strong photometric veto.

It does not mean that the object is a confirmed planet.

### 6.5 Future adjudication

At the time of freezing, TOI 7698.01 remained `PC`.

The external directional mapping was frozen as:

- `SURVIVE` + future `CP/KP` → prospective success;
- `SURVIVE` + future `FP/FA` → prospective failure;
- continued `PC/APC` → pending.

No later photometric re-analysis is permitted to alter the frozen verdict.

No adjudication horizon is set (author's decision of 9 November 2026): the case stays open until the external disposition changes. It can therefore not fail within any bounded time, and it is not counted as evidence for or against the methodological claim; its role is to demonstrate the freezing and archiving mechanics. A later `CP` or `KP` disposition would be recorded as agreement with the frozen verdict, and `FP` or `FA` as disagreement. Note also that \(p=0.001\) is the minimum attainable with 999 phase shifts, so the survival threshold coincides with the resolution floor of the null.

This makes the TESS case qualitatively different from CMS. Its final adjudication is genuinely deferred.

However, this is not an independent TESS discovery experiment. Target selection already uses TOI metadata generated by the TESS vetting ecosystem, including a catalog ephemeris and candidate status. The case therefore tests prospective workflow discipline and robustness of a frozen photometric classifier; it does not estimate the false-positive rate of a blind transit search from raw pixels.

---

## 7. Case study IV: blind gravitational-wave benchmark and accepted transfer failure

### 7.1 Motivation

The first three cases did not combine all of the following: raw time-series data, multiple detectors, non-Gaussian transient noise, a waveform bank, empirical inter-detector backgrounds, and a strict possibility that the transferred implementation itself would fail.

The GWOSC benchmark was therefore preregistered as a **heavy final active benchmark**, not as a new gravitational-wave search. O4b public strain data are available from LIGO Hanford (H1), LIGO Livingston (L1), and Virgo (V1), and GWTC-5.0 documents probable O4b events and provides associated strain products. GWTC-5.0 includes events with \(p_{\rm astro}>0.5\), while the public release provides data-quality information and event-level strain (GWOSC 2026a,b).

The simplified analysis used PyCBC matched filtering, whose established scientific use relies on substantially richer ranking statistics, vetoes, banks, and background estimation than the deliberately compact benchmark implemented here (Usman et al. 2016). Consequently, the benchmark result evaluates **our frozen transfer implementation**, not LVK event validity or the PyCBC search itself.

### 7.2 Metadata-only case selection

Before strain access, a selector queried GWTC-5.0 metadata (GWOSC 2026b) and froze two real events.

The `STRONG` rule required H1 and L1, \(p_{\rm astro}\ge0.99\), network SNR \(\ge12\), and selected the earliest admissible event by GPS time. This yielded

\[
\text{GW240413\_022019},
\]

with \(p_{\rm astro}=0.99\), catalog network SNR 18.1, and detectors H1/L1/V1.

The `BORDERLINE` rule used preregistered tiers. The first non-empty tier required H1/L1,

\[
0.50\le p_{\rm astro}<0.65,\qquad 7\le\rho_{\rm network}\le10,
\]

and selected the earliest admissible event. This yielded

\[
\text{GW240408\_081753},
\]

with \(p_{\rm astro}=0.61\) and catalog network SNR 8.3.

The metadata snapshot, selected-event record, and selection manifest were hashed before strain access.

### 7.3 Exogenous blind construction

After selection was frozen, public H1/L1 strain was downloaded and resampled to 2048 Hz. Three anonymized cases were constructed:

- `STRONG_REAL`: real strain around the strong event;
- `BORDERLINE_REAL`: real strain around the borderline event;
- `TIMESHIFT_NULL`: H1 around the strong event with L1 deterministically shifted by +0.250 s.

The builder imported no analysis classifier and calculated no matched-filter statistic, PSD, p-value, or verdict. The manifest recorded `builder_classifier_calls = 0`.

Truth labels were hidden behind SHA256 commitments. The three blind `.npz` files were hashed and verified against the public manifest before analysis.

### 7.4 Frozen matched-filter classifier

The analysis was executed in the pinned container

`pycbc/pycbc-el8@sha256:c9ca4317622bae61b7912a370733dcfd81d3ddca101193fb5fc7874dcf1b6180`

with PyCBC 2.11.0.

The frozen implementation used:

- 2048 Hz strain;
- 20–512 Hz matched-filter band;
- median Welch PSD using 8 s segments and 4 s stride;
- inverse-spectrum truncation;
- a fixed 24-template non-spinning IMRPhenomD bank;
- per-detector envelope \(E_d(t)=\max_\theta |\rho_d(t,\theta)|\);
- a network statistic maximizing H1/L1 envelope power near the segment center;
- 200 fixed non-zero L1 time slides between 0.1 and 8 s in magnitude.

The empirical null probability was

\[
p_{\rm slide}
=
\frac{1+\#(\rho_{\rm null}\ge\rho_{\rm obs})}{201}.
\]

The balance statistic was

\[
B=
\frac{\min(\rho_{H1}^2,\rho_{L1}^2)}
{\rho_{\rm net}^2}.
\]

The preregistered classifier was:

\[
p_{\rm slide}\le0.005,\ B\ge0.05
\Rightarrow \texttt{SURVIVE},
\]

\[
p_{\rm slide}\ge0.10\ \text{or}\ B<0.02
\Rightarrow \texttt{REJECT},
\]

and `GRAY` otherwise.

### 7.5 Blind results and reveal

Before reveal, the frozen outputs were:

| Blind case | \(\rho_{\rm net}\) | \(p_{\rm slide}\) | \(B\) | Frozen verdict |
|---|---:|---:|---:|---|
| `case_0213b2ed` | 6.714 | 0.06468 | 0.481 | `GRAY` |
| `case_3a620b4e` | 8.768 | 0.25871 | 0.164 | `REJECT` |
| `case_8157794e` | 6.201 | 0.61194 | 0.382 | `REJECT` |

All three result JSON files were hashed before opening the truth key.

The reveal mapped them to:

- `case_0213b2ed` = `STRONG_REAL` → `GRAY`, while only `SURVIVE` was admissible: **FAIL**;
- `case_3a620b4e` = `BORDERLINE_REAL` → `REJECT`, while `SURVIVE` or `GRAY` were admissible: **FAIL**;
- `case_8157794e` = `TIMESHIFT_NULL` → `REJECT`: **OK**.

The strict benchmark verdict was therefore

\[
\boxed{\texttt{GWOSC\_HEAVY\_BENCHMARK = FAIL}}.
\]

### 7.6 Interpretation and closure

The simplified implementation showed specificity against the constructed time-shift null but insufficient sensitivity to the two real selected events under its own frozen rules.

The failure was driven primarily by the time-slide background rather than the detector-balance veto: the strong real event had \(B=0.481\) yet \(p_{\rm slide}=0.0647\), producing `GRAY`; the borderline real event had \(B=0.164\) and \(p_{\rm slide}=0.2587\), producing `REJECT`.

No new template bank, PSD, frequency band, time-slide range, threshold, event, or fourth case was introduced after reveal. Any later investigation of why the simplified classifier underperformed is restricted to methodological characterization and cannot replace the v1 verdict.

A preregistration/code numerical mismatch was also retained rather than repaired post hoc. The preregistration described a \(\pm15\) ms H1/L1 lag bound, while the frozen code implemented 31 samples at 2048 Hz, corresponding to \(\pm15.13671875\) ms. Because this was identified only after blind results were frozen, no rerun was allowed.

This negative result is important for the protocol claim: a workflow that only records successful transfers cannot demonstrate resistance to adaptive rescue.

---

## 8. Applications not used as principal evidence

### 8.1 Radial-velocity exoplanet transfer test (partial, 2/3)

Before the principal transfers of Sections 5–7, the protocol (then v2.0) was applied to a first foreign domain, radial-velocity detection of exoplanets, in replication mode (28–29 July 2026). The design was a paired, three-branch test: a phantom (HD 41248, a 25.6-day signal attributed to stellar rotation, Faria et al. 2020 conclude that the radial-velocity variations are explained by stellar activity and that the data do not provide enough evidence for a planet; this reference verdict is a published model preference, not a proof of absence), a real control (HD 219134 b, transiting, with an orthogonal verifier given by the transit; Gillon et al. 2017), and a synthetic control (a Keplerian signal with \(K=2.25\) m/s injected into the phantom's activity and sampling). A divergence from the expected verdict on at least one branch was defined in advance as a transfer failure.

The initial phantom target, \(\alpha\) Cen B (see Rajpaul et al. 2016 for the status of its putative planet), was abandoned before any decision run: its canonical dataset could not be retrieved by any automatic route, and a reconstruction failed an a priori fidelity gate (rms 12 against 1.5 m/s). The change was recorded in a dated addendum and the target became HD 41248.

Two preregistered iterations were run. In v1 the thresholds were transferred from the control, and 1/3 branches gave the expected verdict (the control only). In v2 the thresholds were calibrated per target and the null hyperparameters were marginalised; 2/3 branches gave the expected verdict (control and injection recovery) and the phantom remained in the grey zone. No threshold was moved after a decision run. A v3 based on Bayesian evidence was specified but not executed, and the test was closed by human decision with a known path to resolution.

The lessons recorded in the 29 July amendment were: the verifier must be accessible, not only exact and exogenous; decision thresholds must be calibrated per target (P10); the decision statistic must match the nuisance mechanism (P11); and an untested self-diagnosis proved wrong (F14). The amendment was headed "to be merged" and was not: protocol v2.1 of 31 August (written after B2) and v2.2 FINAL contain neither P10, P11 nor F14, and use the label F11 for another failure mode (§3.0). The first transfer test thus left its lessons outside the document that governed the principal cases. They were merged on 9 November 2026 into protocol v2.3 DRAFT (principles P10 and P11, failure mode F14 and an accessible-verifier requirement in the central theorem), after the principal cases had been closed.

### 8.2 Mathematical demonstration (illustrative)

A demonstration was run in experimental mathematics on the number of regions of a circle cut by the chords joining \(n\) generic points (Moser's circle problem), with a hash-committed prediction, preregistration `0a2d749c…` (full hash not recoverable from the archived notes [TO INSERT if available]) and seed 20260808. The run hash is `cf21159d2bb44e60e44cf90cc36d6c0460d5edb3c8af94b0c6b82c275d758e7d`, the SHA-256 of the string `circle_regions [1, 2, 4, 8, 16, 31, 57]`, which anyone can recompute. The note recording the demonstration (`protocole_en_mathematiques.md`) has SHA-256 `563b54a737c15bddde385d7cf0bd7e664377bd829c3be5a7312516308a161fa5`. The observed prefix for \(n=1,\dots,5\) (1, 2, 4, 8, 16) is fitted identically by \(2^{n-1}\) and by \(1+\binom{n}{2}+\binom{n}{4}\), so the data do not discriminate between them. The naive extrapolation \(2^{n-1}=32\) for \(n=6\) was registered and then refuted by an exogenous direct count (Euler's formula on the planar graph of the chords), which gives 31 (and 57 for \(n=7\)).

Here the machinery of §§2.3–2.5 is inapplicable (the problem is exact and noise-free) and the weight of the protocol falls on discipline: recognising the degeneracy, distrusting consensus among humans and language models, and using an exogenous checker. This is an illustrative case, not evidence of transferability. The answer is a textbook example. The prediction "32" was registered by the script itself as the naive extrapolation, so it was seeded as the trap and was not an independent prediction made by an AI system; and the preregistration object and the analysis were produced in the same script run, so there was no temporal separation between them. The case illustrates the mechanics (degeneracy check, registered prediction, exogenous checker), not a test of whether the workflow resists a wrong extrapolation.

### 8.3 A registered but parked prospective solar-flare case

A solar-flare forecast was preregistered after the main cross-domain cases.

The next complete UTC day was selected before reading the current NOAA forecast. Thresholds were frozen as:

- NOAA M-class probability \(\ge60\%\) → event expected;
- probability \(\le20\%\) → no M-class event expected;
- intermediate probability → `GRAY`.

For the target day 1 September 2026, the frozen NOAA probability was 10%, producing a `REJECT` / no-M1+-expected prediction.

This forecast is intentionally **parked**. It is not treated as active methodological development and contributes no adjudicated evidence to the conclusions of this draft. Its remaining role is prospective verification under the frozen GOES XRS criterion.

Prospective registrations can be inexpensive to maintain, but each additional active analysis pipeline creates provenance and coordination overhead. This manuscript therefore treats MaNGA, CMS, TESS, and GWOSC as the four principal methodological cases.

### 8.4 Other applications listed in §1.2

The remaining rows of Table 1.2 are summarised below. The RAR/SPARC investigation uses real data; the omics and finance demonstrations use simulated data and are illustrative, like §8.2; HYDRO and wbt-gaia are prospective and unresolved.

#### 8.4.1 RAR / SPARC (real data, 29–30 July 2026)

The protocol was applied in prediction-registration mode to the radial acceleration relation of SPARC galaxies (Lelli et al. 2016; 3317 points in 175 galaxies, frozen table). At fixed baryonic acceleration, the residuals of the relation are independent of surface brightness (\(\rho=-0.01\)) but correlate with gas fraction (\(\rho=-0.166\)). The preregistered prediction, hashed on 29 July 2026 (SHA-256 `f3d3006b524881ae9492014a24004a77ab823bb0ab5958257ded786a9a24a5ea`), was that this correlation is mostly a mass-to-light (M/L) degeneracy rather than a fundamental second parameter, to be falsified if independent per-galaxy M/L values left \(|\rho|\) above 0.15. With the per-galaxy M/L values of Li et al. (2020), \(\rho=-0.157\): the correlation persisted above the threshold and the prediction was refuted on its own terms. The threshold was not moved and the original hash was kept.

A subsequent exploratory analysis found that the correlation is very sensitive to the assumed gas mass (\(\rho=-0.086\) for a gas contribution scaled by 0.75, \(+0.017\) for 0.5; \(\rho=-0.143\) with a global gas fraction independent of the rotation-curve decomposition). The working notes concluded that a plausible gas systematic suffices and that the original prediction was "refuted in its letter, vindicated in its spirit". This paper does not retain that second statement: the gas explanation was found after the refutation, was not preregistered, and has not been tested against independent HI masses (the cleaner test, not undertaken). Presenting it as a vindication would be the kind of adaptive rescue that §2.7 excludes. The M/L values of Li et al. were themselves fitted to rotation curves, so the refutation is not fully external either. [TO CONFIRM: wording; the SHA-256 of the closure note `rar_gas_last_blade.md` is `29cb069d30a46daaaa5c4d53f6b03edcaf9cf29b19f704d41198460b104a610c`.]

#### 8.4.2 Simulated case-control omics (illustrative)

A simulated case-control study (20,000 genes, 40 subjects; seed 20260810, preregistration `529a7403…`, run hash `a215ee58…` [TO INSERT full hashes if recoverable]) has two steps. With no signal, 975 genes are nominally significant at \(p<0.05\) (about 5%), none survives Bonferroni, and the observed count equals the permutation null. With a perfect batch confound and no biology, 8201 genes are nominally significant and 594 survive Bonferroni; a naive label permutation falsely confirms the signal (the confounded statistic is a true systematic difference, so permuting labels lowers the null), and only a control for the batch brings the count to zero. The case illustrates that multiple-comparison correction is necessary but not sufficient, and that confound control is the demanding discipline. As in §8.2, design and analysis were produced in one session, so it illustrates mechanics, not transfer.

#### 8.4.3 Simulated backtest overfitting (illustrative)

On a purely random market with no edge (seed 20260812, preregistration `33a1e493…`, run hash `0f1e0cc9…` [TO INSERT full hashes if recoverable]), the best Sharpe ratio among \(N\) independent strategies grows roughly as \(\sqrt{2\ln N}\): \(-0.12\) for 1, 0.65 for 10, 1.05 for 100, 1.29 for 1000 and 1.37 for 5000. A per-strategy test gives \(t=3.3\) (\(p=9\times10^{-4}\)); the best-of-5000 null (median 1.50) gives a corrected \(p=0.89\); one strategy fixed in advance gives a Sharpe ratio of \(-0.48\). Two earlier attempts of the same session were kept visible: 150 strategies were too few to show an effect, and a grid of 2022 correlated moving-average variants plateaued at 0.76, which showed that the effective multiplicity is not the nominal one. [TO VERIFY before citing: the deflated Sharpe ratio of Bailey and López de Prado, SSRN 10.2139/ssrn.2460551.]

#### 8.4.4 HYDRO and wbt-gaia (prospective, unresolved)

HYDRO is a prospective streamflow forecast on public USGS data run with the same workflow; version 8 was paused on 7 October 2026, with a preregistration freeze deadline of 10 January 2027 [TO CONFIRM wording]. wbt-gaia is a preregistered, blinded test of wide-binary kinematics (Newtonian versus MOND), with Gaia DR3 as rehearsal and Gaia DR4 as target; its configuration was frozen by the annotated tag `gel-interne-v0.9.17` (commit `7f0c44c`) on 9 November 2026, ahead of the DR4 release on 2 December 2026. A secondary statistic was closed on 18 October 2026 against four preregistered criteria. Neither application has produced an outcome at the date of this draft.

---

## 9. Discussion

### 9.1 The main methodological result is closure discipline

The strongest feature of the framework is not its ability to detect signals.

It is its ability to stop.

In MaNGA, the correct result was closure by non-identifiability. In CMS, the correct action was to discard the first benchmark before analysis because the verifier was endogenous. In TESS, the correct action after `SURVIVE` was not to keep optimizing the pipeline but to freeze the result and wait for external adjudication. In GWOSC, the correct action after the strong real event failed to reach `SURVIVE` was to record the benchmark as `FAIL`, not to enrich the bank or weaken the threshold.

These cases share a common structure: a useful protocol must constrain what researchers are allowed to do after a result becomes inconvenient, ambiguous, exciting, or unfavorable to the protocol itself.

### 9.2 AI systems amplify both productivity and adaptive risk

Multi-agent AI workflows make it unusually easy to generate additional tests.

A model can always propose another estimator, another simulation, another subset, another robustness analysis, or another benchmark. This abundance is beneficial during generation and dangerous during validation.

The stopping rule is therefore not bureaucratic overhead. It is a direct response to the low marginal cost of generating post hoc alternatives.

### 9.3 Provenance is part of inference

F12 showed that a scientifically stable conclusion can coexist with an archive failure.

This is not merely a software-engineering concern. If the executed path is not recoverable, readers cannot determine whether the published decision actually corresponds to the preregistered procedure.

Executable provenance must therefore be treated as part of the inferential object.

### 9.4 A benchmark can be blind and still be circular

F13 is particularly relevant to AI evaluation.

Hiding labels from the analyst is insufficient if the benchmark constructor used the classifier to choose which cases enter the benchmark.

This applies far beyond the present CMS example. Any evaluation in which examples are admitted, rejected, or tuned after observing the evaluated system's outputs risks converting external validation into self-consistency testing.

### 9.5 A failed transfer is informative about discipline, not about performance

The GWOSC case changes the interpretation of the cross-domain evidence.

The framework should not be described as a universally successful scientific classifier. It clearly is not: the deliberately simplified GW implementation failed two of three preregistered case constraints.

The relevant success is procedural. The workflow preserved blinded construction, external case definition, fixed rules, pre-reveal hashes, and the failure verdict after reveal. In other words, the framework was able to generate evidence *against the adequacy of its own transferred implementation* without opening an adaptive rescue path.

This is an important distinction between **methodological integrity** and **scientific performance**.

The failure should not be over-read as a property of the protocol, nor of matched filtering. The strong real event (catalogue network SNR 18.1) was recovered by the frozen implementation with \(\rho_{\rm net}=6.714\), a loss by a factor of about 2.7. This points towards limitations of the compact implementation (a 24-template non-spinning bank, the PSD estimation, the 2048 Hz resampling) rather than towards a sensitivity limit of the data. The cause is not diagnosed here, because no investigation was permitted to alter the v1 verdict.

### 9.6 Transferability evidence is not additive without limit

There is diminishing methodological value in adding domains indefinitely.

The four principal cases now occupy distinct logical roles:

1. MaNGA tests whether the protocol can close an attractive scientific claim.
2. CMS tests controlled blind transfer with exogenous constructed truth.
3. TESS tests prospective freezing while the final external disposition remains unknown.
4. GWOSC tests whether a transferred implementation can fail under blind conditions without triggering a rescue analysis.

A fifth active domain would add coordination and provenance cost faster than it adds conceptual coverage. Future gains should come from adjudicating already-frozen prospective cases, formalizing the protocol, and comparing it against alternative workflows rather than increasing the domain count.

### 9.7 What would count against the methodological claim

The claim of Section 13 is falsifiable only if some outcomes would count against it. The following would, and they are stated here before any further case is run. [PROPOSAL: author to validate or amend.]

First, a closed claim whose verdict is changed by a later analysis that the stopping rule should have excluded, without the change being flagged in the archive. Second, an archived package whose clean rerun fails to regenerate the reported decision quantities, discovered after the package was labelled closed (F12 recurring after its countermeasure). Third, an independent reproduction, by someone outside the author's multi-agent workflow, that reaches a different frozen verdict from the same frozen inputs and code. Fourth, a prospective case adjudicated in the direction opposite to its frozen verdict, which would be recorded as a failure of that case and not as noise. Fifth, once such a comparison is performed, a less constrained workflow showing no difference in the rate of unflagged post hoc changes.

Outcomes that would not count against the claim are those the framework explicitly allows: non-identifiability, rejection, ambiguity, a failed benchmark, or a pending case.
---

## 10. Limitations

Several limitations should be explicit.

First, the protocol itself was developed through iteration. Its strongest failure-mode rules were learned from actual mistakes. The framework is therefore empirically hardened rather than deductively complete.

Second, CMS is a controlled benchmark, not an unresolved research problem.

Third, the TESS verdict is not yet externally adjudicated. It currently demonstrates prospective discipline, not predictive success.

Fourth, the framework does not guarantee that a chosen statistic is powerful. It is designed to make failure, ambiguity, and non-identifiability visible without adaptive rescue.

Fifth, a formal comparison against alternative human-only or single-model workflows has not yet been performed.

Sixth, the TESS verdict is still pending and therefore cannot currently be counted as predictive success.

Seventh, GWOSC v1 failed its preregistered transfer criterion. This is not a nuisance result to average away: it demonstrates that the simplified fixed bank and empirical background used here are not an adequate general gravitational-wave classifier under the frozen rules.

Eighth, the GWOSC preregistration contained a small numerical specification mismatch: “±15 ms” corresponded in the frozen implementation to ±31 samples at 2048 Hz, or ±15.1367 ms. The mismatch did not trigger a rerun, but it illustrates why executable specifications are preferable to prose alone.

Ninth, the protocol has not yet produced a fully externally adjudicated natural `GRAY` case. GWOSC produced `GRAY` for a known strong event, but that was a classifier failure, not an unresolved external truth state.

Tenth, all applications were designed and executed by one author with several AI systems, and none has been independently reproduced. Eleventh, the principal cases were governed by protocol v2.2 FINAL, which does not incorporate the lessons recorded after the first, partially failed, transfer test (§8.1); the merge into v2.3 DRAFT came only afterwards (9 November 2026). Twelfth, the three latest principal cases (CMS, TESS, GWOSC) were designed, run and closed within a single day (31 August 2026, about four hours), so no interval for reflection separated them, and the governing protocol (v2.2 FINAL) was itself finalised ten minutes before the first of them; this is consistent with the low-friction setting the paper addresses, but it limits the scrutiny each case received.

---

## 11. Reproducibility and archival requirements

For each closed analysis package, the minimum archive should contain:

1. preregistration or equivalent frozen decision document;
2. exact executed code;
3. input manifests and hashes;
4. explicit random seeds;
5. environment/package information;
6. commands used for execution;
7. output tables and logs;
8. result hashes;
9. a closure note recording the logical interpretation and any provenance exception.

A package should not be described as fully closed until a clean rerun reproduces the decision quantities.

For MaNGA C1–C3, the final F12 archive satisfies this requirement with `STATUS = PASS`.

For the CMS benchmark, blind result hashes were frozen before reveal and the reveal log was subsequently hashed.

For TESS, the target, catalogue snapshot, canonical light curve, and final analysis result were all frozen before any future external adjudication.

For GWOSC, metadata selection was frozen before strain access; the builder recorded zero classifier calls; the three blind strain cases matched hashes in the public manifest; PyCBC was executed from a Docker image pinned by digest; the three result JSON files were hashed before reveal; and the strict `FAIL` was retained after opening the committed truth key.

---

## 12. Recommended multi-agent workflow

A practical implementation can be summarized as follows.

### Phase 0 — question and falsification

Define the target claim, statistic, null alternatives, decisive thresholds, and stopping rule before the final analysis.

### Phase 1 — generation

Allow broad hypothesis and method generation. This is the permissive phase.

### Phase 2 — freeze

Choose the estimator, sample, preprocessing, controls, RNG policy, and decision thresholds.

Hash the preregistration.

### Phase 3 — execution

Run the frozen analysis through one canonical script per decision object where possible.

Do not interpret intermediate failures by inventing new gates.

### Phase 4 — degeneracy and adversarial review

Ask whether an ordinary alternative model passed through the full observational operator can occupy the same decision region.

Use an adversarial critic whose role is to invalidate the claim if technically justified.

### Phase 5 — verdict

Apply the preregistered decision rule.

If a closure criterion is met, freeze the scientific status before any additional characterization.

### Phase 6 — executable closure

Rerun the archived code from a clean location.

Verify hashes, inputs, outputs, seeds, and commands.

Only then label the package closed.

### Phase 7 — external adjudication

Where possible, register a future verifier that is independent of the analysis.

Do not reopen the frozen analysis when the external truth arrives.

---

## 13. Conclusion

AI-assisted empirical science does not primarily need more ways to generate analyses. It needs stronger rules for deciding when an analysis may no longer change its scientific conclusion.

The framework developed here combines preregistration, multi-agent role separation, identical-code forward modelling, paired comparisons, exogenous verification, explicit stopping, and executable provenance.

Its development produced four deliberately non-uniform outcomes. MaNGA closed an attractive astrophysical interpretation as non-identifiable. CMS exposed a circular benchmark before blind analysis and then passed a corrected exogenous benchmark. TESS produced a real prospective `SURVIVE` decision that remains externally unresolved. GWOSC failed its strict cross-domain transfer criterion, and the failure was frozen rather than repaired.

That heterogeneity is the central result. The framework is not presented as a machine for producing positive findings or as evidence that a particular classifier generalizes across domains. It is a governance structure for empirical inference under high analytic flexibility.

The methodological claim is therefore modest but testable:

> AI-assisted research becomes more credible when survival, rejection, ambiguity, non-identifiability, provenance exceptions, and implementation failure are all allowed to become terminal, hashed outcomes.

The next evaluation step should not be another scientific domain. It should be external scrutiny of the protocol itself: independent reproduction, comparison against less constrained workflows, and adjudication of the already-frozen prospective cases.

---

## Declarations

**Use of AI.** The analyses, simulations and drafts of this work were produced by the author with several AI systems (Claude, ChatGPT, DeepSeek and Grok) in the roles described in Section 2.1. The author made every decision on freezing, closure and interpretation. No AI system is an author. [TO COMPLETE: which system performed which role in which case.]

**Availability.** Code, preregistrations, manifests and hashes are published on GitHub only: https://github.com/Eone162116/multiia-method (working draft tagged `v0.5-draft`; [TO INSERT: freeze tag of the final version]). No journal submission and no other archive deposit has been made.

**Known integrity incident.** F10 (§3.0) concerns an earlier public archive record. [TO CONFIRM wording: the corrected archive was prepared but not deposited, and the original record remains online with the defect described.]

---

## References

Abdurro’uf et al. (2022). *The Seventeenth Data Release of the Sloan Digital Sky Surveys: Complete Release of MaNGA, MaStar, and APOGEE-2 Data.* **The Astrophysical Journal Supplement Series, 259**, 35. https://doi.org/10.3847/1538-4365/ac4414

Caldwell, D. A., Jenkins, J. M., & Ting, E. B. (2020). *TESS Light Curves From Full Frame Images ("TESS-SPOC").* STScI/MAST. https://doi.org/10.17909/t9-wpz1-8s54

Faria, J. P., Adibekyan, V., Amazo-Gómez, E. M., et al. (2020). *Decoding the radial velocity variations of HD 41248 with ESPRESSO.* **Astronomy & Astrophysics, 635**, A13. https://doi.org/10.1051/0004-6361/201936389

Gillon, M., Demory, B.-O., Van Grootel, V., et al. (2017). *Two massive rocky planets transiting a K-dwarf 6.5 parsecs away.* **Nature Astronomy, 1**, 0056. https://doi.org/10.1038/s41550-017-0056

GWOSC (2026a). *The O4b Data Release.* Gravitational Wave Open Science Center. Dataset DOI: https://doi.org/10.7935/8emv-ag54

GWOSC (2026b). *GWTC-5.0 Data Release Documentation.* Gravitational Wave Open Science Center. Data-release DOI: https://doi.org/10.7935/bk00-6a89

Huang, C. X. (2020). *TESS Lightcurves From The MIT Quick-Look Pipeline ("QLP").* STScI/MAST. https://doi.org/10.17909/t9-r086-e880

Lelli, F., McGaugh, S. S., & Schombert, J. M. (2016). *SPARC: Mass models for 175 disk galaxies with Spitzer photometry and accurate rotation curves.* **The Astronomical Journal, 152**, 157. https://doi.org/10.3847/0004-6256/152/6/157

Li, P., Lelli, F., McGaugh, S., & Schombert, J. (2020). *A comprehensive catalog of dark matter halo models for SPARC galaxies.* **The Astrophysical Journal Supplement Series, 247**, 31. https://doi.org/10.3847/1538-4365/ab700e

McCauley, T. (2014). *Dimuon event information derived from the Run2010B public Mu dataset.* CERN Open Data Portal. https://doi.org/10.7483/OPENDATA.CMS.CB8H.MFFA

Munafò, M. R., Nosek, B. A., Bishop, D. V. M., et al. (2017). A manifesto for reproducible science. **Nature Human Behaviour, 1**, 0021. https://doi.org/10.1038/s41562-016-0021

NASA Exoplanet Archive (2025–2026). *TESS Objects of Interest Table Data Column Definitions* and *TESS Project Candidates*. California Institute of Technology/NASA Exoplanet Science Institute. https://exoplanetarchive.ipac.caltech.edu/docs/API_TOI_columns.html

Nosek, B. A., Ebersole, C. R., DeHaven, A. C., & Mellor, D. T. (2018). The preregistration revolution. **Proceedings of the National Academy of Sciences, 115**, 2600–2606. https://doi.org/10.1073/pnas.1708274114

Rajpaul, V., Aigrain, S., & Roberts, S. (2016). *Ghost in the time series: no planet for Alpha Cen B.* **Monthly Notices of the Royal Astronomical Society: Letters, 456**, L6–L10. https://doi.org/10.1093/mnrasl/slv164

Ricker, G. R., Winn, J. N., Vanderspek, R., et al. (2015). Transiting Exoplanet Survey Satellite (TESS). **Journal of Astronomical Telescopes, Instruments, and Systems, 1**, 014003. https://doi.org/10.1117/1.JATIS.1.1.014003

Simmons, J. P., Nelson, L. D., & Simonsohn, U. (2011). False-positive psychology: Undisclosed flexibility in data collection and analysis allows presenting anything as significant. **Psychological Science, 22**, 1359–1366. https://doi.org/10.1177/0956797611417632

TESS Team (2021). *TESS Light Curves - All Sectors.* STScI/MAST. https://doi.org/10.17909/t9-nmc8-f686

Usman, S. A., Nitz, A. H., Harry, I. W., et al. (2016). The PyCBC search for gravitational waves from compact binary coalescence. **Classical and Quantum Gravity, 33**, 215004. https://doi.org/10.1088/0264-9381/33/21/215004

---

## Internal status of prospective cases at v0.2 freeze

- **TOI 7698.01:** frozen photometric verdict `SURVIVE`; external disposition still pending.
- **Solar flare, target UTC day 2026-09-01:** frozen NOAA-based verdict `REJECT`; outcome pending at manuscript freeze.
- These pending outcomes are not counted as successful validation evidence in the abstract or conclusions.
