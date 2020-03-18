# CEIDG Datasets

Repository with samples of datasets created from data collected from CEIDG registry. [Centralna Ewidencja Dzialalnosci Gospodarczej](https://prod.ceidg.gov.pl/CEIDG/CEIDG.Public.UI/Search.aspx).

Repository contains two datasets:

* [Continuity of the business in next 12 months](data/100_CEIDG_classification_sample.csv).
* [Survival of businesses registered in 2011](data/100_CEIDG_survival_2011_sample.csv).

Each dataset has been made from raw entry looks like this:

``` 
{
  "_id":"024c41b92bfdc22fa218242b30683c32",
  "DanePodstawowe":{
    "Imie":"Dejta",                               # fake name
    "Nazwisko":"Sajensonowicz",                   # fake surname
    "NIP":"00000000",                             # fake NIP
    "REGON":"00000000",                           # fake REGON
    "Firma":"Jakaś tam firma"                     # fake company name
  },
  "DaneKontaktowe":{
    "AdresPocztyElektronicznej":"some@email.com", #fake email
    "AdresStronyInternetowej":null,
    "Telefon":null,
    "Faks":null
  },
  "DaneAdresowe":{
    "AdresGlownegoMiejscaWykonywaniaDzialalnosci":{
      "TERC":"1465098",
      "SIMC":"0988810",
      "ULIC":"11899",
      "Miejscowosc":"Warszawa",
      "Ulica":"Magenta",
      "Budynek":"155",
      "KodPocztowy":"04-429",
      "Poczta":"Warszawa",
      "Gmina":"Rembertów",
      "Powiat":"Warszawa",
      "Wojewodztwo":"mazowieckie"
    },
    "AdresDoDoreczen":{
      "TERC":"1465098",
      "SIMC":"0988810",
      "ULIC":"11899",
      "Miejscowosc":"Warszawa",
      "Ulica":"Magenta",
      "Budynek":"155",
      "KodPocztowy":"04-429",
      "Poczta":"Warszawa",
      "Gmina":"Rembertów",
      "Powiat":"Warszawa",
      "Wojewodztwo":"mazowieckie"
    },
    "PrzedsiebiorcaPosiadaObywatelstwaPanstw":"Polska"
  },
  "DaneDodatkowe":{
    "DataRozpoczeciaWykonywaniaDzialalnosciGospodarczej":"2012-01-01",
    "DataZawieszeniaWykonywaniaDzialalnosciGospodarczej":"2019-02-28",
    "DataWznowieniaWykonywaniaDzialalnosciGospodarczej":null,
    "DataZaprzestaniaWykonywaniaDzialalnosciGospodarczej":null,
    "DataWykresleniaWpisuZRejestru":null,
    "MalzenskaWspolnoscMajatkowa":"tak",
    "Status":"Zawieszony",
    "KodyPKD":"5320Z,
    4649Z,
    4690Z,
    9529Z"
  },
  "SpolkiCywilneKtorychWspolnikiemJestPrzedsiebiorca":null,
  "Zakazy":null,
  "InformacjeDotyczaceUpadlosciPostepowaniaNaprawczego":null,
  "PelnomocnicyPrzedsiebiorcy":null,
  "Uprawnienia":{
    "Uprawnienie":"od 2012-01-26 do  Rejestr operatorów pocztowych  (wprowadzone przez Urząd Komunikacji Elektronicznej Warszawa)"
  }
}
```
<br>
<br>


## Dataset #1: [Continuity of the business in next 12 months.](data/100_CEIDG_classification_sample.csv)

Short description:

* no of records 100 000 (split into sets: 70% train-valid / 30% test).
* no of features 27.
* binnary classifiaction problem

Record in dataset based on example presented abowe after preprocessing looks like this:

|NIP        |RandomDate |MonthOfStartingOfTheBusiness |QuarterOfStartingOfTheBusiness |MainAddressVoivodeship |MainAddressCounty |CorrespondenceAddressVoivodeship |CorrespondenceAddressCounty |MainAndCorrespondenceAreTheSame | DurationOfExistenceInMonths| NoOfAdditionalPlaceOfTheBusiness|IsPhoneNo |IsEmail |IsWWW |CommunityProperty |HasLicences | NoOfLicences|Sex |HasPolishCitizenship |ShareholderInOtherCompanies |PKDMainSection |PKDMainDivision |PKDMainGroup |PKDMainClass | NoOfUniquePKDSections| NoOfUniquePKDDivsions| NoOfUniquePKDGroups| NoOfUniquePKDClasses| Target|
|:----------|:----------|:----------------------------|:------------------------------|:----------------------|:-----------------|:--------------------------------|:---------------------------|:-------------------------------|---------------------------:|--------------------------------:|:---------|:-------|:-----|:-----------------|:-----------|------------:|:---|:--------------------|:---------------------------|:--------------|:---------------|:------------|:------------|---------------------:|---------------------:|-------------------:|--------------------:|------:|
|00000000 |2018-04-30 |January                      |Q1                             |MAZOWIECKIE            |WARSZAWA          |MAZOWIECKIE                      |WARSZAWA                    |TRUE                            |                          75|                                0|FALSE     |TRUE    |FALSE |tak               |TRUE        |            1|M   |TRUE                 |FALSE                       |H              |53              |532          |5320         |                     3|                     3|                   4|                    4|      1|

<br>

List of features with explanation (if it's necessary):

- **RandomDate**: Randomly chose date beetween 01-11-2017 and 01-11-2018 (or date of termination or suspension if continuity of the Business were stopped earlier in this period).
- **Target**: The binary response variable indicates if continuity of the business was broken in **12 months from random date**. 
- **MonthOfStartingOfTheBusiness**: The month of registering a business in the CEIDG registry.
- **QuarterOfStartingOfTheBusiness**: The quarter of registering a business in the CEIDG registry.
- **MainAddressVoivodeship**.
- **MainAddressCounty**.
- **CorrespondenceAddressVoivodeship**.
- **CorrespondenceAddressCounty**.
- **MainAndCorrespondenceAreTheSame**: Checking if the correspondence address and the main address are the same (with an accuracy to the street).
- **DurationOfExistenceInMonths**: Time in months from registering of the business to **RandomDate** (results has been rounded down to the nearest integer). 
- **NoOfAdditionalPlaceOfTheBusiness**.
- **IsPhoneNo**: Checking if the phone number has been filled in the register (filling in the field is optional).
- **IsEmail**: Checking if the email has been filled in the register (filling in the field is optional).
- **IsWWW**: Checking if the web address has been filled in the register (filling in the field is optional).
- **CommunityProperty**: 
- **HasLicences**: Checking if the business is running with special permissions (eg. sale of alcohol, transportation of people).
- **NoOfLicences**.
- **Sex**: Variable has been created by checking the last letter of a name. If the last letter is 'a' then sex is defined as female, otherwise as male. The disadvantage of this approach is the possibility of not classifying foreigners correctly.
- **HasPolishCitizenship**.
- **ShareholderInOtherCompanies**.

Features listed below based on [Polska Klasyfikacja Działalności](https://www.biznes.gov.pl/en/classification-pkd-code)

- **PKDMainSection**.
- **PKDMainDivision**.
- **PKDMainGroup**.
- **PKDMainClass**.
- **NoOfUniquePKDSections**.
- **NoOfUniquePKDDivsions**.
- **NoOfUniquePKDGroups**.
- **NoOfUniquePKDClasses**.

<br>
<br>

## Dataset #2: [Survival of the businesses registred in 2011.](data/100_CEIDG_survival_2011_sample.csv)

Short description:

* no of records 287 019 (all businesses registered in 2011).
* no of features 26.
* survival analysis problem.

List of features with explanation (if it's neccessary):

- **Status**.
- **StartingDateOfTheBusiness**.
- **DateOfTermination**.
- **Terminated**: Binary variable indicates if company surived.
- **DurationOfExistenceInMonths**: Time in months from registering of the business to 2020-03-01.
- **MainAddressVoivodeship**.
- **MainAddressCounty**.
- **CorrespondenceAddressVoivodeship**.
- **CorrespondenceAddressCounty**.
- **MainAndCorrespondenceAreTheSame**: Checking if the correspondence address and the main address are the same (with an accuracy to the street). 
- **NoOfAdditionalPlaceOfTheBusiness**.
- **IsPhoneNo**: Checking if the phone number has been filled in the register (filling in the field is optional).
- **IsEmail**: Checking if the email has been filled in the register (filling in the field is optional).
- **IsWWW**: Checking if the web address has been filled in the register (filling in the field is optional).
- **CommunityProperty**: 
- **HasLicences**: Checking if the business is running with special permissions (eg. sale of alcohol, transportation of people).
- **NoOfLicences**.
- **Sex**: Variable has been created by checking the last letter of a name. If the last letter is 'a' then sex is defined as female, otherwise as male. The disadvantage of this approach is the possibility of not classifying foreigners correctly.
- **HasPolishCitizenship**.
- **ShareholderInOtherCompanies**.

Features listed below based on [Polska Klasyfikacja Działalności](https://www.biznes.gov.pl/en/classification-pkd-code)

- **PKDMainSection**.
- **PKDMainDivision**.
- **PKDMainGroup**.
- **PKDMainClass**.
- **NoOfUniquePKDSections**.
- **NoOfUniquePKDDivsions**.
- **NoOfUniquePKDGroups**.
- **NoOfUniquePKDClasses**.

Example record:

|NIP        |Status     | YearOfStartingOfTheBusiness|StartingDateOfTheBusiness |DateOfTermination | Terminated| DurationOfExistenceInMonths|MainAddressVoivodeship |MainAddressCounty |CorrespondenceAddressVoivodeship |CorrespondenceAddressCounty |MainAndCorrespondenceAreTheSame | NoOfAdditionalPlaceOfTheBusiness|IsPhoneNo |IsEmail |IsWWW |CommunityProperty |HasLicences | NoOfLicences|Sex |HasPolishCitizenship |ShareholderInOtherCompanies |PKDMainSection |PKDMainDivision |PKDMainGroup |PKDMainClass | NoOfUniquePKDSections| NoOfUniquePKDDivsions| NoOfUniquePKDGroups| NoOfUniquePKDClasses|
|:----------|:----------|---------------------------:|:-------------------------|:-----------------|----------:|---------------------------:|:----------------------|:-----------------|:--------------------------------|:---------------------------|:-------------------------------|--------------------------------:|:---------|:-------|:-----|:-----------------|:-----------|------------:|:---|:--------------------|:---------------------------|:--------------|:---------------|:------------|:------------|---------------------:|---------------------:|-------------------:|--------------------:|
|00000000 |Wykreślony |                        2011|2011-01-01                |2015-08-06        |          1|                          55|MAZOWIECKIE            |WARSZAWA          |MAZOWIECKIE                      |WARSZAWA                    |TRUE                            |                                0|FALSE     |FALSE   |FALSE |-                 |FALSE       |            0|M   |TRUE                 |FALSE                       |F              |43              |432          |4322         |                     1|                     1|                   1|                    1|





