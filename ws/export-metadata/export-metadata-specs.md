# WEBSERVICE SPECIFICATIONS FOR EXPORT METADATA

This API allows mEDRA users who deposits content metadata in mEDRA systems to retrieve and then export it in different formats (Crossref, DOAJ, DOI schema, etc.) than the original one (ONIX). Each user with the need to use the present service must operate only in their(s) prefix(es).

## Endpoint

The API endpoint to access the service is
Testing environement: `https://www-medra-dev.medra.org/servlet/ws/export-metadata`
Production environement: `https://www.medra.org/servlet/ws/export-metadata`

## Autentication

The API service is accessible upon basic authentication. The credentials are the same used for the deposit in mEDRA systems.

## Authorization

### User

The authorization rules on user is the same already present in mEDRA systems, and each user is authorized to export metadata content of their(s) prefix(es).

### Prefix

Any user must operated only on their(s) prefix(es). Any request to the API service with prefix of others is forbidden.
