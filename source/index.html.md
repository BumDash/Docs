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
| --------- | ------ | ----------------------- |
| name      | String | Full name of parent     |
| email     | String | Email Address of parent |


## Response 

>Response looks like the following

```javascript
{
  "stripe_id":"cus_12345",
  "email":"john@gmail.com"
}
```

| Parameter | Type   | Description                                      |
| --------- | ------ | ------------------------------------------------ |
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
| --------- | ------ | -------------------------------------------------- |
| id        | String | Stripe customer ID of customer - from createParent |



## Response 

>Response looks like the following

```javascript
{
  "clientSecret":"1234"
}
```

| Parameter    | Type   | Description                                            |
| ------------ | ------ | ------------------------------------------------------ |
| clientSecret | String | secret to be associated for all future payment intents |

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
| --------- | ----- | ------------------------------------ |
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
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
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

| Parameter | Type   | Description                                        |
| --------- | ------ | -------------------------------------------------- |
| id        | String | Stripe customer ID of customer | 


## Response 

>Response looks like the following

```javascript
{
  "subscription_id":"sub_J2VCueNEWsAbKD"
}
```

| Parameter | Type   | Description                                                                                                                                               |
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| subscription_id     | String | Subscription ID from stripe of the parents subscription to the current price of the delivery service |

# Get parent's Subscription

`GET https://us-east1-bumdash-sandbox.cloudfunctions.net/Subscription`

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
| --------- | ------ | -------------------------------------------------- |
| id        | String | Stripe customer ID of customer | 


## Response 

>Response looks like the following

```javascript
{
  "subscription_ids":["sub_J2VCueNEWsAbKD"]
}
```

| Parameter | Type   | Description                                                                                                                                               |
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| subscription_ids     | String Array | Array of subscription IDs assigned to the user. This should only ever be one but as it may be multiple, I'm returning them all |