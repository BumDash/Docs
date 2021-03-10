---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---
# Intro
BumDash - Docs

# Create Parent - Customer in Stripe

## Request
`POST https://us-east1-bumdash-sandbox.cloudfunctions.net/CreateParent` 

<aside class="notice">
The URL is a standin for now
</aside>

>Requests require the following keys

```javascript
{
  "name":"John Smith",
  "email":"john@gmail.com"
}
```

| Parameter | Type   | Description             |
|-----------|--------|-------------------------|
| email     | String | Email Address of parent |
| name      | String | Full name of parent     |


## Response 

>Response looks like the following

```javascript
{
  "stripe_id":"cus_12345",
  "email":"john@gmail.com"
}
```

| Parameter | Type   | Description                                      |
|-----------|--------|--------------------------------------------------|
| stripe_id | String | Stripe customer ID to be saved to users table    |
| email     | String | Email Address of parent - to ensure data matches |


# setupIntent

`POST https://us-east1-bumdash-sandbox.cloudfunctions.net/setup` 

<aside class="notice">
The URL is a standin for now
</aside>

>Requests require the following keys

```javascript
{
  "id":"cus_1234"
}
```

| Parameter | Type   | Description                                        |
|-----------|--------|----------------------------------------------------|
| id        | String | Stripe customer ID of customer - from createParent |



## Response 

>Response looks like the following

```javascript
{
  "clientSecret":"1234"
}
```

| Parameter    | Type   | Description                                            |
|--------------|--------|--------------------------------------------------------|
| clientSecret | String | secret to be associated for all future payment intents |

# Set Default Payment

`POST https://us-east1-bumdash-sandbox.cloudfunctions.net/Payment` 

<aside class="notice">
On return from creating the payment method, fire this endpoint to save the payment as 'default' on stripe.
</aside>

>Requests require the following keys

```javascript
{
  "id":"cus_1234",
  "payment_id": "pm_5678"
}
```

| Parameter  | Type   | Description                                   |
|------------|--------|-----------------------------------------------|
| id         | String | Stripe customer ID of parent                  |
| payment_id | String | Stripe payment ID of recently created payment |

## Response 

>Response looks like the following

```javascript
{
  "id":"cus_1234"
}
```

| Parameter | Type   | Description                             |
|-----------|--------|-----------------------------------------|
| id        | String | Stripe customer ID of parent to confirm |

# Delete/Detach Payment

`DELETE https://us-east1-bumdash-sandbox.cloudfunctions.net/Payment` 

<aside class="notice">
This is used when customers want to delete and add a new card
</aside>

>Requests require the following keys

```javascript
{
  "id":"cus_1234",
  "payment_id": "pm_5678"
}
```

| Parameter  | Type   | Description                                   |
|------------|--------|-----------------------------------------------|
| id         | String | Stripe customer ID of parent                  |
| payment_id | String | Stripe payment ID of recently created payment |

## Response 

>Response looks like the following

```javascript
{
  "id":"pm_5678"
}
```

| Parameter | Type   | Description                                   |
|-----------|--------|-----------------------------------------------|
| id        | String | Stripe payment ID of recently created payment |

# Edit Payment

`PATCH https://us-east1-bumdash-sandbox.cloudfunctions.net/Payment` 

<aside class="notice">
This only lets a customer edit fields around a payment. To modify Card number, delete and add a new one.
For the fields that are not required only update the field if they're included. Omitted fields will remain what they are prior
</aside>

>Requests require the following keys

```javascript
{
  "id": "cus_J2N9TBvFHSudKf", 
  "payment_id":"pm_1IQIPIF8Q3XD74KdMOvzydvF", 
  "exp_month":"06", 
  "exp_year":"2026", 
  "address_line1":"400 Market St", 
  "address_line2":"Unit 112", 
  "city":"Chapel Hill", 
  "country":"US", 
  "postal_code":"27516", 
  "email":"test@bumdash.com", 
  "name":"John doe", 
  "phone":"+19199995408"
}
```

| Parameter     | Type   | Required | Description                                                                                                                              |
|---------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| id            | String | True     | Stripe customer ID of parent                                                                                                             |
| payment_id    | String | True     | Stripe payment ID of recently created payment                                                                                            |
| address_line1 | String | False    | Updated house and street description                                                                                                     |
| address_line2 | String | False    | Unit number or apartment                                                                                                                 |
| city          | String | False    | City of billing address                                                                                                                  |
| country       | String | False    | 2 digit initial of billing country. See https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements for more info |
| postal_code   | String | False    | Postal code of billing address                                                                                                           |
| state         | String | False    | State of billing address                                                                                                                 |
| email         | String | False    | Email of billing contact                                                                                                                 |
| name          | String | False    | Name of billing contact                                                                                                                  |
| phone         | String | False    | Phone for billing contact                                                                                                                |
| exp_month     | String | False    | Expiration month of card (0 prefixed or not)                                                                                             |
| exp_year      | String | False    | Expiration year of card (2 digits or 4)                                                                                                  |

## Response 

>Response looks like the following

```javascript
{
  "payment_id":"pm_5678"
}
```

| Parameter  | Type   | Description                                   |
|------------|--------|-----------------------------------------------|
| payment_id | String | Stripe payment ID of recently created payment |

# Get Payment

`GET https://us-east1-bumdash-sandbox.cloudfunctions.net/Payment` 

<aside class="notice">
This only lets a customer edit fields around a payment. To modify Card number, delete and add a new one.
For the fields that are not required only update the field if they're included. Omitted fields will remain what they are prior
</aside>

>Requests with params would look like the below

```javascript
Example URL with params:
`https://us-east1-bumdash-sandbox.cloudfunctions.net/Payment?id=cus_J2N9TBvFHSudKf&payment=pm_1IQIPIF8Q3XD74KdMOvzydvF`
```

| Parameter | Type   | Description                                                        |
|-----------|--------|--------------------------------------------------------------------|
| id        | String | Stripe customer ID of parent                                       |
| payment   | String | Stripe payment ID of customers  payment. Can be active or detached |


## Response 

>Response looks like the following

```javascript
{
  "payment_id":"pm_5678",
  "last_four":"1111",
  "card_type":"visa"
}
```

| Parameter  | Type   | Description                                   |
|------------|--------|-----------------------------------------------|
| payment_id | String | Stripe payment ID of recently created payment |
| last_four  | String | Last four digits of payment method            |
| card_type  | String | Card type of payment method if it's a card    |


# Get Customers Route

`POST https://us-east1-bumdash-sandbox.cloudfunctions.net/FindDeliveryDay` 

<aside class="notice">
The URL is a standin for now
</aside>

>Requests require the following keys

```javascript
{
  "lat": 35.248246, 
  "lng":-80.819442
}
```

| Parameter | Type  | Description                          |
|-----------|-------|--------------------------------------|
| lat       | float | Latitude in degrees of the customer  |
| lng       | float | Longitude in degrees of the customer |



## Response 

>Response looks like the following

```javascript
{
  "route":"tcVhaslMyaGEnwlqwgn6"
}
```

| Parameter | Type   | Description                                                                                                                                               |
|-----------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| route     | String | routeID as is stored in the database within the `routes` collection. If the coordinates are out of the service area, the value returns as `Unserviceable` |

# Subscription Management
<aside class="notice">
    This is a work in progress as we figure out the best way to do this. Currently `POST` and creating a subscription is the action of 'activating' a subscription. Pausing isn't currently supported but will be eventually likely as a `PUT`.
</aside>
# Activate subscription

`POST https://us-east1-bumdash-sandbox.cloudfunctions.net/Subscription`

<aside class="notice">
The URL is a standin for now
</aside>

>Requests require the following keys

```javascript
{
  "id":"cus_1234"
}
```

| Parameter | Type   | Description                    |
|-----------|--------|--------------------------------|
| id        | String | Stripe customer ID of customer |


## Response 

>Response looks like the following

```javascript
{
  "subscription_id":"sub_J2VCueNEWsAbKD"
}
```

| Parameter       | Type   | Description                                                                                          |
|-----------------|--------|------------------------------------------------------------------------------------------------------|
| subscription_id | String | Subscription ID from stripe of the parents subscription to the current price of the delivery service |

# Get parent's Subscription

`GET https://us-east1-bumdash-sandbox.cloudfunctions.net/Subscription`

<aside class="notice">
The URL is a standin for now
</aside>

>Requests would look like the below

```javascript

`https://us-east1-bumdash-sandbox.cloudfunctions.net/Subscription/?id=cus_1234`

```

| Parameter | Type   | Description                    |
|-----------|--------|--------------------------------|
| id        | String | Stripe customer ID of customer |


## Response 

>Response looks like the following

```javascript
{
  "subscription_ids":["sub_J2VCueNEWsAbKD"]
}
```

| Parameter        | Type         | Description                                                                                                                    |
|------------------|--------------|--------------------------------------------------------------------------------------------------------------------------------|
| subscription_ids | String Array | Array of subscription IDs assigned to the user. This should only ever be one but as it may be multiple, I'm returning them all |

# Get parent's Invoices

`GET https://us-east1-bumdash-sandbox.cloudfunctions.net/Invoices`

<aside class="notice">
The URL is a standin for now
</aside>

>Requests would look like the below

```javascript

`https://us-east1-bumdash-sandbox.cloudfunctions.net/Invoices?id=cus_1234`

```

| Parameter    | Type   | Required | Description                                                                                                                                |
|--------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------|
| id           | String | True     | Stripe customer ID of customer                                                                                                             |
| lastObjectID | String | False    | Last invoice ID of the list of invoices - including this means an attempt at getting further invoices beyond what was originally returned. |


## Response 

>Response looks like the following. If there are no invoices, rather than array, the value of "invoices" will be `null`

```javascript
{
  "invoices": [
    {
      "delivery_date": "2021-03-01T23:50:20-05:00",
      "amount_due": 2899,
      "amount_paid": 2899,
      "id": "in_1IQQBcF8Q3XD74KdEMLqRJl8",
      "status": "paid",
      "subscription_type": "Weekly Pickup and Delivery",
      "pdfLink": "https://pay.stripe.com/invoice/acct_1GC8FKF8Q3XD74Kd/invst_J2VCR4rHU9g4itf3UwTtZzMT8eZFe9s/pdf",
      "hostedLink": "https://invoice.stripe.com/i/acct_1GC8FKF8Q3XD74Kd/invst_J2VCR4rHU9g4itf3UwTtZzMT8eZFe9s"
    },
    {
      "delivery_date": "2021-03-01T23:19:46-05:00",
      "amount_due": 2899,
      "amount_paid": 2899,
      "id": "in_1IQPi3F8Q3XD74KdTwgx882o",
      "status": "paid",
      "subscription_type": "Weekly Pickup and Delivery",
      "pdfLink": "https://pay.stripe.com/invoice/acct_1GC8FKF8Q3XD74Kd/invst_J2UhQTFAXvE3rusjwHQNFwjxaV3DBzv/pdf",
      "hostedLink": "https://invoice.stripe.com/i/acct_1GC8FKF8Q3XD74Kd/invst_J2UhQTFAXvE3rusjwHQNFwjxaV3DBzv"
    },
  ]
}
```

| Parameter         | Type     | Description                                                                                                                                                |
|-------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| delivery_date     | ISO-8601 | This is the date of the delivery and when the customer is charged                                                                                          |
| amount_due        | Integer  | Amount due for the product that week. This is a whole number reflecting 10X the price to avoid using decimals. Divide by 10 before presenting to customer  |
| amount_paid       | Integer  | Amount paid for the product that week. This is a whole number reflecting 10X the price to avoid using decimals. Divide by 10 before presenting to customer |
| id                | String   | Stripe ID of the Invoice, used if pagination applies for the next page                                                                                     |
| status            | String   | Status of the invoice, can be: "draft", "open", "paid", "uncollectable", "void"                                                                            |
| subscription_type | String   | Product subscription that week, normally this will be either a 'weekly delivery' or 'paused delivery'                                                      |
| pdfLink           | String   | Stripe URL to download the PDF of the invoice                                                                                                              |
| hostedLink        | String   | Stripe URL to view the invoice, can be used to pay due invoices or view receipts                                                                           |