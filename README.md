# Lab 3 – REST API Using Node.js, Express and SQLite

## Project Overview

This project demonstrates the development of a RESTful API using **Node.js, Express.js and SQLite**.

The application provides CRUD (Create, Read, Update and Delete) operations for managing book records. It also supports searching, filtering, sorting, pagination, input validation and error handling through HTTP requests.

### Live Deployment

| Description | Link |
|---|---|
| Live Application | https://lab-03-rest-api-wdz7.onrender.com/ |
| Get All Books | https://lab-03-rest-api-wdz7.onrender.com/books/ |
| GitHub Repository | https://github.com/navaneshreddy/Lab-03-REST-API |

**Deployment Platform:** Render  
**Deployment Status:** Live

---

## Student Details

- **Name:** [K Navaneswar Reddy]
- **Registration Number:** [252U1R8041]
- **Section:** [CSE QE 2A]

---

## Technologies Used

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime environment |
| Express.js | Backend web framework |
| SQLite | Relational database |
| sqlite3 | SQLite database driver |
| sqlite | Promise-based SQLite interface |
| Postman | API testing |
| Git & GitHub | Version control and source code hosting |
| Render | Cloud deployment |

---

## Project Folder Structure

```text
Lab-03-REST-API/
│
├── lab-03/
│   │
│   ├── index.js
│   ├── package.json
│   ├── package-lock.json
│   ├── books.db
│   ├── setup.sql
│   ├── .gitignore
│   ├── .node-version
│   ├── README.md
│   │
│   └── screenshots/
│       ├── 01-get-all-default.png
│       ├── 02-search-filter.png
│       ├── 03-price-range.png
│       ├── 04-sort-order.png
│       ├── 05-pagination.png
│       ├── 06-get-one.png
│       ├── 07-get-one-404.png
│       ├── 08-post-create.png
│       ├── 09-post-invalid-400.png
│       ├── 10-put-update.png
│       ├── 11-delete-book.png
│       └── 12-delete-404.png
│
└── render.yaml
```

### File Descriptions

- **index.js:** Main application file containing the Express server, API routes, validation logic and database operations.
- **package.json:** Contains project metadata, dependencies and execution scripts.
- **package-lock.json:** Locks dependency versions for consistent installations.
- **books.db:** SQLite database containing the book records.
- **setup.sql:** SQL script for creating the book table and inserting sample records.
- **.gitignore:** Specifies files and folders that Git should ignore.
- **.node-version:** Specifies the Node.js version used by the project.
- **README.md:** Project documentation.
- **screenshots/:** Contains screenshots demonstrating API testing.
- **render.yaml:** Contains Render deployment configuration.

---

## Installation and Setup

### Prerequisites

Install the following before running the application locally:

- Node.js
- npm
- Visual Studio Code
- Postman (for API testing)

### Step 1: Clone the Repository

```bash
git clone https://github.com/navaneshreddy/Lab-03-REST-API.git
```

### Step 2: Navigate to the Project Directory

```bash
cd Lab-03-REST-API/lab-03
```

### Step 3: Install Dependencies

```bash
npm install
```

### Step 4: Start the Application

For development mode:

```bash
npm run dev
```

For normal execution:

```bash
npm start
```

The server will run at:

```text
http://localhost:3000
```

The main API endpoint is:

```text
http://localhost:3000/books/
```

---

## Database Structure

The application uses SQLite as its database.

**Database Name:** `books.db`

**Table Name:** `book`

### Table Schema

| Column | Data Type | Description |
|---|---|---|
| id | INTEGER | Unique book ID and primary key |
| title | TEXT | Book title |
| author | TEXT | Book author's name |
| price | INTEGER | Book price |
| pages | INTEGER | Number of pages |

The `setup.sql` file creates the table and inserts 10 initial sample book records.

---

## API Endpoints

**Base URL:**

```text
https://lab-03-rest-api-wdz7.onrender.com
```

| HTTP Method | Endpoint | Description | Success Status |
|---|---|---|---|
| GET | `/books/` | Retrieve all books | 200 |
| GET | `/books/:bookId/` | Retrieve a specific book | 200 |
| POST | `/books/` | Add a new book | 201 |
| PUT | `/books/:bookId/` | Update an existing book | 200 |
| DELETE | `/books/:bookId/` | Delete a book | 200 |

---

## Query Parameters

The GET `/books/` endpoint supports searching, filtering, sorting and pagination.

| Parameter | Description | Example |
|---|---|---|
| search_q | Search books by title | `?search_q=Code` |
| order_by | Sort using a column | `?order_by=price` |
| order | Sort direction | `?order=DESC` |
| limit | Maximum records returned | `?limit=5` |
| offset | Number of records to skip | `?offset=5` |
| min_price | Minimum book price | `?min_price=300` |
| max_price | Maximum book price | `?max_price=500` |

### Examples

**1. Search for a book**

```text
GET /books/?search_q=Code
```

**2. Filter books by price**

```text
GET /books/?min_price=300&max_price=500
```

**3. Sort books by price in descending order**

```text
GET /books/?order_by=price&order=DESC
```

**4. Pagination**

```text
GET /books/?limit=3&offset=0
```

**5. Combine multiple query parameters**

```text
GET /books/?search_q=JavaScript&order_by=price&order=ASC&limit=5&offset=0
```

### Query Parameter Validation

- `order_by` accepts only `id`, `title`, `author`, `price` and `pages`.
- `order` accepts only `ASC` and `DESC`.
- `limit` must be a positive integer.
- `offset` must be a non-negative integer.
- `min_price` and `max_price` must be non-negative numbers.
- Minimum price cannot exceed maximum price.

Invalid query parameters return `400 Bad Request`.

---

## API Testing Using Postman

Postman is used to test all API endpoints by sending HTTP requests and examining the responses.

### 1. GET – Retrieve All Books

**Method:** GET

**URL:**

```text
https://lab-03-rest-api-wdz7.onrender.com/books/
```

**Expected Response:** `200 OK`

Returns a JSON array containing book records.

### 2. GET – Retrieve a Single Book

**Method:** GET

**URL:**

```text
https://lab-03-rest-api-wdz7.onrender.com/books/1/
```

**Expected Response:** `200 OK`

Returns the book with ID 1.

### 3. POST – Create a New Book

**Method:** POST

**URL:**

```text
https://lab-03-rest-api-wdz7.onrender.com/books/
```

In Postman:

1. Select POST.
2. Open the Body tab.
3. Select raw.
4. Choose JSON.
5. Enter the following request:

```json
{
  "title": "Sapiens",
  "author": "Yuval Noah Harari",
  "price": 450,
  "pages": 443
}
```

**Expected Response:** `201 Created`

```json
{
  "message": "Book added successfully",
  "bookId": 11
}
```

The returned ID is an example. The actual ID depends on the database.

### 4. PUT – Update an Existing Book

**Method:** PUT

**URL:**

```text
https://lab-03-rest-api-wdz7.onrender.com/books/11/
```

Select Body → raw → JSON.

```json
{
  "title": "Sapiens Revised Edition",
  "author": "Yuval Noah Harari",
  "price": 499,
  "pages": 450
}
```

**Expected Response:** `200 OK`

```json
{
  "message": "Book updated successfully"
}
```

### 5. DELETE – Delete a Book

**Method:** DELETE

**URL:**

```text
https://lab-03-rest-api-wdz7.onrender.com/books/11/
```

**Expected Response:** `200 OK`

```json
{
  "message": "Book deleted successfully"
}
```

---

## Input Validation and Error Handling

The application validates incoming data before executing database operations.

For POST and PUT requests, the following conditions must be satisfied:

- Title must be a non-empty string.
- Author must be a non-empty string.
- Price must be a non-negative number.
- Pages must be a positive integer.

### HTTP Status Codes

| Status Code | Meaning | Situation |
|---|---|---|
| 200 | OK | Successful GET, PUT or DELETE |
| 201 | Created | Book successfully created |
| 400 | Bad Request | Invalid input or query parameter |
| 404 | Not Found | Book ID or route does not exist |
| 500 | Internal Server Error | Unexpected server-side error |

### Example: Invalid Request

```json
{
  "title": "",
  "author": "Test Author",
  "price": -100,
  "pages": 0
}
```

**Expected Response:** `400 Bad Request`

```json
{
  "message": "Invalid input: title, author, non-negative price, and positive pages are required"
}
```

---

## Screenshots of API Testing

The following screenshots demonstrate the API operations and their responses.

### 1. GET All Books

![GET All Books](screenshots/01-get-all-default.png)

### 2. Search and Filter

![Search Filter](screenshots/02-search-filter.png)

### 3. Price Range Filtering

![Price Range](screenshots/03-price-range.png)

### 4. Sorting Order

![Sort Order](screenshots/04-sort-order.png)

### 5. Pagination

![Pagination](screenshots/05-pagination.png)

### 6. GET Single Book

![Get Single Book](screenshots/06-get-one.png)

### 7. GET Nonexistent Book

![GET 404](screenshots/07-get-one-404.png)

### 8. POST Create Book

![POST Create](screenshots/08-post-create.png)

### 9. POST Invalid Request

![POST Invalid](screenshots/09-post-invalid-400.png)

### 10. PUT Update Book

![PUT Update](screenshots/10-put-update.png)

### 11. DELETE Book

![DELETE Book](screenshots/11-delete-book.png)

### 12. DELETE Nonexistent Book

![DELETE 404](screenshots/12-delete-404.png)

---

## Important Notes About Render Deployment

This application uses SQLite and stores its database in `books.db`.

Render's free web services use an ephemeral filesystem. This means that changes made to the local SQLite database during runtime may be lost when the service restarts, spins down or redeploys.

The original database file is included in the project, so the initial sample records are available after deployment.

For permanent production database storage, a managed database such as PostgreSQL is recommended.

---

## Security and Implementation Features

- Uses Express JSON middleware to process JSON request bodies.
- Uses parameterized SQL queries to reduce SQL injection risks.
- Validates book IDs before database operations.
- Validates request bodies before INSERT and UPDATE operations.
- Uses an allowlist for sorting columns and directions.
- Handles invalid JSON requests.
- Returns appropriate HTTP status codes.
- Initializes the database before starting the Express server.

---

## Conclusion

This project demonstrates the implementation of a RESTful API using Node.js, Express.js and SQLite.

It provides complete CRUD functionality along with searching, filtering, sorting, pagination, input validation and error handling.

The application is deployed on Render and can be accessed publicly through its live URL. Postman is used to verify the API endpoints and their responses.
