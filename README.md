# Global Road and Trail Climb Database
This is a working project to calculate and document all significant hill/mountain climbs in the world. Main use is for cyclists or runners seeking out elevation gains.

## About
If you are unfamiliar with an area, and are an endurance athlete, you may seek out where the best climbs are for an area. This repository is a living database to calculate and attribute all significant hill/mountain climbs in the world, based on currently available OpenStreet Map data and opensource elevation data.

It gets both roads, greenways/paths, and any trails that are on openstreetmaps (OSM has a lot of public trails in it now).

## What defines a climb?
If the street name changes or the surface type changes, it is considered a new climb. This is an architectural decision to not have sprawling confusing climbs. There is a connected_climbs attribute to find and link up adjacent street climbs for a continued experience. Anything that continues on average to ascend up with that same street/trail name will be shown as a climb, until it descends from it's highest peak. So undulating roads that stay the same street name, as long as they are ehaded to their highest peak, are considered one continuous climb. The PDI scoring penalizes descents, so scores should be roughly accurate based on the overall challenge/effort of the climb even with some descents.

If you want to get stats for a part of the climb, the companion Climb Analyzer apps will crop the climb to your selected area to get stats for that portion.

## Scoring
Climbs are scored in one of three ways, depending on your goals. Generally, PDI will probably be the best score type to use:

### Basic Score
Distance = how far the climb goes uphill.
Average grade (%) = how steep it is on average.

A higher score means the climb is either very long, very steep, or both.

For example:
* A 5 km climb at 5% → 5,000 × 5 = 25,000
* A 10 km climb at 3% → 10,000 × 3 = 30,000
* A 2 km climb at 10% → 2,000 × 10 = 20,000

Even though the last one is steep, it’s short — so the total challenge is smaller.

### FIETS Score
The Fiets Index (developed by the Dutch cycling magazine Fiets). This weights the difficulty score based on the grade of the climb and the elevation of the climb, improving on the basic score.

The actual formula is: [H^2/D*10] + (T-1000:1000; but only if greater than 0)

H = ending elevation minus starting elevation in meters.
D = total distance traveled in meters.
T = Height in meters.
Note: Only add T-1000 if that number is greater than zero.

### PDI (PJAMM Difficulty Index) - default/preferred
The [PJAMM difficulty index](https://pjammcycling.com/blog/50.pjamm-difficulty-index) improves on the FIETS score by replacing elevation gain with total work completed, accounting for flat terrain resistance (wind and friction) in addition to overcoming gravity on ascents, and implements a penalty for descents that offer recovery.

## How is the data calculated?
Data is calculated from my open source application [Climb Analyzer](https://github.com/stevehollx/climb-analyzer/tree/main). It crowd-sources analysis, so as others analyze areas that haven't been analyzed before, it optionally posts the analysis to this repo for others to use without the storage/cpu/time requirements to calculate the analysis.

Current version is v2.2.2. Versions will update if i find defects in the data analysis code, but results test independently against a few other sources so it shouldn't change too much from here.

## How can I visualize this data
1. If you have an iPhone/iOS device, download the climb-analyzer companion iOS app. You can download and visualize climbs there on the go. You can't calculate new areas for climbs with this though.
2. If you need to generate analyses or don't have an iOS device, [Climb Analyzer](https://github.com/stevehollx/climb-analyzer/tree/main) has a GUI to visualize the climbs. The app runs on a linux/macos computer, or should also run in Windows with WSL. 

<img src="https://github.com/stevehollx/global-road-and-trail-climbs/blob/main/images/ios_map.png" alt="ios app map screenshot" width="30%"> <img src="https://github.com/stevehollx/global-road-and-trail-climbs/blob/main/images/ios_climb_info.png" alt="ios app climb info screenshot" width="30%"> 

## How to contribute?
Analysis takes time. I am just starting to run through processing what I can individually. As others use my app, it should hopefully accelerate completion of this database.

This goes much faster with some help, or if someone wants to donate some cloud computing. You can help by installing my climb analyzer app and running some full analysis (`./climb-analyzer -r "region name 1, region name 2"`) to post them to this repo. I will approve the merge requests for the data to then show up for eveyone to see in their apps.

Required criteria to post back is with these Climb Analyzer settings:
* Complete US state or country analysis. I'll accept subregions for large countries like russia and china, as I have a utility to merge roads that cross regions within a country.
* Includes analysis of all roads and trails, unfiltered.
* Do not filter out 'cycling only' climbs
* Use all 3 elevation datasets for perscribed by climb-analyzer's setup (dataset varies on region), or at least a submission with 0 elevation lookup errors (where possible with the available datasets)

# Future plans
It may be cool to run a delta of what trails are missing from OSM against what is in mtbproject / trailforks at some point in the future, and anlyze gpx from those trails to complete the trail climb data set. I do have a stash from about 2018 of all US gpx from those sites sitting on a drive somewhere. Not sure the benefit of what is in there and not in OSM though, so not a current focus and instead priority is getting a first run analysis of all global regions.

# Additional info
## Data in files
* Street Name - Some paths and trails don't have names so generic is used there.
* City
* State
* From Center (mi) - Distance from center of state
* Cycling - Is cycling allowed?
* Category - Cycling climb category (i.e. like what is used in cycling Grand Tours; HC, Cat1-4)
* Basic Score - Distance * Average grade
* FIETS Score - Weighted elevation score
* PDI Score - More advanced elevation score from PJAMM
* Elev Gain (ft) - Total elevation gained
* Height (ft) - Highest point of the climb
* Prominence (ft) - Height from start of the climb to the top
* Length (mi) - Total length of the climb
* Avg Grade (%)
* Max Grade (%)
* Highway Type - Classifies the road type, based on OpenStreetMap attributes.
* Surface - Paved, asphalt, gravel, dirt, etc.
* Tracktype - Where available the type of trail is described (double track, single track, etc.)
* Way ID - The OpenStreetMap unique Way identified.
* OSM Link - Hyperlink to that climb's first segment in Open Street Maps
* Connected Climbs - Any additional climbs that connect to this one, such as if the street name changes at an intersection of a continued uphill.
* All Way IDs - The OSM way ids that make up the climb.

## Caveats
I merge climbs that traverse regions within a country (US is the best example; e.g. climbs that go from Oregeon into Idaho). For international climbs that cross country boundaries, those do not merge and stop at the border, unless they are countries in the EU that allow for passing between borders without customs checks AND if the climb is still ascending (rare at borders).

# License
## 📝 License & Attribution

This dataset is licensed under the [Open Database License (ODbL) v1.0](./LICENSE).  
You are free to share and adapt this data, as long as you:
- Attribute the original sources (see below),
- Keep derivative databases under ODbL,
- Clearly indicate if changes were made.

**Attribution:**  
- Most elevation data is derived from © NASA SRTM and USGS NED (public domain)
- Some elevation data based on coverage needs is derived from NASA/METI ASTER or PGC ARCTICDEM.
- Road and base map data © OpenStreetMap contributors, ODbL 1.0  
- Climb list (this repo's results content) Copyright © 2025 Steve Holl

> ⚠️ While commercial use is permitted under ODbL, we kindly ask that commercial entities
> contact me before redistributing this dataset as part of a paid product, and acknlowedgement/credits
> to me are required on any intergrations or implementations.
