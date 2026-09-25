```text

Dataset: mouse-app-lecanemab-ki3-aggregated, derivatives/spimquant-v0.9.0_lantern only.

Background:
Regions with more plaque lose more plaque to Lecanemab in ABSOLUTE terms — expected if the drug removes the same PROPORTION everywhere.

Question:
Does the PROPORTIONAL reduction differ across brain regions, beyond what baseline burden predicts?

Future extensions (not now — data not available in this run):
- Why would the proportion differ? Vessel proximity (vesseldist exists for only 3/36 mice) or microglia (Iba1 not segmented, raw micr/ only). Both need re-processing.

Data setup:
- Per-subject tabular/*seg-coarse*mergedsegstats, concatenated, joined to
  bids/participants.tsv on participant_id.
- Keep PBS (n=16) and Lecanemab (n=16) only; drop WT/control mice.
- Metric: Abeta+fieldfrac (repeat with Abeta+density). Ignore count, nvoxels, volume, vesseldist.
- Carry batch, sex, and QC_notes through for plotting.

Exploration:
1. Control baseline per region:
   - Per-region plot of PBS values (bar = mean, dots = individual mice),
     coloured by batch, QC-flagged mice marked.
   - Report per-region CV across PBS mice (how precisely each baseline is known).
2. Treatment effect per region:
   - Per-region log ratio = log(mean Lecanemab / mean PBS), with 95% CI from bootstrapping mice within each group.
   - Scatter: log ratio (y) vs PBS mean burden (x), one point per region.
     Flat band = uniform proportional effect; slope/outliers =  region-specific.
   - Flag regions with very low PBS burden (ratio unstable).

No hypothesis tests yet — descriptive only.

```