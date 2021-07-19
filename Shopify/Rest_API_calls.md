# Cancel order
```bash
curl -X POST \
-H 'X-Shopify-Access-Token: {{access_token}}' \
https://{{shop}}.myshopify.com/admin/api/2021-04/orders/{{order_id}}/cancel.json | json_pp
```

# Cancel fulfillment order
```bash
curl -X POST \
-H 'X-Shopify-Access-Token: {{access_token}}' \
https://{{shop}}.myshopify.com/admin/api/2021-04/fulfillment_orders/{{fulfillment_order_id}}/cancel.json | json_pp
```

# Get list of enabled webhooks
```bash
curl -X GET \
-H 'X-Shopify-Access-Token: {{access_token}}' \
https://{{shop}}.myshopify.com/admin/api/2021-07/webhooks.json | json_pp
```
# Mark order as high risk
```bash
curl --location -g --request POST \
'https://{{shop}}.myshopify.com/admin/api/2021-01/orders/{{order_id}}/risks.json' \
--header 'X-Shopify-Access-Token: {{access_token}}' \
--header "Content-Type: application/json" \
--data '{"risk":{"message": "high risk message", "recommendation": "cancel", "score": 1.0, "source": "External", "display": true}}'
```

