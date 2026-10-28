# Multimodal LLM: visual token representations

This repository contains public notes and selected reports from experiments on visual representations in multimodal large language models.

## Research questions

- Do visual-token embeddings preserve information about human colour perception?
- How does the surrounding context affect the representation of the same physical colour?
- Are visual tokens interchangeable, or do they contain spatially and spectrally different information?
- Can colour coordinates be reconstructed from visual tokens with a simple linear model?

## Experiments

### Visual-token clustering

For one physical colour (`color_001`) shown under five surrounds (`bb`, `gb`, `gg`, `gw`, `ww`), the 64 visual tokens form an 8x8 spatial grid. Each token is a 3584-dimensional embedding.

KMeans clustering was evaluated for several values of `K`. At `K=2`, the tokens are primarily separated into a central colour patch and surrounding/background regions. Increasing `K` produces additional subgroups, but there is no direct one-to-one correspondence between the number of clusters and the number of colours. The cluster structure changes with the surround, indicating that context affects the visual representation.

### Spectral analysis

FFT/SVD-like analyses show that tokens have different spectral profiles and energy distributions. The visual tokens are therefore not interchangeable. The maximum energy is not always located in the central spatial region.

### Linear reconstruction of LCH

A linear mapping was trained from all visual tokens to the CIE LCH colour coordinates, with train/test splitting by image. Lightness (`L`) and colourfulness (`C`) are reconstructed more reliably than hue (`h`).

### Central-token hypothesis

The hypothesis that central visual tokens vanish or become zero was tested directly. The central tokens do not vanish; their behaviour is better interpreted as a structured response to the image and its surrounding context.

## Data and reproducibility

The experiments used colour stimuli and psychophysical measurements derived from the LUTCHI colour-appearance data, together with visual-token representations extracted from multimodal models. The original embedding arrays, private server paths, model checkpoints, and restricted datasets are not included in this public repository.

The reports in [`reports/`](reports/) document the experimental setup and selected findings. They are provided as research notes rather than as a complete reproducible pipeline.

## Repository structure

```text
.
├── README.md
└── reports/
    ├── experiment-description.pdf
    ├── visual-token-clustering.pdf
    ├── central-token-hypothesis.pdf
    └── token-embedding-analysis.pdf
```

## Status

This is an interim research repository. The next step is to add cleaned scripts and anonymised example data so that the analyses can be reproduced without access to the closed work server.
