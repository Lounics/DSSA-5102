# DSSA-5102

Accessed 01/25/2024

Summary

This data is on COVID-19 death counts and rates in the United States, categorized by month, year of death, residence jurisdiction (U.S., HHS Region), and demographic characteristics (sex, age, race, Hispanic origin). The counts include deaths confirmed or presumed to be due to COVID-19. The information reflects the total number of deaths as of the date of analysis and may not encompass all deaths during the specified period. Data completeness varies due to reporting delays, ranging from 1 to 8 weeks or more. Regional disparities exist in reporting frequency, with some states reporting daily and others weekly or monthly. This data uses 2021 population estimates and age-adjustment methods. The ten HHS regions are listed, and the rates are age-adjusted to the 2000 standard population using the direct method. 



Data is from the CDC, link(https://data.cdc.gov/NCHS/Provisional-COVID-19-death-counts-and-rates-by-mon/yrur-wghw/about_data)



The data was collected using reports of death confirmed from COVID-19 or presumed to be COVID-19. These death certificates were submitted to NCHS and added to the report.



The data was taken from the CDC data repository and downloaded as a raw CSV file.



A small Python program was used to clean the data and attempt to standardize the reporting of numbers, data types, and missing data.

The data was cleaned and transformed in many ways. Additional columns with contextual notes such as the “data_as_of” and “footnotes” columns were dropped to make the data more legible. A date column was added (date data type) using a combination of the year and month columns present in the original dataset. The year and month columns were then dropped as well. All text columns were converted to “str” type and all numerical were converted to “float” type. Column titles were changed to lowercase for readability. All NaNs in string-type columns were replaced with blanks for easier processing.


The numerical data is in terms of deaths for the covid_deaths column and in terms of deaths/selected(adjusted) population for the rate columns.


The only column I created was the date column by combining the strings of the month and date columns to have a string of the format “01-20” and then used a lambda function to apply the date time.strptime to convert the typing into the standard date datatype. For the COVID death rate columns that were already present in the dataset, they are calculated using standard released processes and are linked in the summary present in the link above.


The data was mapped to have consistent blank types and data typing. In addition, there were some sanity checks performed in the Python script to check that subgroups were properly assigned and that no duplicate rows were present in the set.

The column names are as follow:

- jurisdiction_residence: Location of where the data was sourced from (10 HHS Regions)
- group: Defines the groups present in the following subgroup columns (i.e. Race: only Race in subgroup1 or Race and Age: Race as subgroup1 and Age as subgroup2)
- subgroup1: One of the categorical subgroups (Sex, Race, or Age)
- subgroup2: An additional categorical subgroup (not always applicable.
- covid_deaths: Raw number of reported covid deaths
- crude_covid_rate: Death rate per population (using 2021 population data
- aa_covid_rate: Age-Adjusted covid death rate using 2000 standard population.
- crude_covid_rate_ann: Annual covid death rate
- aa_covid_rate_ann: Age-adjusted annual covid death rate
- date: Date for which data was collected (month and year, always pegged as the first day of that month. I.e. January data Is shown with a date of 1-1-20).


There are no set variables that I used or introduced, the only constants are in the formulas for the already calculated rate columns present in the dataset.


There are no regulations on using the data as it is publicly available information presented by the CDC for use in academic and commercial research.
