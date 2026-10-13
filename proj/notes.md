# CoolRoute Brno

Heat-Aware Pedestrian Navigation in Brno, Czechia

Location-based service that helps pedestrians find walking routes with lower heat exposure during hot weather. It will compare a shortest walking route with an alternative that considers observed shade, drinking-water access, places to rest, and possibly steepness. Present the result as a heat-aware estimate, not a guarantee of the coolest route. Brno is the selected city; a compact central pilot area is a starting option.

## Data

The first part is aimed at working with GIS data that will be part of the LBS.

The proposed location-based service will:

* Use at least 5 datasets from the official city data portal. You must choose a city that has a data portal. Since we are focused on Brno, we use datasets of Statutární město Brno - Magistrát města Brna - Otevřená data from [data.Brno](https://data.brno.cz/):
  * [Chodníky / Sidewalks](https://data.brno.cz/datasets/mestobrno::chodn%C3%ADky-sidewalks/about)
  * [Přechody / Pedestrian crossings](https://data.brno.cz/datasets/mestobrno::p%C5%99echody-pedestrian-crossings/about)
  * [Pítka / Drinking fountains](https://data.brno.cz/datasets/mestobrno::p%C3%ADtka-drinking-fountains/about)
  * [Pasport zeleně - stromy, keře / Greenery registry - trees, bushes](https://data.brno.cz/datasets/mestobrno::pasport-zelen%C4%9B-stromy-ke%C5%99e-greenery-registry-trees-bushes/about)
  * [Pasport zeleně - plochy zeleně / Greenery registry - green surfaces](https://data.brno.cz/datasets/mestobrno::pasport-zelen%C4%9B-plochy-zelen%C4%9B-greenery-registry-green-surfaces/about)
  * [Pasport zeleně - technické prvky / Greenery registry - technical equipment](https://data.brno.cz/datasets/mestobrno::pasport-zelen%C4%9B-technick%C3%A9-prvky-greenery-registry-technical-equipment/about)
  * [Vodní toky / Watercourses](https://data.brno.cz/datasets/mestobrno::vodn%C3%AD-toky-watercourses/about)
  * [Průměrné aktuální teploty vzduchu / Average air temperaturatures NOVÉ](https://data.brno.cz/datasets/mestobrno::pr%C5%AFm%C4%9Brn%C3%A9-aktu%C3%A1ln%C3%AD-teploty-vzduchu-average-air-temperaturatures-nov%C3%A9/about)

* Use at least 3 other datasets for different sources. Each dataset must have at least 20 features:
  * [Mobiliář městských částí - Nábytek a vybavení / Municipal furniture](https://gis.brno.cz/ost/edas/public/99620902-b124-46a1-9d96-dd1b03bed311)
  * [Building footprints / Budovy, layer: 334](https://gis.brno.cz/ags3/rest/services/PUBLIC/basemap_brno_zakladni_mapa_seda_3D_tiled/MapServer/334/)

    Obtain the specifically queried data [here](https://gis.brno.cz/ags3/rest/services/PUBLIC/basemap_brno_zakladni_mapa_seda_3D_tiled/MapServer/334/query?where=1%3D1&text=&objectIds=&time=&timeRelation=esriTimeRelationOverlaps&geometry=&geometryType=esriGeometryEnvelope&inSR=&spatialRel=esriSpatialRelIntersects&distance=&units=esriSRUnit_Foot&relationParam=&outFields=*&returnGeometry=true&returnTrueCurves=false&maxAllowableOffset=&geometryPrecision=&outSR=4326&havingClause=&returnIdsOnly=false&returnCountOnly=false&orderByFields=&groupByFieldsForStatistics=&outStatistics=&returnZ=false&returnM=false&gdbVersion=&historicMoment=&returnDistinctValues=false&resultOffset=&resultRecordCount=&returnExtentOnly=false&sqlFormat=none&datumTransformation=&parameterValues=&rangeValues=&quantizationParameters=&uniqueIds=&returnUniqueIdsOnly=false&featureEncoding=esriDefault&f=geojson)

    Save it in the JSON viewer (Ctrl + S) in a GeoJSON.

  * [Elevation contour lines / ZABAGED® – Výškopis – vrstevnice](https://ags.cuzk.gov.cz/arcgis/rest/services/ZABAGED_VRSTEVNICE/MapServer/0/)

    Obtain the specifically queried data [here](https://ags.cuzk.gov.cz/arcgis/rest/services/ZABAGED_VRSTEVNICE/MapServer/0/query?where=1%3D1&text=&objectIds=&time=&timeRelation=esriTimeRelationOverlaps&geometry=16.58%2C49.18%2C16.63%2C49.22&geometryType=esriGeometryEnvelope&inSR=4326&spatialRel=esriSpatialRelIntersects&distance=&units=esriSRUnit_Foot&relationParam=&outFields=*&returnGeometry=true&returnTrueCurves=false&maxAllowableOffset=&geometryPrecision=&outSR=4326&havingClause=&returnIdsOnly=false&returnCountOnly=false&orderByFields=&groupByFieldsForStatistics=&outStatistics=&returnZ=false&returnM=false&gdbVersion=&historicMoment=&returnDistinctValues=false&resultOffset=&resultRecordCount=&returnExtentOnly=false&sqlFormat=none&datumTransformation=&parameterValues=&rangeValues=&quantizationParameters=&uniqueIds=&returnUniqueIdsOnly=false&featureEncoding=esriDefault&f=geojson)

    Save it in the JSON viewer (Ctrl + S) in a GeoJSON.

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

* Use at least three data sets created by team members. Each dataset must have at least 20 features. These datasets are primary data sources, not derived from the first two datasets:

  * Direct observations of shade along sidewalks, with location and observation time.

    * **Fields:** `obs_id`, `observer`, `date_time`, `shade_pct`, `sky`, `sidewalk_segment_m`, `photo_id`, `notes`. At each station estimate shaded share of the next fixed 10 m of walkable sidewalk. Face the direction of travel and use the same rule.
    * **Equipment / time:** Phone GPS/camera, shared form; about 2–3 hours for 60 points plus travel. 
    * **Common errors and controls:** Observer judgment, cloud/time change, GPS drift. Use fixed segment length, same time window, and review photos together.

  * Field measurements of air and/or surface temperature, using a documented and consistent method.

    * **Fields:** `obs_id`, `observer`, `date_time`, `air_c`, `surface_c`, `surface_type`, `shade_state`, `sensor_height_m`, `instrument`, `sky`, `notes`. Measure air in shade at a consistent 1.2–1.5 m height; measure surface at a marked material and note shade.
    * **Equiment / time:** Thermometer; ideally an IR thermometer for surfaces; phone GPS. About 3–4 hours. Record make/model and compare instruments before the walk.
    * **Common errors and controls:** Sensor heated by sun, IR angle/emissivity, different surfaces, weather changes. Timestamp every record and avoid comparing readings taken hours apart as if simultaneous.

  * A field inventory of public resting places, with shared criteria for seating and observed shade.

    * **Fields:** `site_id`, `observer`, `date_time`, `seat_type`, `seats_n`, `shade_now`, `backrest`, `armrest`, `step_free_approach`, `condition`, `comfort_1_5`, `photo_id`, `notes`. Use a shared definition of public access and a short written 1–5 comfort rubric.
    * **Equipment / time:** Phone GPS/camera, checklist; about 2–3 hours.
    * **Common errors and controls:** Subjective comfort and temporary obstructions. Use identical rubric and don’t photograph identifiable people. Expand the pilot if fewer than 20 distinct sites exist.

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
