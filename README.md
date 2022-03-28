# bcdams

------

*This repository is no longer mainatained. See the [Canadian Aquatic Barriers Database](https://cwf-fcf.org/en/explore/fish-passage/aquatic-barrier-database.html) for an aggregated collection of dam point locations in BC, or refer to the list of data sources below.*

------
A geojson collection of point features for locations of BC dams, manually compiled from several data sources by Canadian Wildlife Federation for fish passage modelling.
Includes attributes noting if a dam is a hydro power facility and if it is a barrier to fish passage.



## Method

### Load data, identify duplicates

- locations of BC Dams Layer were compiled using the seven distinct source datasets noted below
- features classified as manmade dam structures were included
- data provided as line (i.e., BC Dams, NHN, and CanVec) or polygon (i.e., NHN and CanVec) features were converted into point features
- each source dataset was inspected using a 100-m tolerance to identify and flag potential duplicates
- flagged records were manually verified using satellite imagery and duplicates were deleted
- in the case of duplicates, the record with the most descriptive attributes was retained based on the priority order listed below

### Identify hydro dams

Manual QA/QC was performed on the combined features using a [list of BC Hydro facilities](https://www.bchydro.com/energy-in-bc/operations/our-facilities.html). This process involved online research with information taken from both white and grey literature, utilizing the BC water license search tool and investigation of satellite imagery to identify/verify the location of all hydro facility structures (e.g. dams and intakes). 139 structures were identified and merged into the existing dam layer where necessary.

### Identify fish passage status

Fishway data obtained from the [CanFishPass database](http://www.fecpl.ca/projects/canfishpass-inventory-of-canadian-fish-passage-facilities/) and BC Hydro was incorporated to identify barriers that employ fish passage measures, and consequently are not considered to be barriers to fish.


## Spatial data sources

1. B.C. Dams (`WHSE_WATER_MANAGEMENT.WRIS_DAMS_PUBLIC_SVW`)

    A provincial-scale dataset that contains the location of barriers classified as dams within BC. Published by the British Columbia Ministry of Forests, Lands, Natural Resource Operations and Rural Development – Water Management. Licensed under Open Government License – British Columbia.

    For more information:
    [https://catalogue.data.gov.bc.ca/dataset/b-c-dams](https://catalogue.data.gov.bc.ca/dataset/b-c-dams)

2.  BC Public Dams KML (`BC Public Dams Database`)

    A provincial scale dataset very similar to BC Dams above, consisting of barriers classified as a dam. Published by the British Columbia provincial government.

    The KMZ is available [for download](https://www2.gov.bc.ca/assets/gov/farming-natural-resources-and-industry/natural-resource-use/land-water-use/water-use/dam-safety/dams-public-20140626-2.kmz)

3.  Provincial Obstacles to Fish Passage (`FISS Database`)

    A provincial-scale dataset that contains all known obstacles to fish passage from several fisheries datasets. Records from the following datasets have been included: The Fisheries Information Summary System (FISS); the Fish Habitat Inventory and Information Program (FHIIP); the Field Data Information System (FDIS) and the Resource Analysis Branch (RAB) inventory studies. This dataset provides information on the following manmade barrier types: Dam, Dam – Unknown Origin, Fisheries Management Dam, Hydro Dam, Irrigation District Dam, Private Dam, Regional District Dam, Water Management Storage Dam, Pump, Velocity Barrier, Culvert, Weir, Wedge. Published by the British Columbia Ministry of Environment and Climate Change Strategy – Knowledge Management. Licensed under Open Government License – British Columbia.

    For more information:
    [https://catalogue.data.gov.bc.ca/dataset/provincial-obstacles-to-fish-passage](https://catalogue.data.gov.bc.ca/dataset/provincial-obstacles-to-fish-passage)

4.  Freshwater Atlas Obstructions (`WHSE_BASEMAPPING.FWA_OBSTRUCTIONS_SP`)

    A provincial-scale dataset that consists of natural obstacles and dams that act as barriers to fish passage. Published by the British Columbia Ministry of Forests, Lands, Natural Resource Operations and Rural Development - GeoBC. Licensed under Open Government License - British Columbia.

    For more information:
    [https://catalogue.data.gov.bc.ca/dataset/freshwater-atlas-obstructions](https://catalogue.data.gov.bc.ca/dataset/freshwater-atlas-obstructions)

5.  Global Reservoir and Dam Database (`GRanD_Dams_Database`)

    A global-scale dataset that contains data on known large dams and associated reservoirs. Now managed by McGill University, this dataset is a product of the Global Water System Project; assembled from numerous sources by eleven participating institutions. Published by Global Dam Watch.

    For more information:
    [http://globaldamwatch.org/data/#core_global](http://globaldamwatch.org/data/#core_global)

6.  National Hydrography Network (`NHN_Barriers_ManmadeType_1`)

    A national-scale dataset that contains lakes, reservoirs, watercourses (rivers and streams), canals, islands, drainage linear network, toponyms or geographical names, constructions and manmade and natural obstacles related to surface waters, etc. The NHN comprises the following manmade obstacles to fish passage: dams, wharfs, breakwaters, dikes/levees and lock gates. NHN Work Unit Limits were created based on Water Survey of Canada Sub-Sub-Drainage Area. Published by Natural Resources Canada. Licensed under Open Government License – Canada.

    For more information:
    [http://ftp.maps.canada.ca/pub/nrcan_rncan/vector/geobase_nhn_rhn/doc/](http://ftp.maps.canada.ca/pub/nrcan_rncan/vector/geobase_nhn_rhn/doc/)

7.  CanVec Manmade Features (`CanVec_Manmade_Features`)

    A national scale dataset that contains dams, protection structures (breakwater, dike/levees), liquid storage facilities (basin, swimming pool, etc.), tanks, buildings, delimiting structures (fence, walls, etc.), landmark features (cross, radar, crane, forts, etc.), chimneys, towers, sewage pipelines, conduit bridges, waste, leisure areas, residential areas, commercial and institutional areas and ritual cultural areas (shrine, cemeteries, etc.) provided as separate spatial layers. Published by Natural Resources Canada. Licensed under Open Government License – Canada.

    For more information:
    [https://open.canada.ca/data/en/dataset/fd4369a4-21fe-4070-914a-067474da0fd6?wbdisable=true](https://open.canada.ca/data/en/dataset/fd4369a4-21fe-4070-914a-067474da0fd6?wbdisable=true)

## Attributes

| column | description  |
|----------|-------------|
| `bcdams_id`      | Unique identifier |
| `source_dataset` | Name of database used as source for the dam location, see data sources for a full list of possible values |
| `source_id`      | From source database, value of unique identifier |
| `dam_name`       | From source database, name of dam  |
| `waterbody_name` | From source database, name of the lake/reservior/river associated with the dam (type of feature varies according to source) |
| `owner`          | From source database, name of the owner of the dam (where available) |
| `hydro_dam_ind` | Indicates whether the dam/structure is associated with a hydro facility (yes = Y; no = N). |
| `barrier_ind`   | Indicates whether the structure associated with the record acts as a barrier to fish (yes = Y; no = N). Records with a value of ‘N’ are structures that are known to have fish passage measure in place (i.e. Pool and Weir, Pool and Weir with Hole, Vertical Shot, Denil, Trap and Truck, Nature-like fishway) and therefore are not represented in the dataset as a barrier to fish. |

## Caveats

Duplicate records still exist within the dataset - further manual QA/QC is required.
