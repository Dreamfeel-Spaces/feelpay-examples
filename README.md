# API Ref - feelpay

```config
This API is still in beta and is meant to change.
```

This is a straightforward JavaScript version of feelpay checkout. Its primary objective is to facilitate payment collection from websites and can seamlessly integrate into both web and mobile applications. To make use of this software, you must either register as a merchant or be furnished with test credentials for the purpose of conducting tests.

# Supported payment methods

1. Card (Visa, Mastercard),
2. Mobile (MPESA, Telkom, Airtel Money) and,
3. feelpay flexi (Buy now, Pay Later, and Save first, Buy Later) - Requires customer have feelpay  account
4. feelpay C2B - setup in dashboard
5. feelpay Wallet (coming soon)

# Merchant setup process

1. In step one of the feelpay merchant setup process, the merchant visits the Feelpay website and proceeds to sign up through the designated "Get started" action. Additionally, the merchant may also reach out to the support team to initiate the merchant setup procedure.

2. The support team requests the KYC information which includes the following details. Some document's will only be required when you request to "Go Live"

- National ID Details (Atleast two directors)
- KRA Pin Certificate
- Passport sized photos
- Certificate of Incorporation
- Company CR12

3. Once verified, the business, along with the support team, thoroughly reviews the details submitted by the merchant. Upon confirming the accuracy and completeness of the information, both parties proceed to sign the merchant agreement form. This formal agreement solidifies the partnership between the merchant and feelpay, outlining the terms and conditions for utilizing the payment services offered by the platform.

4. The support team requests the merchant credentials from their feelpay dashboard.

- For testing purposes, contact the support team who will set you up by providing you will create a new feelpay app at

1. Demo: [https://feelpay.vercel.app](https://feelpay.vercel.app)

2. Demo CDN: [http://feelpay.vercel.app/packages/v1](http://feelpay.vercel.app/packages/v1)

## Integrating the checkout

1. Include script tags to the bottom of your html document. Specify an element with id "dreamfeel-pay-button"

```html
<body>
  <div id="dreamfeel-pay-button"></div>
  <script src="http://feelpay.vercel.app/packages/v1"></script>
</body>
```

2. ## Preparing transaction details

You must keep your CLIENT_ID and CLIENT_SECRET hidden with .env variables, specific to your plaform.

```javascript
const orderDetails = {
  element: "dreamfeel-pay-button",
  clientId: "YOUR_CLIENT_ID",
  clientSecret: "YOUR_CLIENT_SECRET",
  description:"",
  order: {
    // Default for one time order checkout.
    installments: 1,
    orderCompleteAfterInstallment:1
    vat: 16, // percentage
    amount: 3000,
    currency:"KES",  //Only KES supported for now
    // Specify an array of order items.
    items: [
      {
        id: "1",
        name: "",
        price: 0,
        vat: 0,
        url: ``,
        image: "",
      },
    ],
  },
  onSuccess: (detail) => {
    // Handle success
    // const {feelPayCheckoutRequestID, feelPayCheckoutStatus, feelPayOrderId, ...} = detail
    console.log(detail);
  },
  onError: (err) => {
    // Handle error
    // {message:""}
    console.log(err);
  },
  // Run an action when innitialized!
  onInit: () => {},
  // Action when user cancels transaction!
  onUserCancel: () => {},
};
```

3. In another script tag, instantiate feelpay, and innitialize feelpay widget.

```html
<body>
  <script src="http://feelpay.vercel.app/packages/v1"></script>
  <script>
    const feelPay = new FeelPayWidget(orderDetails);
    const pay = await feelPay.init();
  </script>
</body>
```

4. A button will appear "Checkout with feelpay". When clicked, a popup appears, where user can complete transaction.

5. Complete code

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="dreamfeel-pay-button"></div>
    <script src="http://feelpay.vercel.app/packages/v1"></script>
    <script>
      const orderDetails = {
        element: "dreamfeel-pay-button",
        clientId: "YOUR_CLIENT_ID",
        clientSecret: "YOUR_CLIENT_SECRET",
        description: "",
        order: {
          // Default for one time order checkout.
          installments: 1,
          orderCompleteAfterInstallment: 1,
          vat: 16, // percentage
          amount: 3000,
          currency: "KES", //Only KES supported for now
          // Specify an array of order items.
          items: [
            {
              id: "1",
              name: "",
              price: 0,
              vat: 0,
              url: ``,
              image: "",
            },
          ],
        },
        onSuccess: (detail) => {
          // Handle success
          // const {feelPayCheckoutRequestID, feelPayCheckoutStatus, feelPayOrderId, ...} = detail
          console.log(detail);
        },
        onError: (err) => {
          // Handle error
          // {message:""}
          console.log(err);
        },
        // Run an action when innitialized!
        onInit: () => {},
        // Action when user cancels transaction!
        onUserCancel: () => {},
      };
      const feelPay = new FeelPayWidget(orderDetails);
      feelPay.init().then((pay) => {
        console.log(pay);
      });
    </script>
  </body>
</html>
```

### Guides coming for your favorite framework i.e Svelte, React, Angular Svelte
