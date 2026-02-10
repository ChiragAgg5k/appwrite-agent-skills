# Locale

The Locale service allows you to customize your app based on your users&#039; location.

## Get user locale

`get`
Get the current user location based on IP. Returns an object with user country code, country name, continent name, continent code, ip address and suggested currency. You can use the locale header to get the data in a supported language.

([IP Geolocation by DB-IP](https://db-ip.com))


**Response:** `locale`

## List locale codes

`listCodes`
List of all locale codes in [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).


**Response:** `localeCodeList`

## List continents

`listContinents`
List of all continents. You can use the locale header to get the data in a supported language.


**Response:** `continentList`

## List countries

`listCountries`
List of all countries. You can use the locale header to get the data in a supported language.


**Response:** `countryList`

## List EU countries

`listCountriesEU`
List of all countries that are currently members of the EU. You can use the locale header to get the data in a supported language.


**Response:** `countryList`

## List countries phone codes

`listCountriesPhones`
List of all countries phone codes. You can use the locale header to get the data in a supported language.


**Response:** `phoneList`

## List currencies

`listCurrencies`
List of all currencies, including currency symbol, name, plural, and decimal digits for all major and minor currencies. You can use the locale header to get the data in a supported language.


**Response:** `currencyList`

## List languages

`listLanguages`
List of all languages classified by ISO 639-1 including 2-letter code, name in English, and name in the respective language.


**Response:** `languageList`

