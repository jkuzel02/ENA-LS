# CoolRoute Brno — research findings and project guide

**Working city: Brno. Research snapshot: 12 October 2026.** I switched the project from Vienna to Brno after checking the course assignment, official Brno material, and Brno’s open-data catalog. This guide is meant to help a team with limited GIS experience build a clear, defensible pilot.

## 1. Why this is a real citizen problem

The issue is documented by Brno itself. The city describes an urban heat-island effect and provides a thermal map based on aerial thermal surveys, including 2015, 2019 and 2024 data. Brno’s own climate materials also identify dense built-up areas and surfaces with little greenery as hotter, and explain the cooling role of parks and water. ([Brno thermal map and its survey dates](https://gis.brno.cz/mapa/teplotni-mapa/?c=-); [Brno Metropolitan Area climate story map](https://metropolitni.brno.cz/brnenska-metropolitni-oblast-z-vesmiru-satelitni-data-ukazuji-jak-se-zmena-klimatu-projevi-v-brne-a-okoli-do-roku-2100/); [Brno’s green-space analysis](https://data.brno.cz/pages/d8b691b7f84542bc88bf57cbb24ccfdc))

The citizen problem is narrower and practical: **on a hot day, people need to get somewhere on foot and would benefit from knowing which route has more observed shade, nearby drinking water, and places to rest.** The existing thermal map helps show the city-scale heat problem; the proposed service turns that context into route choices and field-checked amenities. It should be described as a **heat-aware route estimate**, not a guaranteed “coolest route.”

Before finalizing the design, ask a few potential users (for example, students, older adults, caregivers, or people who walk to transit) what they do during hot weather and what would make a route recommendation useful. This verifies the service need; the team should not claim broad public demand from a few conversations.

## 2. Assignment checklist

The assignment requires a city with at least 200,000 residents. data.Brno reports **404,296 residents** on its portal homepage ([data.Brno](https://data.brno.cz/)). The assignment also requires:

- 5 or more datasets from the official city open-data portal.
- 3 or more datasets from other sources, each with at least 20 features.
- 3 or more original team datasets, each with at least 20 independently collected observations.
- A citizen-facing app design with at least 6 screens using the project data.
- ArcGIS Online map(s), an Experience Builder application displaying an ArcGIS Online map, SHP or GeoJSON data, a public Figma link, and a PowerPoint presentation.
- Each progress report must name all 3 teammates and give each person’s percentage of work completed so far.

The proposition deadline in the PDF is **18 October 2026, 20:00**; progress reports are due **8 November** and **7 December 2026, 20:00**. Mandatory consultations are listed for the weeks beginning **19 October** and **6 November**. Add these dates to the team calendar.

## 3. Recommended project scope

Start with a walkable pilot around **Malinovského náměstí–Moravské náměstí–Česká**, or another compact central area your team can reach easily. Brno has specifically discussed heat and comfortable seating at Malinovského náměstí, making this a useful place to investigate ([City of Brno report on the urban cooling cell](https://cosedeje.brno.cz/w/mestska-bunka-ukaze-jak-udelat-posezeni-ve-meste-prijemne-i-v-horkych-dnech)). Aim for about 1–2 km². A small area makes the field survey, quality checks, and route comparison manageable.

Build the first version around one question: **“Between these two places, which walkable option has more observed shade and useful water/rest stops?”** Show the shortest route next to a heat-aware alternative. Avoid promising live navigation; a precomputed route comparison is a realistic course prototype.

## 4. Dataset package — 11 datasets

The five official datasets below are published by Statutory City of Brno and documented through Brno’s official open-data catalog (data.Brno/NKOD). All are vector datasets with a GeoJSON or other GIS download option noted in the catalog. Counts are not stated here as exact where I could not query the complete download; record them after downloading.

| ID | Exact dataset | Publisher / category | Link and access | Format / geometry | What it contributes and current limits |
|---|---|---|---|---|---|
| B1 | **Greenery registry – green surfaces** / *Pasport zeleně – plochy zeleně* | Statutární město Brno / official | [National catalog record](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F541efa42b634116d1a2480a2cfc81bdc); record lists GeoJSON, GPKG, SHP-related and other distributions | GeoJSON/GPKG; green-space areas and inventory elements (confirm layer geometry after download); GCS WGS84 is documented | Detailed green infrastructure and tree/vegetation inventory. Data description says current to April 2023, management/coverage vary by responsible district and some areas are incomplete. Strong but not uniform citywide. |
| B2 | **Major parks and green areas** / *Významné plochy zeleně* | Statutární město Brno / official | [National catalog record](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F4a98185bf27f80571428335224caf1b3); GeoJSON/SHP distributions listed | Polygons; WGS84 documented | Major parks and important green public spaces; includes name/ID, accessibility, notes/status and area per catalog description. Useful for green destinations, not proof that any route through a park is shaded. |
| B3 | **Drinking fountains** / *Pítka* | Statutární město Brno / official | [Brno data portal record](https://data.brno.cz/datasets/mestobrno::p%C3%ADtka-drinking-fountains); [NKOD record](https://data.gov.cz/zdroj/datov%C3%A9-sady/44992785/5968771279b379c4d461fe9b9bea3336) | GeoJSON, JSON, CSV, KML and ZIP distributions listed; points; WGS84 | Point layer of Brno drinking fountains; may include a photo. Catalog says updates are irregular/annual. Confirm count and current operating/seasonal status in the source before showing “available now.” CC BY 4.0 is listed for distributions. |
| B4 | **Street slopes** / *Sklony komunikací* | Statutární město Brno / official | [National catalog record and download distributions](https://data.gov.cz/datov%C3%A1-sada?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2Fef795a9a3fab0602c8918e38d1f20a34) | Line features; GeoJSON, GPKG, SHP-related and other formats; WGS84 | Road links with length and maximum/minimum/mean slope in percent, derived from 2019 terrain data. Useful as an effort/accessibility penalty, but it describes road links, not necessarily the sidewalk surface or curb ramp. CC BY 4.0 listed. |
| B5 | **Watercourses** / *Vodní toky* | Statutární město Brno / official | [National catalog record and GeoJSON distributions](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F017158621a74c39f2a2fb2eac5472502) | Lines; GeoJSON, SHP and others; WGS84 | Axes and names of watercourses in Brno. Adds blue-space context and can help identify route alternatives near water; proximity does not prove that the route is cooler. CC BY 4.0 listed. |
| E1 | **OpenStreetMap pedestrian network** clipped to Brno/pilot | OpenStreetMap contributors / external | [Geofabrik Austria? No: use Czech Republic extract](https://download.geofabrik.de/europe/czech-republic.html) | PBF, SHP ZIP or GPKG ZIP; mostly lines | Core walkable network, with path/footway/crossing/steps/access tags. Count the extracted walkable line features after clipping. OSM is crowdsourced; validate connectivity and pedestrian access. Attribute OpenStreetMap contributors and comply with ODbL. |
| E2 | **Urban Atlas Land Cover/Land Use 2021 – Brno functional urban area (FUA code CZ002L2)** | Copernicus Land Monitoring Service / external | [Urban Atlas 2021 product and FUA downloads](https://land.copernicus.eu/en/products/urban-atlas/urban-atlas-2021); Brno appears in the [official product technical documentation](https://library.land.copernicus.eu/products/Urban_Atlas_CLMS_UA2021_LULC_ATBD_v1.html) | FlatGeobuf or GeoPackage vector; polygons | Brno coverage is confirmed in product documentation. Use land-cover classes for green/sealed/built proportions. Count features after downloading the Brno package. This is 2021 land cover, not current shade or temperature. |
| E3 | **Census population grid 2021** | Eurostat GISCO / external | [Official population-grid page](https://ec.europa.eu/eurostat/web/gisco/geodata/population-distribution/population-grids); [2021 downloads](https://gisco-services.ec.europa.eu/pub/population-grid/2021/) | GPKG polygons or raster; 1 km cells, EPSG:3035 | Context for where people, including older residents, may benefit. Count Brno grid cells after clipping. The 1 km resolution is too coarse to route on; comply with GISCO’s download/use rules. |
| F1 | **Observed sidewalk shade** | Your team / original | Collect in the field; export GeoJSON | Points at fixed sidewalk stations | Minimum 20 distinct stations; target 60 (20 per teammate) as a buffer. Team directly estimates shade at the observation time. |
| F2 | **Air and surface temperature observations** | Your team / original | Collect in the field; export GeoJSON | Points | Minimum 20 distinct locations; target 60 paired readings. These are measurements only at their recorded places and times. |
| F3 | **Resting-place inventory** | Your team / original | Collect in the field; export GeoJSON | Points | Minimum 20 distinct, directly observed rest places; target 30–60 if the area contains them. Record shade/access/comfort with a common rubric. If fewer than 20 exist, expand the pilot; do not fabricate or duplicate features. |

### Dataset-count rule and fallback

For each external and field dataset, count actual features/observations in the downloaded or collected file and keep a simple `dataset_counts.csv`: dataset, source, date, full-area count, pilot count, format, license. The City of Brno’s green registry is the one official dataset with a known coverage caveat: portions are unevenly mapped and the described data snapshot is April 2023. The tree inventory may also contain duplicate stewardship records; check the metadata and geometry before analysis.

**Urban Atlas:** Brno’s FUA (CZ002L2) is included in the official Urban Atlas 2021 product documentation and the product page offers packaged FUA downloads. Download the Brno package, count the polygons, and save the count with the project files. If the download is temporarily unavailable, keep E2 provisional and contact the course instructor before substituting or double-counting a second OSM extract.

The Brno thermal map is excellent evidence of the real problem, but it is an existing web map based on thermal surveys, not automatically a downloadable analysis layer. Treat it as context unless the map’s metadata provides a downloadable raster/vector distribution. Do not count a WMS screenshot as underlying GIS features.

## 5. What each Brno dataset means for the analysis

- **Greenery registry:** count trees/vegetation near route links and classify green elements where the schema supports it. Coverage and currency differ by manager. It indicates vegetation potential, not shade at the hour of travel.
- **Major parks:** find green destinations and whether important park polygons are accessible. Use the park boundaries as context; actual shaded paths need field observation.
- **Drinking fountains:** calculate walking distance to a fountain, not straight-line distance when possible. Validate type, operation and seasonal availability.
- **Street slopes:** add a slope penalty for steep road links. Do not claim wheelchair accessibility from slope alone; curb ramps, width, surface condition and obstacles are separate conditions.
- **Watercourses:** map blue-space context. Do not automatically reduce a segment’s heat score just because it is near a river.
- **OSM network:** create the walkable graph used to connect origins, destinations, fountains and rests. Inspect crossings and access restrictions.
- **Land cover:** summarize green/sealed/built classes around route links. This is a surface-type proxy, not a temperature sensor.
- **Population grid:** show broad demand context. It must not be interpreted at the individual-street scale.
- **Team fieldwork:** direct observation gives the strongest evidence about the pilot’s actual shade, temperatures and rest places during collection.

## 6. Fieldwork plan

Choose three adjoining routes in the pilot area, one per teammate. Agree on a common observation form and collect within a reasonably short, mostly clear-weather period. Each dataset needs at least 20 independent features. Targeting 60 provides room to discard bad GPS points or incomplete records.

| Original dataset | Method and fields | Equipment / time | Common errors and controls |
|---|---|---|---|
| **F1 Shade** — point at sidewalk station | Fields: `obs_id`, `observer`, `date_time`, `shade_pct`, `sky`, `sidewalk_segment_m`, `photo_id`, `notes`. At each station estimate shaded share of the next fixed 10 m of walkable sidewalk. Face the direction of travel and use the same rule. | Phone GPS/camera, shared form; about 2–3 hours for 60 points plus travel. | Observer judgment, cloud/time change, GPS drift. Use fixed segment length, same time window, and review photos together. |
| **F2 Temperature** — point at measurement location | Fields: `obs_id`, `observer`, `date_time`, `air_c`, `surface_c`, `surface_type`, `shade_state`, `sensor_height_m`, `instrument`, `sky`, `notes`. Measure air in shade at a consistent 1.2–1.5 m height; measure surface at a marked material and note shade. | Thermometer; ideally an IR thermometer for surfaces; phone GPS. About 3–4 hours. Record make/model and compare instruments before the walk. | Sensor heated by sun, IR angle/emissivity, different surfaces, weather changes. Timestamp every record and avoid comparing readings taken hours apart as if simultaneous. |
| **F3 Resting places** — point at each distinct public seat/rest location | Fields: `site_id`, `observer`, `date_time`, `seat_type`, `seats_n`, `shade_now`, `backrest`, `armrest`, `step_free_approach`, `condition`, `comfort_1_5`, `photo_id`, `notes`. Use a shared definition of public access and a short written 1–5 comfort rubric. | Phone GPS/camera, checklist; about 2–3 hours. | Subjective comfort and temporary obstructions. Use identical rubric and don’t photograph identifiable people. Expand the pilot if fewer than 20 distinct sites exist. |

Make GeoJSON by collecting in QField and exporting from QGIS, or by entering longitude/latitude in a spreadsheet, loading it into QGIS as a delimited-text point layer, and exporting as GeoJSON in WGS84 (EPSG:4326). Use unique IDs and timestamps. Keep any photographs separate and reference them by ID. Your field observations must be your own records, not copied from city data.

## 7. GIS processing — a beginner-friendly sequence

1. **Choose and draw the pilot boundary.** Use a compact central area. Put this polygon in a project folder and use it to clip every download.
2. **Get one dataset working first.** Download Brno’s fountains as GeoJSON. Open it in QGIS, confirm that points appear in Brno, inspect its attribute table, and count its features. This teaches you the same steps you’ll use on the other data.
3. **Download the five Brno layers and three external layers.** Save original files unchanged in `01_sources`. Make working copies in `02_working`. Keep a source log with URL, download date, CRS, license and count.
4. **Prepare the walking links.** Clip OSM to the pilot and keep walkable paths/streets. Remove links that are private or not pedestrian-accessible. Check where line ends should connect. Split links at intersections so each short segment can have its own score.
5. **Join the useful context.** For each segment, calculate length, nearby greenery, distance to a potable fountain and distance to observed rest places. Add mean/max street slope where links match. Add the proportion of green/sealed land cover around the link. Join field temperature/shade by nearest point and collection time.
6. **Keep measurements and proxies separate.** Store observed `shade_pct` and temperature values in their own fields. Keep tree count, land-cover class and distance to park in separate proxy fields. A proxy must never be presented as a measured temperature.
7. **Make a transparent score.** Start with a small number of parts: `walk cost = segment length × (1 + shade penalty + water-gap penalty + rest-gap penalty + optional slope penalty)`. Normalize penalties to 0–1 and document the weights. Give shade/temperature observations the strongest role, tree/land-cover indicators a smaller role, and slope a separate effort penalty. Test whether changing weights changes the recommended route.
8. **Compare routes.** Compute a shortest route and a lower-heat/amenity route on the cleaned pedestrian graph in QGIS/Python or ArcGIS Pro if available. Publish fixed comparison routes if live network analysis is out of scope. Check both routes on the map and in the field.
9. **Publish in ArcGIS Online.** Export final vector layers to SHP or GeoJSON, upload the pilot network, route alternatives, green areas, fountains and field points as hosted layers, and build the web map. Use Experience Builder to present it. Keep the map’s legend and popups plain: show route length, observed shade coverage, nearest fountain/rest and when observations were made.
10. **Make the six-screen Figma prototype.** Suggested screens: (1) start/map, (2) choose origin/destination, (3) compare route options, (4) route details and score explanation, (5) nearby fountains/rest places, (6) submit or review a field observation. Design for a citizen, not a city analyst. Include the public Figma link in the final submission.
11. **Finish the report and presentation.** Explain the citizen problem, official evidence, sources, feature counts, field protocol, map, route comparison and limitations. Include three team members and their actual work-completion percentages in each progress report.

## 8. Feasibility ratings

Scores: 1 = difficult/weak, 5 = easy/strong. Reliability refers to each source’s stated role, not whether it proves cooling.

| Dataset | Acquisition | Relevance | Processing | Reliability | Main limitation |
|---|---:|---:|---:|---:|---|
| B1 Greenery registry | 4 | 5 | 3 | 3 | Coverage/precision vary by manager; described snapshot April 2023. |
| B2 Major parks | 4 | 5 | 3 | 4 | Important green polygons don’t identify shaded paths or opening status. |
| B3 Drinking fountains | 4 | 5 | 4 | 4 | Irregular updates; confirm operation and type. |
| B4 Street slopes | 4 | 3 | 3 | 3 | Road slope not sidewalk condition; derived from 2019 terrain. |
| B5 Watercourses | 4 | 3 | 2 | 4 | Useful context, but nearby water does not prove cooler walking conditions. |
| E1 OSM network | 5 | 5 | 3 | 3 | Crowdsourced; connectivity/access tags need checking. |
| E2 Urban Atlas | 4 | 4 | 3 | 4 | 2021 product; count Brno features after download. |
| E3 Eurostat population grid | 4 | 3 | 3 | 4 | 1 km cells are coarse and use rules apply. |
| F1 Shade | 4 | 5 | 3 | 3 | Time-dependent observer estimate. |
| F2 Temperature | 3 | 5 | 3 | 3 | Sensor/weather/material errors; timestamp and protocol are essential. |
| F3 Rest places | 4 | 4 | 2 | 3 | Subjectivity and not enough sites in a tiny pilot. |

## 9. Suggested division of work

- **Data/GIS lead:** downloads, source and count log, clips and prepares the layers.
- **Fieldwork lead:** pilot boundary, shared survey forms, equipment and field schedule.
- **Design/story lead:** citizen interviews, six Figma screens, progress reports and slides.

All teammates should join fieldwork and understand the final map. Report real contributions, not planned percentages.

## 10. Your next actions

1. Tell your teammates Brno is the working city and agree on the small pilot area.
2. Download and open the **Pítka** GeoJSON in QGIS. Confirm the points are in Brno and write down the actual feature count. If you get stuck, share a screenshot or tell me what step you’re on and I’ll walk you through it.
3. Before full fieldwork, each teammate should independently rate shade at the same five locations. Compare your ratings; adjust the instructions until you agree on what “shade percentage” means.
4. Download the Brno Urban Atlas 2021 package and record its actual feature count.

### Sources checked

- [ENA-LS assignment PDF](ENA-LS_project_assigment.pdf)
- [Brno data portal and population](https://data.brno.cz/)
- [Brno thermal map](https://gis.brno.cz/mapa/teplotni-mapa/?c=-)
- [Brno Metropolitan Area climate analysis](https://metropolitni.brno.cz/brnenska-metropolitni-oblast-z-vesmiru-satelitni-data-ukazuji-jak-se-zmena-klimatu-projevi-v-brne-a-okoli-do-roku-2100/)
- [Brno green-space and sealed-surface analysis](https://data.brno.cz/pages/d8b691b7f84542bc88bf57cbb24ccfdc)
- [Greenery registry](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F541efa42b634116d1a2480a2cfc81bdc)
- [Major parks and green areas](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F4a98185bf27f80571428335224caf1b3)
- [Drinking fountains](https://data.gov.cz/zdroj/datov%C3%A9-sady/44992785/5968771279b379c4d461fe9b9bea3336)
- [Street slopes](https://data.gov.cz/datov%C3%A1-sada?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2Fef795a9a3fab0602c8918e38d1f20a34)
- [Watercourses](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F017158621a74c39f2a2fb2eac5472502)
- [Geofabrik Czech Republic OSM extract](https://download.geofabrik.de/europe/czech-republic.html)
- [Copernicus Urban Atlas 2021](https://land.copernicus.eu/en/products/urban-atlas/urban-atlas-2021) and [product documentation listing Brno FUA CZ002L2](https://library.land.copernicus.eu/products/Urban_Atlas_CLMS_UA2021_LULC_ATBD_v1.html)
- [Eurostat population grids](https://ec.europa.eu/eurostat/web/gisco/geodata/population-distribution/population-grids)
