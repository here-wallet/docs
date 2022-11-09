# Push notifications

All decentralized partner apps can send push notifications to their users through the HERE app. To send a notification, just make a POST request.

```bash
curl -X 'POST' \
  'https://api.herewallet.app/api/v1/dapp/push_notification' \
  -H 'accept: application/json' \
  -H 'authorization: api_key' \
  -H 'Content-Type: application/json' \
  -d '{
  "near_account_id": "mydev.near",
  "message": "NEAR rate is $2.6 today, it'\''s a great time to buy"
}'
```

### ![](<../.gitbook/assets/IMG\_8D06E74B8AEC-1 (1).jpeg>)

### Restrictions

1. You can send no more than one notification per 12 hours
2. The user must have call your dapp's smart contract in the last 7 days
3. The text of the notification must be useful for the user, sending spam or unsubstantiated calls to action is prohibited

### APY KEY

To get the API key, send us an email or telegram. Include a link to the site and the address of the smart contract. Use corporate email.

t.me/heresupport

team@herewallet.app
