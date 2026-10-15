# 🦍 Simulated Mountain Gorilla Movement Ecology & Intergroup Spatial Dynamics

**A Python-based geospatial workflow for movement metrics, home-range estimation, nest-site transitions, intergroup distances, and spatial-overlap analysis using synthetic GPS data.**

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-orange)
![Data](https://img.shields.io/badge/Data-100%25%20synthetic-purple)
![Project](https://img.shields.io/badge/Project-Movement%20ecology-lightgrey)

## Project Overview

This project demonstrates how spatial data can be used to study four movement-ecology questions in a mountain-gorilla-inspired scenario:

1. How far do simulated groups travel per day, and how variable are their paths?
2. What do Minimum Convex Polygon (MCP) and Kernel Density Estimation (KDE) estimates suggest about space use?
3. How far apart are groups at matched times, and how much do their simulated spatial distributions overlap?
4. How close are successive nest locations, and what can the current analysis say about intergroup separation?

**Important:** the repository is a methodological simulation. The results below describe its synthetic dataset and the current code outputs—not mountain gorilla field observations.

## ⚠️ Data Transparency

The dataset used in this project is **synthetic** and was created strictly for **educational, analytical, and portfolio purposes**. It does not represent real mountain gorilla GPS tracks, field observations, nest coordinates, group home ranges, or verified intergroup encounters.

The variable structure, movement context, group labels, and assumptions were informed by published scientific research on mountain gorillas and movement ecology. However, **all GPS fixes, movement paths, home-range estimates, overlap coefficients, close-approach counts, and statistical findings presented in this repository are generated from synthetic data and should not be interpreted as real-world findings**. Coordinates are illustrative simulation locations, not verified tracking records or group ranges.

This project demonstrates how location data could be analyzed in a comparable study. If an appropriately designed study used authorized real-world GPS observations from a relevant institution, similar analytical approaches could be adapted and independently validated. Any future use of real institutional or field data would require the appropriate **data-access permission, research authorization, and applicable ethical or regulatory approvals**.

## Dataset & Study Design

The notebooks report **105,143 rows and 14 columns**, representing six simulated groups over **365 days**. The analysis uses timestamps aligned to 10-minute bins and computes distance metrics between consecutive fixes and between groups at matching times.

| Simulated group label | Scenario group size | GPS fixes in home-range analysis |
|---|---:|---:|
| Amahoro | 17 | 17,523 |
| Hirwa | 13 | 17,518 |
| Kwitonda | 18 | 17,533 |
| Pablo | 24 | 17,535 |
| Susa | 28 | 17,529 |
| Umubano | 12 | 17,505 |
| **Total** | — | **105,143** |

Group sizes and labels are parameters in the synthetic scenario; they are not claims about actual group composition. The current workflow uses Python, pandas, NumPy, SciPy, GeoPandas, Shapely, Matplotlib, and Seaborn.

## Key Results — Simulated Outputs

### 1. Movement-step distribution

The movement notebook reports **102,953 valid steps** after calculating distances between consecutive fixes and excluding cross-day gaps greater than one hour from step, speed, and turning-angle metrics.

| Step-length statistic | Result |
|---|---:|
| Mean | 0.0277 km (27.7 m) |
| Standard deviation | 0.0211 km (21.1 m) |
| Median | 0.0224 km (22.4 m) |
| 25th percentile | 0.0116 km (11.6 m) |
| 75th percentile | 0.0385 km (38.5 m) |
| Maximum | 0.1691 km (169.1 m) |

**Interpretation:** the median simulated step is 22.4 m, while 75% of recorded step lengths are at or below 38.5 m. These are step lengths between successive simulated fixes, not a direct measure of continuous travel or biologically validated speed.

### 2. Daily path length by group

Each group has **365 daily summaries** in the saved movement-analysis output.

| Group | Mean km/day | Median km/day | SD km/day | CV | Minimum–maximum km/day |
|---|---:|---:|---:|---:|---:|
| Amahoro | 1.3207 | 1.3234 | 0.1370 | 0.1037 | 0.9822–1.6682 |
| Hirwa | 1.1823 | 1.1862 | 0.1265 | 0.1070 | 0.7745–1.7058 |
| Kwitonda | 1.2646 | 1.2594 | 0.1341 | 0.1060 | 0.9608–1.6841 |
| Pablo | 1.5139 | 1.5185 | 0.1620 | 0.1070 | 0.9273–1.9476 |
| Susa | 1.4251 | 1.4169 | 0.1528 | 0.1072 | 1.0044–1.8248 |
| Umubano | 1.1197 | 1.1179 | 0.1204 | 0.1075 | 0.8041–1.4529 |

The unweighted mean of the six group means is **1.3044 km/day**. Pablo has the highest reported mean (1.5139 km/day), and Umubano the lowest (1.1197 km/day). Within-group coefficients of variation range from **0.1037 to 0.1075**, indicating relatively low day-to-day variation in this synthetic dataset. These values do not establish real group-level movement patterns or explain why the groups differ.

### 3. Nest-site transition distances

| Metric | Reported result |
|---|---:|
| Mean distance between consecutive nest locations | 0.397 km (397 m) |
| Transitions within 500 m of the previous nest | 70.4% |

**Interpretation:** in the simulated trajectories, about seven in ten consecutive nest transitions are shorter than 500 m. This describes the synthetic nest-location pattern only; it does not validate a field-monitoring strategy or show that real groups can be relocated with the same success.

### 4. Home-range estimates: MCP versus KDE

The saved notebook reports both 95% and 50% MCP areas and KDE utilization-distribution areas.

| Group | MCP 95% km² | MCP 50% km² | KDE 95% km² | KDE 50% km² |
|---|---:|---:|---:|---:|
| Amahoro | 8.16 | 2.49 | 8.27 | 2.42 |
| Hirwa | 7.08 | 1.85 | 7.12 | 1.84 |
| Kwitonda | 9.60 | 3.03 | 9.32 | 2.59 |
| Pablo | 10.94 | 2.79 | 9.92 | 2.78 |
| Susa | 13.32 | 3.73 | 13.71 | 3.54 |
| Umubano | 8.44 | 2.52 | 8.10 | 2.31 |

KDE 95% areas range from **7.12 km² (Hirwa) to 13.71 km² (Susa)**. Susa also has the largest reported MCP 95% area (13.32 km²). The previous README's claim of 18–34 km² is inconsistent with this saved table and should not be retained.

MCP and KDE are different estimators: MCP summarizes a convex polygon around locations, whereas KDE estimates a spatial utilization distribution. Their estimates are not interchangeable. The current code uses a local flat-earth coordinate approximation and a distance-from-centroid filter for the nominal 95%/50% MCP subsets; these implementation choices should be validated before these values are treated as standardized home-range estimates.

### 5. Seasonal MCP summaries

The notebook's seasonal output reports the following 95% MCP ranges across the six simulated groups. Seasonal means below are calculated from the six group-specific results shown by the notebook.

| Simulated season | Mean 95% MCP across groups | Range across groups |
|---|---:|---:|
| Dry season | 8.60 km² | 6.57–12.60 km² |
| Long rains | 6.38 km² | 2.98–9.39 km² |
| Short rains | 4.95 km² | 3.01–6.95 km² |

These summaries describe variation built into or represented by the synthetic trajectories. The notebook does not establish that season causes the differences; formal group-by-season inference and uncertainty estimates would be needed for such a claim.

### 6. Intergroup distances

The intergroup notebook reports **257,564 timestamp-matched pairwise-distance records** covering all **15 unique pairs** among six groups. Daily minima yield **5,475 group-pair-by-day observations** (15 pairs × 365 days).

| Statistic for daily minimum intergroup distance | Result |
|---|---:|
| Mean | 4.5404 km |
| Median | 4.3001 km |
| Standard deviation | 1.9817 km |
| Minimum | 0.0169 km |
| Maximum | 11.2555 km |

The mean daily minimum distance matrix reports the smallest pairwise mean for **Amahoro–Pablo (1.75 km)** and the largest for **Kwitonda–Umubano (7.85 km)**. These are averages of each pair's daily minimum distance, not straight-line distances between fixed group-centre coordinates.

### 7. Spatial distribution overlap

The notebook estimates spatial overlap with a KDE-based Bhattacharyya coefficient (BC), where **0 indicates little or no distributional overlap and 1 indicates identical estimated distributions**.

| Group pair | Reported BC |
|---|---:|
| Amahoro–Pablo | 0.835 |
| Susa–Umubano | 0.623 |
| Kwitonda–Pablo | 0.505 |
| Hirwa–Umubano | 0.438 |
| Amahoro–Hirwa | 0.306 |
| Hirwa–Kwitonda | 0.000 |
| Susa–Pablo | 0.000 |

The strongest non-self overlap in the reported matrix is Amahoro–Pablo (0.835); several pairs round to 0.000 at three decimal places. These coefficients depend on the synthetic coordinates, KDE settings, and grid approximation. A reported zero should be read as zero at the displayed precision, not proof of a true ecological boundary.

### 8. Close-approach observations below 500 m

The current function counts timestamp-level records with pairwise distance below 0.5 km. The saved output reports:

| Simulated group pair | Records below 500 m | Reported rate/day |
|---|---:|---:|
| Amahoro–Pablo | 488 | 1.3370 |
| Kwitonda–Pablo | 112 | 0.3068 |

These are close-approach **observations**, not necessarily independent encounter events: repeated fixes during one close approach can be counted multiple times. Therefore, the current counts do not independently confirm avoidance, conflict, or encounter frequency in a biological sense.

### 9. Intergroup hypothesis test — current output requires correction

The README previously stated that groups actively avoid one another, reporting **p < 0.001** and **Cohen's d = 2.05**. Those values do not match the saved hypothesis-testing notebook. The notebook currently reports:

| Quantity | Saved output |
|---|---:|
| Observed mean daily minimum distance | 4.5404 km |
| Null mean | 5.9586 km |
| Difference (observed − null) | −1.4182 km |
| Permutation replicates | 10,000 |
| One-sided permutation p-value | 0.915200 |
| One-sample t-test | t = −52.9480, p = 1.000000 |
| Mann–Whitney U test | U = 14,220,062, p = 1.000000 |
| Shapiro–Wilk normality test | W = 0.9865, p printed as 0.000000 |
| Cohen's d | −0.8994 |

**Interpretation:** the saved output does **not** support the README's former claim that active avoidance was statistically confirmed. More importantly, these test outputs should not be treated as valid inference yet: the observed values are *daily minimum distances for group pairs*, while each null replicate currently calculates the *mean of all pairwise distances among six randomly sampled locations*. These are different statistics, so the comparison is not like-for-like. The code also applies t-test and Mann–Whitney procedures to inputs that do not share the same sampling unit. The p-values and effect size are documented here to make the current state reproducible, not as evidence for or against real-world gorilla behavior.

A valid analysis should calculate the same prespecified statistic for the observed data and every null replicate, preserve relevant temporal and spatial structure, and then report an appropriately corrected permutation p-value with an effect estimate and uncertainty interval.

## Core Formulas

### Great-circle distance (Haversine)

For two latitude/longitude locations, with angles in radians:

$$
a=\sin^2\left(\frac{\Delta\phi}{2}\right)+\cos(\phi_1)\cos(\phi_2)\sin^2\left(\frac{\Delta\lambda}{2}\right)
$$

$$
d=2R\,\operatorname{atan2}\left(\sqrt{a},\sqrt{1-a}\right),\qquad R=6371\text{ km}
$$

### Daily path length, speed, and coefficient of variation

$$
\mathrm{DPL}_{g,d}=\sum_{t=2}^{T_{g,d}} d_{g,t},\qquad v_{g,t}=\frac{d_{g,t}}{\Delta t}
$$

$$
\mathrm{CV}_g=\frac{s_g}{\overline{\mathrm{DPL}}_g}
$$

Here, $d_{g,t}$ is the distance between consecutive fixes, $\Delta t$ is elapsed time, and $s_g$ is the standard deviation of a group's daily path lengths. The saved daily CV estimates range from 0.1037 to 0.1075.

### Nest-to-nest distance and daily minimum separation

$$
N_{g,d}=d\left(\mathbf{x}^{\mathrm{nest}}_{g,d},\mathbf{x}^{\mathrm{nest}}_{g,d-1}\right)
$$

$$
D_{ab,d}=\min_{t\in d} d\left(\mathbf{x}_{a,t},\mathbf{x}_{b,t}\right)
$$

The second expression describes the daily minimum distance between groups $a$ and $b$ over matched timestamps on day $d$.

### MCP and KDE home-range area

$$
A_{\mathrm{MCP}}=\operatorname{Area}\left(\operatorname{ConvHull}\{(x_i,y_i)\}\right)
$$

For KDE, the $p$% utilization region $R_p$ is the highest-density region containing $p$% of estimated utilization probability; its area is $A_p=\int_{R_p}dA$. The current implementation approximates these calculations on a grid and uses a local coordinate conversion, so the resulting estimates should be interpreted as outputs of this implementation rather than definitive ecological home ranges.

### Bhattacharyya coefficient for spatial overlap

$$
BC(P,Q)=\int\sqrt{p(\mathbf{x})q(\mathbf{x})}\,d\mathbf{x}\ \approx\ \sum_i\sqrt{p_iq_i}
$$

The current notebook normalizes the two gridded KDE surfaces before calculating this coefficient. Reported overlap ranges from 0.000 to 0.835 for the highlighted pairs.

### Cohen's $d$ and a matched permutation test

The current code calculates a standardized mean difference as:

$$
d=\frac{\bar{x}-\bar{y}}{\sqrt{(s_x^2+s_y^2)/2}}
$$

Its reported value is $d=-0.8994$, but it should not be interpreted until the observed and null statistics are defined on the same scale and sampling unit. For a corrected one-sided Monte Carlo permutation test, use the same statistic $T$ in both the observed data and each of $B$ permutations, for example:

$$
\hat{p}=\frac{1+\sum_{b=1}^{B} I(T_b\geq T_{\mathrm{obs}})}{B+1}
$$

The formula above is a recommended corrected-test convention; it is **not** the exact formula currently implemented in the notebook.

## Workflow & Repository

1. `notebooks/01_data_loading_exploration.ipynb` — data loading and exploratory checks.
2. `notebooks/02_movement_analysis.ipynb` — step metrics, daily path lengths, and nest transitions.
3. `notebooks/03_home_range_estimation.ipynb` — MCP/KDE and seasonal estimates.
4. `notebooks/04_intergroup_dynamics.ipynb` — pairwise distances, daily minima, overlap, and close-approach observations.
5. `notebooks/05_hypothesis_testing.ipynb` — null model and statistical tests.
6. `notebooks/06_final_visualizations.ipynb` — combined reporting visualizations.

Core functions are located in `src/movement_metrics.py`, `src/home_range.py`, `src/intergroup_analysis.py`, and `src/visualization.py`. Summary outputs are written under `data/processed/` and `outputs/reports/`; figures are written under `outputs/figures/` when the relevant notebooks are executed.

## Limitations & Reproducibility Priorities

- All observations and findings are synthetic; none should be used to infer actual group movement or conservation outcomes.
- The current intergroup null model compares different statistics with the observed data. Rebuild the test before claiming active avoidance.
- The 500 m function counts repeated timestamp-level proximity records, not distinct encounter episodes.
- MCP/KDE calculations use an approximate local coordinate conversion; the MCP percentile filter and KDE grid estimator require validation against standard geospatial home-range workflows.
- The notebooks expect `data/raw/gorilla_gps_data.csv` or a callable `data_generator.py`. Ensure the synthetic generator, random seed, and required input data are committed and documented so a clean clone can reproduce the saved outputs.
- Re-run the notebooks end-to-end after code changes, regenerate result tables and figures, and update this README from the new outputs.

## References

1. Seaman, D. E., & Powell, R. A. (1996). An evaluation of the accuracy of kernel density estimators for home range analysis. *Ecology*, 77(7), 2075–2085. [https://doi.org/10.2307/2265701](https://doi.org/10.2307/2265701)
2. Robbins, M. M., & Sawyer, S. C. (2007). Intergroup encounters in mountain gorillas of Bwindi Impenetrable National Park, Uganda. *Behaviour*, 144(12), 1497–1519. [https://doi.org/10.1163/156853907782512146](https://doi.org/10.1163/156853907782512146)
3. Grueter, C. C., Ndamiyabo, F., Plumptre, A. J., Abavandimwe, D., Mundry, R., Fawcett, K. A., & Robbins, M. M. (2013). Long-term temporal and spatial dynamics of food availability for endangered mountain gorillas in Volcanoes National Park, Rwanda. *American Journal of Primatology*, 75(3), 267–280.
4. Nathan, R., Getz, W. M., Revilla, E., Holyoak, M., Kadmon, R., Saltz, D., & Smouse, P. E. (2008). A movement ecology paradigm for unifying organismal movement research. *Proceedings of the National Academy of Sciences*, 105(49), 19052–19059. [https://doi.org/10.1073/pnas.0800375105](https://doi.org/10.1073/pnas.0800375105)

## Author

**Bruno Rudahongerwa Rwarahoze**  
Former Data Entry Intern at the Dian Fossey Gorilla Fund (DFGF)
