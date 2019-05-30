# Transaction-Type
#### officeId
office id is clane office office id, basically means that this transactions are coming from clane's headquarters

#### ClientId
This is the id of the client saved on Fineract - e.g: The client with an id of 1 is the one initiating all the transactions below

#### savingsId
Savings id is the id of the savings account. ones you have this service in your service, always pass it on the url {fineract_client_savings_account_id} whenever you need to carry out a transaction on that account.

#### resourceId
Resource id is the id assigned to each transactions or any operation on fineract. 

### Sample guide of how you can best create a clane wallet customer

- collect all the user KYC parameters as usuall.
basic body you can pass to fineract
```
body = {
	officeId: GET_FROM_ENV,
	externalId: random_id_optional,
	firstname: clane_user_first_name,
	lastname: clane_user_last_name,
	dateFormat: "dd MMMM yyyy",
	locale: "en", :active => true,
	activationDate: "04 March 2009",
	submittedOnDate: "04 March 2009",
	savingsProductId: GET_FROM_ENV
}
```
- this will create a cleint and a savings account for the customer at onces and then the response will look like so;
```
{
	"officeId": 1,
	"clientId": 1,
	"resourceId": 1,
	"savingsId": 10
}
```
Take the `clientId` and `savingsId` then store on your service along side other parameters. e.g `fineract_client_id` & `fineract_client_savings_fineract_client_savings_account_id`
- Note: it is advice the fineract process is complete before savings user KYC on your service


### Block Account
Block a certain amount of money. e.g: Block 5000 NGN
```
POST: /api/v1/savingsaccounts/{fineract_client_savings_account_id}/transactions?command=holdAmount
```
#### Request
```
{
	"transactionDate":"25 May 2019",
	"transactionAmount": 5000,
	"locale":"en",
	"dateFormat":"dd MMMM yyyy",
	"currency": 566
}
```
#### Response
```

{
	"officeId": 1,
	"clientId": 1,
	"savingsId": 3,
	"resourceId": 38,
	"block_amount": 5000,
	"block_authorization_id": "6ce86ebe-6287-4572-b525-bc600da108b4"
}
```

### Unblobk Account All(Reversal)
Unblock the complete 5000 NGN
```
POST /api/v1/savingsaccounts/{fineract_client_savings_account_id}/transactions/{resourceId}?command=releaseAmount
```
#### Request (optional)
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

### Debit Account (withdraw)
Debit 2000 NGN from customers account
```
POST: /api/v1/savingsaccounts/{fineract_client_savings_account_id}/transactions?command=withdrawal
```
#### Request
```
{
	"locale": "en",
	"dateFormat": "dd MMMM yyyy",
	"transactionDate": "27 May 2013",
	"transactionAmount": 2000,
}

```
#### Response
```
{
	"officeId": 1,
	"clientId": 2,
	"savingsId": 1,
	"resourceId": 48,
	"debited_amount": 2000
	"block_authorization_id": "816b04d5-bfe4-42cc-bdcd-d09c2c4490b3"
}
```

### Reverse Debit Transaction
Reverse 2000 NGN back to the customers account, it is a credit back to the customer's account
```
POST: /api/v1/savingsaccounts/{fineract_client_savings_account_id}/transactions/{resourceId}?command=undo
```
#### Request(optional)
```
{

}

```
#### Response
```
{
	"officeId": 1,
	"clientId": 2,
	"savingsId": 4,
	"resourceId": 33,
	"reversed_amount": 2000
}

```

### Debit Account From a Blocked Amount
In the case where the Blocked 5000 NGN was not completely unblocked, Debit 1000 from the Blocked 5000
```
POST: /api/v1/savingsaccounts/{fineract_client_savings_account_id}/transactions/{resourceId_of_blocked_amount}?command=debitAccountFromBlockedAmount
```
#### Request
```
{
	"locale":"en",
	"dateFormat":"dd MMMM yyyy",
	"debit_amount": 1000
}
```
#### Response
```
{
	"officeId": 1,
	"clientId": 2,
	"savingsId": 4,
	"resourceId": 34,
	"debit_amount": 1000
}
```















