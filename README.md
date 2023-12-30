# Khalti Js package for easy khalti gateway implementation

## Usage

### Installation

```bash
    pnpm add khalti-js
```

### Initialization

```ts
// Set up Khalti with your credentials
const khalti = new Khalti({
  mode: "Sandbox", // or 'Production'
  secretKey: "your-secret-key",
  returnUrl: "https://your-website.com/return",
  websiteUrl: "https://your-website.com",
});
```

### Get Payment URL

```ts
const orderData = {
  amount: 10000, // Amount in paisa
  purchase_order_id: "123456789",
  purchase_order_name: "Order #123456",
  customer_info: {
    name: "John Doe",
    email: "john.doe@example.com",
    phone: "9801234567",
  },
  amount_breakdown: [
    { label: "Actual Price", amount: 9000 },
    { label: "VAT", amount: 1000 },
  ],
  product_details: [
    {
      identity: "product-1",
      name: "Product 1",
      total_price: 9000,
      quantity: 1,
      unit_price: 9000,
    },
  ],
};

const paymentUrl = khalti.getPaymentUrl(orderData);

console.log("Payment URL:", paymentUrl);

// Response example

// {
//     "pidx": "bZQLD9wRVWo4CdESSfuSsB",
//     "payment_url": "https://test-pay.khalti.com/?pidx=bZQLD9wRVWo4CdESSfuSsB",
//     "expires_at": "2023-05-25T16:26:16.471649+05:45",
//     "expires_in": 1800
// }
```

### Get Payment lookup

Basically get the details about the payment if it pending, paid and so on.

```ts
const paymentStatus = await khalti.getPaymentStatus("bZQLD9wRVWo4CdESSfuSsB");
console.log("Payment Status", paymentStatus);

// Response example

// {
//    "pidx": "HT6o6PEZRWFJ5ygavzHWd5",
//    "total_amount": 1000,
//    "status": "Completed",
//    "transaction_id": "GFq9PFS7b2iYvL8Lir9oXe",
//    "fee": 0,
//    "refunded": false
// }
```
