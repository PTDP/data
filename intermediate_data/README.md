# How we join Scraped Facilities with Canonical Facilities
In order to find to join facilties we scrape from vendors with those facilties as they exist in other datasets like [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) , we follow three steps:
1) Geocode facilties using the Google Places API
2) Based on the geocoding, and fuzzy matches between the scraped facility name, and names that exist in order data sets, programmatically join
3) Manually validate the results of step 2, providing overridden information when necessary.

The final output of step 3 represents the facilities as they appear in PTDP's data products for external consumption.