

```markdown
# AzamPay Payment Request Guide

## Introduction
This guide demonstrates how to make a payment request to AzamPay using the API. You will send a POST request with necessary payment details, including the account number, amount, currency, and more. This process involves authenticating your request with an access token and API key.

## Prerequisites
Before you begin, make sure you have the following:

- **Node.js** installed on your machine.
- **dotenv** and **node-fetch** libraries installed.
- A **valid API token** (bearer token) for authentication.
- A **valid API key** (X-API-Key) provided by AzamPay.
- Your **AzamPay credentials** (such as base URL, account details).

## Setting Up Your Project

### Step 1: Install Dependencies
First, install the required dependencies using npm:

```bash
npm install dotenv node-fetch
```

### Step 2: Create a `.env` File
Create a `.env` file in the root directory of your project to securely store sensitive credentials:

```env
TOKEN=your-authentication-token
API_KEY=your-api-key
BASE_URL=https://api.azampay.co.tz
```

- **TOKEN**: The bearer token for authentication.
- **API_KEY**: Your API key for accessing the AzamPay services.
- **BASE_URL**: The base URL for the AzamPay API (you can replace it with the production URL when you're ready).

Make sure to replace `your-authentication-token`, `your-api-key`, and `https://api.azampay.co.tz` with actual values provided by AzamPay.

### Step 3: Set Up Payment Request
Now, use the following JavaScript code to send a payment request to AzamPay.

```javascript
// Import required libraries
require('dotenv').config();
const fetch = require('node-fetch');

// Define the payment data object
const data = {
    'accountNumber': '0778611556',  // Recipient's phone number
    'amount': '2000',               // Payment amount
    'currency': 'TZS',              // Currency (Tanzanian Shillings)
    'externalId': 'aserswerxcvqwety',  // A unique external ID
    'provider': 'Tigo',             // Mobile network provider (e.g., Tigo, Vodacom, etc.)
    'additionalProperties': {
        'property1': null,          // Add any extra properties if needed
        'property2': null           // Add any extra properties if needed
    }
};

// Set up the headers for authentication and content type
const headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + process.env.TOKEN,  // Bearer token for authentication
    'X-API-Key': process.env.API_KEY               // API key for access
};

// Define the API endpoint URL
const url = `${process.env.BASE_URL}/azampay/mno/checkout`;

// Make the POST request to AzamPay's checkout endpoint
fetch(url, {
    method: 'POST',
    headers: headers,
    body: JSON.stringify(data) // Convert data object to JSON
})
.then(res => res.json()) // Parse the response as JSON
.then(responseData => {
    console.log('Response:', responseData); // Handle the response data here
})
.catch(err => {
    console.error('Error:', err); // Handle any errors
});
```

### Step 4: Run the Script
Execute the script to make the payment request:

```bash
node paymentRequest.js
```

### Sample Response
A successful response will look like this:

```json
{
    "status": "success",
    "message": "Payment processed successfully",
    "transactionId": "1234567890"
}
```

In case of an error, the response might look like:

```json
{
    "status": "error",
    "message": "Invalid account number or insufficient balance"
}
```

### Step 5: Error Handling
The `catch` block in the code handles any errors that may occur during the request, such as network failures or API errors. Ensure you check the console for any error messages.

## Additional Notes

- **Security**: Always keep your API credentials (e.g., `TOKEN` and `API_KEY`) secure. Do not expose them in public repositories.
- **Switch to Production**: Once you're ready for production, replace the sandbox URL with the production URL provided by AzamPay.

## Conclusion
By following this guide, you can integrate AzamPay payment functionality into your application. Use the generated token and API key for authentication and make payment requests through the AzamPay API.

For further support or more advanced use cases, consult the official AzamPay documentation or reach out to their support team.
```
