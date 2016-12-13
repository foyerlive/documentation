# FoyerLive POS Packet
The following outlines a process for sending order data to a POS platform.

Please Note: The customer only interacts in the **bolded** sections highlighted below.

## FoyerLive POS Checkout Process

- Customer
    - Enters store with FoyerLive Product Finder application
    - Selects & configures product(s)
    - **Optionally enters their E-Mail address or Mobile phone number**
- Application
    - Sends cart data to FoyerLive Platform
- FoyerLive Platform
    - Stores cart details and delivers a JWT encoded packer of the Order.
- 3rd Party POS
    - Returns a order ID.
- Application
    - Displays successfuly delivered message, along with the order id.
- FoyerLive Platform - Optionally
    - Delivers a order confirmation message via SMS or E-mail
- Customer
    - Visits checkout area and quotes order ID
    - Pays for order via existing POS
- 3rd Party POS
    - Pings FoyerLive Server for successful order along with the order ID.
    
## Cart Data Example - Multiple Products
```json
{
    "organisationId": 1,
    "productData": [
        {
            "sku": "541JON-BRN-8-MED",
            "qty": 1
        },
        {
            "sku": "266RAN-BLK-8-MED",
            "qty": 1
        }
    ],
    "mode": "paypal",
    "storeCode": "MELCENTRAL2-0100",
    "redirectCode": "5285E",
    "pingBackURI": "https://api.foyerlive.com/redirect/pingback/5285E"
}
```

## Store Code Parameter
The `storeCode` parameter is provided to allow the E-Commerce platform to keep track of orders arriving from a particular store & display device, and additionally a reference to an employee via a 4 digit number. Simply split the storeCode at the '-' to receive each part: i.e. `MELCENTRAL2-0100` References device `MELCENTRAL2` and the retail associate code `100`.

## Mode Parameter
The `mode` parameter is provided to find out if the device/user selected `paypal` as a checkout method, if so, attempt to automatically redirect the user, or `manual` - where the e-commerce platform should simply present the populated cart, ready to begin the checkout process.
