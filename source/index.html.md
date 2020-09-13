---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

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

| Parameter | Type   | Description                    |
| --------- | ------ | ------------------------------ |
| id        | String | Stripe customer ID of customer |



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








