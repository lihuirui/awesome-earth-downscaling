# STATUS — awesome-earth-downscaling

**Updated:** 2026-11-05 (Asia/Shanghai)

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

## Update routine
Every ~3 days: search new arXiv/GitHub hits for weather/climate/hydro downscaling + Earth-2/CorrDiff; merge verified entries into README + data/papers.json; push if changed.
