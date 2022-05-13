## Cards

### Create customer
```go
data := map[string]interface{}{
    "name": "Gaurav Kumar",
    "contact": 9123456780,
    "email": "gaurav.kumar@example.com",
    "fail_existing": 0,
    "notes": map[string]interface{}{
        "notes_key_1": "Tea, Earl Grey, Hot",
        "notes_key_2": "Tea, Earl Grey… decaf.",
    },
}
body, err := client.Customer.Create(data, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| name*          | string      | Name of the customer                        |
| email        | string      | Email of the customer                       |
| contact      | string      | Contact number of the customer              |
| fail_existing | string | If a customer with the same details already exists, the request throws an exception by default. Possible value is `0` or `1`|
| notes         | object      | A key-value pair                            |

**Response:**
```json
{
  "id": "cust_1Aa00000000003",
  "entity": "customer",
  "name": "Gaurav Kumar",
  "email": "Gaurav.Kumar@example.com",
  "contact": "9000000000",
  "gstin": null,
  "notes": {
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "created_at": 1582033731
}
```
-------------------------------------------------------------------------------------------------------

### Create Order

```go
data := map[string]interface{}{
   "amount":100,
   "currency":"INR",
   "customer_id":"<customerId>",
   "method":"card",
   "token":map[string]interface{}{
      "max_amount":5000,
      "expire_at":2709971120,
      "frequency":"monthly",
   },
   "receipt":"Receipt No. 1",
   "notes":map[string]interface{}{
      "notes_key_1":"Tea, Earl Grey, Hot",
      "notes_key_2":"Tea, Earl Grey... decaf.",
   },
}
body, err := client.Order.Create(data, nil)
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| customerId*   | string      | The id of the customer to be fetched |
| receipt      | string  | Your system order reference id.  |
| method    | string  | Payment method used to make the registration transaction. Possible value is `card`.  |
| token  | object  | All keys listed [here](https://razorpay.com/docs/api/recurring-payments/cards/authorization-transaction/#112-create-an-order) are supported |
| notes | object  | A key-value pair  |

**Response:**
```json
{
   "id":"order_1Aa00000000002",
   "entity":"order",
   "amount":100,
   "amount_paid":0,
   "amount_due":100,
   "currency":"INR",
   "receipt":"Receipt No. 1",
   "method":"card",
   "description":null,
   "customer_id":"cust_4xbQrmEoA5WJ01",
   "token":{
      "max_amount":5000,
      "expire_at":2709971120,
      "frequency":"monthly"
   },
   "offer_id":null,
   "status":"created",
   "attempts":0,
   "notes":{
      "notes_key_1":"Tea, Earl Grey, Hot",
      "notes_key_2":"Tea, Earl Grey… decaf."
   },
   "created_at":1565172642
}
```
-------------------------------------------------------------------------------------------------------

### Create registration link

```go
data:= map[string]interface{}{
  "customer":map[string]interface{}{
    "name":"Gaurav Kumar",
    "email":"gaurav.kumar@example.com",
    "contact":"9123456780",
  },
  "type":"link",
  "amount":"100",
  "currency":"INR",
  "description":"Registration Link for Gaurav Kumar",
  "subscription_registration":map[string]interface{}{
    "method":"card",
    "max_amount":"500",
    "expire_at":1609423824,
  },
  "receipt":"Receipt No. 1",
  "email_notify":1,
  "sms_notify":1,
  "expire_by":1681987284,
  "notes":map[string]interface{}{
    "note_key 1":"Beam me up Scotty",
    "note_key 2":"Tea. Earl Gray. Hot.",
  },
}

body, err := client.Invoice.CreateRegistrationLink(data, nil)
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| customer   | object      | Details of the customer to whom the registration link will be sent. |
| type*  | string | the value is `link`. |
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| description*  | string      | A brief description of the payment.   |
| subscription_registration   | object  | All keys listed [here](https://razorpay.com/docs/api/recurring-payments/cards/authorization-transaction/#121-create-a-registration-link) are supported  |
| receipt      | string  | Your system order reference id.  |
| sms_notify  | boolean  | SMS notifications are to be sent by Razorpay (default : 1)  |
| email_notify | boolean  | Email notifications are to be sent by Razorpay (default : 1)  |
| expire_by    | integer | The timestamp, in Unix format, till when the customer can make the authorization payment. |
| notes | object  | A key-value pair  |

**Response:**
```json
{
  "id": "inv_FHrXGIpd3N17DX",
  "entity": "invoice",
  "receipt": "Receipt No. 24",
  "invoice_number": "Receipt No. 24",
  "customer_id": "cust_BMB3EwbqnqZ2EI",
  "customer_details": {
    "id": "cust_BMB3EwbqnqZ2EI",
    "name": "Gaurav Kumar",
    "email": "gaurav.kumar@example.com",
    "contact": "9123456780",
    "gstin": null,
    "billing_address": null,
    "shipping_address": null,
    "customer_name": "Gaurav Kumar",
    "customer_email": "gaurav.kumar@example.com",
    "customer_contact": "9123456780"
  },
  "order_id": "order_FHrXGJNngJyEAe",
  "line_items": [],
  "payment_id": null,
  "status": "issued",
  "expire_by": 4102444799,
  "issued_at": 1595491014,
  "paid_at": null,
  "cancelled_at": null,
  "expired_at": null,
  "sms_status": "pending",
  "email_status": "pending",
  "date": 1595491014,
  "terms": null,
  "partial_payment": false,
  "gross_amount": 100,
  "tax_amount": 0,
  "taxable_amount": 0,
  "amount": 100,
  "amount_paid": 0,
  "amount_due": 100,
  "currency": "INR",
  "currency_symbol": "₹",
  "description": "Registration Link for Gaurav Kumar",
  "notes": {
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot."
  },
  "comment": null,
  "short_url": "https://rzp.io/i/VSriCfn",
  "view_less": true,
  "billing_start": null,
  "billing_end": null,
  "type": "link",
  "group_taxes_discounts": false,
  "created_at": 1595491014,
  "idempotency_key": null
}
```
-------------------------------------------------------------------------------------------------------

## Create an order to charge the customer

```go
data:= map[string]interface{}{
   "amount":100,
   "currency":"INR",
   "customer_id":"<customerId>",
   "method":"card",
   "token":map[string]interface{}{
      "max_amount":5000,
      "expire_at":2709971120,
      "frequency":"monthly",
   },
   "receipt":"Receipt No. 1",
   "notes":map[string]interface{}{
      "notes_key_1":"Tea, Earl Grey, Hot",
      "notes_key_2":"Tea, Earl Grey... decaf.",
   },
}
body, err := client.Order.Create(data, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| customerId*   | string      | The id of the customer to be fetched |
| method      | string  | Payment method used to make the registration transaction. Possible value is `card`.  |
| receipt      | string  | Your system order reference id.  |
| token  | object  | All keys listed [here](https://razorpay.com/docs/api/recurring-payments/cards/subsequent-payments/#31-create-an-order-to-charge-the-customer) are supported |
| notes | object  | A key-value pair  |

**Response:**
```json
{
   "id":"order_1Aa00000000002",
   "entity":"order",
   "amount":100,
   "amount_paid":0,
   "amount_due":100,
   "currency":"INR",
   "receipt":"Receipt No. 1",
   "method":"card",
   "description":null,
   "customer_id":"cust_4xbQrmEoA5WJ01",
   "token":{
      "max_amount":5000,
      "expire_at":2709971120,
      "frequency":"monthly"
   },
   "offer_id":null,
   "status":"created",
   "attempts":0,
   "notes":{
      "notes_key_1":"Tea, Earl Grey, Hot",
      "notes_key_2":"Tea, Earl Grey… decaf."
   },
   "created_at":1565172642
}
```
-------------------------------------------------------------------------------------------------------

## Create a recurring payment

```go
data:= map[string]interface{}{
  "email": "gaurav.kumar@example.com",
  "contact": "9123456789",
  "amount": 1000,
  "currency": "INR",
  "order_id": "<orderId>",
  "customer_id": "<customerId>",
  "token": "<tokenId>",
  "recurring": "1",
  "description": "Creating recurring payment for Gaurav Kumar",
  "notes": map[string]interface{}{
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot.",
  },
}
body, err := Client.Payment.CreateRecurringPayment(data, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| email*   | string      | The customer's email address |
| contact*   | string      | The customer's phone number |
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| orderId*   | string      | The id of the order to be fetched |
| customerId*   | string      | The id of the customer to be fetched |
| tokenId*   | string      | The id of the token to be fetched |
| recurring*   | boolean      | Possible values is `0` or `1` |
| description  | string      | A brief description of the payment.   |
| notes | object  | A key-value pair  |

**Response:**
```json
{
  "razorpay_payment_id" : "pay_1Aa00000000001",
  "razorpay_order_id" : "order_1Aa00000000001",
  "razorpay_signature" : "9ef4dffbfd84f1318f6739a3ce19f9d85851857ae648f114332d8401e0949a3d"
}
```
-------------------------------------------------------------------------------------------------------

### Create an Authorization Payment

Please refer this [doc](https://razorpay.com/docs/api/recurring-payments/cards/authorization-transaction/#113-create-an-authorization-payment) for authorization payment

-------------------------------------------------------------------------------------------------------

## Send/Resend notifications

```go
body, err := client.Invoice.Notify("<invoiceId>", "<medium>", nil, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| invoiceId*   | string      | The id of the invoice to be fetched |
| medium*   | string      | Possible values are `sms` or `email` |

**Response:**
```json
{
    "success": true
}
```
-------------------------------------------------------------------------------------------------------

## Cancel registration link

```go
body, err := client.Invoice.Cancel("<invoiceId>", nil, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| invoiceId*   | string      | The id of the invoice to be fetched |

**Response:**
```json
{
    "id": "inv_FHrfRupD2ouKIt",
    "entity": "invoice",
    "receipt": "Receipt No. 1",
    "invoice_number": "Receipt No. 1",
    "customer_id": "cust_BMB3EwbqnqZ2EI",
    "customer_details": {
        "id": "cust_BMB3EwbqnqZ2EI",
        "name": "Gaurav Kumar",
        "email": "gaurav.kumar@example.com",
        "contact": "9123456780",
        "gstin": null,
        "billing_address": null,
        "shipping_address": null,
        "customer_name": "Gaurav Kumar",
        "customer_email": "gaurav.kumar@example.com",
        "customer_contact": "9123456780"
    },
    "order_id": "order_FHrfRw4TZU5Q2L",
    "line_items": [],
    "payment_id": null,
    "status": "cancelled",
    "expire_by": 4102444799,
    "issued_at": 1595491479,
    "paid_at": null,
    "cancelled_at": 1595491488,
    "expired_at": null,
    "sms_status": "sent",
    "email_status": "sent",
    "date": 1595491479,
    "terms": null,
    "partial_payment": false,
    "gross_amount": 100,
    "tax_amount": 0,
    "taxable_amount": 0,
    "amount": 100,
    "amount_paid": 0,
    "amount_due": 100,
    "currency": "INR",
    "currency_symbol": "₹",
    "description": "Registration Link for Gaurav Kumar",
    "notes": {
        "note_key 1": "Beam me up Scotty",
        "note_key 2": "Tea. Earl Gray. Hot."
    },
    "comment": null,
    "short_url": "https://rzp.io/i/QlfexTj",
    "view_less": true,
    "billing_start": null,
    "billing_end": null,
    "type": "link",
    "group_taxes_discounts": false,
    "created_at": 1595491480,
    "idempotency_key": null
}
```
-------------------------------------------------------------------------------------------------------

## Fetch token by payment id

```go
body, err := client.Payment.Fetch("<paymentId>", nil, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| paymentId*   | string      | The id of the payment to be fetched |

**Response:**
```json
{
  "id": "pay_FHfqtkRzWvxky4",
  "entity": "payment",
  "amount": 100,
  "currency": "INR",
  "status": "captured",
  "order_id": "order_FHfnswDdfu96HQ",
  "invoice_id": null,
  "international": false,
  "method": "card",
  "amount_refunded": 0,
  "refund_status": null,
  "captured": true,
  "description": null,
  "card_id": "card_F0zoXUp4IPPGoI",
  "bank": null,
  "wallet": null,
  "vpa": null,
  "email": "gaurav.kumar@example.com",
  "contact": "+919876543210",
  "customer_id": "cust_DtHaBuooGHTuyZ",
  "token_id": "token_FHfn3rIiM1Z8nr",
  "notes": {
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot."
  },
  "fee": 0,
  "tax": 0,
  "error_code": null,
  "error_description": null,
  "error_source": null,
  "error_step": null,
  "error_reason": null,
  "acquirer_data": {
    "auth_code": "541898"
  },
  "created_at": 1595449871
}
```
-------------------------------------------------------------------------------------------------------

## Fetch tokens by customer id

```go
body, err := client.Token.All("<customerId>", nil, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| customerId*   | string      | The id of the customer for whom tokens are to be retrieved |

**Response:**
```json
{
   "entity":"collection",
   "count":1,
   "items":[
      {
         "id":"token_HouA2OQR5Z2jTL",
         "entity":"token",
         "token":"2JPRk664pZHUWG",
         "bank":null,
         "wallet":null,
         "method":"card",
         "card":{
            "entity":"card",
            "name":"Gaurav Kumar",
            "last4":"8950",
            "network":"Visa",
            "type":"credit",
            "issuer":"STCB",
            "international":false,
            "emi":false,
            "sub_type":"consumer",
            "expiry_month":12,
            "expiry_year":2021,
            "flows":{
               "otp":true,
               "recurring":true
            }
         },
         "recurring":true,
         "recurring_details":{
            "status":"confirmed",
            "failure_reason":null
         },
         "auth_type":null,
         "mrn":null,
         "used_at":1629779657,
         "created_at":1629779657,
         "expired_at":1640975399,
         "dcc_enabled":false,
         "billing_address":null
      }
   ]
}
```
-------------------------------------------------------------------------------------------------------

### Fetch card

```go
body, err := client.Card.Fetch("<cardId>", nil, nil)
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| cardId*          | string | card id to be fetched                                               |

-------------------------------------------------------------------------------------------------------

## Delete tokens

```go
body, err := client.Token.Delete("<customerId>", "<tokenId>", nil, nil)
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| customerId*   | string      | The id of the customer with whom the token is linked |
| tokenId*   | string      | The id of the token to be deleted |

**Response:**
```json
{
    "deleted": true
}
```
-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/recurring-payments/cards/authorization-transaction/)**