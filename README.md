# CEIDG Datasets

This repository contains samples of data gathered from [Centralna Ewidencja Dzialalnosci Gospodarczej](https://prod.ceidg.gov.pl/CEIDG/CEIDG.Public.UI/Search.aspx).


## Dataset #1. Continuity of the Business in next 12 months.

Based on the raw data, the following features were created:
- **RandomDate**: Randomly chose date beetween 01-11-2017 and 01-11-2018 (or date of termination or suspension if continuity of the Business were stopped earlier in this period).
- **Target**: The binary variable indicates if continuity of the business was broken in **12 months from random date**. 
- **MonthOfStartingOfTheBusiness**: The month of registering a business in the CEIDG registry.
- **QuarterOfStartingOfTheBusiness**: The quarter of registering a business in the CEIDG registry.
- **MainAddressVoivodeship**.
- **MainAddressCounty**.
- **CorrespondenceAddressVoivodeship**.
- **CorrespondenceAddressCounty**.
- **MainAndCorrespondenceAreTheSame**: Checking if the correspondence address and the main address are the same (with an accuracy to the street).
- **DurationOfExistenceInMonths**: Time in months from registering of the business to **RandomDate** (months was 
- **NoOfAdditionalPlaceOfTheBusiness**.
- **IsPhoneNo**.
- **IsEmail**.
- **IsWWW**.
- **CommunityProperty**.
- **HasLicences**.
- **NoOfLicences**.
- **Sex**.
- **HasPolishCitizenship**.
- **ShareholderInOtherCompanies**.
- **PKDMainSection**.
- **PKDMainDivision**.
- **PKDMainGroup**.
- **PKDMainClass**.
- **NoOfUniquePKDSections**.
- **NoOfUniquePKDDivsions**.
- **NoOfUniquePKDGroups**.
- **NoOfUniquePKDClasses**.

## Dataset #2. Time of Survival of the Businesses from Day of Registration.


