# TXST-GEO-5418-Courtright

Suitability Analysis from Texas State's GEO 5418 (Introduction to Geographic Information Systems I) graduate course.

A GIS-based suitability analysis identifying land within the Austin-Round Rock-San Marcos MSA suitable for new sustainable housing development, built to address the region's severe housing shortage amid sustained population growth.

The attached paper covers a suitability analysis on the Austin-Round Rock-San Marcos MSA for sustainable residential development. The analysis was conducted using ArcGIS Pro and Census, grocery store location, and household income data. The analysis also uses county boundaries, highway routes, slope and aspect information, and data from the National Land Cover Database.

## Methodology

Seven binary criterion rasters (1 = Pass, 0 = Fail) were generated and multiplied together in Raster Calculator, so a cell only passes if it satisfies all criteria simultaneously:

1. **Population Density** ≥ 250 people/mi² (vector query → Polygon to Raster → Reclassify)
2. **Median Household Income** ≥ $50,000 (vector query → Polygon to Raster → Reclassify)
3. **Distance from Highway** — 0.5–10 miles (Euclidean Distance → Reclassify)
4. **Distance from Grocery Store** — within 10 miles (Geocoded via Display XY → Euclidean Distance → Reclassify)
5. **Compatible Land Cover** — Developed Open Space, Developed Low Intensity, Grassland/Herbaceous, Shrub/Scrub, Barren Land, Pasture/Hay (NLCD Reclassify)
6. **Slope** ≤ 3° (Slope tool on DEM → Reclassify)
7. **Aspect** — 112.5°–247.5° / SE–SW facing (Aspect tool on DEM → Reclassify)

## Results

- **532,715 cells** met all seven criteria (**≈184.85 mi²** of suitable land)
- Suitable land concentrates along the **I-35 corridor**, from Round Rock through Austin and southwest toward San Marcos, with the **Cedar Park / Round Rock** area emerging as the strongest cluster
- Eastern and western peripheries of the MSA were largely excluded, primarily by the highway, grocery, and population density criteria

## Repository Contents

| File | Description |
|---|---|
| `Courtright_Final_Report.pdf` | Full written report with data, methodology, results, and discussion |
| `Pop_Dens.png` | Population density by census tract, statewide context (Figure 1) |
| `Crit1.png` | Criterion 1 — Population Density |
| `Crit2.png` | Criterion 2 — Median Household Income |
| `Crit3.png` | Criterion 3 — Distance from Highway |
| `Crit4.png` | Criterion 4 — Distance from Grocery Store |
| `Crit5.png` | Criterion 5 — Compatible Land Cover |
| `Crit6v2.png` | Criterion 6 — Slope |
| `Crit7v2.png` | Criterion 7 — Aspect |
| `Final.png` | Final overlay — suitable sites meeting all 7 criteria |

## Software & Data

- **ArcGIS Pro** — all geoprocessing, raster analysis, and cartographic output
- **Coordinate system:** NAD 1983 State Plane Texas Central FIPS 4203 (US Feet)
- **Cell size:** 98.4252 ft (~30 m), standardized across all raster operations
- Data sources: U.S. Census Bureau (tracts, income, population), county boundaries, highway network, DEM (slope/aspect), NLCD 2011 land cover, geocoded grocery store locations

## Limitations

- Socioeconomic data (2019) and land cover data (NLCD 2011) predate current conditions in a fast-growing region
- Binary overlay treats all criteria as equally weighted; a weighted overlay would give a more graduated result
- Grocery store dataset may be incomplete
- DEM resolution (93.53 ft) limits precision of slope/aspect along the Balcones Escarpment
- Analysis does not account for land ownership, zoning, or other legal development constraints

## License

See `LICENSE`.
