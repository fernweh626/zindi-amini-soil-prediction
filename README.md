# Amini Soil Prediction Challenge — Turning Soil Models into Fertiliser Decisions

> **My role:** Competitions Lead at [Zindi](https://zindi.world) (April 2019 – November 2025). I owned this competition as a product and was the partner manager for the Amini relationship, which I led across 5 challenges.
> **Competition page:** https://zindi.world/competitions/amini-soil-prediction-challenge
> **Data (not redistributed here):** https://zindi.world/competitions/amini-soil-prediction-challenge/data
> **Winning solution (I published it on Zindi):** https://zindi.world/learn/first-place-solution-amini-soil-prediction-a-hundred-heads-are-better-than-one

## The problem
Soil health drives yield and food security, but lab soil analysis is slow and expensive. Participants built a model that predicts **11 soil nutrients** (N, P, K, Ca, Mg, S, Fe, Mn, Zn, Cu, B) from soil and environmental data collected on African farms in 2019, then used those predictions to calculate each nutrient's **gap** for maize to reach a target yield of **4 tonnes per hectare**. That supports scalable, lower-cost soil analysis and more precise fertiliser recommendations.

- **Partner:** [Amini](https://amini.ai), a deep-tech data-solutions company working across the Global South
- **Evaluation metric:** Root Mean Squared Error (RMSE) on the nutrient gap

## Product thinking
**The key design choice: score the decision, not the prediction.** A soil model that predicts parts-per-million is useful to a data scientist but not to a farmer. The challenge turns the model's output into an agronomic action by converting ppm to kg/ha and comparing it against what a 4 t/ha maize crop requires:

```
Available (kg/ha) = ppm × soil depth (cm) × bulk density (g/cm³) × 0.1
Required  (kg/ha) = nutrient uptake per tonne × 4 t/ha
Gap       (kg/ha) = Required − Available
```
A positive gap means the farmer needs to add that nutrient. A negative gap means there is already an excess. Ranking participants on the gap means the leaderboard measures what matters in the field.

**Users:** (1) data scientists on Zindi; (2) Amini and, downstream, the farmers and agronomists who act on nutrient recommendations.

**Participant enablement:** a beginner-friendly starter notebook walks through loading, EDA, preprocessing, a multi-output model, and the ppm-to-gap calculation, so first-timers can produce a valid submission end to end.

**Incentives:** cash prizes for the top 3 (1st $1,250, 2nd $750, 3rd $500), NVIDIA Deep Learning Institute courses and certificates for the top 50 contributors, and 5,000 Zindi points.

## My contribution
- Partner management for Amini across 5 challenges, including this one
- **Data sourcing:** pulled and assembled **7 environmental data products** for the relevant years and farm locations, giving participants spatial and environmental features alongside the soil measurements
- Challenge design: scoped the task and the evaluation metric, and defined the gap calculation
- Wrote the starter notebook
- Published the winning solution so the approach is shared with the community

## Approach (benchmark)
| Step | Decision | Why |
|---|---|---|
| Targets | 11 nutrient concentrations (ppm), predicted jointly | One model interface for all nutrients |
| Model | `MultiOutputRegressor(RandomForestRegressor)` | Simple, strong baseline with little tuning |
| Missing values | Mean imputation | Easy for beginners to follow |
| Gap calculation | Apply the agronomic formula to the predicted ppm and bulk density | Connects model output to the scored decision |

## Results & impact
| | RMSE |
|---|---|
| Benchmark | 1131.62 |
| Winning solution | 1055.17 |

The winning solution took a "hundred heads are better than one" approach, an ensemble of many models, written up in the link above.

## Repo contents
```
notebooks/starter_notebook.ipynb   # participant-facing starter (as published, with outputs)
data/                              # empty — download from Zindi (link above)
```
To run: download the data into `data/`, `pip install -r requirements.txt`, open the notebook.

## Attribution & licensing
The notebook was written by me while at Zindi for the competition. The competition data is © its owners and governed by the Zindi competition rules; it is not included here. The notebook's saved outputs include a few small previews of rows.
