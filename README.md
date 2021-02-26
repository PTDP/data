
![logo](logo.png)

# Prison Telecom Data Project

## Background 
The [Prison Telecom Data Project](https://prisontelecomdata.org), launched in January 2021, tracks the rates charged by prison telecom providers for their services, and changes to those rates over time. We started collecting data on traditional phone services in January 2021.

* **Latest data**: Our latest data on prison telecom rates is maintained in this repository. 

## Our Process  
Our dataset includes information on prison telecom rates scraped from the leading telecom service providers: ICS and Securus. We scrape, and normalize this data serveral times per month. Our scraper production code more detailed documentation are available on GitHub. 

In order to build a normalized data-set of facilities, we do some manual data cleaning, and manipulation. All such changes are committed to github, which represents our production data. We save all raw, un-normalized scraped data to long-lived cloud storage buckets.

We are continuously adding to and refining our scrapers. In production, we also join our telecom data with external facility-level data collected by the [UCLA COVID-19 Data Project](https://github.com/uclalawcovid19behindbars/data) in order provide a more expansive picture of conditions within a specific facility.

**Contributors**: You can see our [team page](https://prisontelecomdata.org/team) for an updated list of contributors. Please reach out at prison.telcom.data.project@gmail.com if you would like to contribute code, data, or time. We always welcome additional contributors! 

## Our Data 
Our core dataset includes the following metrics:

* Cumulative COVID-19 cases 
* Cumulative COVID-19 deaths 
* Active COVID-19 cases 
* COVID-19 tests administered 

We also collect additional information based on what agencies report (e.g. population data and vaccination data). While we aim to collect facility-level data, not all jurisdictions report COVID-19 metrics at the facility level. Some DOCs only report statewide totals, and others do not report any data for certain metrics. Authorities also vary dramatically in how they define the metrics that they report. We do our best to standardize these variables, but comparing data across jurisdictions and over time should be done with caution. 

**Note**: Because our data is scraped from private entities, it is updated and ammended on a schedule we do not control. Furthur, our data represents telecom rates as those entities report them publicly, rather than what rates are in practice.

## Data Dictionary 
We maintain two data tables. One represents `Rates`, and the other `Facilities`.

The full set of variables that we report includes the following: 

| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `Rate.ID`          | Integer ID that uniquely identifies every rate                                                                             |
| `Source`         | The URI from which each rate was scraped                                |
| `Duration.Initial`         | The billing period (seconds) at the beginning of a telecom service. For example, the first minute of a call.                       |
| `Duration.Additional`         | The billing increment following the `Duration.Initial`. For example, every minute following the first minute of a call.                      |
| `Amount.Initial`         | The amount (USD, cents) that a telecom service costs during the `Duration.Initial` period.                            |
| `Amount.Additional`         | The amount (USD, cents) that a telecom service costs during each `Duration.Additional` period.     
| `Amount.Tax`         | The percent tax applied to the sum of all billing line-items associated with the call itself. When not provided explicitly by a vendor, the tax percent is calculated from a given-tax line-item, and rounded to 2 significant digits.   
| `Phone`         | The phone number provided to the rate calculator.                              |
| `In.State`         | Boolean representing whether the origin phone number is located in the same state as the facility called.                              |
| `Facility`                | The unique facility ID associated with the rate. See the `Facility` table below.                                                                                            |
| `Scraped`                | An array of ISO Strings (UTC) representing each time a scraper encountered this unique rate. We consider a rate to be unique if any of the tracked variables (other than `Scraped`) are unique.                                                                                            |

| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `Facility.ID`          | Integer ID that uniquely identifies every facility                                                                             |
| `Jurisdiction`         | Whether the facility falls under `state`, `county`, `federal`, or `immigration` jurisdiction                                   |
| `State`                | State where the facility is located                                                                                            |
| ``                 | ISO Time name                                                                                                                  |
| `Date`                 | Date data was scraped (not necessarily date updated by the reporting source)                                                   |  
| `Source`               | Source from which the data was scraped                                                                                         |
| `Residents.Confirmed`  | Cumulative number of incarcerated individuals infected with COVID-19                                                           |
| `Staff.Confirmed`      | Cumulative number of staff infected with COVID-19                                                                              |
| `Residents.Deaths`     | Cumulative number of incarcerated individuals who died from COVID-19                                                           |
| `Staff.Deaths`         | Cumulative number of staff who died from COVID-19                                                                              |
| `Residents.Recovered`  | Cumulative number of incarcerated individuals who recovered from COVID-19                                                      |
| `Staff.Recovered`      | Cumulative number of staff who recovered from COVID-19                                                                         |
| `Residents.Tadmin`     | Cumulative number of COVID-19 tests administered to incarcerated individuals                                                   |
| `Staff.Tested`         | Cumulative number of staff tested for COVID-19                                                                                 |
| `Residents.Negative`   | Cumulative number of incarcerated individuals who tested negative for COVID-19                                                 |
| `Staff.Negative`       | Cumulative number of staff who tested negative for COVID-19                                                                    |
| `Residents.Pending`    | Number of incarcerated individuals currently with pending test results for COVID-19                                            |
| `Staff.Pending`        | Number of staff currently with pending test results for COVID-19                                                               |
| `Residents.Quarantine` | Number of incarcerated individuals currently in quarantine from COVID-19                                                       |
| `Staff.Quarantine`     | Number of staff currently in quarantine from COVID-19                                                                          |
| `Residents.Active`     | Number of incarcerated individuals currently infected with COVID-19                                                            |
| `Population.Feb20`     | Population of the facility as close to February 1, 2020 as possible                                                            |
| `Residents.Population` | Current population of incarcerated individuals reported by agency website                                                      |
| `Residents.Tested`     | Cumulative number of incarcerated individuals tested for COVID-19                                                              |
| `Residents.Initiated`  | Cumulative number of incarcerated individuals who have initiated COVID-19 vaccination (i.e. received any dosage of a vaccine)  |
| `Residents.Completed`  | Cumulative number of incarcerated individuals who have fully completed their COVID-19 vaccination schedule                     |
| `Residents.Vadmin`     | Cumulative number of COVID-19 vaccines administered to incarcerated individuals                                                |
| `Staff.Initiated`      | Cumulative number of staff who have initiated COVID-19 vaccination (i.e. received any dosage of a vaccine)                     |
| `Staff.Completed`      | Cumulative number of staff who have fully completed their COVID-19 vaccination schedule                                        |
| `Staff.Vadmin`         | Cumulative number of COVID-19 vaccines administered to staff                                                                   |
| `Address`              | The facility's address                                                                                                         |
| `Zipcode`              | The facility's zipcode                                                                                                         |
| `City`                 | The facility's city                                                                                                            |
| `County`               | The facility's county                                                                                                          |
| `Latitude`             | The facility's latitude                                                                                                        |
| `Longitude`            | The facility's longitude                                                                                                       |
| `County.FIPS`          | The facility's 5-digit county FIPS code                                                                                        |
| `HIFLD.ID`             | The facility's corresponding [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) ID |

## Citations

Citations for academic publications and research reports:

> Hayden Betts. Prison Telecom Data Project: Jail/Prison Telecom Dataset [date you downloaded the data]. UCLA Law, 2020, https://prisontelecomdata.org/.

Citations for media outlets, policy briefs, and online resources:

> Prison Telecom Data Project, https://prisontelecomdata.org/.

## License 
Our data is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). That means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may not use our work for commercial purposes, which means anything primarily intended for or directed toward commercial advantage or monetary compensation. 
