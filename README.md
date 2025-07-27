# OpenCartPostmanCollection


````markdown
# Shopping Cart API Test Collection (Postman)

This project contains a Postman collection to test the Shopping Cart [OpenCart API Documentation](https://docs.opencart.com/en-gb/system/users/api/)
 It covers token generation, adding products, retrieving, updating, and deleting cart contents. The collection includes detailed tests validating response status codes, JSON structure


## API Endpoints Covered

1. **Create Token**  
   Generate an authentication token for API access.

2. **Add New Product (POST)**  
   Add a product to the shopping cart.

3. **Get Cart Content (GET)**  
   Retrieve current cart items, vouchers, and totals.

4. **Update Cart (POST)**  
   Modify product quantities or other cart details.

5. **Delete Cart (DELETE)**  
   Remove items or clear the shopping cart.

---

## Project Files

- `Opencart API.postman_environment.json` — Postman environment file for variables like base URL and token.


---

## Local Setup and Execution

### Prerequisites

- XAMPP installed with **MySQL** and **Apache** running.
- [Node.js](https://nodejs.org/) installed.
- Newman CLI installed globally:

```bash
npm install -g newman
````


### Steps to Prepare the Environment
1. **Opencart initial installation**
   https://github.com/opencart/opencart/blob/master/INSTALL.md
2. **Start XAMPP**
   Open XAMPP Control Panel and start **Apache** and **MySQL** services.
   <img width="636" height="469" alt="image" src="https://github.com/user-attachments/assets/785dc0dd-a7a8-4662-bd8f-4f1c99a6712c" />


3. **Create Database**

   * Navigate to `http://localhost/phpmyadmin` in your browser.
   * Create a new database for your application.
   * <img width="1323" height="497" alt="image" src="https://github.com/user-attachments/assets/3d61ae81-312f-43b4-8d44-d5fdbc579f6c" />


4. **Create API Requests**
   Build and test your API requests in Postman.

5. **Export Postman Collection**
   Export your Postman collection JSON file to your local machine.

### Steps to Run Tests Locally

1. Open your terminal and navigate to the folder containing the collection JSON.

2. Run the collection using Newman:

```bash
newman run "Opencart API.postman_collection.json" -r htmlextra
```

This command runs the tests and generates a colorful HTML report.

For a simpler HTML report, run:

```bash
newman run "Opencart API.postman_collection.json" -r html
```

---

## Jenkins Integration

### Steps to Run Newman Tests in Jenkins (macOS)

1. Push your project and collection files to GitHub.

2. In Jenkins, create or configure a job with a shell execution step containing the following script:

```bash

# Ensure correct PATH
export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"

# Verify Node and Newman installation
node --version
newman --version

# Prepare directories
mkdir -p newman
chmod -R 755 newman

# Run Newman collection
newman run "Opencart API.postman_collection.json" \
  --reporters cli,html,htmlextra \
  --reporter-html-export newman/newman-report.html \
  --color off
```

3. Use Jenkins **HTML Publisher Plugin** to publish the HTML report:

* Set the report directory to `reports`
* Set the index page to `newman-report.html`
* <img width="716" height="419" alt="image" src="https://github.com/user-attachments/assets/26b742c5-7c81-4047-ace3-cd06a4ef72a1" />


  <img width="741" height="708" alt="image" src="https://github.com/user-attachments/assets/12f0a8bf-8561-4fc4-ab91-17ae0370173a" />


---

## Tests Included

* HTTP status code validation (e.g., 200 OK)
* Response body JSON structure verification
* Field presence and data type checks

---

## Example API Response (GET Cart Content)

```json
{
  "products": [
    {
      "cart_id": "70",
      "product_id": "40",
      "name": "iPhone",
      "model": "product 11",
      "option": [],
      "quantity": "4",
      "stock": true,
      "shipping": "1",
      "price": "$123.20",
      "total": "$492.80",
      "reward": 0
    }
  ],
  "vouchers": [],
  "totals": [
    {
      "title": "Sub-Total",
      "text": "$404.00"
    },
    {
      "title": "Eco Tax (-2.00)",
      "text": "$8.00"
    },
    {
      "title": "VAT (20%)",
      "text": "$80.80"
    },
    {
      "title": "Total",
      "text": "$492.80"
    }
  ]
}
```

---

## Resources

* [OpenCart API Documentation](https://docs.opencart.com/en-gb/system/users/api/)

---

## Contributing

Contributions, issues, and feature requests are welcome!

---

## License

This project is licensed under the MIT License.




