# Shopier Api

## Info


This API is written by [Fatih Akdogan](https://github.com/0x178F) (0x178F), updated to the latest version by [Ruslan](https://github.com/frqher) (frqher).


## Usage:
```bash
npm install shopier-api
npm install api
```

#### Create an instance of the Shopier class.

```javascript
const sdk = require('api')('@shopier/v1.0#fg3hy496lgdue51p');
const Shopier = require('../shopier');

const shopier = new Shopier('apiKey', 'apiSecret')
```

#### Set the buyer's information.
```javascript
shopier.setBuyer({
  id: '010101',
  product_name: 'Balance',
  first_name: 'isim',
  last_name: 'soyisim',
  email: 'eposta@gmail.com',
  phone: '50XXXXXX'
})
```


#### Set buyer's billing address.
```javascript
shopier.setOrderBilling({
  billing_address: 'Abdurrahman Nafiz Gürman,Mh, G. Ali Rıza Gürcan Cd. No:27',
  billing_city: 'Istanbul',
  billing_country: 'Türkiye',
  billing_postcode: '34164'
})
```

#### Set buyer's shipping address.
```javascript
shopier.setOrderShipping({
  shipping_address: 'Abdurrahman Nafiz Gürman,Mh, G. Ali Rıza Gürcan Cd. No:27',
  shipping_city: 'Istanbul',
  shipping_country: 'Türkiye',
  shipping_postcode: '34164'
})
```

#### How much will the customer pay?
#### For 15₺:
```javascript
const paymentPage = shopier.payment(15)
```
> This will return the purchase form as html.



#### If we give an example for Express JS:
```javascript
app.get('/pay', (req, res) => {
    res.end(paymentPage)
})
```

> Now that we have render the html, a callback will be required after checkout.

```javascript
app.post('/shopier-notify', (req, res) => {
  sdk.auth("Your SHOPIER_BEARER");
        sdk.getOrdersId({id: req.body.payment_id})
        .then( async ({ data }) => {
            console.log("Payment has been made successfully")
        })
        .catch(err => {
            console.log(err);
        });
})
```

#### If payment was successful, it will return order_id, payment_id, installment.
```
{ order_id: 10592, payment_id: 413449826, installment: 0 }
```
