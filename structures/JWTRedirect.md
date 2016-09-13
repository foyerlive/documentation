# FoyerLive Redirect Management
The following outlines the current process for checking out via mobile or e-mail.

Please Note: The customer only interacts in the **bolded** sections highlighted below.  As far as they are aware, it is a 4 step process for a completed order.

## FoyerLive Text Message & E-Mail Based Checkout Process

- Customer
    - Enters store with FoyerLive Product Finder application
    - Selects & configures product(s)
    - **Enters their E-Mail address or Mobile phone number**
- Application
    - Sends cart data to FoyerLive Platform
- FoyerLive Platform
    - Stores cart details and delivers a Short URL to customer
- Application
    - Displays successfuly delivered message.
- **Customer**
    - **Visits delivered Short URL:** e.g. `http://foyer.to/khj34h`
- FoyerLive Platform
    - Confirms Short URL is valid
    - Loads cart data
    - Encodes cart data: `JWT::encode( <data>, <organisationSecret>, 'HS256' )`
    - Constructs `Long Redirect URL: http://yourecommerceplatform.com/instoreorder/<data>`
    - Returns a HTTP 302 Redirect to Long Redirect URL
- Customer
    - Redirected to `Long Redirect URL`
- E-Commerce Platform
    - Decodes and validates cart data: `JWT::decode( <data>, <organisationSecret>, 'H256' )`
    - Creates a local session & cart/order for the customer
    - Products from the decoded cart data are added to the local cart/order
        - If products are unavailable: Redirect to Cart page with unavailable products messaging
    - Cart is processed for promotions and can optionally have coupons applied (e.g. free shipping)
        - Optionally save the storeCode information with the order
    - Checkout process is initiated
    - If PayPal express is available: HTTP 302 Redirect to PayPal Express Checkout
- Customer
    - Redirected to `PayPal Express Checkout`
- PayPal
    - Validates order information and presents login screen with cart contents and total order value
- **Customer**
    - **Enters / Confirms login details with PayPal**
    - **Confirms payment & shipping information**
- PayPal
    - Validates the payment details and delivers a HTTP 302 Redirect back to E-Commerce Platform with confirmation information
- E-Commerce Platform
    - Validates PayPal order confirmation and retrieves shipping information
        - Optionally can present a final 'Confirm Order' page
    - Marks order as paid, delivers receipt via e-mail
    - Displays standard 'Order Successful' page
    - Pings FoyerLive Server for successful order
- Customer
    - Patiently waits for :package:
    
    
## Cart Data Example - Single Product
```json
{
    "organisationId": 1,
    "productData": {
        "sku": "541JON-BRN-8-MED"
    },
    "mode": "manual",
    "storeCode": "MELCENTRAL1-0100",
    "redirectCode": "5285E",
    "pingBackURI": "https://api.foyerlive.com/redirect/pingback/5285E"
}
```
    
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