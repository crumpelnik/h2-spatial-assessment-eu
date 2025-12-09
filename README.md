# h2-spatial-assessment-eu

Data and code repository for  
**Rumpelnik, C., Zakeri, B., Surana, K.**  
*A spatially resolved assessment of green hydrogen diffusion in Europe.*

---

## Repository structure

### Data

Includes open-source data files required to run the analysis, including:

1)  
2)  
3)  
4)  

**Note:**  
The empirical analysis (Code Module *Empirics – Model*) uses natural gas power plant data from **S&P Capital IQ**, which is a commercial data source. Running this module therefore requires a valid S&P Capital IQ subscription.

Data can be obtained via:

- *Screener* → *Power Plants*
- Region: European Union  
- Generation technology: **Natural Gas**  
  (or **Wind** for robustness tests)

---

### Code

Includes all code required to run the analysis and reproduce the figures.  
The code is structured into sequential modules that build on one another and must be run in order.

---

#### **1) Empirics – Model**

Cost competitiveness forecast and extension to 2100.

- Estimation of the empirical diffusion model (fitted to natural gas power plants)
- **Extended Data Figure 1:** Distribution of predictors in the diffusion model  
- **Supplementary Figure 1:** Capacity of natural gas power plants  
- **Supplementary Figure 2:** Spatial autocorrelation  
- **Supplementary Figure 3:** Serial autocorrelation  
- **Supplementary Figure 6:** Cost competitiveness trajectory  
- **Supplementary Table 1:** Collinearity test  

---

#### **2) Empirics – Marginal Effects**

- Marginal effects calculation
- **Figure 2:** Average marginal effects of spatial spillovers and cost competitiveness on adoption probability  
- **Supplementary Figure 4:** Average marginal effects of cost competitiveness and spatial spillovers using wind as historical analogue  
  - Uses Figure 2 code  
  - Produced when *Empirics – Model* is first run for wind  

---

#### **3) Simulation – Model**

- Preparation of offtaker dataset (e.g. aggregation of heavy-duty transport)
- Calculation of predictor variables on the hydrogen offtaker dataset
- Simulation of baseline green hydrogen demand projections
- **Figure 5:** Baseline projections of expected green hydrogen demand before policy intervention  
- **Supplementary Figure 5:** Baseline projections using wind as historical analogue  
  - Uses Figure 5 code  
  - Produced when *Empirics – Model* is first run for wind  
- **Extended Data Tables 2 and 3**

---

#### **4) Network – Centrality**

6)  
7)  
8)  

---

