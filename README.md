# WHMCS Square Payment Gateway
Square Payment Gateway for WHMCS

With our e-commerce API, you can take payments with Square on your own website.

Square Checkout lets merchants accept online payments for supported payment types using a checkout workflow hosted on squareup.com that simplifies the process of accepting online payments by providing:

    Chargeback protection for qualifying transactions.
    Next business day deposits.
    PCI compliance.
    SSL support.

While SSL is not required to use Checkout, Square strongly recommends that merchant sites be SSL certified to reduce the risk of man-in-the-middle attacks.

## The Checkout UI

Square Checkout has two main screens: payment processing and payment confirmation.

The payment processing screen is where customers enter their credit card details and (optionally) confirm their shipping information:

![Alt text](https://docs.connect.squareup.com/assets/docs/checkout-screen-01-ed78eb4b8dc9074cae25f31b1a2d555735f64d99bbd2872ca664a7e29de3e077.png "Checkout")

The payment confirmation page is only displayed if you opt not to redirect the customer to your own confirmation page:

![Alt text](https://docs.connect.squareup.com/assets/docs/checkout-screen-02-de37e8f955599cb14f999d440ade31bc8f18dc8ba2ca15ca4ac8975e8477091c.png "Confirmation")

## Requirements

To use Square Checkout on your website, you must be using a hosting solution that allows you to create dynamic pages that support server side scripting (e.g., PHP, Ruby, ASP, Java). If your hosting solution only supports HTML, you cannot use Square Checkout at this time.

## How it works

Square Checkout is a RESTful web service and payment UI, hosted on Square’s servers, for collecting and processing payment information. To take payments with Checkout, merchant sites need to add code that sends order information to Square and (optionally) verifies the result.

In general, completing an order with Square Checkout involves the following steps:

    Merchant - Create a POST request:
        Package the order information as a JSON message. NOTE: Currently, Square Checkout cannot calculate shipping costs or taxes dynamically, those totals must be provided in the POST request as line items in the order.
        Add an authorization token to the header.
    Merchant - Send the generated POST request to Square Checkout and process the response:
        Save the returned checkout ID.
        Automatically redirect the customer to the returned Checkout page URL.
    Customer - Provide payment details using the Square Checkout UI.
    Square Checkout - Process the transaction and sends email confirmation to merchant and customer.
    Merchant - Verify the transaction results.

Which would look something like this:

![Alt text](https://docs.connect.squareup.com/assets/docs/example-square-checkout-flow-20e0619fde88b6d5345618928159e45d79907f69837be66b395d66599c513a40.png "Square Checkout")

Once payment processing completes, transaction and buyer details can be accessed via the Square Dashboard.

## Send the POST request to Square Checkout

The full Checkout URL for a given location ID is:

https://connect.squareup.com/v2/locations/{{LOCATION_ID}}/checkouts

When Checkout receives a merchant request at that URL it:

    Authenticates the authorization token.
    Authenticates the location ID.
    Verifies the location ID belongs to the merchant account indicated by the authorization token and the location is able to create payments and orders.
    Initializes a new transaction with the order information.
    Returns a new checkout ID and a checkout URL of the form

    https://connect.squareup.com/v2/checkout?c={{CHECKOUT_ID}}&l={{LOCATION_ID}}

When the merchant site receives the response it saves the checkout ID with the local order information then redirects the customer to the Square-hosted Checkout URL.

## Provide payment details using the Square Checkout UI

When the customer is redirected to Square Checkout, they are presented with a screen where they can review the order details as an itemized list and enter their payment information. If the original POST request included shipping information, those fields are pre-populated for the customer.

Data entry validation in the Checkout UI includes:

    Proper formatting for email address.
    Proper formatting for credit card number.
    Credit card expiration date not in the past.
    All required fields populated.

## Process the transaction

Once the payment card information is submitted, Square Checkout will try to authorize and capture payment. In the event of a recoverable error (e.g., the card is declined), the customer is prompted to correct their information.

Once payment is processed, Checkout sends two verification emails: one to the customer at the provided address and one to the merchant at the email address associated with their Square account. The transaction and buyer details can also be accessed through the Square Dashboard.

If the original POST request included a redirect URL, the customer is automatically sent to that URL, otherwise, they are presented with a Square Checkout confirmation page.

## Verify transaction results

Square strongly recommends setting a redirect URL and verifying transaction results to guard against order spoofing. Checkout will append the transaction ID, checkout ID, and store-generated order ID to the redirect URL to facilitate verification. In order to verify the transaction results, merchants should query Square’s Transaction endpoint for the transaction details and confirm the store-generated order ID, checkout ID, and transaction totals match the expected values. For more information on how to verify transaction results, please see the Square Checkout Setup guide. 


For integration with your WHMCS, Contact us : bhagwansahane89@gmail.com
