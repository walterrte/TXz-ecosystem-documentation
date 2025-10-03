# API Documentation

## For Developers

**Base URL:** `https://txz-dev.fun/.netlify/functions/`

**Authentication:** JWT tokens (wallet signature-based)

## Available Endpoints

## Whitelist API

```bash
POST /whitelist-register
Content-Type: application/json

{
  "email": "user@example.com",
  "wallet_address": "ABC...XYZ",
  "twitter_handle": "@username",
  "discord_username": "user#1234",
  "solhunt_username": "player123",
  "referral_code": "TXZ-12345678-ABCD"
}

Response: 200 OK
{
  "success": true,
  "referral_code": "TXZ-87654321-DCBA",
  "tier": "Bronze",
  "points": 25
}
```

## Presale Contribution API

```bash
POST /presale-contribute
Content-Type: application/json
Authorization: Bearer <JWT_TOKEN>

{
  "wallet_address": "ABC...XYZ",
  "amount_usd": 100,
  "transaction_signature": "5Kn...xyz",
  "payment_method": "SOL",
  "referral_code": "TXZ-12345678-ABCD"
}

Response: 200 OK
{
  "success": true,
  "txz_amount": 50000,
  "contribution_id": "uuid-here"
}
```

## User Stats API

```bash
GET /user-stats?wallet=ABC...XYZ
Authorization: Bearer <JWT_TOKEN>

Response: 200 OK
{
  "wallet_address": "ABC...XYZ",
  "total_contributed": 500,
  "txz_allocated": 250000,
  "tier": "Gold",
  "points": 67,
  "referral_earnings": 1250,
  "referral_count": 5
}
```

## Presale Stats API

```bash
GET /presale-stats

Response: 200 OK
{
  "total_raised": 125000,
  "total_contributors": 847,
  "txz_sold": 62500000,
  "is_live": true,
  "time_remaining": 432000
}
```

## Rate Limits

| Endpoint | Limit |
|----------|-------|
| /whitelist-register | 100/min |
| /presale-contribute | 50/min |
| /user-auth | 100/min |
| /admin-auth | 20/min |
| Public endpoints | 200/min |

## Error Codes

```javascript
400 - Bad Request (validation failed)
401 - Unauthorized (invalid/missing JWT)
403 - Forbidden (insufficient permissions)
404 - Not Found
429 - Too Many Requests (rate limited)
500 - Internal Server Error
```

## Full API Documentation

[📖 View Complete API Docs](#) | [🔧 Postman Collection](#) | [💻 Code Examples](#)

---
