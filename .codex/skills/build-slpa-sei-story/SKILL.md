---
name: build-slpa-sei-story
description: >
  Build, audit, and update the research story, causal chain, algorithm logic,
  claim boundaries, figure logic, and evidence closure for the current SLPA-SEI
  paper on source-free online test-time adaptation for time-varying SEI. Use
  automatically for any SLPA-SEI task involving problem framing, temporal-scale
  definitions, algorithm changes, STDA or LTDA roles, figures, experiments,
  claims, paper structure, or consistency between manuscript, code, and evidence.
---

# SLPA-SEI Story Builder

## Purpose and routing

Lock the verified algorithm before discussing novelty, naming modules, designing
figures, or writing paper sections. Convert the method into one causal story
instead of stacking familiar primitives. Separate algorithm decisions from
observations, interpretations, hypotheses, and validated evidence.

Treat this skill as the single source of truth for **SLPA-SEI-specific scientific
content**:

- the research setting, practical problem, and novelty boundary;
- the causal story and the distinction from prior time-varying SEI;
- the active modules, equations, states, parameters, and online order;
- the contribution spine, claim boundaries, figure logic, and evidence closure;
- the datasets, protocols, ablations, and results that can support each claim.

Do not use this skill as the primary store for general academic prose rules,
paragraph style, generic section templates, citation formatting, or LaTeX writing
conventions. Those reusable rules belong to `write-research-paper`. Retain a
section-specific instruction here only when it encodes an SLPA-SEI scientific
decision, evidence boundary, or terminology constraint.

Read `references/current-method.md` whenever locking equations, state variables,
parameters, gradients, or online order. Read
`references/experiment-evidence-2026-08.md` whenever using numerical results,
sensitivity claims, stability claims, backbone comparisons, complexity values,
runtime measurements, efficiency figures, or failure cases. Read
`references/citation-registry.md` before proposing citation keys, generating a
BibTeX block, or adding literature to any SLPA-SEI manuscript section.

Use `write-research-paper` after this skill when producing final academic prose or
LaTeX. The story skill decides what is scientifically true and claimable; the
writing skill decides how that verified content should be structured and
expressed. If code, results, and this contract conflict, identify the conflict and
follow the newest verified implementation or explicit user decision.

### Request-level routing

- For an SLPA-SEI scientific decision, method audit, novelty boundary, experiment
  claim, or figure logic, stay in this skill and load only the matching project
  references.
- For final prose, translation, LaTeX, paragraph organization, or section style,
  first produce a compact verified fact-and-claim packet from this skill, then
  route it to `write-research-paper`.
- For a request to find framing ideas, structural examples, recent citations, or
  academic collocations, route literature retrieval and writing-reference lookup
  to `write-research-paper`. Use this skill afterward to test whether the borrowed
  framing matches SLPA-SEI's setting and novelty boundary.
- For a new paper supplied as a reference, do not store its general writing
  patterns here. Send them to the external-paper corpus and phrase bank owned by
  `write-research-paper`; retain only an SLPA-SEI-specific comparison or claim
  boundary when it changes the project story.
- For a verified paper cited by SLPA-SEI, check the project citation registry
  before assigning a key. Reuse the registered key and keep one bibliography
  record for that paper. Add a new registry record only after its identity and
  publication metadata have been verified.
- For new code, results, or an explicit algorithm decision, update the project
  source of truth before drafting or polishing text.

Use one handoff cycle: story lock -> writing draft -> story consistency check.
Avoid repeatedly sending unchanged prose between the two skills.

## 1. Locked current method

### 1.1 Research setting

Treat SLPA-SEI as a method for closed-set specific emitter identification under:

- source-free, unlabeled, online test-time adaptation;
- time-varying wireless reception conditions;
- a fixed registered-emitter set;
- one online update per adaptation step or short-term observation interval;
- persistent model parameters and a compact historical prediction reference;
- Batch Normalization (BN)-only adaptation, with all other trainable parameters
  frozen, when this matches the verified code.

Treat `source-free` only as an information-access condition. It means that the
source training signals are unavailable during online adaptation. It does not
explain sequential signal arrival, persistent updating, or the influence of one
online adjustment on later identification. In the Abstract and Introduction,
prefer the concrete operational statement `without access to source training
signals during adaptation` when that wording advances the argument. Do not force
`source-free` into the framework definition or use it as the grammatical subject
of the continuous online process.

Use `short-term observation interval` only when acquisition order or an explicit
temporal stream is preserved. Otherwise use `adaptation step`. Keep prediction
before update and adapt-before-score protocols distinct.

### 1.2 Final algorithm structure

The current method name is **Short- and Long-Term Predictive Alignment for
Specific Emitter Identification (SLPA-SEI)**. The short and long terms denote two
online adaptation timescales; they are not two states aligned directly to each
other. The only active method organization is

\[
\mathrm{SLPA\text{-}SEI}
=
\mathrm{STDA}
+
\mathrm{LTDA}.
\]

The modules are:

1. **Short-Term Decision Alignment (STDA)** for the current prediction structure;
2. **Long-Term Distribution Alignment (LTDA)** for current-to-history prediction-
   distribution alignment.

Use **dual-timescale predictive alignment** as the umbrella story. Do not restore
Propagation-Guided Channel Intervention (PGCI), independent data augmentation,
CO-SigDEM, channel-direction projection, Hi-MEC, EMA-MEC, Confidence Balance
(CB), a transmitter-wise confidence state, confidence gating, or reliable-sample
selection as current method components.

### 1.3 No-new-hyperparameter lock

Keep the existing method parameter names:

- `lambda_mec`, written as \(\lambda_{\mathrm{mec}}\), weights LTDA relative to STDA;
- `ema_momentum`, written as \(\mu\) after defining the code-name mapping, controls
  the update of the historical prediction reference.

Do not introduce \(\lambda_{\mathrm{ME}}\), \(\lambda_{\mathrm{LT}}\), a new
divergence weight, an adaptive gate, a threshold, or another method hyperparameter.
Treat \(\epsilon\) used for numerical safety as an implementation constant, not a
tunable contribution.

## 2. Core causal story

### 2.1 Practical phenomenon

Time-varying wireless reception conditions change the received signal and can
degrade the emitter decisions of a source-trained SEI model. Because each online
update is retained, an erroneous or biased decision introduced by one incoming
signal batch can also affect the identification of later batches.

### 2.2 Dual-timescale problem

State two connected but distinct difficulties in communication-facing language:

- **short term:** the received signals in the current observation interval can
  produce ambiguous emitter decisions, and many signals may be assigned to only
  a few registered emitters;
- **long term:** adaptation based only on the current batch lacks a compact
  historical reference, so a locally biased update can continue to influence the
  identification of subsequent batches.

Do not make entropy minimization the physical origin of either problem. Reception
variation produces the mismatch; entropy and divergence are optimization tools.

When contrasting SLPA-SEI with prior time-varying or cross-condition SEI, use the
following boundary. Prior work commonly treats signals acquired at different
times, channels, frequencies, receiver configurations, or propagation conditions
as distinct domains and focuses on source--target mismatch through robust
representations, DA, DG, or current-data adaptation. SLPA-SEI additionally models
the sequential consequence of source-free online updating: an identification
bias at the current step can enter the retained online identifier and influence
later emitter decisions.
Frame the distinction as extending cross-condition adaptation with dual-timescale
online regulation, not as proving that every prior method ignores history.

The two timescales are **adaptation timescales**. They distinguish current-interval
decision distortion from the effect of a retained update on later identification
decisions. Do not equate them with fast and slow physical channel fading unless
the system model and experiments explicitly establish those channel processes.

### 2.3 Methodological response

In the Abstract, Introduction, contributions, and story discussion, present only
the framework and module roles. State that STDA improves emitter identification
within the current observation interval, while LTDA uses information accumulated
from preceding signal batches to maintain identification consistency over time.
Explain their objectives and update operations only in the Proposed Method.

### 2.4 Bounded claim

Claim that the design is intended to coordinate current-interval identification
and identification consistency across successive signal batches. Do not claim
complete channel invariance, semantic alignment, feature alignment, environment
alignment, true activity-prior recovery, guaranteed stability, or robustness to
arbitrary abrupt changes.

### 2.5 Section ownership contract

Once the outline of a major section assigns a topic to each subsection, treat
each assignment as exclusive. Every paragraph, equation, and claim must have one
subsection owner. Do not duplicate material across adjacent subsections and do
not add a bridge paragraph merely to summarize the preceding subsection,
announce the next subsection, or preview its method. Use the fixed heading order
to carry the transition.

For the current SLPA-SEI paper, lock the problem-oriented boundaries as follows:

- **System Model** owns the signal entities, received-signal process, incoming
  signal sequence, available information, online processing order, and generic
  identifier state required to define the operating setting.
- **Problem Description** owns only the difficulties encountered by SEI under
  time-varying reception. It explains how changing reception conditions impair
  identification within the current interval and how a locally inaccurate online
  adjustment can influence later intervals when the adjusted identifier is
  retained. It refers to the entities and processing sequence already established
  in System Model instead of defining them again. It stops after stating the
  unresolved short- and long-timescale identification problem.
- **Problem Formulation** translates that verified problem into
  method-independent mathematical variables, constraints, and optimization
  objectives. It establishes what must be optimized, what information is
  available, and why both temporal scales make the objective necessary. It does
  not derive the proposed module objectives or explain how SLPA-SEI realizes the
  objective.
- **Proposed Method** owns SLPA-SEI, STDA, LTDA, their loss definitions,
  historical-reference construction, update order, trainable-parameter scope,
  component interaction, and solution mechanism.

Accordingly, neither Problem Description nor Problem Formulation may contain
`To address this problem`, name SLPA-SEI, STDA, or LTDA, prescribe the use of
historical information, preview a component, or claim an advantage of the
proposed framework. A Problem Formulation may establish a method-independent
ideal or constrained optimization target, but all component-specific objectives
and update operations belong to Proposed Method.

### 2.6 Abstract- and Introduction-scale story

When building an Introduction, keep the causal story broader than the method
section. Use this sequence:

1. establish SEI as hardware-rooted physical-layer device identification;
2. explain why time-varying reception weakens source-trained SEI;
3. summarize the boundary of offline DA/DG and current-only online adaptation;
4. explain that prior cross-time or variable-channel SEI mainly reduces the
   difference between signals collected under different conditions, whereas
   retained online updates allow a current identification bias to affect later
   batches;
5. identify the short-term ambiguous or concentrated decisions and the long-term
   carry-over of locally biased updates in plain language;
6. introduce SLPA-SEI and give one high-level role sentence for STDA and LTDA;
7. close with problem, method, and validation contributions.

Compress the same causal order for the Abstract instead of changing its
abstraction level.

Do not turn the Abstract or Introduction into a compressed method section. For
SLPA-SEI, keep CE, ME, entropy, JS divergence, EMA, stop-gradient, probability-
distribution definitions, reference-update order, BN-update scope, complexity,
and parameter details out of both sections. Do not discuss decision boundaries,
representation geometry, or similar learning-theory concepts there. Introduce
solution-specific terms only in Proposed Method. Problem Formulation may define
the signal stream, decision variables, information constraints, and the minimum
probability notation needed to state a method-independent optimization objective,
without revealing the loss design, historical-reference construction, or update
rule.

For the SLPA-SEI Problem Description, start from the received-signal and online
processing setting already defined in System Model. Explain in communications
language how time-varying reception affects identification within the current
interval and how retaining each online adjustment creates dependence across
successive intervals. Do not redefine the received-signal model, incoming stream,
generic identifier, or parameter transition in this subsection. Use prose and,
only when necessary, a compact relation built from symbols already defined in
System Model. End with the unresolved short- and long-timescale identification
problem rather than an optimization objective, a proposed response, or a sentence
that leads into the method.

For the SLPA-SEI Problem Formulation, represent the identifier through an implicit
mapping such as \(f_\theta(\mathbf{x})\) or a conditional emitter score. Use the
minimum mathematical variables, information constraints, and method-independent
objective needed to formalize identification under the current reception
condition together with consistency across successive online adjustments. Do not
expand softmax, sigmoid, network layers, entropy objectives, divergence measures,
historical-reference updates, or STDA and LTDA operators. Those definitions belong
to Proposed Method.

## 3. Short-Term Decision Alignment

**Keep the STDA subsection under exclusive STDA ownership.** Do not mention
LTDA, a historical reference, cross-component coordination, or another module as
an opening, transition, comparison, or closing sentence. Put all framework-level
interaction in Overall Method or Joint Objective.

**Do not use `To realize this design` or another repeated formula-announcement
template.** Move directly from the completed methodology argument to the
probability quantity or objective that mathematically implements STDA.

**Do not define STDA as a list of losses or explain its equation line by line.**
The methodology must establish the dual-level current-decision design and its
functional advantages independently of the formula block.

**Do not use `at the signal level`, `at the signal-set level`, `at two levels`,
or similar level-based sentence templates in STDA prose.** Describe the two
scopes with concrete grammatical subjects, for example `For each received
signal`, `Across the current signal set`, `The individual-decision term`, and
`The aggregate emitter statistic`.

**Do not introduce logits, softmax, a backbone forward mapping, a historical
state, or an additional balancing coefficient in STDA.** If emitter probabilities
have not been defined earlier, define them once in prose.

**Audit STDA twice.** During planning, verify that every sentence belongs to the
current signal set and that the design argument is complete without equations.
After drafting, verify the same ownership boundary, remove stock transitions,
and confirm that the compact objective exactly matches the current method.

For probabilities \(p_{i,c}^t\) over \(C\) registered emitters, define

\[
\mathcal H_{\mathrm{CE}}^t
=
-\frac{1}{N_t}\sum_{i=1}^{N_t}\sum_{c=1}^{C}
p_{i,c}^t\log p_{i,c}^t,
\]

\[
\overline p_{t,c}
=
\frac{1}{N_t}\sum_{i=1}^{N_t}p_{i,c}^t,
\qquad
\mathcal H_{\mathrm{ME}}^t
=
-\sum_{c=1}^{C}\overline p_{t,c}\log\overline p_{t,c}.
\]

Lock the scalar objective as

\[
\boxed{
\mathcal L_{\mathrm{STDA}}^t
=
\mathcal H_{\mathrm{CE}}^t
-
\mathcal H_{\mathrm{ME}}^t
}.
\]

Do not add a marginal-entropy coefficient. Explain Conditional Entropy (CE) as
instantaneous identity-decision refinement and Marginal Entropy (ME) as short-term
identity-concentration control. CE promotes decisive predictions; ME prevents the
aggregate predictions from being captured by only a few categories.

For \(\mathbf u=[1/C,\ldots,1/C]\), the identity

\[
-\mathcal H_{\mathrm{ME}}^t
=
D_{\mathrm{KL}}(\overline{\mathbf p}_t\|\mathbf u)-\log C
\]

may support the decision-alignment interpretation. Treat \(\mathbf u\) only as a
soft non-concentration reference, never as the true transmitter activity profile.
Do not present CE, ME, or information maximization as standalone novelties.

Build the methodology paragraphs from the two current-interval failures:
ambiguous individual assignments and aggregate concentration on a narrow subset
of registered emitters. Explain why confidence refinement alone can reinforce a
dominant category, then present STDA as one dual-level decision design that
coordinates per-signal decisiveness with aggregate non-concentration. Package its
verified properties through current-set-only information, a fixed CE--ME
combination, no auxiliary trainable network, no extra term-balancing coefficient,
and compatibility with the permitted BN-only update.

Distribute the STDA equations through the methodology narrative instead of
stacking CE, the aggregate probability, ME, and the final objective in one
`aligned` block. Use the semantic order `probability-vector definition -> CE
objective -> CE interpretation -> aggregate probability -> ME objective -> ME
interpretation -> joint STDA objective`. Each displayed equation must perform one
clear explanatory role, and the prose must interpret that role before introducing
the next mathematical object. A short multi-line block is acceptable only when
its lines define one mathematically inseparable object; visual compactness alone
is not a reason to combine distinct objectives.

Keep `eq:stda_objective` on the final joint objective when preserving manuscript
references. Define only indispensable symbols, explain the interaction between
CE and ME once, and retain the boundary that uniformity is a soft
non-concentration interpretation rather than a true emitter activity prior. Omit
the optional KL identity unless it establishes a theoretical interpretation
needed by the local argument; when omitted, preserve its valid interpretive
boundary in prose. Write the final subsection as connected paragraphs without
outline labels such as `Design motivation`, `Dual-level decision organization`,
or `Mathematical formulation`.

## 4. Long-Term Distribution Alignment

**Keep the LTDA subsection under exclusive LTDA ownership.** Do not mention
STDA or another component as an opening, transition, comparison, complement, or
closing sentence. Put all framework-level interaction in Overall Method or Joint
Objective.

**Do not use `To realize this design` or another repeated formula-announcement
template.** Introduce the historical reference or current-to-history relation
directly after the methodology argument.

**Do not define LTDA as `JS plus EMA` or turn the subsection into a divergence
and moving-average tutorial.** The methodology must establish the missing-
reference problem, compact temporal design, active historical participation, and
deployment properties independently of the formulas.

**Do not introduce another historical state, replayed raw signals, a standard JS
expansion, or a recursive EMA derivation in the main LTDA subsection.** Retain
only the equations and update-order facts needed to reproduce the active module.

**Audit LTDA twice.** During planning, verify that every sentence belongs to the
long-term reference mechanism and that the design argument is complete without
operator names. After drafting, recheck single-module ownership, remove stock
transitions, and confirm the discrepancy, gradient path, and reference-update
order against the current method.

### 4.1 Historical reference

Use only \(\mathbf q_t\in\mathbb R^C\) as the compact long-term prediction-
distribution reference. Do not introduce \(\mathbf r_t\), class-confidence EMA,
CB, a complete identification state, or storage of historical raw signals.

### 4.2 Explicit alignment

Lock the current LTDA objective as

\[
\boxed{
\mathcal L_{\mathrm{LTDA}}^t
=
D_{\mathrm{JS}}
\!\left(
\overline{\mathbf p}_t
\middle\|
\operatorname{sg}(\mathbf q_{t-1})
\right)
}.
\]

Define \(D_{\mathrm{JS}}\) once when exact reproducibility requires it. Explain that
the Jensen--Shannon divergence is symmetric and bounded, but do not present this
standard property as a new theorem. A divergence choice is a structural design
choice, not a new hyperparameter.

### 4.3 Temporal update

After constructing the current loss, update the detached reference as

\[
\boxed{
\mathbf q_t
=
\mu\mathbf q_{t-1}
+
(1-\mu)\operatorname{sg}(\overline{\mathbf p}_t)
},
\qquad
\mu=\texttt{ema\_momentum}.
\]

The initialization of \(\mathbf q_0\) must match code and be stated explicitly.
Do not silently assume a uniform, source-prior, or first-interval initialization.

EMA accumulation alone is not alignment. The active alignment is the explicit JS
discrepancy between differentiable \(\overline{\mathbf p}_t\) and detached
\(\mathbf q_{t-1}\). Compute the discrepancy against the previous reference before
writing the current distribution into \(\mathbf q_t\).

The expansion

\[
\mathbf q_t
=
\mu^t\mathbf q_0
+
(1-\mu)\sum_{\tau=1}^{t}
\mu^{t-\tau}\operatorname{sg}(\overline{\mathbf p}_{\tau})
\]

may explain the compact temporal memory. State the \(O(C)\) state cost and zero
additional trainable parameters only in the experimental complexity analysis,
never in Proposed Method.

Build the methodology paragraphs from the absence of a temporal reference in a
current-set-only online update. Explain why retained parameter adjustments make
preceding identification behavior relevant, then present the detached
class-level statistic as an active reference for coordinating
successive updates. Package LTDA through its explicit current-to-history
comparison, compact historical reference, no historical raw-signal replay, no
auxiliary trainable network, and compatibility with the single-pass online protocol.
Treat these as design properties or intended capabilities unless controlled
evidence establishes their empirical effect.

Use the mathematical construction only for the JS discrepancy and the subsequent
EMA reference update. Introduce \(\mathbf q_{t-1}\) directly, then present and
interpret the discrepancy before presenting the reference-update equation. Keep
these equations in separate narrative positions because one defines the active
alignment objective and the other defines the temporal state transition. State
the verified initialization, keep gradients through the current aggregate
distribution, and detach the retained reference. The discrepancy must be
constructed before the current distribution enters \(\mathbf q_t\). Explain the
gradient and update order once at the point where each fact becomes necessary.
Write the final subsection as connected paragraphs without outline labels,
resource calculations, efficiency metrics, or a standard divergence expansion.

## 5. Joint objective and online transition

Use the total loss

\[
\boxed{
\mathcal L_{\mathrm{SLPA\text{-}SEI}}^t
=
\mathcal L_{\mathrm{STDA}}^t
+
\lambda_{\mathrm{mec}}\mathcal L_{\mathrm{LTDA}}^t
}.
\]

Do not multiply the entire objective by `lambda_mec`; that would largely duplicate
learning-rate scaling. Define its current role as the relative LTDA weight while
retaining the existing parameter name.

Partition parameters as
\(\theta=(\theta^{\mathrm{BN}},\theta^{\mathrm{fix}})\). When code matches, use

\[
\theta_t^{\mathrm{BN}}
=
\theta_{t-1}^{\mathrm{BN}}
-
\eta\nabla_{\theta^{\mathrm{BN}}}
\mathcal L_{\mathrm{SLPA\text{-}SEI}}^t,
\qquad
\theta_t^{\mathrm{fix}}=\theta_0^{\mathrm{fix}}.
\]

Keep BN affine parameters, BN running statistics, and \(\mathbf q_t\) conceptually
distinct. Use the verified evaluation order. A typical prequential transition is:

1. receive current unlabeled signals with \(\theta_{t-1}\) and \(\mathbf q_{t-1}\);
2. record current predictions;
3. compute STDA and LTDA with gradients through current predictions;
4. update allowed BN parameters once;
5. detach and store \(\mathbf q_t\);
6. pass \((\theta_t,\mathbf q_t)\) to the next step.

## 6. Algorithm completeness and novelty boundary

Treat the algorithm as structurally complete when all of the following hold:

- STDA has a defined input, objective, and BN gradient path;
- LTDA compares current and previous explicit distributions;
- only the historical reference is detached;
- reference initialization and update order are defined;
- the joint objective uses the same adaptable BN parameters;
- no removed module remains active in code, equations, pseudocode, or figures.

Do not add modules merely to create apparent depth. The contribution should center
on the dual-timescale organization, compact temporal reference, and lightweight
source-free online implementation. Because CE--ME and EMA/JS are established
primitives, never claim these primitives themselves as inventions. The scientific
risk is whether LTDA adds a distinct and stable effect beyond STDA; treat that as
an evidence question, not a reason to embellish the algorithm in prose.

Do not confuse claim restraint with under-selling the method. After explaining
each module's mechanism, state its functional consequence and the information
required by its operations. Package STDA through its coordinated per-signal
decisiveness and aggregate non-concentration, fixed CE--ME combination,
current-set-only information path, and lack of an auxiliary trainable network.
Package LTDA through its explicit current-to-history discrepancy, detached
historical reference, and absence of historical raw-signal replay or an auxiliary
trainable network. Present their joint value as dual-timescale
coordination under one BN-only online update. Keep parameter counts, FLOPs,
runtime, storage complexity, state cost, and other efficiency metrics exclusively
in Experiments. Treat method statements as design properties or intended
capabilities unless controlled results establish an empirical effect. Do not turn
them into guarantees of correction, stability, robustness, invariance,
generality, or superiority.

## 7. Figure logic

Use a two-module overview. The figures must have visibly different centers:

- **STDA figure:** current observation interval, individual predictions, CE-driven
  decisiveness, ME-driven non-concentration, and current decision structure;
- **LTDA figure:** timeline, \(\overline{\mathbf p}_t\), \(\mathbf q_{t-1}\), JS
  discrepancy, stop-gradient, and EMA reference update.

Do not redraw the full backbone as the main content of both figures. Use concrete
variables and deterministic operators instead of abstract model-shaped icons.
Keep figures compact, English-only, and consistent with IEEE schematics.

Open the Proposed Method with a compact `Overall Method` subsection when the
framework figure is introduced. Its overview paragraph should identify the
figure as the complete SLPA-SEI framework, state that the framework contains
exactly STDA and LTDA, give one task-level role for each module, and explain that
the two modules coordinate current-signal identification with consistency across
successive signal sets. Keep this roadmap at four to six sentences. Leave
probability definitions, entropy terms, JS divergence, EMA, gradient paths,
BN-update scope, and the detailed online order to the component and joint-update
subsections. Do not reduce the overview to a two-sentence module inventory, and
do not expand it into a step-by-step algorithm description.

## 8. Claim and evidence protocol

Use these statuses:

- **Observed:** visible in verified code, logs, or raw results;
- **Validated:** supported by a controlled experiment;
- **Interpretation:** plausible but not isolated;
- **Hypothesis:** requires a new test;
- **Decision:** a chosen method or writing design.

Never turn a design intention into an empirical finding. Keep uniform-
hyperparameter, target-tuned, backbone-specific, and dataset-specific results
separate. Existing results from removed modules or an inactive LTDA gradient path
are legacy evidence and must not be attributed to the final STDA--LTDA method.

For the current experimental organization and deferred analyses, follow
`references/experiment-evidence-2026-08.md`. In particular, treat temporal
trajectory analysis as a research TODO until its stream order, visualization
protocol, and claim boundary are verified. Do not present that planned analysis
as completed evidence or force it into the current paper outline.

### Experimental-settings boundary

Treat `Experimental Settings` strictly as a reproducibility description, not as
an overview of the experiment section. Include only the information needed to
reconstruct the common setup:

- dataset names, citations, acquisition characteristics, selected subsets,
  emitter counts, sample counts, signal format, domains or distances, and the
  corresponding train/test partition rules;
- the default backbone, trainable and frozen parameter scope, optimizer, source-
  training settings, online-adaptation settings, software versions, and hardware;
- the values and design of the retained hyperparameters, including
  `lambda_mec` and `ema_momentum`, when verified.

Allow numerical dataset statistics and implementation settings because they are
reproducibility metadata. Exclude all empirical outcomes, including accuracy,
runtime measurements, improvements, rankings, result comparisons, and claims
about what an experiment demonstrates. Do not enumerate the main experiment,
ablation, backbone study, or sensitivity analysis; explain their purposes; refer
forward to result tables; define evaluation metrics; or insert averaging formulas
in this subsection. Keep experiment organization and proof targets in later
result subsections. Never turn an unverified legacy value into a current setting;
retain an explicit placeholder until the current configuration is confirmed.

Use only established academic terms for experimental settings, protocols, and
problem definitions. Verify terminology against primary literature before using
it as a formal label. Do not coin a protocol name, acronym, or quasi-standard
term for a project-specific data split. When no established term exactly names
the split, use the closest established setting and describe the source--target
mapping operationally without assigning a new label.

For WiSig, use the established `single-source test-time adaptation` setting rather
than `leave-one-domain-out`: each acquisition date is selected in turn as the
labeled source domain, and each remaining date defines an independent unlabeled
target-domain transfer task. Describe the resulting 12 ordered source--target
tasks explicitly. Justify only choices that protect validity, such as source-only
model selection and state reinitialization that prevents cross-target carryover.

### Main identification-performance introduction

Open the main accuracy-and-runtime subsection by emphasizing the deployment
setting, not by repeating dataset partitions or narrating table columns. Use this
order:

1. state the verified common backbone, currently SCNN, and the relevant adaptable
   parameter scope;
2. define single-step online TTA operationally: process the target stream once,
   permit at most one update for each incoming target batch, and do not revisit
   batches for iterative optimization;
3. explain why this constraint matters for practical SEI: continuously arriving
   signals require timely decisions under limited latency and computation, so the
   experiment tests whether one unlabeled adaptation step supplies a useful
   correction;
4. introduce accuracy and efficiency as coordinated but visually distinct evidence,
   define the timing boundary, and use Direct Testing as the no-adaptation inference
   reference when included;
5. summarize the two dataset-specific accuracy tables, the compact complexity
   table, and the two-panel runtime figure in one short paragraph only.

Do not spend separate paragraphs before the tables re-explaining the 12 WiSig
tasks, ORACLE train/test partitions, state-reset rules, source split ratios,
sample counts, or detailed averaging mechanics already given in `Experimental
Settings`. Mention an average only briefly when needed to interpret the table.
Keep result interpretation and method comparisons after the tables.

### Post-main-results evidence order

When organizing only the material after the main accuracy-and-runtime comparison,
use this order:

1. place a compact complexity table and two-panel runtime figure immediately after
   the main accuracy result; report total parameters, online-updated parameters,
   GFLOPs per adaptation step, zero auxiliary trainable parameters, and \(O(C)\)
   historical-reference storage only when verified, and do not count this
   supporting efficiency analysis as another formal experiment;
2. report the WiSig ablation with exactly Direct Testing (source only), STDA only,
   LTDA only, and full SLPA-SEI under identical optimization and reset rules;
3. report a fixed-protocol multi-backbone comparison using the verified active
   backbone list, with Direct Testing, one common TTA baseline, STDA, and SLPA-SEI
   when these rows have all been regenerated consistently;
4. report the final active implementation's compact
   \(\lambda_{\mathrm{mec}}\)-by-
   \(\mu=\texttt{ema_momentum}\) sensitivity grid with all other settings fixed.

For each WiSig source-date column in the ablation, average the three independently
evaluated target dates. If an overall column is shown, use the unweighted average
of the four source-date results. Never reuse legacy ablation labels such as
`w/o CADF`, `w/o MEC`, `w/o Gate`, or `RFF-DEM` for the final STDA--LTDA method.

Do not lock a backbone name merely because it appeared in a draft paragraph.
Verify the active backbone set and regenerated result table first. Keep one
hyperparameter protocol across backbones unless a separately disclosed tuned
comparison is the intended experiment, and never mix uniform and tuned rows.

Treat a repeated numeric token such as `20.00`, when explicitly requested by the
user, as layout scaffolding only. It is not observed evidence, cannot establish a
ranking or module contribution, and must be replaced before any result-dependent
claim is finalized.

## 9. Preferred terminology

Use communication-domain wording in the Abstract, Introduction, Related Work,
contribution statements, figure narratives, and story discussions. Read
`references/communication-facing-language.md` before drafting or auditing any of
these parts. In the Abstract and Introduction, stop at the framework-and-module
level. Reserve solution-specific, model-internal vocabulary for the Proposed
Method, equations, pseudocode, and implementation details where it is needed for
scientific precision. Use Problem Formulation to define the signal stream,
available information, temporal setting, and research objective without revealing
the solution operators prematurely.

Prefer:

- `time-varying wireless conditions`;
- `short-term observation interval`;
- `current emitter decisions` or `current identification behavior` in high-level
  prose;
- `historical identification statistics` in high-level prose;
- `a locally biased update affecting later batches` in high-level prose;
- `dual-timescale predictive alignment`;
- `BN-only single-step online adaptation`.

Keep `current prediction structure`, `historical prediction-distribution
reference`, and `prediction-distribution drift` only in the Proposed Method or a
technical analysis where their model-level meaning is defined explicitly. Do not
use `prediction`, `distribution shift`, `model state`, `decision boundary`,
`entropy`, or similar machine-learning shorthand when a direct statement about
received signals, registered emitters, identification results, or retained online
updates is equally accurate.

Avoid as active method language:

- `environment adaptation` or `environment alignment`;
- `semantic`, `feature`, `channel`, or `source--target domain alignment`;
- `identification state` for \(\mathbf q_t\);
- `channel-invariant`, `pure fingerprint`, `channel removal`;
- `PGCI`, `CO-SigDEM`, `Hi-MEC`, `EMA-MEC`, `DA/CB hierarchy`;
- `guarantees`, `eliminates`, `significant`, `robust`, `stable`, or
  `state-of-the-art` without matching evidence.

## 10. Contribution spine

Use the following framework-first four-part contribution structure for the
current SLPA-SEI paper:

1. propose SLPA-SEI as an online TTA framework based on dual-timescale alignment
   for SEI under time-varying wireless conditions, and state its overall
   innovation as coordinating current-signal identification with identification
   consistency across successive signal sets;
2. present STDA as a separately designed module and state its verified role in
   improving the identification of currently received signals;
3. present LTDA as a separately designed module and state its verified role in
   using accumulated historical identification information to maintain
   consistency over time;
4. report the controlled evaluation of the complete framework and its modules,
   with datasets, comparison scope, and any numerical advantage bounded by the
   verified experiment record.

Place the overall framework before the module-level contributions and place
experimental validation last. Do not add a separate problem-formulation bullet
when the framework item already states the organizing research insight. Keep the
framework and module items distinct without presenting their standard internal
operators as independent innovations.

Write the list as four contribution claims rather than a table of contents. Each
item must contain a clear authorship action, the distinctive problem or
information considered by the design, and the resulting SEI capability. Do not
end an item after saying that a module is a short- or long-timescale component.
Use the following internal structure:

1. **Overall framework:** open with `we propose SLPA-SEI`; name online TTA under
   time-varying wireless conditions and dual-timescale alignment; then state the
   overall innovation as jointly considering current-signal identification and
   the influence of retained adjustments on later signal sets. Close with the
   resulting coordination between immediate adaptation and identification
   consistency over time.
2. **STDA:** open with `we design STDA`; name the current incoming signal set as
   its focus; then state that the design strengthens identification under the
   current reception condition within one online adjustment. Do not use the weak
   standalone description `STDA is the short-timescale component` as the claimed
   contribution.
3. **LTDA:** open with `we design LTDA`; state that it uses compact identification
   information accumulated from preceding signal sets; then state that this
   provides a long-term reference for coordinating successive online adjustments
   without replaying historical raw signals. Keep EMA and divergence details in
   Proposed Method.
4. **Experiments:** name WiSig, ORACLE, and the consistent single-step online
   protocol; report the strongest verified accuracy comparison as the main
   empirical outcome; then use ablation, processing requirements, backbone, and
   parameter studies as supporting evidence for the claimed framework and module
   effects. Use `percentage points` for an absolute accuracy difference. Use
   `percent` only for a relative change. Do not use `significant` without a
   statistical significance test.

Prefer `propose`, `design`, `develop`, `establish`, `coordinate`, `improve`, and
`maintain` when they match the verified contribution. Avoid allowing `consists
of`, `is a component of`, `covers`, `we evaluate`, or `we conduct experiments`
to carry an item by themselves. These constructions describe paper contents but
do not explain the innovation or its consequence. Strengthen the list with exact
research functions and verified outcomes rather than unsupported adjectives.

Do not list CE, ME, JS divergence, EMA, or BN-only updating as five independent
innovations.

## 11. Required response pattern

When asked to build or audit the story, return only the sections needed for the
request, using this order when a full audit is useful:

1. current locked algorithm;
2. causal story spine;
3. STDA and LTDA roles;
4. unresolved code--equation conflicts;
5. claim boundaries;
6. evidence needed for unsupported claims.

Lead with the conclusion. Distinguish required algorithm corrections from writing
improvements. Do not recommend new modules or hyperparameters unless verified
evidence shows that the locked algorithm is inadequate and the user asks for an
algorithm redesign.

## 12. Final self-check

Before returning any SLPA-SEI story decision, verify:

- SLPA-SEI contains only STDA and LTDA;
- STDA is exactly CE minus ME with no new coefficient;
- LTDA is current-to-history JS alignment with a differentiable current path;
- \(\mathbf q_t\) is the only historical prediction reference;
- `lambda_mec` and `ema_momentum` are the only method-specific parameters;
- removed augmentation, projection, CB, confidence, and gating mechanisms are absent;
- alignment claims name an explicit decision or distribution reference;
- the online prediction, parameter update, and reference update order is closed;
- code, equations, pseudocode, figures, and prose describe one algorithm version.
- Abstract-, Introduction-, and story-level prose is understandable to a
  communications reviewer without relying on unexplained machine-learning
  shorthand;
- the Abstract and Introduction name only SLPA-SEI, STDA, LTDA, and their
  communication-level roles, without exposing CE, ME, entropy, JS divergence,
  EMA, gradients, decision boundaries, or reference-update mechanics;
- probability, distribution, divergence, and update-reference terms remain exact
  in the Proposed Method wherever they are required to define or reproduce the
  algorithm;
- every paragraph and equation belongs to exactly one locked subsection, with no
  duplicated content or functionless bridge paragraph between adjacent
  subsections;
- the Problem Description contains only the time-varying SEI setting, causes,
  short- and long-timescale difficulties, and resulting identification problem;
  it does not preview SLPA-SEI, STDA, LTDA, historical-information use, or another
  solution operation;
- the Problem Formulation establishes only the method-independent variables,
  constraints, and optimization objective needed to provide the mathematical
  basis and necessity of the task; it does not explain the proposed method;
- the Problem Description does not redefine the signal model or online processing
  sequence owned by System Model;
- the Problem Formulation uses an implicit identifier mapping and does not expose
  activation functions, layer operations, or the STDA and LTDA solution
  operators;
- every cited paper reuses its project citation-registry key and occurs only once
  in the manuscript bibliography;
- deferred temporal analysis is not represented as completed evidence or a locked
  experimental claim.
