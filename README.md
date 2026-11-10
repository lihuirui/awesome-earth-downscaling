# Awesome Earth Downscaling (地球科学降尺度)

> Curated list of **weather / climate / hydrology downscaling** (降尺度 / super-resolution) resources: classical, dynamical, and especially **deep learning**, with a focus on **NVIDIA Earth-2 / CorrDiff**.

> 仅收录已核验链接的论文、代码与工具；禁止编造 arXiv ID、作者或年份。

**Last updated:** 2026-11-10 (Asia/Shanghai) · Maintainer: [lihuirui](https://github.com/lihuirui)

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
- [Remote Sensing Spatial Downscaling / 遥感空间降尺度](#remote-sensing-spatial-downscaling--遥感空间降尺度)
- [Datasets & Benchmarks / 数据集与基准](#datasets--benchmarks--数据集与基准)
- [Libraries & Toolkits / 工具库](#libraries--toolkits--工具库)
- [Recent arXiv (2023–2026) / 近年预印本](#recent-arxiv-20232026--近年预印本)
- [Tutorials & Practical Guides / 教程与实践](#tutorials--practical-guides--教程与实践)
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
- **CorrDiffEra5Hrrr (distilled)** — official Earth2Studio diagnostic (v0.20.0, 2026-10-29) [[Docs](https://nvidia.github.io/earth2studio/main/modules/generated/models/dx/CorrDiffEra5Hrrr/)] [[Source](https://github.com/NVIDIA/earth2studio/blob/main/earth2studio/models/dx/corrdiff_era5_hrrr.py)] — _ERA5 0.25° → 3 km HRRR over CONUS; default `load_model` is the distilled 2-step generator (pass `distilled_model=False` for the 50-step teacher)._
- **CorrDiff CMIP6→ERA5** — official Earth2Studio / NVIDIA checkpoint [[HF](https://huggingface.co/nvidia/corrdiff-cmip6-era5)] [[Source](https://github.com/NVIDIA/earth2studio/blob/main/earth2studio/models/dx/corrdiff_cmip6.py)] — _CorrDiff U-Net; daily CMIP6 fields on a common ~300 km grid → hourly 25 km ERA5-like global fields (spatial and temporal)._
- **PrecipCorrDiff** — Kumar, Chattopadhyay, Bachhav et al. (2026) [[arXiv](https://arxiv.org/abs/2610.19994)] — _CorrDiff-style residual diffusion for IMD precipitation 0.25°→0.0625°; improves extremes & spatial bias vs SRGAN / original CorrDiff._
- **CorrFlow (residual flow matching)** — SIMO Group (2026) [[Code](https://github.com/SIMOGroup/CorrFlow)] — _Keeps CorrDiff two-stage residual mean+corrector; replaces diffusion corrector with conditional flow matching (1 Euler step); ERA5→ERA5-Land precip (SE Asia). arXiv ID not verified yet._

### Diffusion & Generative / 扩散与生成模型

- **Generative diffusion-based downscaling for climate** — Watt & Mansfield (2024) [[arXiv](https://arxiv.org/abs/2404.17752)] [[Code](https://github.com/robbiewatt1/ClimateDiffuse)] — _Continental ERA5 2°→0.25° diffusion vs U-Net; ensembles + spectra._
- **Conditional diffusion for regional precipitation** — Shidqi et al. (2023) [[arXiv](https://arxiv.org/abs/2312.07112)] — _DDPM conditioned on multi-variable LR CESM fields; 4×/8× precip._
- **Debias Coarsely, Sample Conditionally (OT + diffusion)** — Wan et al. (2023) [[arXiv](https://arxiv.org/abs/2305.15618)] — _Optimal transport + probabilistic diffusion for statistical downscaling._
- **STVD — Precipitation Downscaling with Spatiotemporal Video Diffusion** — (NeurIPS 2024) [[Code](https://github.com/mandt-lab/STVD)] — _Spatiotemporal video diffusion for precip downscaling._
- **WassDiff** — generative precip downscaling focused on extremes [[GitHub](https://github.com/Way-Yuhao/WassDiff)]
- **PrecipCorrDiff** — see Earth-2 section [[arXiv](https://arxiv.org/abs/2610.19994)]
- **Foundation model–conditioned precip diffusion** — Ribeiro et al. (2026) [[arXiv](https://arxiv.org/abs/2608.25858)] — _Concat vs cross-attn vs frozen Prithvi WxC encoder for daily precip DDPM (Colorado River Basin)._
- **CPMGEM-hourly (video diffusion)** — Addison, Kendon & Watson (2026) [[arXiv](https://arxiv.org/abs/2610.26145)] — _60 km daily predictors → 8.8 km hourly precip emulating Met Office CPM; flood extremes._
- **Multivariate monthly→daily spatio-temporal diffusion** — Huang et al. (2026) [[arXiv](https://arxiv.org/abs/2610.19885)] — _Conditional guidance: monthly 1° T+precip → daily 0.25° without retraining._
- **Flow matching for convective-scale precip** — Wetherell (2026) [[arXiv](https://arxiv.org/abs/2606.00281)] [[Code](https://github.com/mo-tomaswetherell/mo-flow-sg)] — _Conditional flow matching downscaling (mo-flow-sg)._
- **CorrFlow** — residual flow-matching corrector on CorrDiff stack [[Code](https://github.com/SIMOGroup/CorrFlow)]
- **Operator-Aware Posterior Sampling** — Saccardi, Saathof, Joseph & Dauwels (2026) [[arXiv](https://arxiv.org/abs/2610.39592)] [[Code](https://github.com/CarloSaccardi/operator-aware-weather-downscaling)] — _Diffusion prior with a learned coarse operator and per-channel guidance normalization; ERA5→CERRA multivariate downscaling without retraining the prior._
- **CD-FFM (likelihood functional flow matching)** — Liu, Toropainen, Kheder & Boy (2026) [[arXiv](https://arxiv.org/abs/2610.33482)] [[Code](https://github.com/Holmes-Alan/CD-FFM)] — _Treats the HR field as a continuous random field queryable at any location/resolution; ERA5→1 km daily temperature over Fennoscandia, also transfers to precip; reports faster sampling than a CorrDiff-style baseline._

### GAN / CNN / U-Net

- **DeepSD** — Vandal et al. (2017) [[arXiv](https://arxiv.org/abs/1703.03126)] [[Code](https://github.com/tjvandal/deepsd)] *(KDD 2017)* — _Stacked SRCNN landmark for precip statistical downscaling._
- **Stochastic GAN downscaling of precip forecasts** — Harris et al. (2022) [[arXiv](https://arxiv.org/abs/2204.02028)] — _GAN / VAE-GAN from NWP to radar; CRPS & spectra._
- **Price & Rasp generative precip downscaling** — (2022) [[arXiv](https://arxiv.org/abs/2203.12297)] *(AISTATS)* — _Deep generative models for precip forecast resolution/accuracy._
- **DSGAN** — GAN for precipitation downscaling [[GitHub](https://github.com/lzhengchun/DSGAN)]
- **DeepESD** — Baño-Medina et al. convolutional+dense PP downscaling (see 2024 intercomparison above)
- **Probabilistic U-Net climate downscaling** — Alipourhajiagha et al. (2025) [[arXiv](https://arxiv.org/abs/2511.03197)] [[Code](https://github.com/MaryamAlipourH/prob-unet-climate-downscaling)] *(NeurIPS 2025 AI4Science Workshop)*
- **ERA5→IMERG daily precip (West Africa)** — Sagna, Lguensat & Diatta (2026) [[arXiv](https://arxiv.org/abs/2610.16816)] — _U-Net / GAN downscaling of daily ERA5 (0.25°) to IMERG V07 (0.1°) over West Africa (JJASO 2000–2024); deterministic U-Nets are too dry and lose sub-few-hundred-km variance._

### Transformer & Neural Operators

- **Fourier Neural Operators for Arbitrary Resolution Climate Data Downscaling** — Yang et al. (2023) [[arXiv](https://arxiv.org/abs/2305.14452)] — _FNO for flexible-resolution climate downscaling._
- **ORBIT-2** — Exascale Vision Transformer for weather/climate downscaling & forecasting [[GitHub](https://github.com/XiaoWang-Github/ORBIT-2)]
- **Spherical Physics-informed Neural Operator** — Ye et al. (2026) [[arXiv](https://arxiv.org/abs/2610.24708)] [[DOI](https://doi.org/10.24963/ijcai.2026/734)] *(IJCAI 2026)* — _Spherical Laplacian decomposition plus physics constraints for global-to-regional meteorological downscaling; reports zero-shot queries at arbitrary locations._

### Physics-informed & Hybrid

- **Hard-Constrained Deep Learning for Climate Downscaling** — Harder et al. [[arXiv](https://arxiv.org/abs/2208.05424)] — _Hard physical constraints in DL downscaling._

## Remote Sensing Spatial Downscaling / 遥感空间降尺度

Curated from Milan Janosov’s [10(+2) Papers & Resources on Spatial Downscaling in Remote Sensing](https://milanjanosov.substack.com/p/10-papers-and-resources-on-spatial) ([X post](https://x.com/milan_janosov/status/2112440683835310405)). **All 12 items are spatial downscaling** (遥感空间降尺度；ML 语境常称 super-resolution).

> Caveat from the thread: downscaling does not invent new measurements—detail must come from a sharper guide (e.g. 10 m optical guiding 1 km thermal); otherwise detail is generative, not measured. Prefer products with error bars / uncertainty maps vs true HR observations.

### Surveys & Theory / 综述与理论
- **Downscaling in remote sensing** — Atkinson (2013) [[DOI](https://doi.org/10.1016/j.jag.2012.04.012)] — _Foundational RS downscaling review (area-to-point + super-resolution mapping)._
- **A review of spatial downscaling of satellite remotely sensed soil moisture** — Peng et al. (2017) [[DOI](https://doi.org/10.1002/2016RG000543)] — _Reviews of Geophysics survey of satellite SM downscaling._
- **An Overview of Theoretical and Practical Issues in Spatial Downscaling of Coarse Resolution Satellite-derived Products** — Park & Kim (2019) [[DOI](https://doi.org/10.7780/kjrs.2019.35.4.8)] — _Theory/practice overview for coarse satellite products._

### Thermal / LST / Evapotranspiration / 热红外·地表温度·蒸散
- **downscale-satelliteLST** — Python LST downscaling toolkit [[GitHub](https://github.com/pansism/downscale-satelliteLST)]
- **Downscaling a Satellite Thermal Image from 1000 m to 10 m (Python)** — Aboutalebi tutorial [[Article](https://towardsdatascience.com/downscaling-a-satellite-thermal-image-from-1000-m-to-10-m-python-3b2ed19ff103/)] [[Code](https://github.com/TIDOP-USAL/LST_S3_10m)] — _Sentinel-3 1 km → 10 m via Sentinel-2 NDVI._
- **Evaluating the feasibility of using Sentinel-2 and Sentinel-3 for high-resolution ET** — (2019) [[DOI](https://doi.org/10.1016/j.rse.2018.11.019)] *(RSE)* — _S2+S3 thermal sharpening for field-scale ET._
- **Combining Landsat 8 and Sentinel-2 in GEE for higher-resolution urban LST** — Onačillová et al. (2022) [[DOI](https://doi.org/10.3390/rs14164076)] [[Code](https://github.com/palubad/LST-downscaling-to-10m-GEE)] — _L8 LST → 10 m with S2 indices in Google Earth Engine._
- **A Data Mining Approach for Sharpening Thermal Satellite Imagery over Land** — Gao et al. (2012) [[DOI](https://doi.org/10.3390/rs4113287)] [[Code](https://github.com/radosuav/pyDMS)] — _Data Mining Sharpener (DMS); pyDMS reimplementation._
- **High-resolution LST gap-filling with multi-source DL** — Kustura et al. (2025) [[DOI](https://doi.org/10.3390/rs17020318)] — _CNN gap-filling / high-res LST (comment #12)._

### Deep Learning / Generative / 深度学习
- **Generative Adversarial Models for Extreme Geospatial Downscaling** — Li & Cao (2024/2025) [[arXiv](https://arxiv.org/abs/2402.14049)] [[Code](https://github.com/LiGuiye/LAG_Climate)] — _LAG conditional GAN; up to 64× wind/solar._
- **TAUT: Terrain-Adaptive U-Net Transformer for spatiotemporal temperature downscaling** — (2026) [[DOI](https://doi.org/10.3390/rs18030416)] — _0.1°→0.01°, 3 h→1 h T2m over SW China with terrain RS._
- **ESA OpenSR — Trustworthy SR of multispectral Sentinel-2 with latent diffusion** — Donike et al. (2025) [[DOI](https://doi.org/10.1109/jstars.2025.3542220)] [[Code](https://github.com/ESAOpenSR/opensr-model)] — _LDSR-S2 10 m→2.5 m RGB-NIR with uncertainty (comment #11)._

## Hydrology-focused Downscaling / 水文降尺度

- **RainNet** — large-scale imagery dataset & benchmark for spatial precip downscaling (NeurIPS 2022) [[GitHub](https://github.com/neuralchen/RainNet)]
- **GPM-Downscaling** — ML methods for satellite precipitation downscaling [[GitHub](https://github.com/XiaogangHe/GPM-Downscaling)]
- **RainFARM** — stochastic precip downscaling (R / Julia) [[rainfarmr](https://github.com/jhardenberg/rainfarmr)] [[RainFARM.jl](https://github.com/jhardenberg/RainFARM.jl)]
- **TopoPyScale** — hillslope-scale climate downscaling [[GitHub](https://github.com/ArcticSnow/TopoPyScale)]
- **SwAIther-Precip** — Assouline et al. (2026) [[arXiv](https://arxiv.org/abs/2605.16163)] — _Lead-time-aware U-Net bias correction + diffusion SR: AIFS → ~km precip over Switzerland (CombiPrecip); CRPS −48% vs raw AIFS._
- **CPMGEM-hourly** — Addison et al. (2026) [[arXiv](https://arxiv.org/abs/2610.26145)] — _Hourly km-scale precip video-diffusion emulator for flood/hydro extremes (UK CPM)._
- **PrecipCorrDiff (IMD)** — Kumar et al. (2026) [[arXiv](https://arxiv.org/abs/2610.19994)] — _High-res IMD gridded precip for hydro/climate applications (India)._
- **ERA5→IMERG West Africa** — Sagna et al. (2026) [[arXiv](https://arxiv.org/abs/2610.16816)] — _Daily monsoon precip downscaling to IMERG 0.1° (see U-Net section)._

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

- **[Earth2Studio](https://github.com/NVIDIA/earth2studio)** — AI weather/climate workflows (includes CorrDiff; v0.20.0 adds distilled CorrDiffEra5Hrrr and CorrDiff CMIP6)
- **[PhysicsNeMo](https://github.com/NVIDIA/physicsnemo)** — NVIDIA physics-ML framework (CorrDiff / regional diffusion examples)
- **[scikit-downscale](https://github.com/pangeo-data/scikit-downscale)** — statistical downscaling
- **[ClimateDiffuse](https://github.com/robbiewatt1/ClimateDiffuse)** — diffusion climate downscaling
- **xarray / dask / Zarr** — data plumbing for large geospatial tensors
- **CDO / ESMF** — remapping & regridding utilities

## Recent arXiv (2023–2026) / 近年预印本

Selected verified entries (also mirrored in `data/papers.json`):

- 2026 — Operator-aware posterior sampling (ERA5→CERRA) [[arXiv](https://arxiv.org/abs/2610.39592)] [[Code](https://github.com/CarloSaccardi/operator-aware-weather-downscaling)]
- 2026 — CD-FFM functional flow matching [[arXiv](https://arxiv.org/abs/2610.33482)] [[Code](https://github.com/Holmes-Alan/CD-FFM)]
- 2026 — Spherical physics-informed neural operator [[arXiv](https://arxiv.org/abs/2610.24708)]
- 2026 — ERA5→IMERG daily precip over West Africa [[arXiv](https://arxiv.org/abs/2610.16816)]
- 2026 — PrecipCorrDiff (IMD CorrDiff-style) [[arXiv](https://arxiv.org/abs/2610.19994)]
- 2026 — CPMGEM-hourly video-diffusion precip [[arXiv](https://arxiv.org/abs/2610.26145)]
- 2026 — Multivariate monthly→daily diffusion [[arXiv](https://arxiv.org/abs/2610.19885)]
- 2026 — Foundation model–conditioned precip diffusion [[arXiv](https://arxiv.org/abs/2608.25858)]
- 2026 — Flow matching convective-scale precip [[arXiv](https://arxiv.org/abs/2606.00281)] [[Code](https://github.com/mo-tomaswetherell/mo-flow-sg)]
- 2026 — SwAIther-Precip (AIFS→km Switzerland) [[arXiv](https://arxiv.org/abs/2605.16163)]
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

## Tutorials & Practical Guides / 教程与实践

### Hugging Face — Small U-Net downscaler on AIFS-ENS (France T2m)
Blog (2026-10-20): [Do we really need bigger AI weather forecasting models to improve resolution?](https://huggingface.co/blog/EmmaScharfmann/downscaling-a-weather-forecasting-model) — Emma Scharfmann, Aritra Roy Gosthipaty, Kashif Rasul.

**One-line takeaway:** 不必总造更大的全球细网格模型；可在现有 0.25° 预报上叠一个小残差降尺度器学地形/海岸局地细节。

**Recipe (compressed):**
1. **Task** — ensemble 2 m temperature, France, ~28 km (0.25°) → ~5.5 km (~0.05°).
2. **Train data** — coarse ERA5 + fine CERRA (2014–2019 train / 2020 eval); interpolate coarse→fine grid; learn **residual** (fine − interp).
3. **Statics** — fine orography, height difference vs coarse terrain, land fraction, distance-to-coast, lon/lat, season & time-of-day.
4. **Model** — ~2M-param U-Net; inject noise → multiple fine samples per coarse member; **fair CRPS** loss (land only).
5. **Train cost** — ~1 hour on one GPU (~20 epochs).
6. **Inference** — plug onto any same-var 0.25° France forecast (demo: AIFS-ENS; also tried GEFS / mention Aurora, Atlas). 10 coarse × 4 samples → 40 members; seconds per run.
7. **Reported skill (vs Météo-France stations)** — first 2 days: RMSE −14%, CRPS −21%; 10 days: −9% / −14%. Corrects mountains & coasts; does **not** fix large-scale bias of the coarse model.
8. **Limits called out** — only ~10–30% of coarse–fine difference predictable from these inputs; strong diurnal error cycle; demo ≠ full paper evaluation; power spectrum is a key diagnostic.

**Artifacts**
- Code: [weather-forecast-model-downscaler](https://github.com/EmmaScharfmann/weather-forecast-model-downscaler) (`tutorial_inference.ipynb`, `training_tutorial.ipynb`)
- Model: [EmmaScharfmann/france-temperature-downscaler](https://huggingface.co/EmmaScharfmann/france-temperature-downscaler)
- Demo Space: [downscaling-demo](https://huggingface.co/spaces/EmmaScharfmann/downscaling-demo)
- Stations dataset: [EmmaScharfmann/france-stations](https://huggingface.co/datasets/EmmaScharfmann/france-stations)
- Coarse AI models mentioned: [ecmwf/aifs-ens-1.0](https://huggingface.co/ecmwf/aifs-ens-1.0), [microsoft/aurora](https://huggingface.co/microsoft/aurora), [nvidia/atlas-era5](https://huggingface.co/nvidia/atlas-era5)

**Formal papers cited in the blog (4):**
- Lang et al. (2026) AIFS-CRPS [[DOI](https://doi.org/10.1038/s44387-026-00073-7)]
- Hersbach et al. (2020) ERA5 [[DOI](https://doi.org/10.1002/qj.3803)]
- Ridal et al. (2024) CERRA [[DOI](https://doi.org/10.1002/qj.4764)]
- Ferro (2014) Fair ensemble scores / CRPS [[DOI](https://doi.org/10.1002/qj.2270)]

Related (mentioned, not a formal ref): Google DeepMind [WeatherNext 3](https://blog.google/innovation-and-ai/models-and-research/google-deepmind/introducing-weathernext-3/) (~5 km surface T/q, closed).

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