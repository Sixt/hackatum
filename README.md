# Sixt @hackaTUM 
Sixt is on the way from being Europe's leading car rental company to becoming a global mobility provider that will disrupt the entire market. Take your place on the driver seat of this journey and choose if you want to build a more secure way of carsharing using blockchain, improve user experience via AR or create anything else simply awesome with our APIs and telematic solutions which allow you to unlock the car with a web-service call.

# STYLEGUIDE
[http://styleguide.sixt.io](http://styleguide.sixt.io)

# API

## Telematics
### Available Cars

BMW i8 | BMW 3er | BMW 1er
--- | --- | ---
WBY2Z61040VG33170 | WBA8J11070A698134 | WBA1S710707B62821

### Unlock
```GET https://hackatum.goorange.sixt.com/vehicle/:vin/unlock"```

**Query parameters:**

`vin`: `WBY2Z61040VG33170` or `WBA8J11070A698134` or `WBA1S710707B62821`

#### Response
```
{
    "status": "ERROR"
}
```
##### Notes
`status`: `OK` or `ERROR`


---

### Lock
```GET https://hackatum.goorange.sixt.com/vehicle/:vin/lock"```

#### Response
```
{
    "status": "ERROR"
}
```

**Query parameters:**

`vin`: `WBY2Z61040VG33170` or `WBA8J11070A698134` or `WBA1S710707B62821`

##### Notes
`status`: `OK` or `ERROR`


---

## Locations Search
### Request
```
GET https://web-api.orange.sixt.com/v1/locations?term=<term>&latitude=<latitude>&<longitude>
```
**Query parameters:**

- term="term to search"
- latitude=-90.0 to 90.0
- longitude=-180.0 to 180.0 

**Additional information:**

1. `type` can be `location` or `station`, if not set result is combination ot both `location` or `station`.
2. `Locale` (`language`) is resolved by upported locales are de_DE, en_US

**Parameters requirements**
`Term` is required, all other parameters are optional.

### Response
```
[
    {
      "id": "S_11",
      "title": "Munich Airport",
      "subtitle": "Terminalstr. Mitte/MWZ, 85356 München, Germany",
      "type": "station",
      "subtypes": ["airport", "car", "motorcycle", "truck"]
    },{
      "id": "L_ChIJ2V-Mo_l1nkcRfZixfUq4DAE",
      "title": "München",
      "subtitle": "München, Deutschland",
      "type": "location",
      "subtypes": ["locality", "political", "geocode"]
    }
...
]
```
**Note:** 

- Stations `ID-s` have prefix `S_`.
- Locations `ID-s` have prefix `L_`.

#### Success

| HTTP Status Code      |
|:-----------------|
|`200 OK` |

#### Errors

| HTTP Status Code      | Error Codes |
|:-----------------|:------------|
|`400 Bad Request` |`INVALID_TERM`, `INVALID_PROVIDER`, `INVALID_VEHICLE_TYPE`|

See Status Codes / Errors for other errors that may occur

---

## Location GEO search
### Request
```
GET https://web-api.orange.sixt.com/v1/locations/geo?latitude=<latitude>&longitude=<longitude>
```
**Query parameters:**

- latitude=-90.0 to 90.0
- longitude=-180.0 to 180.0  

**Additional information:**

1. Supported locales are de_DE, en_US

**Parameters requirements**
`latitude` and `longitude` are required, all other parameters are optional.

### Response
```
[
    {
      "id": "S_11",
      "title": "Munich Airport",
      "subtitle": "Terminalstr. Mitte/MWZ, 85356 München, Germany",
      "type": "station",
      "subtypes": ["airport", "car", "motorcycle", "truck"],
      "coordinates": {
        "latitude": 48.1351253,
        "longitude": 11.5819806
      }
    }
...
]
```

#### Success

| HTTP Status Code      |
|:-----------------|
|`200 OK` |

#### Errors

| HTTP Status Code      | Error Codes |
|:-----------------|:------------|
|`400 Bad Request` |`WRONG_COORDINATES`, `INVALID_PROVIDER`, `INVALID_VEHICLE_TYPE`|

---

## Offer
### Query for available offers

Sending a **GET** request on the resource `/v1/rentaloffers/offers?pickupStation={stationId}&returnStation={stationId}&pickupDate={ISO8601}&returnDate={ISO8601}&areaCode=de&vehicleType=car` will return all available offers for given search criteria.

* **vehicleType** should be **car**
* **driverBirthday** can be used to affect the prices according to the actual driver's age. Format is YYYY-MM-DD, example: 1990-06-20
* **age** same as driverBirthday, but in number of years. Will only be used if driverBirthday is empty/not set. Example: 21

### Request
```
https://web-api.orange.sixt.com/v1/rentaloffers/offers?pickupStation=<pickupStation>&returnStation=<returnStation>&pickupDate=<PICKUP_DATE>&returnDate=<RETURN_DATE>&areaCode=de&vehicleType=car
```

### Response
```json
{
  "info": {
    "rentalInformationUrl": "string",
    "taxInformation": "string",
    "termsAndConditionsUrl": "string"
  },
  "offers": [{
    "acrissCode": "string",
    "additionalCharges": [{
      "amount": 0,
      "description": "string",
      "descriptionBullets": [
        "string"
      ],
      "enabled": true,
      "iconUrl": "string",
      "id": "string",
      "maxAmount": 0,
      "price": {
        "amount": {
          "currency": "string",
          "display": "string",
          "value": 0
        },
        "prefix": "string",
        "taxInfo": "string",
        "tracking": 0,
        "trackingNet": 0,
        "unit": "string"
      },
      "subCharges": [
        null
      ],
      "subtitle": "string",
      "title": "string",
      "type": "string"
    }],
    "billingSections": [{
      "items": [
        null
      ],
      "price": {
        "amount": {
          "currency": "string",
          "display": "string",
          "value": 0
        },
        "prefix": "string",
        "taxInfo": "string",
        "tracking": 0,
        "trackingNet": 0,
        "unit": "string"
      },
      "reference": "string",
      "title": "string",
      "type": "string"
    }],
    "vehicleType": "car",
    "vehicleGroupInfo": {
      "airCondition": true,
      "automatic": true,
      "baggage": {
        "bags": 0,
        "suitcases": 0
      },
      "bodyStyle": "string",
      "bodyStyleKey": "string",
      "doors": 0,
      "driverRequirements": {
        "licenseCategory": "string",
        "licenseMinYears": 0,
        "minAge": 0,
        "youngDriverAge": 0
      },
      "maxPassengers": 0,
      "modelExample": {
        "additionalExamples": [
          "string"
        ],
        "imageUrl": "string",
        "name": "string"
      },
      "modelGuaranteed": true,
      "navigationSystem": true,
      "premium": true,
      "luxury": true
    },
    "description": "string",
    "id": "string",
    "images": {
      "large": "string",
      "medium": "string",
      "small": "string"
    },
    "includedCharges": [{
      "title": "string"
    }],
    "onRequest": true,
    "payment": {
      "paymentMethods": [{
        "code": "string",
        "name": "string"
      }],
      "paymentOptions": [{
        "diffPrice": {
          "amount": {
            "currency": "string",
            "display": "string",
            "value": 0
          },
          "prefix": "string",
          "taxInfo": "string",
          "tracking": 0,
          "trackingNet": 0,
          "unit": "string"
        },
        "id": "string",
        "price": {
          "amount": {
            "currency": "string",
            "display": "string",
            "value": 0
          },
          "prefix": "string",
          "taxInfo": "string",
          "tracking": 0,
          "trackingNet": 0,
          "unit": "string"
        }
      }],
      "paymentRequired": true,
      "selectedPaymentOption": "string"
    },
    "prices": {
      "dayPrice": {
        "amount": {
          "currency": "string",
          "display": "string",
          "value": 0
        },
        "prefix": "string",
        "taxInfo": "string",
        "tracking": 0,
        "trackingNet": 0,
        "unit": "string"
      },
      "payablePrice": {
        "amount": {
          "currency": "string",
          "display": "string",
          "value": 0
        },
        "prefix": "string",
        "taxInfo": "string",
        "tracking": 0,
        "trackingNet": 0,
        "unit": "string"
      },
      "totalPrice": {
        "amount": {
          "currency": "string",
          "display": "string",
          "value": 0
        },
        "prefix": "string",
        "taxInfo": "string",
        "tracking": 0,
        "trackingNet": 0,
        "unit": "string"
      }
    },
    "sortIndexes": {
      "name": 0,
      "popularity": 0,
      "price": 0
    },
    "splashImages": [{
      "url": "string"
    }],
    "status": "string",
    "unlimited": true
  }]
}
```


#### Success

| HTTP Status Code      |
|:-----------------|
|`200 OK` |

#### Errors

| HTTP Status Code      | Error Codes |
|:-----------------|:------------|
|`404 Not Found` |`NOT_FOUND`|
|`401 Unauthorized` |`n/a`|
|`400 Bad Request` |`EMPTY_PICKUP_STATION`|
|`404 Bad Request` |`INVALID_PICKUP_STATION`|
|`404 Bad Request` |`EMPTY_RETURN_STATION`|
|`404 Bad Request` |`INVALID_RETURN_STATION`|
|`404 Bad Request` |`EMPTY_PICKUP_DATE`|
|`404 Bad Request` |`INVALID_PICKUP_DATE`|
|`404 Bad Request` |`EMPTY_RETURN_DATE`|
|`404 Bad Request` |`INVALID_RETURN_DATE`|
|`404 Bad Request` |`INVALID_CAR_TYPE`|
|`500 Internal Server Error` |`n/a`|
|`504 Gateway Timeout` |`n/a`|




---
