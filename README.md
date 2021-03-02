
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
**Note**: Because our data is scraped from private entities, it is updated and ammended on a schedule we do not control. Furthur, our data represents telecom rates as those entities report them publicly, rather than what rates are in practice.

## Data Dictionary 
We maintain three data tables. One represents `Rates`, one is a join table representing that data that each company stores about facilities `CompanyFacilities`, and one represents normalized, canonical data that links a company's representation of a facility to that facility as it exists in the real world `CanonicalFacilities`.

The full set of variables that we report includes the following: 

# Rates
| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `id`                   | Integer ID that uniquely identifies every rate                                                                                 |
| `durationInitial`      | The billing period (seconds) at the beginning of a telecom service. For example, the first minute of a call.                   |
| `durationAdditional`   | The billing increment following the `durationInitial`. For example, every minute following the first minute of a call.         |
| `amountInitial`        | The amount (USD, cents) that a telecom service costs during the `durationInitial` period.                                      |
| `amountAdditional`     | The amount (USD, cents) that a telecom service costs during each `durationAdditional` period.     
| `pctTax`               | The percent tax applied to the sum of all billing line-items associated with the call itself. When not provided explicitly by a vendor, the tax percent is calculated from a given-tax line-item, and rounded to 2 significant digits.   
| `phone`                | The phone number provided to the rate calculator.                                                                              |
| `inState`              | Boolean representing whether the origin phone number is located in the same state as the facility called.                      |    
| `service`              | The type of phone service. For example, Securus offers difference billing standards depending on whether an incarcerated person uses direct billing to pay for a call or traditional collect.
| `company`              | `ICS` or `SECURUS`                                                                                                             |
| `source`               | The URI of the rate calculator used                                                                                            |
| `companyFacility`      | A reference to the `CompanyFacilities` entry that indicates a company's internal representation of the facility that this rate belongs to                                                    |
| `updatedAt`            | An array of ISO Strings (UTC) representing each time a scraper encountered this unique rate. We consider a unique rate to be the combination of all of the following normalized variables. If any of these changes, we create a new unique rate: `durationInitial`, `durationAdditional`, `amountInitial`, `amountAdditional`, `pctTax`, `phone`, `inState`, `service`, `companyFacility`.                                                                                                                                |                                               |

# CompanyFacilities
| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `id`                   | Integer ID that uniquely identifies every facility                                                                             |
| `facilityInternal`     | The facility name that the company uses internally                                                                             |
| `agencyInternal`       | The agency name that the company uses internally                                                                               |
| `stateInternal`        | The facility state that the company users internal (STUSAB)                                                                    |  
| `company`              | The name of the company: `ICS` or `SECURUS`                                                                                    |
| `canonicalFacility`    | A reference to the `CanonicalFacilities` entry that links a company facility to a normalized facility that can be joined with other data sets  
| `updatedAt`            | Last update to this record ISO String (UTC)                                                                                    |

# CanonicalFacilities
| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `id`                   | Integer ID that uniquely identifies every facility                                                                             |
| `name`                 | Normalized facility name, pulled, in order of preference, from HIFLD, UCLACovid19, Google Maps API, or Company Internal Representation                                                                      |
| `jurisdiction`         | Whether the facility falls under `state`, `county`, `federal`, or `immigration` jurisdiction, from HIFLD, UCLACovid19, or manual aggregation, or order of preference.                                                                                                                                               |
| `address`              | From Google Maps API                                                                                                           |
| `googlePlaceName`      | From Google Maps API                                                                                                           |
| `longitude`            | From Google Maps API                                                                                                           |
| `latitude`             | From Google Maps API                                                                                                           |
| `state`                | From Company Internal representation (STUSAB)                                                                                  |
| `HIFLDID`              | The facility's corresponding [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) ID |
| `HIFLD_POPULATION`     | Population reported by HIFLD, duplicated here for convenience |
| `HIFLD_CAPACITY`       | Capacity reported by HIFLD, duplicated here for convenience |
| `HIFLD_SOURCE`         | Source of `HIFLD_POPULATION` and `HIFLD_CAPACITY`, duplicated here for convenience |
| `HIFLD_SOURCEDATE`     | Date `HIFLD_POPULATION` and `HIFLD_CAPACITY` data were scraped, duplicated here for convenience |
| `UCLACovid19ID`        | The facility's corresponding [UCLA Covid-19 Behind Bars Data Project](https://github.com/uclalawcovid19behindbars/data/blob/master/latest-data/adult_facility_covid_counts.csv) ID |
| `UCLACovid19_POPULATION` | Facility population reported by UCLACovid19, duplicated here for convenience |
| `UCLACovid19_SOURCE`     | Source of `UCLACovid19_POPULATION`, duplicated here for convenience |
| `UCLACovid19_SOURCEDATE` | Date `UCLACovid19_POPULATION` data was scraped, duplicated here for convenience  |

# Joined Rates
A convenience CSV, which expands foreign key references in rates (`companyFacility` and `canonicalFacility`), for data analysis.

## Citations

Citations for academic publications and research reports:

> Hayden Betts. Prison Telecom Data Project: Jail/Prison Telecom Dataset [date you downloaded the data]. UCLA Law, 2020, https://prisontelecomdata.org/.

Citations for media outlets, policy briefs, and online resources:

> Prison Telecom Data Project, https://prisontelecomdata.org/.

## License 
Our data is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). That means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may not use our work for commercial purposes, which means anything primarily intended for or directed toward commercial advantage or monetary compensation. 
