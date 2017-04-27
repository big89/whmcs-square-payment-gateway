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

![Alt text](https://docs.connect.squareup.com/assets/docs/checkout-screen-01-479b0602ad0bc414846a8ed21e5c94dfcf9d65250e473f6be579da704f356be8.png "Checkout")

The payment confirmation page is only displayed if you opt not to redirect the customer to your own confirmation page:

![Alt text](https://docs.connect.squareup.com/assets/docs/checkout-screen-02-b3771631ee6be722997668b41d5cc302bebf6ed2949481548c329bf96435c505.png "Confirmation")

## Requirements

To use Square Checkout on your website, you must be using a hosting solution that allows you to create dynamic pages that support server side scripting (e.g., PHP, Ruby, ASP, Java). If your hosting solution only supports HTML, you cannot use Square Checkout at this time.

## Square Checkout in a nutshell

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

For integration with your WHMCS, Contact us : bhagwansahane89@gmail.com
