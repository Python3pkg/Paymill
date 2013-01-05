Minimal python API client library for [Paymill](https://www.paymill.com/) API v2

Usage:
======

To create a recurring payment (subscription):
---------------------------------------------

How to setup a recurring payment with your customer for $10 a year.

```python

from paymill import core

PRIVATE_KEY = '<your paymill private key>'

# first we must get the token generated by the clientside js lib
# (see https://www.paymill.com/en-gb/documentation-3/reference/paymill-bridge/index.html)
token = request.get('paymillToken')

pm = core.Paymill(PRIVATE_KEY)

client = pm.create('client', {'email':'test@example.com', 'description':'sub test'})
offer = pm.create('offer', {'amount':1000, 'currency':'USD', 'interval':'year', 'name':'annual'})
payment = pm.create('payment', {'token':token, 'client':client['data']['id']})
sub = pm.create('subscription', {'client':client['data']['id'], 'offer':offer['data']['id'], 'payment':payment['data']['id']})

sub_id = sub['data']['id'])		
```

Simple!