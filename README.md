# Global Road and Trail Climb Database
This is a working project to calculate and document all significant hill/mountain climbs in the world. Main use is for cyclists or runners seeking out elevation gains.

## About
If you are unfamiliar with an area, and are an endurance athlete, you may seek out where the best climbs are for an area. This repository is a living database to calculate and attribute all significant hill/mountain climbs in the world, based on currently available OpenStreet Map data and opensource elevation data.

It gets both roads, greenways/paths, and any trails that are on openstreetmaps (OSM has a lot of public trails in it now).

If the street name changes or the surface type changes, it is considered a new climb. This is an architectural decision to not have sprawling confusing climbs. There is a connected_climbs attribute to find and link up adjacent street climbs for a continued experience.

## Criteria
To prevent this from containing all flat roads across the world, the list is filtered to a climb score of > 6000, as derived by Distance (meters) × Average Grade (%).

This gives a single number that reflects how long and steep a climb is.

Distance = how far the climb goes uphill.
Average grade (%) = how steep it is on average.

A higher score means the climb is either very long, very steep, or both.

For example:
* A 5 km climb at 5% → 5,000 × 5 = 25,000
* A 10 km climb at 3% → 10,000 × 3 = 30,000
* A 2 km climb at 10% → 2,000 × 10 = 20,000

Even though the last one is steep, it’s short — so the total challenge is smaller.
👉 This makes it easy to compare different climbs, no matter where they are.

So short, gentle hills don’t make the list — only climbs that are significant enough to be interesting for cyclists runners, etc. Roughly a ~3+ minute long climb on a bike should make the list.

## How is the data calculated?
Data is calculated from my open source application [Climb Analyzer](https://github.com/stevehollx/climb-analyzer/tree/main). It crowd-sources analysis, so as others analyze areas that haven't been analyzed before, it optionally posts the analysis to this repo for others to use without the storage/cpu/time requirements to calculate the analysis.

## How to contribute?
Analysis takes time. I am just starting to run through processing what I can individually. As others use my app, it should hopefully accelerate completion of this database.

This goes much faster with some help, or if someone wants to donate some cloud computing. You can help by installing my climb analyzer app and running some analysis and posting them back here. Mark your name down in the `./registry.csv` to sign up for processing a country/state, and then post it back up here.

Required criteria to post back is with these Climb Analyzer settings:
* Complete US state or country analysis. I'll accept subregions for large countries like russia and china, as I have a utility to merge roads that cross regions within a country.
* Filtered got basic climb score of 0.
* Do not filter out 'cycling only' climbs
* Use all 3 datasets for elevation perscribed by climb-analyzer's setup (dataset varies on region)

# Future plans
I may build a cloud webapp to interface with this data in a nicer UI, once we get enough processed data. Looking for cloud compute donations for that, as it will cost some money to host and serve.

It may be cool to run a delta of what trails are missing from OSM against what is in mtbproject / trailforks at some point in the future, and anlyze gpx from those trails to complete the trail climb data set. I do have a stash from about 2018 of all US gpx from those sites sitting on a drive somewhere. So that is my next goal with this project.

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
* OSM Link - Hyperlink to that segments Open Street map page
* Connected Climbs - Any additional climbs that connect to this one, such as if the street name changes at an intersection of a continued uphill.

## Caveats
I merge climbs that traverse regions within a country (US is the best example; e.g. climbs that go from Oregeon into Idaho). For international climbs that cross country boundaries, I think it is best to keep those split, so you know that you may be crossing a customs boundary.

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
- Climb list © 2025 Steve Holl

> ⚠️ While commercial use is permitted under ODbL, we kindly ask that commercial entities
> contact us before redistributing this dataset as part of a paid product.
