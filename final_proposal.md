Crashes and Causes: A Data-Driven Analysis of Motor Vehicle Collisions
in New York City (2012–2024)
================
Team XX: Daniel Jiao (UNI: dj2764), Xinyu Wang(UNI: xwang3106), Yuyang
Wang (UNI: yw4660), Haoyi Tan (UNI: ht2717)

## Motivation

Motor vehicle collisions are a leading cause of injury and death in
urban settings.  
In New York City, hundreds of crashes are recorded every day, and these
events reflect patterns in traffic volume, street design, driver
behavior, and policy interventions such as *Vision Zero*.

Understanding **when** and **where** crashes occur, and **which
factors** contribute to severe outcomes, can provide actionable insights
for traffic safety planning and public policy.

In this project, we will use the NYC Open Data **“Motor Vehicle
Collisions – Crashes”** dataset to study temporal, spatial, and causal
patterns in motor vehicle collisions across New York City.

## Team Members

- **Daniel Jiao** (UNI: dj2764) – data acquisition, cleaning, and
  pipeline setup  
- **Xinyu Wang** (UNI: xxxxxx) – exploratory data analysis and
  visualization  
- **Yuyang Wang** (UNI: yw4660) – modeling and statistical analysis  
- **Haoyi Tan** (UNI: ht2717) – website, report integration, and
  screencast

## Initial Questions

We plan to focus on the following questions; these may evolve as our
analysis progresses:

1.  **Temporal trends**
    - How have the number and severity of crashes changed over time
      (2012–2024)?  
    - Are there clear **seasonal patterns** or **daily/weekly cycles**
      in crash frequency?
2.  **Spatial variation**
    - Which boroughs and neighborhoods experience the highest collision
      rates and most severe crashes?  
    - Can we identify “hot spots” of collisions using spatial
      visualization?
3.  **Contributing factors**
    - What are the most common **contributing factors** (e.g., driver
      inattention, unsafe speed, alcohol involvement)?  
    - How do these factors differ by borough, time of day, or vehicle
      type (e.g., private cars vs taxis vs bicycles)?
4.  **Policy evaluation (Vision Zero)**
    - Did the launch of NYC’s *Vision Zero* initiative in 2014 coincide
      with noticeable changes in crash counts and fatalities?  
    - Are trends in serious injury and fatal crashes different before
      and after 2014?

## Data

Our primary dataset is:

- **NYC Open Data – Motor Vehicle Collisions: Crashes**
  - Portal:
    <https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95>  
  - Unit of observation: one row per reported collision  
  - Coverage: 2012–present, all five NYC boroughs

Key variables we expect to use include:

- `CRASH_DATE`, `CRASH_TIME` – date and time of crash  
- `BOROUGH`, `ZIP_CODE` – borough and ZIP code  
- `LATITUDE`, `LONGITUDE` – crash coordinates  
- `NUMBER_OF_PERSONS_INJURED`, `NUMBER_OF_PERSONS_KILLED`  
- `CONTRIBUTING_FACTOR_VEHICLE_1` … `CONTRIBUTING_FACTOR_VEHICLE_5`  
- `VEHICLE_TYPE_CODE_1` … `VEHICLE_TYPE_CODE_5`  
- `ON_STREET_NAME`, `CROSS_STREET_NAME`  
- `COLLISION_ID` – unique identifier

### Data cleaning and preprocessing (planned)

Because the full dataset is large (millions of rows), we plan to:

- Restrict the main analysis to a recent time window (e.g.,
  **2015–2024**) while keeping earlier years for trend checks.  
- Filter to observations with non-missing boroughs and valid
  coordinates.  
- Create new variables:
  - `year`, `month`, `weekday`, `hour` from `CRASH_DATE` and
    `CRASH_TIME`  
  - indicators for any injury / any fatality  
  - grouped categories of contributing factors (e.g., *Driver
    Inattention*, *Unsafe Speed*, *Alcohol Involvement*, *Other*).  
- Remove obvious duplicates or records with impossible values (e.g.,
  negative counts).

We will use **R**, primarily the `tidyverse` ecosystem, for data import,
cleaning, and analysis.

## Planned Analyses / Visualizations / Coding Challenges

We anticipate the following main components:

1.  **Exploratory Data Analysis (EDA)**
    - Time series plots of monthly crash counts and injury/fatality
      counts by borough.  
    - Distribution of crashes by hour of day and day of week (e.g.,
      heatmaps).  
    - Top contributing factors overall and stratified by borough or time
      of day.
2.  **Spatial analysis**
    - Map crash locations using `leaflet` or `ggplot2` with spatial data
      (`sf`).  
    - Aggregate to neighborhood or ZIP code for **crash density**
      visualizations.  
    - Identify high-risk areas (“hot spots”) and compare across
      boroughs.
3.  **Policy / temporal comparison**
    - Compare crashes **before vs after 2014** (Vision Zero start)
      using:
      - Summary statistics  
      - Time-series plots with vertical reference lines  
      - Simple regression / interrupted time series–style comparisons
        (if appropriate).
4.  **Modeling (injury / fatality risk)**
    - Build exploratory logistic regression models for:
      - probability of any injury, and/or  
      - probability of any fatality  
    - Predictors may include borough, hour of day, contributing factor
      categories, and vehicle type.  
    - Assess variable importance and model fit; interpret coefficients
      in a public-health context.
5.  **Visualization and communication**
    - Well-labeled, publication-quality figures created using
      `ggplot2`.  
    - Potential interactive elements (e.g., interactive maps or hover
      tooltips) on the project website.

Coding challenges we anticipate include:

- Efficiently handling a large dataset (memory and speed).  
- Working with date-time variables and combining `CRASH_DATE` and
  `CRASH_TIME`.  
- Cleaning and recoding free-text contributing factor variables into
  meaningful groups.  
- Integrating static and (optionally) interactive visualizations into a
  reproducible website.

## Intended Final Products

- **Written report (R Markdown → HTML)**  
  A self-contained document describing motivation, data, methods,
  results, and discussion.

- **Project website**  
  Built using R Markdown / Quarto and GitHub Pages, with:

  - Landing page summarizing motivation and main findings  
  - Detailed EDA and analysis pages  
  - Embedded full report

- **Screencast (≈2 minutes)**  
  A narrated video that walks through the project motivation and key
  visualizations, aimed at classmates and a general audience.

- **GitHub repository**  
  Public repo containing:

  - `data/` (raw and cleaned data or scripts to download)  
  - `scripts/` (cleaning and analysis code)  
  - `report/` (Rmd + rendered HTML)  
  - `docs/` or `website/` (project website files)

## Planned Timeline

This timeline may be adjusted after the project review meeting, but our
current plan is:

- **Week 1 (Proposal + Setup)**
  - Finalize research questions and team roles  
  - Create GitHub repository and basic folder structure  
  - Download a subset of data and complete initial cleaning
- **Week 2 (EDA + Basic Visualizations)**
  - Summaries by borough, time, and injury/fatality severity  
  - Initial time trend and heatmap visualizations
- **Week 3 (Spatial & Factor Analysis)**
  - Create maps of crash density and hot spots  
  - Analyze contributing factors and vehicle types
- **Week 4 (Modeling + Draft Report)**
  - Fit preliminary models for injury/fatality risk  
  - Draft written report and integrate figures
- **Week 5 (Polish + Website + Screencast)**
  - Finalize report and website structure  
  - Record and upload screencast  
  - Final checks for reproducibility and clarity

We will discuss this plan with the teaching team during the project
review meeting and adjust as needed.
