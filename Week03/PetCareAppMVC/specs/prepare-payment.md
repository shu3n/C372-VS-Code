The method and URL are exactly GET /payments/prepare/:serviceId.
The price comes from the server’s catalogue, and the client never supplies it.
The response has exactly five fields: serviceId and amount are numbers, the other three are strings.
The 404 response is {"error":"Service not found"}.
Successful response:
HTTP 200 with exactly five fields:
{ "serviceId": 1, "serviceName": "Vaccination", "amount": 35,
  "currency": "sgd", "status": "READY_FOR_PAYMENT" }
serviceId and amount are JSON numbers (35, not "35.00").
serviceName, currency and status are strings.
currency is always "sgd". status is always "READY_FOR_PAYMENT".
No other fields are returned.
If the serviceId is not in the catalogue (anything other than 1, 2 or 3,
for example 999): HTTP 404 with {"error":"Service not found"}.
This is the only error response in scope.
- AC1: GET /payments/prepare/1   -> 200; Vaccination; amount 35
- AC2: GET /payments/prepare/2   -> 200; Pet Grooming; amount 50
- AC3: GET /payments/prepare/3   -> 200; Boarding; amount 80
- AC4: GET /payments/prepare/999 -> 404; {"error":"Service not found"}
- AC5: Any successful response has exactly the 5 named fields, with
       serviceId and amount as numbers, currency "sgd", status
       "READY_FOR_PAYMENT", and no extra fields.