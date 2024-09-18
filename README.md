

# flexpoint Project

This is a Laravel project for managing products.

## Setup

1. Import SQL in Database:
   - Import the provided SQL file into your database management system.

2. Folder Placement:
   - Place the project folder in the `htdocs` directory if using XAMPP.

3. Running the Application:
   - Open a terminal in the project directory and run:
     ```
     php artisan serve
     ```
   - Access the application via `http://127.0.0.1:8000/`.

## Usage

- Visit `http://127.0.0.1:8000/admin-dashboard` to access the admin dashboard.
- Utilize the product dropdown menu to perform various product-related operations.

## Additional Notes

- Ensure proper configuration of your database credentials in the `.env` file.
- Customize routes, controllers, and views based on specific project requirements.
- Install necessary dependencies using Composer with `composer install`.

---


## Project Functionality Overview
This project demonstrates how to handle product-related actions such as purchases and new product creations using Laravel's **Events**, **Listeners**. When a product is purchased , events are triggered to update product quantities and  send email notifications when prodcut is  added. Emails are sent asynchronously using **Jobs** to ensure a smooth user experience without delays.

---

## Events, Listeners, and Jobs

### 1. ProductPurchased Event
The `ProductPurchased` event is triggered when a product is purchased. It holds information about the purchased product and informs the listeners to handle further actions like updating inventory.

### 2. UpdateProductQuantity Listener
The `UpdateProductQuantity` listener listens for the `ProductPurchased` event and is responsible for decreasing the product’s quantity in the database. After a successful purchase, it deducts the quantity from the available stock.



### 3. SendNewProductEmail Job
The `SendNewProductEmail` job is responsible for sending an email notification when a new product is created. It runs asynchronously, ensuring that the product creation process is not delayed by the email-sending process.

---

## Email Notifications

### New Product Email Notification
When a new product is added to the system, an email is sent to notify users. The email content is handled by the `NewProductCreated` mailable, which formats and sends the notification using the product details.

---

## Event & Listener Registration

Events and listeners are registered in the `EventServiceProvider`. This ensures that when an event is triggered (e.g., `ProductPurchased` or `NewProductAdded`), the respective listeners or jobs are dispatched to handle the logic.

---

## Asynchronous Email Dispatch
To avoid slowing down the request-response cycle, email notifications are dispatched using **Laravel Jobs**. This allows the system to handle emails in the background without affecting the performance of the application.

---

## Import and Export Products

### Import Products
The `importProducts` method is responsible for importing products into the system from an external source, such as a CSV or Excel file. This functionality allows for bulk product additions, making it easier to manage a large catalog.

- **Method**: `importProducts(Request $request)`
- **Description**: Handles importing products into the system from a request, typically through a file upload.

### Export Products
The `exportProducts` method is responsible for exporting the product list from the system. This functionality is useful for generating reports, backups, or sharing product data externally.

- **Method**: `exportProducts()`
- **Description**: Handles exporting the product data into a format such as CSV or Excel for easy sharing and management.

---

## Conclusion
This project effectively demonstrates how to leverage Laravel's **Events**, **Listeners**, **Jobs**, and file handling for managing products, including purchases, imports, exports, and notifications. By using **Jobs** to send emails asynchronously, the application ensures a responsive and smooth user experience. The import/export functionality simplifies bulk product management.

