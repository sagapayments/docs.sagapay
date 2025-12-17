# SagaPay API Documentation

**API Base URL:** `https://api.sagapay.no/api/v1`

Welcome to the SagaPay API documentation. This documentation covers all available API endpoints for integrating SagaPay payment solutions into your applications.

---

## Authentication

All API requests require authentication using an API key. Include your API key in the request header:

```
X-Api-Key: your_api_key
```

### API Key Types

| Type | Prefix | Description |
|------|--------|-------------|
| Live | `spay_live_` | Production API key for live transactions |
| Test | `spay_test_` | Sandbox API key for testing |

### Example Request

```bash
curl -X GET \
  -H 'Content-Type: application/json' \
  -H 'X-Api-Key: spay_live_xxxxxxxxxxxxx' \
  'https://api.sagapay.no/api/v1/merchants'
```

---

## API Documentation by Category

| # | API | Description | File |
|---|-----|-------------|------|
| 1 | [Orders API](./01-orders-api.md) | Create and manage payment orders | `01-orders-api.md` |
| 2 | [Payments API](./02-payments-api.md) | Initiate and process payments | `02-payments-api.md` |
| 3 | [Transactions API](./03-transactions-api.md) | Access transaction data | `03-transactions-api.md` |
| 4 | [Receipts API](./04-receipts-api.md) | Manage digital receipts | `04-receipts-api.md` |
| 5 | [Merchants API](./05-merchants-api.md) | Merchant account management | `05-merchants-api.md` |
| 6 | [Stores API](./06-stores-api.md) | Store location management | `06-stores-api.md` |
| 7 | [Terminals API](./07-terminals-api.md) | Terminal configuration | `07-terminals-api.md` |
| 8 | [Reporting API](./08-reporting-api.md) | Reports and analytics | `08-reporting-api.md` |

---

## Quick Reference - All Endpoints

### Orders API
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /orders | Create a new order |
| POST | /orders/:orderId | Update an existing order |
| GET | /orders/:orderId | Get order details |
| GET | /orders/:orderId/status | Get order status |
| DELETE | /orders/:orderId | Cancel an order |
| PUT | /orders/:orderId/receipt | Update order receipt |
| GET | /orders/:orderId/adjustments | Get order adjustments |
| GET | /orders/:orderId/tokens | Get order payment tokens |
| GET | /orders/:terminalId/online | Get online orders for terminal |

### Payments API
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /payments | Initiate a payment |
| POST | /payments/:paymentId/capture | Capture pre-authorized payment |
| GET | /payments/:paymentId/status | Get payment status |
| POST | /payments/:paymentId/void | Void a payment |

### Transactions API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /transactions | List transactions |
| GET | /transactions/:transactionId | Get transaction details |
| GET | /transactions/:transactionId/pdf | Download receipt PDF |

### Receipts API
| Method | Endpoint | Description |
|--------|----------|-------------|
| PUT | /orders/:orderId/receipt | Update receipt information |
| GET | /receipts/:receiptId | Get receipt details |
| POST | /receipts/:receiptId/send | Send receipt to customer |

### Merchants API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /merchants | Get merchant information |
| PUT | /merchants | Update merchant settings |
| GET | /merchants/payment-methods | Get enabled payment methods |

### Stores API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /stores | List all stores |
| POST | /stores | Create a new store |
| GET | /stores/:storeId | Get store details |
| PUT | /stores/:storeId | Update a store |
| DELETE | /stores/:storeId | Delete a store |
| GET | /stores/:storeId/terminals | List store terminals |

### Terminals API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /terminals | List all terminals |
| GET | /terminals/:terminalId | Get terminal details |
| PUT | /terminals/:terminalId | Update terminal settings |
| GET | /terminals/:terminalId/status | Get terminal status |
| POST | /terminals/:terminalId/reboot | Reboot terminal |

### Reporting API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /reports | Get reports summary |
| GET | /reports/transactions | Transaction report |
| GET | /reports/sales | Sales summary report |
| GET | /reports/settlements | Settlement report |
| GET | /reports/refunds | Refunds report |
| GET | /reports/export | Export report (CSV/PDF) |

---

## Payment Methods

| Method | Code | Description |
|--------|------|-------------|
| Card | `CARD` | Credit/debit card payments |
| Card Not Present | `CARD_NP` | Card refunds |
| Tokenized Card | `CTOKEN` | Saved card payments |
| Vipps | `SVIPPS` | Vipps mobile payments |
| Swish (Sweden) | `SSWISH` | Swish payments |
| Swish (Norway) | `NSWISH` | Swish payments |
| Klarna | `KLARNA` | Buy now, pay later |
| MobilePay | `SMOBILEPAY` | MobilePay payments |
| Gift Card | `GIFTCARD` | Gift card/voucher payments |

---

## Currencies

SagaPay supports the following currencies (ISO 4217):

| Code | Currency |
|------|----------|
| NOK | Norwegian Krone |
| SEK | Swedish Krona |
| DKK | Danish Krone |
| EUR | Euro |
| USD | US Dollar |
| GBP | British Pound |

---

## Response Format

All API responses follow a consistent format:

### Success Response

```json
{
  "status": "SUCCESS",
  "data": {
    // Response data
  },
  "message": "Operation completed successfully"
}
```

### Error Response

```json
{
  "error": "Error Type",
  "message": "Human-readable error message",
  "details": [
    "Specific error detail 1",
    "Specific error detail 2"
  ]
}
```

---

## HTTP Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Invalid API key |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource not found |
| 409 | Conflict - Resource state conflict |
| 422 | Unprocessable Entity - Validation failed |
| 429 | Too Many Requests - Rate limit exceeded |
| 500 | Internal Server Error |

---

## Rate Limits

| Tier | Requests/Minute | Requests/Hour |
|------|-----------------|---------------|
| Standard | 60 | 1000 |
| Enterprise | 300 | 10000 |

When rate limited, the API returns a `429` status code with `retryAfter` indicating seconds until the limit resets.

---

## Environments

| Environment | Base URL |
|-------------|----------|
| Production | `https://api.sagapay.no/api/v1` |
| Sandbox | `https://api.sagapay.no/api/v1` (use test API key) |

---

## Support

For technical support or questions about the SagaPay API:

- **Email:** support@sagapay.no
- **Documentation:** https://docs.sagapay.no
- **Dashboard:** https://dashboard.sagapay.no

---

© 2025 SagaPay. All rights reserved.
