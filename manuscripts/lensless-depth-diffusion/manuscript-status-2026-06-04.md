# Manuscript: Lensless Depth Diffusion

## Metadata

- Project ID: `lensless-depth-diffusion`
- Working title: Physics-Guided Depth Estimation for PSF-Stack Lensless Imaging
- Target format: final graphics project report, short conference-paper style
- Status: manuscript and poster updated with the synthetic-only `LDLDM` results, rebuilt architecture figure, and metric-only comparison table
- Current PDF export: `exports/main-prelim-2026-06-04.pdf`
- HTML archive: `https://donggeonbae.github.io/writing/projects/lensless-depth-diffusion-manuscript-status/`
- Canonical live status: `https://donggeonbae.github.io/research/projects/lensless-depth-diffusion-final-model-status/`

## Core Claim

PSF-stack deconvolution provides depth-dependent focus evidence. The final `LDLDM` model places that physics inside latent diffusion through a learnable PSF-Wiener bank, focus-posterior evidence, a latent depth VAE, and conditional denoising.

## Final Method Text

The manuscript should describe `LDLDM` compactly:

- Synthetic lensless measurement from RGB, depth, and a 42-plane PSF stack.
- PSF-stack Wiener deconvolution and focus-posterior features.
- Latent depth VAE encoder/decoder.
- Conditional latent denoising U-Net.
- Focus-posterior alignment inside the latent diffusion condition.
- Learned depth-prior initialization for sampling.
- Depth-guided RGB fusion from deconvolution planes.

Avoid describing the method as only `deconv + UNet`. Supervised deconvolution and plane-posterior models are diagnostic references, not `LDLDM`.

## Final Results

| Method | fg delta1 | fg delta2 | fg delta3 | fg MAE | Boundary MAE |
| --- | ---: | ---: | ---: | ---: | ---: |
| Physics focus, lambda=1e-4 | 0.391 | 0.617 | 0.816 | 0.2137 | 0.2368 |
| Raw-measurement U-Net | 0.436 | 0.629 | 0.753 | 0.2040 | 0.3760 |
| Deconv-volume U-Net | 0.865 | 0.926 | 0.949 | 0.0501 | 0.1144 |
| FlatNet3D-style RGB/depth | 0.823 | 0.908 | 0.939 | 0.0685 | 0.1740 |
| Plane-posterior U-Net | 0.898 | 0.939 | 0.957 | 0.0369 | 0.0925 |
| **LDLDM** | 0.879 | 0.918 | 0.931 | 0.0847 | 0.1126 |
| Plane-posterior + calibration | 0.885 | 0.946 | 0.971 | 0.0406 | 0.1099 |

Final interpretation:

- `LDLDM` is selected because it is the promoted physics-integrated latent diffusion model.
- It substantially improves over physics-only inference and remains below direct plane-posterior supervision.
- The 98% target is not reached.

## Scope Note

The current manuscript is scoped to synthetic train/test evaluation. Real-capture validation is left as the next step for demonstrating practical effectiveness and is not included in the final comparison table.

## Figure Set

| Figure | Manuscript role | Current status |
| --- | --- | --- |
| Architecture | Method overview | Uses the synthetic LDLDM architecture figure with PSF-Wiener physics, latent encoder/decoder, diffusion denoising, and output fusion |
| Figure 2: deconvolution focus planes | Physics evidence | Split into a large two-column figure using `z={14,22,30,38}`; excludes weak early planes |
| Figure 3: depth comparison | Qualitative comparison | Separate two-column comparison showing RGB, GT depth, physics baseline, and `LDLDM`; teacher/error omitted |

## Discussion Points

- The deconvolution volume is the strongest representation across all non-diffusion and diffusion variants.
- `LDLDM` is methodologically aligned with the project objective, but not SOTA on this dataset.
- The current gap is mainly calibration and boundary ambiguity.
- The next validation step is to test measured lensless captures with calibrated exposure, sensor noise, and PSF alignment.

## Verification Status

- Shared synthetic-test diffusion evaluation completed.
- Paper and poster now use the final `LDLDM` aggregate.
- Architecture figure has been replaced in the paper, poster, and figure archive.
- Paper Figure 2 and Figure 3 are now separated into two-column wide figures.
- Final PDFs and encrypted HTML pages have been rebuilt after the latest text and metric update.
