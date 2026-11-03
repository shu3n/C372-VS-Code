
# Feature: Prepare payment details

## 1. User goal
A pet owner wants to review the selected pet service and the amount due before paying.

## 2. Scope
The feature returns payment details for one service as JSON.
It does NOT charge money, call a payment gateway, create new tables or add new pages.
No login is required for this classroom mock endpoint.

## 3. Request
GET /payments/prepare/:serviceId
Input: serviceId in the URL. The price comes from the server catalogue,
never from the client.

## 4. Service catalogue
| ID | Service name | Price |
|----|--------------|-------|
| 1  | Vaccination  | 35    |
| 2  | Pet Grooming | 50    |
| 3  | Boarding     | 80    |

## 5. Successful response
HTTP 200 with exactly five fields:
{ "serviceId": 1, "serviceName": "Vaccination", "amount": 35,
  "currency": "sgd", "status": "READY_FOR_PAYMENT" }
serviceId and amount are numbers. The other fields are strings.
currency is always "sgd" and status is always "READY_FOR_PAYMENT".

## 6. Unsuccessful response
If the service does not exist: HTTP 404 with {"error":"Service not found"}.

## 7. Acceptance criteria
- AC1: Service ID 1 returns 200, Vaccination, amount 35.
- AC2: Service ID 2 returns 200, Pet Grooming, amount 50.
- AC3: Service ID 3 returns 200, Boarding, amount 80.
- AC4: Service ID 999 returns 404 and {"error":"Service not found"}.
- AC5: Any successful response has exactly 5 fields with the correct types and fixed values.

## 8. Open questions
- What should happen for a malformed ID such as "abc"? (Not agreed yet.)


