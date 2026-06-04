# Manuscript: Lensless Depth Diffusion

## Metadata

- Project ID: `lensless-depth-diffusion`
- Working title: Physics-Integrated Latent Diffusion for Lensless Depth Estimation
- Target venue: final graphics project report, short conference-paper style
- Status: preliminary manuscript exists in working project; final metrics pending
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

The working manuscript currently reports Ours v15, a physics-integrated latent diffusion model for depth estimation from synthetic lensless measurements. Current best full-test evidence uses the 225k-step checkpoint; the final 330k checkpoint has finished training and its full-test evaluation is running.

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

Avoid describing Ours as simply `deconv + UNet`.

## Experiments or Analysis

Current setup:

- Train: 66,000 RGB/depth pairs.
- Test: 6,000 RGB/depth pairs.
- Current reported Ours checkpoint candidate: v15 at 225,000 steps, approximately 3.41 epochs.
- Active convergence run: v15 continuation reached 330,000 steps, equal to 5.0 epochs.
- Latest continuation checkpoint verified: 330,000 steps.
- Latest train-log state observed: step 330,000.
- 225k, 230k, and 235k full-test evaluations are complete as intermediate convergence checks.
- A 4-GPU sharded full-test evaluation is running for the final 330k `latest.pt`.

## Results

Preliminary full-test result:

| Method | fg delta1 | fg delta2 | fg delta3 | fg MAE |
| --- | ---: | ---: | ---: | ---: |
| Physics-only focus/deconv | 0.391 | 0.617 | 0.816 | 0.214 |
| Ours v15, 195k | 0.871 | 0.913 | 0.930 | 0.0567 |
| Ours v15, 225k | 0.878 | 0.920 | 0.938 | 0.0536 |
| Ours v15, 230k | 0.865 | 0.908 | 0.928 | 0.0561 |
| Ours v15, 235k | 0.857 | 0.904 | 0.924 | 0.0600 |

The supervised residual teacher reaches a higher reported delta3 in existing notes, but it is not the final `Ours` model because the project objective is physics-integrated diffusion.

Current convergence signal: the 225k checkpoint has completed the 6,000-sample test evaluation with foreground delta3 0.938 and MAE 0.0536. The 230k and 235k full evaluations are weaker, so the running final 330k evaluation is the remaining check before changing or locking the final `Ours` row.

## Figure Plan

The manuscript figure set is maintained in `donggeonbae/figure` and should be updated before replacing paper exports.

| Figure | Manuscript role | Required update before final |
| --- | --- | --- |
| Architecture | Method overview for latent diffusion plus PSF-Wiener posterior guidance | Keep latent encoder/decoder, denoising UNet, reverse guidance, and real PSF/raw/RGB/depth/output insets visible |
| Deconvolution focus planes | Evidence that the stack carries depth-dependent focus | Use z=14,22,30,38 unless a new calibration makes early planes useful |
| Depth results | Qualitative comparison | Use RGB, GT depth, physics-only focus, and Ours; omit teacher and pure error maps |

## Discussion

The current result supports the claim that deconvolution focus structure is a useful depth cue and that a latent diffusion prior can regularize it. The main unresolved question is whether the reverse-diffusion posterior guidance gives measurable gains over static conditioning or mainly improves methodological alignment and interpretability.

## Limitations

- Measurements are currently synthetic rather than measured lensless raw captures.
- Final 5epoch full-test metrics are not yet available.
- 225k, 230k, and 235k intermediate full-test metrics are complete; the 330k full-test evaluation is running.
- 98% target has not been verified by the diffusion model.
- Architecture figure is currently a bitmap and may need vector redraw for final readability.
- Some related-work citation metadata still needs final verification.

## Conclusion

The manuscript should report Ours as the best physics-integrated diffusion model, not the best supervised baseline. Final claims must be updated after the active 330k full-test evaluation completes.

## Citation Gaps

- Verify exact MWDNs citation metadata.
- Verify FlatNet3D citation metadata and dataset/method claims.
- Verify Marigold, DiffusionDepth, DiffBIR, StableSR, and HYPIR citations.
- Add access dates for code repositories used as method context.

## Verification Gaps

- Full 6,000-sample evaluation of 225k checkpoint is complete.
- Full 6,000-sample evaluations of 230k and 235k checkpoints are complete and weaker than 225k.
- Full 6,000-sample evaluation of final 330k checkpoint.
- Decide best v15 checkpoint for `Ours`.
- Update paper table, poster table, figure captions, and HTML research note.
- Rebuild the working paper PDF and presentation poster PDF after the selected checkpoint is fixed.
- Replace `exports/main-prelim-2026-06-04.pdf` after final checkpoint metrics are written into the paper.
