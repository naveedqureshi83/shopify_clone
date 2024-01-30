* TEST CASES OF API *

### Creates a customer

````markdown
# Test Case: Create a Customer

## Description

Send a POST request to the API endpoint to create a new customer.

### Endpoint

`/admin/api/2024-01/customers.json`

### Method

POST

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Request Body

````json
{
  "customer": {
    "first_name": "Steve",
    "last_name": "Lastnameson",
    "email": "vencab@gmail.com",
    "phone": "+15142546123",
    "verified_email": true,
    "addresses": [
      {
        "address1": "123 Oak St",
        "city": "Ottawa",
        "province": "ON",
        "phone": "555-1212",
        "zip": "123 ABC",
        "last_name": "Lastnameson",
        "first_name": "Mother",
        "country": "CA"
      }
    ],
    "send_email_invite": true
  }
}

## Verification Steps

1. **Verify Successful Customer Creation**

    - **Verify HTTP Response Status Code:**
        - Expected: 201 Created
        - The API should successfully create the customer.

    - **Verify the Creation of the Customer:**
        - Send a separate request to retrieve the customer details.

2. **Negative Test - Existing Email**

    - Send a POST request with an email that already exists in the system.

    - **Verify HTTP Response Status Code:**
        - Expected: 422 Unprocessable Entity
        - The API should return a 422 Unprocessable Entity status code.

3. **Negative Test - Missing Required Fields**

    - Send a POST request with missing required fields (e.g., missing email).

    - **Verify HTTP Response Status Code:**
        - Expected: 400 Bad Request
        - The API should return a 400 Bad Request status code.

4. **Negative Test - Unauthorized Access**

    - Send a POST request without valid authentication credentials.

    - **Verify HTTP Response Status Code:**
        - Expected: 401 Unauthorized
        - The API should return a 401 Unauthorized status code.

5. **Negative Test - Invalid Endpoint**

    - Send a POST request to an invalid endpoint.

    - **Verify HTTP Response Status Code:**
        - Expected: 404 Not Found
        - The API should return a 404 Not Found status code.

### Creates an account activation URL for a customer

Send a POST request to the API endpoint to create an account activation URL for a customer:

### Endpoint
`{{baseUrl}}/admin/api/2024-01/customers/7816234008860/account_activation_url.json`

### Method
POST

### Headers
- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Request Body
```json
{
  // Include any necessary parameters for creating the account activation URL.
}

1. **Successful Activation URL Creation:**
   - **Request:** Send a valid request to the API endpoint with the necessary parameters.
   - **Expected Response:**
     - Status Code: 200
     - Body:
       ```json
       {
         "account_activation_url": "https://42e469-3.myshopify.com/account/activate/7816234008860/0399e4bd0cbe8be00c2a546d2305665e-1706610410"
       }
       ```

2. **Invalid Customer ID:**
   - **Request:** Send a request with an invalid or non-existent customer ID.
   - **Expected Response:**
     - Status Code: 404
     - Body:
       ```json
       {
         "error": "Customer not found"
       }
       ```

3. **Missing Required Parameters:**
   - **Request:** Send a request with missing or incomplete parameters.
   - **Expected Response:**
     - Status Code: 400
     - Body:
       ```json
       {
         "error": "Missing required parameters"
       }
       ```

4. **Unauthorized Access:**
   - **Request:** Send a request without proper authentication or authorization.
   - **Expected Response:**
     - Status Code: 401
     - Body:
       ```json
       {
         "error": "Unauthorized access"
       }
       ```

5. **Expired Activation URL:**
   - **Scenario:** Attempt to use an activation URL after it has expired.
   - **Expected Response:**
     - Status Code: 403
     - Body:
       ```json
       {
         "error": "Activation URL has expired"
       }
       ```

6. **Duplicate Activation URL Request:**
   - **Scenario:** Attempt to request an activation URL for a customer who already has an active URL.
   - **Expected Response:**
     - Status Code: 409
     - Body:
       ```json
       {
         "error": "Activation URL already exists for the customer"
       }
       ```

### Sends an account invite to a customer

```markdown
# Test Case: Send Customer Invite

## Description

Send a POST request to the API endpoint to send an invitation to a customer.

### Endpoint

`{{baseUrl}}/admin/api/2024-01/customers/7815925235996/send_invite.json`

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Method

POST

### Request Body

```json
{
  "customer_invite": {
    "to": "new_test_email@shopify.com",
    "from": "j.limited@example.com",
    "subject": "Welcome to my new shop",
    "custom_message": "My awesome new store",
    "bcc": ["j.limited@example.com"]
  }
}
````
````

## Verification Steps

1. **Verify Successful Customer Invite**

   - **Verify HTTP Response Status Code:**

     - Expected: 201 Created
     - The API should successfully send the customer invite.

   - **Verify Response Body:**
     - Expected:
       ```json
       {
         "customer_invite": {
           "to": "new_test_email@shopify.com",
           "from": "j.limited@example.com",
           "subject": "Welcome to my new shop",
           "custom_message": "My awesome new store",
           "bcc": ["j.limited@example.com"]
         }
       }
       ```
       The API should return the details of the sent customer invite.

2. **Negative Test - Invalid Customer ID**

   - Send a POST request to an invalid customer ID endpoint.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

3. **Negative Test - Missing Required Fields**

   - Send a POST request with missing required fields.

   - **Verify HTTP Response Status Code:**
     - Expected: 400 Bad Request
     - The API should return a 400 Bad Request status code.

4. **Negative Test - Unauthorized Access**

   - Send a POST request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

5. **Negative Test - Duplicate Invitation**

   - Send a second POST request to send an invitation to the same customer.

   - **Verify HTTP Response Status Code:**
     - Expected: 409 Conflict
     - The API should return a 409 Conflict status code, indicating that an invitation has already been sent to the customer.

````

### Retrieves a list of customers

Certainly! Here's a sample API test case for the given cURL command:

```markdown
# API Test Case: Retrieve Customer Information

## Description

Send a GET request to the API endpoint to retrieve information about specific customers.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Expected Response

```json
{
  "customers": [
    {
      "id": 7812466770204,
      "created_at": "2024-01-30T09:50:41+05:30",
      "updated_at": "2024-01-30T14:48:26+05:30",
      "orders_count": 0,
      "state": "enabled",
      "total_spent": "0.00",
      "last_order_id": null,
      "note": null,
      "verified_email": true,
      "multipass_identifier": null,
      "tax_exempt": false,
      "tags": "",
      "last_order_name": null,
      "currency": "INR",
      "addresses": [
        {
          "id": 9817368330524,
          "customer_id": 7812466770204,
          "company": null,
          "province": "Ontario",
          "country": "Canada",
          "province_code": "ON",
          "country_code": "CA",
          "country_name": "Canada",
          "default": true
        }
      ],
      "tax_exemptions": [],
      "email_marketing_consent": {
        "state": "not_subscribed",
        "opt_in_level": "single_opt_in",
        "consent_updated_at": null
      },
      "sms_marketing_consent": {
        "state": "not_subscribed",
        "opt_in_level": "single_opt_in",
        "consent_updated_at": null,
        "consent_collected_from": "OTHER"
      },
      "admin_graphql_api_id": "gid://shopify/Customer/7812466770204",
      "default_address": {
        "id": 9817368330524,
        "customer_id": 7812466770204,
        "company": null,
        "province": "Ontario",
        "country": "Canada",
        "province_code": "ON",
        "country_code": "CA",
        "country_name": "Canada",
        "default": true
      }
    }
  ]
}
```

## Verification Steps

1. **Verify Successful Customer Retrieval**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully retrieve customer information.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Invalid Customer IDs**

   - Send a GET request with invalid or non-existent customer IDs.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

````

### Retrieves a single customer

```markdown
# API Test Case: Retrieve Customer by ID

## Description

Send a GET request to the API endpoint to retrieve information about a specific customer using their ID.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]
````

### Expected Response

```json
{
  "customer": {
    "id": 7812466770204,
    "created_at": "2024-01-30T09:50:41+05:30",
    "updated_at": "2024-01-30T09:50:41+05:30",
    "orders_count": 0,
    "state": "enabled",
    "total_spent": "0.00",
    "last_order_id": null,
    "note": null,
    "verified_email": true,
    "multipass_identifier": null,
    "tax_exempt": false,
    "tags": "",
    "last_order_name": null,
    "currency": "INR",
    "addresses": [
      {
        "id": 9817368330524,
        "customer_id": 7812466770204,
        "company": null,
        "province": "Ontario",
        "country": "Canada",
        "province_code": "ON",
        "country_code": "CA",
        "country_name": "Canada",
        "default": true
      }
    ],
    "tax_exemptions": [],
    "email_marketing_consent": {
      "state": "not_subscribed",
      "opt_in_level": "single_opt_in",
      "consent_updated_at": null
    },
    "sms_marketing_consent": {
      "state": "not_subscribed",
      "opt_in_level": "single_opt_in",
      "consent_updated_at": null,
      "consent_collected_from": "OTHER"
    },
    "admin_graphql_api_id": "gid://shopify/Customer/7812466770204",
    "default_address": {
      "id": 9817368330524,
      "customer_id": 7812466770204,
      "company": null,
      "province": "Ontario",
      "country": "Canada",
      "province_code": "ON",
      "country_code": "CA",
      "country_name": "Canada",
      "default": true
    }
  }
}
```

## Verification Steps

1. **Verify Successful Customer Retrieval by ID**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully retrieve customer information using the specified ID.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Non-Existent Customer ID**

   - Send a GET request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

````

### Retrieves all orders that belong to a customer


```markdown
# API Test Case: Retrieve Orders for a Customer

## Description

Send a GET request to the API endpoint to retrieve all orders that belong to a specific customer.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]
### Expected Response

```json
{
  "orders": []
}
```

## Verification Steps

1. **Verify Successful Order Retrieval for a Customer**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully retrieve all orders for the specified customer.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Non-Existent Customer ID**

   - Send a GET request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

4. **Negative Test - No Orders for Customer**

   - Verify the behavior when the customer has no orders.

   - **Verify HTTP Response Status Code:**
     - Expected: 200 OK
     - The API should return an empty list of orders.

````

### Retrieves a count of customers


Certainly! Here's a sample API test case for the given cURL command:

```markdown
# API Test Case: Retrieve Customer Count

## Description

Send a GET request to the API endpoint to retrieve the count of customers.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Expected Response

```json
{
  "count": 2
}
```

## Verification Steps

1. **Verify Successful Customer Count Retrieval**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully retrieve the count of customers.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Invalid Endpoint**

   - Send a GET request to an invalid or non-existent endpoint for customer count.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

4. **Negative Test - Invalid Access Token**

   - Send a GET request with an invalid or expired access token.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

5. **Negative Test - Empty Customer Count**

   - Verify the behavior when there are no customers.

   - **Verify HTTP Response Status Code:**
     - Expected: 200 OK
     - The API should return a count of 0.

````

### Searches for customers that match a supplied query

Certainly! Here's a sample API test case for the given cURL command:

```markdown
# API Test Case: Search for Customers

## Description

Send a GET request to the API endpoint to search for customers that match a supplied query.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]
### Expected Response

```json
{
  "customers": []
}
```

## Verification Steps

1. **Verify Successful Customer Search**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully search for customers based on the provided query.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Invalid Query Parameters**

   - Send a GET request with an invalid or missing query parameter.

   - **Verify HTTP Response Status Code:**
     - Expected: 400 Bad Request
     - The API should return a 400 Bad Request status code.

4. **Negative Test - Invalid Access Token**

   - Send a GET request with an invalid or expired access token.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

5. **Negative Test - No Matching Customers**

   - Verify the behavior when there are no customers matching the provided query.

   - **Verify HTTP Response Status Code:**
     - Expected: 200 OK
     - The API should return an empty array in the "customers" field.

````

### Updates a customer

Certainly! Below is a sample API test case for the given cURL command:

```markdown
# API Test Case: Update Customer Information

## Description

Send a PUT request to the API endpoint to update customer information.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Expected Response

```json
{
  "customer": {
    "id": 7812466770204,
    "created_at": "2024-01-30T09:50:41+05:30",
    "updated_at": "2024-01-30T09:50:41+05:30",
    "orders_count": 0,
    "state": "enabled",
    "total_spent": "0.00",
    "last_order_id": null,
    "note": null,
    "verified_email": true,
    "multipass_identifier": null,
    "tax_exempt": false,
    "tags": "",
    "last_order_name": null,
    "currency": "INR",
    "addresses": [
      {
        "id": 9817368330524,
        "customer_id": 7812466770204,
        "company": null,
        "province": "Ontario",
        "country": "Canada",
        "province_code": "ON",
        "country_code": "CA",
        "country_name": "Canada",
        "default": true
      }
    ],
    "tax_exemptions": [],
    "email_marketing_consent": {
      "state": "not_subscribed",
      "opt_in_level": "single_opt_in",
      "consent_updated_at": null
    },
    "sms_marketing_consent": {
      "state": "not_subscribed",
      "opt_in_level": "single_opt_in",
      "consent_updated_at": null,
      "consent_collected_from": "OTHER"
    },
    "admin_graphql_api_id": "gid://shopify/Customer/7812466770204",
    "default_address": {
      "id": 9817368330524,
      "customer_id": 7812466770204,
      "company": null,
      "province": "Ontario",
      "country": "Canada",
      "province_code": "ON",
      "country_code": "CA",
      "country_name": "Canada",
      "default": true
    }
  }
}
```

## Verification Steps

1. **Verify Successful Customer Update**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully update the customer information.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Negative Test - Unauthorized Access**

   - Send a PUT request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Invalid Customer ID**

   - Send a PUT request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

4. **Negative Test - Missing Metafield Key**

   - Send a PUT request with missing metafield key.

   - **Verify HTTP Response Status Code:**
     - Expected: 400 Bad Request
     - The API should return a 400 Bad Request status code.

5. **Negative Test - Invalid Content Type Header**

   - Send a PUT request with an invalid Content-Type header.

   - **Verify HTTP Response Status Code:**
     - Expected: 415 Unsupported Media Type
     - The API should return a 415 Unsupported Media Type status code.

````

### Deletes a customer

Certainly! Below is a sample API test case for the given cURL command:

```markdown
# API Test Case: Delete Customer

## Description

Send a DELETE request to the API endpoint to delete a customer.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]
### Expected Response

```json
{}
```

## Verification Steps

1. **Verify Successful Customer Deletion**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK or 204 No Content
     - The API should successfully delete the customer.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected empty response `{}`.

2. **Negative Test - Unauthorized Access**

   - Send a DELETE request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

3. **Negative Test - Invalid Customer ID**

   - Send a DELETE request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

4. **Negative Test - Attempt to Delete Non-Existent Customer**

   - Verify the behavior when trying to delete a customer that does not exist.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

5. **Negative Test - Missing Access Token**

   - Send a DELETE request without providing the X-Shopify-Access-Token header.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

````

### Creates a new address for a customer


```markdown
# API Test Case: Create New Address for a Customer

## Description

Send a POST request to the API endpoint to create a new address for a customer.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]
### Expected Response

```json
{
  "customer_address": {
    "id": 9820781314332,
    "customer_id": 7816234008860,
    "company": "Fancy Co.",
    "province": "Quebec",
    "country": "Canada",
    "province_code": "QC",
    "country_code": "CA",
    "country_name": "Canada",
    "default": false
  }
}
```

## Verification Steps

1. **Verify Successful Address Creation**

   - **Verify HTTP Response Status Code:**

     - Expected: 201 Created
     - The API should successfully create a new address for the customer.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Verify Default Address Status**

   - **Verify the "default" field in the response:**
     - Expected: false
     - Ensure that the newly created address is not set as the default address for the customer.

3. **Negative Test - Unauthorized Access**

   - Send a POST request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

4. **Negative Test - Invalid Customer ID**

   - Send a POST request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

5. **Negative Test - Missing Required Fields**

   - Send a POST request with missing required fields (e.g., missing first name) and ensure that the API returns an appropriate error response.

   - **Verify HTTP Response Status Code:**
     - Expected: 422 Unprocessable Entity
     - The API should return a 422 Unprocessable Entity status code.

6. **Negative Test - Invalid Content-Type Header**

   - Send a POST request with an invalid Content-Type header.

   - **Verify HTTP Response Status Code:**
     - Expected: 415 Unsupported Media Type
     - The API should return a 415 Unsupported Media Type status code.

````

### Retrieves a list of addresses for a customer

```markdown
# API Test Case: Retrieve Addresses for a Customer

## Description

Send a GET request to the API endpoint to retrieve a list of addresses for a customer.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Expected Response

```json
{
  "addresses": [
    {
      "id": 9817368330524,
      "customer_id": 7812466770204,
      "company": null,
      "province": "Ontario",
      "country": "Canada",
      "province_code": "ON",
      "country_code": "CA",
      "country_name": "Canada",
      "default": true
    }
  ]
}
```

## Verification Steps

1. **Verify Successful Address Retrieval**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully retrieve the list of addresses for the customer.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Verify Address Details**

   - **Verify the details of the retrieved address:**
     - Expected: The address details in the response should match the expected values.

3. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

4. **Negative Test - Invalid Customer ID**

   - Send a GET request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

5. **Negative Test - Invalid Limit Parameter**

   - Send a GET request with an invalid or missing limit parameter.

   - **Verify HTTP Response Status Code:**
     - Expected: 400 Bad Request
     - The API should return a 400 Bad Request status code.

6. **Negative Test - Missing Access Token**

   - Send a GET request without providing the X-Shopify-Access-Token header.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

````

### Retrieves details for a single customer address

Certainly! Below is a sample API test case for the given cURL command:

```markdown
# API Test Case: Retrieve Details for a Single Customer Address

## Description

Send a GET request to the API endpoint to retrieve details for a single customer address.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Expected Response

```json
{
  "customer_address": {
    "id": 9817368330524,
    "customer_id": 7812466770204,
    "company": null,
    "province": "Ontario",
    "country": "Canada",
    "province_code": "ON",
    "country_code": "CA",
    "country_name": "Canada",
    "default": true
  }
}
```

## Verification Steps

1. **Verify Successful Address Retrieval**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK
     - The API should successfully retrieve details for the specified customer address.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Verify Address Details**

   - **Verify the details of the retrieved address:**
     - Expected: The address details in the response should match the expected values.

3. **Negative Test - Unauthorized Access**

   - Send a GET request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

4. **Negative Test - Invalid Customer ID**

   - Send a GET request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

5. **Negative Test - Invalid Address ID**

   - Send a GET request with an invalid or non-existent address ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

6. **Negative Test - Missing Access Token**

   - Send a GET request without providing the X-Shopify-Access-Token header.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

````

### Updates an existing customer address

```markdown
# API Test Case: Update Existing Customer Address

## Description

Send a PUT request to the API endpoint to update an existing customer address.

### Headers

- Content-Type: application/json
- X-Shopify-Access-Token: [YourAccessToken]

### Request Body

```json
{
  "address": {
    "id": 207119551,
    "zip": "90210"
  }
}
```

### Expected Response

```json
{
  "customer_address": {
    "customer_id": 7812466770204,
    "country": "Canada",
    "province": "Ontario",
    "company": null,
    "id": 9817368330524,
    "province_code": "ON",
    "country_code": "CA",
    "country_name": "Canada",
    "default": true
  }
}
```

## Verification Steps

1. **Verify Successful Address Update**

   - **Verify HTTP Response Status Code:**

     - Expected: 200 OK or 204 No Content
     - The API should successfully update the existing customer address.

   - **Verify Response Body:**
     - Compare the received JSON response with the expected structure and data.

2. **Verify Address Details After Update**

   - **Send a separate request to retrieve the updated address details:**
     - Use the GET method to retrieve the details of the customer address and ensure that the zip code has been updated.

3. **Negative Test - Unauthorized Access**

   - Send a PUT request without valid authentication credentials.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

4. **Negative Test - Invalid Customer ID**

   - Send a PUT request with an invalid or non-existent customer ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

5. **Negative Test - Invalid Address ID**

   - Send a PUT request with an invalid or non-existent address ID.

   - **Verify HTTP Response Status Code:**
     - Expected: 404 Not Found
     - The API should return a 404 Not Found status code.

6. **Negative Test - Missing Access Token**

   - Send a PUT request without providing the X-Shopify-Access-Token header.

   - **Verify HTTP Response Status Code:**
     - Expected: 401 Unauthorized
     - The API should return a 401 Unauthorized status code.

7. **Negative Test - Missing Required Fields in Request Body**

   - Send a PUT request with missing required fields in the request body.

   - **Verify HTTP Response Status Code:**
     - Expected: 400 Bad Request
     - The API should return a 400 Bad Request status code.

````
### Sets the default address for a customer

Certainly! Below is an API test case for the provided `PUT` method that sets the default address for a customer. This test case is written in a Gherkin-like syntax for better readability:

```gherkin
## API Test Case: Set Default Address for a Customer

**Test Steps:**

1. **Send a PUT request to set the default address for a customer:**
   - **Endpoint:** `/admin/api/2024-01/customers/207119551/addresses/1053317292/default.json`
   - **Method:** PUT
   - **Headers:**
     - Content-Type: application/json
     - X-Shopify-Access-Token: [YourAccessToken]
   - **Verify:** The API should successfully update the default address for the specified customer.

2. **Verify the HTTP response status code:**
   - **Expected:** 200 OK - The API should return a success status code.

3. **Verify the response body for the updated customer address:**
   - **Expected Response Body:**
     ```json
     {
         "customer_address": {
             "id": 9817368330524,
             "customer_id": 7812466770204,
             "company": null,
             "province": "Ontario",
             "country": "Canada",
             "province_code": "ON",
             "country_code": "CA",
             "country_name": "Canada",
             "default": true
         }
     }
     ```
   - **Verify:** The response should contain the updated customer address details with the "default" field set to true.

4. **Negative Test - Non-existing Customer ID:**
   - **Send a PUT request to set the default address for a non-existing customer ID.**
   - **Expected:** The API should return an appropriate error response (e.g., 404 Not Found), indicating that the customer was not found.

5. **Negative Test - Non-existing Address ID:**
   - **Send a PUT request to set the default address with a non-existing address ID for the specified customer.**
   - **Expected:** The API should return an appropriate error response (e.g., 404 Not Found), indicating that the address was not found.

6. **Negative Test - Unauthorized Access:**
   - **Send a PUT request without valid authentication credentials.**
   - **Expected:** The API should return a 401 Unauthorized status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a PUT request to an invalid endpoint for setting the default address.**
   - **Expected:** The API should return a 404 Not Found status code.

**Note:**
- Replace [YourAccessToken] with the actual access token.
- Adjust the endpoint and test steps based on your specific API version and requirements.
````

### Performs bulk operations for multiple customer addresses

**Test Steps:**

1. **Send a PUT request to perform bulk operations for multiple customer addresses:**

   - **Endpoint:** `/admin/api/2024-01/customers/207119551/addresses/set.json?address_ids%5B%5D=1053317290&operation=destroy`
   - **Method:** PUT
   - **Headers:**
     - Content-Type: application/json
     - X-Shopify-Access-Token: [YourAccessToken]
   - **Verify:** The API should successfully perform bulk operations for the specified customer addresses.

2. **Verify the HTTP response status code:**

   - **Expected:** 200 OK - The API should return a success status code.

3. **Verify the response body:**

   - **Expected Response Body:**
     ```json
     {}
     ```
   - **Verify:** The response body should be an empty JSON object `{}`, indicating a successful operation.

4. **Negative Test - Non-existing Customer ID:**

   - **Send a PUT request to perform bulk operations for a non-existing customer ID.**
   - **Expected:** The API should return an appropriate error response (e.g., 404 Not Found), indicating that the customer was not found.

5. **Negative Test - Non-existing Address ID in Bulk Operations:**

   - **Send a PUT request to perform bulk operations with a non-existing address ID for the specified customer.**
   - **Expected:** The API should return an appropriate error response (e.g., 404 Not Found), indicating that the address was not found.

6. **Negative Test - Unauthorized Access:**

   - **Send a PUT request without valid authentication credentials.**
   - **Expected:** The API should return a 401 Unauthorized status code.

7. **Negative Test - Invalid Endpoint:**
   - **Send a PUT request to an invalid endpoint for performing bulk operations.**
   - **Expected:** The API should return a 404 Not Found status code.

### Removes an address from a customer’s address list

**Test Steps:**

1. **Send a DELETE request to remove an address from a customer’s address list:**

   - **Endpoint:** `/admin/api/2024-01/customers/207119551/addresses/1053317291.json`
   - **Method:** DELETE
   - **Headers:**
     - Content-Type: application/json
     - X-Shopify-Access-Token: [YourAccessToken]
   - **Verify:** The API should successfully remove the specified address from the customer's address list.

2. **Verify the HTTP response status code:**

   - **Expected:** 200 OK - The API should return a success status code.

3. **Verify the response body for a successful removal:**

   - **Expected Response Body:**
     ```json
     {}
     ```
   - **Verify:** The response body should be an empty JSON object `{}`, indicating a successful removal.

4. **Negative Test - Attempt to Delete Default Address:**

   - **Send a DELETE request to remove the customer’s default address.**
   - **Expected:** The API should return an appropriate error response with a message indicating that the default address cannot be deleted.
     ```json
     {
       "errors": {
         "base": ["Cannot delete the customer’s default address"]
       }
     }
     ```
   - **Verify:** The API should return an error message specifying that the customer’s default address cannot be deleted.

5. **Negative Test - Non-existing Customer ID:**

   - **Send a DELETE request to remove an address from a non-existing customer ID.**
   - **Expected:** The API should return an appropriate error response (e.g., 404 Not Found), indicating that the customer was not found.

6. **Negative Test - Non-existing Address ID:**

   - **Send a DELETE request to remove a non-existing address ID for the specified customer.**
   - **Expected:** The API should return an appropriate error response (e.g., 404 Not Found), indicating that the address was not found.

7. **Negative Test - Unauthorized Access:**

   - **Send a DELETE request without valid authentication credentials.**
   - **Expected:** The API should return a 401 Unauthorized status code.

8. **Negative Test - Invalid Endpoint:**
   - **Send a DELETE request to an invalid endpoint for removing an address.**
   - **Expected:** The API should return a 404 Not Found status code.
