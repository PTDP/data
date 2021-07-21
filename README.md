
![logo](logo.png)

# Prison Telecom Data Project

For more background about The Prison Telecom Data Project visit our [website](https://staging.prisontelecom.org).

## Our Data 

You can download a CSV with our latest rate data [here](https://github.com/PTDP/data/blob/main/data/rates.md).

**Note**: Because our data is scraped from private entities, it is updated and ammended on a schedule we do not control. Furthur, our data represents telecom rates as those entities report them publicly, rather than what rates are in practice.


## Data Dictionary 
We maintain one flat data table for public consumption.

The full set of variables that we report includes the following: 

# Rates
| Variable               | Description                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `facilityUID`          | ID that uniquely identifies the facility associated with a rate                                                                |
| `HIFLDID`              | The facility's corresponding [Homeland Infrastructure Foundation-Level Data](https://hifld-geoplatform.opendata.arcgis.com/datasets/prison-boundaries/data) ID |
| `facility`             | The canonical name for a facility (usually the same as the HIFLD name)                                                         |
| `facilityInternal`     | The name a vendor uses for the facility tied to particular rate                                                                |
| `agencyInternal`       | The vendor-reported parent entity for a faciilty. Used by ICS and GTL                                                          |
| `agencyFullNameInternal`| An expanded version of agencyInternal, used by ICS                                                                            |
| `address`              | The canonical facility address (via HIFLD or manual correction)                                                                
| `city`                 | The canonical facility city (via HIFLD or manual correction)                                                                   |
| `state`                | The canonical facility state (via HIFLD or manual correction)                                                                  |
| `zip`                  | The canonical facility zip (via HIFLD or manual correction)                                                                    |
| `countyfips`           | The canonical facility countyfips (via HIFLD or manual correction)                                                             |
| `longitude`            | The canonical facility longitude (via HIFLD or manual correction)                                                              |
| `latitude`             | The canonical facility latitude (via HIFLD or manual correction)                                                               |
| `type`                 | The canonical facility type (via HIFLD or manual correction) `LOCAL`, `COUNTY`, `STATE`, `FEDERAL`, or `MULTI`                 |
| `population`           | The canonical facility population (via HIFLD or manual correction)                                                             |
| `capacity`             | The canonical facility capacity (via HIFLD or manual correction)                                                               |
| `securelvl`            | The canonical facility security level (via HIFLD or manual correction) `CLOSE`, `JUVENILE`, `MINIMUM`, `MEDIUM`, or `MAXIMUM`  |
| `durationInitial`      | The billing period (seconds) at the beginning of a telecom service. For example, the first minute of a call.                   |
| `durationAdditional`   | The billing increment following the `durationInitial`. For example, every minute following the first minute of a call.         |
| `amountInitial`        | The amount (USD, cents) that a telecom service costs during the `durationInitial` period.                                      |
| `amountAdditional`     | The amount (USD, cents) that a telecom service costs during each `durationAdditional` period.     
| `pctTax`               | The percent tax applied to the sum of all billing line-items associated with the call itself. When not provided explicitly by a vendor, the tax percent is calculated from a given-tax line-item, and rounded to 2 significant digits.   
| `phone`                | The phone number provided to the rate calculator.                                                                              |
| `inState`              | Boolean representing whether the origin phone number is located in the same state as the facility called.                      |    
| `service`              | The type of phone service. For example, Securus offers difference billing standards depending on whether an incarcerated person uses direct billing to pay for a call or traditional collect.
| `source`               | The URI of the rate calculator used                                                                                            |
| `company`              | `ICS`, `SECURUS` or `GTL`                                                   |
| `hidden`               | Whether or not PTDP is currently hiding this rate from display on its website due to lack of confidence in the link to a canonical facility                                                    |
| `createdAt`            | The time this record was scraped ISO String (UTC)     

## Our Methodology  
You can read the complete details of our methodogy [here](https://prisontelecom.org/methods).

**Contributors**: You can see our [team page](https://prisontelecom.org/team) for an updated list of contributors. Please reach out at prison.telcom.data.project@gmail.com if you would like to contribute code, data, or time. We always welcome additional contributors!                                                                              |

## Citations

Citations for academic publications and research reports:

> Hayden Betts. Prison Telecom Data Project: Jail/Prison Telecom Dataset [date you downloaded the data]. Prison Telecom Data Project, 2021, https://prisontelecom.org/.

Citations for media outlets, policy briefs, and online resources:

> Prison Telecom Data Project, https://prisontelecom.org/.

## License 
Our data is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). That means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may not use our work for commercial purposes, which means anything primarily intended for or directed toward commercial advantage or monetary compensation. 
