```markdown
# AzamPay Token Generation Guide

## Introduction
AzamPay is a payment platform that allows you to integrate payment functionalities into your application. This documentation will guide you through the process of generating an authentication token using AzamPay's API.

## Prerequisites
Before you begin, make sure you have the following:

- **Node.js** installed on your machine.
- **dotenv** and **node-fetch** libraries installed.
- Your **AzamPay credentials** (provided to you by AzamPay).

## Setting Up Your Project

### Step 1: Install Dependencies
First, install the required dependencies using npm:

```bash
npm install dotenv node-fetch
```

### Step 2: Create a `.env` File
Create a `.env` file in the root directory of your project. This file will securely store your AzamPay credentials:

```env
APP_NAME=your-app-name
CLIENT_ID=your-client-id
CLIENT_SECRET=your-client-secret
```

- **APP_NAME**: The name of your application.
- **CLIENT_ID**: Your unique client ID provided by AzamPay.
- **CLIENT_SECRET**: Your client secret provided by AzamPay.

Make sure to replace `your-app-name`, `your-client-id`, and `your-client-secret` with the actual credentials you received from AzamPay.

### Step 3: Set Up Token Generation Request
In your project, create a JavaScript file (e.g., `generateToken.js`) and use the following code to generate an authentication token.

```javascript
// Import required libraries
require('dotenv').config();
const fetch = require('node-fetch');

// Data object containing the credentials from the .env file
const data = {
    'appName': process.env.APP_NAME,
    'clientId': process.env.CLIENT_ID,
    'clientSecret': process.env.CLIENT_SECRET
};

// Make a POST request to AzamPay's GenerateToken endpoint
fetch('https://authenticator-sandbox.azampay.co.tz/AppRegistration/GenerateToken', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(data) // Convert data object to JSON
})
.then(res => res.json()) // Parse the response as JSON
.then(data => {
    console.log('Response:', data); // Handle the response data
})
.catch(err => {
    console.error('Error:', err); // Handle any errors
});
```

### Step 4: Run the Script
Execute the script to generate the authentication token by running the following command:

```bash
node generateToken.js
```

If the request is successful, you will see the response in your console with the generated token.

### Sample Response
A successful response will look like this:

```json
{
    "status": "success",
    "message": "Token generated successfully",
    "token": "your-generated-token-here"
}
```

### Step 5: Error Handling
In case of an error, the `catch` block will log the error. For example:

```json
{
    "status": "error",
    "message": "Invalid client ID or secret"
}
```

## Additional Notes

- **Security**: Always ensure your credentials (like client ID and secret) are stored securely. Do not expose them publicly, especially in public repositories.
- **Switch to Production**: Once you're ready to move to production, replace the sandbox URL with the production URL provided by AzamPay.

## Conclusion
After successfully generating the token, you can now use it for further AzamPay API integrations.

For more information or support, reach out to AzamPay or refer to the official documentation (if available).
```
