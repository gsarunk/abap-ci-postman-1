# ABAP CI with Postman

Visit my blog about this repository --> https://medium.com/pacroy/continuous-integration-in-abap-3db48fc21028

## Components

- *abap_unit_coverage.postman_collection.json* - Run ABAP Unit and check code coverage
- *abap_sci.postman_collection.json* - Run SCI via ATC
- *NPL.postman_environment.json* - Environment parameters - the 'config file'

## Running with Postman

1. Import JSON files into Postman.
2. Edit imported Environment parameters *NPL*
3. Setup proper Authorization in the first request
4. Test running the collection

## Running with Newman CLI

Example:

```
newman run abap_unit_coverage.postman_collection.json --insecure --bail --environment NPL.postman_environment.json --global-var username=username --global-var password=password
```

*Replace username and password with your SAP ID accordingly.

## Environment Parameters

| Name | Description |
| --- | --- |
| protocol | `http` or `https` |
| host | hostname of your SAP server\* |
| port | port of your SAP server\* |
| client | Your SAP client to run on |
| package | The package you want to run against, including its subpackages\** |
| coverage_type | `statement`, `branch`, or `procedure` |
| coverage_min | Minimum coverage percentage to 'pass' |
| coverage_maxlevel | Number of depth level to cumulate and display coverage result |
| coverage_chklevel | Number of depth level to check against minimum percentage. 0 means only top-level |
| exclusion | Object to excluded from coverage check in JSON array of `{"name": "", "type": "", "reason": ""}`. See coverage result for actual name and type to exclude. |
| atc_variant | SCI Variant to run the check |
| x-csrf-token | *Automatically filled during run* |

\* You can check the host and port via transaction `SICF` and select *Test Service*.  
\** You can also selectively run several packages, classes, or programs. Feel free to adjust the request XML. See object uri and type from *ABAP Communication Log* view in ADT.  
