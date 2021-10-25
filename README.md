# Alaska Airlines Data Science Interview
## Practical Assessment
Emily Yamauchi
[![LinkedIn][linkedin-shield]][linkedin-url]

[LINK to Google Slide Deck](https://docs.google.com/presentation/d/18pG2f4qhC4xT-a2VQVc7HP_wRRp_9W1waalIwlBTHxY/edit?pli=1#slide=id.p)

## Introduction

### Objective

The purpose of this exercise was to find a way to predict whether a flight would be delayed or not- a potential delay can be mitigated by asking the crew to fly faster, but doing so increases fuel costs, so correctly classifying the outcomes is important.  
On the flip side, missing the incorrectly labeled non-delay flights would decrease Alaska Airlines' on-time performance.   

### Data Source

The original flights dataset was given as a part of this assessment. 
It contained nearly 300,000 rows of data, with each row representing a flight from Mar 2020 to Feb 2021.  
The schema of the flights dataset is as follows:  

| Column Name             | Description                                     |
|-------------------------|-------------------------------------------------|
| `OPER_CARR_CD`          | Operating airline – AS = Alaska Airlines, QX = Horizon Airlines, OO = Skywest Airlines |
| `ACT_ORIG`              | Origin airport code  |
| `ACT_DEST`		  | Destination airport code |
| `FLT_NBR`		  | Flight number |
| `ACT_FULL_TAIL_NBR`	  | Unique identifier for each individual aircraft |
| `ACT_AC_TYPE`		  | Aircraft types with different performance and seat configuration –Boeing 737, Airbus A320/321, De Havilland DH8-400, Embraer E175 |
| `SKD_MILES`		  | Number of flight miles between origin and destination |
| `ACT_TAXI_OUT_MIN`	  | Minutes between gate departure and take off from runway at the origin |
| `ACT_TAXI_IN_MIN`	  | Minutes between touch down onto runway and gate arrival at the destination |
| `SKD_ZULU_DPTR_DDTM`	  | Scheduled departure datetime in UTC time |
| `ACT_ZULU_DPTR_DTTM`	  | Actual departure datetime in UTC time |
| `SKD_ZULU_ARRV_DTTM`	  | Scheduled arrival datetime in UTC time |
| `ACT_ZULU_ARRV_DTTM`	  | Actual arrival datetime in UTC time |
| `ACT_ORIG_GMT_OFFSET`	  | Time offset to convert from UTC time to the origin airport’s local time |
| `ACT_DEST_GMT_OFFSET`	  | Time offset to convert from UTC time to the destination airport’s local time | 


Additionally, aircraft data is taken from [FAA](https://www.faa.gov/licenses_certificates/aircraft_certification/aircraft_registry/releasable_aircraft_download/) archives, specifically from the `2020 Aircraft Registration Database`.

A flight is classified as being delayed if it arrives 14 minutes or more past its scheduled arrival time.  

### Data Processing and Assumptions Made

- If the actual arrival time is missing, then there is no way to determine whether the flight was delayed or not, so these flights were excluded from the dataset.  
- One key assumption made was that scheduled flight times are consistent for all given origin, destination, and flight number combination. This way, if a flight was missing its scheduled arrival time, it can be calculated using the mean of all other existing flight schedules with the same origin, destination, and flight number.
- Some of the aircrafts in the FAA aircraft data archive was missing the manufacture year, in which case the date of certification was used as a proxy

### Known Issues

The airport codes for the origin and destination airports are included in the model, but the codes themselves do not provide much information and have high cardinality. 
What would be potentially more useful would be to find the coordinates for these airports and together with the departure/arrival datetime, find the weather for that given location to use as a variable in the model. 
While there are weather data APIs, I was not able to locate one which gave granular hourly historical data without a paid subscription.

### Folder Structure

```
 AL-Technical
    ├── LICENSE
    ├── README.md
    ├── data_clean
    │   ├── flights_cleaned.csv
    │   └── flights_clean_new.csv
    ├── data_raw
    │   ├── ReleasableAircraft.2020.zip
    │   ├── airport_codes_csv.csv
    │   └── Predict Delays Mar 2020 to Feb 2021.csv
    └── Alaska-Airlines-Assessment.ipynb
```
<p align="right">(<a href="#top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->

[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/eyamauchi/