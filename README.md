# Awesome Earth Downscaling (地球科学降尺度)

> Curated list of **weather / climate / hydrology downscaling** (降尺度 / super-resolution) resources: classical, dynamical, and especially **deep learning**, with a focus on **NVIDIA Earth-2 / CorrDiff**.

> 仅收录已核验链接的论文、代码与工具；禁止编造 arXiv ID、作者或年份。

**Last updated:** 2026-11-05 (Asia/Shanghai) · Maintainer: [lihuirui](https://github.com/lihuirui)

**Stats:** see [`data/papers.json`](data/papers.json) for structured DL / recent entries.

## Table of Contents

- [Surveys / 综述](#surveys--综述)
- [Classical & Statistical Downscaling / 经典与统计降尺度](#classical--statistical-downscaling--经典与统计降尺度)
- [Dynamical Downscaling / 动力降尺度](#dynamical-downscaling--动力降尺度)
- [Deep Learning Methods / 深度学习方法](#deep-learning-methods--深度学习方法)
  - [NVIDIA Earth-2 & CorrDiff / 英伟达 Earth-2](#nvidia-earth-2--corrdiff--英伟达-earth-2)
  - [Diffusion & Generative / 扩散与生成模型](#diffusion--generative--扩散与生成模型)
  - [GAN / CNN / U-Net](#gan--cnn--u-net)
  - [Transformer & Neural Operators](#transformer--neural-operators)
  - [Physics-informed & Hybrid](#physics-informed--hybrid)
- [Hydrology-focused Downscaling / 水文降尺度](#hydrology-focused-downscaling--水文降尺度)
- [Datasets & Benchmarks / 数据集与基准](#datasets--benchmarks--数据集与基准)
- [Libraries & Toolkits / 工具库](#libraries--toolkits--工具库)
- [Recent arXiv (2023–2026) / 近年预印本](#recent-arxiv-20232026--近年预印本)
- [Related Awesome Lists / 相关列表](#related-awesome-lists--相关列表)
- [Maintenance](#maintenance)

---

## Surveys / 综述

- **Are Deep Learning Methods Suitable for Downscaling Global Climate Projections?** — González-Abad & Gutiérrez (2024) [[arXiv](https://arxiv.org/abs/2411.05850)] [[Code](https://doi.org/10.5281/zenodo.14016954)] — _DeepESD vs U-Net intercomparison for PP projection downscaling over Spain._
- **Deep Learning and Foundation Models for Weather Prediction: A Survey** — Shi et al. (2025) [[arXiv](https://arxiv.org/abs/2501.06907)] [[Code](https://github.com/JimengShi/DL-Foundation-Models-Weather)] — _Training-paradigm taxonomy; curated code & datasets (broader weather ML, includes downscaling context)._
- **Deep learning in statistical downscaling for deriving high spatial resolution gridded meteorological data: A systematic review** — (ISPRS J. Photogramm. Remote Sens., 2024) [[DOI](https://doi.org/10.1016/j.isprsjprs.2023.12.011)] — _Systematic review of DL statistical downscaling for gridded meteorology._
- **On the modern deep learning approaches for precipitation downscaling** — (Earth Science Informatics, 2023) [[DOI](https://doi.org/10.1007/s12145-023-00970-4)] — _Compares DeepSD, ConvLSTM, U-Net, SR-GAN for precip._

## Classical & Statistical Downscaling / 经典与统计降尺度

- **BCSD / Bias Correction Spatial Disaggregation** — widely used MOS-style pipeline; Python example [[Code](https://github.com/tjvandal/bcsd-python)]
- **scikit-downscale** — statistical climate downscaling in Python (Pangeo) [[GitHub](https://github.com/pangeo-data/scikit-downscale)]
- **ClimDown** — PCIC daily climate downscaling library (R) [[GitHub](https://github.com/pacificclimate/ClimDown)]
- **carbonplan/cmip6-downscaling** — CMIP6 climate downscaling workflows [[GitHub](https://github.com/carbonplan/cmip6-downscaling)]
- **NEX-GDDP** — NASA Earth Exchange Global Daily Downscaled Projections (CMIP6) — see Thrasher et al. dataset papers / NASA NEX pages

> Classic methods also include quantile mapping, SDSM-style regression, analogs, and weather generators (see Maraun & Widmann textbook literature).

## Dynamical Downscaling / 动力降尺度

- **WRF** — Weather Research and Forecasting Model (regional nesting workhorse)
- **RegCM** — ICTP Regional Climate Model
- **CORDEX** — Coordinated Regional Climate Downscaling Experiment (multi-RCM ensembles)

> Dynamical downscaling provides physically consistent fields at ~10–50 km (or finer) but at high compute cost; often paired with statistical post-processing.

## Deep Learning Methods / 深度学习方法

### NVIDIA Earth-2 & CorrDiff / 英伟达 Earth-2

- **CorrDiff (Residual Corrective Diffusion)** — Mardani, Brenowitz, Cohen, Pathak et al. (2023) [[arXiv](https://arxiv.org/abs/2309.15214)] — _Two-step UNet mean + corrector diffusion; km-scale atmospheric downscaling (e.g. 25 km → 2 km); core Earth-2 generative downscaling method._
- **PhysicsNeMo CorrDiff example** — NVIDIA training/inference recipes [[Docs](https://docs.nvidia.com/physicsnemo/latest/physicsnemo/examples/weather/corrdiff/README.html)] [[Code](https://github.com/NVIDIA/physicsnemo)] — _Official example (legacy path; see also regional weather diffusion)._
- **Earth2Studio** — NVIDIA open framework for AI weather/climate workflows; includes CorrDiff diagnostics models [[GitHub](https://github.com/NVIDIA/earth2studio)] [[CorrDiff source](https://github.com/NVIDIA/earth2studio/blob/main/earth2studio/models/dx/corrdiff.py)]
- **CorrDiff NIM / API overview** — production-oriented CorrDiff downscaling service docs [[Docs](https://docs.nvidia.com/nim/earth-2/corrdiff/latest/overview.html.md)]
- **CorrDiff US (GEFS→HRRR)** — CONUS generative downscaling model card [[API ref](https://docs.api.nvidia.com/nim/reference/nvidia-corrdiff)]

### Diffusion & Generative / 扩散与生成模型

- **Generative diffusion-based downscaling for climate** — Watt & Mansfield (2024) [[arXiv](https://arxiv.org/abs/2404.17752)] [[Code](https://github.com/robbiewatt1/ClimateDiffuse)] — _Continental ERA5 2°→0.25° diffusion vs U-Net; ensembles + spectra._
- **Conditional diffusion for regional precipitation** — Shidqi et al. (2023) [[arXiv](https://arxiv.org/abs/2312.07112)] — _DDPM conditioned on multi-variable LR CESM fields; 4×/8× precip._
- **Debias Coarsely, Sample Conditionally (OT + diffusion)** — Wan et al. (2023) [[arXiv](https://arxiv.org/abs/2305.15618)] — _Optimal transport + probabilistic diffusion for statistical downscaling._
- **STVD — Precipitation Downscaling with Spatiotemporal Video Diffusion** — (NeurIPS 2024) [[Code](https://github.com/mandt-lab/STVD)] — _Spatiotemporal video diffusion for precip downscaling._
- **WassDiff** — generative precip downscaling focused on extremes [[GitHub](https://github.com/Way-Yuhao/WassDiff)]

### GAN / CNN / U-Net

- **DeepSD** — Vandal et al. (2017) [[arXiv](https://arxiv.org/abs/1703.03126)] [[Code](https://github.com/tjvandal/deepsd)] *(KDD 2017)* — _Stacked SRCNN landmark for precip statistical downscaling._
- **Stochastic GAN downscaling of precip forecasts** — Harris et al. (2022) [[arXiv](https://arxiv.org/abs/2204.02028)] — _GAN / VAE-GAN from NWP to radar; CRPS & spectra._
- **Price & Rasp generative precip downscaling** — (2022) [[arXiv](https://arxiv.org/abs/2203.12297)] *(AISTATS)* — _Deep generative models for precip forecast resolution/accuracy._
- **DSGAN** — GAN for precipitation downscaling [[GitHub](https://github.com/lzhengchun/DSGAN)]
- **DeepESD** — Baño-Medina et al. convolutional+dense PP downscaling (see 2024 intercomparison above)
- **Probabilistic U-Net climate downscaling** — Alipourhajiagha et al. (2025) [[arXiv](https://arxiv.org/abs/2511.03197)] [[Code](https://github.com/MaryamAlipourH/prob-unet-climate-downscaling)] *(NeurIPS 2025 AI4Science Workshop)*

### Transformer & Neural Operators

- **Fourier Neural Operators for Arbitrary Resolution Climate Data Downscaling** — Yang et al. (2023) [[arXiv](https://arxiv.org/abs/2305.14452)] — _FNO for flexible-resolution climate downscaling._
- **ORBIT-2** — Exascale Vision Transformer for weather/climate downscaling & forecasting [[GitHub](https://github.com/XiaoWang-Github/ORBIT-2)]

### Physics-informed & Hybrid

- **Hard-Constrained Deep Learning for Climate Downscaling** — Harder et al. [[arXiv](https://arxiv.org/abs/2208.05424)] — _Hard physical constraints in DL downscaling._

## Hydrology-focused Downscaling / 水文降尺度

- **RainNet** — large-scale imagery dataset & benchmark for spatial precip downscaling (NeurIPS 2022) [[GitHub](https://github.com/neuralchen/RainNet)]
- **GPM-Downscaling** — ML methods for satellite precipitation downscaling [[GitHub](https://github.com/XiaogangHe/GPM-Downscaling)]
- **RainFARM** — stochastic precip downscaling (R / Julia) [[rainfarmr](https://github.com/jhardenberg/rainfarmr)] [[RainFARM.jl](https://github.com/jhardenberg/RainFARM.jl)]
- **TopoPyScale** — hillslope-scale climate downscaling [[GitHub](https://github.com/ArcticSnow/TopoPyScale)]

> Hydrology uses often target precip intensity/extremes, catchment forcing, and flood-relevant fields; prefer methods that preserve intermittency and heavy tails.

## Datasets & Benchmarks / 数据集与基准

- **ERA5 / ERA5-Land** — ECMWF reanalysis (common LR/HR pairs via coarsening or land product)
- **HRRR / GEFS** — used in CorrDiff US (GEFS→HRRR) setups
- **PRISM / Daymet** — high-res US observational grids (common downscaling targets)
- **CHIRPS / IMERG / GPM** — satellite precip products for hydro downscaling
- **CESM / CMIP** — GCM fields as LR inputs for climate downscaling
- **RainNet benchmark** — spatial precip downscaling imagery [[GitHub](https://github.com/neuralchen/RainNet)]
- **CorrDiff CONUS dataset notes** — PhysicsNeMo docs for ERA5–HRRR style training data [[Docs](https://github.com/NVIDIA/physicsnemo/blob/main/examples/weather/regional_weather_diffusion/docs/CORRDIFF_CONUS_DATASET.md)]

## Libraries & Toolkits / 工具库

- **[Earth2Studio](https://github.com/NVIDIA/earth2studio)** — AI weather/climate workflows (includes CorrDiff)
- **[PhysicsNeMo](https://github.com/NVIDIA/physicsnemo)** — NVIDIA physics-ML framework (CorrDiff / regional diffusion examples)
- **[scikit-downscale](https://github.com/pangeo-data/scikit-downscale)** — statistical downscaling
- **[ClimateDiffuse](https://github.com/robbiewatt1/ClimateDiffuse)** — diffusion climate downscaling
- **xarray / dask / Zarr** — data plumbing for large geospatial tensors
- **CDO / ESMF** — remapping & regridding utilities

## Recent arXiv (2023–2026) / 近年预印本

Selected verified entries (also mirrored in `data/papers.json`):

- 2025 — Probabilistic U-Net climate downscaling [[arXiv](https://arxiv.org/abs/2511.03197)] [[Code](https://github.com/MaryamAlipourH/prob-unet-climate-downscaling)]
- 2025 — DL & foundation models for weather (survey) [[arXiv](https://arxiv.org/abs/2501.06907)]
- 2024 — DL suitability for GCM projection downscaling [[arXiv](https://arxiv.org/abs/2411.05850)]
- 2024 — Generative diffusion climate downscaling [[arXiv](https://arxiv.org/abs/2404.17752)] [[Code](https://github.com/robbiewatt1/ClimateDiffuse)]
- 2023 — CorrDiff residual corrective diffusion [[arXiv](https://arxiv.org/abs/2309.15214)]
- 2023 — Conditional DDPM regional precip [[arXiv](https://arxiv.org/abs/2312.07112)]
- 2023 — FNO arbitrary-resolution climate downscaling [[arXiv](https://arxiv.org/abs/2305.14452)]
- 2023 — OT + diffusion statistical downscaling [[arXiv](https://arxiv.org/abs/2305.15618)]
- 2022 — GAN stochastic precip forecast downscaling [[arXiv](https://arxiv.org/abs/2204.02028)]
- 2022 — Generative precip forecasts (Price & Rasp) [[arXiv](https://arxiv.org/abs/2203.12297)]
- 2022 — Hard-constrained DL climate downscaling [[arXiv](https://arxiv.org/abs/2208.05424)]
- 2022 — UK local-scale climate ML emulation [[arXiv](https://arxiv.org/abs/2211.16116)]

## Related Awesome Lists / 相关列表

- [awesome-time-series-foundation-models](https://github.com/lihuirui/awesome-time-series-foundation-models)
- [awesome-ai-earth-science](https://github.com/lihuirui/awesome-ai-earth-science) _(sibling list)_
- [Awesome-LWMs](https://github.com/lihuirui/Awesome-LWMs) _(large weather models)_
- [DL-Foundation-Models-Weather](https://github.com/JimengShi/DL-Foundation-Models-Weather)

## Maintenance

- Structured entries: [`data/papers.json`](data/papers.json)
- Status / gaps: [`STATUS.md`](STATUS.md)
- Contributions: [`CONTRIBUTING.md`](CONTRIBUTING.md)
- License: [CC0-1.0](LICENSE)

This list is updated on a **~3-day cadence** (automated) plus manual curation. Prefer PRs with verified links.
