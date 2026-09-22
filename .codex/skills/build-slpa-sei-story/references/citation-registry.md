# SLPA-SEI Citation Registry

This file records the canonical citation identity for papers already verified for
the SLPA-SEI manuscript. Use one row per paper. Reuse the exact key in every
section and keep one corresponding entry in the manuscript BibTeX database.

Before adding a paper, check DOI first and normalized title second. If the paper
already appears here, update missing verified metadata in its existing row rather
than creating an alias. Prefer the final published version over an earlier
preprint when both represent the same work.

| Canonical key | Verified paper | Persistent identifier | Current SLPA-SEI use |
|---|---|---|---|
| `liu2023longspan` | A Long Time Span-Specific Emitter Identification Method Based on Unsupervised Domain Adaptation | `10.3390/rs15215214` | Long-span and domain-adaptation related work |
| `liu2024msida` | Multi-Scale Iterative Domain Adaptation for Specific Emitter Identification | `10.1007/s10489-024-05484-0` | Domain-adaptation related work |
| `wan2024vcsei` | VC-SEI: Robust Variable-Channel Specific Emitter Identification Method Using Semi-Supervised Domain Adaptation | `10.1109/TWC.2024.3463740` | Variable-channel and domain-adaptation related work |
| `wu2026crossday` | Toward Robust IoT Device Authentication: Cross-Day Specific Emitter Identification via Domain Adaptation | `10.1109/JIOT.2026.3680586` | Cross-day domain-adaptation related work |
| `wang2025singlesource` | Avoiding Shortcuts: Enhancing Channel-Robust Specific Emitter Identification via Single-Source Domain Generalization | `10.1109/TWC.2025.3528568` | Single-source domain-generalization related work |
| `wan2025sigmix` | SigMix: Robust Specific Emitter Identification Method Enhanced by Cross-Time and Cross-Receiver Mixing Augmentation | `10.1109/JIOT.2025.3546406` | Cross-time and cross-receiver generalization related work |
| `wang2025tfmix` | TFMix: A Robust Time-Frequency Mixing Approach for Domain Generalization in Specific Emitter Identification | `10.1109/TCCN.2025.3541723` | Time-frequency domain-generalization related work |
| `IsmailFawaz2020inceptionTime` | InceptionTime: Finding AlexNet for Time Series Classification | `10.1007/s10618-020-00710-y` | SCNN architectural basis |
| `wang2021tent` | Tent: Fully Test-Time Adaptation by Entropy Minimization | `https://openreview.net/forum?id=uXl3bZLkr3c` | Foundational test-time-adaptation baseline |
| `niu2022eata` | Efficient Test-Time Model Adaptation without Forgetting | `https://proceedings.mlr.press/v162/niu22a.html` | Efficient test-time-adaptation baseline |
| `shanmugam2021betteraggregation` | Better Aggregation in Test-Time Augmentation | `10.1109/ICCV48922.2021.00125` | AugTTA comparison method |
| `ganin2016dann` | Domain-Adversarial Training of Neural Networks | `https://www.jmlr.org/papers/v17/15-239.html` | Domain-adversarial comparison method |
| `sun2016deepcoral` | Deep CORAL: Correlation Alignment for Deep Domain Adaptation | `10.1007/978-3-319-49409-8_35` | Correlation-alignment comparison method |
| `niu2023sar` | Towards Stable Test-Time Adaptation in Dynamic Wild World | `https://openreview.net/forum?id=g2YraF75Tj` | Dynamic test-time-adaptation baseline |
| `li2026rfftta` | RFF-TTA: Physical Information-Aware Prototype for Temporally Varying RF Fingerprinting Online Test-Time-Adaptation | `10.1609/aaai.v40i1.37034` | Radio-frequency test-time adaptation |
| `zha2026anr` | Adaptive Noise-Resilient Test-Time Adaptation for RF Signal Recognition | `10.1109/TCCN.2026.3657107` | Radio-frequency test-time adaptation under noise variation |
| `hanna2022wisig` | WiSig: A Large-Scale WiFi Signal Dataset for Receiver and Channel Agnostic RF Fingerprinting | `10.1109/ACCESS.2022.3154790` | WiSig dataset and cross-date experiments |
| `sankhe2019oracle` | ORACLE: Optimized Radio clAssification through Convolutional neuraL nEtworks | `10.1109/INFOCOM.2019.8737463` | ORACLE dataset and distance-dependent experiments |

## Maintenance contract

For each newly verified paper, record its canonical key, exact published title,
DOI or authoritative publication URL, and intended use in SLPA-SEI. If a later
metadata check finds that two rows are the same paper, retain the earlier stable
key, merge the verified information, update all manuscript citations, and remove
the duplicate row and BibTeX entry.

Do not register a paper from a search-result snippet alone. Do not invent missing
metadata. Dataset papers, baselines, and newly added related work should be added
here only after their official publication record has been checked.
