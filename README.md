# hapi-ccavenue
hapi-ccavenue is a ccavenue payment gateway integration for hapijs.

# Usage

```javascript
var ccavenue = require('hapi-ccavenue');

//required
ccavenue.setMerchant("Merchant Id");
ccavenue.setWorkingKey("Working Key");
ccavenue.setRedirectUrl("Redirect Url");

You can also send customer info (Optional).

For more detail 
https://world.ccavenue.com/downloads/CCAVenueWorldIntegrationManual.pdf


// Server url where you want to send data to ccavenue
server.route({
    method: 'GET',
    path: '/make-payment',
    handler: function(request, reply) {
        var param = {
            billing_cust_address: 'Bangalore',
            billing_cust_name: 'Nitish Kumar'
        }; //It would be better to receive these values from the request
        
        ccavenue.setOtherParams(param); //Set Customer Info
        ccavenue.setOrderAmount("<------Amount---->");
        ccavenue.setOrderId("<----------Order Id---------->"); //To be generated
        ccavenue.makePayment(reply);
    }

});

// Server url should be as redirect url (which you are passing as Redirect Url).
server.route({
    method: 'POST',
    path: '/redirect-link',
    handler: function(request, reply) {
        var data = ccavenue.paymentRedirect(request); //It will get response from ccavenue payment.

        if (data.isCheckSumValid == true && data.AuthDesc == 'Y') {
            // Success
            // Your code
        }
        else if (data.isCheckSumValid == true && data.AuthDesc == 'N') {
            // Unuccessful
            // Your code
        }
        else if(data.isCheckSumValid == true && data.AuthDesc == 'B') {
            // Batch processing mode
            // Your code
        }
        else {
            // Illegal access
            // Your code
        }
    }
});

For more detail 
https://world.ccavenue.com/downloads/CCAVenueWorldIntegrationManual.pdf

```
# Express Users
Express users can check this [link]() out by Nitesh Kumar Singh.

# CCAVenue Manual

  [CCAVenue World Integration Manual](https://world.ccavenue.com/downloads/CCAVenueWorldIntegrationManual.pdf)
    
# Installation

    $ npm install hapi-ccavenue
    
    
    
## License

The MIT License (MIT)
Copyright (c) 2017 Satnam Sandhu

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Bugs

See <https://github.com/satnam-sandhu/hapi-ccavenue/issues>.
    
