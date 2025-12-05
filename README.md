# h2-spatial-assessment-eu

Data and code repository for Rumpelnik, C., Zakeri, B., Surana K. A spatially resolved assessment of green hydrogen diffusion in Europe.

The repository is structured as follos:

Data: Includes open-source data files required to run the analysis including
1) 
2)
3)
4)

Note that the empirical analysis (code module x) uses natrual gas power plant data from S&P Capital IQ, which is a commercial source. To run this code, a subscription to S&P Capital IQ is required. Data can be downloaded by going to Screener / Power Plants, selecting European Union Countries and Natural Gas (Wind for robustness test) as generation technology.


Code: Includes code required to run the analysis and produce the figures. Code is structured in several modules which need to be run sequentially, as they build on each other.

**1) Empirics - Model:** 
 ---- Cost competitiveness forecast and extension to 2100
 ---- Estimation of empirical diffusion model (fitted to natural gas power plants)
 ---- Extended Data Figure 1: Distribution of predictors in the diffusion model
 ---- Supplementary Figure 1: Capacity of natural gas power plants
 ---- Supplementary Figure 2: Spatial autocorrelation
 ---- Supplementary Figure 3: Serial autocorrelation
 ---- Supplementary Figure 6: Cost competititveness trajectory
 ---- Supplementary Table 1: Collinearity test
**2) Empirics - Marginal Effects**
---- Marginal effects calculation
---- Figure 2: Average marginal effects of spatial spilloverts and cost competitiveness on aqdoption probability
---- Supplementary Figure 4: Average marginal effects of cost competitiveness and spatial spillovers on adoption using wind as historical analogue (uses Figure 2 code, produces SF 4 when Empirics - Model Module is run for Wind before)
**3) Simulation - Model**
---- Prepares offtaker dataset for analysis (aggregation of heavy duty, etc.)
---- Calculate predictor variables on the H2 offtaker dataset
---- Simulates green H2 demand baseline projections
---- Figure 5: Baseline projections of expected green H2 demand before policy intervention
---- Supplementary Figure 5: Baseline projections of expected green H2 demand before policy intervention using wind as historical analogue (uses Figure 5 code, produces SF 5 when EMPIRICS - MODEL Module is run for Wind before)
---- Extended Data Tables 2 and 3
**4) Network - Centrality**  
6)
7)
8)
