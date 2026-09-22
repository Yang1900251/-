# Communication-Facing Language for SLPA-SEI

Use this reference when writing or auditing the SLPA-SEI story, Abstract,
Introduction, Related Work, contribution statements, figure narratives, or other
high-level prose for a communications or signal-processing audience.

## Core rule

Describe the received-signal condition, identification consequence, and temporal
carry-over without naming model-internal quantities in high-level sections.
Prefer established SEI and communications nouns: received signals, registered
emitters, acquisition periods, wireless reception conditions, identification
results, identification accuracy, retained online updates, and information
accumulated from earlier received signals.

Reserve `observation interval` for the system model, problem formulation, or a
sentence whose temporal boundary must be explicit. Do not repeatedly use
`observe`, `observed`, `observation`, or their derivatives in the Abstract.
Prefer `currently received signals`, `later signals`, `successive signal
arrivals`, and `over time` when they preserve the intended meaning.

Keep `predicate`, `prediction`, `predictive`, `entropy`, probability-level
descriptions, and similar computer-science or model-internal vocabulary out of
the Abstract, Introduction, contribution statements, and framework overview when
a concrete communications expression is available. Prefer `received signal`,
`emitter decision`, `identification result`, `acquisition condition`, `online
adjustment`, and `historical identification information`. Preserve `Predictive`
only in the official name **Short- and Long-Term Predictive Alignment for
Specific Emitter Identification**; preserve other official component names when
they must be expanded. Define entropy, probability, divergence, and loss terms
only in Problem Formulation or Proposed Method when required for mathematical
precision.

Before selecting wording for the Abstract, Introduction, or framework overview,
use `write-research-paper` to consult the reviewed communications and SEI entries
in its reference-paper corpus and the source-backed patterns in its academic
phrase bank. Borrow only conventional rhetorical functions and collocations.
Keep the SLPA-SEI facts and terminology fixed by this story skill.

Avoid colons and em dashes when presenting the SLPA-SEI problem, framework, or
module roles in ordinary prose. Write the framework definition and the STDA and
LTDA roles as complete sentences. Use a colon only when a contribution list,
formal definition, or necessary enumeration requires it. Preserve hyphens inside
established terms and names such as `source-free`, `time-varying`, and
`SLPA-SEI`.

Expand every English acronym once at its first manuscript occurrence using the
form `full English term (ACRONYM)`, and use only the acronym thereafter. Apply
this rule consistently to `specific emitter identification (SEI)`, `domain
adaptation (DA)`, `domain generalization (DG)`, `test-time adaptation (TTA)`, the
full SLPA-SEI method name, `Short-Term Decision Alignment (STDA)`, and `Long-Term
Distribution Alignment (LTDA)`. Do not repeat a full expansion in later sections.

Do not force this wording into the Proposed Method when it would hide the actual
operation. Keep prediction probabilities, batch-average distributions, entropy,
JS divergence, EMA, stop-gradient, and BN parameters when defining the algorithm
mathematically there.

Use `source-free` precisely and sparingly. It denotes only the absence of source
training signals during adaptation. It does not cause sequential signal arrival,
one-step updating, or cross-interval influence. In high-level prose, state the
underlying condition directly when clearer, such as `without access to source
training signals during adaptation`. Do not repeatedly attach `source-free` to
SEI, online operation, the proposed framework, and every contribution once the
access condition has been established.

## Section routing

- **Story, Abstract, and Introduction:** stay at the framework-and-module level.
  Explain received-signal changes, current identification, cross-batch effects,
  and one communication-level role for STDA and LTDA. Do not name their losses,
  divergences, moving-average update, gradients, decision boundaries, or internal
  probability references.
- **Related Work:** describe what earlier SEI methods handle in terms of
  acquisition times, channels, frequencies, receivers, and reception conditions;
  then state the unresolved online carry-over effect.
- **Problem Formulation:** define the received-signal stream, available data,
  online order, retained updates, and short- and long-term research requirements.
  Do not introduce solution-specific operators.
- **Proposed Method:** first give the framework and module roles, then introduce
  probability-, entropy-, divergence-, and reference-update details inside the
  corresponding component subsections.
- **Experiments:** report identification accuracy, acquisition conditions,
  adaptation order, and temporal performance before interpreting model-internal
  statistics.

## Overall Method subsection

Use the opening of Proposed Method as a framework roadmap rather than a compressed
algorithm. Build one paragraph in this order:

1. identify the cited figure as the overall SLPA-SEI framework;
2. state that the framework contains the two complementary modules STDA and LTDA;
3. give the verified current-signal identification role of STDA;
4. give the verified historical-information and cross-step consistency role of
   LTDA;
5. state that their combination coordinates the short and long adaptation
   timescales;
6. optionally indicate that the following subsections provide the detailed
   formulations.

Target four to six sentences with moderate detail. Use SLPA-SEI, STDA, and LTDA
as the grammatical subjects, and prefer direct verbs such as `consists of`,
`improves`, `uses`, `maintains`, and `coordinates`. Do not place the signal-by-
signal pipeline, loss equations, probability notation, reference-update formula,
gradient behavior, or complete deployment-constraint list in this paragraph.
Those details belong to the component and joint-update subsections. A two-
sentence statement that only names the modules is too thin to orient the reader.

## Preferred replacements in high-level prose

Use these as meaning-preserving rewrites, not as automatic word substitutions:

- `prediction` -> `emitter decision`, `identification result`, or `identification
  behavior`;
- `uncertain predictions` -> `ambiguous or low-confidence emitter decisions`;
- `class concentration` -> `many received signals being assigned to only a few
  registered emitters`;
- `prediction-distribution deviation/drift` -> `successive batches producing
  increasingly biased emitter decisions` or `a locally biased update affecting
  later batches`;
- `historical prediction-distribution reference` -> `compact historical
  identification statistics`;
- `current-to-history distribution alignment` -> `maintaining consistency
  between current and accumulated historical identification statistics`;
- `model state` -> `retained online identifier` or `retained online parameters`;
- `cross-step error propagation` -> `an error introduced by one incoming batch
  affecting the identification of later batches`;
- `domain shift` -> `changes between acquisition periods or wireless reception
  conditions`;
- `source--target mismatch` -> `the difference between source-condition and
  current-condition received signals`.

## Abstract and Introduction module template

Define SLPA-SEI with a basic statement of its framework type and unifying
function. Use `an online test-time adaptation framework based on dual-timescale
alignment for SEI under time-varying wireless conditions`. State separately that
the adaptation does not access source training signals when this access
constraint is needed for the argument. Follow with one short role clause for STDA
and one for LTDA. Do not place the detailed alignment target, historical
reference construction, update order, or optimization mechanism in the method-
definition sentence.

Use this abstraction level for SLPA-SEI:

1. time-varying wireless reception conditions alter the received signals and
   weaken emitter identification;
2. existing time-varying SEI methods mainly reduce differences across acquisition
   conditions, while retained online updates create an additional cross-period
   effect;
3. SLPA-SEI addresses this issue through STDA and LTDA;
4. STDA improves identification for currently received signals;
5. LTDA uses information accumulated from earlier received signals to maintain
   identification consistency over time;
6. the two modules jointly support source-free online SEI under time-varying
   reception conditions.

Stop at this level. Do not explain CE, ME, entropy, JS divergence, EMA,
stop-gradient, BN-only updating, probability-distribution references, or decision
boundaries in the Abstract or Introduction. Those terms belong to the Proposed
Method and its technical analysis.

## Contribution-language strength

Make the SLPA-SEI contribution explicit through concrete authorship and function:

- use `we propose SLPA-SEI` for the complete framework;
- use `we design two complementary modules` for STDA and LTDA;
- state that STDA `improves` or `refines` current emitter identification;
- state that LTDA `uses accumulated historical identification information to
  maintain identification consistency over time`.

Do not use `introduce`, `regulate`, `regularize`, `regularization term`, or
`auxiliary constraint` as the main wording that carries an SLPA-SEI innovation in
the Abstract, Introduction, contribution list, or Conclusion. These terms make
the contribution sound like a minor optimization attachment and obscure the
dual-timescale framework. Retain an exact mathematical term in the Proposed
Method only when it is required to define the implemented operation.

Strengthen the contribution through the verified research setting, the
dual-timescale organization, and the distinct role of each designed module. Do
not compensate with unsupported `novel`, `first`, `significant`, `robust`, or
`state-of-the-art` claims.

For the current paper, order the contribution list as overall SLPA-SEI framework,
STDA module, LTDA module, and experimental validation. The first item must state
the framework's organizing innovation. Give each module its own item because the
two modules answer different adaptation timescales. Keep the validation item
last, and include numerical superiority only after it has been verified against
the final experiment record.

Make every contribution item answer both `what did we design or consider?` and
`what SEI capability does this realize?`. Avoid list-like descriptions such as
`STDA is the short-timescale component`, `LTDA is the long-timescale component`,
or `the experiments cover ...` unless the same item also states the distinctive
function and verified consequence. The framework item should emphasize the new
coordination of current and successive signal sets. The STDA item should
emphasize current-condition identification. The LTDA item should emphasize the
use of accumulated historical identification information for consistency over
time. The experiment item should lead with the verified comparative result and
use the remaining studies as evidence rather than as an inventory.

Use two sentences per item when needed. The first sentence should claim the
framework, module, or evaluation through `we propose`, `we design`, `we develop`,
or `we demonstrate`. The second should state the resulting identification
capability or verified outcome through concrete communications language. Do not
inflate the list with `novel`, `innovatively`, `unequivocally`, `superior`, or
`state-of-the-art` when the same strength can be conveyed by the exact design
distinction or a numerical comparison.

## Mechanism-evidence boundary

Do not add a mechanism explanation to the Abstract, Introduction, framework
overview, contribution list, or Conclusion merely to make the method sound
deeper or to increase length. Include a mechanism only when it is supported by
the verified implementation and equations, a controlled experiment, an
established physical model, or a directly relevant precedent in the reviewed SEI
or communications literature. Distinguish a verified design operation from an
empirical effect and a plausible interpretation.

For SLPA-SEI high-level prose, use only the verified role statements:

- STDA improves emitter identification for currently received signals;
- LTDA uses accumulated historical identification information to maintain
  identification consistency over time.

Keep current-decision ambiguity, identification-result concentration, entropy
effects, historical-bias suppression, and error carry-over explanations in
Proposed Method or a verified technical analysis. Do not state that STDA
increases inter-emitter separability or that LTDA corrects accumulated errors,
prevents error propagation, or guarantees long-term stability without matching
evidence. When the evidence establishes only the intended function, state the
module role without an added causal explanation.

## Literature-grounded comparison boundary

### TTA route in Related Work

Build the TTA subsection from operational value to the SLPA-SEI boundary.

1. State that TTA uses incoming unlabeled signals to adjust a source-trained
   identifier during testing. This allows the identifier to respond to the
   reception condition currently encountered without repeated offline training.
2. Explain the processing advantage only at the level supported by each method.
   Parameter-restricted, sample-selective, single-step, or nonparametric designs
   may limit online processing requirements and support time-sensitive SEI. Do
   not describe TTA as universally real-time or low-cost.
3. Give the principal characteristic of each representative general method.
   Tent establishes direct online adjustment through normalization-parameter
   updating. EATA reduces unnecessary or unreliable updates and preserves
   important source-model parameters. SAR addresses unstable updating under
   mixed changes, limited test data, and imbalanced class arrivals. Acknowledge
   that these methods were developed primarily for visual recognition.
4. State that TTA remains less studied in SEI, then acknowledge recent
   field-specific work. RFF-TTA uses physical-impairment augmentation and
   prototype guidance for temporally varying radio fingerprints without model
   retraining. ANR updates BN parameters for radio-frequency recognition under
   dynamic noise conditions. Do not reduce these studies to generic entropy-
   driven methods.
5. Close with the exact remaining boundary. Existing field-specific work
   improves identification under a current temporal or noise condition, whereas
   SLPA-SEI studies parameter-updating continuous SEI in which an adjustment is
   retained for later signal sets. State the SLPA-SEI distinction as coordinating
   current-signal identification with identification consistency across
   successive signal sets through two connected adaptation timescales.

Use the three general TTA methods as a development sequence rather than a list of
equivalent baselines. Give each one a distinct setting, response, and verified
capability. Keep their model-internal terms only where necessary to characterize
the cited method accurately.

### Deployment-necessity chain

Establish the need for SLPA-SEI through verified information and deployment
constraints rather than a vague claim that prior methods are weak:

1. DA methods use target-condition signals to adapt a source-trained identifier;
   conventional implementations also retain access to source signals, and
   semi-supervised variants require some target labels. Do not claim that every
   DA method requires target labels because unsupervised DA does not.
2. DG methods avoid target-data access during training by learning from available
   source conditions or source-side condition expansion. Their effectiveness
   depends on what reception variability is represented during source training,
   and the deployed identifier does not use incoming unlabeled signals for online
   adjustment.
3. In continuous wireless monitoring, the source signal archive may be
   unavailable on the deployed receiver, newly received signals generally lack
   immediate emitter labels, and reception conditions can continue to change
   after deployment.
4. These simultaneous constraints motivate source-free, unlabeled, online
   adaptation that can use each incoming signal set without revisiting source
   signals or requiring target annotation.
5. Because the resulting online adjustments are retained, the method must
   coordinate current-signal identification with consistency over time. This
   requirement motivates the dual-timescale organization of SLPA-SEI.

Do not claim that SLPA-SEI removes the need for a source-trained identifier. The
method starts from a source-trained SEI model; its source-free property means
that source signals are unavailable during online adaptation. Do not use
`depends on a powerful source model` as the main contrast, because that
dependence is shared by SLPA-SEI. Build the necessity from data access, label
availability, online order, and persistent updates.

For the Abstract, compress the chain to: existing DA and DG capabilities ->
their distinct data-access or deployment boundary -> source-free and unlabeled
continuous reception -> need for dual-timescale online adaptation. Keep the
category distinctions explicit even when the wording is compressed.

Do not use `deployment gap`, `real-time deployment`, `real-time capability`, or
`low computational overhead` in high-level prose unless the paper reports a
matching hardware platform, timing boundary, latency requirement, and controlled
measurement. These phrases can make readers expect an actual field deployment or
a verified deadline guarantee. When that evidence is unavailable, describe the
setting as `time-sensitive continuous SEI` or `continuous online SEI` and support
its practicality with verified design facts: one online update for each incoming
signal set, no source-signal access during adaptation, no historical raw-signal
replay, BN-only updating, and no auxiliary trainable network when confirmed by
the final implementation.

Do not claim that these design facts prove real-time operation or universally low
cost. State that they limit online processing requirements or support
time-sensitive operation. Reserve `modest processing overhead` or a stronger
efficiency conclusion for verified runtime and complexity evidence under a
reported protocol.

Separate the two directly relevant cross-condition research routes before
stating the SLPA-SEI gap:

- **Cross-condition DA:** treat signals collected under different dates,
  channels, receivers, or other reception conditions as source and target data,
  and use target-condition signals to improve identification under that
  condition. Examples include ADL-ID, LTS-SEI, MSIDA, and VC-SEI.
- **Cross-condition DG:** learn reception-robust identification from available
  source conditions or source-side condition expansion, with the goal of
  maintaining identification under unseen acquisition conditions. Do not say DG
  aligns the source with the current target condition during training when that
  target condition is unavailable.

Do not characterize all DA or DG methods as current-only. ADL-ID evaluates short-
and long-term temporal adaptation; LTS-SEI addresses signals separated by long
time spans; MSIDA uses second- and day-scale signals with iterative adaptation.
These temporal scales describe acquisition gaps, domain scales, or repeated
cross-condition adaptation. Distinguish them from SLPA-SEI's two online
adaptation timescales, which coordinate identification within the current
observation interval and consistency across successive intervals.

Do not use continual or incremental learning as a primary comparison route in
the Abstract, Introduction, contribution statements, or novelty discussion.
SLPA-SEI uses a fixed registered-emitter set and does not introduce new classes,
incremental tasks, task boundaries, replay-based retention, or historical-task
retraining. Its long-term component belongs to persistent online test-time
adaptation rather than continual-learning knowledge retention.

Place the SLPA-SEI distinction at the intersection of its access and update
conditions: the source signals are unavailable, incoming signals are unlabeled,
each observation interval permits one online update, the registered-emitter set
is fixed, and retained updates affect the identifier used for later intervals.
The unresolved issue is therefore the sequential consequence of persistent
source-free online adjustment. A locally biased adjustment made from the current
observation interval may enter the retained identifier and influence later
emitter decisions. SLPA-SEI coordinates current-interval identification with
identification consistency across successive intervals through a compact
historical reference, without replaying historical raw signals.

Use this comparison pattern in story discussions, the Introduction, and Related
Work:

> Existing time-varying SEI methods mainly improve cross-condition
> identification through condition adaptation or reception-robust learning.
> However, under source-free and unlabeled continuous
> online operation, the adjustment made from each observation interval is
> retained and becomes part of the identifier used for subsequent signals. An
> inaccurate current adjustment may therefore continue to affect later emitter
> decisions. SLPA-SEI improves identification within the current observation
> interval while using information accumulated from preceding intervals to
> maintain identification consistency over time.

Keep the following evidence anchors when this comparison requires citations:

- ADL-ID: temporal unsupervised DA evaluated over short- and long-term
  acquisition gaps, arXiv:2301.12360;
- LTS-SEI: long-time-span unsupervised DA, DOI: 10.3390/rs15215214;
- MSIDA: second- and day-scale iterative DA, DOI:
  10.1007/s10489-024-05484-0;
- single-source DG for channel-robust SEI, DOI: 10.1109/TWC.2025.3528568.

## Claim discipline

- Do not equate the method's short and long adaptation timescales with fast and
  slow physical fading.
- Do not narrow the paper to an additive-noise problem unless the system model and
  experiments explicitly isolate noise as the studied cause.
- Do not say every prior time-varying SEI method ignores history. State that most
  prior work emphasizes differences across acquisition conditions, while SLPA-SEI
  additionally addresses how retained online updates influence later observation
  intervals.
- Keep the official names Short-Term Decision Alignment, Long-Term Distribution
  Alignment, and Short- and Long-Term Predictive Alignment unchanged.
