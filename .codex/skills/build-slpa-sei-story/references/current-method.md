# SLPA-SEI Current Method Contract

Read this reference when locking equations, state variables, parameter meanings,
gradients, figures, or the online update order.

## 1. Scope

SLPA-SEI, short for **Short- and Long-Term Predictive Alignment for Specific
Emitter Identification**, addresses closed-set SEI under source-free, unlabeled,
online TTA and
time-varying wireless reception conditions. The registered emitter set is fixed.
The verified implementation adapts only allowed BN parameters and retains a compact
historical prediction-distribution reference across steps.

Use observation-interval language only when temporal acquisition order is real or
explicitly constructed. Otherwise use adaptation-step language.

## 2. Final structure

\[
\mathrm{SLPA\text{-}SEI}
=
\mathrm{STDA}
+
\mathrm{LTDA}.
\]

No third module is active. PGCI, signal augmentation, CO-SigDEM, projection,
Hi-MEC, EMA-MEC, DA/CB hierarchy, class-confidence history, confidence gating,
and reliable-sample filtering are removed from the current method.

## 3. STDA

For current probabilities \(p_{i,c}^t\), define

\[
\mathcal H_{\mathrm{CE}}^t
=
-\frac{1}{N_t}\sum_{i,c}p_{i,c}^t\log p_{i,c}^t,
\]

\[
\overline p_{t,c}
=
\frac{1}{N_t}\sum_i p_{i,c}^t,
\qquad
\mathcal H_{\mathrm{ME}}^t
=
-\sum_c\overline p_{t,c}\log\overline p_{t,c},
\]

and

\[
\mathcal L_{\mathrm{STDA}}^t
=
\mathcal H_{\mathrm{CE}}^t
-
\mathcal H_{\mathrm{ME}}^t.
\]

Do not add \(\lambda_{\mathrm{ME}}\). CE refines individual current decisions;
ME controls aggregate current concentration. The uniform-reference interpretation
of ME is a soft anti-collapse device, not a true emitter activity prior.

## 4. LTDA

Use only \(\mathbf q_t\in\mathbb R^C\) as the historical prediction reference.
The active discrepancy is

\[
\mathcal L_{\mathrm{LTDA}}^t
=
D_{\mathrm{JS}}
\left(
\overline{\mathbf p}_t
\middle\|
\operatorname{sg}(\mathbf q_{t-1})
\right).
\]

The current distribution must remain differentiable. Detach only the historical
reference. Construct the discrepancy before updating the reference:

\[
\mathbf q_t
=
\mu\mathbf q_{t-1}
+
(1-\mu)\operatorname{sg}(\overline{\mathbf p}_t),
\qquad
\mu=\texttt{ema\_momentum}.
\]

State \(\mathbf q_0\) exactly as initialized in code. EMA accumulation is not the
alignment objective; JS supplies the current-to-history alignment.

## 5. Joint objective and parameters

\[
\mathcal L_{\mathrm{SLPA\text{-}SEI}}^t
=
\mathcal L_{\mathrm{STDA}}^t
+
\lambda_{\mathrm{mec}}
\mathcal L_{\mathrm{LTDA}}^t.
\]

The only method-specific parameters are:

- `lambda_mec`: relative weight of LTDA;
- `ema_momentum`: historical-reference momentum.

Retain these names. Do not introduce another method coefficient, threshold, gate,
or divergence parameter.

## 6. Gradient and state order

Keep gradients through current probabilities and the current aggregate. Stop
gradients through the stored reference. A typical prequential step is:

1. receive signals with \((\theta_{t-1},\mathbf q_{t-1})\);
2. score current signals;
3. compute STDA and LTDA;
4. update permitted BN parameters once;
5. store detached \(\mathbf q_t\);
6. continue with \((\theta_t,\mathbf q_t)\).

Verify the exact scoring order from code. Distinguish BN affine parameters, BN
running statistics, model parameters, and \(\mathbf q_t\).

## 7. Claim boundaries

Use `dual-timescale predictive alignment`, `current decision structure`, and
`historical prediction-distribution reference`. Do not claim semantic, feature,
channel, environment, or source--target alignment; complete identification state;
true activity-prior recovery; guaranteed stability; or arbitrary abrupt-change
robustness.

## 8. Required implementation facts

Verify before final equations or pseudocode:

1. exact logits/probability extraction for every backbone;
2. exact \(\mathbf q_0\) initialization;
3. current prediction and reference-update order;
4. BN affine and running-statistics behavior;
5. nonzero LTDA gradient through current predictions;
6. exact numerical safety operation in JS divergence;
7. that no removed loss or state remains active.
