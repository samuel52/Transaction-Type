# Transaction-Type

### Block Account
```
POST: /api/v1/savingsaccounts/{account_id}/transactions?command=holdAmount
```
#### Request
```
{
	"transactionDate":"25 May 2019",
	"transactionAmount": 2000,
	"locale":"en",
	"dateFormat":"dd MMMM yyyy",
	"account_number": "000000003",
	"currency": 599
}
```
#### Response
```

{
	"officeId": 1,
	"clientId": 1,
	"savingsId": 3,
	"resourceId": 38,
	"block_amount": 2000,
	"block_authorization_id": "6ce86ebe-6287-4572-b525-bc600da108b4"
}
```

### Unblobk Account(Reversal)
```
/api/v1/savingsaccounts/{account_id}/transactions/{resourceId}?command=releaseAmount
```
#### Request 
```
{
	"block_authorization_id": "6ce86ebe-6287-4572-b525-bc600da108b4"
}
```
#### Response
```
{
	"officeId": 1,
	"clientId": 1,
	"savingsId": 3,
	"resourceId": 41,
	"unblock_amount": 2000
}
```