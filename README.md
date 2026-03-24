# Trade Market API

Trade Market API is a layered ASP.NET Core Web API for managing an online store domain. It provides endpoints for products, categories, customers, receipts, and sales statistics, with a structure designed to keep data access, business logic, and HTTP delivery clearly separated.

## Project Highlights

- Built with `.NET 6` and `ASP.NET Core Web API`
- Uses `Entity Framework Core` with `SQL Server`
- Follows a layered architecture: `Data`, `Business`, `WebApi`
- Includes automated tests with `NUnit`, `Moq`, and `FluentAssertions`
- Exposes Swagger documentation in the Development environment

## Solution Structure

```text
TradeMarketPL-net6.sln
|-- Data
|   |-- Entities
|   |-- Interfaces
|   |-- Repositories
|   `-- Migrations
|-- Business
|   |-- Models
|   |-- Services
|   `-- Interfaces
|-- WebApi
|   |-- Controllers
|   |-- Properties
|   `-- Startup configuration
`-- TradeMarket.Tests
```

## Architecture

### Data Layer

The `Data` project is responsible for persistence and database interaction. It contains the EF Core `DbContext`, entity classes, repository implementations, and migrations.

### Business Layer

The `Business` project contains service interfaces, domain models, and application logic. It acts as the boundary between persistence and the API layer.

### API Layer

The `WebApi` project exposes REST endpoints, configures dependency injection, wires up Swagger, and hosts the application runtime.

### Test Layer

The `TradeMarket.Tests` project contains automated tests for application behavior and supports validation of the service and API layers.

## Technology Stack

- `.NET 6`
- `ASP.NET Core`
- `Entity Framework Core 6`
- `SQL Server / LocalDB`
- `Swagger / OpenAPI`
- `NUnit`
- `Moq`
- `FluentAssertions`
- `AutoMapper`

## Getting Started

### Prerequisites

- `.NET 6 SDK`
- `SQL Server LocalDB` or another accessible SQL Server instance
- `Visual Studio 2022` or the `dotnet` CLI

### Configuration

The default development connection string is defined in `WebApi/appsettings.Development.json`:

```json
"ConnectionStrings": {
  "Market": "Server=(localdb)\\mssqllocaldb;Database=MarketDB;Trusted_Connection=True;MultipleActiveResultSets=true"
}
```

If needed, replace it with a connection string for your local SQL Server instance.

### Restore Packages

```powershell
dotnet restore
```

### Apply Database Migrations

```powershell
dotnet ef database update --project Data --startup-project WebApi
```

### Run the Application

```powershell
dotnet run --project WebApi
```

The default launch profile exposes the API at:

- `http://localhost:5000`
- `https://localhost:5001`

Swagger UI is available in Development at:

- `http://localhost:5000/swagger`
- `https://localhost:5001/swagger`

## Running Tests

```powershell
dotnet test
```

## API Surface

### Products

- `GET /api/products`
- `GET /api/products/{id}`
- `GET /api/products?categoryId=1&minPrice=20&maxPrice=50`
- `POST /api/products`
- `PUT /api/products/{id}`
- `DELETE /api/products/{id}`

### Product Categories

- `GET /api/products/categories`
- `POST /api/products/categories`
- `PUT /api/products/categories/{id}`
- `DELETE /api/products/categories/{id}`

### Customers

- `GET /api/customers`
- `GET /api/customers/{id}`
- `GET /api/customers/products/{id}`
- `POST /api/customers`
- `PUT /api/customers/{id}`
- `DELETE /api/customers/{id}`

### Receipts

- `GET /api/receipts`
- `GET /api/receipts/{id}`
- `GET /api/receipts/{id}/details`
- `GET /api/receipts/{id}/sum`
- `GET /api/receipts/period?startDate=2021-12-01&endDate=2021-12-31`
- `POST /api/receipts`
- `PUT /api/receipts/{id}`
- `PUT /api/receipts/{id}/products/add/{productId}/{quantity}`
- `PUT /api/receipts/{id}/products/remove/{productId}/{quantity}`
- `PUT /api/receipts/{id}/checkout`
- `DELETE /api/receipts/{id}`

### Statistics

- `GET /api/statistics/popularProducts?productCount=2`
- `GET /api/statistics/customer/{id}/{productCount}`
- `GET /api/statistics/activity/{customerCount}?startDate=2020-07-21&endDate=2020-07-22`
- `GET /api/statistics/income/{categoryId}?startDate=2020-07-21&endDate=2020-07-22`

## Development Notes

- Swagger is enabled only for the Development environment.
- The solution uses shared analyzer configuration through `code-analysis.ruleset`.
- Style rules are configured in `stylecop.json`.
