# Manuscript: Lensless Depth Diffusion

## Metadata

- Project ID: `lensless-depth-diffusion`
- Working title: Physics-Integrated Latent Diffusion for Lensless Depth Estimation
- Target venue: final graphics project report, short conference-paper style
- Status: manuscript and PDF export updated with final v15 330k metrics plus real-adaptive learnable deconvolution diagnostics
- Related research notes: `../../research/notes/lensless-depth-diffusion/final-model-status-2026-06-04.md`
- Related reviews: none yet
- Related figures: `../../figure/figures/lensless-depth-diffusion/figure-set-2026-06-04.md`
- Related presentation: `../../presentation/poster/lensless-depth-diffusion/poster-2026-06-04.md`
- Current PDF export: `exports/main-prelim-2026-06-04.pdf`
- HTML archive: `https://donggeonbae.github.io/writing/projects/lensless-depth-diffusion-manuscript-status/`
- Canonical live status: `https://donggeonbae.github.io/research/projects/lensless-depth-diffusion-final-model-status/`

## Core Claim

PSF-stack deconvolution provides depth-dependent focus evidence, and integrating that physics into a latent diffusion depth model yields substantially better depth estimates than physics-only focus scoring while preserving the project objective of physics-aware diffusion.

## Abstract

The working manuscript reports Ours v15, a physics-integrated latent diffusion model for depth estimation from synthetic lensless measurements. Final full-test evidence uses the 330k-step checkpoint after 5.0 epochs.

## Introduction

The introduction should motivate lensless depth estimation as a problem where the measurement is governed by a depth-dependent PSF stack. The key gap is that static deconvolution or supervised restoration does not directly answer how physics should affect the diffusion reverse process.

## Related Work

Citation groups to verify before final submission:

- MWDNs and Wiener/deconvolution-based lensless restoration.
- FlatNet3D and supervised lensless 3D reconstruction.
- Marigold and DiffusionDepth for diffusion-based depth priors.
- DiffBIR, StableSR, and related restoration diffusion methods as contrastive examples, not direct templates.

## Method

The final method should be described compactly:

- Synthetic lensless measurement generation from RGB, depth, and a 42-plane PSF stack.
- PSF-stack Wiener deconvolution volume and focus-derived features.
- Latent depth autoencoder.
- Conditional latent denoising model.
- DAPS-lite posterior guidance/refinement during reverse diffusion.
- Depth-guided RGB plane fusion for reconstruction checks.
- Real-capture diagnostic branch: learnable Wiener inverse plus residual artifact adapter trained against pseudo labels.

Avoid describing Ours as simply `deconv + UNet`.

## Experiments or Analysis

Current setup:

- Train: 66,000 RGB/depth pairs.
- Test: 6,000 RGB/depth pairs.
- Current reported Ours checkpoint: v15 at 330,000 steps, equal to 5.0 epochs.
- Active convergence run: complete.
- Latest continuation checkpoint verified: 330,000 steps.
- Latest train-log state observed: step 330,000.
- 225k, 230k, and 235k full-test evaluations are complete as intermediate convergence checks.
- A 4-GPU sharded full-test evaluation is complete for the final 330k `latest.pt`.
- `Ours-RealAdapt` real-capture diagnostic trained for 30 epochs; best checkpoint selected at epoch 15 by 20250505 pseudo-label foreground MAE.

## Results

Final full-test result:

| Method | fg delta1 | fg delta2 | fg delta3 | fg MAE |
| --- | ---: | ---: | ---: | ---: |
| Physics-only focus/deconv | 0.391 | 0.617 | 0.816 | 0.214 |
| Ours v15, 195k | 0.871 | 0.913 | 0.930 | 0.0567 |
| Ours v15, 225k | 0.878 | 0.920 | 0.938 | 0.0536 |
| Ours v15, 230k | 0.865 | 0.908 | 0.928 | 0.0561 |
| Ours v15, 235k | 0.857 | 0.904 | 0.924 | 0.0600 |
| Ours v15, 330k | 0.877 | 0.922 | 0.941 | 0.0515 |

The supervised residual teacher reaches a higher reported delta3 in existing notes, but it is not the final `Ours` model because the project objective is physics-integrated diffusion.

Convergence signal: the 330k checkpoint improves over 225k on foreground delta2, delta3, MAE, AbsRel, RMSE, and boundary MAE, although 225k remains slightly better on foreground delta1. The final manuscript row is therefore `Ours v15, 330k`.

Real-capture diagnostic after the learnable deconvolution update:

| Split | Samples | Physics focus MAE / d1 / d3 | Diffusion Ours MAE / d1 / d3 | Ours-RealAdapt MAE / d1 / d3 |
| --- | ---: | ---: | ---: | ---: |
| 20250505 real validation | 20 | 0.230 / 0.294 / 0.852 | 0.365 / 0.337 / 0.639 | 0.264 / 0.382 / 0.648 |
| 20250527 real subset | 32 | 0.291 / 0.218 / 0.662 | 0.419 / 0.198 / 0.390 | 0.177 / 0.363 / 0.692 |

These real-capture values use provided pseudo-depth labels, not independently measured GT depth. They are included as a domain-gap diagnostic rather than a replacement for the synthetic full-test table. `Ours-RealAdapt` is the response to the validation artifact issue: it makes the PSF inverse learnable and suppresses fixed deconvolution artifacts, but it is not relabeled as the final diffusion `Ours`.

## Figure Plan

The manuscript figure set is maintained in `donggeonbae/figure` and should be updated before replacing paper exports.

| Figure | Manuscript role | Required update before final |
| --- | --- | --- |
| Architecture | Method overview for latent diffusion plus PSF-Wiener posterior guidance | Keep latent encoder/decoder, denoising UNet, reverse guidance, and real PSF/raw/RGB/depth/output insets visible |
| Deconvolution focus planes | Evidence that the stack carries depth-dependent focus | Use z=14,22,30,38 unless a new calibration makes early planes useful |
| Depth results | Qualitative comparison | Use RGB, GT depth, physics-only focus, and Ours; omit teacher and pure error maps |
| Real-data comparison | Domain-gap diagnostic | Show measured raw, pseudo labels, physics, supervised baselines, teacher, Ours-RealAdapt, and diffusion Ours |

## Discussion

The final result supports the claim that deconvolution focus structure is a useful depth cue and that a latent diffusion prior can regularize it. The main unresolved question is whether the reverse-diffusion posterior guidance can be made metric-dominant over simpler integrated diffusion or supervised teacher variants. The real-capture pseudo-label diagnostic also shows that synthetic-trained checkpoints do not transfer cleanly to measured raw captures without exposure/PSF calibration. The learnable deconvolution update reduces this failure mode on pseudo labels, especially on the 20250527 real subset, but it should be described as real-domain adaptation rather than as proof of diffusion superiority.

## Limitations

- Measurements are currently synthetic rather than measured lensless raw captures.
- Final 5epoch full-test metrics are available.
- 225k, 230k, 235k, and 330k full-test metrics are complete.
- 98% target has not been verified by the diffusion model.
- Real-capture comparison currently uses pseudo labels and should be treated as a domain-gap diagnostic only.
- `Ours-RealAdapt` improves real pseudo-label alignment, but it is supervised real-domain fitting and does not replace the diffusion-method row.
- Architecture figure is currently a bitmap and may need vector redraw for final readability.
- Some related-work citation metadata still needs final verification.

## Conclusion

The manuscript reports Ours as the best physics-integrated diffusion model, not the best supervised baseline. The final reported checkpoint is v15 at 330k steps.

## Citation Gaps

- Verify exact MWDNs citation metadata.
- Verify FlatNet3D citation metadata and dataset/method claims.
- Verify Marigold, DiffusionDepth, DiffBIR, StableSR, and HYPIR citations.
- Add access dates for code repositories used as method context.

## Verification Gaps

- Full 6,000-sample evaluation of 225k checkpoint is complete.
- Full 6,000-sample evaluations of 230k and 235k checkpoints are complete and weaker than 225k.
- Full 6,000-sample evaluation of final 330k checkpoint is complete.
- Best v15 checkpoint for `Ours` is 330k.
- Paper table, poster table, figure captions, and HTML research note are updated.
- Working paper PDF and presentation poster PDF are rebuilt.
- `exports/main-prelim-2026-06-04.pdf` has been replaced after final checkpoint metrics were written into the paper.
- Real-capture figures and manuscript discussion are updated with `Ours-RealAdapt`.
