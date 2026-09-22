# SLPA-SEI Evidence Contract (2026-08 transition)

Read this reference before using numerical results, sensitivity claims, stability
claims, backbone comparisons, ablations, or failure cases.

## Contents

1. Evidence statuses and final-method boundary
2. Existing parameter and backbone evidence
3. Required evidence and locked experiment plan
4. Complexity and runtime interpretation
5. Deferred temporal-analysis TODO
6. Wording boundaries

## 1. Evidence statuses

- **Observed:** visible in verified code, logs, or raw tables.
- **Validated:** supported by a controlled comparison under one stated protocol.
- **Interpretation:** plausible explanation not isolated by a comparison.
- **Hypothesis:** requires a new test.
- **Decision:** selected algorithm or writing design.

Do not merge results across different backbones, source--target directions,
learning rates, batch sizes, scoring orders, or tuning protocols.

## 2. Final-method evidence boundary

The final SLPA-SEI algorithm contains only STDA and active-gradient LTDA. Results generated
with PGCI, channel intervention, projection, CO-SigDEM, CB, confidence history, or
an LTDA term disconnected from current predictions are legacy records. They may
document development history but must not support final-method accuracy,
mechanism, sensitivity, or contribution claims.

Treat results explicitly recorded under the former name `DEM-SEI` as legacy
evidence unless they have been regenerated with the final STDA--LTDA
implementation. Never relabel an old `DEM-SEI` result as `SLPA-SEI` solely because
the manuscript method was renamed.

## 3. Existing parameter sweep

Older logs contain a two-dimensional sweep over parameters named \(\lambda\) and
\(\mu\). Because the old implementation did not provide the current LTDA gradient
path, that sweep cannot establish sensitivity of the final STDA--LTDA algorithm.

The final method introduces no new parameter dimension. If sensitivity is reported,
rerun the existing `lambda_mec` by `ema_momentum` analysis with the final active
implementation and state the exact backbone, dataset, stream, range, and fixed
optimization settings.

## 4. Backbone-result boundary

Historical repository records contain inconsistent or incomplete multi-backbone
summaries. Known issues include earlier CNN output-contract mismatch, missing
CVCNN rows in a uniform table, and a newer ResNet raw result not entering an older
summary. Use only regenerated or manually verified final tables for paper claims.
Keep uniform-hyperparameter results separate from backbone- or target-tuned best
results.

## 5. Required final-method evidence

Claims about the two-module method should be tied to evidence such as:

- source-only, STDA-only, LTDA-only, and STDA+LTDA comparisons;
- verification that LTDA produces nonzero gradients through current predictions;
- fixed-protocol multiple-backbone results;
- runtime, updated-parameter count, and \(O(C)\) reference memory;
- repeated runs with a statement of what each seed changes;
- visible failure cases, including historical lag or adverse transfer directions.

## 6. Locked experimental organization

Use WiSig and ORACLE for complementary purposes instead of forcing one domain
protocol onto both datasets.

- **WiSig:** retain the verified cross-date source--target protocol for the main
  accuracy comparison.
- **ORACLE:** treat 2 ft, 8 ft, and the verified far-distance condition as three
  independent distance-specific train/test tasks. Train a separate source model
  on the training partition at each distance and adapt to the corresponding
  held-out test stream. Reinitialize model parameters, optimizer state, and
  \(\mathbf q_0\) between distances. Do not describe this protocol as
  cross-distance adaptation, unseen-distance generalization, or distance
  invariance.
- Report ORACLE accuracy per distance and use an unweighted macro-average across
  the three distance-level accuracies when an overall value is needed.
- Prefer independent capture runs or official train/test partitions within each
  distance. A random split of one capture provides weaker distribution-shift
  evidence and must be described accordingly.

Plan **four formal experiment groups**. Experimental settings, repeated-seed
reporting, implementation gradient checks, and analytic complexity statements are
supporting elements rather than additional experiment groups.

### Experiment 1: Overall identification performance and runtime

- **Protocol:** use one common method list. Report identification accuracy in the
  two dataset-specific main tables. Report analytic complexity in a compact table
  and empirical processing time in a separate two-panel figure within the same
  overall performance-and-efficiency experiment group. For WiSig, use the verified
  cross-date source--target protocol. For ORACLE, use 2 ft, 8 ft, and 64 ft as
  three independent within-distance train/test tasks and verify the far-distance
  metadata before publication. Reinitialize the model, optimizer, and
  \(\mathbf q_0\) between independent target tasks.
- **Artifact organization:** keep the WiSig and ORACLE accuracy tables focused on
  predictive performance. Use the complexity table for total parameters,
  online-updated parameters, and GFLOPs per adaptation step. Use the runtime figure
  for full-stream time under the selected WiSig D1 \(\rightarrow\) D2--D4 setting
  and ORACLE 2-ft setting. Treat these selected settings as representative timing
  cases, not dataset-wide averages, unless additional measurements establish that.
- **Timing rule:** use one fixed backbone, device, batch size, warm-up procedure,
  CUDA synchronization rule, and timing boundary. State whether forward,
  backward, optimizer, data loading, and state-reset costs are included. Repeat the
  measurement and report a mean with dispersion or a median with a stated repeat
  count whenever feasible.
- **Purpose:** jointly assess identification effectiveness and deployment-time
  overhead rather than presenting efficiency as an isolated experiment.
- **Supports:** cross-date effectiveness on WiSig, independent second-dataset
  validation across the tested ORACLE distance-specific tasks, and measured
  runtime under the reported hardware and protocol.
- **Does not support alone:** cross-distance transfer, unseen-distance
  generalization, backbone independence, separate module contributions, or
  hardware-independent speed.
- **Complexity note:** total parameters primarily describe model footprint, while
  online-updated parameters and GFLOPs per step better characterize adaptation
  overhead. Report the updated-parameter ratio and \(O(C)\) historical-reference
  state in the table note or immediately afterward. Do not create a separate
  efficiency experiment solely for these quantities.

#### Provisional working records from the 2026-08 discussion

Treat the following values as a working record that still requires provenance and
measurement verification. The row supplied as `DEM-SEI (ours)` cannot be relabeled
as final `SLPA-SEI` until it is regenerated or verified against the active
STDA--LTDA implementation.

| Method | Total params | Updated params/step | Forward GFLOPs/batch | GFLOPs/step |
|---|---:|---:|---:|---:|
| Direct Testing | 1,055,773 | 0 | 34.55 | 34.55 |
| TENT | 1,055,773 | 1,140 | 34.55 | 103.66 |
| DEM-SEI, provisional | 1,055,773 | 1,140 | 34.55 | 103.66 |
| ETTA | 1,055,773 | 1,140 | 34.55 | 103.66 |
| AugTTA | 2,111,546 | 1,056,913 | 69.11 | 172.77 |
| DeepCORAL | 1,055,773 | 1,140 | 69.11 | 207.33 |
| DANN | 9,327,647 | 1,140 | 75.51 | 213.68 |

The supplied full-setting processing times are:

| Method | WiSig D1 \(\rightarrow\) D2--D4 (s) | ORACLE 2 ft (s) |
|---|---:|---:|
| Direct Testing | 2.15 | 7.41 |
| TENT | 1.78 | 21.10 |
| ETTA | 3.95 | 32.38 |
| AugTTA | 2.78 | 37.14 |
| DANN | 3.97 | 46.01 |
| DeepCORAL | 3.64 | 49.15 |
| DEM-SEI, provisional | 2.04 | 21.40 |

Before publication, resolve the counterintuitive WiSig observation that TENT and
the provisional proposed-method row are faster than Direct Testing. Use identical
timing scopes, warm up the device, synchronize CUDA around the timed region, and
repeat each method. Do not interpret this ordering as evidence that adaptation is
cheaper than inference unless it persists under the controlled protocol.

#### Complexity interpretation rules

- Explain equal total parameters by the shared backbone. A loss function can change
  optimization without adding trainable weights.
- Explain the repeated count of 1,140 online-updated parameters by the common
  BN-only scope when verified.
- Explain equal forward FLOPs by the same backbone, input shape, batch size, and
  number of backbone forwards. Explain equal step FLOPs only when the accounting
  uses the same forward/backward schedule.
- Count every auxiliary model or discriminator resident at test time in total
  parameters. Count every weight changed online in updated parameters. Verify the
  AugTTA and DANN accounting explicitly rather than inferring it from method names.
- Define whether `GFLOPs/step` is profiler output or an estimate. If backward cost
  is approximated as a multiple of forward cost, disclose the rule and apply it
  uniformly.
- Do not infer identical wall-clock time from identical GFLOPs. Loss evaluation,
  augmentation, optimizer work, memory traffic, kernel utilization, and state
  updates can produce different measured runtimes.
- Prefer the compact complexity table over a combined parameter/FLOPs chart.
  Parameters and GFLOPs have incompatible units and scales, so grouped bars or a
  dual-axis bar-line chart can overstate a relationship that is not intrinsic.

#### Runtime-figure rules

- Use two adjacent panels with independent y-axis scales because the WiSig and
  ORACLE measurements cover substantially different ranges and may represent
  different stream sizes.
- Keep method order identical across panels. Use a white background, horizontal
  method labels, and a restrained IEEE-style blue/yellow palette. Identify WiSig
  and ORACLE through panel titles and, if needed, a compact dataset legend.
- State that the vertical axis is total processing time in seconds for the selected
  complete setting. Do not label it per-batch latency, per-sample latency, or
  training time unless that quantity was actually measured.
- Use separate y-axis limits without implying that bar heights are directly
  comparable across datasets. Do not use a broken axis or a shared scale merely to
  force visual symmetry.

### Experiment 2: Component ablation

- **Protocol:** compare Source Only, STDA only, LTDA only, and STDA+LTDA on WiSig
  with the default backbone and identical optimization settings.
- **Purpose:** isolate the contribution of each active module and test whether
  their combination adds value beyond either module alone.
- **Supports:** statements such as `LTDA improves over STDA alone` only when the
  corresponding controlled result supports them.
- **Does not support alone:** the claimed temporal mechanism; additionally verify
  a nonzero LTDA gradient through current predictions as an implementation check.

### Experiment 3: Backbone generalization

- **Protocol:** evaluate Source Only, a common TTA baseline, STDA, and SLPA-SEI on
  the selected backbones using the same WiSig split and evaluation order. Keep
  uniform-hyperparameter results separate from backbone-tuned results.
- **Purpose:** determine whether the observed gain depends on one particular
  feature extractor or classifier architecture.
- **Supports:** architecture-level consistency only across the tested backbones.
- **Does not support:** universal model independence or conclusions based on
  incomplete legacy backbone tables.

### Experiment 4: Parameter sensitivity

- **Protocol:** rerun the final active method on WiSig over a compact grid of
  \(\lambda_{\mathrm{mec}}\) and \(\mu=\texttt{ema_momentum}\), preferably three
  representative values per parameter unless evidence requires a wider range.
- **Purpose:** show how the relative LTDA weight and historical-reference momentum
  affect performance and justify the selected operating point.
- **Supports:** a broad empirical plateau only over the actually tested range.
- **Does not support:** parameter-free behavior or global hyperparameter
  insensitivity. Do not add sensitivity studies for \(\epsilon\), Adam settings,
  or other non-contribution constants merely to increase experiment count.

Use repeated runs and report mean plus dispersion for the principal quantitative
comparisons when feasible. State what each seed changes. This strengthens the four
groups above but is not counted as a fifth experiment. Confusion matrices are
optional diagnostic visualizations rather than a required independent experiment.

Do not require every diagnostic experiment on both datasets. Use ORACLE primarily
as independent second-dataset validation and WiSig for mechanism, backbone, and
sensitivity analyses unless a later verified protocol justifies otherwise.

## 7. Deferred temporal-analysis TODO

**Status: planned research item, not completed evidence.** Temporal trajectory
analysis is currently deferred because an appropriate precedent, stream protocol,
and claim boundary still require literature and implementation review. Do not
place it in the current experimental-results outline as if it were already run,
and do not use it to claim temporal stability, recovery, or historical-lag
behavior.

Before activating this analysis, verify:

1. whether the dataset preserves genuine acquisition order or only a fixed loader
   order;
2. whether the horizontal axis should be an adaptation-step index rather than
   physical time;
3. whether any constructed stream is clearly labeled as constructed;
4. which quantities are defensible to plot, such as windowed accuracy,
   \(D_{\mathrm{JS}}(\overline{\mathbf p}_t\|\mathbf q_{t-1})\), or prediction
   concentration;
5. how visualization-only choices such as a smoothing window are disclosed;
6. how historical lag and abrupt-change failure cases are reported without
   turning a design intention into a finding.

Until these questions are resolved, keep temporal behavior as a TODO in planning
notes or future analysis, not as a promised paper contribution or completed
experiment. If activated after review, count it as a potential fifth experiment
group rather than silently folding it into the current four-group plan.

## 8. Wording boundaries

Allowed only when supported under the exact protocol:

- `improves over STDA alone`;
- `exhibits a broad empirical plateau over the tested parameter range`;
- `shows low run-to-run dispersion`;
- `uses an O(C) historical prediction reference`;
- `adds no auxiliary trainable network`.

Avoid without direct evidence:

- `guarantees stable adaptation`;
- `eliminates channel effects`;
- `recovers the true transmitter activity profile`;
- `is hyperparameter-insensitive` without range and protocol;
- `is robust across backbones or directions` from a tuned single case;
- any final-method claim based on removed-module results.
