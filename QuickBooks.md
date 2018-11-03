# Connect Quickbooks API using Python

One package we can use: `python-quickbooks`  
https://github.com/sidecars/python-quickbooks

Get Balance Sheet report in sandbox from QB API  
```
token = ***Access Token***
realmID = ***realmID***
URL = f"https://sandbox-quickbooks.api.intuit.com"+"/v3/company/{realmID}/reports/BalanceSheet"
res = requests.get(url=URL,headers={
    "Accept": "application/json",
    "Authorization":"Bearer "+token,
    "Accept":"*/*",
    "Content-Type":"application/json"
})
```

Post Data to QB (Create a vendor called Giant in QB)
```
token = ***Access Token***
realmID = ***realmID***
data = {
        "CompanyName": "Giant",
        "DisplayName": "Giant"
        }
URL = f"https://sandbox-quickbooks.api.intuit.com"+"/v3/company/{realmID}/vendor"
res = requests.post(url=URL,
    headers={
        "Accept": "application/json",
        "Authorization":"Bearer "+token,
        "Accept":"*/*",
        "Content-Type":"application/json"
    },
    json=data
)
```
