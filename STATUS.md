# STATUS — awesome-earth-downscaling

**Updated:** 2026-11-25 (Asia/Shanghai)

## First-fill method
- Gemini/agy capacity was saturated; first content authored via lightweight WebSearch + WebFetch + `gh` repo search (quota-conscious).
- All arXiv abs / GitHub / NVIDIA docs links in README were checked reachable (HTTP 200) where noted in the fill session.
- Prefer verified links; omit rather than invent.

## Coverage
- Strong: NVIDIA Earth-2 / CorrDiff, diffusion downscaling, DeepSD, surveys, common toolkits/datasets.
- Partial: hydrology-specific methods (starter set); classical SDSM literature pointers are high-level.
- Gaps / TODO:
  - Expand 2025–2026 arXiv sweep when export.arxiv.org rate limits ease
  - Add more hydro runoff / flood-oriented DL downscaling papers with verified code
  - Link official SDSM / ClimDown paper DOIs in classical section
  - Optional: bibtex export from papers.json
  - Track arXiv ID for SIMOGroup/CorrFlow when published (repo pushed 2026-11-09; title still has no matching arXiv)
  - Optional backlog (predate this sweep; not added): CORDEX-ML-Bench [[arXiv:2606.29172](https://arxiv.org/abs/2606.29172)]; China 3 km CorrDiff [[arXiv:2512.05377](https://arxiv.org/abs/2512.05377)]; analog-initialized latent transport km-scale downscaling [[arXiv:2610.03736](https://arxiv.org/abs/2610.03736)]; CEDDAR precip diffusion [[DOI](https://doi.org/10.5194/egusphere-2026-1139)] [[code](https://github.com/TheaQG/CEDDAR)] (EGUsphere discussion started 2026-03-09; no arXiv); scale-adaptive joint spatiotemporal SR [[arXiv:2604.21903](https://arxiv.org/abs/2604.21903)] [[code](https://github.com/mdefez/Precipitation_Dowscaling)] (v1 April 2026; v2 2026-11-19)

## Update routine
Every ~3 days: search new arXiv/GitHub hits for weather/climate/hydro downscaling + Earth-2/CorrDiff; merge verified entries into README + data/papers.json; push if changed.

## 2026-11-25 — Incremental sweep (post 2026-11-22)
Added **2** verified papers (abs HTTP 200; MUNDO code HTTP 200):
- Beyond Resolution (inference-time parameterized temporal consistency) [[arXiv:2611.27641](https://arxiv.org/abs/2611.27641)] — noise-conditioned teacher-forcing on a diffusion U-Net GCM→RCM downscaler; one inference noise parameter interpolates between autoregressive and per-timestep independent sampling. Hourly Europe AWI-CM1 (1°) → ICON (0.11°, regridded to 0.25°) for precipitation and T2m; AR rollouts up to six months show no progressive degradation, and AR better preserves daily precip maxima. Authors state code will be released upon publication; no public repo verified this run.
- MUNDO [[arXiv:2611.30868](https://arxiv.org/abs/2611.30868)] + [code](https://github.com/dataymeric/mundo) — multiresolution generative temporal downscaling with a null-space parameterization that enforces exact observation consistency in one network evaluation (interpolation and disaggregation). Evaluated on Lorenz-96, 2D physical systems, and multivariate ERA5 over Europe.

No new Earth2Studio stable release after v1.0.0 (1.1.0a0 is unreleased). CorrFlow still has no verified arXiv ID (2610.24750 is a different CorrFlow paper). Left on the optional backlog (older than this window): CEDDAR [[DOI](https://doi.org/10.5194/egusphere-2026-1139)] + [code](https://github.com/TheaQG/CEDDAR) (EGUsphere 2026-03-09; no arXiv); scale-adaptive joint spatiotemporal SR [[arXiv:2604.21903](https://arxiv.org/abs/2604.21903)] (v1 April 2026; v2 2026-11-19) + [code](https://github.com/mdefez/Precipitation_Dowscaling). Method: lightweight arXiv API + WebSearch + HTTP checks (agy not used this run).

## 2026-11-22 — Incremental sweep (post 2026-11-16)
Added **1** verified paper (abs + code HTTP 200) and noted Earth2Studio **v1.0.0**:
- PC-RF (Physics-Constrained Rectified Flow) [[arXiv:2611.22283](https://arxiv.org/abs/2611.22283)] [[AIAS+ 2026]] + [code](https://github.com/arunshar/pc-rf) — conditional rectified-flow climate downscaler with physics penalties and an inference projection (non-negativity + domain-mean mass) on ERA5. The paper reports the projection certifies NVR/MCE; penalties add no separable perceptual gain vs RF-base. Code README documents known issues (wrong ERA5 divergence operator; no included checkpoints).
- Earth2Studio **v1.0.0** ([release 2026-11-18 22:01 UTC](https://github.com/NVIDIA/earth2studio/releases/tag/1.0.0); PyPI 1.0.0) — general release with breaking xarray interfaces; CorrDiff ERA5-HRRR is `DomainAdaptable` (`with_region` subdomain inference). Existing CorrDiffEra5Hrrr / CorrDiff CMIP6→ERA5 source and docs links still HTTP 200.

The 2026-11-19 scheduled run did not land a commit; this sweep covers 2026-11-16–11-22. CorrFlow still has no verified arXiv ID. Skipped as out of scope or not a statistical downscaling methods paper: MAGIC GRACE DA [[arXiv:2611.15421](https://arxiv.org/abs/2611.15421)] (already skipped 11-16); PARDIG precipitation estimation [[arXiv:2611.13941](https://arxiv.org/abs/2611.13941)]; PECAN distributed hydrologic modeling [[arXiv:2611.13346](https://arxiv.org/abs/2611.13346)]; One2N recursive forecast-resolution refinement [[arXiv:2611.12249](https://arxiv.org/abs/2611.12249)] (submitted 2026-11-09; forecasting, not listed here); CV/video uses of the word “downscaling”. Method: lightweight arXiv API + GitHub/PyPI/docs HTTP checks (agy not used this run).

## 2026-11-16 — Incremental sweep (post 2026-11-13)
Added **1** verified paper (abs HTTP 200):
- Hybrid ML-analog downscaling of unprecedented climate extremes [[arXiv:2611.15284](https://arxiv.org/abs/2611.15284)] — EnScale generative RCM emulation + analog matching for GCM ensemble-boosted heatwaves (Paris / Western Europe). Related EnScale method [[arXiv:2509.26258](https://arxiv.org/abs/2509.26258)] [[code](https://github.com/m-schillinger/enscale)] (HTTP 200) is cited in the note; not added as a separate historical entry this run.

No new Earth2Studio release after v0.20.0; CorrFlow still has no verified arXiv ID. Skipped as out of scope or unverified as a methods paper: MAGIC GRACE DA [[arXiv:2611.15421](https://arxiv.org/abs/2611.15421)]; CARM EO SR risk masks [[arXiv:2611.06151](https://arxiv.org/abs/2611.06151)]; RATSIFT solar temporal downscaling [[arXiv:2611.03738](https://arxiv.org/abs/2611.03738)]; GitHub-only IGARSS 2027 TWS downscaling [granger-prior-tws-downscaling](https://github.com/BOUTAYEBAnasse/granger-prior-tws-downscaling) (no arXiv/DOI yet). Method: lightweight arXiv API + GitHub search + HTTP checks (agy not used this run).

## 2026-11-13 — Incremental sweep (post 2026-11-10)
Added **2** verified papers (all abs/GitHub HTTP 200):
- PROLA [[arXiv:2611.11318](https://arxiv.org/abs/2611.11318)] [[NeurIPS 2026]] + [code](https://github.com/yms020615/PROLA) — predictive spatiotemporal weather downscaling (PEFT)
- Spatially varying quantile downscaling of Spain summer Tmax [[arXiv:2611.12677](https://arxiv.org/abs/2611.12677)]

No new Earth2Studio release after v0.20.0; CorrFlow still has no verified arXiv ID. Method: lightweight arXiv API + GitHub search + HTTP checks (agy not used this run).

## 2026-11-10 — Incremental sweep (post 2026-11-07)
Added **4** verified late-Oct 2026 papers (missed in the 11-07 sweep; all abs/GitHub/DOI HTTP 200) and official Earth2Studio CorrDiff model links:
- Operator-Aware Posterior Sampling [[arXiv:2610.39592](https://arxiv.org/abs/2610.39592)] + [code](https://github.com/CarloSaccardi/operator-aware-weather-downscaling)
- CD-FFM likelihood functional flow matching [[arXiv:2610.33482](https://arxiv.org/abs/2610.33482)] + [code](https://github.com/Holmes-Alan/CD-FFM)
- Spherical Physics-informed Neural Operator [[arXiv:2610.24708](https://arxiv.org/abs/2610.24708)] [[DOI](https://doi.org/10.24963/ijcai.2026/734)] (IJCAI 2026)
- ERA5→IMERG daily precip over West Africa [[arXiv:2610.16816](https://arxiv.org/abs/2610.16816)]
- Earth2Studio v0.20.0 (2026-10-29): [CorrDiffEra5Hrrr](https://nvidia.github.io/earth2studio/main/modules/generated/models/dx/CorrDiffEra5Hrrr/) (distilled ERA5→3 km HRRR) and [CorrDiff CMIP6→ERA5](https://huggingface.co/nvidia/corrdiff-cmip6-era5)

No core weather/hydro downscaling papers with new arXiv IDs announced 2026-11-07–11-10 were found (2611.03925 is a TC dataset, not a downscaling method). Method: lightweight arXiv API + WebSearch + HTTP checks (agy not used this run).

## 2026-11-07 — Incremental sweep (post 2026-11-05)
Added **7** verified entries (all abs/GitHub HTTP 200):
- PrecipCorrDiff [[arXiv:2610.19994](https://arxiv.org/abs/2610.19994)] — CorrDiff-style IMD precip
- SwAIther-Precip [[arXiv:2605.16163](https://arxiv.org/abs/2605.16163)] — AIFS→km Switzerland precip
- CPMGEM-hourly [[arXiv:2610.26145](https://arxiv.org/abs/2610.26145)] — video diffusion hourly precip
- Foundation-conditioned precip diffusion [[arXiv:2608.25858](https://arxiv.org/abs/2608.25858)] — Prithvi WxC
- Flow matching convective-scale precip [[arXiv:2606.00281](https://arxiv.org/abs/2606.00281)] + [mo-flow-sg](https://github.com/mo-tomaswetherell/mo-flow-sg)
- CorrFlow residual flow matching [[SIMOGroup/CorrFlow](https://github.com/SIMOGroup/CorrFlow)] (no arXiv yet)
- Multivariate monthly→daily diffusion [[arXiv:2610.19885](https://arxiv.org/abs/2610.19885)]

Method: lightweight WebSearch + arXiv/GitHub HTTP checks (agy not used this run).

## 2026-11-05 — Milan Janosov RS downscaling list
Imported all **12/12** spatial-downscaling items from [Milan’s Substack](https://milanjanosov.substack.com/p/10-papers-and-resources-on-spatial) / [X](https://x.com/milan_janosov/status/2112440683835310405) into README section *Remote Sensing Spatial Downscaling* +  (DOI/arXiv/GitHub verified; LinkedIn shortlinks resolved via titles).

## 2026-11-05 — HF AIFS downscaler blog
Extracted **4 formal papers** from References + compressed tutorial (U-Net residual ensemble, ERA5→CERRA, fair CRPS) into README *Tutorials* section; linked code/model/demo/stations. WeatherNext 3 noted as related mention only.