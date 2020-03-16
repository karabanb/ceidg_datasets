# CEIDG Datasets

This repository contains samples of data gathered from [Centralna Ewidencja Dzialalnosci Gospodarczej](https://prod.ceidg.gov.pl/CEIDG/CEIDG.Public.UI/Search.aspx).

Raw entry in json format looks like this:

``` json
{
  "_id":"024c41b92bfdc22fa218242b30683c32",
  "DanePodstawowe":{
    "Imie":"Janusz",
    "Nazwisko":"Szklarczyk",
    "NIP":"1130106921",
    "REGON":"011138543",
    "Firma":"WAWA OPERATOR JANUSZ SZKLARCZYK"
  },
  "DaneKontaktowe":{
    "AdresPocztyElektronicznej":"j23gpw@onet.eu",
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

Record in dataset based on example presented abowe after preprocessing looks like this:



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



