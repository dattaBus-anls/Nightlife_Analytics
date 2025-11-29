# Nightlife_Analytics

**Author:** Apu Datta  
**Course:** STA 9750 – Data Analysis for Public Policy  
**Project type:** NYC nightlife mobility analysis (Quarto + R)

---

## 1. Project Overview

New York City’s nightlife is more than entertainment – it drives service jobs, late-night transportation demand, and the perceived safety of busy streets. This project combines:

- **TLC night-time trip records (Yellow + Uber/Lyft)**
- **Yelp nightlife venues (bars, clubs, lounges, etc.)**

to study how **COVID-19 reshaped night-time mobility in NYC (8 PM–4 AM)**.

**Main question**

> Has COVID changed the way the city moves at night, and how is that linked to nightlife intensity across neighborhoods?

The analysis focuses on three periods:

- **Pre-COVID** – baseline nightlife curve and spatial pattern  
- **During COVID** – collapse of late-night trips  
- **Post-COVID** – uneven and partial recovery, with stronger reliance on rideshare

All results are documented in `quarto/Nightlife Analytics.qmd` and rendered to HTML.

---

## 2. Key Findings (Short Summary)

- **Hourly pattern shifted.** Pre-COVID nights follow a classic nightlife curve with a strong midnight peak. During COVID, the curve collapses across all hours; late-night (midnight–3 AM) nearly disappears. Post-COVID, early evening trips rebound strongly, but the late-night tail remains weaker than pre-COVID.

- **Weekends were hit hardest.** Weekend nights (Fri–Sat) lost the most volume during COVID. After reopening, weekend trips rebound faster than weekdays, showing nightlife-driven travel returning earlier and more strongly.

- **Trips got shorter during COVID.** Trip distances and durations are shortest and least variable during COVID, indicating that people stayed closer to home and made fewer long discretionary trips.

- **Rideshare dominance increased.** FHVs (Uber/Lyft) already dominated night trips pre-COVID. Their share rises further during and after COVID, while Yellow cab share stays low and does not recover – a structural shift in night-time transport.

- **Nightlife density predicts mobility.** Taxi zones with more Yelp nightlife venues systematically generate more night trips. The relationship weakens during COVID but re-emerges post-COVID, although recovery is uneven across neighborhoods.

- **Changes are statistically significant.** Bootstrap confidence intervals, permutation tests, and negative binomial count models all show large, statistically significant differences in night-time trip intensity across the three COVID periods.

---

## 3. Data Sources

1. **TLC Trip Records (Parquet) – Night Trips (8 PM–4 AM)**  
   - Source: NYC Taxi & Limousine Commission  
   - URL: <https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page>  
   - Providers: `yellow`, `fhvhv` (Uber/Lyft)  
   - Months used: June & December, 2019–2023  
   - Key fields: pickup/dropoff time, PULocationID, DOLocationID, distance, fare, provider

2. **TLC Taxi Zone Shapefile**  
   - URL: <https://d37ci6vzurychx.cloudfront.net/misc/taxi_zones.zip>  
   - Used to join trips and Yelp venues to borough + zone polygons.

3. **Yelp Nightlife Venues (Fusion API / Dataset)**  
   - Bars, clubs, lounges, and other nightlife venues in NYC  
   - Fields: name, rating, price tier, latitude/longitude, categories  
   - Converted to spatial points, spatially joined to TLC taxi zones.

---

## 4. Repository Structure

```text
Nightlife_Analytics/
├─ data/
│  ├─ tlc/          # cached parquet + RDS night-trip data (ignored by git)
│  ├─ tlc_zones/    # TLC taxi_zones shapefile (downloaded automatically)
│  └─ yelp/         # Yelp nightlife snapshot nightlife_nyc.csv (ignored by git)
├─ Image/           # static images used in the Quarto report
├─ quarto/
│  ├─ Nightlife Analytics.qmd     # main analysis + report
│  ├─ Nightlife Analytics.html    # rendered HTML (ignored by git)
│  ├─ Nightlife-Analytics_cache/  # Quarto cache (ignored by git)
│  ├─ Nightlife Analytics_files/  # HTML dependencies (ignored by git)
│  └─ scripts/                    # helper R scripts (if any)
├─ scripts/        # project-level helper scripts (optional)
├─ Nightlife Analytics.Rproj
├─ .gitignore
└─ README.md
