# CoolRoute Brno

Heat-Aware Pedestrian Navigation in Brno, Czechia

## Team Members

* [Dominik Jakubec](https://is.mendelu.cz/auth/lide/clovek.pl?id=100907;) (`xjakubec`)
* [Jiří Kužel](https://is.mendelu.cz/auth/lide/clovek.pl?id=100910;) (`xkuzel`)
* [Vojtěch Střílka](https://is.mendelu.cz/auth/lide/clovek.pl?id=100912;) (`xstrilka`)

## Project Description

Location-based service that helps pedestrians find walking routes with lower heat exposure during hot weather. The service will compare the shortest walking route with an alternative one that considers visible overhead cover, drinking-water access, places to rest and route steepness.

## Data

The first part is aimed at working with GIS data that will be part of the LBS.

### Official City Data Portal

Use at least 5 datasets from the official city data portal.

Datasets from the official city data portal ([data.brno.cz](https://data.brno.cz/)):

- [Chodníky / Sidewalks](https://data.brno.cz/datasets/mestobrno::chodn%C3%ADky-sidewalks/about)
- [Pasport zeleně - plochy zeleně / Greenery registry - green surfaces](https://data.brno.cz/datasets/mestobrno::pasport-zelen%C4%9B-plochy-zelen%C4%9B-greenery-registry-green-surfaces/about)
- [Pasport zeleně - stromy, keře / Greenery registry - trees, bushes](https://data.brno.cz/datasets/mestobrno::pasport-zelen%C4%9B-stromy-ke%C5%99e-greenery-registry-trees-bushes/about)
- [Pasport zeleně - technické prvky / Greenery registry - technical equipment](https://data.brno.cz/datasets/mestobrno::pasport-zelen%C4%9B-technick%C3%A9-prvky-greenery-registry-technical-equipment/about)
- [Pítka / Drinking fountains](https://data.brno.cz/datasets/mestobrno::p%C3%ADtka-drinking-fountains/about)
- [Přechody / Pedestrian crossings](https://data.brno.cz/datasets/mestobrno::p%C5%99echody-pedestrian-crossings/about)
- [Vodní toky / Watercourses](https://data.brno.cz/datasets/mestobrno::vodn%C3%AD-toky-watercourses/about)
- [Průměrné aktuální teploty vzduchu / Average air temperatures NOVÉ](https://datahub.brno.cz/datasets/mestobrno::pr%C5%AFm%C4%9Brn%C3%A9-aktu%C3%A1ln%C3%AD-teploty-vzduchu-average-air-temperaturatures-nov%C3%A9/about)

### Different Sources

Use at least 3 datasets from different sources. Each dataset must have at least 20 features.

* [Mobiliář městských částí - Nábytek a vybavení / Municipal furniture](https://gis.brno.cz/ost/edas/public/99620902-b124-46a1-9d96-dd1b03bed311)
* [Building footprints / Budovy, layer: 334](https://gis.brno.cz/ags3/rest/services/PUBLIC/basemap_brno_zakladni_mapa_seda_3D_tiled/MapServer/334/)

  Obtain the specifically queried data [here](https://gis.brno.cz/ags3/rest/services/PUBLIC/basemap_brno_zakladni_mapa_seda_3D_tiled/MapServer/334/query?where=1%3D1&text=&objectIds=&time=&timeRelation=esriTimeRelationOverlaps&geometry=&geometryType=esriGeometryEnvelope&inSR=&spatialRel=esriSpatialRelIntersects&distance=&units=esriSRUnit_Foot&relationParam=&outFields=*&returnGeometry=true&returnTrueCurves=false&maxAllowableOffset=&geometryPrecision=&outSR=4326&havingClause=&returnIdsOnly=false&returnCountOnly=false&orderByFields=&groupByFieldsForStatistics=&outStatistics=&returnZ=false&returnM=false&gdbVersion=&historicMoment=&returnDistinctValues=false&resultOffset=&resultRecordCount=&returnExtentOnly=false&sqlFormat=none&datumTransformation=&parameterValues=&rangeValues=&quantizationParameters=&uniqueIds=&returnUniqueIdsOnly=false&featureEncoding=esriDefault&f=geojson)

  Save it in the JSON viewer (Ctrl + S) in a GeoJSON.

* [Elevation contour lines / ZABAGED® – Výškopis – vrstevnice](https://ags.cuzk.gov.cz/arcgis/rest/services/ZABAGED_VRSTEVNICE/MapServer/0/)

  Obtain the specifically queried data [here](https://ags.cuzk.gov.cz/arcgis/rest/services/ZABAGED_VRSTEVNICE/MapServer/0/query?where=1%3D1&text=&objectIds=&time=&timeRelation=esriTimeRelationOverlaps&geometry=16.58%2C49.18%2C16.63%2C49.22&geometryType=esriGeometryEnvelope&inSR=4326&spatialRel=esriSpatialRelIntersects&distance=&units=esriSRUnit_Foot&relationParam=&outFields=*&returnGeometry=true&returnTrueCurves=false&maxAllowableOffset=&geometryPrecision=&outSR=4326&havingClause=&returnIdsOnly=false&returnCountOnly=false&orderByFields=&groupByFieldsForStatistics=&outStatistics=&returnZ=false&returnM=false&gdbVersion=&historicMoment=&returnDistinctValues=false&resultOffset=&resultRecordCount=&returnExtentOnly=false&sqlFormat=none&datumTransformation=&parameterValues=&rangeValues=&quantizationParameters=&uniqueIds=&returnUniqueIdsOnly=false&featureEncoding=esriDefault&f=geojson)

  Save it in the JSON viewer (Ctrl + S) in a GeoJSON.

* [human-settlement.emergency.copernicus.eu](https://human-settlement.emergency.copernicus.eu) — [GHS-BUILT-H - R2023A](https://human-settlement.emergency.copernicus.eu/ghs_buH2023.php)

* Query all pedestrian footways in Brno at [Overpass Turbo](https://overpass-turbo.eu)

  Head over to Overpass Turbo and run the following query:

  ```overpass
  [out:json][timeout:180];

  area["name"="Brno"]
      ["boundary"="administrative"]
      ["admin_level"="8"]->.brno;

  way["highway"="footway"](area.brno);

  out geom;

  ```

  Then just download the data in GeoJSON format via Export button.

### Custom Datasets

Use at least 3 datasets created by team members. Each dataset must have at least 20 features.

Datasets created by team members independently of the datasets mentioned above:

- **Resting objects:** Publicly accessible seating locations, including seating type, presence of a backrest, and visible overhead cover. These locations should help users find places to take a break along a route.

  **Fields:**

  - `id` (long)
  - `date_time` (datetime)
  - `object_type` (text -- e.g., bench, chair, picnic table)
  - `backrest` (bool)
  - `covered` (bool)
  - `cover_type` (text -- e.g., none, trees, roof, mixed)
  - `notes` (text)
- **Public indoor refuges:** Indoor locations where pedestrians can take a break from direct sunlight without making a purchase, such as publicly accessible libraries or shopping centres. The dataset should contain verified opening hours, access restrictions, and seating availability. These locations will be presented as potential refuges from the heat.

  **Fields:**

  - `id` (long)
  - `date_time` (datetime)
  - `refuge_type` (text -- e.g., library, shopping centre)
  - `opening_hours` (text -- e.g., Mon--Fri 09:00--18:00)
  - `access_restrictions` (text -- e.g., none, registration required)
  - `seating` (bool)
  - `notes` (text)
- **Stair sets:** Distinct publicly accessible stair flights or connected stair sets, with step count, handrail presence, overhead cover, and availability of a step-free alternative. Stairs add physical effort. These records should help users choose less strenuous walking routes during hot weather.

  **Fields:**

  - `id` (long)
  - `date_time` (datetime)
  - `step_count` (long)
  - `handrail` (bool)
  - `overhead_cover` (text -- e.g., none, trees, roof, mixed)
  - `step_free_alternative` (text -- e.g., yes, no, unknown)
  - `notes` (text)

## Application Design

The second part is the design of the LBS in Figma. The design can be either a web or mobile application.

The requirements for the application:

* At least 6 screens.
* Use the data used in the Data part of this assignment.
* Be available for citizens; this is not an application for city officials.

Possible screens include a map, origin and destination selection, route comparison, route details and score explanation, nearby fountains/resting places, and field observation submission or review.

## The Final Project

The final project will consist of:

* ArcGIS Online map(s) representing the final analysis and project output.
* A web application showing an ArcGIS Online map, built using Experience Builder.
* Anything else you want to add (other maps, dashboards, StoryMap, etc.).
* Datasets in SHP or GeoJSON format.
* Figma design of the web or mobile application, with a public link to the design.
* A PowerPoint presentation describing the proposed LBS and the results.

## Schedule

* **2026/10/18 20:00** — Project proposition with the names of the three team members. Include at least 20 lines describing the problem, the idea behind the application, the data used, and how it will benefit citizens.
* **Week from 2026/10/19** — Mandatory consultation during lecture/seminars; report what has been done so far.
* **2026/11/08 20:00** — Progress report, mainly describing the data used and the reasoning behind dataset choices.
* **Week from 2026/11/06** — Mandatory consultation during lecture/seminars; report what has been done so far.
* **2026/12/07 20:00** — Progress report on work completed since the previous report.
* **Last week of the semester** — Final project presentations.

> Each report must contain the team-member list and each member’s percentage of work completed on the project so far.
