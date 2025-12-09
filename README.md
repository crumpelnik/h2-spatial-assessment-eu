# h2-spatial-assessment-eu

Data and code repository for  
**Rumpelnik, C., Zakeri, B., Surana, K.**  
*A spatially resolved assessment of green hydrogen diffusion in Europe.*

---

## Repository structure

### Data

Includes open-source data files required to run the analysis, including:

1)  INET_PipeSegments-geojson

Open-source geojson file from SciGrid Gas (https://arxiv.org/abs/2201.08827) including natural gas pipeline segment geodata. Data is used to calculate proximity between individual natural gas power plants (empirical analysis) and h2 offtakers (simulation) and high order natural gas pipeline corridors.

2)  cost_competitiveness_fossil.xlsx

Cost time series data (up to 2050) for fossil incumbents based on Odenweller and Ueckerdt (2025). The green hydrogen ambition and implementation gaps. Raw original data files are accessible in their Github repository (https://github.com/aodenweller/green-hydrogen-gap/tree/master). Includes an xlsx computation module for the estimation of a flat carbon price scenario.

3)  cost_competitiveness_green.xlsx

Cost time series data (up to 2050) for green hydrogen and derivatives based on Odenweller and Ueckerdt (2025). The green hydrogen ambition and implementation gaps. Raw original data files are accessible in their Github repository (https://github.com/aodenweller/green-hydrogen-gap/tree/master) 

4)  h2_database.xlsx

Original database of 14,000+ potential green hydrogen offtakers aggregating information from multiple data sources (including ETS and Eurostat). Details on database build-up are disclosed in the Methods section of the article. Additional information on the database build-up is available upon request. Variable list below.

## Data fields

| Variable name | Description |
|--------------|-------------|
| `account_holder_name` | Name of the entity owning or operating the installation (industrial sectors only) |
| `installation_name` | Name of the individual installation or facility (all except heavy duty / fuel stations) |
| `Sector` | High-level economic sector classification |
| `Industry` | Detailed industry classification |
| `Index_2030` | Activity level index 2030 relative to 2023 |
| `Index_2050` | Activity level index 2050 relative to 2023 |
| `emissions` | Annual carbon emissions associated with the installation in T C02e |
| `production` | Annual production output of the installation in T|
| `match` | Indicator whether the installation could be matched in a specific geocoding step (industrial sectors only) |
| `manual` | Indicator whether matching or classification required manual validation (industrial sectors only)|
| `hydrogen` | (H2-specific) energy consumption in 2023/24 in KT |
| `hydrogen_2030` | (H2-specific) energy consumption in 2030 in KT |
| `hydrogen_2050` | (H2-specific) energy consumption in 2050 in KT  |
| `passengerkm` | Passenger transport activity in passenger-km (aviation / airports only) |
| `tonnekm` | Shipping freight activity in tonne-km (shipping / ports only) |
| `capacity_p` | Installed capacity (MW) |
| `distributed_tonnekm` | Heavy duty freight activity in tonnekm (heavy duty / (agggregated) fuel stations only) |
| `population` | Population in number of inhibitants (heat installations / cities only) |
| `BM` | Benchmark emissions factor (weighted realized emissions factor) |
| `BM_AL` | Benchmark emissions factor for allocation of emissions credits |
| `NUTS1_code` | NUTS-1 regional code |
| `NUTS1_name` | NUTS-1 region name |
| `NUTS2_code` | NUTS-2 regional code |
| `NUTS2_name` | NUTS-2 region name |
| `NUTS3_code` | NUTS-3 regional code |
| `NUTS3_name` | NUTS-3 region name |
| `contact_country` | Two letter country code of the installation's location |
| `lon` | Longitude of the installation (WGS84) |
| `lat` | Latitude of the installation (WGS84) |


5) emission_factors_secs.xlsx

Supplementary file documenting the estimation, sourcing and allocation of emissions benchmarks and hydrogen-specific energy consumption factors on a sub-activity level.

**Note:**  
The empirical analysis (Code Module *Empirics – Model*) uses natural gas power plant data from **S&P Capital IQ**, which is a commercial data source. Running this module therefore requires a valid S&P Capital IQ subscription.

Data can be obtained via the Power Plant Unit Screener function in S&P Capital IQ Pro:

- *Screener* → *Power Plant Units*
- European Union Countries
- Gen tech: **Natural Gas**  
  (or **Wind** for robustness tests)

---

### Code

Includes all code required to run the analysis and reproduce the figures.  
The code is structured into sequential modules that build on one another and must be run in order.

---

#### **1) Empirics – Model**

- Estimation of the empirical diffusion model (fitted to natural gas power plants)
- Cost competitiveness forecast and extension to 2100.
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
  - Uses Figure 2 code; produced when *Empirics – Model* is first run for wind  

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

-Computation of network centrality scores (marker for spillover potential)
- **Figure 3:** Spatial spillover poptential of green H2 offtakers across regions
- **Figure 4:** Spatial spillover poptential of green H2 offtakers across sectors
- **Extended Data Figure 3:** Distribution of spillover potential excl. heating

---
#### **5) Simulation - Policy - Intervention **

- Policy intervention simulation

---

#### **6) Network – Policy - Effectiveness**

-Computation of network centrality scores (marker for spillover potential)
- **Figure 3:** Spatial spillover poptential of green H2 offtakers across regions
- **Figure 4:** Spatial spillover poptential of green H2 offtakers across sectors
- **Extended Data Figure 3:** Distribution of spillover potential excl. heating

