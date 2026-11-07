# STATUS — awesome-earth-downscaling

**Updated:** 2026-11-07 (Asia/Shanghai)

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

## 2026-11-07 — Seven requested sources (direct vs related)

Collected as **5 papers + 1 NVIDIA official example + 1 toolkit**, not seven papers. Used the attached verification brief only; no extra literature sweep. Date: 2026-11-07 (Asia/Shanghai).

**Direct weather downscaling**
- Enriched in place: **Precipitation Downscaling Using Foundation Model-Conditioned Diffusion** [[arXiv:2608.25858](https://arxiv.org/abs/2608.25858)] (README + `data/papers.json`). `code_url` stays empty; no checkpoint was inferred.
- Added: **Earth observation embeddings are effective subgrid descriptors for probabilistic weather downscaling** [[arXiv:2608.12271](https://arxiv.org/abs/2608.12271)]. 10 m is the Tessera embedding resolution, not the weather grid. Cited code was not inspected.

**Enriched, not duplicated**
- **NVIDIA Earth2Studio** — updated the existing Earth-2 entry and the Libraries cross-listing (docs, unified API, breaking 1.0.0 note, toolkit-not-paper). No third README listing. Added one `papers.json` record because the toolkit was absent there; `year` is `null` (no publication date established).

**Related enabling work** (new subsection; not labeled as downscaling results)
- **MoWE** — PhysicsNeMo documentation example for forecast fusion [[docs](https://docs.nvidia.com/physicsnemo/latest/physicsnemo/examples/weather/mixture_of_experts/readme.html)]. Not a paper; no checkpoint invented.
- **ESFM** — heterogeneous-input forecasting [[arXiv:2605.00850](https://arxiv.org/abs/2605.00850)]. Year only (20 Apr vs 5 May 2026 headings differ).
- **Any2Any** — modality translation. Official page is the [ICML 2026 poster](https://icml.cc/virtual/2026/poster/66068), not the PMLR homepage; arXiv [2603.04114](https://arxiv.org/abs/2603.04114).
- **Geospatial Foundation Embeddings as Transferable Catchment Descriptors** — rainfall–runoff transfer [[DOI](https://doi.org/10.1029/2026GL122814)]. Identity and indexed abstract corroborated; publisher body not read (DOI timeout, publisher HTTP 400). **Not fully primary-page verified.** Indexed Zenodo `10.5281/zenodo.19157884` was not fetched, so code/data availability is not claimed. Author line keeps Shen, C. (given name not established).

Cited code URLs for ESFM, Any2Any, and the Tessera downscaling repo are recorded as citations only.

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