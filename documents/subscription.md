## Subscriptions

### Create subscription

```go
data := map[string]interface{}{
  "plan_id":"plan_JCPs6ZkAutbaCe",
  "total_count":3,
  "quantity": 1,
  "customer_notify":1,
  "start_at":1649491485,
  "expire_by":1683532925,
  "addons":[]interface{}{
    map[string]interface{}{
      "item":map[string]interface{}{
        "name":"Delivery charges",
        "amount":3000,
        "currency":"INR",
      },
    },
  },
  "notes":map[string]interface{}{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf.",
  },
}
body, err := client.Subscription.Create(data, nil)
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| plan_id*          | string | The unique identifier for a plan that should be linked to the subscription.|
| total_count*   | string | The number of billing cycles for which the customer should be charged  |
| customer_notify    | boolean | Indicates whether the communication to the customer would be handled by you or us |
| quantity    | integer | The number of times the customer should be charged the plan amount per invoice |
| start_at    | integer | The timestamp, in Unix format, for when the subscription should start. If not passed, the subscription starts immediately after the authorization payment. |
| expire_by    | integer | The timestamp, in Unix format, till when the customer can make the authorization payment. |
| addons    | object | Array that contains details of any upfront amount you want to collect as part of the authorization transaction. |
| notes          | object | Notes you can enter for the contact for future reference.   |

**Response:**
```json
{
  "id": "sub_00000000000001",
  "entity": "subscription",
  "plan_id": "plan_00000000000001",
  "status": "created",
  "current_start": null,
  "current_end": null,
  "ended_at": null,
  "quantity": 1,
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "charge_at": 1580453311,
  "start_at": 1580626111,
  "end_at": 1583433000,
  "auth_attempts": 0,
  "total_count": 6,
  "paid_count": 0,
  "customer_notify": true,
  "created_at": 1580280581,
  "expire_by": 1580626111,
  "short_url": "https://rzp.io/i/z3b1R61A9",
  "has_scheduled_changes": false,
  "change_scheduled_at": null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count": 5
}
```
-------------------------------------------------------------------------------------------------------

### Create subscription link

```go
data := map[string]interface{}{
  "plan_id": "plan_00000000000001",
  "total_count": 12,
  "quantity": 1,
  "start_at": 1561852800,
  "expire_by": 1561939199,
  "customer_notify": 1,
  "addons": []interface{}{
    map[string]interface{}{
    "item": map[string]interface{}{
      "name": "Delivery charges",
      "amount": 30000,
      "currency": "INR",
      },
    },
  },
  "offer_id":"offer_JHD834hjbxzhd38d",
  "notes": map[string]interface{}{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf.",
  },
  "notify_info":map[string]interface{}{
    "notify_phone": "9123456789",
    "notify_email": "gaurav.kumar@example.com",
  },
}
body, err := client.Subscription.Create(data, nil)
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| plan_id*          | string | The unique identifier for a plan that should be linked to the subscription.|
| total_count*   | string | The number of billing cycles for which the customer should be charged  |
| customer_notify    | boolean | Indicates whether the communication to the customer would be handled by you or us |
| quantity    | integer | The number of times the customer should be charged the plan amount per invoice |
| start_at    | integer | The timestamp, in Unix format, for when the subscription should start. If not passed, the subscription starts immediately after the authorization payment. |
| expire_by    | integer | The timestamp, in Unix format, till when the customer can make the authorization payment. |
| addons    | object | Array that contains details of any upfront amount you want to collect as part of the authorization transaction. |
| notes          | object | Notes you can enter for the contact for future reference.   |
| notify_info          | object | The customer's email and phone number to which notifications are to be sent. (PN: Use this array only if you have set the `customer_notify` parameter to 1. That is, Razorpay sends notifications to the customer.)  |

**Response:**
```json
{
  "id":"sub_00000000000002",
  "entity":"subscription",
  "plan_id":"plan_00000000000001",
  "status":"created",
  "current_start":null,
  "current_end":null,
  "ended_at":null,
  "quantity":1,
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "charge_at":1580453311,
  "start_at":1580453311,
  "end_at":1587061800,
  "auth_attempts":0,
  "total_count":12,
  "paid_count":0,
  "customer_notify":true,
  "created_at":1580283117,
  "expire_by":1581013800,
  "short_url":"https://rzp.io/i/m0y0f",
  "has_scheduled_changes":false,
  "change_scheduled_at":null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count":12
}
```
-------------------------------------------------------------------------------------------------------

### Fetch all subscriptions

```go
options := map[string]interface{}{
    "count": 1,
}
body, err := client.Subscription.All(options, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| from  | timestamp | timestamp after which the payments were created  |
| to    | timestamp | timestamp before which the payments were created |
| count | integer   | number of payments to fetch (default: 10)        |
| skip  | integer   | number of payments to be skipped (default: 0)    |
| plan_id  | string   | The unique identifier of the plan for which you want to retrieve all the subscriptions    |

**Response:**
```json

{
  "entity": "collection",
  "count": 1,
  "items": [
    {
      "id": "sub_00000000000001",
      "entity": "subscription",
      "plan_id": "plan_00000000000001",
      "customer_id": "cust_D00000000000001",
      "status": "active",
      "current_start": 1577355871,
      "current_end": 1582655400,
      "ended_at": null,
      "quantity": 1,
      "notes": {
        "notes_key_1": "Tea, Earl Grey, Hot",
        "notes_key_2": "Tea, Earl Grey… decaf."
      },
      "charge_at": 1577385991,
      "offer_id": "offer_JHD834hjbxzhd38d",
      "start_at": 1577385991,
      "end_at": 1603737000,
      "auth_attempts": 0,
      "total_count": 6,
      "paid_count": 1,
      "customer_notify": true,
      "created_at": 1577356081,
      "expire_by": 1577485991,
      "short_url": "https://rzp.io/i/z3b1R61A9",
      "has_scheduled_changes": false,
      "change_scheduled_at": null,
      "remaining_count": 5
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

### Fetch particular subscription

```go
body, err := client.Subscription.Fetch("<subscriptionId>", nil, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to be fetched  |

**Response:**
```json
{
  "id": "sub_00000000000001",
  "entity": "subscription",
  "plan_id": "plan_00000000000001",
  "customer_id": "cust_D00000000000001",
  "status": "active",
  "current_start": 1577355871,
  "current_end": 1582655400,
  "ended_at": null,
  "quantity": 1,
  "notes":{
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "charge_at": 1577385991,
  "start_at": 1577385991,
  "end_at": 1603737000,
  "auth_attempts": 0,
  "total_count": 6,
  "paid_count": 1,
  "customer_notify": true,
  "created_at": 1577356081,
  "expire_by": 1577485991,
  "short_url": "https://rzp.io/i/z3b1R61A9",
  "has_scheduled_changes": false,
  "change_scheduled_at": null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count": 5
}
```

-------------------------------------------------------------------------------------------------------

### Cancel particular subscription

```go
data := map[string]interface{}{
  "cancel_at_cycle_end": 1,
}
body, err := client.Subscription.Cancel("<subscriptionId>", data, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to be cancelled  |
| cancel_at_cycle_end  | boolean | Possible values:<br>0 (default): Cancel the subscription immediately. <br> 1: Cancel the subscription at the end of the current billing cycle.  |

**Response:**
```json
{
  "id": "sub_00000000000001",
  "entity": "subscription",
  "plan_id": "plan_00000000000001",
  "customer_id": "cust_D00000000000001",
  "status": "cancelled",
  "current_start": 1580453311,
  "current_end": 1581013800,
  "ended_at": 1580288092,
  "quantity": 1,
  "notes":{
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "charge_at": 1580453311,
  "start_at": 1577385991,
  "end_at": 1603737000,
  "auth_attempts": 0,
  "total_count": 6,
  "paid_count": 1,
  "customer_notify": true,
  "created_at": 1580283117,
  "expire_by": 1581013800,
  "short_url": "https://rzp.io/i/z3b1R61A9",
  "has_scheduled_changes": false,
  "change_scheduled_at": null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count": 5
}
```
-------------------------------------------------------------------------------------------------------

### Update particular subscription

```go
body, err := client.Subscription.Update("<subscriptionId>", options, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to be updated  |
| options  | object | All parameters listed [here](https://razorpay.com/docs/api/subscriptions/#update-a-subscription) for update   |

**Response:**
```json
{
  "id":"sub_00000000000002",
  "entity":"subscription",
  "plan_id":"plan_00000000000002",
  "customer_id":"cust_00000000000002",
  "status":"authenticated",
  "current_start":null,
  "current_end":null,
  "ended_at":null,
  "quantity":3,
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "charge_at":1580453311,
  "start_at":1580453311,
  "end_at":1606588200,
  "auth_attempts":0,
  "total_count":6,
  "paid_count":0,
  "customer_notify":true,
  "created_at":1580283807,
  "expire_by":1580626111,
  "short_url":"https://rzp.io/i/yeDkUKy",
  "has_scheduled_changes":false,
  "change_scheduled_at":null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count":6
}
```

-------------------------------------------------------------------------------------------------------

### Fetch details of pending update

```go
body, err := client.Subscription.PendingUpdate("<subscriptionId>", nil, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to fetch pending update  |

**Response:**
```json
{
  "id":"sub_00000000000001",
  "entity":"subscription",
  "plan_id":"plan_00000000000003",
  "customer_id":"cust_00000000000001",
  "status":"active",
  "current_start":1580284732,
  "current_end":1580841000,
  "ended_at":null,
  "quantity":25,
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "charge_at":1580841000,
  "start_at":1580284732,
  "end_at":1611081000,
  "auth_attempts":0,
  "total_count":6,
  "paid_count":1,
  "customer_notify":true,
  "created_at":1580284702,
  "expire_by":1580626111,
  "short_url":"https://rzp.io/i/fFWTkbf",
  "has_scheduled_changes":true,
  "change_scheduled_at":1557253800,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count":5
}
```
-------------------------------------------------------------------------------------------------------

### Cancel a update

```go
body, err := client.Subscription.CancelScheduledChanges("<subscriptionId>", nil, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to be cancel an update  |

**Response:**
```json
{
  "id": "sub_00000000000001",
  "entity": "subscription",
  "plan_id": "plan_00000000000003",
  "customer_id": "cust_00000000000001",
  "status": "active",
  "current_start": 1580284732,
  "current_end": 1580841000,
  "ended_at": null,
  "quantity": 1,
  "notes": {
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "charge_at": 1580841000,
  "start_at": 1580284732,
  "end_at": 1611081000,
  "auth_attempts": 0,
  "total_count": 6,
  "paid_count": 1,
  "customer_notify": true,
  "created_at": 1580284702,
  "expire_by": 1580626111,
  "short_url": "https://rzp.io/i/fFWTkbf",
  "has_scheduled_changes": false,
  "change_scheduled_at": 1527858600,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count": 5
}
```
-------------------------------------------------------------------------------------------------------

### Pause a subscription

```go
options := map[string]interface{}{ "pause_at" : "now" }
body, err := client.Subscription.Pause("<subscriptionId>", options, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to be paused  |
| pause_at  | string | To pause the subscription, possible values: `now`  |

**Response:**
```json
{
  "id": "sub_00000000000001",
  "entity": "subscription",
  "plan_id": "plan_00000000000001",
  "status": "paused",
  "current_start": null,
  "current_end": null,
  "ended_at": null,
  "quantity": 1,
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "charge_at": null,
  "start_at": 1580626111,
  "end_at": 1583433000,
  "auth_attempts": 0,
  "total_count": 6,
  "paid_count": 0,
  "customer_notify": true,
  "created_at": 1580280581,
  "paused_at": 1590280581,
  "expire_by": 1580626111,
  "pause_initiated_by": "self",
  "short_url": "https://rzp.io/i/z3b1R61A9",
  "has_scheduled_changes": false,
  "change_scheduled_at": null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count": 6
}
```
-------------------------------------------------------------------------------------------------------

### Resume a subscription

```go
options := map[string]interface{}{ "resume_at" : "now" }
body, err := client.Subscription.Resume("<subscriptionId>", options, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to be resumed  |
| resume_at  | string | To resume the subscription, possible values: `now`  |

**Response:**
```json
{
  "id": "sub_00000000000001",
  "entity": "subscription",
  "plan_id": "plan_00000000000001",
  "status": "active",
  "current_start": null,
  "current_end": null,
  "ended_at": null,
  "quantity": 1,
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "charge_at": 1580453311,
  "start_at": 1580626111,
  "end_at": 1583433000,
  "auth_attempts": 0,
  "total_count": 6,
  "paid_count": 0,
  "customer_notify": true,
  "created_at": 1580280581,
  "paused_at": 1590280581,
  "expire_by": 1580626111,
  "pause_initiated_by": null,
  "short_url": "https://rzp.io/i/z3b1R61A9",
  "has_scheduled_changes": false,
  "change_scheduled_at": null,
  "source": "api",
  "offer_id":"offer_JHD834hjbxzhd38d",
  "remaining_count": 6
}
```
-------------------------------------------------------------------------------------------------------

### Fetch all invoices for a subscription

```go
data:= map[string]interface{}{ "subscription_id": "sub_00000000000001" }
body, err := client.Invoice.All(data, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to fetch invoices  |

**Response:**
```json
{
  "entity": "collection",
  "count": 1,
  "items": [
    {
      "id": "inv_00000000000003",
      "entity": "invoice",
      "receipt": null,
      "invoice_number": null,
      "customer_id": "cust_00000000000001",
      "customer_details": {
        "id": "cust_00000000000001",
        "name": null,
        "email": "gaurav.kumar@example.com",
        "contact": "+919876543210",
        "gstin": null,
        "billing_address": null,
        "shipping_address": null,
        "customer_name": null,
        "customer_email": "gaurav.kumar@example.com",
        "customer_contact": "+919876543210"
      },
      "order_id": "order_00000000000002",
      "subscription_id": "sub_00000000000001",
      "line_items": [
        {
          "id": "li_00000000000003",
          "item_id": null,
          "ref_id": null,
          "ref_type": null,
          "name": "Monthly Plan",
          "description": null,
          "amount": 99900,
          "unit_amount": 99900,
          "gross_amount": 99900,
          "tax_amount": 0,
          "taxable_amount": 99900,
          "net_amount": 99900,
          "currency": "INR",
          "type": "plan",
          "tax_inclusive": false,
          "hsn_code": null,
          "sac_code": null,
          "tax_rate": null,
          "unit": null,
          "quantity": 1,
          "taxes": []
        }
      ],
      "payment_id": "pay_00000000000002",
      "status": "paid",
      "expire_by": null,
      "issued_at": 1593344888,
      "paid_at": 1593344889,
      "cancelled_at": null,
      "expired_at": null,
      "sms_status": null,
      "email_status": null,
      "date": 1593344888,
      "terms": null,
      "partial_payment": false,
      "gross_amount": 99900,
      "tax_amount": 0,
      "taxable_amount": 99900,
      "amount": 99900,
      "amount_paid": 99900,
      "amount_due": 0,
      "currency": "INR",
      "currency_symbol": "₹",
      "description": null,
      "notes": [],
      "comment": null,
      "short_url": "https://rzp.io/i/Ys4feGqEp",
      "view_less": true,
      "billing_start": 1594405800,
      "billing_end": 1597084200,
      "type": "invoice",
      "group_taxes_discounts": false,
      "created_at": 1593344888,
      "idempotency_key": null
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

### Delete offer linked to a subscription

```go
body, err := client.Subscription.DeleteOffer("<subscriptionId>", "<offerId>", nil, nil)
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| subscriptionId*  | string | The id of the subscription to offer need to be deleted  |
| offerId*  | string | The id of the offer linked to subscription  |

**Response:**
```json
{
    "id": "sub_I3GGEs7Xgmnozy",
    "entity": "subscription",
    "plan_id": "plan_HuXrfsI0ZZ3peu",
    "customer_id": "cust_I3FToKbnExwDLu",
    "status": "active",
    "current_start": 1632914901,
    "current_end": 1635445800,
    "ended_at": null,
    "quantity": 1,
    "notes": [],
    "charge_at": 1635445800,
    "start_at": 1632914901,
    "end_at": 1645986600,
    "auth_attempts": 0,
    "total_count": 6,
    "paid_count": 1,
    "customer_notify": true,
    "created_at": 1632914246,
    "expire_by": 1635532200,
    "short_url": "https://rzp.io/i/SOvRWaYP81",
    "has_scheduled_changes": false,
    "change_scheduled_at": null,
    "source": "dashboard",
    "payment_method": "card",
    "offer_id": null,
    "remaining_count": 5
}
```
-------------------------------------------------------------------------------------------------------

### Authentication Transaction

Please refer this [doc](https://razorpay.com/docs/api/subscriptions/#authentication-transaction) for authentication of transaction

-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/subscriptions/#subscriptions)**