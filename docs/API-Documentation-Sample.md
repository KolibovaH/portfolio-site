---
id: api-docs
title: API Documentation Sample
sidebar_position: 1
---

# Stripe API Documentation

## Introduction
The Stripe API is a powerful and flexible RESTful interface that enables developers to integrate payment processing into websites and applications. Whether you're building a subscription service, an online store, or a marketplace, Stripe provides secure and scalable tools to manage transactions, customers, invoices, and more.

## How to Connect and Authenticate
To connect to the Stripe API, use the following base URL: `https://api.stripe.com` 

Stripe uses [API keys](https://docs.stripe.com/keys) to authenticate all API requests. To obtain your API key, you’ll first need to create an account in the [Stripe Dashboard](https://dashboard.stripe.com/).

Once registered, navigate to the [API keys section](https://dashboard.stripe.com/apikeys) of your dashboard to view and copy your **Secret key**. This key will be used to authorize your API requests.

Include the **Secret key** in the `Authorization` header as a **Bearer token** in every request.

**Example using `curl`:**
```
curl https://api.stripe.com/v1/customers \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -G
```
**Example using using the `Authorization` header explicitly:**
```
curl https://api.stripe.com/v1/customers \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -G
```
Both examples are valid. The `-u` format is shorthand for Basic Auth, and the colon (`:`) means an empty password.

**Test in the Right Environment**

- Test mode keys (`sk_test_...`) allow you to safely simulate API interactions.

- Live mode keys (`sk_live_...`) are used in production.

Stripe’s API base URL remains the same for both test and live environments; the mode is determined by the key you use.

## Request and Responses
The Stripe API is a RESTful interface that uses standard HTTP methods and JSON payloads for communication. Each interaction with the API involves sending an HTTP request and receiving a JSON-formatted response.

### Request Format
Stripe API requests follow a consistent structure:

- **Base URL:**
```
https://api.stripe.com
```

- **HTTP Methods Used:**

`GET` – Retrieve resources (e.g., a customer or charge)

`POST` – Create or modify resources

`DELETE` – Remove resources

- **Authentication:**

Use your secret key in the `Authorization` header:
```
Authorization: Bearer sk_test_YourSecretKey

```
- **Content Type:**

Stripe expects data to be sent as `application/x-www-form-urlencoded`.

**Example (Create a Customer):**

```
curl https://api.stripe.com/v1/customers \
  -u sk_test_YourSecretKey: \
  -d "email=customer@example.com" \
  -d "name=Jane Doe"
```
### Response Format
Stripe returns a **JSON object** for every request. A successful response will include a structured object representing the resource you interacted with.

- **Success Example (`201 Created`):**
```
{
  "id": "cus_1234567890",
  "object": "customer",
  "email": "customer@example.com",
  "name": "Jane Doe",
  ...
}
```
- **Error Example (`400 Bad Request`):**
```
{
  "error": {
    "type": "invalid_request_error",
    "message": "Missing required param: email.",
    "param": "email"
  }
}

```
**Idempotency**

For operations like charging a card, Stripe supports **idempotency keys** to prevent duplicate transactions if a request is retried. Add the key as a header:
```
Idempotency-Key: a_unique_key_generated_by_you
```

### Errors
|  Code    |          | Description |
|----------|----------|----------|
|   200      | OK | Success. |
|   400      | Bad Request | Unacceptable request, often due to missing a required parameter. |
|   401      | Unauthorized | No valid API key provided. |
|   402      | Request Failed | The parameters were valid but the request failed. |
|   403      | Forbidden | The API key doesn’t have permissions to perform the request. |
|   404      | Not Found | The requested resource doesn’t exist. |
|   409      | Conflict | The request conflicts with another request. |
|   429      | Too Many Requests | Too many requests hit the API too quickly. |
|   500, 502, 503, 504      | Server Errors | Something went wrong on Stripe’s end. |

## Functionalities

### Balance
You can use the Balance request to find out what is the balance on my credit card...

Operations available:

| Operation | Endpoint |Description|
|----------|----------|----------|
| `GET`    | `{{baseUrl}}/v1/balance`    | Reterieve a balance.|

The Balance Object
```
{
  "object": "balance",
  "available": [
    {
      "amount": 666670,
      "currency": "usd",
      "source_types": {
        "card": 666670
      }
    }
  ],
  "connect_reserved": [
    {
      "amount": 0,
      "currency": "usd"
    }
  ],
  "livemode": false,
  "pending": [
    {
      "amount": 61414,
      "currency": "usd",
      "source_types": {
        "card": 61414
      }
    }
  ]
}
```
#### Parameters (Attributes)

- **`available`**

**Value** - `array of objects`

**Description** - Available funds that you can transfer or pay out automatically by Stripe or explicitly through the [Transfers API](https://docs.stripe.com/api/balance/balance_object#transfers) or [Payouts API](https://docs.stripe.com/api/balance/balance_object#payouts). You can find the available balance for each currency and payment type in the source_types property.

Child Parameters:

| Key | Value | Description |
|----------|----------|----------|
| `available.amount`  | `integer` | Balance amount.   |
| `available.currency`| `enum`    | Three-letter [ISO currency code](https://www.iso.org/iso-4217-currency-codes.html), in lowercase. Must be a [supported currency](https://stripe.com/docs/currencies). |
| `available.source_types`  | `nullable object` | Breakdown of balance by source types. Funds coming from certain source / payment method types must be shown separately.   |

- **`livemode`**

**Value** - `boolean`

**Description** - `true` if in live mode, `false` if in test mode.

- **`pending`**

**Value** - `array of objects`

**Description** - Funds that aren’t available in the balance yet. You can find the pending balance for each currency and each payment type in the `source_types` property.

Child Parameters:

| Key | Value | Description |
|----------|----------|----------|
| `pending.amount`  | `integer` |  Balance amount.  |
| `pending.currency`| `enum`    | Three-letter [ISO currency code](https://www.iso.org/iso-4217-currency-codes.html), in lowercase. Must be a [supported currency](https://stripe.com/docs/currencies). |
| `pending.source_types`  | `pending.source_types` | Breakdown of balance by source types. Funds coming from certain source / payment method types must be shown separately.   |

### Customers
This object represents a customer of your business. Use it to create recurring charges, save payment and contact information, and track payments that belong to the same customer.

Operations available:

| Operation | Endpoint | Description |
|----------|----------|----------|
| `POST`    | `{{baseUrl}}/v1/customers`    | Create a customer.|
| `POST`    | `{{baseUrl}}/v1/customers/:id` | Update a customer. |
| `GET`     | `{{baseUrl}}/v1/customers`    | List all customers. |
| `GET`     | `{{baseUrl}}/v1/customers/:id`| Retrieve a customer. |
| `DELETE`  | `{{baseUrl}}/v1/customers/:id`| Delete a customer. |
| `GET`     | `{{baseUrl}}/v1/customers/search`| Search a customer.|

The Customers Object
```
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```
#### Parameters (Attributes)

- **`id`**

**Value** - `string`

**Description** - Unique identifier for the object.

- **`address`**

**Value** - `nullable object`

**Description** - The customer’s address.

Child Parameters:

| Key | Value | Description |
|----------|----------|----------|
| `address.city`  | `nullable string` | City, district, suburb, town, or village.   |
| `address.country`| `nullable string` | Two-letter country code ([ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)). |
| `address.line1`  | `nullable string` | Address line 1 (e.g., street, PO Box, or company name).  |
| `address.line2`  | `nullable string` | Address line 2 (e.g., apartment, suite, unit, or building). |
| `address.postal_code` | `nullable string` | ZIP or postal code. |
| `address.state` | `nullable string` | State, county, province, or region. |

- **`description`**

**Value** - `nullable string`

**Description** - An arbitrary string attached to the object. Often useful for displaying to users.

- **`email`**

**Value** - `nullable string`

**Description** - The customer’s email address.

- **`metadata`**

**Value** - `object`

**Description** - Set of key-value pairs that you can attach to an object. This can be useful for storing additional information about the object in a structured format.

- **`name`**

**Value** - `nullable string`

**Description** - The customer’s full name or business name.

- **`phone`**

**Value** - `nullable string`

**Description** - The customer’s phone number.

- **`shipping`**

**Value** - `nullable object`

**Description** - Mailing and shipping address for the customer. Appears on invoices emailed to this customer.

Child Parameters:

| Key | Value | Description |
|----------|----------|----------|
| `shipping.address`  | `object` | Customer shipping address.  |
| `shipping.name`| `string` | Customer name. |
| `shipping.phone`  | `nullable string` | Customer phone (including extension).  |

- **`tax`**

**Value** - `object`

**Description** - Tax details for the customer.

Child Parameters:

| Key | Value | Description |
|----------|----------|----------|
| `tax.automatic_tax`  | `enum` | Surfaces if automatic tax computation is possible given the current customer location information.  |
| `tax.ip_address`| `nullable string` | A recent IP address of the customer used for tax reporting and tax location inference. |
| `tax.location`  | `nullable object` | The identified tax location of the customer.  |



