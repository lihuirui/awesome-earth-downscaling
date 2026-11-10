# STATUS — awesome-earth-downscaling

**Updated:** 2026-11-10 (Asia/Shanghai)

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
  - Track arXiv ID for SIMOGroup/CorrFlow when published

## Update routine
Every ~3 days: search new arXiv/GitHub hits for weather/climate/hydro downscaling + Earth-2/CorrDiff; merge verified entries into README + data/papers.json; push if changed.

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