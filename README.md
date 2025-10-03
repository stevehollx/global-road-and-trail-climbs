# Global Road and Trail Climb Database
This is a working project to calculate and document all significant hill/mountain climbs in the world. Main us is for cyclists or runners seeking out elevation gains.

## About
If you are unfamiliar with an area, and are an endurance athlete, you may seek out where the best climbs are for an area. This repository is a living database to calculate and attribute all significant hill/mountain climbs in the world.

## Criteria
To prevent this from containing all flat roads across the world, the list is filtered to a climb score of > 6000, as derived by Distance (meters) × Average Grade (%).

This gives a single number that reflects how long and steep a climb is.

Distance = how far the climb goes uphill.
Average grade (%) = how steep it is on average.

A higher score means the climb is either very long, very steep, or both.

For example:
A 5 km climb at 5% → 5,000 × 5 = 25,000
A 10 km climb at 3% → 10,000 × 3 = 30,000
A 2 km climb at 10% → 2,000 × 10 = 20,000

Even though the last one is steep, it’s short — so the total challenge is smaller.
👉 This makes it easy to compare different climbs, no matter where they are.

So short, gentle hills don’t make the list — only climbs that are significant enough to be interesting for cyclists runners, etc. Roughly a ~3+ minute long climb on a bike should make the list.

## How is the data calculated?
Data is calculated from my open source application [Climb Analyzer](https://github.com/stevehollx/climb-analyzer/tree/main).

## How to contribute?
Analysis takes time. I am just starting to run through the United States a day at a time. I estimate this will complete around December 2025.

This would go much faster with some help, or if someone wants to donate some cloud computing.

Help contribute to the hive if you have a linux server and some basic IT chops. The app has a setup wizard and is pretty easy to run, but does require some linux and docker knowledge.

Want to help? Message me, or mark your name down in the registry.csv to sign up for processing a country/state, and then post it back up here. Required criteria to post back is with these Climb Analyzer settings:
* Complete US state or country analysis
* Filtered got basic climb score of > 6000
* Do not filter out 'cycling only' climbs
* Include reverse geocoding so we get the nearest city/state for the climb
* Use both SRTM + NED data in the US. For other countries, SRTM is fine as long as it isn't for Russia, Canada, Greenland, Sweden, Norway, Finland, Iceland, Antarctica, or Alaska. Those areas will need ASTER or ARCTIC30m data. It would be ideal to have ASTER30m loaded as a fallback for SRTM data if analyzing outside of the US for beter accuracy.
* Please name the file with the elevation data used, e.g. france-srtm30m.xlsx
* Choosing to keep XLSX as the desired format for now. If we get results over the 65,535 Excel row limit, I may choose to switch everything to CSV, but I like the native filtering open.

# Future plans
I may build a webapp to interface with this data in a nicer UI, once we get enough data.

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
