# CoolRoute Brno

Heat-Aware Pedestrian Navigation in Brno, Czechia

Location-based service that helps pedestrians find walking routes with lower heat exposure during hot weather. It will compare a shortest walking route with an alternative that considers observed shade, drinking-water access, places to rest, and possibly steepness. Present the result as a heat-aware estimate, not a guarantee of the coolest route. Brno is the selected city; a compact central pilot area is a starting option.

## Data

The first part is aimed at working with GIS data that will be part of the LBS.

The proposed location-based service will:

* Use at least 5 datasets from the official city data portal. You must choose a city that has a data portal, [data.Brno](https://data.brno.cz/):
  * [Greenery registry — green surfaces](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F541efa42b634116d1a2480a2cfc81bdc) (*Pasport zeleně – plochy zeleně*).
  * [Major parks and green areas](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F4a98185bf27f80571428335224caf1b3) (*Významné plochy zeleně*).
  * [Drinking fountains](https://data.brno.cz/datasets/mestobrno::p%C3%ADtka-drinking-fountains) (*Pítka*).
  * [Street slopes](https://data.gov.cz/datov%C3%A1-sada?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2Fef795a9a3fab0602c8918e38d1f20a34) (*Sklony komunikací*).
  * [Watercourses](https://data.gov.cz/dataset?iri=https%3A%2F%2Fdata.gov.cz%2Fzdroj%2Fdatov%C3%A9-sady%2F44992785%2F017158621a74c39f2a2fb2eac5472502) (*Vodní toky*).

* Use at least 3 other datasets for different sources. Each dataset must have at least 20 features:
  * [OpenStreetMap pedestrian network](https://download.geofabrik.de/europe/czech-republic.html) for routing, using the Geofabrik Czech Republic extract.
  * [Copernicus Urban Atlas 2021](https://land.copernicus.eu/en/products/urban-atlas/urban-atlas-2021) land-cover data for the Brno functional urban area.
  * [Eurostat 2021 population grid](https://ec.europa.eu/eurostat/web/gisco/geodata/population-distribution/population-grids) for broad population context.

* Use at least three data sets created by team members. Each dataset must have at least 20 features. These datasets are primary data sources, not derived from the first two datasets:
  * Direct observations of shade along sidewalks, with location and observation time.
  * Field measurements of air and/or surface temperature, using a documented and consistent method.
  * A field inventory of public resting places, with shared criteria for seating and observed shade.

Verify that each candidate dataset is available and suitable before counting it toward the requirements. Record its source, license, date, CRS, coverage, and actual feature count. Keep observed measurements separate from proxies such as tree cover or land use; those proxies do not directly measure route temperature or shade. See [research.md](../research.md) and [results.md](../results.md) for dataset verification and analysis guidance.

### How to obtain the datasets

1. **Brno datasets:** open each catalogue link above, find its download/distribution section, and download a GIS file such as GeoJSON or GeoPackage. If a catalogue record only describes a service, follow its distribution link and check that the data can be downloaded. Save the original files and note the download date and license.
2. **OpenStreetMap:** open the [Geofabrik Jihomoravský kraj page](https://download.geofabrik.de/europe/czech-republic/jihomoravsky.html), choose the current `free.gpkg.zip`, unzip it, and add the GeoPackage in QGIS. Use the roads/paths layer and inspect its pedestrian-related attributes. The regional extract is smaller than the whole-Czechia file and covers Brno.
3. **Urban Atlas:** open the [Copernicus Urban Atlas dataset page](https://land.copernicus.eu/en/products/urban-atlas?tab=datasets), select the Urban Atlas Land Cover/Land Use 2021 product, then use its download option to obtain the Brno functional urban area (FUA code CZ002L2). If prompted, sign in to Copernicus Data Space. Unzip the downloaded package and add its vector layer to QGIS.
4. **Eurostat population grid:** open the [Eurostat population grids page](https://ec.europa.eu/eurostat/web/gisco/geodata/population-distribution/population-grids), choose the 2021 census grid and download the GeoPackage ZIP. Unzip and open it in QGIS; the grid uses EPSG:3035. Select the cells covering the study area. Read and follow the download/use conditions on the page.
5. **Team field data:** agree on the observation form and collection method first. Record each observation as a separate feature with a unique ID, location, date/time, and the required measurements or attributes. Export each layer from QGIS as GeoJSON.

For every downloaded or collected dataset, open it in QGIS, check that it appears in the correct place, inspect its attribute table, and record the actual feature count. Keep the original download unchanged; make clipped or cleaned copies for analysis. Ask for help with one source at a time if a download page or QGIS step is confusing.

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
