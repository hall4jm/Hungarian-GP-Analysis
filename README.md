# Hungarian GP Strategy Analysis
*Ferrari vs. Max Verstappen — strategy, pace, and pit windows at the Hungaroring*

> This project investigates Ferrari’s race strategy in response to Max Verstappen at the Hungarian Grand Prix, using lap-by-lap telemetry to understand where time was gained/lost and how tire choices and pit timing shaped the result. :contentReference[oaicite:0]{index=0}

---

## Why this project matters
- **Product thinking:** frames a real racing question (“Did strategy, pace, or traffic cost more?”) and answers it with measurable evidence.
- **Causality instincts:** distinguishes *pace deltas* from *strategy effects* (undercut/overcut risk, tire degradation).
- **Tech breadth:** data ingestion from an external API (FastF1), feature engineering, visualization, scenario analysis, and reproducibility.
- **Communication:** turns raw telemetry into clear, decision-ready visuals (in `images/`) suitable for briefings. :contentReference[oaicite:1]

---

## Repository structure

├─ F1Analysis.ipynb # Main analysis notebook
├─ images/ # Exported figures used in the write-up
├─ Cache/ # FastF1 on-disk cache to speed up data access
└─ README.md # You are here

*Folders/files based on the repo listing.* :contentReference[oaicite:2]{index=2}

---

## Key questions
1. **Where did Ferrari gain/lose time vs. Verstappen?** (clean air vs. traffic, in-/out-laps, tire phase)
2. **How much did pit timing and tire choice matter?** (undercut/overcut windows, degradation)
3. **What alternative strategies plausibly out-perform what was used?** (counterfactuals)

---

## Methods
- **Data source:** FastF1 timing/telemetry and session info (laps, compounds, stints, pit stops, weather).
- **Feature engineering:** per-lap pace deltas, stint segmentation, in/out-lap tags, compound & age features, simple traffic/clean-air flags.
- **Visualization:** lap-time delta traces, stint box/violin plots, tire usage timelines, cumulative gap curves, and undercut “windows”.
- **Scenario analysis:** “what-if” pit calls within realistic windows and degradation assumptions (illustrative).
- **Reproducibility:** uses an on-disk cache (`Cache/`) and exports figures to `images/` for portability. :contentReference[oaicite:3]{index=3}

---

## Executive summary
- **Baseline pace:** Summarize Ferrari vs. Verstappen median pace by stint and compound.
- **Strategy impact:** Quantify the **undercut/overcut** realized at each stop (e.g., “+2.3s net gain from earlier stop on Lap 17”).
- **Decisive moments:** Point to the laps/segments where the cumulative gap bent the most (e.g., pit in/out, traffic clusters).
- **Counterfactual:** One recommended alternative (e.g., delay stop by X laps to avoid traffic, or avoid the hard compound) and the modeled time delta.
---

## Results highlights (figure guide)
- **Lap-by-lap delta chart:** Shows rolling gap vs. Verstappen with pit windows marked.
- **Stint comparison:** Box/violin plots of Ferrari vs. Verstappen by compound & stint age.
- **Tire usage timeline:** Compound choices across the field and Ferrari/Verstappen alignment.
- **Undercut windows:** Visual band of laps where pitting is advantageous given degradation assumptions.
- **Cumulative time lost to traffic:** Heatmap or table attributing loss to traffic vs. tire phase vs. pit execution.