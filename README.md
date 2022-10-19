# Analysis of COVID-19 and its impacts in USA

View a slideshow presentation of this readme at 

[Presentation Deck](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/presentation/Covid-19%20-%20USA%20Analysis.pdf)


Some of the technologies used in this project:
* Python
* Pandas
* Numpy
* Matplotlib
* Seaborn

## Table of Contents

 1. Introduction - COVID-19
 2. Databases​
 3. Questions & Analysis
 4. ​Impacts  of COVID-19 in USA​
 5. Vaccination  Impacts​
 6. Government Responses​


## Introduction - COVID-19

COVID-19 is vastly documented in several Universities and Research Groups, and the consolidated information of the latest confirmed cases and deaths, as well as the guidance for the different regions globally are published by the World Health Organization (**WHO** - https://www.who.int/).

The picture below shows the status of the figures worldwide as of 18th October 2022.

![Covid-19 - Worldwide figures as of 18/10/2022](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/Covid-19%20World%20Map.jpg)

## Databases

### Oxford Database

The University of Oxford and Research Groups have orgasised several initiatives to tackle with the research of COVID-19. One of these Research Groups is the Oxford COVID-19 Government Response Tracker (OxCGRT), which collects systematic information on policy measures that governments have taken to tackle COVID-19 ([https://www.bsg.ox.ac.uk/research/covid-19-government-response-tracker](https://www.bsg.ox.ac.uk/research/covid-19-government-response-tracker)).

They manage a database that is maintained daily, since 1st January 2020, covering several indicators such as school closures, workplace closures, travel restrictions, vaccination policy, rescaled to a value from 0 to 100 (100 = strictest).

These policies are recorded on a scale to reflect the extent of government action, and scores are aggregated into a suite of policy indices.

The main indicators (or indices) considered for this proposed analysis are:
* ConfirmedCases
* ConfirmedDeaths
* PopulationVaccinated
* GovernmentResponseIndex_SimpleAverage

#### Data Cleaning and Preparation
As part of the scope of this project, we have used two databases available, which covers USA States in 2020 and 2021:
* [OxCGRT_USA_differentiated_withnotes_2020.csv](https://github.com/OxCGRT/covid-policy-tracker/blob/master/data/United%20States/OxCGRT_USA_differentiated_withnotes_2020.csv "OxCGRT_USA_differentiated_withnotes_2020.csv")
* [OxCGRT_USA_differentiated_withnotes_2021.csv](https://github.com/OxCGRT/covid-policy-tracker/blob/master/data/United%20States/OxCGRT_USA_differentiated_withnotes_2021.csv "OxCGRT_USA_differentiated_withnotes_2021.csv")

Some steps were required to clean up the data and calculate some important fields for the analysis.

*Required Fields from the database:*
* Date
* RegionName
* ConfirmedCases
* ConfirmedDeaths
* PopulationVaccinated (%)
* GovernmentResponseIndex_SimpleAverage

*Calculated Fields:*
* Cases Per Capita (%)
* Deaths Per Capita (%)
* Deaths per Confirmed Cases (%)
* PopulationVaccinated (\*)
(\*) Need to calculate using Census API (described in the next session), based on the % of Population Vaccinated that is available from the Oxford Database.

Finally, and very important, the National data was extracted on the fields where "RegionName" is empty. Also, "Washington DC" was removed from the analysis when comparing the different States.

### USA Census Bureau

The Census Bureau's mission is to serve USA as the nation's leading provider of quality data about its people and economy.

U.S. Census Bureau provide access to demographic, economic and population data (database and API).

For this project, we have used Census API to fetch for the information required to calculate some of the fields mentioned in the previous session:
* Region Name
* State
* Population per State

The data frame created from this API call is merged with the Oxford database, so the merged one could be used in the analysis phase of this project.

The sum of the population of all States brings the National population.

Finally, no cleanup was required for this data frame.

## Questions & Analysis

The following questions were enumerated in order to proceed with the Data Analysis proposed by this Project:

 1. What state was most impacted by COVID-19 (by population)
	* Deaths per capita?
	* Cases per capita?
2. Did vaccination rate impact the spread of COVID-19?
	* Spread (Confirmed Cases) vs. Vaccination Rate
	* Deaths vs. Vaccination Rate
3. Did Government Response change COVID-19 impact?
	* Government vs. Deaths
	* Government vs. Confirmed Cases

These questions are going to be answered / explained in the next sessions, considering the information extracted from the database, analysis and conclusions.

## USA States and the impacts of COVID-19

This analysis was mainly done considering the latest information from 2021 database, more exactly on the last date (31/12/2022).

### Deaths per Capita (%) / State

"*Deaths per Capita (%)*" is calculated based on the number of "*Confirmed Deaths*" divided by the "*Population*" of each State. Finally, this rate is multiplied by 100 to get the percentage rate.

![Deaths per Capita (%) / State](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2021%20-%20Deaths%20Per%20Capita.png)

The following can be analysed from this graph and data extracted:
* 31 States above the **National Average** (**0.24%**) for Deaths per Capita.
* 3 States presenting Deaths per capita above 0.33%: Alabama, Arizona, Mississipi.
* **Mississipi** presented the highest rate of Deaths Per Capita (0.35045%).
* **Vermont** presented the lowest rate of Deaths Per Capita (0.07544%).

### Confirmed Cases per Capita (%) / State

"*Confirmed Cases per Capita (%)*" is calculated based on the number of "*Confirmed Cases*" divided by the "*Population*" of each State. Finally, this rate is multiplied by 100 to get the percentage rate.

![Confirmed Cases per Capita (%) / State](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2021%20-%20Confirmed%20Cases%20Per%20Capita.png)

The following can be analysed from this graph and data extracted:

* 31 States above the **National Average** (**17.09%**) for Confirmed Cases per Capita.
* 4 States presenting Confirmed Cases per capita above 21%: North Dakota, Rhode Island, Alaska, Tennessee.
* **North Dakota** presented the highest rate of Confirmed Cases Per Capita (22.92%).
* Hawaii presented the lowest rate of Confirmed Cases Per Capita (7.95%).

### Confirmed Cases and Deaths / State

The following graph brings the absolute data as of 31/12/2022:

![Confirmed Cases and Deaths / State](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2021%20-%20Confirmed%20Cases%20and%20Deaths%20per%20State.png)

* National average:
	* Confirmed Cases: 54,512,513
	* Confirmed Deaths: 820,719
	* Deaths per Confirmed Case Ratio: 1.50 %.

* States with higher population present higher absolute figures for Confirmed Cases and Deaths.
	* California
		* Confirmed Cases: 5,517,870
		* Deaths: 76,478
	* Texas
		* Confirmed Cases: 4,630,880
		* Deaths: 75,744
	* Florida
		* Confirmed Cases: 4,209,927
		* Deaths: 62,504

### Deaths per Confirmed Cases (%) / State

"*Deaths per Confirmed Cases (%)*" is calculated based on the number of "*Confirmed Deaths*" divided by the "*Confirmed Cases*" of each State. Finally, this rate is multiplied by 100 to get the percentage rate.

![Deaths per Confirmed Cases (%) / State](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2021%20-%20Deaths%20Per%20Confirmed%20Cases.png)

* **National average** for Deaths per Confirmed Cases Rate as of 31-Dec-2021: **1.50%**
* 5 States presenting Deaths per Confirmed Cases Rate above 1.80%: Pennsylvania, Louisiana, Alabama, New Jersey, Mississippi.
* **Mississipi** presented the highest Deaths per Confirmed Cases Rate (1.92%).
* **Utah** presented the lowest Deaths per Confirmed Cases Rate (0.59%).

![Deaths per Confirmed Cases Ratio (%)](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2021%20-%20Deaths%20per%20Confirmed%20Cases%20Ratio.png)

* Over 365 days in 2021, the **National average** for Deaths per Confirmed Cases Ratio fluctuated from **1,64%** on 01-01-2021 to **1,50%** on 31-12-2021.
* The **highest** Deaths per Confirmed Cases Rate identified in **18-03-2021**: 1.80 %.
* The **lowest** Deaths per Confirmed Cases Rate identified in **31-12-2021**: 1.50 %.
* Significant **decrease** of Deaths per Confirmed Cases Rate in **July-2021**.
* In further analysis, this difference can be considered with **Vaccination index** and **Government responses**.

## Did vaccination rate impact the spread of COVID-19?

This analysis was mainly done considering the latest information from the a concatenated database containing both 2020 and 2021 databases.

### Confirmed Cases (%) and Population Vaccinated (%)

![2020 & 2021 :: Confirmed Cases (%) and Population Vaccinated (%)](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2020-2021%20-%20Deaths%20per%20Confirmed%20Cases%20Ratio%20and%20Population%20Vaccinated%20%28Percentage%29.png)

* Vaccination started only in **2021**.
* More than **63%** of the population vaccinated by the end of 2021.
* **16.65%** of the population already confirmed to have had COVID-19 by the end of 2021.
* We can see a **lower increase** of the confirmed cases after the **first month of the vaccination**, and the curve becomes flatter.
	* Without the Vaccination, the confirmed deaths would be much higher at the end of the year, and
	* Number of deaths would be higher, following the deaths per confirmed cases rate.

### Deaths per Confirmed Cases Ratio (%) and Population Vaccinated (%)

![2020 & 2021 :: Deaths per Confirmed Cases Ratio and Population Vaccinated (Percentage)](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2020-2021%20-%20Deaths%20per%20Confirmed%20Cases%20Ratio%20and%20Population%20Vaccinated%20%28Percentage%29.png)

* Vaccination started only in **2021**.
* After the start of the Vaccination program, the rate of deaths per confirmed case became stable (**fluctuation up to 0.3%**) and flat.
* The Vaccination impacted positively in the decrease of the rate of deaths per confirmed cases. In 2021:
	* The **highest** Deaths per Confirmed Cases Rate: **1.80 %**.
	* The **lowest** Deaths per Confirmed Cases Rate: **1.50 %**.


## Did Government Response change COVID impact?

The Oxford COVID-19 Government Response Tracker (OxCGRT) maintain several indicators such as school closures, workplace closures, travel restrictions, vaccination policy, rescaled to a value from 0 to 100 (100 = strictest) since 01/01/2020.

These indicators are quite complex, and a Government Response Index is calculated by this research group under "GovernmentResponseIndex_SimpleAverage" field.

The next graphs will bring the visualisation of the impact of the higher Government Response Index to drive to a lower rate of Deaths per Confirmed Cases.

![2020 & 2021 :: Deaths per Cases Ratio (%) and Government Response Index (%)](https://github.com/MechaBirdzilla/Project-1/blob/cheila-test-branch/images/2020-2021%20-%20Deaths%20per%20Cases%20Ratio%20and%20Government%20Response%20Index%20%28Percentage%29.png)


## Conclusion

* States with higher population present higher absolute figures for Confirmed Cases and Deaths.​
* As of 31/12/2021:​
	* Mississipi presented the highest rate of​ Deaths Per Capita (0.35045%).​
	* North Dakota presented the highest rate of​ Confirmed Cases Per Capita (22.92%).​
* The Vaccination impacted positively in the decrease of the rate of deaths per confirmed cases. In 2021:​
	* The highest Deaths per Confirmed Cases​ Rate: 1.80 %.​
	* The lowest Deaths per Confirmed Cases​ Rate: 1.50 %.​
* Maximum government response index is from April 2020 to July 2020 which is the period of the first lockdown. significant decrease in death rate.