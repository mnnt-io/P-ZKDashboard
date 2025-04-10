# Andrometa Dashboard API Documentation

This document outlines the API endpoints and interactions that are used by the Andrometa Dashboard.
We are currently updating these API endpoints as we finish integrating with the Skale blockchain.

## Base URL

All API requests were made to the following base URL:

```
https://api.andrometa.gg/v1
```

## Authentication

Most API endpoints require authentication using an API key:

1. Obtain an API key from the dashboard settings
2. Include the API key in the request header
3. API responses will include status codes and formatted data

## Endpoints

### User Endpoints

#### Get User Data

```
GET /user/data
```

Retrieves user data including token holdings and farm positions.

**Response:**

```json
{
	"status": "Success",
	"data": {
		"result": {
			"holdings": {
				"shrd": "25000"
			},
			"farm_positions": [
				{
					"id": "pos_12345",
					"staked": "15000",
					"rewards": "750"
				}
			]
		}
	}
}
```

### Token Endpoints

#### Get SHRD Token Price

```
GET /tokens/shrd/price
```

Retrieves current SHRD token price data.

**Response:**

```json
{
	"status": "Success",
	"result": {
		"symbol": "SHRD",
		"price": 0.003443,
		"currency": "USD",
		"change_24h": 2.5,
		"updated_at": "2023-05-15T14:30:45Z"
	}
}
```

#### Get SHRD Historical Price Data

```
GET /tokens/shrd/history
```

Retrieves historical price data with various query parameters.

**Query Parameters:**

-   `period`: Time period (1d, 7d, 30d, 90d, 1y, all)
-   `interval`: Data point interval (1m, 5m, 15m, 1h, 4h, 1d)

**Example Request:**

```
GET /tokens/shrd/history?period=7d&interval=1h
```

**Response:**

```json
{
	"status": "Success",
	"result": {
		"symbol": "SHRD",
		"currency": "USD",
		"interval": "1h",
		"data": [
			{
				"timestamp": 1652620800000,
				"price": 0.003415,
				"volume": 1250000
			},
			{
				"timestamp": 1652624400000,
				"price": 0.003422,
				"volume": 980000
			}
		]
	}
}
```

#### Get SHRD Distribution Data

```
GET /tokens/shrd/distribution
```

Retrieves token distribution data.

**Query Parameters:**

-   `period`: Time period (1d, 7d, 30d)

**Example Request:**

```
GET /tokens/shrd/distribution?period=7d
```

**Response:**

```json
{
	"status": "Success",
	"result": {
		"current_distribution": 3256994,
		"past_average": 522555,
		"current_average": 1676496,
		"distribution_by_day": [
			{
				"date": "2023-05-14",
				"amount": 4500000
			},
			{
				"date": "2023-05-15",
				"amount": 3800000
			}
		],
		"past_week": {
			"total": 28500000,
			"average": 4071428
		},
		"current_week": {
			"total": 31250000,
			"average": 4464285
		}
	}
}
```

### Farm Endpoints

#### Get Farm Positions

```
GET /farms/positions
```

Retrieves user's farm positions.

**Response:**

```json
{
	"status": "Success",
	"result": {
		"positions": [
			{
				"id": "shrd-staking",
				"name": "SHRD Staking",
				"staked": {
					"tokens": 15000,
					"value_usd": 51.645
				},
				"rewards": {
					"pending": 150,
					"claimed": 750,
					"token": "SHRD"
				},
				"apr": 12.5,
				"start_date": "2023-03-15T00:00:00Z"
			}
		]
	}
}
```

#### Stake Tokens

```
POST /farms/stake
```

Creates a new staking position.

**Request Body:**

```json
{
	"farm_id": "shrd-staking",
	"amount": "5000"
}
```

**Response:**

```json
{
	"status": "Success",
	"result": {
		"position_id": "pos_67890",
		"staked_amount": "5000",
		"timestamp": "2023-05-15T15:45:30Z"
	}
}
```

### Treasury Endpoints

#### Get Treasury Data

```
GET /treasury/data
```

Retrieves treasury information.

**Response:**

```json
{
	"status": "Success",
	"result": {
		"total_value_usd": 1250000,
		"assets": [
			{
				"token": "SHRD",
				"amount": 350000000,
				"value_usd": 1204050
			},
			{
				"token": "USDC",
				"amount": 45950,
				"value_usd": 45950
			}
		],
		"monthly_revenue": 45000,
		"monthly_expenses": 27500
	}
}
```

### Vesting Endpoints

#### Get Vesting Plans

```
GET /vesting/plans
```

Retrieves user's token vesting plans.

**Response:**

```json
{
	"status": "Success",
	"result": {
		"plans": [
			{
				"id": "vp_12345",
				"token": "SHRD",
				"total_amount": 100000,
				"claimed_amount": 25000,
				"remaining_amount": 75000,
				"start_date": "2023-01-01T00:00:00Z",
				"end_date": "2024-01-01T00:00:00Z",
				"next_release": {
					"date": "2023-06-01T00:00:00Z",
					"amount": 8333
				},
				"release_schedule": "monthly"
			}
		]
	}
}
```

#### Claim Vested Tokens

```
POST /vesting/claim
```

Simulates claiming vested tokens.

**Request Body:**

```json
{
	"plan_id": "vp_12345"
}
```

**Response:**

```json
{
	"status": "Success",
	"result": {
		"claimed_amount": 8333,
		"transaction_id": "txn_987654321",
		"remaining_amount": 66667,
		"next_release": {
			"date": "2023-07-01T00:00:00Z",
			"amount": 8333
		}
	}
}
```

## Error Handling

API errors are returned with a `Failure` status and an error message:

```json
{
	"status": "Failure",
	"error": {
		"message": "Error message describing the issue"
	}
}
```

Common error types:

-   Authentication errors
-   Invalid parameters
-   Resource not found
-   Permission errors
-   Server errors

## Note on Implementation

The current API implementation is off-chain, with plans to integrate with Skale blockchain in the future. All functionality currently simulates blockchain operations without actual on-chain transactions.
