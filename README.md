# h2-spatial-assessment-eu

Data and code repository for  
**Rumpelnik, C., Zakeri, B., Surana, K.**  
*Spatially Informed Demand-Side Policies for Green Hydrogen Diffusion in Europe.*

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

#### Data fields

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

5) supplementary_figure_11_data.xlsx

Supplementary file documenting the estimation of levelized technology costs for decarbonization technologies alternative to green H2 (CCUS, direct electrification, biomass). Input for supplementary figure 11.

**Note:**  
The empirical analysis (Code Module *Empirics – Model*) uses natural gas power plant data from **S&P Capital IQ**, which is a commercial data source. Running this module therefore requires a valid S&P Capital IQ subscription.

Data can be obtained via the Power Plant Unit Screener function in S&P Capital IQ Pro:

- *Screener* → *Power Plant Units*
- European Union Countries
- Gen tech: **Natural Gas**  
  (or **Wind** for robustness tests)

6)  second_pass_coefs.rds

Extracted coefficients from regression in empirical analysis module. This file can be used if there is no access to the underlying (commercial) data needed to run the empirical analysis modules.

---

### Code

Includes all code required to run the analysis and reproduce the figures.  
The code is structured into sequential modules that build on one another and must be run in order. Note that for running Modules 1 and 2 (Empirical analysis) access to S&P Capital IQ proprietary and commercial data is required (see above).
However, the code and datafiles are structured in a way that simulation and network analysis (starting with module 3) can be run without running the empirical analysis beforehand, with limited adjustments (commenting in and out) in Module 3. 03-simulation-model-standalone already has been adjusted to work without input from the two empirical modules.

#### How to run this code

This repository contains a Jupyter Notebook (.ipynb) written in R. To run it, you need R and the R Jupyter kernel (IRkernel). You can set up the environment following these steps:

1. Install R
Download and install R from:
https://cran.r-project.org/

Alternatively, using Conda:
conda create -n r_env r-base
conda activate r_env

2. Install the R Jupyter Kernel

Start R and run:

install.packages("IRkernel")
IRkernel::installspec()

If using Conda, register the environment explicitly:

IRkernel::installspec(name = "r_env", displayname = "R (r_env)")

Install Jupyter (if needed)

pip install notebook

or

conda install jupyter

3. Launch Jupyter

Make sure you are in the correct environment, then run:

jupyter notebook

Open the .ipynb file and select the R kernel.

4. Notes

Ensure R and Jupyter are installed in the same environment. The notebooks include a setup cell that (i) sets PROJ_LIB for PROJ/CRS support in some conda/docker environments, and (ii) automatically installs and loads required R packages via install.packages(). System dependencies for geospatial packages (e.g., GDAL, GEOS, PROJ) must be available on the machine (provided by conda or the OS).

If the sf package fails to install, the required system libraries are likely missing. In that case, install them first. For Conda users, run:

conda install -c conda-forge r-sf

or

conda install -c conda-forge gdal geos proj

On Ubuntu/Debian systems, run:

sudo apt install libgdal-dev libgeos-dev libproj-dev

Then restart R and reinstall sf.

Run modules sequentially.

---

#### **1) 01 - Empirics – Model**

- Cost competitiveness forecast and extension to 2100
- Estimation of empirical diffusion model (fitted to natural gas power plants)
- Extended Data Figure 2: Distribution of predictors in the diffusion model
- Supplementary Figure 1: Capacity of natural gas power plants and cogeneration plants
- Supplementary Figure 2: Spatial dependency of natural gas power plant siting over time
- Supplementary Figure 3: Natural gas power plant additions by year and generation technology
- Supplementary Figure 8: Spatial autocorrelation
- Supplementary Figure 9: Serial autocorrelation
- Supplementary Figure 10: Cost competititveness trajectory

---

#### **2) 02 - Empirics – Marginal Effects**

- Marginal effects calculation
- Figure 2: Average marginal effects of spatial spilloverts and cost competitiveness on aqdoption probability
- Supplementary Figure 4: Average marginal effects of cost competitiveness and spatial spillovers on adoption using cogeneration plants as historical analogue. (uses Figure 2 code, produces SF 4 when EMPIRICS - MODEL Module is with Cogenerator = Yes filter before)
- Supplementary Figure 6: Average marginal effects of cost competitiveness and spatial spillovers on adoption using cogeneration plants as historical analogue. (uses Figure 2 code, produces SF 4 when EMPIRICS - MODEL Module is run for Wind before)

---

#### **3) 03 - Simulation – Model**

- Prepares offtaker dataset for analysis (aggregation of heavy duty, etc.)",
- Calculate predictor variables on the H2 offtaker dataset",
- Simulates green H2 demand baseline projections",
- **Figure 5: ** Baseline projections of expected green H2 demand before policy intervention\n",
- Supplementary Figure 5: Baseline projections of expected green hydrogen demand before policy intervention using cogeneration plants as historical analogue,
(Uses Figure 5 code; produced when Empirics-Model is first run for cogeneration plants)\n",
- **Supplementary Figure 7:** Baseline projections of expected green hydrogen demand before policy intervention using wind plants as historical analogue,
(Uses Figure 5 code; produced when Empirics-Model is first run for wind plants)\n",
- **Supplementary Figure 13:** Baseline projections of expected green hydrogen demand with flat carbon pricing,
(Uses Figure 5 code; produced when Empirics-Model and Simulation-Model are first run for carbon_price_setting = flat_carbon_price)\n",
- **Extended Data Tables 2 and 3**

**Use 03-Simulation-Model-Standalone if there is no access to S&P Capital IQ, this version draws the model coefficients from the datafile.**

---

#### **4) 04 - Network – Centrality**

-Computation of network centrality scores (marker for spillover potential)
- **Figure 3:** Spatial spillover poptential of green H2 offtakers across regions
- **Figure 4:** Spatial spillover poptential of green H2 offtakers across sectors
- **Extended Data Figure 1:** Map of H2 valleys and corridors
- **Extended Data Figure 3:** Distribution of spillover potential excl. heating

---
#### **5) 05 - Simulation – Policy - Intervention**

- 5a: Policy intervention for controlled setting
- 5b: Policy intervention for EHB style setting
- 5c: Policy intervention for EHB style setting - loop across multiple centrality criterion weights
- **Supplementary Figure 16:** Policy effectiveness for different centrality criterion weights
---

#### **6) 06 - Simulation – Policy - Effectiveness**

- **Figure 6:** Differences in expected green H2 demand and policy cost effectiveness for a spatially targeted demand-side CfD
- **Supplementary Figure 14:** Differences in expected green H2 demand and policy cost effectiveness for a spatially targeted demand-side CfD: Results for alternative baselines (Controlled setting)
- **Supplementary Figure 15:** Differences in expected green H2 demand and policy cost effectiveness for a spatially targeted demand-side CfD: Results for alternative baselines (EHB setting)

---

#### **7) SI - Saturation**

- **Supplementary Figure 11:** Cost trajectories for alternative decarbonization technologies in EUR MWh

---

#### **8) SI - Carbon Price**

- **Supplementary Figure 12:** Carbon price projections in EUR/t C02 equivalent

---

Expected run time is less than 3 hours on standard hardware.

