# 📚 Library Management Database

This is a beginner-friendly project that demonstrates how to create and manage a **Library Management System** using **SQLite** and **DBeaver**. The database keeps track of authors, books, library members, and book loans.

---

## 🧾 Overview

This project includes the following four main tables:

| Table Name | Description |
|------------|-------------|
| `authors`  | Stores information about book authors |
| `books`    | Stores details of books and links each book to its author |
| `members`  | Stores details of library members |
| `loans`    | Tracks which member borrowed which book, and when it was returned |

The relationships between tables are managed using **foreign keys**. For example, each book has an `author_id` that refers to an author, and each loan refers to both a `book_id` and a `member_id`.

---

## 🛠️ How to Set It Up
### Step 1: Create a New SQLite Database

1. In DBeaver, go to **File > New > Database Connection**
2. Choose **SQLite** → Click **Next**
3. Select a location and name for your database file (e.g., `library.db`)
4. Click **Finish**

### Step 2: Create the Tables

1. Right-click your new database connection → **SQL Editor > New SQL Script**
2. Copy and paste the following SQL:

```sql
-- Authors Table
CREATE TABLE authors (
    author_id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

-- Books Table
CREATE TABLE books (
    book_id INTEGER PRIMARY KEY,
    title TEXT NOT NULL,
    author_id INTEGER,
    published_year INTEGER,
    FOREIGN KEY (author_id) REFERENCES authors(author_id)
);

-- Members Table
CREATE TABLE members (
    member_id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    join_date DATE
);

-- Loans Table
CREATE TABLE loans (
    loan_id INTEGER PRIMARY KEY,
    book_id INTEGER,
    member_id INTEGER,
    loan_date DATE,
    return_date DATE,
    FOREIGN KEY (book_id) REFERENCES books(book_id),
    FOREIGN KEY (member_id) REFERENCES members(member_id)
);
