# CIS 301 - Public API Integration Lab

## Project Description
This project demonstrates how to integrate a public API using FastAPI and a Python command-line client using Typer.

The server retrieves book information from the Open Library API using an ISBN number. The client sends HTTP requests to the FastAPI server and displays the responses in JSON format.

```
## Requirements
- Python 3.12
- FastAPI
- Uvicorn
- Requests
- Pydantic
- Typer

## Installation
Create a virtual environment:

```powershell
python -m venv .venv
```

Install the required packages:

```powershell
python -m pip install -r requirements.txt
```

## Running the Server

Open the PyCharm terminal in the `public_api_lab` folder and run:

```powershell
python -m uvicorn server.main:app --reload
```

The server runs at:

http://127.0.0.1:8000

API documentation:

http://127.0.0.1:8000/docs

## Running the Client

Open a second terminal while the server is running.

Navigate to the client folder:

```powershell
cd client
```

Display available commands:

```powershell
python client.py --help
```

Get a book using its ISBN:

```powershell
python client.py get_book 9780140328721
```

## Additional Challenges Completed

I implemented Challenges 1, 2, 3, and 5.

### Challenge 1: Search Books by Title

Added an endpoint that allows users to search for books by title using the Open Library API.

**Server endpoint:** `GET /books/search`

**Client command:**

```powershell
python client.py search_title "great"
```

### Challenge 2: Cache Book Data

Implemented a dictionary in the FastAPI server to store book information after a successful ISBN lookup.

When the same ISBN is requested again, the server retrieves the information from the cache instead of sending another request to Open Library.

**Client commands:**

```powershell
python client.py get_book 9780140328721
python client.py get_book 9780140328721
```

The cache is stored in memory and resets when the server restarts.

### Challenge 3: Validate Publication Date Range

Added optional minimum and maximum publication years to check whether a book's publication date falls within a specified range.

**Valid date range test:**

```powershell
python client.py get_book 9780140328721 --min-year 1980 --max-year 2020
```

**Invalid date range test:**

```powershell
python client.py get_book 9780140328721 --min-year 2020 --max-year 2025
```

The server returns an error when the publication year is outside the requested range.

### Challenge 5: Fetch Multiple ISBNs

Added an endpoint that allows users to retrieve information for multiple ISBN numbers in one request.

**Server endpoint:** `GET /books/multiple`

**Client command:**

```powershell
python client.py multiple  9780140328721 9780142437247
```

The server returns results for each requested ISBN.

## Error Handling

The application includes error handling for:
- Invalid ISBN numbers
- Books not found
- Open Library connection errors
- Invalid publication date ranges
- Missing or unrecognized publication dates

## Testing

The application is tested using the PyCharm terminal, Postman and FastAPI Swagger UI.

The tests include retrieving a book by ISBN, searching by title, testing the cache, validating publication dates, and retrieving multiple ISBNs.