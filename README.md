# API Reference

## Authentication

Authentication is performed via HTTP Basic Auth.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

## Errors

The API uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a reservation failed, etc.).

## Handling errors

Our API raise exceptions for many reasons, such as a failed charge, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.

## Dates

The date format is ISO 8601 and can be passed in the local time of the tenant or in UTC.

For example:

2018-10-09T09:00:00

2018-10-09T07:00:00.000Z

## Local Development

To develop and test the API when developing locally, the developer needs to do the following to set it up:

1. Open the [superadmin localhost]([localhost superadmin](http://localhost:8080/admin/superadmin)) in your browser.

2. Go to the [Hosts page](http://localhost:8080/admin/superadmin/host) and add the following host if it doesn't exist yet:
  - **tenant:** mt
  - **host:** 127.0.0.99

3. Go to the ApiKeys page of our [localhost superadmin](http://localhost:8080/admin/superadmin/apikey) and generate a pair of keys, one for your **admin** requests and another for your **consumer** requests:
  - **name:** first name character + surname + _admin/consumer
  - **type:** admin/consumer

4. Save the user & password returned when generating each apiKey. This will be the one you'll need to perform the HTTP Basic Authentication.

> **NOTE:** You can copy the username afterwards, but not the password. However, you can reset the password too afterwards.

5. Click on the newly generated api key, and move to the **tenants** tab.

6. Click on "New" and add one of your local tenants, and an ApiKey that you are indicated. Otherwise, ask the Dev Team about your API Key.

---------------------------

> **ATENCIÓN:** Por defecto, los endpoints añadidos con `web.addApi` desde el servidor aplican un filtro de privilegios **admin** exclusivamente, salvo que se indique lo contrario al añadirlo con `web.addApi` con un parámetro `filter`.

> **INFO:** El endpoint y la lógica de /tenants está gestionada en el archivo [src/libs/stdlib/server.ts](../../libs/stdlib/server.ts), dentro de la función `serveApi`, y no se encuentra como el resto de endpoints en el archivo [src/api/server/main.ts](./main.ts)

| Name | Method | Endpoint | Privilege | Resource |
| - | - | - | - | - |
| [Tenants](#tenants) | GET | /tenants | - |
| [Tenant](#tenant) | GET | /tenant | consumer, admin |
| [Search Availability](#availability) | GET | /searchAvailability | consumer, admin | bookings
| [extras](#extras) | GET | /extras | consumer | bookings |
| [List reservation types](#listreservationtypes) | GET | /availabilityTypes | consumer | bookings |
| [Resources](#resources) | GET | /resources | consumer, admin | bookings |
| [Save Resources](#saveResources) | POST | /saveResources | admin | bookings |
| [Make reservations](#makereservations) | POST | /makeReservation | consumer | bookings |
| [Confirm reservations](#confirmreservations) | POST | /confirmReservation | consumer | bookings |
| [Cancel reservations](#cancelreservations) | POST | /confirmReservation | consumer | bookings |
| [Sale information](#saleinfo) | GET | /sale | consumer | bookings |
| [Bookings](#bookings) | GET | /bookings | consumer | bookings |
| [Reservation types](#reservationtypes) | GET | /reservationtypes | admin | - |
| [Teesheet Rules](#teesheetrules) | GET | /teesheetRules | admin | - |
| [Reservations](#reservations) | GET | /reservations | admin | - |
| [Clients](#clients) | GET | /clients | admin | - |
| [Clients Full](#clientsfull) | GET | /clientsFull | admin | - |
| [Save client](#SaveClient) | POST | /saveClient | admin | - |
| [ClientGroups](#clientgroups) | GET | /clientGroups| admin | - |
| [Save ClientGroups](#saveclientgroups) | GET | /saveClientGroups | admin | - |
| [Client tags](#clientTags) | GET | /clientTags | admin | - |
| [Save tag](#savetag) | POST | /saveTag | admin | - |
| [Save client tags](#saveclienttags) | GET | /saveClientTags | admin | - |
| [Delete client tag](#deleteclienttag) | GET | /deleteClientTag | admin | - |
| [Products](#products) | GET | /products | admin | - |
| [Save Products](#saveproducts) | POST | /saveProduct | admin | - |
| [Families (Departments)](#families) | GET | /families | admin | - |
| [Save Family (Department)](#savefamily) | POST | /saveFamily | admin | - |
| [Subfamilies](#subfamilies) | GET | /subfamilies | admin | - |
| [Save Subfamilies](#SaveSubFamilies) | POST | /saveSubfamily | admin | - |
| [Payments](#payments) | GET | /payments | admin | - |
| [Get Payment Methods](#paymentmethods) | GET | /paymentMethods | admin | - |
| [Save Payment Method](#savePaymentmethod) | POST | /savePaymentMethod | admin | - |
| [Salelines](#salelines) | GET | /salelines | admin | - |
| [ConfirmSalelines](#confirmSalelines) | POST | /confirmSalelines | admin | - |
| [Invoices](#invoices) | GET | /invoices | admin | - |
| [Tickets](#tickets) | GET | /tickets | admin | - |
| [Prices](#prices) | GET | /prices | admin | - |
| [Save price](#saveprice) | POST | /savePrice | admin | - |
| [Delete prices](#deleteprices) | POST | /deletePrice | admin | - |
| [New sale](#newSale) | POST | /newSale | admin | - |
| [Create sale](#createSale) | POST | /createSale | admin | - |
| [Cancel sales](#cancelSales) | POST | /cancelSales | admin | - |
| [Blockouts](#blockouts) | GET | /blockouts | admin | - |
| [Blockout](#blockout) | POST | /blockout | admin | - |
| [Cancel blockout](#cancelblockout) | POST | /cancelblockout | admin | - |
| [Tax Types](#taxtypes) | GET | /taxTypes | admin | - |
| [Save Tax Types](#savetaxtypes) | POST | /taxTypes | admin | - |
| [Get Memberships](#memberships) | GET | /membership | admin | - |
| [Save Memberships](#saveMemberships) | POST | /saveMembership | admin | - |
| [Get Membership Clients](#membershipClient) | GET | /membershipClient | admin | - |
| [Sale Membership to Clients](#saleMembership) | POST | /saleMembership | admin | - |
| [Get Voucher](#vouchers) | GET | /vouchers | admin | - |
| [Save Voucher](#saveVoucher) | POST | /saveVoucher | admin | - |
| [Get Voucher Products](#voucherProducts) | GET | /voucherProducts | admin | - |
| [Save Voucher Product](#saveVoucherProduct) | POST | /saveVoucherProduct | admin | - |
| [Get Voucher Movement](#voucherMovements) | GET | /voucherMovements | admin | - |
| [Get Voucher Recharge](#voucherRecharges) | GET | /voucherRecharges | admin | - |
| [Save Voucher Recharge](#saveVoucherRecharge) | POST | /saveVoucherRecharge | admin | - |
| [Get Voucher Types](#voucherTypes) | GET | /voucherTypes | admin | - |
| [Save Voucher Type](#saveVouchertype) | POST | /saveVoucherType | admin | - |
| [Get Areas](#areas) | GET | /areas | admin | - |
| [Save Area](#saveArea) | POST | /saveArea | admin | - |
| [Get Bookings Types](#bookingsTypes) | GET | /bookingsTypes | admin | - |
| [Save Booking Type](#saveBookingsType) | POST | /saveBookingsType | admin | - |
| [Get Bookings Resource Types](#bookingsResourceTypes) | GET | /bookingsResourceTypes | admin | - |
| [Save Booking Resource Type](#saveBookingsResourceType) | POST | /saveBookingsResourceType | admin | - |
| [Get Bookings Intervals](#bookingsIntervals) | GET | /bookingsIntervals | admin | - |
| [Save Booking Interval](#saveBookingsInterval) | POST | /saveBookingsInterval | admin | - |
| [Get Bookings Views](#bookingsViews) | GET | /bookingsView | admin | - |
| [Save Booking View](#saveBookingsView) | POST | /saveBookingsView | admin | - |
| [Save Bookings Type Tag](#saveBookingsTypeTag) | POST | /saveBookingsTypeTag | admin | - |
| [Get Bookings Configurations](#bookingsConfig) | GET | /bookingsConfig | admin | - |
| [Save Booking Configuration](#saveBookingsConfig) | POST | /saveBookingsConfig | admin | - |
| [Get Bookings Stocks](#bookingsStocks) | GET | /bookingsStock | admin | - |
| [Save Booking Stock](#saveBookingsStock) | POST | /saveBookingsStock | admin | - |
| [Delivery Notes](#deliverynotes) | GET | /deliveryNotes | admin | - |
| [Save Delivery Note](#savedeliverynote) | POST | /saveDeliveryNote | admin | - |
| [Delivery Lines](#deliverylines) | GET | /deliveryLines | admin | - |
| [Save Delivery Line](#savedeliveryline) | POST | /saveDeliveryLine | admin | - |
| [Cart](#cart) | GET | /cart | - | - |
| [Get Blog Posts](#getBlogPosts) | GET | /blog/posts | admin | - |
| [Save activity](#saveActivity) | POST | /saveActivity | admin | - |
| [Delete activity](#deleteActivity) | POST | /deleteActivity | admin | - |
| [Add client to activity](#addClientToActivity) | POST | /addClientToActivity | admin | - |
| [Delete cliente from activity](#deleteClientFromActivity) | "POST" | /deleteClientFromActivity | admin | - |
---------------------------


<h2 id="tenants">Tenants</h2>

Returns the tenants this key has access to.

Method: GET

Example request

```
$ curl -i https://mt.golfmanager.es/api/tenants \
   -u user:key
```

Example response

```json
["demo1","demo2","demo3"]
```


<h2 id="availability">Search availability</h2>

List available slots.

Method: GET

| Argument       | Type     | Required | Description                                                                                           |
| -------------- | -------- | -------- | ----------------------------------------------------------------------------------------------------- |
| tenant         | string   | yes      |                                                                                                       |
| start          | datetime | yes      | The start of the search period                                                                        |
| end            | datetime | yes      | The end of the search period                                                                          |
| slots          | int      | no       | The number of green fees (default is 1)                                                               |
| tags           | string[] | no       | Array of tags that the reservation types must have                                                    |
| idResource     | int      | no       | The resource id returned from /api/resources to limit results to a specific resource                  |
| idResourceType | int      | no       | The resource idResourceType returned from /api/resources to limit results to a specific resource type |

If idResourceType is omitted, the first resource type ordered by idResourceType is used.

List of valid tags:

    18holes
    9holes
    tee1
    tee10
    buggy
    trolley
    electric-trolley
    clubs


Example:

```bash
curl https://mt.golfmanager.es/api/searchAvailability \
 -u user:key \
 -d tenant=demo \
 -d start="2019-04-23T07:00:00" \
 -d end="2019-04-23T11:00:00" \
 -d slots=2
```

Example searching only for reservations that contain 9 or 18 holes:

```bash
curl https://mt.golfmanager.es/api/searchAvailability \
 -u user:key \
 -d tenant=demo \
 -d start="2019-04-23T07:00:00" \
 -d end="2019-04-23T11:00:00" \
 -d tags=["9holes", "18holes"]
 -d slots=2
```

Response:

Returns a list of slots:

| Argument               | Type          | Optional | Description                                                          |
| ---------------------- | ------------- | -------- | -------------------------------------------------------------------- |
| idType                 | int           | no       | The reservation type id.                                             |
| max                    | int           | no       | The maximum number of slots allowed.                                 |
| min                    | int           | no       | The minimum number of slots allowed.                                 |
| multiple               | int           | no       | In case this type must be reserved in multiples.                     |
| price                  | float         | no       | The price per slot including taxes.                                  |
| start                  | datetime      | no       | The date of this slot.                                               |
| tags                   | string[]      | no       | Array of tags to filter types.                                       |
| idResource             | prepayPercent | yes      | id of the available resource (Tee1 or Tee10 for example).            |
| resourceName           | prepayPercent | yes      | name of the available resource.                                      |
| resourceTags           | prepayPercent | yes      | tags of the available resource.                                      |
| minCancelAdvance       | datetime      | yes      | Limit date to cancel the reservation.                                |
| maxReservationsPerSale | int           | yes      | The maximum number of reservations in a sale.                        |
| maxReservationsPerDay  | int           | yes      | The maximum number of reservations that can be made in the same day. |
| maxActiveReservations  | int           | yes      | the maximum number of reservations that can be made in advance.      |
| onCredit               | bool          | yes      | If it is a sale  on credit.                                          |
| dueDate                | dueDate       | yes      | The sale due date if it is on credit.                                |
| prepayPercent          | prepayPercent | yes      | The % to pay when making the reservation.                            |

See above the list of valid tags.

Example:

```json
[
  {
    "idType": 1,
    "max": 4,
    "min": null,
    "multiple": null,
    "name": "Green Fee 18 holes",
    "price": 50,
    "start": "2018-11-09T10:00:00",
    "idResource": 1,
    "resourceName": "Tee 1",
    "resourceTags": [],
    "tags": [
      "18holes",
      "tee1"
    ]
  },
  {
    "idType": 3,
    "max": 4,
    "min": null,
    "multiple": null,
    "name": "Green Fee 9 holes",
    "price": 35,
    "start": "2018-11-09T10:00:00",
    "idResource": 1,
    "resourceName": "Tee 1",
    "resourceTags": [],
    "tags": [
      "9holes"
    ]
  },
  {
    "idType": 33,
    "max": 4,
    "min": 2,
    "multiple": 2,
    "name": "Pack 2 GF+ Buggy",
    "price": 59,
    "start": "2018-11-09T10:00:00",
    "idResource": 2,
    "resourceName": "Tee 10",
    "resourceTags": [],
    "tags": [
      "18holes",
      "buggy"
    ]
  }
]
```



 - [Reservation types](#listreservationtypes)
<h2 id="listreservationtypes">List reservation types</h2>

Methbod: GET

Arguments: optionally an array of tags to return only results containing those tags.

Example:

```bash
curl https://mt.golfmanager.es/api/availabilityTypes \
 -u user:key \
 -d tenant=demo
```

Or filtering by tag:

```bash
curl https://mt.golfmanager.es/api/availabilityTypes \
 -u user:key \
 -d tenant=demo \
 -d tags=["18holes", "9holes"]
```

Response:

```json
[
    {
        "description": "Precio por persona",
        "id": 1,
        "max": null,
        "min": null,
        "multiple": null,
        "name": "GF18",
        "tags": [
            "18holes"
        ]
    },
    {
        "description": "Oferta sólo Online!",
        "id": 2,
        "max": null,
        "min": null,
        "multiple": null,
        "name": "GF9",
        "tags": [
            "9holes"
        ]
    }
]
```



 - [Extras](#extras)
<h2 id="extras">List available extras</h2>

Methbod: GET

| Argument       | Type     | Required | Description                                         |
| -------------- | -------- | -------- | --------------------------------------------------- |
| tenant         | string   | yes      |                                                     |
| start          | datetime | yes      | The reservation date                                |
| idResourceType | datetime | no       | The resource type to which this extra is associated |

Example:

```bash
curl https://mt.golfmanager.es/api/extras \
 -u user:key \
 -d tenant=demo \
 -d start="2019-08-23T07:00:00"
```

Response:

```json
[
  {
    "config": {
      "createDate": "2019-06-14T13:43:26Z",
      "deleted": false,
      "dueDate": null,
      "id": 22,
      "idClient": null,
      "idClientGroup": null,
      "idCreateUser": 129,
      "idMembership": null,
      "idType": null,
      "maxActiveReservations": null,
      "maxAdvance": null,
      "maxReservationsPerDay": null,
      "maxReservationsPerSale": null,
      "minAdvance": null,
      "minCancelAdvance": null,
      "prepayPercent": 25,
      "timeout": "20m"
    },
    "description": "Alquiler Moto 18",
    "icon": null,
    "id": 88,
    "idResource": null,
    "max": null,
    "min": null,
    "multiple": null,
    "name": "Moto Alquiler",
    "price": 22,
    "quantity": 5,
    "rack": 22
  }
]
```










<h2 id="makereservations">Make reservations</h2>

Methbod: POST

Arguments: an array of reservation objects. Each reservations must specify:

| Argument   | Type     | Required | Description                                                               |
| ---------- | -------- | -------- | ------------------------------------------------------------------------- |
| idType     | int      | yes      | The reservation type                                                      |
| start      | datetime | yes      | The date of this slot                                                     |
| timeout    | datetime | no       | The date when it will be released if it is not confirmed                  |
| idResource | int      | no       | The resource id returned from /api/resources to force a specific resource |
| name       | string   | no       | The client's name                                                         |
| email      | string   | no       | The client's email                                                        |
| customTag  | string   | no       | Extra information for the club; a single word is recommended              |

Example:

```bash
curl https://mt.golfmanager.es/api/makeReservation \
 -u user:key \
 -d tenant=demo \
 -d 'reservations=[{"idType":1,"start":"2018-11-09T10:00:00%2B02:00"}]'
```

Response:

Return reservations with their ID in case they need to be canceled. It also returns the sale information.

Example:

```json
{
    "cart": {
        "idSale": 7729,
        "quantity": 2,
        "total": 116.8,
        "units": 2
    },
    "reservations": [
        {
            "email": null,
            "end": "2019-07-06T08:00:00+02:00",
            "id": 40857,
            "idParentReservation": null,
            "idSale": 7729,
            "idType": 1,
            "isExtra": null,
            "name": "n.,m",
            "reference": "33DS",
            "start": "2019-07-06T07:50:00+02:00",
            "timeout": "2019-07-05T18:13:39.655208969+02:00"
        },
        {
            "email": null,
            "end": "2019-07-06T10:20:00+02:00",
            "id": 40859,
            "idParentReservation": null,
            "idSale": 7729,
            "idType": 29,
            "isExtra": null,
            "name": null,
            "reference": "33DS",
            "start": "2019-07-06T07:50:00+02:00",
            "timeout": "2019-07-05T18:13:39.655208969+02:00"
        }
    ]
}
```


<h2 id="confirmreservations">Confirm reservations</h2>

Confirm reservations that where created with a timeout.

Methbod: POST

| Argument       | Type     | Required | Description                                         |
| -------------- | -------- | -------- | --------------------------------------------------- |
| tenant         | string   | no       |                                                     |
| ids            | array    | yes      | The reservations IDs                                |
| paymentMethod  | string   | no       | The method used to pay for the reservations         |

If paymentMethod is present, it will be used to pay for all the reservations.
If it isn't, only reservations that don't require payment will be confirmed, otherwise the API will throw an error.
In order to confirm reservations with price zero, the payment method must be omitted.
A payment method with that name must already exist in the database or the API will throw an error.

Example:

```bash
curl https://mt.golfmanager.es/api/confirmReservation \
 -u user:key \
 -d tenant=demo \
 -d 'ids=[234]'
```

Response:

If it succeeded or the error.

Example:

```json
{ "success": true }
```


<h2 id="cancelreservations">Cancel reservations</h2>

Cancel reservations by id.

Methbod: POST

Example:

```bash
curl https://mt.golfmanager.es/api/cancelReservation \
 -u user:key \
 -d tenant=demo \
 -d 'ids=[234]'
```

Response:

If it succeeded or the error.

Example:

```json
{ "success": true }
```



<h2 id="saleinfo">Sale information</h2>

Show information about a sale by id.

Methbod: GET

Example:

```bash
curl https://mt.golfmanager.es/api/sale \
 -u user:key \
 -d tenant=demo \
 -d 'id=34'
```

Response:

```json
{
    "lines": [
        {
            "canceled": false,
            "createDate": "2019-01-29T19:04:46.618880302Z",
            "description": "GF18, Tee 1, 31-01-2019 10:00, 3LG1B, John Smith",
            "onCredit": false,
            "paid": false,
            "prepayPercent": 0,
            "temp": true,
            "total": 0
        }
    ]
}
```

### Bookings

List reservations created bu the API client

Method: GET

| Argument          | Type     | Required | Description                       |
| --------          | -------- | -------- | --------------------------------- |
| tenant            | string   | yes      | Tenant name                       |
| start             | datetime | yes      | Start date and time search period |
| end               | datetime | yes      | End date and time search period   |
| id                | int      | no       | Filter reservation by id          |
| includeExtras     | bool     | no       | Include extras                    |
| includeCrossovers | bool     | no       | Include crossovers                |

Example:

```bash
curl https://mt.golfmanager.es/api/bookings \
 -u user:key \
 -d tenant=demo \
 -d start=2018-12-14T08:00:00%2B01:00 \
 -d end=2018-12-14T18:00:00%2B01:00
```

Response:

Return a list of reservations

Example:

```json
[
    {
        "beneficiaryNationality": "USA",
        "checkin": false,
        "confirmDate": null,
        "createDate": "2019-11-20T17:58:46.204610474Z",
        "end": "2019-11-20T19:08:46.203014019Z",
        "id": 1,
        "idResource": 3,
        "idSale": 1209,
        "idSaleLine": 12358,
        "idType": 1,
        "noShow": false,
        "paid": false,
        "productName": "GF 18",
        "reference": "HJK30",
        "start": "2019-11-20T18:58:46.203014019Z",
        "total": 150
    }
]
```













# Admin





<h2 id="tenant">Tenant</h2>

Returns general information about the tenant like phone, address, etc...

Methbod: GET

Example:

```bash
curl https://mt.golfmanager.es/api/tenant \
 -d tenant=demo \
 -u user:key
```

Response:

Example:

```json
{
    "country": "Spain",
    "culture": "es-ES",
    "currency": "EUR",
    "email": "info@golfmanager.com",
    "image": "392416535538319349sA1PFATw5.png",
    "latitude": "40.2269911",
    "logo": "3899613330138759642L7prno4J.png",
    "longitude": "-3.2406688",
    "name": "Demo Golf Club",
    "phone": "636236052",
    "province": "Madrid",
    "street": "Orense 64",
    "town": "Madrid",
    "web": "https://golfmanager.com",
    "zipCode": "28020",
    "timezoneName": "Atlantic/Canary",
}
```





<h2 id="reservationtypes">Reservation Types</h2>

List reservation types

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| ids      | int[]  | no       | The id or ids to be fetched                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/reservationtypes \
 -u user:key \
 -d tenant=demo
```

Response:

Example:

```json
[
    {
        "description": null,
        "end": null,
        "id": 1,
        "idProduct": 1,
        "idResource": 1,
        "idResourceType": 1,
        "max": null,
        "min": null,
        "multiple": null,
        "name": "GF18",
        "productName": "Test Product",
        "resourceName": "Tee test",
        "resourceTypeName": "Green fees",
        "start": null,
        "tags": "18holes",
        "weekDays": 127,
        "resources": [],
        "extras": []
    }
]
```

<h2 id="resources">Resources</h2>

List resources

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |
| search   | string | no       | Search resources by text                                      |

Example:

```bash
curl https://mt.golfmanager.es/api/resources \
 -u user:key \
 -d tenant=demo
```

Response:
If the `hideOnline` property is set to true, the resource must not be used to create reservations even if it shows availability.

Example:

```json
[
    {
        "id": 1,
        "idResourceType": 1,
        "name": "Tee 1",
        "hideOnline": false,
        "resourceTypeName": "Green fees",
        "tags": [
            "tee1"
        ]
    },
    {
        "id": 2,
        "idResourceType": 1,
        "name": "Tee 10",
        "hideOnline": true,
        "resourceTypeName": "Green fees",
        "tags": [
            "tee10"
        ]
    }
]
```

<h2 id="saveResources">Save Resources</h2>

Save resources

Method: POST

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/resources \
 -u user:key \
 -d tenant=demo
```

Response:
If the `hideOnline` property is set to true, the resource must not be used to create reservations even if it shows availability.

Example:

```json
[
    {
        "id": 1,
        "idResourceType": 1,
        "name": "Tee 1",
        "hideOnline": false,
        "resourceTypeName": "Green fees",
        "tags": [
            "tee1"
        ]
    },
    {
        "id": 2,
        "idResourceType": 1,
        "name": "Tee 10",
        "hideOnline": true,
        "resourceTypeName": "Green fees",
        "tags": [
            "tee10"
        ]
    }
]
```

<h2 id="teesheetRules">Teesheet Rules</h2>

List slots

Method: GET

| Argument | Type     | Required | Description                    |
| -------- | -------- | -------- | ------------------------------ |
| tenant   | string   | yes      | Tenant name                    |
| start    | datetime | yes      | The start of the search period |
| end      | datetime | yes      | The end of the search period   |

Example:

```bash
curl https://mt.golfmanager.es/api/teesheetRules \
 -u user:key \
 -d tenant=demo \
 -d start="2019-01-01T23:00:00.000Z" \
 -d end="2019-01-02T17:23:00.000Z"
```

Response:

Example:

```json
{
    "resourceTypes": [
        {
            "id": 2,
            "name": "Buggies",
            "online": false,
            "slots": 2,
            "stock": true
        },
        {
            "id": 1,
            "name": "Green fees",
            "online": false,
            "slots": 4,
            "stock": false
        }
    ],
    "resources": [
        {
            "id": 1,
            "name": "Tee 1",
            "notOnline": false
        }
    ],
    "slots": [
        {
            "day": "2019-01-01",
            "intervals": [
                {
                    "end": null,
                    "endTime": "14:00",
                    "id": 1,
                    "idResourceType": 1,
                    "name": "test",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": "09:00",
                    "weekDays": 127
                },
                {
                    "end": null,
                    "endTime": "22:00",
                    "id": 2,
                    "idResourceType": 1,
                    "name": "test",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": "14:00",
                    "weekDays": 127
                }
            ],
            "types": [
                {
                    "end": null,
                    "endTime": null,
                    "id": 1,
                    "idResource": 1,
                    "idResourceType": 1,
                    "max": null,
                    "min": null,
                    "multiple": null,
                    "name": "GF18",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": null,
                    "tags": [
                        "18holes"
                    ],
                    "weekDays": 127,
                    "duration": 10
                },
                {
                    "end": null,
                    "endTime": null,
                    "id": 2,
                    "idResource": null,
                    "idResourceType": 1,
                    "max": null,
                    "min": null,
                    "multiple": null,
                    "name": "GF9",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": null,
                    "tags": [
                        "9holes"
                    ],
                    "weekDays": 127
                }
            ]
        },
        {
            "day": "2019-01-02",
            "intervals": [
                {
                    "end": null,
                    "endTime": "14:00",
                    "id": 1,
                    "idResourceType": 1,
                    "name": "test",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": "09:00",
                    "weekDays": 127
                },
                {
                    "end": null,
                    "endTime": "22:00",
                    "id": 2,
                    "idResourceType": 1,
                    "name": "test",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": "14:00",
                    "weekDays": 127
                }
            ],
            "types": [
                {
                    "end": null,
                    "endTime": null,
                    "id": 1,
                    "idResource": 1,
                    "idResourceType": 1,
                    "max": null,
                    "min": null,
                    "multiple": null,
                    "name": "GF18",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": null,
                    "tags": [
                        "18holes"
                    ],
                    "weekDays": 127
                },
                {
                    "end": null,
                    "endTime": null,
                    "id": 2,
                    "idResource": null,
                    "idResourceType": 1,
                    "max": null,
                    "min": null,
                    "multiple": null,
                    "name": "GF9",
                    "online": false,
                    "priority": 0,
                    "start": null,
                    "startTime": null,
                    "tags": [
                        "9holes"
                    ],
                    "weekDays": 127
                }
            ]
        }
    ],
    "stocks": [
        {
            "end": null,
            "id": 1,
            "idResourceType": 2,
            "name": "Summer",
            "priority": 0,
            "start": null,
            "stock": 25
        }
    ]
}
```





### Reservations

List reservations

Method: GET

| Argument          | Type     | Required | Description                       |
| --------          | -------- | -------- | --------------------------------- |
| tenant            | string   | yes      | Tenant name                       |
| start             | datetime | yes      | Start date and time search period |
| end               | datetime | yes      | End date and time search period   |
| idClient          | int      | no       | Filter reservations by client id  |
| includeExtras     | bool     | no       | Include extras                    |
| includeCrossovers | bool     | no       | Include crossovers                |

Example:

```bash
curl https://mt.golfmanager.es/api/reservations \
 -u user:key \
 -d tenant=demo \
 -d start=2018-12-14T08:00:00%2B01:00 \
 -d end=2018-12-14T18:00:00%2B01:00
```

Response:

Return a list of reservations

Example:

```json
[
    {
        "beneficiaryGroupName": "Visitor",
        "beneficiaryNationality": "USA",
        "checkin": false,
        "clientGroupName": "TTOO A Crédito",
        "clientNationality": "Spain",
        "confirmDate": null,
        "createDate": "2019-11-20T17:58:46.204610474Z",
        "end": "2019-11-20T19:08:46.203014019Z",
        "familyName": "Golf",
        "id": 1,
        "idBeneficiary": 2,
        "idBeneficiaryGroup": 2,
        "idClient": 1,
        "idClientGroup": 1,
        "idFamily": 1,
        "idProduct": 1,
        "idResource": 3,
        "idSale": 1209,
        "idSaleLine": 12358,
        "idSubfamily": 1,
        "idType": 1,
        "noShow": false,
        "online": false,
        "paid": false,
        "productName": "GF 18",
        "reference": "HJK30",
        "start": "2019-11-20T18:58:46.203014019Z",
        "subfamilyName": "Gree fees",
        "total": 150
    }
]
```

<h2 id="clientgroups">Client groups</h2>

List client groups

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/clientGroups \
 -u user:key \
 -d tenant=demo
```

Response:

Example:

```json
[
    {
        "id": 1,
        "name": "Agents"
    }
]
```

<h2 id="saveclientgroups">Save Client groups</h2>

Save a ClientGroup. If it has an id it will update it, otherways it will create a new one.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveClientGroups \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"John\",\"color\":\"#EEEEEE\"}"
```

Response:

The ID of the modified or created resource.

### SaveClient

Save a client. If it has an id it will update it, otherways it will create a new one.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveClient \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"John\",\"nationality\":\"ES\",\"gender\":1,\"idGroup\":40}"
```

Response:

The ID if it is created. Nothing if it is an update.


### Client Tags

<h2 id="clientTags">Save tag</h2>

List client groups

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/clientTags \
 -u user:key \
 -d tenant=demo
```

Response:

```json
[
    {
      //TODO...
    }
]
```

### SaveTag

<h2 id="savetag">Save tag</h2>

Save a tag. If it has an id it will update it, otherways it will create a new one.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveTag \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"test123\"}"
```

Response:

The ID if it is created. Nothing if it is an update.


### Clients

List clients

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| search   | string | no       | Search clients by text                                      |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl -X GET https://mt.golfmanager.es/api/clients \
 -u user:key \
 -d tenant=demo \
 -d search=a \
 -d count=500
```

Response:

Return a list of clients:

| Argument | Type   | Description      |
| -------- | ------ | ---------------- |
| id       | int    | The client id    |
| name     | string | The client name  |
| email    | string | The client email |

Example:

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@test.com"
  },
  {
    "id": 2,
    "name": "Jane Doe",
    "email": "janedoe@test.com"
  }
]
```


### ClientsFull

Lists clients with all their properties

Method: GET

| Argument        | Type   | Required | Description                                                 |
| --------------- | ------ | -------- | ----------------------------------------------------------- |
| tenant          | string | yes      | Tenant name                                                 |
| id              | number | no       | Search clients by id (exact match)                          |
| email           | string | no       | Search clients by email (exact match)                       |
| phone           | string | no       | Search clients by phone (exact match)                       |
| search          | string | no       | Search clients by name (contains)                           |
| centerCard      | string | no       | Search clients by center card (exact match)                 |
| memberCode      | string | no       | Search clients by member code (exact match)                 |
| updateDateStart | date   | no       | Search clients modified after this date                     |
| updateDateEnd   | date   | no       | Search clients modified before this date                    |
| offset          | int    | no       | The offset of the first row to be returned                  |
| count           | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/clientsFull -G \
 -u user:key \
 -d tenant=demo \
 -d search=foo \
 -d count=500
```

Response:

Returns a list of clients:

| Argument | Type   | Description      |
| -------- | ------ | ---------------- |
| id       | int    | The client id    |
| name     | string | The client name  |
| email    | string | The client email |
| ...      | ...    | ...              |

Example:

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "johndoe@test.com",
    ...
  },
  {
    "id": 2,
    "name": "Jane Doe",
    "email": "janedoe@test.com",
    ...
  }
]
```

<h2 id="saveclienttags">Adds tags to a client</h2>

Method: POST

| Argument | Type   | Required | Description      |
| -------- | ------ | -------- | -----------      |
| tenant   | string | yes      | Tenant name      |
| idTags   | array  | yes      | Array of tag IDs |
| idClient | int    | yes      | The client ID    |

Example:

```bash
curl https://mt.golfmanager.es/api/saveClientTags \
 -u user:key \
 -d tenant=demo \
 -d idTags=[5, 15] \
 -d idClient=10
```

<h2 id="deleteclienttag">Delete client tag</h2>

Method: POST

| Argument | Type   | Required | Description |
| -------- | ------ | -------- | ----------- |
| tenant   | string | yes      | Tenant name |
| idTag    | int    | yes      | Tag ID      |
| idClient | int    | yes      | Client ID   |

Example:

```bash
curl https://mt.golfmanager.es/api/deleteClientTag \
 -u user:key \
 -d tenant=demo \
 -d idTag=5 \
 -d idClient=10
```

### Products

List products

Method: GET

| Argument   | Type   | Required | Description                                                 |
| ---------- | ------ | -------- | ----------------------------------------------------------- |
| tenant     | string | yes      | Tenant name                                                 |
| search     | string | no       | Search products by text                                     |
| sellOnline | string | no       | Allowed to be selled online                                 |
| offset     | int    | no       | The offset of the first row to be returned                  |
| count      | int    | no       | The maximum number of rows to be returned. (default is 100) |

Available values for sellOnline:

| Value  | Description                                          |
| ------ | ---------------------------------------------------- |
| true   | All products with the sell online check, checked     |
| false  | All products with the sell online check, not checked |
| none   | All products, with or without sell online            |

Example:

```bash
curl https://mt.golfmanager.es/api/products \
 -u user:key \
 -d tenant=demo \
 -d search=a \
 -d sellOnline=true \
 -d count=500
```

Response:

Return a list of products:

| Argument | Type   | Description      |
| -------- | ------ | ---------------- |
| id       | int    | The product id   |
| name     | string | The product name |

Example:

```json
[
  {
    "basePercent": null,
    "id": 1,
    "idBaseProduct": null,
    "idSubfamily": 1,
    "name": "Test Product 1",
    "price": 50
  }
]
```

### Saveproducts

Create or update a product

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveProduct \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"Name\",\"price\":\"1\",\"idSubfamily\":\"2\"}"
```

Returns the Id of the product

### Families

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/families \
 -u user:key \
 -d tenant=demo \
 -d search=a \
 -d count=500
```

Response:

Return a list of families/departments:

| Argument | Type   | Description      |
| -------- | ------ | ---------------- |
| id       | int    | The family id    |
| name     | string | The family name  |
| code     | string | The family code  |

Example:

```json
[
  {
    "id": 1,
    "name": "Green Fees",
    "code": "GF"
  }
]
```

<h2 id="savefamily">Save a family</h2>

Save a Family. If it has an id it will update it, otherways it will create a new one.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveFamily \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"Greenfees\",\"code\":\"GF\"}"
```

Response:

The ID of the modified or created family.

### Subfamilies

List subfamilies

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/subfamilies \
 -u user:key \
 -d tenant=demo \
 -d count=500
```

Response:

Return a list of subfamilies:

| Argument    | Type   | Description                   |
| ----------- | ------ | ------------------            |
| id          | int    | The subfamily id              |
| name        | string | The subfamily name            |
| code        | string | The subfamily code            |
| account     | string | The subfamily account         |
| familyName  | string | The subfamily's parent family |
| companyName | string | The subfamily's company       |

Example:

```json
[
  {
    "id": 1,
    "name": "Subfamily test",
    "code": null,
    "account": "123123",
    "familyName": "Family test",
    "companyName": null,
  }
]
```

### SaveSubFamilies

Create a new Subfamily or update an existing one. To do an update the field id must be included in the JSON.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example to create a new one:

```bash
curl https://mt.golfmanager.es/api/saveSubfamily \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"Greenfees\",\"idFamily\":\"2\"}"
```

Example to update an existing subfamily:

```bash
curl https://mt.golfmanager.es/api/saveSubfamily \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"New Name\",\"id\":\"23\"}"
```

Response:

The ID of the modified or created resource.

### Payments

List payments filtered by dates or client

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| start    | date   | no       | Start date                                                  |
| end      | date   | no       | End date                                                    |
| idClient | int    | no       | Client ID. Either the ID or the range of dates is required  |

Example:

```bash
curl https://mt.golfmanager.es/api/payments \
 -u user:key \
 -d tenant=demo \
 -d start=2020-08-29 \
 -d end=2020-08-30T15:16:17
```

Response:

Returns a list of payments:

| Argument | Type   | Description      |
| -------- | ------ | ---------------- |
| id       | int    | The payment id   |
| amount   | float  | Payment amount   |

The function returns many more properties, including those created by the club.

Example:

```json
[
  {
    "id": 1,
    "amount": 1.5,
    ...
  }
]
```


### Salelines

List salelines filtered by dates or client

Method: GET

| Argument  | Type   | Required | Description                                                 |
| --------  | ------ | -------- | ----------------------------------------------------------- |
| tenant    | string | yes      | Tenant name                                                 |
| start     | date   | no       | Start date                                                  |
| end       | date   | no       | End date. Maximum date range is 90 days                     |
| idClient  | int    | no       | Client ID. Either the ID or the range of dates is required  |
| byUseDate | bool   | no       | Filter by use date. Default is create date                  |

Example:

```bash
curl https://mt.golfmanager.es/api/salelines \
 -u user:key \
 -d tenant=demo \
 -d start=2020-08-29 \
 -d end=2020-08-30T15:16:17
```

Response:

Returns a list of salelines:

| Argument    | Type   | Description         |
| --------    | ------ | ------------------- |
| id          | int    | The payment id      |
| total       | float  | Saleline total      |
| productName | string | Nombre del producto |
| clientName  | string | Nombre del cliente  |
| memberCode  | string | Número de socio     |
| barcode     | string | Product's bar code  |

The function returns many more properties, including those created by the club.

Example:

```json
[
  {
    "id": 1,
    "total": 1.5,
    ...
  }
]
```

<h2 id="confirmSalelines">Confirm Salelines</h2>

Mark salelines as paid.

Method: POST

| Argument | Type  | Required | Description        |
| -------- | ----- | -------- | ------------------ |
| ids      | int[] | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/confirmSalelines \
 -u user:key \
 -d tenant=demo \
-d ids=[1,2]
 ```

### Invoices

List invoices filtered by dates or client

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| start    | date   | no       | Start date                                                  |
| end      | date   | no       | End date. Maximum date range is 90 days                     |
| idClient | int    | no       | Client ID. Either the ID or the range of dates is required  |

Example:

```bash
curl https://mt.golfmanager.es/api/invoices \
 -u user:key \
 -d tenant=demo \
 -d start=2020-08-29 \
 -d end=2020-08-30T15:16:17
```

Response:

Returns a list of invoices:

| Argument    | Type   | Description         |
| --------    | ------ | ------------------- |
| id          | int    | The invoice id      |
| name        | string | Client name         |
| number      | string | Invoice number      |
| lines       | array  | Invoice lines       |
| ...         | ...    | ...                 |

The function returns many more properties, including those created by the club.

Example:

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "number": "FAT 201",
    "lines": [
      {
        "id": 1,
        "idSaleline": 1,
        "description": "Product 1",
        "total": 11.22,
        ...
      }
    ]
    ...
  }
]
```


### Tickets

List tickets filtered by dates, id or number

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| start    | date   | no       | Start date                                                  |
| end      | date   | no       | End date. Maximum date range is 90 days                     |
| id       | int    | no       | Ticket id                                                   |
| number   | string | no       | Ticket number                                               |

* Either dates or id/number are required

Example:

```bash
curl https://mt.golfmanager.es/api/tickets \
 -u user:key \
 -d tenant=demo \
 -d start=2020-08-29 \
 -d end=2020-08-30T15:16:17
```

Response:

Returns a list of tickets:

| Argument    | Type   | Description         |
| --------    | ------ | ------------------- |
| id          | int    | The ticket id       |
| clientName  | string | Client name         |
| number      | string | Ticket number       |
| lines       | array  | Ticket lines        |
| payments    | array  | Ticket payments     |
| client      | json   | Client Info         |
| ...         | ...    | ...                 |

The function returns many more properties, including those created by the club.

Example:

```json
[
  {
    "id": 1,
    "clientName": "John Doe",
    "number": "FAT 201",
    "lines": [
      {
        "id": 1,
        "idSaleline": 1,
        "description": "Product 1",
        "total": 11.22,
        ...
      }
    ]
    ...
  }
]
```


### Prices

List prices

Method: GET

| Argument      | Type   | Required | Description                                                 |
| ------------- | ------ | -------- | ----------------------------------------------------------- |
| tenant        | string | yes      | Tenant name                                                 |
| offset        | int    | no       | The offset of the first row to be returned                  |
| count         | int    | no       | The maximum number of rows to be returned. (default is 100) |
| idProduct     | int    | no       | Filter prices by product ID                                 |
| idClientGroup | int    | no       | Filter prices by client group ID                            |

Example:

```bash
curl https://mt.golfmanager.es/api/prices \
 -u user:key \
 -d tenant=demo
```

Response:

Example:

```json
[
    {
        "channel": null,
        "end": null,
        "endTime": null,
        "holiday": false,
        "id": 1,
        "idAgeGroup": null,
        "idClient": null,
        "idClientGroup": null,
        "idFamilySales": null,
        "idMembership": null,
        "idProduct": 1,
        "maxAdvance": null,
        "maxSales": null,
        "minAdvance": null,
        "minSales": null,
        "name": "Twilight",
        "price": 100,
        "priority": 0,
        "start": null,
        "startTime": null,
        "weekdays": 0
    }
]
```


<h2 id="saveprice">Save price</h2>

Save a price. If it has an id it will update it, otherways it will create a new one.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/savePrice \
 -u user:key \
 -d tenant=demo \
 -d data="{\"idProduct\":1,\"name\":\"Twilight\",\"price\":100,\"priority\":0,\"weekDays\":127}"
```

Response:

The ID if it is created. Nothing if it is an update.

<h2 id="deleteprices">Delete prices</h2>

Delete multiple prices

Method: POST

| Argument | Type   | Required | Description              |
| -------- | ------ | -------- | ------------------------ |
| tenant   | string | yes      | Tenant name              |
| idPrices | int[]  | yes      | Array with the price ids |

Example:

```bash
curl https://mt.golfmanager.es/api/deletePrices \
 -u user:key \
 -d tenant=demo \
 -d idPrices=[1,2]
```

















### newSale

Creates new sale

Method: POST

| Argument       | Type   | Required | Description      |
| -------------- | ------ | -------- | ---------------- |
| tenant         | string | yes      | Tenant name      |
| idProduct      | int    | yes      | The product id   |
| idClient       | int    | yes      | The client id    |
| parentName     | int    | yes      | Referer name     |
| idParent       | int    | yes      | Referer id       |
| idCashRegister | int    | no       | Cash register id |

Example:

```bash
curl https://mt.golfmanager.es/api/newSale \
 -u user:key \
 -d tenant=demo \
 -d idProduct=1 \
 -d idClient=1 \
 -d parentName="Test platform" \
 -d idParent=1
```

Response:

Return SaleLine id:

| Argument   | Type | Description     |
| ---------- | ---- | --------------- |
| saleLineId | int  | The SaleLine id |

Example:

```json
[
  {
    "saleLineId": 1
  },
  {
    "saleLineId": 2
  }
]
```

### createSale

Creates new sale and optionally pays for the items

Method: POST

| Argument       | Type   | Required | Description      |
| -------------- | ------ | -------- | ---------------- |
| tenant         | string | yes      | Tenant name                                    |
| idClient       | int    | yes      | The client id                                  |
| paymentMethod  | string | no       | Payment method used to pay for the lines       |
| idVoucher      | int    | no       | The id of the voucher if paying with one       |
| parentName     | int    | no       | Referer name                                   |
| idParent       | int    | no       | Referer id                                     |
| idCashRegister | int    | no       | Cash register id                               |
| salelines      | array  | yes      | The salelines including idProduct and quantity |

Example:

```bash
curl https://mt.golfmanager.es/api/createSale \
 -u user:key \
 -d tenant=demo \
 -d salelines='[{ "idProduct": 1, "quantity": 2 }]' \
 -d idClient=1 \
 -d paymentMethod=Visa
```

Response:
An object with two properties: idSale, lines

Example:

```json
{
  idSale: 1,
  lines:
  [
    {
      "id": 1,
      "total": 10,
      ...
    },
    {
      "id": 2,
      "total": 20,
      ...
    }
  ]
}
```

### cancelSales

Cancel multiple sales

Method: POST

| Argument    | Type   | Required | Description                 |
| ----------- | ------ | -------- | --------------------------- |
| tenant      | string | yes      | Tenant name                 |
| idSaleLines | int[]  | yes      | Array with the saleline ids |

Example:

```bash
curl https://mt.golfmanager.es/api/cancelSales \
 -u user:key \
 -d tenant=demo \
 -d idLines=[1,2]
```

### blockouts

List blockouts

Method: GET

| Argument   | Type     | Required | Description                            |
| ---------- | -------- | -------- | -------------------------------------- |
| tenant     | string   | yes      | Tenant name                            |
| idResource | int      | no       | The resource id                        |
| start      | datetime | no       | Start date and time for blocking slots |
| end        | datetime | no       | End date and time for blocking slots   |

Example:

```bash
curl https://mt.golfmanager.es/api/blockouts \
 -u user:key \
 -d tenant=demo
 -d idResource=2
 -d start='2019-04-12'
```


Response:

Example:

```json
[
  {
    "bgColor": "#138533",
    "createDate": "2019-03-29T13:02:36Z",
    "deleted": false,
    "end": "2019-04-13T21:59:59Z",
    "endTime": 52800000,
    "fgColor": "#901a1a",
    "id": 85,
    "idCreateUser": 53,
    "idResource": 2,
    "name": "Bloqueo Torneos",
    "start": "2019-04-12T22:00:00Z",
    "startTime": 28800000,
    "weekDays": 127
  },
  {
    "bgColor": "#d49595",
    "createDate": "2019-06-11T11:42:35Z",
    "deleted": false,
    "end": "2019-06-22T22:00:00Z",
    "endTime": 38400000,
    "fgColor": "#901a1a",
    "id": 118,
    "idCreateUser": 129,
    "idResource": 2,
    "name": "Bloqueo",
    "start": "2019-06-22T22:00:00Z",
    "startTime": 27000000,
    "weekDays": 127
  }
]
```

### blockout

Block slots in the occupation table

Method: POST

| Argument   | Type     | Required | Description                            |
| ---------- | -------- | -------- | -------------------------------------- |
| tenant     | string   | yes      | Tenant name                            |
| idResource | int      | yes      | The resource id                        |
| start      | datetime | yes      | Start date and time for blocking slots |
| end        | datetime | yes      | End date and time for blocking slots   |
| name       | string   | no       | Name to label the blocked slots        |
| bgColor    | string   | no       | Background color for slots             |
| fgColor    | string   | no       | Foreground color for slots             |

Example:

```bash
curl https://mt.golfmanager.es/api/blockout \
 -u user:key \
 -d tenant=demo \
 -d idResource=1 \
 -d start=2018-12-14T08:00:00%2B01:00 \
 -d end=2018-12-14T18:00:00%2B01:00 \
 -d name=Test tournament \
 -d bgColor=#000000 \
 -d fgColor=#ffffff \
```


Response:

The object created with its id

Example:

```json
{
    "id": 26,
    "idResource": 1,
    "start": "2018-12-14T08:00:00%2B01:00",
    "end": "2018-12-14T18:00:00%2B01:00",
    "name": null,
    "bgColor": null,
    "fgColor": null,
}
```

<h2 id="cancelblockout">Cancel blockout</h2>

Cancel a blockout by ID

Method: POST

| Argument | Type   | Required | Description            |
| -------- | ------ | -------- | ---------------------- |
| tenant   | string | yes      | Tenant name            |
| id       | int    | yes      | The blockout object id |

Example:

```bash
curl https://mt.golfmanager.es/api/cancelblockout \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

<h2 id="taxtype">Tax Types</h2>

Get all Tax Types

Method: GET

| Argument | Type   | Required | Description            |
| -------- | ------ | -------- | ---------------------- |
| tenant   | string | yes      | Tenant name            |
| id       | int    | no       | The taxType  object id |

Example:

```bash
curl https://mt.golfmanager.es/api/taxTypes \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

<h2 id="savetaxtype">Create or update Tax Types</h2>

Create or update a tax Types

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveTaxTypes \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"Name\",\"percent\":\"1\",\"code\":\"CO\",\"description\":\"My tax\"}"
```

<h2 id="memberships">Get Memberships</h2>

Get all memberships

Method: GET

| Argument | Type   | Required | Description              |
| -------- | ------ | -------- | ------------------------ |
| tenant   | string | yes      | Tenant name              |
| id       | int    | no       | The membership object id |

Example:

```bash
curl https://mt.golfmanager.es/api/membership \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

<h2 id="saveMemberships">Update or create Memberships</h2>

Create or update a Membership

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveMembership \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Membership\",\"period\":\"1\",\"idProduct\":1}"
```

Available period values:

| Id  | Description    |
| --- | -------------- |
| 1   | single         |
| 3   | fortnight      |
| 4   | month          |
| 5   | bimonth        |
| 6   | trimester      |
| 7   | fourMonths     |
| 8   | semester       |
| 9   | year           |
| 10  | yearFromStart  |

---------------------------

<h2 id="membershipClient">Get Membership Client</h2>

Get all membership clients.

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| id       | int    | no       | The membership client object id                                    |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |
| start    | datetime | yes    | Start date and time for membership |
| end      | datetime | yes    | End date and time for membership   |
| idParent | int      | no     | Filter by clients |
| idMembership | int  | no     | Filter membership clients by memberships |
| idParent | int      | no     | Filter membership clients by parent |
| activated | int     | no     | Filter membership clients by activation status |

Example:

```bash
curl https://mt.golfmanager.es/api/membershipClient \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

<h2 id="saleMembership">Sale Membership to Client</h2>

Create or update a Membership Client (and its sale)

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |
| idSale   | int  | no       | If available, the id of the sale you want it to assign to |
| paid     | bool | no       | If true, it will mark the client as activated |

NOTE: If you mark a membershipClient as paid, a new sale will be generated either way (with a price of 0€). If desired, the saleline can be confirmed by passing the returned id to the `confirmSalelines` endpoint.

Example:

```bash
curl https://mt.golfmanager.es/api/saleMembership \
 -u user:key \
 -d tenant=demo \
 -d data="{\"start\": \"2022-07-15T23:00:00Z\", \"description\": null, \"idBankAccount\": null, \"idClient\": 1, \"idMembership\": 1}"
 -d paid=true
```

### vouchers

Get all vouchers

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| id       | int    | no       | The voucher object id                                       |
| idClient | int    | no       | Get vouchers by id client                                   |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

```bash
curl https://mt.golfmanager.es/api/vouchers \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveVoucher

Create or update a Voucher

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveVoucher \
 -u user:key \
 -d tenant=demo \
 -d data="{\"comments\":\"Comment\",\"remaining\":\"1\",\"unlimited\":1,\"weekdays\":1,\"online\":1}"
```

### voucherProducts

Get all voucher Products

Method: GET

| Argument | Type   | Required | Description              |
| -------- | ------ | -------- | ------------------------ |
| tenant   | string | yes      | Tenant name              |
| id       | int    | no       | The voucher object id    |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

```bash
curl https://mt.golfmanager.es/api/voucherProducts \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveVoucherProduct

Create or update a Voucher Product

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveVoucherProduct \
 -u user:key \
 -d tenant=demo \
 -d data="{\"idProduct\":\"324\",\"idType\":\"12\",\"ratio\":1}"
```

### voucherMovements

Get all voucher movements

Method: GET

| Argument | Type   | Required | Description              |
| -------- | ------ | -------- | ------------------------ |
| tenant   | string | yes      | Tenant name              |
| id       | int    | no       | The voucher movement object id    |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |
| fromDate | date   | no       | From this creation date |
| toDate   | date   | no       | Until this creation date |

```bash
curl https://mt.golfmanager.es/api/voucherMovements \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### voucherRecharges

Get all voucher recharges

Method: GET

| Argument | Type   | Required | Description              |
| -------- | ------ | -------- | ------------------------ |
| tenant   | string | yes      | Tenant name              |
| id       | int    | no       | The voucher recharge object id    |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

```bash
curl https://mt.golfmanager.es/api/voucherRecharges \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveVoucherRecharge

Create or update a Voucher Recharge

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveVoucherRecharge \
 -u user:key \
 -d tenant=demo \
 -d data="{\"idVoucher\":\"324\",\"idVoucherMovement\":\"12\",\"amount\":1}"
```

### voucherTypes

Get all voucher types

Method: GET

| Argument | Type   | Required | Description              |
| -------- | ------ | -------- | ------------------------ |
| tenant   | string | yes      | Tenant name              |
| id       | int    | no       | The voucher type object id    |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

```bash
curl https://mt.golfmanager.es/api/voucherTypes \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveVoucherType

Create or update a Voucher Type

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Allowed modes:
 - 1: money
 - 2: units
 - 3: products

Example:

```bash
curl https://mt.golfmanager.es/api/saveVoucherType \
 -u user:key \
 -d tenant=demo \
 -d data="{\"idProduct\":\"324\",\"unlimited\":\"0\",\"amount\":1,\"name\":\"My Name\",\"mode\":\"1\"}"
```


### Paymentmethods

Get all payment methods

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| id       | int    | no       | The paymentMethod object id to recover                      |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/paymentMethods \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### SavePaymentmethod

Create or update a Payment Method

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/savePaymentmethod \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"field\":\"1\",\"otherField\":1}"
```

### areas

Get all Bookings Areas

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| id       | int    | no       | The Area object id to recover                               |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/areas -G \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveArea

Create or update a Bookings Area

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveArea \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"id\":\"1\"}"
```

### bookingsTypes

Get all bookings types

Method: GET

| Argument    | Type   | Required | Description                                                   |
| --------    | ------ | -------- | ------------------------------------------------------------- |
| tenant         | string | yes      | Tenant name                                                   |
| id             | int    | no       | The Type object id to recover                                 |
| offset         | int    | no       | The offset of the first row to be returned                    |
| count          | int    | no       | The maximum number of rows to be returned. (default is 100)   |
| includeTags    | bool   | no       | Includes an array with the IDs of tags associated to the type |
| idResourceType | int    | no       | If included, returns the bookings Resource Types filtered by their ResourceType id |

Example:

```bash
curl https://mt.golfmanager.es/api/bookingsTypes -G \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveBookingsType

Create or update a Bookings Type

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsType \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"idResourceType\":\"1\"}"
```

### bookingsResourceTypes

Get all bookings resource types

Method: GET

| Argument    | Type   | Required | Description                                                   |
| --------    | ------ | -------- | ------------------------------------------------------------- |
| tenant      | string | yes      | Tenant name                                                   |
| id          | int    | no       | The Type object id to recover                                 |
| offset      | int    | no       | The offset of the first row to be returned                    |
| count       | int    | no       | The maximum number of rows to be returned. (default is 100)   |
| name        | string | no       | If included, returns the bookings Resource Types filtered by their name |

Example:

```bash
curl https://mt.golfmanager.es/api/bookingsResourceTypes -G \
 -u user:key \
 -d tenant=demo \
 -d id=1
```

### saveBookingsResourceType

Create or update a Bookings Resource Type

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsResourceType \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"slots\":\"4\"}"
```

### bookingsIntervals

Get all the Bookings Intervals

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |
| id       | int    | no       | Filter by ID                                                |

Example:

```bash
curl https://mt.golfmanager.es/api/bookingsIntervals -G \
 -u user:key \
 -d tenant=demo \
```

### saveBookingsInterval

Store or update a Booking Interval

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsInterval \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"idResourceType\":\"1\",\"duration\":\"10\",\"priority\":\"1\",\"bgcolor\":\"#bac0ba\"}"
```

### bookingsViews

Get all the Bookings Views

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |
| id       | int    | no       | Filter by ID                                                |

Example:

```bash
curl https://mt.golfmanager.es/api/bookingsView -G \
 -u user:key \
 -d tenant=demo \
```

### saveBookingsView

Store or update a Booking View

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsView \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"priority\":\"1\",\"pixelsPerMin\":\"1\",\"hourColumnInterval\":\"1\"}"
```

### bookingsConfigs

Get all the Bookings Configurations

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/bookingsConfig -G \
 -u user:key \
 -d tenant=demo \
```

### saveBookingsConfig

Store or update a Bookings Configuration

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsConfig \
 -u user:key \
 -d tenant=demo \
 -d data="{\"name\":\"My Name\",\"idClient\":1,\"idType\":1,\"maxReservationsPerDay\":1}"
```

### bookingsStocks

Get all the Bookings Stocks

Method: GET

| Argument       | Type   | Required | Description                                                 |
| -------------- | ------ | -------- | ----------------------------------------------------------- |
| tenant         | string | yes      | Tenant name                                                 |
| offset         | int    | no       | The offset of the first row to be returned                  |
| count          | int    | no       | The maximum number of rows to be returned. (default is 100) |
| idResourceType | int    | no       | Filter by resource type                                     |

Example:

```bash
curl https://mt.golfmanager.es/api/bookingsStock -G \
 -u user:key \
 -d tenant=demo \
```

### saveBookingsStock

Store or update a Booking Stock

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsStock \
 -u user:key \
 -d tenant=demo \
 -d data="{\"idResourceType\":1,\"name\":\"My Name\",\"priority\":1,\"stock\":1,\"start\":\"1\"}"
```

### saveBookingsTypeTag

Store or update a Booking Type Tag

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveBookingsTypeTag \
 -u user:key \
 -d tenant=demo \
 -d data="{\"idTag\":1,\"idTag\":1}"
```

### DeliveryNotes

List delivery notes

Method: GET

| Argument   | Type   | Required | Description                                                 |
| ---------- | ------ | -------- | ----------------------------------------------------------- |
| tenant     | string | yes      | Tenant name                                                 |
| id         | int    | no       | Get delivery note by id                                    |
| offset     | int    | no       | The offset of the first row to be returned                  |
| count      | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/products \
 -u user:key \
 -d tenant=demo \
```

Response:

Return a list of delivery notes:

| Argument | Type   | Description      |
| -------- | ------ | ---------------- |
| id       | int    | The product id   |
| name     | string | The product name |

Example:

```json
[
  {
    "comments": null,
    "date": "2022-09-08T22:00:00Z",
    "description": null,
    "id": 110,
    "idSupplier": null,
    "idWarehouse": 1,
    "number": null,
    "status": 1,
  }
]
```

### SaveDeliveryNote

Create or update a delivery note

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveDeliveryNote \
 -u user:key \
 -d tenant=demo \
 -d data='{"idWarehouse":1,"status":1,"date":"2022-09-09"}'
```

Returns the id of the delivery note


### DeliveryLines

List delivery lines

Method: GET

| Argument   | Type   | Required | Description                                                 |
| ---------- | ------ | -------- | ----------------------------------------------------------- |
| tenant     | string | yes      | Tenant name                                                 |
| idDelivery | int    | no       | Get delivery lines by delivery note id                      |
| offset     | int    | no       | The offset of the first row to be returned                  |
| count      | int    | no       | The maximum number of rows to be returned. (default is 100) |

Example:

```bash
curl https://mt.golfmanager.es/api/deliverylines \
 -u user:key \
 -d tenant=demo \
```

Response:

Return a list of delivery lines:

| Argument   | Type   | Description      |
| ---------- | ------ | ---------------- |
| id         | int    | The product id   |
| idDelivery | string | The product name |

Example:

```json
[
  {
    "id": 257,
    "idDelivery": 109,
    "idProduct": 1800,
    "netUnitCost": 3.25,
    "quantity": 2,
    "received": 1,
  }
]
```

### SaveDeliveryLine

Create or update a delivery line

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveDeliveryLine \
 -u user:key \
 -d tenant=demo \
 -d data='{"idDelivery":110,"quantity":110,"received":4,"idProduct":1801,"netUnitCost":2}'
```

Returns the id of the delivery note

### getBlogPosts

If the tenant has the blog module installed, get all posts

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| search   | string | no       | Searchs by title                                            |
| offset   | int    | no       | The offset of the first row to be returned                  |
| count    | int    | no       | The maximum number of rows to be returned. (default is 100) |
| priority | int    | no       | THe priority used to sort the blog posts                    |

Example:

```bash
curl https://mt.golfmanager.es/api/blog/posts -G \
 -u user:key \
 -d tenant=demo \
 -d search="my search"
```

### cart

Returns...

Method: GET

| Argument | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| tenant   | string | yes      | Tenant name                                                 |
| idSale   | int | yes       |  ID of the sale                                            |
Example:

```bash
curl https://mt.golfmanager.es/api/blog/posts -G \
 -u user:key \
 -d tenant=demo \
 -d idSale=1
```

### saveActivity

Save an activity. If it has an id it will update it, otherways it will create a new one.

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| data     | json | yes      | The object as json |

Example:

```bash
curl https://mt.golfmanager.es/api/saveActivity \
 -u user:key \
 -d tenant=demo \
 -d data='{"name":"activity name","description":"activity description","start":"10/10/2022","idProduct":1801}'
```

Response:

The ID of the modified or created family.

Required properties:
- name: string
- start: datetime
- description: string


### deleteActivity

Delete activity

Method: POST

| Argument | Type | Required | Description                |
| -------- | ---- | -------- | -------------------------- |
| id       | int  | yes      | Id of activity to delete   |

Only activities created from the API can be deleted

Example:

```bash
curl https://mt.golfmanager.es/api/deleteActivity \
 -u user:key \
 -d tenant=demo \
 -d id=325
```

### addClientToActivity

Add a client to an activity

Method: POST

| Argument   | Type | Required | Description        |
| ---------- | ---- | -------- | ------------------ |
| idClient   | int  | yes      | Client's ID        |
| idActivity | int  | yes      | Activity's ID      |

Example:

```bash
curl https://mt.golfmanager.es/api/addClientToActivity \
 -u user:key \
 -d tenant=demo \
 -d idClient=4274
 -d idActivity=31
```

Response:

The ID of the registration.

### deleteClientFromActivity

Delete a client from an activity

Method: POST

| Argument | Type | Required | Description        |
| -------- | ---- | -------- | ------------------ |
| id       | int  | yes      | Registration ID    |

Registration ID is the ID returned by addClientToActivity. 

Example:

```bash
curl https://mt.golfmanager.es/api/deleteClientFromActivity \
 -u user:key \
 -d tenant=demo \
 -d id=325
```


## Terms of Service

- Thank you for using Golfmanager! When you develop on the Golfmanager Platform,
you agree to be bound by the following terms, so please read them carefully.

- The API is provided as-is and without any warranty whatsoever. Golfmanager is not liable for any
damage due to unavailable or incorrect APIs.

- Whilst Golfmanager uses all reasonable endeavours to correct any errors or omissions on the
Golfmanager Platform as soon as practicable once they have been brought to Golfmanager's
attention, Golfmanager makes no promises, guarantees, representations or warranties of
any kind whatsoever (express or implied).

- Abuse or excessively frequent requests to Golfmanager via the API may result in
the temporary or permanent suspension of your Account's access to the API. Golfmanager,
in our sole discretion, will determine abuse or excessive usage of the API. We will make
a reasonable attempt to warn you via email prior to suspension.

- Golfmanager has the right to change these General API Terms and Conditions and
any Specific API Terms and Conditions.