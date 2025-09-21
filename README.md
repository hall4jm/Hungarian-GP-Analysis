# Hungarian GP 2022 — Strategy & Pace Analysis
*Ferrari vs. Max Verstappen at the Hungaroring*

This repository contains a race-analysis notebook that dissects the **2022 Hungarian Grand Prix** through lap‑by‑lap telemetry and strategy reconstruction. The goal is to separate **pure pace** from **strategy choices** (tire compound, pit timing, and traffic) and explain how a likely Ferrari victory unraveled.

> **TL;DR:** Ferrari had competitive pace in phases of the race, but a **hard-tyre switch around Lap 40** derailed the strategy. Meanwhile, Verstappen executed a **soft → medium** plan with strong in/out-laps and racecraft that overcame setbacks.

---

## What this project demonstrates (for hiring managers)
- **Causal instincts:** distinguishes where time was lost to *strategy* vs *pace* vs *traffic*.
- **Feature engineering:** turns raw timing and tire logs into stint, compound-age, and gap features.
- **Clear communication:** annotated visuals (gap evolution, tire timelines) that support a crisp, defensible story.
- **Reproducibility:** FastF1 cache, deterministic preprocessing, and figures exported to `images/`.

---

## Repository structure
```
.
├─ F1Analysis.ipynb        # Main analysis notebook
├─ images/                 # Exported figures (tyre timeline, gap evolution, etc.)
└─ cache/                  # FastF1 on-disk cache (auto-created on first run)
```
> The notebook also references illustrative images such as `images/Tyre Compound.PNG` (qualifying/start compounds) and a meme image used in the intro.

---

## Data & Tools
- **Data source:** [FastF1](https://theoehrly.github.io/Fast-F1/) timing + telemetry for the **2022 Hungarian GP (Race)**.
- **Key entities:** driver lap times, tyre compound & age, pit events, stint segmentation.
- **Libraries:** `fastf1`, `pandas`, `matplotlib`, `seaborn`.

---

## Analytical questions
1. **Start/qualifying tyre positions:** Who started on which compound and why did that matter at the Hungaroring?
2. **Stint‑by‑stint pace:** How did Ferrari’s clean‑air pace compare to Verstappen on each compound?
3. **Pit windows & under/overcut risk:** Where were the profitable laps to stop given degradation patterns?
4. **Cumulative time accounting:** When did the gap bend most (in‑laps, out‑laps, traffic, compound choice)?
5. **Counterfactual:** Would avoiding the **hard** tyre have kept Ferrari ahead?

---

## What the notebook shows (highlights)
- **Start & tyre mix:** 2022 regs allowed divergent tyre choices; Ferrari started on **mediums** while rivals chose mixes that enabled flexible strategies. See `images/Tyre Compound.PNG` for a grid‑level view.
- **Early race:** Verstappen’s pace and clear racecraft let him carve forward despite starting behind Ferrari and Mercedes, setting up a **soft → medium** path.
- **Ferrari pit sequence:** An attempted **overcut** with Sainz failed to deliver durable track position; **Leclerc overtook Verstappen on Lap ~31** and built a margin.
- **Critical decision:** Around **Lap ~40**, Ferrari boxed Leclerc for **hards**—a compound that proved slow to warm and off‑pace in race conditions.
- **Gap evolution:** The **cumulative gap plot** (“Ferrari’s Lost Victory”) shows the lead flipping after the hard‑tyre stop; even with Verstappen’s errors (e.g., a spin), the superior compound strategy and execution prevailed.

> Exact numeric deltas (e.g., median stint pace or undercut seconds) depend on your local re‑run. The notebook renders the annotated gap figure and tyre timeline used to support the narrative.

---

## Figures (as referenced in the notebook)
- **Tyre usage timeline / grid compounds** — `images/Tyre Compound.PNG`
- **Cumulative time gap vs. Verstappen** — built from a `gap_df` and annotated around **Lap 40** (strategy change)
- *(Optional)* Stint box/violin plots and in/out‑lap callouts if you export them to `images/`

You can embed these in this README for quick viewing:
```html
<p align="center">
  <img src="./images/Tyre Compound.PNG" width="520" alt="Starting tyre compounds (Top 10)"/>
</p>
```

---

## How to run
### 1) Environment
```bash
python -m venv .venv && source .venv/bin/activate  # (or use conda)
pip install fastf1 pandas matplotlib seaborn
```

### 2) Cache & data
The first run downloads timing/telemetry to `./cache/`:
```python
import fastf1 as f1
f1.Cache.enable_cache('cache')
```

### 3) Execute the analysis
Open the notebook and **Run All**:
```bash
jupyter lab F1Analysis.ipynb
# or
jupyter notebook F1Analysis.ipynb
```

---

## Results summary (edit with your run’s numbers)
- **Clean‑air stint pace:** Ferrari vs. Verstappen per compound (median ± IQR).
- **Undercut/overcut realized:** seconds gained/lost at each stop.
- **Key inflection laps:** e.g., **Lap ~31** (Leclerc pass), **Lap ~40** (hard‑tyre stop), with notes on traffic and out‑laps.
- **Takeaway:** Avoiding the **hard** tyre and mirroring a **M→M** or **M→S** path likely preserves track position given observed degradation.

Keep this section tight (3–5 bullets) and cite figures from `images/`.

---

## Assumptions & limitations
- **Degradation model** is empirical from lap deltas; not a physics sim.
- **Safety Car/VSC** effects are treated descriptively; no probabilistic sim.
- **Telemetry gaps** or atypical laps are filtered when computing stint summaries.

---

## Portfolio polish & roadmap
To elevate this into a *case‑study grade* project, consider:
1. **Back‑testing “what‑if”s:** a simple Monte Carlo sim sampling tyre warm‑up, pit loss, and degradation to produce a distribution of race‑time outcomes for each strategy path.
2. **Causal framing:** estimate treatment effect of tyre choice on lap time via Bayesian hierarchical modeling across stints (control for tyre age and track evolution).
3. **Packaging:** extract data/feature/plot logic into a small `race_sim` Python package + CLI (with unit tests) for other races.
4. **Interactive app:** Streamlit demo where a user toggles pit laps/compounds and sees predicted outcome ranges.

---

## Attribution
- Built with **FastF1** and publicly available 2022 Hungarian GP race timing/telemetry.
- Respect series data rights when sharing figures.

---

### Project tagline (for the repo header)
> **“Ferrari’s Lost Victory: how a Lap‑40 hard‑tyre call flipped the 2022 Hungarian GP.”**
