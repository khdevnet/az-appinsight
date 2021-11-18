# az-appinsight
```
// count of requests by name
let start=datetime("2021-08-01T10:00:00.000Z");
let end=datetime("2021-08-31T10:59:00.000Z");
let dataset=requests
    // additional filters can be applied here
    | where timestamp > start and timestamp < end
    | where resultCode == 200
    | where (cloud_RoleName == 'customer-api');// select a filtered set of requests and count them by name
dataset
| where ((tolower(url) == "https://customer-api/api/cars/get"))// change 'operation_Name' on the below line to segment by a different property
| summarize count_=sum(itemCount), val=1 by request=operation_ParentId
| summarize countVal=sum(val) by cv1=val


let start=datetime("2021-08-01T00:00:00.000Z");
let end=datetime("2021-08-31T23:59:00.000Z");
let dataset=requests
    // additional filters can be applied here
    | where timestamp > start and timestamp < end
    | where resultCode == 200
    | where (cloud_RoleName == 'customer-api');// select a filtered set of requests and count them by name
dataset
| where ((tolower(url) == "https://customer-api/api/cars/get"))// change 'operation_Name' on the below line to segment by a different property
| count



let start=datetime("2021-08-01T00:00:00.000Z");
let end=datetime("2021-08-31T23:59:00.000Z");
let dataset=traces
    // additional filters can be applied here
    | where timestamp > start and timestamp < end
    | where message startswith "After POST /cars/add";
dataset | count
```
