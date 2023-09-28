# WEBSERVICE SPECIFICATIONS FOR EXPORT METADATA

This API allows mEDRA users who deposits content metadata in mEDRA systems to retrieve and then export it in different formats (Crossref, DOAJ, DOI schema, etc.) than the original one (ONIX). Each user with the need to use the present service must operated only in their(s) prefix(es).

## Endpoint

The API endpoint to access the service is \
Testing environement: `https://www-medra-dev.medra.org/servlet/ws/export-metadata` (UNDER CONSTRUCTION)\
Production environement: `https://www.medra.org/servlet/ws/export-metadata` (UNDER CONSTRUCTION)

## Autentication

The API service is accessible upon basic authentication. The credentials are the same used for the deposit in mEDRA systems.

## Authorization

> #### User

The authorization rules on user is the same already present in mEDRA systems, and each user is authorized to export metadata content of their(s) prefix(es).

> #### Prefix

Any user must operated only on their(s) prefix(es). Any request to the API service with prefix of others is forbidden.

## Http method

The Http method allowed is **GET**, and the api accepts the following [Parameters](#Parameters)

## Parameters

The table below lists all the parameters (mandatory or optional) expected by the export metadata API service. There is no priority, order, etc., in parameters, the user could provide it (or them) to the API as prefered. The metadata export result is obtained considering all the parameters provided to the API in AND conditions.

| **Parameter** | **Type** | **Case sensitive** | **Description** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- | --- |
| `doi` | DOIList | No | DOI List desired to obtain metadata | `doi=10.5236/SAW` <br/> `doi=10.5236/SAW,10.5236/SAV,10.5236/MONP`| For more than one DOI, the token separator is comma (,). Non more than 30 DOIs must be requested for metadata export |
| `prefix` | String | No | The prefix desired to obtain in export metadata | `prefix=10.5236`| Only for one prefix the metadata export must be requested. The searched metadata must exactly match the prefix |
| `issn` | String | No | The issn desired to obtain in export metadata result | `issn=1946-2166` <br/> `issn=19462166` | Only for one issn the metadata export must be requested. issn with hyphen is also allowed as issn without hyphen. The searched metadata must exactly match the issn <br/> Please pay attention to special characters dash and en-dash|
| `isbn` | String | No | The isbn desired to obtain in export metadata return | `isbn=978-88-89637-15-9` <br/> `issn=9788889637159` | Only for one isbn the metadata export must be requested. isbn with hyphen is also allowed as issn without hyphen. The searched metadata must exactly match the isbn <br/> Please pay attention to special characters dash and en-dash|
| `jounalIssueNumber` | String | No | The DOI Journal Issue Number desired in export metadata result | `journalIssueNumber=9` | Only for one DOI Journal Issue Number the metadata export must be requested. The searched metadata must exactly match the journalIssueNumber |
| `jounalIssueDate` | Date | No | The DOI Journal Issue Date desired in export metadata result | `journalIssueDate=2023` <br/> `journalIssueDate=2023-07` <br> `journalIssueDate=2023-07-25` | The DOI Journal Issue Date apply the `right LIKE` search retrieve. A record with `202305` present in the database will not be return if the DOI Journal Issue Date searched for is `20230513`. Instead, a record with `20230513` present in the database will be return if the DOI Journal Issue Date searched for is `20230513` |
| `format` | Format | Yes | The format desired for export metadata result | `format=DOAJ` | Only for one format the metadata export must be requested |
| `publicationDate` | Date | No | The DOI publication Date desired in export metadata result | `publicationDate=2023` <br/> `publicationDate=2023-07` <br> `publicationDate=2023-07-25` | The DOI publication Date apply the `right LIKE` search retrieve. A record with `202305` present in the database will not be return if the DOI publication Date searched for is `20230513`. Instead, a record with `20230513` present in the database will be return if the DOI Journal Issue Date searched for is `20230513` |
| `creationDate` | DateRange | Yes | The export of all metadata content with first DOI creation Date for | `creationDate=[2022-10-10,2022-11-12]` <br/> `creationDate=[2022-10-10,]` <br> `creationDate=[,2022-11-12]` | The first DOI creation of the metadata content |
| `updateDate` | DateRange | Yes | The export of all metadata content with last DOI update Date for | `creationDate=[2022-10-10,2022-11-12]` <br/> `creationDate=[2022-10-10,]` <br> `creationDate=[,2022-11-12]` | The last DOI UPDATE of the metadata content |

> #### Parameters type
> | **Type** | **Description** | **Sample** |
> | --- | --- | --- |
> | DOIList | DOI string with comma token separator. If the DOI contains a comma, the DOI must be encoded | `doi=10.5236/SAW` <br/> `doi=10.5236/SAW,10.5236/SAV,10.5236/MONP` |
> | Date | Date in one of the following format <br/> YYYY <br/> YYYY-MM <br/> YYYY-MM-DD | `2003` <br/> `2003-11` <br/> `2003-11-29` |
> | Format | Enumeration, allowed values are: <br/> DOAJ <br/> CROSS44 <br/> CROSS48 <br/> ONIX <br/> PUBMED | `DOAJ` <br/> `ONIX` |
> | DateRange | A range of date with the following meaning: <br/> a. From a date to now <br/> [{Date},] <br/> b. Until a date <br/> [,{Date}] <br> c. Between two dates <br/> [{Date},{Date}] | a. From 01/02/2022 to now <br/> `[2022-02-01,]` <br/> b. Until 01/02/2022 <br/> `[,2022-02-01]` <br> c. From 01/02/2022 to 03/04/2023 <br/> `[2022-02-01,2023-04-03]`|

> #### Format description
> | **ENUM** | **Format Description** | **Note** |
> | --- | --- | --- |
> | ONIX | ONIX for DOI 2.0 (last release of the schema) | The old format (1.0/1.1) are tranformed in the last format 2.0 |
> | CROSS44 | Crossref Schema 4.4.2 | |
> | CROSS48 | Crossref Schema 4.8.1 | |
> | DOAJ | DOAJ (no version) | |
> | PUBMED | PUBMED JATS | |
>
> In the future, evaluation is planned to export DOI metadata content in other format such as:
> >- DOI Schema
> >- Format of our DOI Content Negotiation

## Some instances of HTTP requests
> - Export in DOAJ format of DOIs metadata with prefix `10.5236` and ISSN `1234-3456` <br/>
Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?issn=1234-456&format=DOAJ&prefix=10.5236` <br/>
Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?issn=1234-456&format=DOAJ&prefix=10.5236` <br/>
> - Export in ONIX format of DOIs metadata with prefix `10.5236` and received the last update of metadata `2023-03-31` <br/>
Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&updateDate=[2023-03-31,2023-03-31]` <br/>
Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&updateDate=[2023-03-31,2023-03-31]` <br/>
> - Export in CROSS44 format of DOIs metadata with prefix `10.5236` and ISBN `978-88-00-00091-1`, published in `2023` and the metadata was created between `2023-01-12` and `2023-03-31` <br/>
Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=CROSS44&prefix=10.5236&isbn=978-88-00-00091-1&publicationDate=2023&creationDate=[2023-01-12,2023-03-31]` <br/>
Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=CROSS44&prefix=10.5236&isbn=978-88-00-00091-1&publicationDate=2023&creationDate=[2023-01-12,2023-03-31]` <br/>

## Validation of  HTTP requests input parameters
The API implementation validates the input parameters in the following order:
1. If the mandatory parameter `format` is not present in the request, a 400 Bad Request is returned with error message `The format is required`
2. In the request, if both parameters `doi` and `prefix` are present or neither the `doi` parameter nor the `prefix` parameter are present, a 400 Bad Request is returned with such error `Either doi or prefix is required`
3. if the `doi` parameter is present in the request and there are other parameters besides `format`, a 400 Bad Request is returned with the following error `The syntax for DOI request is /ws/export-metadata?format=&doi=`

## Some instances of expected HTTP requests output
> | **URL** | **HTTP Code** | **HTTP Status Message** |
> | --- | --- | --- |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata` | `400` | `format is required` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX` | `400` | `either doi or prefix is required` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&doi=10.100` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&doi=10.100` | `400` | `either doi or prefix is required` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&doi=10.100` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&doi=10.100` | `200` | `OK` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236` | `200` | `OK` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?updateDate=[2023-03-31,2023-03-31]` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?updateDate=[2023-03-31,2023-03-31]` | `400` | `format is required` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&updateDate=[2023-03-31,2023-03-31]` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&updateDate=[2023-03-31,2023-03-31]` | `400` | `either doi or prefix is required` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&doi=10.100&updateDate=[2023-03-31,2023-03-31]` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&doi=10.100&updateDate=[2023-03-31,2023-03-31]` | `400` | `either doi or prefix is required` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&doi=10.100&updateDate=[2023-03-31,2023-03-31]` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&doi=10.100&updateDate=[2023-03-31,2023-03-31]` | `400` | `the syntax for DOI request is /ws/export-metadata?format=&doi=` |
> |Testing environment: <br/> `https://www-medra-dev.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&updateDate=[2023-03-31,2023-03-31]` <br/> Production environment: <br/> `https://www.medra.org/servlet/ws/export-metadata?format=ONIX&prefix=10.5236&updateDate=[2023-03-31,2023-03-31]` | `200` | `OK` |
>
> Moreover, further validations are made for each parameter present in the HTTP request, as the table below recaps:
>
> | **Parameter** | **Type** | **Validation** |
> | --- | --- | --- |
> | doi | DOIList | If the string is empty, a 400 Bad Request is returned with message `the value in doi is empty`. No further validation in made on the string syntax, neither in the DOI syntax or constraints |
> | prefix | string | If the string is empty, a 400 Bad Request is returned with message `the value in prefix is empty`. No further validation in made on the string syntax |
> | issn | string | If the string is empty, a 400 Bad Request is returned with message `the value in issn is empty`. No further validation in made on the string syntax |
> | isbn | string | If the string is empty, a 400 Bad Request is returned with message `the value in isbn is empty`. No further validation in made on the string syntax |
> | journalIssueNumber | string | If the string is empty, a 400 Bad Request is returned with message `the value in journalIssueNumber is empty`. No further validation in made on the string syntax |
> | journalIssueDate | Date | It's restrict to Date format, otherwise a 400 Bad Request is returned with message `the value in journalIssueDate is not valid`. Doesn't matter if the date really exists (i.e. the value `2324-13-33` or `2023-02-30` is accepted) |
> | format | Format | the value must be among those present in the enum Format, otherwise a 400 Bad Request is returned with message `the value format is not valid`. The same error is thrown in case of empty value in format parameter |
> | publicationDate | Date | It's restrict to Date format, otherwise a 400 Bad Request is returned with message `the value in publicationDate is not valid`. Doesn't matter if the date really exists (i.e. the value `2324-13-33` or `2023-02-30` is accepted) |
> | creationDate | DateRange | It's restrict to DateRange type, otherwise a 400 Bad Request is returned with message `the value in creationDate is not valid`. Doesn't matter if the date really exists (i.e. the value `2324-13-33` or `2023-02-30` is accepted), neither the accuracy of the range (i.e. `[2022-12-01,2021-12-01]` is accepted) |
> | updateDate | DateRange | It's restrict to DateRange type, otherwise a 400 Bad Request is returned with message `the value in updateDate is not valid`. Doesn't matter if the date really exists (i.e. the value `2324-13-33` or `2023-02-30` is accepted), neither the accuracy of the range (i.e. `[2022-12-01,2021-12-01]` is accepted) |

## HTTP Response
The HTTP response will contained a zip file (MIME type "application/zip").
## HTTP Status Response Code
The possible HTTP status code response are present in the following table:
> | **Code** | **Status** | **Message description** |
> | --- | --- | --- |
> | 200 | OK | Request successfully completed, the response contains the zip file with all the xml file generated |
> | 400 | Bad Request | Invalid request, i.e no mandatory parameter is present, Date format is not valid, no parameter is specified  |
> | 401 | Unauthorized | Invalid credentials (username or password is wrong) |
> | 403 | Forbidden | The user have no grant on prefix, or no right to export metadata |
> | 500 | Internal Server Error | Internal error while processing the request  |
