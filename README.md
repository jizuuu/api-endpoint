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
  C -->|Update Status| D6["PUT /bookings/{id}/status"]
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
  D -->|Update Status| E5["PUT /payments/{id}/status"]
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
---
Users Flow:
---
### Authentication Flow
```mermaid
sequenceDiagram
    participant User
    participant System

    User->>System: POST /auth/register (Enter email, password, details)
    System-->>User: Registration Success/Failure (Account Created/Error Message)
    
    User->>System: POST /auth/login (Enter credentials)
    System-->>User: Authentication Success/Failure (Access Granted/Error)

    User->>System: POST /auth/logout (Click Logout)
    System-->>User: Logout Success (Session Ended)
```
---
### Booking Flow
```mermaid
sequenceDiagram
    participant User
    participant System

    %% Step 1: Check-in & Check-out Date Selection
    User->>System: GET /calendar (View available dates)
    System-->>User: Show calendar for selection

    User->>System: POST /bookings (Submit Check-in & Check-out Dates)
    System-->>User: Save Dates & Create Pending Booking ID

    %% Step 2: Select Package & Rate
    User->>System: GET /packages (View available packages)
    System-->>User: List of available packages

    User->>System: PUT /bookings/{id} (Select a package)
    System-->>User: Update booking with selected package

    %% Step 3: Guest Information
    User->>System: PUT /bookings/{id} (Enter personal details)
    System-->>User: Save guest information

    %% Step 4: Payment Processing
    User->>System: POST /payments (Submit GCASH Reference Code & Payment Terms)
    System-->>User: Link payment to booking & update status

    %% Step 5: Booking Confirmation
    User->>System: GET /bookings/{id} (Review booking details)
    System-->>User: Display booking summary with total amount

    User->>System: PUT /bookings/{id}/status (Accept terms & confirm booking)
    System-->>User: Booking finalized and status updated
```
---
### Packages Flow
```mermaid
sequenceDiagram
    participant User
    participant System

    User->>System: GET /packages (View available packages)
    System-->>User: List of all packages

    User->>System: GET /packages/{id} (View package details)
    System-->>User: Return package information
```
---
### Payment Flow
```mermaid
sequenceDiagram
    participant User
    participant System

    User->>System: GET /bookings/{id}/payments (Check Payment Status)
    System-->>User: Return Payment Details

    User->>System: POST /payments (Select Payment Method & Confirm)
    System-->>User: Payment Success/Failure Message

    User->>System: GET /payments/{id} (View Payment Receipt)
    System-->>User: Display Payment Details
```
---
### Billing Flow
```mermaid
sequenceDiagram
    participant User
    participant System

    User->>System: GET /billing (View all invoices)
    System-->>User: Return list of invoices

    User->>System: GET /billing/{id} (View specific invoice)
    System-->>User: Return invoice details
```
---
### Discount Flow
```mermaid
sequenceDiagram
    participant User
    participant System

    User->>System: GET /discounts (View Available Discounts)
    System-->>User: Display Discount List

    User->>System: POST /bookings (Apply Discount Code)
    System-->>User: Discount Applied or Invalid Code
```
---
### Access Control
| Entity              | Operation                               | Admin  | Staff  | Customer |
|---------------------|---------------------------------------|--------|--------|----------|
| **Users**          | Create (POST /auth/register)         | ✅     | ❌     | ✅ (Self) |
|                   | Read (GET /users/{id})               | ✅ (All) | ✅ (Own) | ✅ (Own) |
|                   | Update (PUT /users/{id})             | ✅ (All) | ✅ (Own) | ✅ (Own) |
|                   | Delete (DELETE /users/{id})          | ✅ (All) | ❌     | ❌       |
| **Content Management** | Create (POST /content)          | ✅     | ✅     | ❌       |
|                   | Read (GET /content)                  | ✅     | ✅     | ✅       |
|                   | Read (GET /content/{id})             | ✅     | ✅     | ✅       |
|                   | Update (PUT /content/{id})           | ✅     | ✅     | ❌       |
|                   | Delete (DELETE /content/{id})        | ✅     | ❌     | ❌       |
| **Roles**         | Create (POST /roles)                 | ✅     | ❌     | ❌       |
|                   | Read (GET /roles)                    | ✅     | ✅     | ❌       |
|                   | Update (PUT /roles/{id})             | ✅     | ❌     | ❌       |
|                   | Delete (DELETE /roles/{id})          | ✅     | ❌     | ❌       |
| **Bookings**      | Create (POST /bookings)              | ✅     | ✅     | ✅ (Own) |
|                   | Read (GET /bookings/{id})            | ✅ (All) | ✅ (Own) | ✅ (Own) |
|                   | Read (GET /bookings)                 | ✅     | ✅     | ❌       |
|                   | Update (PUT /bookings/{id})          | ✅     | ✅ (Own) | ❌       |
|                   | Delete (DELETE /bookings/{id})       | ✅     | ❌     | ❌       |
|                   | Update Status (PUT /bookings/{id}/status) | ✅ | ✅ | ❌ |
| **Payments**      | Create (POST /payments)              | ✅     | ✅     | ✅ (Own) |
|                   | Read (GET /payments/{id})            | ✅ (All) | ✅ (Own) | ✅ (Own) |
|                   | Read (GET /bookings/{id}/payments)   | ✅     | ✅     | ✅ (Own) |
|                   | Update (PUT /payments/{id})         | ✅     | ❌     | ❌       |
|                   | Update Status (PUT /payments/{id}/status) | ✅ | ✅ | ❌ |
|                   | Delete (DELETE /payments/{id})      | ✅     | ❌     | ❌       |
| **Billing**       | Create (POST /billing)              | ✅     | ✅     | ✅ (Own) |
|                   | Read (GET /billing)                 | ✅     | ✅     | ✅ (Own) |
|                   | Read (GET /billing/{id})           | ✅ (All) | ✅ (Own) | ✅ (Own) |
|                   | Update (PUT /billing/{id})         | ✅     | ✅     | ❌       |
| **Packages**      | Create (POST /packages)            | ✅     | ✅     | ❌       |
|                   | Read (GET /packages)               | ✅     | ✅     | ✅       |
|                   | Read (GET /packages/{id})          | ✅     | ✅     | ✅       |
|                   | Update (PUT /packages/{id})        | ✅     | ✅     | ❌       |
|                   | Delete (DELETE /packages/{id})     | ✅     | ❌     | ❌       |
| **Discounts**     | Create (POST /discounts)           | ✅     | ✅     | ❌       |
|                   | Read (GET /discounts)              | ✅     | ✅     | ✅       |
|                   | Update (PUT /discounts/{id})       | ✅     | ✅     | ❌       |
|                   | Delete (DELETE /discounts/{id})    | ✅     | ❌     | ❌       |
| **Reports**       | Create (POST /reports)             | ✅     | ✅     | ❌       |
|                   | Read (GET /reports)                | ✅     | ✅     | ❌       |
|                   | Read (GET /reports/{id})           | ✅     | ✅     | ❌       |

---
