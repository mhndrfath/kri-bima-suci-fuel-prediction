# Vessel Fuel Consumption Prediction — KRI Bima Suci

Machine-learning models for fuel-consumption estimation on the Indonesian Navy training vessel **KRI Bima Suci**, using operational data from noon reports and engine logbooks.

This is the work from my undergraduate thesis at Institut Teknologi Sepuluh Nopember (ITS), Department of Marine Engineering, Faculty of Marine Technology — Bachelor of Engineering Degree in Digital Marine Operation and Maintenance (DMOM), February 2022.

📄 **[Read the full thesis (PDF)](./04211841000028-Undergraduate_Thesis.pdf)**

---

## Problem

KRI Bima Suci, the Indonesian Navy's tall-ship training vessel (111.2m × 13.65m, 2,500 tons, MAN 6L21/31 main engine at 1,290 kW), was running short of fuel during voyages. The cause was that fuel-consumption estimation aboard was being done manually, without computer-assisted modelling.

The thesis goal: build a machine-learning model that estimates fuel consumption from a small number of routinely-recorded operational variables, accurately enough that crew can plan voyage fuel loads with confidence.

## Approach

**Input variables** (selected from variables routinely recorded on noon reports and available without specialised sensors):

| Variable | Type | Notes |
|----------|------|-------|
| Ship speed | Continuous (knots) | Primary driver — quadratic effect on hull resistance |
| Wind power | Beaufort scale | External environmental factor |
| Sea condition | Categorical | Calm / moderate / choppy |
| Engine RPM | Continuous | Indirect effect via engine load |

**Target variable:** fuel consumption (litres).

**Variables considered but excluded** due to lack of recording on KRI Bima Suci's operational documents: vessel displacement, freshwater consumption, engine load, draft.

**Methods compared:** six ML approaches — three classification methods (Naive Bayes, K-Nearest Neighbour, K-Means clustering) and three regression methods (Linear Regression, Polynomial Regression, Support Vector Regression).

**Data source:** ship noon reports and engine logbooks for KRI Bima Suci voyages, 16–25 November 2021. Data was provided by the head of the engine room (Mayor Laut (T) Budi Luhur, Indonesian Navy Academy).

## Results

### Regression models

| Model | Accuracy | Mean error |
|-------|----------|-----------|
| Linear Regression | 29.4% | 151.99 L |
| **Polynomial Regression** | **98.99%** | **13.66 L** |
| Support Vector Regression | — | 107.26 L |

Polynomial Regression was selected as the best-performing regression model — accuracy was an order of magnitude better than Linear Regression and the mean error of 13.66 L was within operational tolerance for voyage planning on this vessel class.

### Classification models

| Model | Accuracy |
|-------|---------|
| Naive Bayes | 79.57% |
| **K-Nearest Neighbour** | **84.95%** |
| K-Means | (used for clustering only — no accuracy metric) |

### Website prototype

A smartphone-first prototype was designed in Figma with frontend logic in JavaScript, intended for use by engine-room personnel. The five core menus were: ship details, annual trip schedule, fuel-consumption estimation, regression input, and classification input.

The frontend was not connected to a live backend at the navy's request — vessel operational data is confidential.

## Conclusion

- Polynomial Regression on these four operational variables produced fuel-consumption estimates within ~14 L of actual on test data — a substantial improvement over the manual estimation method previously used aboard.
- Many additional variables (displacement, draft, engine load) would likely improve accuracy further if recording were extended.
- A computer-assisted estimation tool is feasible on this vessel class with the data already routinely recorded.

## Future work

Recommendations from the thesis (Chapter 5):

1. Extend the recorded variable set (engine load, displacement, draft, freshwater) to improve model robustness.
2. Add additional regression and classification methods to give users more comparison options.
3. Port the prototype from web to native mobile (Android / iOS) for offline operation aboard.
4. Add role-based access (engine division / commander / public) with appropriate views.

---

## Repository structure

```
.
├── 04211841000028-Undergraduate_Thesis.pdf   # Full thesis document
├── README.md                                  # This file
├── notebooks/                                 # [TO ADD: reproducible analysis notebooks]
├── data/                                      # [TO ADD: sample/synthetic data — see note below]
└── prototype/                                 # [TO ADD: website prototype assets / Figma export]
```

## A note on data

The original KRI Bima Suci operational data is confidential and cannot be published in this repository. The notebooks (when added) will reproduce the analysis using either:

- Synthetic data generated to match the statistical distributions of the original noon-report variables, or
- A public maritime fuel-consumption dataset for benchmarking the same methods.

The original results reported above are from the thesis using the real KRI Bima Suci dataset.

## Citation

If you reference this work, please cite:

> Firdaus, M. A. (2022). *Estimation of Fuel Consumption on KRI Bima Suci Using Machine Learning.* Bachelor's thesis, Department of Marine Engineering, Institut Teknologi Sepuluh Nopember, Surabaya, Indonesia.

Supervisors: Ir. Dwi Priyanta, M.SE.; Ir. Hari Prastowo, M.Sc.

## Author

**Mahendra Alfath Firdaus**
mahendraalfathfirdaus@gmail.com · github.com/mhndrfath
