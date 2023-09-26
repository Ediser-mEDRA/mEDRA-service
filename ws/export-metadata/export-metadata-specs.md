# WEBSERVICE SPECIFICATIONS FOR EXPORT METADATA

This API allows mEDRA users who deposits content metadata in mEDRA systems to retrieve and then export it in different formats (Crossref, DOAJ, DOI schema, etc.) than the original one (ONIX). Each user with the need to use the present service must operated only in their(s) prefix(es).

## Endpoint

The API endpoint to access the service is \
Testing environement: `https://www-medra-dev.medra.org/servlet/ws/export-metadata` \
Production environement: `https://www.medra.org/servlet/ws/export-metadata`

## Autentication

The API service is accessible upon basic authentication. The credentials are the same used for the deposit in mEDRA systems.

## Authorization

> #### User

The authorization rules on user is the same already present in mEDRA systems, and each user is authorized to export metadata content of their(s) prefix(es).

> #### Prefix

Any user must operated only on their(s) prefix(es). Any request to the API service with prefix of others is forbidden.

## Http method

The Http method allowed is **GET**, and the api accepts the following [parameters](#Parameters)

## Parameters

The table below lists all the parameters (mandatory or optional) expected by the export metadata API service. There is no priority, order, etc., in parameters, the user could provide it (or them) to the API as prefered. The metadata export result is obtained considering all the parameters provided to the API in AND conditions. \
| **Parameter** | **Type** | **Case sensitive** | **Description** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- | --- |
| doi | DOIList | No | DOI List desired to obtain metadata | doi=10.5236/SAW
doi=10.5236/SAW,10.5236/SAV,10.5236/MONP,10.5236/MONW,10.5236/MONCHW,10.5236/STW
| For more than one DOI, the token separator is comma (,). Non more than 30 DOIs must be requested for metadata export |
