QuickShop is an expanding online store that sells a variety of things, including groceries, apparel, electronics, and home goods. The need to secure QuickShop's data and the company's customer
base grows. The database is central to QuickShop's operations and manages user data, product inventory, sales transactions, and complex order details.

QuickShop implements a role-based access control (RBAC) system, assigning user accounts to specific roles with tailored access privileges. This ensures that users can only access the data necessary for 
their job functions, minimizing the risk of unauthorized modifications or data breaches. Here's a breakdown of the policies and rules defining what actions each role can perform on different tables within 
the database:

1. Administrator
The ultimate authority, with full access to all database tables (Users, Products, Orders, OrderDetails). Administrators can create, view, edit, and delete any record within the system. They are also
responsible for managing user roles and access permissions. However, the administrator can not create an order as only the customer can place an order.

2. Sales Personnel
Orders table: The sales personnel can view a list of orders, including details such as order ID, date, total amount, and user ID. The sales personnel can also update order table information on the order
date and total amount. The sales personnel should not update orders and user IDs because they are primary and foreign keys, respectively, and allowing sales personnel to edit these keys directly is
typically not recommended because it can result in inconsistent data and security flaws. Instead, the database system should automatically maintain the primary and foreign keys, allowing users to edit
additional record properties through the application interface. This method streamlines the application logic and aids in maintaining data integrity.

Order Details table: The sales personnel can view a list of order details, including detail ID, order ID, product ID, quantity, and price. The sales personnel can update order details, particularly the 
quantity. Still, other rows are strictly off-limits because, as previously mentioned, detail and order ID are primary and foreign keys, respectively, and it is not recommended for users to edit these keys 
directly to ensure data consistency and flaws. Moreover, the price row depends on input from the quantity row (i.e., price = price per quantity * quantity), and sales personnel updating dependent rows 
might lead to data consistency and integrity issues.

Product Table: The sales personnel can view product table details, including product ID, name, stock quantity, description, and price, and don't require product modification capabilities.

3. Inventory Manager:
Product table: The inventory manager can view the list of products, including product ID, quantity, and price. The inventory manager can also update the information in this table. They can input,
edit, and delete data when necessary. The IDs are generated and are not to be altered by the inventory manager; instead, they can only edit the data they input in the first place.

Order table: The inventory manager can view the order information, including the product ordered and all the details corresponding to the order, including order ID, user ID, quantity, and price. 
This ensures that they have all the relevant information to keep track of the inventory. When the inventory manager is aware of some product that is always getting sold out, for example, they would be able
to restock on time, and this benefits the business greatly.

User table: Although the inventory manager possesses access to the order table, which contains user details such as the user's name, they are strictly prohibited from altering such information. Such 
actions from the inventory manager would compromise the authenticity and integrity of the data, making the system less trustworthy as data is falsified.

Order Details table: The inventory manager can view order detail information such as order ID, order detail ID, Product ID, quantity, and price.

4. Customer

Users table: The customer can view user information, namely Name, ID, email, and role in relation to their login credentials. Additionally, the customer can update their name, email, and password, which 
requires password verification to ensure the user's identity. The customer can not modify their user ID as users are not recommended to edit this key directly to ensure data consistency and flaws. Instead,
it is left to the database to manage automatically.

Orders table: The customer can view order information about the date and the total amount corresponding to the user ID of the customer currently logged into the session. Additionally, customers directly 
enter information in order tables concerning the ordered quantity while the system calculates the price by multiplying the amount ordered with the cost per quantity. The user ID is retrieved from the 
currently running logged-in session, and the date will correspond to the current date extracted from the system. The user ID, product ID, and date data can not be directly handled by the user to prevent 
data consistency flaws as they are primary keys and to reduce the risk of errors when choosing the order date.

Order details table: The customer can view order details information about the ordered product name, description, and quantity corresponding to the user logged into the session. Additionally, the system 
should automatically be able to enter information in the order details table corresponding to any customer order to maintain data consistency between the orders and the order details table.

Products table: The customer can view order details information about the ordered product name, description, and quantity corresponding to the user logged into the session. Additionally, the system should 
automatically enter information in the order details table corresponding to any customer order to maintain data consistency between the orders and the order details table.

Guide:

Database connection - connection.php

Login - login.php

Register - signUp.php

Logout - Logout.php

Landing page - index.php 

Admin pages:

manage orders table - manage_orders.php

manage order details table - manage_orderdetails

manage users table - manage_users.php

manage products table - manage_product.php

Customer pages:
homepage - Customer-Homepage.php

profile view and edit - Customer-profile.php

order products - Customer-SearchProducts.php

order history - Customer-OrderHistory.php

edit login details - Customer-EditLogin.php

Sales manager pages:

Dashboard - sales_dash.php

managing order and order view tables - orders.php

view product tables - products.php

Inventory pages:
Dashboard - inventory_dash.php

Order and order view tables - inventory_orders.php

managing product tables - inventory_products.php
