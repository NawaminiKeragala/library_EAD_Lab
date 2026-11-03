# Library API — Lab 02

A Spring Boot REST API for managing books, using Spring Data JPA, MySQL, and Jakarta Bean Validation.

## Requirements

- Java 21
- MySQL with a database named `library_db`

## Run locally

Create the database in MySQL:

```sql
CREATE DATABASE library_db;
```

Set your database credentials in PowerShell, then start the application:

```powershell
$env:DB_USERNAME = 'root'
$env:DB_PASSWORD = 'your-database-password'
.\mvnw.cmd spring-boot:run
```

The API runs at `http://localhost:8080/api/books`. Hibernate creates or updates the database tables automatically.

The connection URL defaults to `jdbc:mysql://localhost:3306/library_db` and can be overridden with `DB_URL`. For local development, an optional `application-local.properties` file in the project root can hold `spring.datasource.password` and other settings. This file is ignored by Git. Environment variables are recommended when cloning this repository.

On macOS or Linux, use `sh ./mvnw` in place of `.\mvnw.cmd` and set environment variables using your shell.

## Endpoints

| Method | Path | Action |
| --- | --- | --- |
| GET | `/api/books` | List all books |
| GET | `/api/books/{id}` | Get a book by ID |
| POST | `/api/books` | Create a book |
| PUT | `/api/books/{id}` | Update a book |
| DELETE | `/api/books/{id}` | Delete a book |

Example request body for creating or updating a book:

```json
{
  "title": "Sample Book",
  "author": "Sample Author",
  "isbn": "9781234567897",
  "price": 1500.0
}
```

Title and author must not be blank. Price must be zero or positive when supplied. Requests for missing book IDs return HTTP 404.

## Tests

With MySQL running and database credentials configured:

```powershell
.\mvnw.cmd test
```
