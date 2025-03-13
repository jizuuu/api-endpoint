## API Endpoints
### Authentication API
```mermaid
graph LR;
  A[Authentication] -->|Register| A1["POST /auth/register"]
  A -->|Login| A2["POST /auth/login"]
  A -->|Logout| A3["POST /auth/logout"]
  A -->|Get User| A4["GET /users/{id}"]
```
---
### Content Management API
```mermaid
graph LR;
    B[Content Management] -->|GET| B1["GET /content"]
    B -->|GET| B2["GET /content/{id}"]
    B -->|POST| B3["POST /content"]
    B -->|PUT| B4["PUT /content/{id}"]
    B -->|DELETE| B5["DELETE /content/{id}"]
```
---
### Roles API
```mermaid
graph LR;
  B[Roles] -->|Get All Roles| C1["GET /roles"]
  B -->|Create Role| C2["POST /roles"]
  B -->|Update Role| C3["PUT /roles/{id}"]
  B -->|Delete Role| C4["DELETE /roles/{id}"]
```
---
### Booking API
```mermaid
graph LR;
  C[Booking] -->|Create Booking| D1["POST /bookings"]
  C -->|Get Booking by ID| D2["GET /bookings/{id}"]
  C -->|Get All Bookings| D3["GET /bookings"]
  C -->|Update Booking| D4["PUT /bookings/{id}"]
  C -->|Delete Booking| D5["DELETE /bookings/{id}"]
  C -->|Update Status| D6["PATCH /bookings/{id}/status"]
  C -->|Get Bookings by User| D7["GET /users/{id}/bookings"]
```
---
### Payment API
```mermaid
graph LR;
  D[Payment] -->|Create Payment| E1["POST /payments"]
  D -->|Get Payment by ID| E2["GET /payments/{id}"]
  D -->|Get Payments by Booking| E3["GET /bookings/{id}/payments"]
  D -->|Update Payment| E4["PUT /payments/{id}"]
  D -->|Update Status| E5["PATCH /payments/{id}/status"]
  D -->|Delete Payment| E6["DELETE /payments/{id}"]
```
---
### Billing API
```mermaid
graph LR;
  E[Billing] -->|Get All| F1["GET /billing"]
  E -->|Get by ID| F2["GET /billing/{id}"]
  E -->|Create Billing| F3["POST /billing"]
  E -->|Update Billing| F4["PUT /billing/{id}"]
```
---
### Packages API
```mermaid
graph LR;
  F[Packages] -->|Get All Packages| G1["GET /packages"]
  F -->|Get Package by ID| G2["GET /packages/{id}"]
  F -->|Create Package| G3["POST /packages"]
  F -->|Update Package| G4["PUT /packages/{id}"]
  F -->|Delete Package| G5["DELETE /packages/{id}"]
```
---
### Discounts API
```mermaid
graph LR;
  G[Discounts] -->|Get All Discounts| H1["GET /discounts"]
  G -->|Create Discount| H2["POST /discounts"]
  G -->|Update Discount| H3["PUT /discounts/{id}"]
  G -->|Delete Discount| H4["DELETE /discounts/{id}"]
```
---
### Reports API
```mermaid
graph LR;
  H[Reports] -->|Get All Reports| I1["GET /reports"]
  H -->|Generate Report| I2["POST /reports"]
  H -->|Get Report by ID| I3["GET /reports/{id}"]
```
