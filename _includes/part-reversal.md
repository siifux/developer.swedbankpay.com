
### Part-reversal

As mentioned above, the `reversal transaction is used when a captured payment needs to be reversed.
A transaction can also be partly reversed, meaning you can reverse..
See the example below on how to do a part `reversal`.

{:.code-header}
**Request**

```http
POST /psp/{{ api resource }}/payments/{{ page.payment_id }}/reversals HTTP/1.1
Host: {{ page.api_host }}
Authorization: Bearer <AccessToken>
Content-Type: application/json
{
    "transaction": {
        "amount": 5000,
        "vatAmount": 0,
        "bonusAmount": 0,
        "payeeReference": "Reference1590150468",
        "description": "description for transaction",
        "orderItems": [
            {
                "reference": "P1",
                "name": "Product1",
                "type": "PRODUCT",
                "class": "ProductGroup1",
                "itemUrl": "https://example.com/products/123",
                "imageUrl": "https://example.com/product123.jpg",
                "description": "Product 1 description",
                "discountDescription": "Volume discount",
                "quantity": 2,
                "quantityUnit": "pcs",
                "unitPrice": 2500,
                "discountPrice": 0,
                "vatPercent": 0,
                "amount": 5000,
                "vatAmount": 0
            }
        ]
    }
}
```

{:.code-header}
**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json
{
    "payment": "/psp/{{ api resource }}/payments/{{ page.payment_id }}",
    "reversal": {
        "id": "/psp/{{ api resource }}/payments/{{ page.payment_id }}/reversals/{{ page.transaction_id }}",
        "transaction": {
            "id": "/psp/{{ api resource }}/payments/{{ page.payment_id }}/transactions/{{ page.transaction_id }}",
            "created": "2020-05-22T12:27:49.2383655Z",
            "updated": "2020-05-22T12:27:49.444977Z",
            "type": "Reversal",
            "state": "Completed",
            "number": 40101653482,
            "amount": 2500,
            "vatAmount": 0,
            "description": "description for transaction",
            "payeeReference": "someUniqueReference1590150468",
            "isOperational": false,
            "operations": []
        }
    }
}
```