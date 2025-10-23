## Trade Market Web Application
**Project Goal**

The Trade Market is a web application built using ASP.NET, designed to manage an online store with a focus on products, customers, receipts, and statistical insights. The application follows a three-layer architecture to ensure modularity, maintainability, and scalability. Additionally, a separate testing project is implemented to validate the functionality of each layer using NUnit.
Architecture

The project is structured into three distinct layers, each with specific responsibilities:
1.	**Data Access Layer (DAL)**
   
Handles data operations, including database context and entity definitions.<br/>
Implements repositories to manage data retrieval and storage.<br/>
Technologies: Entity Framework Core for ORM, SQL Server for data storage.

2.	**Business Logic Layer (BLL)**

Contains interfaces, models, and services that encapsulate the core business logic of the store.<br/>
Manages operations such as product filtering, customer management, and receipt processing.<br/>
Ensures separation of concerns by mediating between the DAL and the presentation layer.

4.	**Web Service Layer (Presentation Layer)**
   
Provides a RESTful API for client interaction, handling HTTP requests and responses.<br/>
Includes data validation and filtering to ensure secure and accurate communication with users.<br/>
Note: The visual interface is not included; this layer focuses solely on REST API endpoints.<br/>
Uses Swagger for API documentation and testing.

## API Routes
The application exposes a RESTful API with the following endpoints:
```
GET/api/products – all products
GET/api/products/{id} – a selected products
GET/api/products?categoryId=1&minPrice=20&maxPrice=50 – search for products by filter, ffor example, goods of category with Id = 1 and price less then maxPrice=50 and more then minPrice = 20
POST/api/products – add a product
PUT/api/products/{id} – change a product
DELETE/api/products/{id} – delete a product
GET/api/products/categories - get all categories
POST/api/products/categories - add a category 
PUT/api/products/categories{id} - update a category
DELETE/api/products/categories/{id} - delete a category

GET/api/customers – all customers
GET/api/customers/products/{id} - all customers who bought specified product
GET/api/customers/{id} – a selected customer
POST/api/customers – add a customer
PUT/api/customers/{id} – change a customer
DELETE/api/customers/{id} – delete a customer

GET/api/receipts – all receipts
GET/api/receipts/{id} – a selected receipt
GET/api/receipts/{id}/details - all details 
GET/api/receipts/{id}/sum – a selected receipt sum
GET/api/receipts/period?startDate=2021-12-1&endDate=2020-12-31 – all receipts by period, for example, from 2021-12-1 to 2020-12-31
POST/api/receipts – add a receipt
PUT/api/receipts/{id} – change a receipt
PUT/api/receipts/{id}/products/add/{productId}/{quantity} – add a product to a receipt
PUT/api/receipts/{id}/products/remove/{productId}/{quantity} – remove a product from a receipt
PUT/api/receipts/{id}/checkout – change a receipt check out value to true
DELETE/api/receipts/{id} – delete a receipt

GET/api/statistic/popularProducts?productCount=2 - Gets most popular products
GET/api/statisic/customer/{id}/{productCount} - Gets the concrete number of most favourite products of customer
GET/api/statistic/activity/{customerCount}?startDate= 2020-7-21&endDate= 2020-7-22 – Gets the most active customers in a period of time, for example, from 2020-7-21 to 2020-7-22
GET/api/statistic/income/{categoryId}?startDate= 2020-7-21&endDate= 2020-7-22 – Gets the income of category in a period of time, for example, from 2020-7-21 to 2020-7-22
```

## Testing

A dedicated testing project ensures the reliability of each layer:<br/>
•	Unit Tests: Validate individual components (e.g., repository methods, service logic) using NUnit.<br/>
•	Integration Tests: Verify interactions between layers, such as API endpoints and database operations.<br/>
•	Tests are organized by layer (Data, Business, Web Service) to ensure comprehensive coverage.<br/>

Technologies Used<br/>
•	ASP.NET Core: Web framework for building the REST API.<br/>
•	Entity Framework Core: ORM for database interactions.<br/>
•	Swagger/OpenAPI: API documentation and testing.<br/>
•	NUnit: Unit and integration testing framework.<br/>
•	SQL Server: Database for storing products, customers, receipts, and categories.

## Future Improvements<br/>
•	Implement authentication and authorization for secure API access.<br/>
•	Add caching mechanisms to improve performance for frequently accessed endpoints.<br/>
•	Enhance filtering capabilities with additional parameters (e.g., product name, customer demographics).<br/>
•	Integrate a front-end interface to interact with the API.

