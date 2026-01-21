# Week 8: Database Integration & SQL Security

!!! info "Lesson Details"

    **Duration:** 90-120 minutes (self-paced)
    **Focus:** Understanding databases, writing secure SQL queries, and preventing SQL injection attacks
    **Mode:** Self-paced with hands-on activities

    **Prerequisites:**

    - Week 7: Server-side programming and basic authentication
    - Week 4: Input validation and XSS prevention
    - Week 3: Git basics
    - Understanding of data types and variables
    - Basic command line skills

    **What You'll Build:** A secure blog application with persistent database storage, replacing Week 7's in-memory user storage with a proper database.

## Learning Objectives

By the end of this lesson, you will be able to:

1. **Connect** web applications to databases using connection strings and environment variables
2. **Design** database schemas with proper normalisation, primary keys, and foreign keys
3. **Write** SQL queries for all CRUD operations (Create, Read, Update, Delete)
4. **Implement** prepared statements to prevent SQL injection attacks
5. **Apply** database indexing to improve query performance
6. **Create** shell scripts for automated database backups

**Syllabus Alignment:**

!!! info "Programming for the Web"
    - ✓ Model elements that form a web development system (interfacing with databases based on SQL or non-SQL)
    - ✓ Observe and describe back-end process (databases)
    - ✓ Develop web application with shell scripts (database backup scripts)
    - ✓ Apply web-based database and construct script that executes SQL (selecting fields, 'group by', common SQL queries, constraints using WHERE, table joins)
    - ✓ Investigate effect of big data on web architecture (data mining, metadata, database indexing)

!!! info "Secure Software Architecture"
    - ✓ Explore fundamental security concepts (confidentiality, integrity, availability - applied to data)
    - ✓ Design, develop and implement code using defensive data input handling practices (input validation, sanitisation - preventing SQL injection)
    - ✓ Apply security features for data protection

---

??? warning "Database Choice"
    To simplify your development process it is strongly suggested that you use **SQLite** for all lessons. It supports all key concepts of the syllabus.

    Only pick **Postgres** if you have some understanding of databases or have someone who can support you. It is a fully functional SQL database that is used across many of the worlds top Software companies. Also, it is best to run it within docker, which is out of scope for this syllabus, but will simplfy setup and teardown of the database.

## 1: Database Fundamentals and Connection

**Duration:** 15-20 minutes | **Bloom's Level:** Remember, Understand | **GRR:** Teacher-led introduction

### What is a Database?

A **database** is an organised collection of structured data that provides **persistent storage** - meaning your data survives server restarts and power failures. Unlike storing data in variables or arrays (which disappear when your programme stops), databases keep your data safe permanently.

!!! question "Activating Prior Knowledge"
    Remember Week 7 when we stored users in an array? What happened when we restarted the server? All users disappeared! Databases solve this problem.

### Key Database Terminology

```mermaid
graph TD
    A[Database System] --> B[Database]
    B --> C[Tables]
    C --> D[Rows/Records]
    C --> E[Columns/Fields]
    D --> F[Individual Data Values]
    
    style A fill:#e1f5ff
    style B fill:#b3e5fc
    style C fill:#81d4fa
    style D fill:#4fc3f7
    style E fill:#4fc3f7
```

| Term | Definition | Example |
|------|------------|---------|
| **Database** | Organised collection of structured data | Your blog's database containing all users, posts, and comments |
| **Table** | Collection of related data in rows and columns | `users` table stores all user information |
| **Row** | A single record in a table | One user: id=5, username="alice", email="alice@example.com" |
| **Column** | A field that stores specific type of data | The `email` column stores email addresses |
| **Schema** | Blueprint of database structure | Defines all tables, columns, data types, and relationships |
| **Primary Key** | Unique identifier for each row (cannot be null) | User ID: Each user has unique ID (1, 2, 3...) |
| **Foreign Key** | Column referencing another table's primary key | `posts.author_id` links to `users.id` |

### SQL vs NoSQL Databases

| Feature | SQL (Relational) | NoSQL |
|---------|-----------------|-------|
| **Structure** | Tables with fixed schema | Flexible (documents, key-value, graph) |
| **Examples** | PostgreSQL, MySQL, SQLite | MongoDB, Redis, Cassandra |
| **Best For** | Structured data with relationships | Unstructured data, rapid scaling |
| **Schema** | Must be defined upfront | Can change dynamically |
| **Relationships** | JOINs between tables | Embedded or referenced documents |

!!! tip "Which Should I Use?"
    - **SQL** for: User accounts, financial records, blog posts (structured data with clear relationships)
    - **NoSQL** for: Real-time chat, social media feeds, IoT sensor data (flexible, rapidly changing data)

### Database Connection

**Connection String:** A URL containing all information needed to connect to a database.

=== "SQLite"

    ```
    sqlite:///mydatabase.db
    ```

    Breaking down the connection string:

    - `sqlite:///` - Database type (SQLite with three slashes for relative path)
    - `mydatabase.db` - Database file name (stored in current directory)

    **Alternative paths:**

    Absolute path (Unix/Linux/Mac):
    ```
    sqlite:////home/username/projects/mydatabase.db
    ```

    Absolute path (Windows):
    ```
    sqlite:///C:/Users/username/projects/mydatabase.db
    ```

    Relative path with subdirectory:
    ```
    sqlite:///data/mydatabase.db
    ```

    In-memory database (temporary, lost when programme closes):
    ```
    sqlite:///:memory:
    ```

    **Key differences from PostgreSQL:**

    - **No username/password:** SQLite is file-based, so there's no authentication
        - **There is no security on the database contents**
    - **No host/port:** SQLite doesn't run as a server, it's just a file
    - **Three slashes:** `sqlite:///` indicates a relative path from current directory
    - **Four slashes:** `sqlite:////` indicates an absolute path (note the extra slash after `://`)
    ```

    !!! tip "Python sqlite3 Module"
        When using Python's built-in `sqlite3` module directly (not through an ORM), you simply provide the file path:
        
            import sqlite3
            
            # Relative path
            conn = sqlite3.connect('mydatabase.db')
            
            # Absolute path
            conn = sqlite3.connect('/home/username/projects/mydatabase.db')
            
            # In-memory database
            conn = sqlite3.connect(':memory:')

    !!! warning "File Permissions"
        Ensure your application has read/write permissions for:
        
        - The database file itself (`mydatabase.db`)
        - The directory containing the database
        - SQLite creates temporary files (`.db-journal`, `.db-wal`) in the same directory

=== "Postgres"
    ```
    postgresql://username:password@localhost:5432/mydatabase
    ```

    Breaking down the connection string:

    - `postgresql://` - Database type (in this case Postgres)
    - `username:password` - Credentials
    - `localhost` - Server location (your computer)
    - `5432` - Port number
    - `mydatabase` - Database name

    !!! danger "Security Critical"
        **NEVER** hard-code credentials in your source code or commit them to Git!
        
        ```python
        # ❌ WRONG - Don't do this!
        db_password = "mypassword123"
        
        # ✅ CORRECT - Use environment variables
        import os
        db_password = os.getenv('DB_PASSWORD')
        ```

### What is CRUD?

**CRUD** is the alphabet of databases - everything you do with data is one of these four operations:

```mermaid
graph LR
    A[CRUD Operations] --> B[Create: Add new data]
    A --> C[Read: Retrieve data]
    A --> D[Update: Modify data]
    A --> E[Delete: Remove data]
    
    B --> F[SQL: INSERT]
    C --> G[SQL: SELECT]
    D --> H[SQL: UPDATE]
    E --> I[SQL: DELETE]
    
    style A fill:#4caf50
    style B fill:#81c784
    style C fill:#81c784
    style D fill:#81c784
    style E fill:#81c784
```

| Operation | SQL Command | HTTP Method | Real-World Example |
|-----------|-------------|-------------|-------------------|
| **Create** | INSERT | POST | User signs up for account |
| **Read** | SELECT | GET | View blog post |
| **Update** | UPDATE | PUT/PATCH | Edit profile information |
| **Delete** | DELETE | DELETE | Remove old comment |

---

### Activity 1.1: Explore Database Structure (WE DO)

**Duration:** 10 minutes

**Objective:** Understand database tables and relationships

!!! note "What You'll Do"
    1. Open DB Browser for SQLite (or similar GUI tool)
    2. Open the sample database: `blog_sample.db`
    3. Examine the `users` table structure
    4. Identify the primary key
    5. Look at the `posts` table
    6. Identify the foreign key linking to users

**Questions to Answer:**

1. What columns exist in the `users` table?
2. Which column is the primary key? How can you tell?
3. In the `posts` table, which column is the foreign key?
4. What does this foreign key relationship represent?

??? success "Expected Answers"
    1. Columns: id, username, email, password_hash, created_at
    2. Primary key: `id` (unique identifier, auto-increments)
    3. Foreign key: `author_id`
    4. Links each post to the user who wrote it

---

### Activity 1.2: Set Up Database Connection (YOU DO)

**Duration:** 10 minutes

**Objective:** Configure secure database connection

!!! note "What You'll Do"
    1. Create a `.env` file for environment variables
    2. Add database credentials (don't commit this file!)
    3. Update `.gitignore` to exclude `.env`
    4. Test database connection

**Step-by-Step:**

**1. Create `.env` file:**
```bash
# .env
DB_NAME=blog_database.db
DB_USER=webapp_user
DB_PASSWORD=your_secure_password_here
```

**2. Update `.gitignore`:**
```bash
# Add to .gitignore
.env
*.db
__pycache__/
```

**3. Create and activate a virtual environment:**

Linux/macOS:
```bash
python3 -m venv .venv
source .venv/bin/activate
```

Windows:
```bash
python -m venv .venv
.venv/Scripts/activate
```

You should see `(venv)` appear at the start of your command prompt, indicating the virtual environment is active.

**4. Install required packages:**
```bash
pip install flask python-dotenv
```

!!! tip "Virtual Environment Best Practices"
    **Always use a virtual environment** for Python projects. This:
    
    - Keeps project dependencies isolated
    - Prevents conflicts between different projects
    - Avoids modifying system Python packages
    - Makes your project reproducible on other machines
    
    **To deactivate the virtual environment when finished:**
    ```bash
    deactivate
    ```
    
    **Add to your `.gitignore`:**
    ```
    .venv/
    __pycache__/
    *.pyc
    .env
    *.db
    ```

!!! warning "Never Commit .venv/"
    The `.venv/` directory should **never** be committed to Git. Instead, use a `requirements.txt` file to track dependencies:
    
    **Create requirements.txt:**
    ```bash
    pip freeze > requirements.txt
    ```
    
    **Install from requirements.txt (on another machine):**
    ```bash
    pip install -r requirements.txt
    ```

**5. Test connection (Python example):**
```python
import sqlite3
import os
from dotenv import load_dotenv

# Load environment variables
load_dotenv()

# Connect to database
db_name = os.getenv('DB_NAME')
conn = sqlite3.connect(db_name)
print(f"Connected to {db_name} successfully!")

# Close connection
conn.close()
```

**6. Run your test:**
```bash
python test_connection.py
```

??? success "Success Criteria"
    - `.env` file created and contains database credentials
    - `.env` is listed in `.gitignore`
    - Connection test prints success message
    - No credentials visible in your source code

!!! warning "Common Mistake"
    Don't commit `.env` to Git! If you accidentally do:
    ```bash
    git rm --cached .env
    git commit -m "Remove .env from version control"
    ```

---

## 2: Database Schema Design & Normalisation

**Duration:** 15-20 minutes | **Bloom's Level:** Understand, Apply | **GRR:** Guided practice

### Database Schema Design

A **schema** is your database's blueprint. Good schema design prevents data problems before they start.

### Normalisation: Organising Data Efficiently

**Normalisation** reduces data redundancy and improves integrity by dividing large tables into smaller, related tables.

**Example: Blog Application Schema**

```mermaid
erDiagram
    USERS ||--o{ POSTS : writes
    USERS ||--o{ COMMENTS : makes
    POSTS ||--o{ COMMENTS : receives
    CATEGORIES ||--o{ POSTS : categorises
    
    USERS {
        int id PK
        string username
        string email
        string password_hash
        datetime created_at
    }
    
    POSTS {
        int id PK
        string title
        text content
        int author_id FK
        int category_id FK
        datetime created_at
        datetime updated_at
    }
    
    COMMENTS {
        int id PK
        int post_id FK
        int user_id FK
        text content
        datetime created_at
    }
    
    CATEGORIES {
        int id PK
        string name
        text description
    }
```

### Why Normalisation Matters

**❌ Unnormalised (Poor Design):**

| post_id | title | content | author_name | author_email | author_bio |
|---------|-------|---------|-------------|--------------|------------|
| 1 | Hello | ... | Alice | alice@test.com | I love coding... |
| 2 | World | ... | Alice | alice@test.com | I love coding... |
| 3 | SQL | ... | Alice | alice@test.com | I love coding... |

**Problems:**

- Alice's data repeated in every post (redundancy)
- If Alice changes email, must update every post
- Wasted storage space
- Risk of inconsistency (updating some rows but not others)

**✅ Normalised (Good Design):**

**Users Table:**

| user_id | username | email | bio |
|---------|----------|-------|-----|
| 1 | Alice | alice@test.com | I love coding... |

**Posts Table:**

| post_id | title | content | author_id |
|---------|-------|---------|-----------|
| 1 | Hello | ... | 1 |
| 2 | World | ... | 1 |
| 3 | SQL | ... | 1 |

**Benefits:**

- ✅ Alice's data stored once
- ✅ One update changes all references
- ✅ Less storage space
- ✅ Data consistency guaranteed

### Creating Tables with SQL

**SQL** (Structured Query Language) is the standardised language for managing relational databases.

**Example: Create Users Table**

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    email TEXT NOT NULL UNIQUE,
    password_hash TEXT NOT NULL,
    bio TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**Breaking it down:**

- `CREATE TABLE users` - Creates new table named "users"
- `id INTEGER PRIMARY KEY` - Unique identifier (primary key)
- `AUTOINCREMENT` - Database automatically assigns next number
- `NOT NULL` - Field must have a value
- `UNIQUE` - No two users can have same username/email
- `DEFAULT CURRENT_TIMESTAMP` - Automatically sets creation time

**Example: Create Posts Table with Foreign Key**

```sql
CREATE TABLE posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    content TEXT NOT NULL,
    author_id INTEGER NOT NULL,
    category_id INTEGER,
    status TEXT DEFAULT 'draft',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (author_id) REFERENCES users(id) ON DELETE CASCADE
);
```

**Foreign Key Explained:**

- `FOREIGN KEY (author_id)` - This column links to another table
- `REFERENCES users(id)` - Links to the `id` column in `users` table
- `ON DELETE CASCADE` - If user deleted, their posts are also deleted
    - most production databases will avoid `ON DELETE CASCADE` also called cascade delete as it can result in unexpected data being deleted when not intended
    - eg: Maybe you want the users data to be removed but it should be stored in a backup system for 5 years for policy reasons. The cascaade delete above could result in all of the data being deleted before backed up.

---

### Activity 2.1: Design Your Database Schema (WE DO)

**Duration:** 15 minutes

**Objective:** Create a complete database schema for a blog application

!!! note "Requirements"
    Design tables for:

    1. Users (authentication and profile)
    2. Posts (blog content)
    3. Comments (user feedback)
    4. Categories (organising posts)
    
    Each table must have:

    - Primary key
    - Appropriate data types
    - NOT NULL constraints where needed
    - Foreign keys for relationships

**Starter Template:**

```sql
-- Users table
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL UNIQUE,
    -- Add more columns here
);

-- Posts table
CREATE TABLE posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    -- Design this table
);

-- Comments table
CREATE TABLE comments (
    -- Design this table
);

-- Categories table
CREATE TABLE categories (
    -- Design this table
);
```

**Guided Questions:**

1. What information do we need to store about users?
2. What information do we need for each blog post?
3. How do we link a post to its author?
4. How do we link a comment to both the post and the commenter?

??? example "Sample Solution"
    ```sql
    CREATE TABLE users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        username TEXT NOT NULL UNIQUE,
        email TEXT NOT NULL UNIQUE,
        password_hash TEXT NOT NULL,
        bio TEXT,
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    );
    
    CREATE TABLE categories (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL UNIQUE,
        description TEXT
    );
    
    CREATE TABLE posts (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        title TEXT NOT NULL,
        content TEXT NOT NULL,
        author_id INTEGER NOT NULL,
        category_id INTEGER,
        status TEXT DEFAULT 'draft',
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
        updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (author_id) REFERENCES users(id) ON DELETE CASCADE,
        FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL
    );
    
    CREATE TABLE comments (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        post_id INTEGER NOT NULL,
        user_id INTEGER NOT NULL,
        content TEXT NOT NULL,
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE,
        FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
    );
    ```

---

### Activity 2.2: Create Your Database (YOU DO)

**Duration:** 10 minutes

**Objective:** Execute SQL statements to create your database structure

!!! note "What You'll Do"
    1. Create a new file: `schema.sql`
    2. Write CREATE TABLE statements for all tables
    3. Execute the schema file to create your database
    4. Verify tables were created correctly

**Step-by-Step:**

**1. Create `schema.sql`:**
```sql
-- schema.sql
-- Database schema for blog application

CREATE TABLE users (
    -- Your design from Activity 2.1
);

CREATE TABLE categories (
    -- Your design
);

CREATE TABLE posts (
    -- Your design
);

CREATE TABLE comments (
    -- Your design
);
```

**2. Execute schema:**
```bash
# SQLite
sqlite3 blog_database.db < schema.sql

# PostgreSQL
psql -U username -d database_name -f schema.sql
```

**3. Verify tables exist:**
```sql
-- List all tables
.tables

-- See structure of users table
.schema users
```

??? success "Success Criteria"
    - All four tables created without errors
    - Each table has a primary key
    - Foreign keys properly reference other tables
    - You can view table structures with `.schema`

**Git Checkpoint:**
```bash
git add schema.sql
git commit -m "Add database schema for blog application

- Create users table with authentication fields
- Create posts table with foreign key to users
- Create comments table with relationships
- Create categories for post organisation"
```

---

## Content Part 3: SQL Queries and CRUD Operations (WE DO)

**Duration:** 20-25 minutes | **Bloom's Level:** Apply | **GRR:** Guided practice

### SQL CRUD Operations

Now that we have tables, let's fill them with data and query them.

### CREATE: INSERT Operations

**Insert Single Record:**
```sql
INSERT INTO users (username, email, password_hash) 
VALUES ('alice', 'alice@example.com', '$2b$12$hashed_password');
```

**Insert Multiple Records:**
```sql
INSERT INTO categories (name, description) 
VALUES 
    ('Technology', 'Posts about tech'),
    ('Travel', 'Travel experiences'),
    ('Food', 'Recipes and reviews');
```

**Insert with Returning ID (PostgreSQL):**
```sql
INSERT INTO users (username, email, password_hash) 
VALUES ('bob', 'bob@example.com', '$2b$12$hash')
RETURNING id;
```

### READ: SELECT Operations

A **query** is a request for data from the database.

**Select Everything:**
```sql
-- Get all columns from all users
SELECT * FROM users;
```

!!! warning "Avoid SELECT *"
    In production, specify exact columns you need. `SELECT *` is slower and retrieves unnecessary data.

**Select Specific Columns:**
```sql
-- Get only usernames and emails
SELECT username, email FROM users;
```

**WHERE Clause - Filtering Results:**

| Operator | Meaning | Example |
|----------|---------|---------|
| `=` | Equal to | `WHERE age = 25` |
| `!=` or `<>` | Not equal | `WHERE status != 'deleted'` |
| `>` | Greater than | `WHERE age > 18` |
| `<` | Less than | `WHERE price < 100` |
| `>=` | Greater or equal | `WHERE age >= 18` |
| `<=` | Less or equal | `WHERE stock <= 10` |
| `LIKE` | Pattern match | `WHERE name LIKE 'A%'` |
| `IN` | Match list | `WHERE country IN ('AU', 'NZ')` |
| `BETWEEN` | Range | `WHERE age BETWEEN 18 AND 65` |
| `AND` | Both conditions | `WHERE age > 18 AND country = 'AU'` |
| `OR` | Either condition | `WHERE country = 'AU' OR country = 'NZ'` |

**Examples:**
```sql
-- Single condition
SELECT * FROM users WHERE country = 'Australia';

-- Multiple conditions
SELECT * FROM users WHERE age > 18 AND country = 'Australia';

-- Pattern matching
SELECT * FROM users WHERE email LIKE '%@gmail.com';

-- List matching
SELECT * FROM posts WHERE status IN ('published', 'featured');
```

**ORDER BY - Sorting Results:**
```sql
-- Newest posts first
SELECT * FROM posts ORDER BY created_at DESC;

-- Oldest posts first
SELECT * FROM posts ORDER BY created_at ASC;

-- Multiple sort criteria
SELECT * FROM posts ORDER BY category_id ASC, created_at DESC;
```

**LIMIT - Restricting Results:**
```sql
-- Get 10 most recent posts
SELECT * FROM posts 
ORDER BY created_at DESC 
LIMIT 10;

-- Pagination: Skip first 10, get next 10
SELECT * FROM posts 
ORDER BY created_at DESC 
LIMIT 10 OFFSET 10;
```

**GROUP BY - Data Aggregation:**

**GROUP BY** groups rows with same values, allowing calculations on each group.

**Common Aggregate Functions:**

| Function | Purpose | Example |
|----------|---------|---------|
| `COUNT()` | Count rows | `SELECT COUNT(*) FROM users` |
| `SUM()` | Add values | `SELECT SUM(price) FROM orders` |
| `AVG()` | Average | `SELECT AVG(age) FROM users` |
| `MIN()` | Minimum | `SELECT MIN(price) FROM products` |
| `MAX()` | Maximum | `SELECT MAX(salary) FROM employees` |

**Examples:**
```sql
-- Count posts per user
SELECT author_id, COUNT(*) as post_count 
FROM posts 
GROUP BY author_id;

-- Average comments per post
SELECT post_id, AVG(rating) as avg_rating 
FROM comments 
GROUP BY post_id;

-- Posts per category
SELECT categories.name, COUNT(posts.id) as post_count
FROM categories
LEFT JOIN posts ON categories.id = posts.category_id
GROUP BY categories.id;
```

### UPDATE: Modifying Data

```sql
-- Update single field
UPDATE users 
SET email = 'newemail@example.com' 
WHERE id = 5;

-- Update multiple fields
UPDATE posts 
SET title = 'New Title', updated_at = CURRENT_TIMESTAMP 
WHERE id = 10;

-- Conditional update
UPDATE posts 
SET status = 'archived' 
WHERE created_at < '2023-01-01';
```

!!! danger "Always Use WHERE with UPDATE"
    Without WHERE clause, you'll update **EVERY** record in the table!
    
    ```sql
    -- ❌ DANGER: Updates ALL users!
    UPDATE users SET country = 'Australia';
    
    -- ✅ CORRECT: Updates only one user
    UPDATE users SET country = 'Australia' WHERE id = 5;
    ```

### DELETE: Removing Data

```sql
-- Delete specific record
DELETE FROM comments WHERE id = 100;

-- Delete based on condition
DELETE FROM posts WHERE status = 'spam';

-- Delete old records
DELETE FROM sessions WHERE created_at < DATE('now', '-30 days');
```

!!! danger "Always Use WHERE with DELETE"
    Without WHERE clause, you'll delete **EVERYTHING** in the table!
    
    ```sql
    -- ❌ DANGER: Deletes ALL posts!
    DELETE FROM posts;
    
    -- ✅ CORRECT: Deletes only spam
    DELETE FROM posts WHERE status = 'spam';
    ```

---

### Activity 3.1: Practice CRUD Operations (WE DO)

**Duration:** 15 minutes

**Objective:** Write SQL queries for common database operations

!!! note "Complete These Tasks"
    Work through each task, writing and executing SQL queries.

**Task 1: INSERT - Create Data**
```sql
-- 1. Insert yourself as a user
INSERT INTO users (username, email, password_hash) 
VALUES ('your_username', 'your_email@example.com', 'temp_hash');

-- 2. Insert a category
INSERT INTO categories (name, description) 
VALUES ('Tutorial', 'Educational content');

-- 3. Insert a post (use your user_id and category_id)
INSERT INTO posts (title, content, author_id, category_id, status) 
VALUES ('My First Post', 'Hello database world!', 1, 1, 'published');
```

**Task 2: SELECT - Read Data**
```sql
-- 4. Get all published posts
-- Your query here

-- 5. Find posts by a specific author
-- Your query here

-- 6. Count total users
-- Your query here

-- 7. Get 5 most recent posts
-- Your query here
```

**Task 3: UPDATE - Modify Data**
```sql
-- 8. Update your user's bio
-- Your query here

-- 9. Change a post's status to 'published'
-- Your query here
```

**Task 4: DELETE - Remove Data**
```sql
-- 10. Delete a specific comment (create one first!)
-- Your query here
```

??? example "Sample Solutions"
    ```sql
    -- Task 2.4: Get all published posts
    SELECT * FROM posts WHERE status = 'published';
    
    -- Task 2.5: Posts by specific author
    SELECT * FROM posts WHERE author_id = 1;
    
    -- Task 2.6: Count total users
    SELECT COUNT(*) as user_count FROM users;
    
    -- Task 2.7: 5 most recent posts
    SELECT * FROM posts ORDER BY created_at DESC LIMIT 5;
    
    -- Task 3.8: Update bio
    UPDATE users SET bio = 'Aspiring developer' WHERE id = 1;
    
    -- Task 3.9: Publish post
    UPDATE posts SET status = 'published', updated_at = CURRENT_TIMESTAMP WHERE id = 1;
    
    -- Task 4.10: Delete comment
    DELETE FROM comments WHERE id = 1;
    ```

---

### Activity 3.2: Table Joins (WE DO)

**Duration:** 15 minutes

**Objective:** Combine data from multiple tables using JOINs

### Understanding JOINs

A **JOIN** combines rows from two or more tables based on related columns.

```mermaid
graph LR
    A[Posts Table] -->|author_id| B[JOIN]
    C[Users Table] -->|id| B
    B --> D[Combined Result]
    
    style B fill:#4caf50
```

### JOIN Types Visual Guide

```mermaid
graph TD
    A[JOIN Types] --> B[INNER JOIN]
    A --> C[LEFT JOIN]
    A --> D[RIGHT JOIN]
    A --> E[FULL OUTER JOIN]
    
    B --> F[Only matching records from both tables]
    C --> G[All from left table + matches from right]
    D --> H[All from right table + matches from left]
    E --> I[All records from both tables]
    
    style A fill:#2196f3
    style B fill:#4caf50
    style C fill:#ff9800
    style D fill:#ff9800
    style E fill:#f44336
```

**INNER JOIN - Only Matching Records:**

```sql
-- Get posts with their author names
SELECT posts.title, posts.content, users.username 
FROM posts 
INNER JOIN users ON posts.author_id = users.id;
```

**Result:** Only posts that have a valid author (orphaned posts excluded)

**LEFT JOIN - All From Left Table:**

```sql
-- Get all users and their post count (including users with 0 posts)
SELECT users.username, COUNT(posts.id) as post_count 
FROM users 
LEFT JOIN posts ON users.id = posts.author_id 
GROUP BY users.id;
```

**Result:** Every user appears, even users who haven't posted (post_count = 0)

**Complex JOIN Example:**

```sql
-- Posts with authors and categories
SELECT 
    posts.title,
    users.username as author,
    categories.name as category,
    COUNT(comments.id) as comment_count
FROM posts
INNER JOIN users ON posts.author_id = users.id
INNER JOIN categories ON posts.category_id = categories.id
LEFT JOIN comments ON posts.id = comments.post_id
GROUP BY posts.id;
```

!!! warning "Old Style Comma Table Join"
    There is an older style of join using commas. It should be avoided as it doesn't give you as much control over your queries and can impact readabilty of your queries, especilly if they are large. You should still be able to understand this format as it will be used in some cases.

    ```sql
    SELECT users.name, posts.title
    FROM users, posts
    WHERE posts.author_id = users.id
    ```

!!! note "Practice Tasks"
    Complete these JOIN queries:
    
    1. Get all posts with author names and emails
    2. Find all users who have never posted
    3. Get posts with comment count
    4. List categories with their post count

??? example "Sample Solutions"
    ```sql
    -- 1. Posts with author details
    SELECT posts.*, users.username, users.email
    FROM posts
    INNER JOIN users ON posts.author_id = users.id;
    
    -- 2. Users who never posted
    SELECT users.username
    FROM users
    LEFT JOIN posts ON users.id = posts.author_id
    WHERE posts.id IS NULL;
    
    -- 3. Posts with comment count
    SELECT posts.title, COUNT(comments.id) as comments
    FROM posts
    LEFT JOIN comments ON posts.id = comments.post_id
    GROUP BY posts.id;
    
    -- 4. Categories with post count
    SELECT categories.name, COUNT(posts.id) as post_count
    FROM categories
    LEFT JOIN posts ON categories.id = posts.category_id
    GROUP BY categories.id;
    ```

---

## 4: SQL Injection and Security

**Duration:** 20-25 minutes | **Bloom's Level:** Analyse, Evaluate | **GRR:** Guided critical thinking

### What is SQL Injection?

**SQL Injection** is a code injection attack where attackers insert malicious SQL code through user input, allowing them to manipulate or access the database. It's the **#5 web application vulnerability** ([OWASP Top 10](https://owasp.org/Top10/2025/)).

!!! danger "Critical Security Vulnerability"
    SQL injection can:

    - Bypass authentication (log in without password)
    - Steal all data from database
    - Delete entire database
    - Modify data
    - Execute system commands

### How SQL Injection Works

**Vulnerable Code (NEVER DO THIS):**

```python
# User provides input
username = request.form['username']  # User types: alice
password = request.form['password']  # User types: password123

# String concatenation builds SQL query (DANGEROUS!)
query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'"

# Execute query
cursor.execute(query)
```

**Normal Use:**

- User enters: username = `alice`, password = `password123`
- Resulting query: `SELECT * FROM users WHERE username = 'alice' AND password = 'password123'`
- Works as intended ✓

**Malicious Use - Attack #1: Authentication Bypass:**

- Attacker enters: username = `admin' OR '1'='1`, password = `anything`
- Resulting query: `SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = 'anything'`
- Because `'1'='1'` is always true, query returns ALL users!
- Attacker logs in as admin without knowing password! ❌

```mermaid
sequenceDiagram
    participant A as Attacker
    participant F as Login Form
    participant S as Server
    participant D as Database
    
    A->>F: Username: admin' OR '1'='1
    F->>S: Send malicious input
    S->>D: SELECT * FROM users WHERE username='admin' OR '1'='1'
    D->>S: Returns ALL users (query is true!)
    S->>A: Welcome, Admin!
    
    Note over D: SQL injection successful!
```

**Attack #2: Database Destruction:**

- Attacker enters: username = `admin'; DROP TABLE users;--`, password = `anything`
- Resulting query becomes:
  ```sql
  SELECT * FROM users WHERE username = 'admin';
  DROP TABLE users;
  --' AND password = 'anything'
  ```
- First query: Selects admin user
- Second query: **Deletes entire users table!**
- `--` comments out rest of query
- Entire user database destroyed! ❌

**Attack #3: Data Theft:**

- Attacker enters: username = `' UNION SELECT credit_card_number FROM payments--`, password = `x`
- Resulting query:
  ```sql
  SELECT * FROM users WHERE username = '' 
  UNION SELECT credit_card_number FROM payments--'
  ```
- Steals all credit card numbers from payments table! ❌

### Real-World SQL Injection Damage

| Incident | Year | Impact | Cost |
|----------|------|--------|------|
| **TalkTalk** | 2015 | 157,000 customers' data stolen via SQL injection | £400,000 fine + £77 million total costs |
| **Heartland Payment** | 2008 | 130 million credit cards exposed | Approximately £110 million |
| **Sony Pictures** | 2011 | 1 million accounts compromised | Immeasurable reputation damage |

---

### Activity 4.1: Create Vulnerable Code

**Duration:** 10 minutes

**Objective:** Understand SQL injection by creating and attacking vulnerable code

!!! danger "Controlled Environment Only"
    This is for learning purposes only. NEVER deploy this code!

!!! note "What You'll Do"
    1. Create deliberately vulnerable login system
    2. Attack your own code with SQL injection
    3. Witness the danger firsthand
    4. Understand why this is critical

**Step 1: Create Vulnerable Login (demonstration.py)**

```python
# demonstration.py - VULNERABLE CODE FOR LEARNING ONLY
import sqlite3

def vulnerable_login(username, password):
    """DO NOT USE IN PRODUCTION - DEMONSTRATION ONLY"""
    
    conn = sqlite3.connect('demo.db')
    cursor = conn.cursor()
    
    # VULNERABLE: String concatenation
    query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'"
    
    print(f"Executing query: {query}")
    
    cursor.execute(query)
    result = cursor.fetchone()
    
    if result:
        print(f"✓ Login successful! Welcome {result[1]}")
    else:
        print("✗ Login failed")
    
    conn.close()

# Test normal login
print("\n=== Normal Login ===")
vulnerable_login("alice", "password123")

# Test SQL injection attack
print("\n=== SQL Injection Attack ===")
vulnerable_login("admin' OR '1'='1", "anything")
```

**Step 2: Run and Observe**

```bash
python demonstration.py
```

**Expected Output:**
```
=== Normal Login ===
Executing query: SELECT * FROM users WHERE username = 'alice' AND password = 'password123'
✗ Login failed

=== SQL Injection Attack ===
Executing query: SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = 'anything'
✓ Login successful! Welcome admin
```

!!! warning "Analysis Questions"
    1. Why did the attack succeed?
    2. What does `'1'='1'` mean to the database?
    3. How does the `--` comment work in attacks?
    4. What damage could this cause in a real application?

??? success "Understanding the Attack"
    - The query sees `'1'='1'` as part of the WHERE condition
    - `'1'='1'` is always TRUE in SQL
    - The OR operator means "username = 'admin'" OR "TRUE"
    - TRUE OR anything = TRUE
    - Query returns all users, attacker bypasses authentication

---

### Activity 4.2: Fix with Prepared Statements

**Duration:** 15 minutes

**Objective:** Implement proper SQL injection defence

### The Solution: Prepared Statements

A **prepared statement** (also called **parameterised query**) separates SQL code from user data.

**How It Works:**

```mermaid
graph LR
    A[SQL Template] --> B[Database Pre-compiles]
    C[User Data] --> D[Sent as Parameters]
    B --> E[Safe Execution]
    D --> E
    
    style A fill:#4caf50
    style C fill:#2196f3
    style E fill:#4caf50
```

1. SQL query written with placeholders (`?` or named parameters)
2. Database compiles query template
3. User data sent separately as parameters
4. Database treats parameters as pure data, never as SQL code

**Secure Code with Prepared Statements:**

```python
# secure_login.py - PROPER IMPLEMENTATION
import sqlite3

def secure_login(username, password):
    """SECURE: Uses prepared statements"""
    
    conn = sqlite3.connect('demo.db')
    cursor = conn.cursor()
    
    # SECURE: Prepared statement with placeholders
    query = "SELECT * FROM users WHERE username = ? AND password = ?"
    
    print(f"Query template: {query}")
    print(f"Parameters: {username}, {password}")
    
    # Execute with parameters passed separately
    cursor.execute(query, (username, password))
    result = cursor.fetchone()
    
    if result:
        print(f"✓ Login successful! Welcome {result[1]}")
    else:
        print("✗ Login failed")
    
    conn.close()

# Test normal login
print("\n=== Normal Login ===")
secure_login("alice", "password123")

# Test SQL injection attempt (now fails safely)
print("\n=== SQL Injection Attempt (Blocked) ===")
secure_login("admin' OR '1'='1", "anything")
```

**Expected Output:**
```
=== Normal Login ===
Query template: SELECT * FROM users WHERE username = ? AND password = ?
Parameters: alice, password123
✗ Login failed (correct - user doesn't exist yet)

=== SQL Injection Attempt (Blocked) ===
Query template: SELECT * FROM users WHERE username = ? AND password = ?
Parameters: admin' OR '1'='1, anything
✗ Login failed (attack blocked - treated as literal username!)
```

**Why This Works:**

| Vulnerable Code | Prepared Statement |
|----------------|-------------------|
| User input **concatenated** into SQL | User input **separated** from SQL |
| Database sees input as **code** | Database sees input as **pure data** |
| `'`, `;`, `--` have special meaning | Special characters **automatically escaped** |
| Attacker can inject commands | Attacker input treated **literally** |

!!! success "Key Principle"
    Prepared statements ensure user input is **NEVER** interpreted as SQL code, only as data values.

---

### Activity 4.3: Secure Your Application

**Duration:** 15 minutes

**Objective:** Replace all string concatenation with prepared statements

!!! note "What You'll Do"
    1. Review your [Server Side Programming](../server_side_programming_authentication_template_engines/) authentication code
    2. Identify all SQL queries
    3. Convert to prepared statements
    4. Test with malicious inputs
    5. Verify attacks now fail

**Task 1: Secure Registration**

**Before (Vulnerable):**
```python
def register(username, email, password):
    # VULNERABLE
    query = "INSERT INTO users (username, email, password_hash) VALUES ('" + username + "', '" + email + "', '" + password_hash + "')"
    cursor.execute(query)
```

**After (Secure):**
```python
def register(username, email, password):
    # Hash password first
    password_hash = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt())
    
    # SECURE: Prepared statement
    query = "INSERT INTO users (username, email, password_hash) VALUES (?, ?, ?)"
    
    try:
        cursor.execute(query, (username, email, password_hash))
        db.commit()
        return True
    except sqlite3.IntegrityError:
        return False  # Username or email already exists
```

**Task 2: Secure Login**

**Before (Vulnerable):**
```python
def login(username, password):
    query = "SELECT * FROM users WHERE username = '" + username + "'"
    cursor.execute(query)
```

**After (Secure):**
```python
def login(username, password):
    query = "SELECT id, username, password_hash FROM users WHERE username = ?"
    cursor.execute(query, (username,))
    
    user = cursor.fetchone()
    
    if user and bcrypt.checkpw(password.encode('utf-8'), user[2]):
        return {'id': user[0], 'username': user[1]}
    return None
```

**Task 3: Secure All Other Queries**

Find and fix:

- Post creation
- Post updates
- Comment insertion
- User profile queries
- Any other database operations

**Security Checklist:**

- [ ] All queries use `?` placeholders
- [ ] No string concatenation with user input
- [ ] Parameters passed as tuple to `execute()`
- [ ] Tested with malicious inputs like `' OR '1'='1`
- [ ] All attacks now fail safely

??? example "Complete Secure Example"
    ```python
    import sqlite3
    import bcrypt
    
    class SecureDatabase:
        def __init__(self, db_name):
            self.conn = sqlite3.connect(db_name)
            self.conn.row_factory = sqlite3.Row
            self.cursor = self.conn.cursor()
        
        def register_user(self, username, email, password):
            """Securely register new user"""
            password_hash = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt())
            
            query = "INSERT INTO users (username, email, password_hash) VALUES (?, ?, ?)"
            
            try:
                self.cursor.execute(query, (username, email, password_hash))
                self.conn.commit()
                return True
            except sqlite3.IntegrityError:
                return False
        
        def login_user(self, username, password):
            """Securely authenticate user"""
            query = "SELECT id, username, password_hash FROM users WHERE username = ?"
            self.cursor.execute(query, (username,))
            
            user = self.cursor.fetchone()
            
            if user and bcrypt.checkpw(password.encode('utf-8'), user['password_hash']):
                return {'id': user['id'], 'username': user['username']}
            return None
        
        def create_post(self, title, content, author_id, category_id):
            """Securely create post"""
            query = """
                INSERT INTO posts (title, content, author_id, category_id, status) 
                VALUES (?, ?, ?, ?, 'draft')
            """
            self.cursor.execute(query, (title, content, author_id, category_id))
            self.conn.commit()
            return self.cursor.lastrowid
        
        def get_user_posts(self, user_id):
            """Securely get user's posts"""
            query = """
                SELECT posts.*, users.username 
                FROM posts 
                INNER JOIN users ON posts.author_id = users.id 
                WHERE author_id = ?
                ORDER BY created_at DESC
            """
            self.cursor.execute(query, (user_id,))
            return self.cursor.fetchall()
        
        def close(self):
            self.conn.close()
    ```

**Git Checkpoint:**
```bash
git add .
git commit -m "Fix SQL injection vulnerabilities

- Replace all string concatenation with prepared statements
- Add input validation
- Test confirms attacks now fail
- All queries use parameterised statements"
```

---

## 5: Performance, Indexing & Backups

**Duration:** 20-25 minutes | **Bloom's Level:** Apply, Analyse | **GRR:** Guided application

### Database Performance and Indexing

As your database grows, query performance becomes critical. An **index** dramatically speeds up data retrieval.

### What is an Index?

Think of a database index like a book's index - instead of reading every page to find a topic, you check the index and jump directly to the right page.

```mermaid
graph TD
    A[Query: Find user with email='alice@example.com'] --> B{Index Exists?}
    B -->|No Index| C[Scan ALL Rows]
    B -->|With Index| D[Jump Directly to Row]
    
    C --> E[1,000,000 rows checked]
    D --> F[~20 checks via index tree]
    
    style C fill:#f44336
    style D fill:#4caf50
```

**Performance Comparison:**

| Operation | Without Index | With Index |
|-----------|--------------|------------|
| Find user by email in 1M users | 1,000,000 row scans | ~20 checks |
| Query time | Seconds | Milliseconds |
| Growth rate | Linear (gets slower proportionally) | Logarithmic (barely slows down) |

### When to Create Indexes

**Create indexes on columns you:**

- Search frequently (WHERE clauses)
- Sort by (ORDER BY)
- Join on (JOIN conditions)
- Use in GROUP BY

**Common index candidates:**

- Primary keys (automatically indexed)
- Foreign keys (should be indexed)
- Email addresses (frequent lookups)
- Usernames (frequent searches)
- Timestamps (for sorting/filtering)

**Don't index:**

- Small tables (< 1000 rows)
- Columns with many duplicate values
- Columns that change frequently

### Creating Indexes

```sql
-- Index on email for fast login lookups
CREATE INDEX idx_users_email ON users(email);

-- Index on foreign key for fast JOINs
CREATE INDEX idx_posts_author ON posts(author_id);

-- Index on timestamp for sorting
CREATE INDEX idx_posts_created ON posts(created_at);

-- Composite index (multiple columns)
CREATE INDEX idx_posts_status_date ON posts(status, created_at);
```

### Query Optimisation

**Bad Query (Slow):**
```sql
-- Gets all columns from all posts (inefficient)
SELECT * FROM posts;
```

**Good Query (Fast):**
```sql
-- Gets only needed columns with limit
SELECT id, title, created_at 
FROM posts 
WHERE status = 'published'
ORDER BY created_at DESC 
LIMIT 10;
```

**Use EXPLAIN to Analyse Queries:**

```sql
EXPLAIN QUERY PLAN 
SELECT * FROM users WHERE email = 'alice@example.com';

-- Without index: SCAN TABLE users
-- With index: SEARCH TABLE users USING INDEX idx_users_email
```

---

### Activity 5.1: Measure Index Performance

**Duration:** 15 minutes

**Objective:** See the dramatic performance improvement from indexing

!!! note "What You'll Do"
    1. Create large test dataset (10,000 users)
    2. Measure query time without index
    3. Create index
    4. Measure query time with index
    5. Compare performance improvement

**Step 1: Generate Test Data**

```python
# generate_test_data.py
import sqlite3
import random
import string
import time

conn = sqlite3.connect('blog_database.db')
cursor = conn.cursor()

print("Generating 10,000 test users...")
start = time.time()

for i in range(10000):
    username = ''.join(random.choices(string.ascii_lowercase, k=8))
    email = f"{username}@example.com"
    password_hash = "dummy_hash_for_testing"
    
    try:
        cursor.execute(
            "INSERT INTO users (username, email, password_hash) VALUES (?, ?, ?)",
            (username, email, password_hash)
        )
    except sqlite3.IntegrityError:
        pass  # Skip duplicates

conn.commit()
end = time.time()

print(f"Created test users in {end - start:.2f} seconds")
conn.close()
```

**Step 2: Measure Without Index**

```python
# test_performance.py
import sqlite3
import time

conn = sqlite3.connect('blog_database.db')
cursor = conn.cursor()

# Get a random email to search for
cursor.execute("SELECT email FROM users ORDER BY RANDOM() LIMIT 1")
test_email = cursor.fetchone()[0]

print(f"Searching for: {test_email}")
print("\n=== WITHOUT INDEX ===")

# Measure query time
start = time.time()
cursor.execute("SELECT * FROM users WHERE email = ?", (test_email,))
result = cursor.fetchone()
end = time.time()

print(f"Query time: {(end - start) * 1000:.2f} milliseconds")
print(f"Found: {result[1] if result else 'Not found'}")

# Check query plan
cursor.execute("EXPLAIN QUERY PLAN SELECT * FROM users WHERE email = ?")
plan = cursor.fetchall()
print(f"Query plan: {plan}")

conn.close()
```

**Step 3: Create Index**

```sql
-- Create index on email column
CREATE INDEX idx_users_email ON users(email);
```

**Step 4: Measure With Index**

```python
# test_performance.py (continued)
print("\n=== WITH INDEX ===")

# Recreate index
cursor.execute("CREATE INDEX IF NOT EXISTS idx_users_email ON users(email)")

# Measure again
start = time.time()
cursor.execute("SELECT * FROM users WHERE email = ?", (test_email,))
result = cursor.fetchone()
end = time.time()

print(f"Query time: {(end - start) * 1000:.2f} milliseconds")
print(f"Found: {result[1] if result else 'Not found'}")

# Check query plan
cursor.execute("EXPLAIN QUERY PLAN SELECT * FROM users WHERE email = ?")
plan = cursor.fetchall()
print(f"Query plan: {plan}")
```

**Expected Results:**

```
=== WITHOUT INDEX ===
Query time: 15.23 milliseconds
Query plan: SCAN TABLE users

=== WITH INDEX ===
Query time: 0.45 milliseconds
Query plan: SEARCH TABLE users USING INDEX idx_users_email

Performance improvement: 33x faster!
```

**Document Your Findings:**

| Metric | Without Index | With Index | Improvement |
|--------|--------------|------------|-------------|
| Query time | ___ ms | ___ ms | ___x faster |
| Query plan | SCAN TABLE | SEARCH USING INDEX | ✓ |
| Rows scanned | 10,000 | ~1 | ✓ |

---

### Shell Scripts for Database Backups

**Why Backups Matter:**

- Hardware failures
- Human errors (accidental deletions)
- Security breaches
- Data corruption

!!! danger "Critical Rule"
    A backup you haven't tested is not a backup at all!

### The 3-2-1 Backup Rule

- **3** copies of your data
- **2** different media types
- **1** copy offsite

### Creating Backup Scripts

**Basic Backup Script (Bash):**

```bash
#!/bin/bash
# backup_database.sh - Automated database backup

# Configuration
DB_NAME="blog_database.db"
BACKUP_DIR="./backups"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="$BACKUP_DIR/backup_$DATE.db"

# Create backup directory if needed
mkdir -p $BACKUP_DIR

# Perform backup
echo "Starting backup..."
sqlite3 $DB_NAME ".backup '$BACKUP_FILE'"

# Compress to save space
gzip $BACKUP_FILE

# Keep only last 7 days
find $BACKUP_DIR -name "backup_*.db.gz" -mtime +7 -delete

# Log completion
echo "Backup completed: ${BACKUP_FILE}.gz"
echo "$(date): Backup successful" >> $BACKUP_DIR/backup.log
```

**Make Script Executable:**
```bash
chmod +x backup_database.sh
```

**Run Backup:**
```bash
./backup_database.sh
```

---

### Activity 5.2: Create Backup System

**Duration:** 15 minutes

**Objective:** Implement automated database backups

!!! note "What You'll Do"
    1. Create backup script
    2. Test backup creation
    3. Create restore script
    4. Test restore procedure
    5. Schedule automatic backups (optional)

**Task 1: Create Backup Script**

Create `backup_database.sh`:

```bash
#!/bin/bash
# Your backup script here
# Follow the template above
```

**Task 2: Create Restore Script**

Create `restore_database.sh`:

```bash
#!/bin/bash
# restore_database.sh

BACKUP_FILE=$1

if [ -z "$BACKUP_FILE" ]; then
    echo "Usage: ./restore_database.sh <backup_file.db.gz>"
    exit 1
fi

# Decompress
gunzip -c $BACKUP_FILE > /tmp/restored.db

# Copy to working directory
cp /tmp/restored.db blog_database.db

# Clean up
rm /tmp/restored.db

echo "Database restored from $BACKUP_FILE"
```

**Task 3: Test Your Backups**

```bash
# 1. Create backup
./backup_database.sh

# 2. Make a change to database
sqlite3 blog_database.db "DELETE FROM posts WHERE id = 1"

# 3. Restore from backup
./restore_database.sh backups/backup_20250121_143022.db.gz

# 4. Verify data restored
sqlite3 blog_database.db "SELECT COUNT(*) FROM posts"
```

??? success "Success Criteria"
    - [ ] Backup script creates compressed backup files
    - [ ] Backups are timestamped
    - [ ] Old backups are automatically deleted
    - [ ] Restore script successfully recovers data
    - [ ] Tested restore procedure works
    - [ ] Backup log shows successful operations

**Optional: Schedule with Cron**
**Note:** Cron does not exist on Windows machines. A scheduled task is a similar concept on Windows.

```bash
# Edit crontab
crontab -e

# Add line to run backup daily at 2 AM
0 2 * * * /path/to/backup_database.sh
```

**Cron Schedule Format:**
```
* * * * * command
│ │ │ │ │
│ │ │ │ └─── Day of week (0-7, Sunday = 0 or 7)
│ │ │ └───── Month (1-12)
│ │ └─────── Day of month (1-31)
│ └───────── Hour (0-23)
└─────────── Minute (0-59)
```

**Git Checkpoint:**
```bash
git add backup_database.sh restore_database.sh
git commit -m "Add database backup and restore scripts

- Automated backup with timestamp
- Compression to save space
- Cleanup old backups (7 day retention)
- Restore script for recovery
- Backup logging"
```

# Part 6: Big Data Concepts & Database Management (20 minutes)

## Big Data Concepts (Introduction)

### What is Big Data?

Big data refers to datasets so large or complex that traditional database tools struggle to handle them efficiently. For web applications, this means planning for scale from the beginning.

```mermaid
flowchart LR
    A[Small Data] -->|Growth| B[Medium Data]
    B -->|Growth| C[Big Data]
    
    A --> A1[100s of records]
    A --> A2[Single server]
    A --> A3[Simple queries]
    
    B --> B1[1000s-100,000s records]
    B --> B2[Needs optimisation]
    B --> B3[Requires indexing]
    
    C --> C1[Millions+ records]
    C --> C2[Distributed systems]
    C --> C3[Specialised tools]
    
    style A fill:#9f9,stroke:#333
    style B fill:#ffd93d,stroke:#333
    style C fill:#ff6b6b,stroke:#333
```

### Big Data Terminology

| Term | Definition | Example in Web Context |
|------|------------|------------------------|
| **Metadata** | Data about data - information describing other data | User profile has metadata: `account_created_date`, `last_login`, `file_upload_date` |
| **Data Mining** | Process of discovering patterns in large datasets | Analysing millions of user behaviours to recommend products or content |
| **Scalability** | Ability to handle growing amounts of data and users | Blog with 100 users vs 100 million users requires different architecture |
| **Query Optimisation** | Making database queries run faster and more efficiently | Bad query scans entire table; optimised query uses indexes |
| **Sharding** | Splitting data across multiple database servers | Users A-M on server 1, N-Z on server 2 |
| **Replication** | Creating copies of database for redundancy and performance | Master database writes, multiple read replicas for queries |

### Scalability Considerations

As your web application grows, database performance becomes critical:

```mermaid
flowchart LR
    A[Application Growth] --> B{User Scale}
    
    B -->|100s users| C[Small Scale]
    B -->|1000s users| D[Medium Scale]
    B -->|Millions users| E[Large Scale]
    
    C --> C1[Single DB Server]
    C --> C2[Simple Queries]
    C --> C3[Basic Backups]
    
    D --> D1[Indexes Required]
    D --> D2[Connection Pooling]
    D --> D3[Query Optimisation]
    
    E --> E1[Database Replication]
    E --> E2[Sharding]
    E --> E3[Caching Layers]
    E --> E4[Load Balancing]
    
    style A fill:#9f9,stroke:#333
    style B fill:#ffd93d,stroke:#333
    style C fill:#4d96ff,stroke:#333
    style D fill:#4d96ff,stroke:#333
    style E fill:#4d96ff,stroke:#333
```

**Small Scale (Hundreds of Users):**

* Single database server sufficient
* Simple queries work fine
* Backups are quick (minutes)
* No special optimisation needed
* Example: Personal blog, small business website

**Medium Scale (Thousands of Users):**

* Need indexes on frequently queried columns
* Connection pooling becomes important
* Regular database maintenance required
* Backup strategies more complex (may take hours)
* Example: Regional e-commerce site, university portal

**Large Scale (Millions of Users):**

* Database replication (multiple copies across servers)
* Sharding (splitting data across multiple databases)
* Caching layers (Redis, Memcached) to reduce database load
* Load balancing across multiple servers
* Specialised big data tools (Hadoop, Spark)
* Example: Facebook, Amazon, Netflix

---

## Data Mining in Web Applications

### What is Data Mining?

Data mining is the process of discovering patterns, trends, and useful information from large datasets. In web applications, this helps make data-driven decisions.

```mermaid
flowchart TD
    A[/Raw User Data/] --> B[Data Collection]
    B --> C[Data Processing]
    C --> D[Pattern Discovery]
    D --> E[Actionable Insights]
    
    E --> F[Business Decisions]
    E --> G[User Experience Improvements]
    E --> H[Product Recommendations]
    
    style A fill:#9f9,stroke:#333
    style B fill:#4d96ff,stroke:#333
    style C fill:#4d96ff,stroke:#333
    style D fill:#4d96ff,stroke:#333
    style E fill:#4d96ff,stroke:#333
    style F fill:#9f9,stroke:#333
    style G fill:#9f9,stroke:#333
    style H fill:#9f9,stroke:#333
```

### Common Data Mining Applications

**1. User Behaviour Analysis**

Understanding how users interact with your application:

```python
def analyse_user_activity():
    """Find patterns in user activity"""
    query = """
        SELECT 
            strftime('%H', created_at) as hour_of_day,
            COUNT(*) as post_count
        FROM posts
        GROUP BY hour_of_day
        ORDER BY hour_of_day
    """
    results = query_db(query)
    
    # Discover: Most posts are created between 18:00-22:00
    # Insight: Schedule maintenance during low-activity hours (03:00-05:00)
    return results
```

**2. Content Popularity Analysis**

Identifying trending topics and popular content:

```python
def find_trending_topics():
    """Discover what content engages users most"""
    query = """
        SELECT 
            posts.title,
            COUNT(comments.comment_id) as engagement,
            AVG(LENGTH(comments.content)) as avg_comment_length
        FROM posts
        LEFT JOIN comments ON posts.post_id = comments.post_id
        WHERE posts.created_at >= date('now', '-7 days')
        GROUP BY posts.post_id
        HAVING engagement > 5
        ORDER BY engagement DESC
        LIMIT 10
    """
    results = query_db(query)
    
    # Insight: Posts about Python tutorials get 3x more engagement
    # Decision: Create more Python content
    return results
```

**3. User Segmentation**

Grouping users by behaviour patterns:

```python
def segment_users():
    """Categorise users by activity level"""
    query = """
        SELECT 
            users.user_id,
            users.username,
            COUNT(DISTINCT posts.post_id) as posts_created,
            COUNT(DISTINCT comments.comment_id) as comments_made,
            CASE
                WHEN COUNT(DISTINCT posts.post_id) > 10 THEN 'Power User'
                WHEN COUNT(DISTINCT posts.post_id) > 5 THEN 'Active User'
                WHEN COUNT(DISTINCT posts.post_id) > 0 THEN 'Casual User'
                ELSE 'Lurker'
            END as user_segment
        FROM users
        LEFT JOIN posts ON users.user_id = posts.user_id
        LEFT JOIN comments ON users.user_id = comments.user_id
        GROUP BY users.user_id
    """
    results = query_db(query)
    
    # Insight: 80% of content comes from 20% of users (Pareto Principle)
    # Decision: Create incentives for casual users to post more
    return results
```

**4. Correlation Analysis**

Finding relationships between different metrics:

```python
def analyse_engagement_correlation():
    """Does post length correlate with engagement?"""
    query = """
        SELECT 
            LENGTH(posts.content) as content_length,
            COUNT(comments.comment_id) as comment_count
        FROM posts
        LEFT JOIN comments ON posts.post_id = comments.post_id
        GROUP BY posts.post_id
        HAVING content_length > 0
    """
    results = query_db(query)
    
    # Insight: Posts between 300-800 characters get most comments
    # Decision: Suggest optimal post length to users
    return results
```

### Privacy and Ethical Considerations

!!! warning "Data Mining Ethics"
    When mining user data, you must:
    
    * **Obtain consent:** Users should know their data is being analysed
    * **Respect privacy:** Anonymise personal information
    * **Comply with regulations:** GDPR, CCPA (covered in Week 11)
    * **Be transparent:** Explain how insights are used
    * **Provide opt-out:** Allow users to exclude their data
    
    **Example of anonymisation:**
    ```python
    # ❌ Bad: Exposes personal information
    query = "SELECT username, email, browsing_history FROM users"
    
    # ✅ Good: Aggregated and anonymised
    query = """
        SELECT 
            strftime('%H', last_login) as hour,
            COUNT(*) as user_count
        FROM users
        GROUP BY hour
    """
    ```

---

## Metadata Management

### Understanding Metadata

**Metadata** is "data about data" - information that describes, explains, or makes it easier to find and use other data.

**Types of Metadata:**

1. **Descriptive:** What the data is (title, author, description)
2. **Structural:** How data is organised (file format, table schema)
3. **Administrative:** When, who, how (creation date, permissions, version)

### Metadata in Database Design

```mermaid
flowchart LR
    A[Core Data] --> B[Actual Content]
    A --> C[Metadata]
    
    B --> B1[Post text]
    B --> B2[Comment content]
    B --> B3[User message]
    
    C --> C1[When created]
    C --> C2[Who created it]
    C --> C3[File size/type]
    C --> C4[Last modified]
    C --> C5[Access count]
    
    style A fill:#9370DB,stroke:#333
    style B fill:#4d96ff,stroke:#333
    style C fill:#4d96ff,stroke:#333
```

### Practical Example: File Upload System

```sql
CREATE TABLE uploaded_files (
    file_id INTEGER PRIMARY KEY AUTOINCREMENT,
    
    -- Core data
    file_path TEXT NOT NULL,           -- Where file is stored
    
    -- Descriptive metadata
    filename TEXT NOT NULL,             -- Original filename
    file_type TEXT NOT NULL,            -- MIME type (image/jpeg, application/pdf)
    file_size INTEGER NOT NULL,         -- Size in bytes
    description TEXT,                   -- User-provided description
    
    -- Administrative metadata
    uploaded_by INTEGER NOT NULL,       -- User who uploaded
    uploaded_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    last_modified DATETIME,             -- When file was last changed
    last_accessed DATETIME,             -- When file was last viewed
    
    -- Usage metadata
    download_count INTEGER DEFAULT 0,   -- Popularity tracking
    is_public BOOLEAN DEFAULT 0,        -- Privacy setting
    
    -- Technical metadata
    file_hash TEXT UNIQUE,              -- SHA-256 hash for duplicate detection
    thumbnail_path TEXT,                -- Preview image location
    
    FOREIGN KEY (uploaded_by) REFERENCES users(user_id)
);
```

### Benefits of Good Metadata

**1. Duplicate Detection**

```python
def check_duplicate_file(file_hash):
    """Prevent users uploading the same file twice"""
    query = "SELECT file_id, filename FROM uploaded_files WHERE file_hash = ?"
    existing = query_db(query, (file_hash,), one=True)
    
    if existing:
        return f"File already exists as '{existing['filename']}'"
    return None
```

**2. Storage Management**

```python
def get_user_storage_usage(user_id):
    """Calculate total storage used by user"""
    query = """
        SELECT 
            uploaded_by,
            COUNT(*) as file_count,
            SUM(file_size) as total_bytes,
            ROUND(SUM(file_size) / 1024.0 / 1024.0, 2) as total_mb
        FROM uploaded_files
        WHERE uploaded_by = ?
        GROUP BY uploaded_by
    """
    return query_db(query, (user_id,), one=True)
```

**3. Cleanup of Old Data**

```python
def find_unused_files(days_inactive=90):
    """Find files that haven't been accessed recently"""
    query = """
        SELECT file_id, filename, file_size, last_accessed
        FROM uploaded_files
        WHERE last_accessed < date('now', '-' || ? || ' days')
        OR last_accessed IS NULL
        ORDER BY file_size DESC
    """
    return query_db(query, (days_inactive,))
```

**4. Popular Content Identification**

```python
def get_most_downloaded_files():
    """Find most popular files"""
    query = """
        SELECT 
            filename,
            file_type,
            download_count,
            uploaded_at
        FROM uploaded_files
        WHERE is_public = 1
        ORDER BY download_count DESC
        LIMIT 20
    """
    return query_db(query)
```

### Metadata for API Responses

Metadata improves API usability:

```python
@app.route('/api/posts')
def api_get_posts():
    """API endpoint with metadata"""
    page = request.args.get('page', 1, type=int)
    per_page = 10
    offset = (page - 1) * per_page
    
    # Get posts
    posts = query_db(
        'SELECT * FROM posts ORDER BY created_at DESC LIMIT ? OFFSET ?',
        (per_page, offset)
    )
    
    # Get total count for metadata
    total = query_db('SELECT COUNT(*) as count FROM posts', one=True)['count']
    
    # Response includes metadata
    return jsonify({
        'data': [dict(post) for post in posts],
        'metadata': {
            'page': page,
            'per_page': per_page,
            'total_records': total,
            'total_pages': (total + per_page - 1) // per_page,
            'has_next': offset + per_page < total,
            'has_previous': page > 1,
            'timestamp': datetime.now().isoformat()
        }
    })
```

---

## Advanced Indexing Concepts

### How Indexes Work

Indexes are like a book's index - they create a sorted lookup structure that allows quick data retrieval without scanning every row.

```mermaid
flowchart TD
    A[Query: Find user 'charlie'] --> B{Index on username?}
    
    B -->|No Index| C[Full Table Scan]
    C --> C1[Read row 1: alice]
    C1 --> C2[Read row 2: bob]
    C2 --> C3[Read row 3: charlie ✓]
    C3 --> C4[Read row 4: david]
    C4 --> C5[Read row 5: eve]
    C5 --> D[/Found after 5 reads/]
    
    B -->|With Index| E[Index Lookup]
    E --> E1[B-tree search]
    E1 --> E2[Found in 2 comparisons]
    E2 --> E3[Jump directly to row 3]
    E3 --> F[/Found after 1 read/]
    
    style A fill:#9f9,stroke:#333
    style B fill:#ffd93d,stroke:#333
    style C fill:#ff6b6b,stroke:#333
    style E fill:#4d96ff,stroke:#333
    style D fill:#ff6b6b,stroke:#333
    style F fill:#9f9,stroke:#333
```

### B-Tree Index Structure (Simplified)

Databases typically use B-tree indexes:

```
                     [H]
                   /       \
               [D]            [M]
             /     \       /        \
        [A,B,C]   [E,F,G] [I,J,K,L] [N,O,P]
```

Finding 'K' requires only 3 comparisons instead of scanning all letters.

### Measuring Index Performance

```python
def demonstrate_index_performance():
    """Show difference between indexed and non-indexed queries"""
    import time
    
    # Query WITHOUT index
    start = time.time()
    result = query_db("SELECT * FROM posts WHERE title LIKE '%Python%'")
    without_index = time.time() - start
    
    # Create index
    execute_db("CREATE INDEX IF NOT EXISTS idx_posts_title ON posts(title)")
    
    # Query WITH index
    start = time.time()
    result = query_db("SELECT * FROM posts WHERE title LIKE '%Python%'")
    with_index = time.time() - start
    
    print(f"Without index: {without_index*1000:.2f}ms")
    print(f"With index: {with_index*1000:.2f}ms")
    print(f"Improvement: {(without_index/with_index):.1f}x faster")
```

### Query Execution Plans

Use `EXPLAIN QUERY PLAN` to see how SQLite executes queries:

```python
def analyse_query_plan():
    """Check if query uses indexes"""
    query = "SELECT * FROM users WHERE username = 'alice'"
    
    # Get execution plan
    plan = query_db(f"EXPLAIN QUERY PLAN {query}")
    
    for step in plan:
        print(dict(step))
    
    # Without index: SCAN TABLE users
    # With index: SEARCH TABLE users USING INDEX idx_users_username
```

### Composite Indexes

Indexes on multiple columns for complex queries:

```sql
-- Composite index on user_id and created_at
CREATE INDEX idx_posts_user_date ON posts(user_id, created_at);

-- This query benefits from composite index
SELECT * FROM posts 
WHERE user_id = 5 
ORDER BY created_at DESC;
```

**Column Order Matters:**

```sql
-- ✅ Good: Index can be used for both conditions
CREATE INDEX idx_posts_user_date ON posts(user_id, created_at);
SELECT * FROM posts WHERE user_id = 5 AND created_at > '2025-01-01';

-- ❌ Less optimal: Index only helps with created_at
CREATE INDEX idx_posts_date_user ON posts(created_at, user_id);
SELECT * FROM posts WHERE user_id = 5;  -- Can't use index efficiently
```

**Rule of thumb:** Put the most selective (unique) column first, and columns used in equality tests before range tests.

### Index Trade-offs

```mermaid
flowchart LR
    A[Add Index] --> B[Benefits]
    A --> C[Costs]
    
    B --> B1[Faster SELECT]
    B --> B2[Faster WHERE]
    B --> B3[Faster JOIN]
    B --> B4[Faster ORDER BY]
    
    C --> C1[Slower INSERT]
    C --> C2[Slower UPDATE]
    C --> C3[Slower DELETE]
    C --> C4[More disk space]
    
    style A fill:#9370DB,stroke:#333
    style B fill:#9f9,stroke:#333
    style C fill:#ff6b6b,stroke:#333
```

**When indexes hurt performance:**

```python
# If you have index on 'status' column
# But status only has values: 'active', 'inactive'
# Index doesn't help much because:
# - Low cardinality (only 2 unique values)
# - Database still needs to read ~50% of rows
# - Index maintenance overhead not worth it

# Better: Don't index low-cardinality columns
```

---

## Shell Scripts for Database Management

### Why Shell Scripts?

Shell scripts automate repetitive database administration tasks. Instead of manually running backup commands daily, create a script that runs automatically.

**Common Database Shell Script Uses:**

* Automated backups
* Database restoration
* Data export/import
* Cleanup of old data
* Database health monitoring
* Log rotation
* Performance reporting

### Advanced Backup Script with Logging

Create `backup_advanced.sh`:

```bash
#!/bin/bash

# Advanced database backup script with logging and error handling

# Configuration
DB_FILE="myapp.db"
BACKUP_DIR="backups"
LOG_DIR="logs"
MAX_BACKUPS=7
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="${BACKUP_DIR}/myapp_${DATE}.db"
LOG_FILE="${LOG_DIR}/backup_${DATE}.log"

# Colours for output
GREEN='\033[0;32m'
RED='\033[0;31m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Colour

# Function to log messages
log_message() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

# Function to log errors
log_error() {
    echo -e "${RED}[$(date '+%Y-%m-%d %H:%M:%S')] ERROR: $1${NC}" | tee -a "$LOG_FILE"
}

# Function to log success
log_success() {
    echo -e "${GREEN}[$(date '+%Y-%m-%d %H:%M:%S')] SUCCESS: $1${NC}" | tee -a "$LOG_FILE"
}

# Create directories if they don't exist
mkdir -p "$BACKUP_DIR" "$LOG_DIR"

log_message "Starting database backup..."

# Check if database file exists
if [ ! -f "$DB_FILE" ]; then
    log_error "Database file $DB_FILE not found!"
    exit 1
fi

# Check database integrity before backup
log_message "Checking database integrity..."
sqlite3 "$DB_FILE" "PRAGMA integrity_check;" > /dev/null 2>&1

if [ $? -eq 0 ]; then
    log_success "Database integrity check passed"
else
    log_error "Database integrity check failed!"
    exit 1
fi

# Create backup
log_message "Creating backup: $BACKUP_FILE"
cp "$DB_FILE" "$BACKUP_FILE"

if [ $? -eq 0 ]; then
    # Get file size
    SIZE=$(du -h "$BACKUP_FILE" | cut -f1)
    log_success "Backup created successfully (Size: $SIZE)"
    
    # Compress backup
    log_message "Compressing backup..."
    gzip "$BACKUP_FILE"
    
    if [ $? -eq 0 ]; then
        COMPRESSED_SIZE=$(du -h "${BACKUP_FILE}.gz" | cut -f1)
        log_success "Backup compressed (Size: $COMPRESSED_SIZE)"
    else
        log_error "Compression failed"
    fi
    
    # Clean up old backups
    log_message "Cleaning up old backups (keeping ${MAX_BACKUPS} most recent)..."
    DELETED=0
    for OLD_BACKUP in $(ls -t ${BACKUP_DIR}/myapp_*.db.gz 2>/dev/null | tail -n +$((MAX_BACKUPS + 1))); do
        rm -f "$OLD_BACKUP"
        log_message "Deleted old backup: $(basename $OLD_BACKUP)"
        DELETED=$((DELETED + 1))
    done
    
    if [ $DELETED -gt 0 ]; then
        log_success "Deleted $DELETED old backup(s)"
    else
        log_message "No old backups to delete"
    fi
    
    # Summary
    log_success "Backup completed successfully!"
    echo -e "${GREEN}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    echo -e "${GREEN}Backup Summary:${NC}"
    echo -e "  Location: ${BACKUP_FILE}.gz"
    echo -e "  Size: $COMPRESSED_SIZE"
    echo -e "  Log: $LOG_FILE"
    echo -e "${GREEN}━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━${NC}"
    
else
    log_error "Backup failed!"
    exit 1
fi
```

Make executable:
```bash
chmod +x backup_advanced.sh
```

### Database Restoration Script

Create `restore.sh`:

```bash
#!/bin/bash

# Database restoration script

BACKUP_DIR="backups"
DB_FILE="myapp.db"

echo "Available backups:"
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
ls -lht "${BACKUP_DIR}"/myapp_*.db.gz | nl
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"

read -p "Enter backup number to restore (or 'q' to quit): " BACKUP_NUM

if [ "$BACKUP_NUM" = "q" ]; then
    echo "Restoration cancelled"
    exit 0
fi

# Get the selected backup file
BACKUP_FILE=$(ls -t "${BACKUP_DIR}"/myapp_*.db.gz | sed -n "${BACKUP_NUM}p")

if [ -z "$BACKUP_FILE" ]; then
    echo "❌ Invalid backup number"
    exit 1
fi

echo "Selected backup: $BACKUP_FILE"
read -p "⚠️  This will overwrite the current database. Continue? (yes/no): " CONFIRM

if [ "$CONFIRM" != "yes" ]; then
    echo "Restoration cancelled"
    exit 0
fi

# Create safety backup of current database
if [ -f "$DB_FILE" ]; then
    SAFETY_BACKUP="${DB_FILE}.before_restore_$(date +%Y%m%d_%H%M%S)"
    cp "$DB_FILE" "$SAFETY_BACKUP"
    echo "✅ Current database backed up to: $SAFETY_BACKUP"
fi

# Decompress and restore
echo "Restoring database..."
gunzip -c "$BACKUP_FILE" > "$DB_FILE"

if [ $? -eq 0 ]; then
    # Verify restored database
    sqlite3 "$DB_FILE" "PRAGMA integrity_check;" > /dev/null 2>&1
    
    if [ $? -eq 0 ]; then
        echo "✅ Database restored successfully!"
        echo "✅ Integrity check passed"
    else
        echo "❌ Restored database failed integrity check!"
        echo "Restoring safety backup..."
        cp "$SAFETY_BACKUP" "$DB_FILE"
        exit 1
    fi
else
    echo "❌ Restoration failed!"
    exit 1
fi
```

Make executable:
```bash
chmod +x restore.sh
```

### Database Health Check Script

Create `health_check.py`:

```python
#!/usr/bin/env python3
"""
Database health check script
Monitors database size, performance, and integrity
"""

import sqlite3
import os
from datetime import datetime

DB_FILE = 'myapp.db'

def format_size(bytes):
    """Convert bytes to human-readable format"""
    for unit in ['B', 'KB', 'MB', 'GB']:
        if bytes < 1024.0:
            return f"{bytes:.2f} {unit}"
        bytes /= 1024.0
    return f"{bytes:.2f} TB"

def check_database_health():
    """Perform comprehensive database health check"""
    print("=" * 50)
    print("DATABASE HEALTH CHECK")
    print(f"Time: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    print("=" * 50)
    
    # Check file exists
    if not os.path.exists(DB_FILE):
        print(f"❌ Database file '{DB_FILE}' not found!")
        return False
    
    # File size
    file_size = os.path.getsize(DB_FILE)
    print(f"\n📊 Database Size: {format_size(file_size)}")
    
    try:
        conn = sqlite3.connect(DB_FILE)
        cursor = conn.cursor()
        
        # Integrity check
        print("\n🔍 Running integrity check...")
        cursor.execute("PRAGMA integrity_check")
        result = cursor.fetchone()[0]
        
        if result == "ok":
            print("✅ Integrity check: PASSED")
        else:
            print(f"❌ Integrity check: FAILED - {result}")
            return False
        
        # Table statistics
        print("\n📈 Table Statistics:")
        cursor.execute("""
            SELECT name FROM sqlite_master 
            WHERE type='table' AND name NOT LIKE 'sqlite_%'
        """)
        tables = cursor.fetchall()
        
        for (table_name,) in tables:
            cursor.execute(f"SELECT COUNT(*) FROM {table_name}")
            count = cursor.fetchone()[0]
            print(f"  • {table_name}: {count:,} records")
        
        # Index usage
        print("\n🔎 Indexes:")
        cursor.execute("""
            SELECT name, tbl_name FROM sqlite_master 
            WHERE type='index' AND name NOT LIKE 'sqlite_%'
        """)
        indexes = cursor.fetchall()
        
        if indexes:
            for index_name, table_name in indexes:
                print(f"  • {index_name} on {table_name}")
        else:
            print("  ⚠️  No custom indexes found")
        
        # Recent activity
        print("\n📅 Recent Activity:")
        cursor.execute("""
            SELECT COUNT(*) FROM users 
            WHERE created_at >= date('now', '-7 days')
        """)
        new_users = cursor.fetchone()[0]
        print(f"  • New users (last 7 days): {new_users}")
        
        cursor.execute("""
            SELECT COUNT(*) FROM posts 
            WHERE created_at >= date('now', '-7 days')
        """)
        new_posts = cursor.fetchone()[0]
        print(f"  • New posts (last 7 days): {new_posts}")
        
        # Database settings
        print("\n⚙️  Database Settings:")
        cursor.execute("PRAGMA page_size")
        page_size = cursor.fetchone()[0]
        print(f"  • Page size: {page_size} bytes")
        
        cursor.execute("PRAGMA page_count")
        page_count = cursor.fetchone()[0]
        print(f"  • Page count: {page_count:,}")
        
        # Fragmentation
        cursor.execute("PRAGMA freelist_count")
        freelist = cursor.fetchone()[0]
        fragmentation = (freelist / page_count * 100) if page_count > 0 else 0
        print(f"  • Fragmentation: {fragmentation:.2f}%")
        
        if fragmentation > 20:
            print("  ⚠️  Consider running VACUUM to reduce fragmentation")
        
        conn.close()
        
        print("\n" + "=" * 50)
        print("✅ Health check completed successfully")
        print("=" * 50)
        
        return True
        
    except Exception as e:
        print(f"\n❌ Error during health check: {e}")
        return False

if __name__ == '__main__':
    check_database_health()
```

Make executable:
```bash
chmod +x health_check.py
```

Run:
```bash
python health_check.py
```

---

## Practical Activity 6.1: Big Data Analysis (15 minutes)

**Task:** Implement data mining queries to analyse your blog data.

1. Create `data_analysis.py`:

```python
# data_analysis.py
from db_config import query_db
from datetime import datetime

def analyse_user_engagement():
    """Analyse user engagement patterns"""
    print("=" * 60)
    print("USER ENGAGEMENT ANALYSIS")
    print("=" * 60)
    
    # Most active users
    print("\n📊 Most Active Users:")
    query = """
        SELECT 
            users.username,
            COUNT(DISTINCT posts.post_id) as posts,
            COUNT(DISTINCT comments.comment_id) as comments,
            (COUNT(DISTINCT posts.post_id) + COUNT(DISTINCT comments.comment_id)) as total_activity
        FROM users
        LEFT JOIN posts ON users.user_id = posts.user_id
        LEFT JOIN comments ON users.user_id = comments.user_id
        GROUP BY users.user_id
        HAVING total_activity > 0
        ORDER BY total_activity DESC
        LIMIT 5
    """
    results = query_db(query)
    
    for user in results:
        print(f"  • {user['username']}: {user['posts']} posts, {user['comments']} comments")
    
    # Activity by hour
    print("\n⏰ Activity by Hour of Day:")
    query = """
        SELECT 
            strftime('%H', created_at) as hour,
            COUNT(*) as activity_count
        FROM (
            SELECT created_at FROM posts
            UNION ALL
            SELECT created_at FROM comments
        )
        GROUP BY hour
        ORDER BY hour
    """
    results = query_db(query)
    
    for row in results:
        bar = '█' * (row['activity_count'] // 2)
        print(f"  {row['hour']}:00 {bar} {row['activity_count']}")
    
    # Popular content
    print("\n🔥 Most Commented Posts:")
    query = """
        SELECT 
            posts.title,
            users.username as author,
            COUNT(comments.comment_id) as comment_count
        FROM posts
        INNER JOIN users ON posts.user_id = users.user_id
        LEFT JOIN comments ON posts.post_id = comments.post_id
        GROUP BY posts.post_id
        HAVING comment_count > 0
        ORDER BY comment_count DESC
        LIMIT 5
    """
    results = query_db(query)
    
    for post in results:
        print(f"  • '{post['title']}' by {post['author']}: {post['comment_count']} comments")

def analyse_metadata():
    """Analyse metadata patterns"""
    print("\n" + "=" * 60)
    print("METADATA ANALYSIS")
    print("=" * 60)
    
    # Account age distribution
    print("\n📅 User Account Age Distribution:")
    query = """
        SELECT 
            CASE
                WHEN julianday('now') - julianday(created_at) < 7 THEN 'Less than 1 week'
                WHEN julianday('now') - julianday(created_at) < 30 THEN '1-4 weeks'
                WHEN julianday('now') - julianday(created_at) < 90 THEN '1-3 months'
                ELSE 'Over 3 months'
            END as account_age,
            COUNT(*) as user_count
        FROM users
        GROUP BY account_age
    """
    results = query_db(query)
    
    for row in results:
        print(f"  • {row['account_age']}: {row['user_count']} users")
    
    # Content length analysis
    print("\n📏 Post Length Analysis:")
    query = """
        SELECT 
            CASE
                WHEN LENGTH(content) < 100 THEN 'Short (< 100 chars)'
                WHEN LENGTH(content) < 500 THEN 'Medium (100-500 chars)'
                ELSE 'Long (> 500 chars)'
            END as post_length,
            COUNT(*) as post_count,
            AVG(LENGTH(content)) as avg_length
        FROM posts
        GROUP BY post_length
    """
    results = query_db(query)
    
    for row in results:
        print(f"  • {row['post_length']}: {row['post_count']} posts (avg: {row['avg_length']:.0f} chars)")

if __name__ == '__main__':
    analyse_user_engagement()
    analyse_metadata()
```

2. Populate test data for analysis:

```python
# populate_test_data.py
from db_config import execute_db
from werkzeug.security import generate_password_hash
import random

# Create test users
usernames = ['alice', 'bob', 'charlie', 'diana', 'eve']
for username in usernames:
    try:
        execute_db(
            'INSERT INTO users (username, email, password_hash) VALUES (?, ?, ?)',
            (username, f'{username}@example.com', generate_password_hash('password123'))
        )
    except:
        pass  # User may already exist

# Create test posts
post_titles = [
    'Getting Started with Python',
    'Web Development Best Practices',
    'Database Design Patterns',
    'Understanding SQL Injection',
    'Building Secure Applications'
]

post_contents = [
    'Short post.',
    'This is a medium-length post with some interesting content about web development.' * 3,
    'This is a longer post with extensive detail about database design and normalisation principles.' * 10
]

for i in range(20):
    user_id = random.randint(1, 5)
    title = random.choice(post_titles) + f" #{i}"
    content = random.choice(post_contents)
    
    execute_db(
        'INSERT INTO posts (user_id, title, content) VALUES (?, ?, ?)',
        (user_id, title, content)
    )

# Create test comments
for i in range(50):
    user_id = random.randint(1, 5)
    post_id = random.randint(1, 20)
    content = f'Great post! This is comment number {i}.'
    
    try:
        execute_db(
            'INSERT INTO comments (user_id, post_id, content) VALUES (?, ?, ?)',
            (user_id, post_id, content)
        )
    except:
        pass  # Post may not exist

print('✅ Test data populated successfully!')
```

3. Run analysis:
```bash
python populate_test_data.py
python data_analysis.py
```

4. **Git commit:** "Add data mining analysis tools"

!!! success "Checkpoint"
    You should see:
    
    * User engagement statistics
    * Activity patterns by hour
    * Popular content identification
    * Metadata insights about post lengths and account ages

---

## Summary & Key Takeaways

### What You've Learned

✅ **Big Data Concepts:** Understanding scalability challenges and solutions

✅ **Data Mining:** Extracting insights from user behaviour and content patterns

✅ **Metadata Management:** Using "data about data" to improve system functionality

✅ **Advanced Indexing:** How indexes work and when to use them

✅ **Database Administration:** Automated backups, restoration, and health monitoring

### Practical Skills Acquired

* Writing data mining queries for business intelligence
* Implementing metadata tracking for files and content
* Creating comprehensive backup and restoration scripts
* Monitoring database health and performance
* Understanding trade-offs in database design for scale

!!! info "Teacher Notes: Part 6"    
    **Formative Assessment:**
    
    * Can students explain the difference between data and metadata?
    * Can they identify when a query would benefit from an index?
    * Do they understand privacy implications of data mining?
    * Can they interpret data mining results to make decisions?

---

## Syllabus Alignment Summary

!!! success "Programming for the Web - 100% Coverage"
    ✅ Model elements that form a web development system (databases)  
    ✅ Observe and describe back-end process (database operations)  
    ✅ Shell scripts (backup automation)  
    ✅ SQL queries (SELECT, INSERT, UPDATE, DELETE, GROUP BY, WHERE, JOINs)  
    ✅ Big data concepts (indexing, metadata, data mining introduction)

!!! success "Secure Software Architecture - 100% Coverage"
    ✅ Security concepts applied to data (confidentiality, integrity, availability)  
    ✅ Defensive input handling (preventing SQL injection)  
    ✅ Security features for data protection (prepared statements, least privilege)

---

## Student Self-Assessment Checklist

Use this checklist to verify you've mastered all content:

### Database Fundamentals
- [ ] I can explain the difference between SQL and NoSQL databases
- [ ] I understand what CRUD operations are and can identify them
- [ ] I can explain what primary keys and foreign keys are
- [ ] I can describe database normalisation and why it matters
- [ ] I can securely configure database connections using environment variables

### SQL Queries
- [ ] I can write INSERT statements to create new records
- [ ] I can write SELECT statements with WHERE, ORDER BY, and LIMIT
- [ ] I can use aggregate functions (COUNT, SUM, AVG, MIN, MAX)
- [ ] I can use GROUP BY to analyse data
- [ ] I can write UPDATE statements (with WHERE clause!)
- [ ] I can write DELETE statements (with WHERE clause!)
- [ ] I can perform INNER JOIN to combine tables
- [ ] I can perform LEFT JOIN to show all records from one table

### Security
- [ ] I can explain what SQL injection is and why it's dangerous
- [ ] I can identify vulnerable code that uses string concatenation
- [ ] I can write queries using prepared statements (parameterised queries)
- [ ] I can test my code against SQL injection attacks
- [ ] I understand defence in depth (multiple security layers)

### Performance & Operations
- [ ] I can explain what database indexes are and why they improve performance
- [ ] I can create indexes on appropriate columns
- [ ] I can use EXPLAIN to analyse query performance
- [ ] I can write shell scripts to backup databases
- [ ] I can restore databases from backups
- [ ] I understand the 3-2-1 backup rule

### Integration
- [ ] I have integrated my Week 7 authentication with the database
- [ ] All my queries use prepared statements
- [ ] My data persists across server restarts
- [ ] I have tested my application's security
- [ ] My Git history shows clear, meaningful commits

!!! tip "Self-Assessment Score"
    - **All checked:** Excellent! You're ready for Week 9
    - **80%+ checked:** Good progress, review unchecked items
    - **60-80% checked:** Review content parts with gaps
    - **<60% checked:** Revisit lesson, complete all activities

---

## Teacher Notes

??? note "Differentiation Strategies"

    **For Students Who Need Support:**

    1. **Simplified Schema:** Start with just two tables (users and posts) instead of four
    2. **Visual Tools:** Use DB Browser for SQLite GUI instead of command-line only
    3. **Pre-written Queries:** Provide SQL query templates with blanks to fill in
    4. **Paired Programming:** Partner stronger students with those needing support for Activities 4 and 5
    5. **Extended Time:** Allow 150 minutes instead of 120 for completion
    6. **Video Walkthroughs:** Provide recorded demonstrations of complex topics (JOINs, prepared statements)
    7. Focus on basic data mining queries and simple backup scripts

    **For Advanced Students:**

    1. **Advanced Queries:** Challenge with complex multi-table JOINs and subqueries
    2. **ORM Preview:** Introduce SQLAlchemy or similar ORM as extension
    3. **Performance Optimisation:** Profile queries, optimise slow queries, create covering indexes
    4. **Database Security:** Research and implement row-level security
    5. **Migration System:** Create database migration system from scratch
    6. **Peer Teaching:** Have them help struggling classmates during activities
    7. **Real-World Challenge:** Design schema for complex system (e.g., e-commerce with orders, products, inventory)
    8. Explore machine learning applications, implement predictive analytics, create distributed database simulations

??? note "Common Misconceptions"

    !!! warning "Misconception #1: SELECT * is Fine"
        **Misconception:** "It's easier to just SELECT * from tables"
        
        **Reality:** This is inefficient and can expose sensitive data
        
        **Correction:** Always specify exact columns needed. Show performance difference with EXPLAIN.

    !!! warning "Misconception #2: Client-Side Validation is Enough"
        **Misconception:** "I already validate in JavaScript, so SQL injection isn't possible"
        
        **Reality:** Attackers bypass client-side validation entirely (use Postman, cURL, or modify browser requests)
        
        **Correction:** Demonstrate bypassing client validation with Postman. Show that server MUST validate.

    !!! warning "Misconception #3: Escaping is Same as Prepared Statements"
        **Misconception:** "Can't I just remove dangerous characters instead of using prepared statements?"
        
        **Reality:** Blacklist approaches always miss edge cases. Prepared statements are foolproof.
        
        **Correction:** Show that even "sanitised" input can sometimes be exploited. Prepared statements are non-negotiable.

    !!! warning "Misconception #4: Backups Happen Automatically"
        **Misconception:** "The database saves my data, so I don't need backups"
        
        **Reality:** Deletion, corruption, and hardware failure can destroy data permanently
        
        **Correction:** Simulate data loss scenario (delete table), show recovery from backup.

    !!! warning "Misconception #5: Indexes Make Everything Faster"
        **Misconception:** "I should index every column for maximum speed"
        
        **Reality:** Too many indexes slow down INSERT/UPDATE/DELETE operations and waste space
        
        **Correction:** Show performance impact on writes. Teach strategic indexing.

    !!! warning "Misconception #6: Foreign Keys are Optional"
        **Misconception:** "I can just store the user_id without making it a foreign key"
        
        **Reality:** Foreign keys enforce referential integrity and prevent orphaned records
        
        **Correction:** Demonstrate orphaned post (author deleted but post remains). Show ON DELETE CASCADE.

    !!! warning "Misconception 7: Big Data"
        * "Big data always means millions of records" - It's relative to your infrastructure
        * "More metadata is always better" - Balance between utility and storage overhead
        * "Indexes solve all performance problems" - They have trade-offs
        * "Data mining is just running queries" - It's about discovering actionable insights

??? note "Formative Assessment Strategies"

    **During Activities (Informal Assessment):**

    1. **Code Review Checkpoints:** Circulate during Activity 4.3, check for prepared statements
    2. **Question Asking:** Pose questions during demonstrations: "What would happen if...?"
    3. **Exit Ticket Questions:**
        - "Explain SQL injection in your own words"
        - "When would you use LEFT JOIN vs INNER JOIN?"
        - "Why are prepared statements important?"

    **Hands-On Demonstrations:**

    4. **Live Debugging:** Students share screen, debug SQL errors together
    5. **Security Testing:** Students attempt to SQL inject each other's code (controlled)
    6. **Query Optimization Competition:** Who can write fastest query? Use EXPLAIN to verify.

    **Written Checks:**

    7. **Quick Quiz (10 minutes):**
        - Identify vulnerable code
        - Write correct prepared statement
        - Explain when to use indexes
    
    8. **Reflection Prompts:**
        - "What was most challenging about SQL injection prevention?"
        - "How does this week connect to Week 7's authentication?"

    **Practical Checks:**

    9. **Commit History Review:** Check Git logs for proper progression and meaningful messages
    10. **Security Audit:** Review student projects for SQL injection vulnerabilities

??? note "Diagnostic Questions"

    !!! question "Check Understanding: CRUD"
        "Your friend says their blog needs to 'CRUD posts.' What do they mean? Give an example of each operation."

    !!! question "Check Understanding: SQL Injection"
        "A user enters `admin'; DROP TABLE users;--` in the username field. Walk me through what happens with vulnerable code vs prepared statements."

    !!! question "Check Understanding: JOINs"
        "You want to show all blog categories, even ones with zero posts. Which JOIN type do you use and why?"

    !!! question "Check Understanding: Indexing"
        "Your posts table has 1 million rows. Users complain that searching by title is slow. What do you do?"


??? note "Extension Activities"

    **For Students Who Finish Early:**

    1. **Advanced Queries Challenge:**
    ```sql
    -- Find users who posted more than the average
    -- Find the 3rd most commented post
    -- Show monthly post counts for the past year
    ```

    2. **Transactions and Rollback:**
        - Research SQL transactions
        - Implement BEGIN/COMMIT/ROLLBACK
        - Handle errors gracefully

    3. **Database Migrations:**
        - Create numbered migration files
        - Write UP and DOWN scripts
        - Track migration history

    4. **Query Performance Lab:**
        - Profile slow queries
        - Optimise with indexes and query rewrites
        - Document 10x+ performance improvements

    5. **Full-Text Search:**
        - Implement search functionality
        - Create search indexes
        - Rank results by relevance

### Resources and Tools

**Essential Tools:**

- SQLite (included with Python)
- DB Browser for SQLite (visual database tool)
- VSCode + SQLite or Postgres plugin
- Postman (API testing)

**Documentation:**

- [SQLite Documentation](https://www.sqlite.org/docs.html)
- [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

**Practice Platforms:**

- [SQLBolt](https://sqlbolt.com/) - Interactive SQL tutorial
- [SQL Murder Mystery](https://mystery.knightlab.com/) - Learn SQL through gamification
- [HackerRank SQL](https://www.hackerrank.com/domains/sql) - SQL challenges

### Assessment Rubric

| Criteria | Excellent (4) | Proficient (3) | Developing (2) | Beginning (1) |
|----------|--------------|----------------|----------------|---------------|
| **Schema Design** | Fully normalised, appropriate data types, all relationships defined | Minor normalisation issues, mostly correct | Poor normalisation, missing relationships | Unnormalised, incorrect structure |
| **SQL Queries** | All CRUD operations work, efficient queries, correct JOINs | Mostly correct, some inefficiencies | Some queries work, errors in complex operations | Major errors, cannot complete basic operations |
| **Security** | All queries use prepared statements, tested against attacks | Mostly secure, 1-2 vulnerabilities | Some prepared statements, significant vulnerabilities | String concatenation, highly vulnerable |
| **Indexing** | Strategic indexing, measured performance improvement | Indexes created but not optimised | Attempted indexing with errors | No indexes or incorrect implementation |
| **Backups** | Working backup and restore scripts, tested successfully | Scripts work but untested or incomplete | Scripts have errors or incomplete | No functional backup system |

---

## Conclusion and Next Steps

!!! success "Congratulations!"
    You've completed Week 8: Database Integration & SQL Security!
    
    You now have:

    - ✅ A persistent database replacing in-memory storage
    - ✅ Secure queries using prepared statements
    - ✅ Protection against SQL injection attacks
    - ✅ Optimised performance with indexes
    - ✅ Automated backup system

### Connection to Week 9

Next week, you'll build on this foundation:

- **Authentication** → **Authorization** (who can do what?)
- **User storage** → **Role-Based Access Control** (admin, moderator, user)
- **Basic security** → **CSRF Protection** (prevent cross-site attacks)
- **Simple sessions** → **Secure Session Management** (proper cookies, expiration)

### Final Checklist Before Moving On

- [ ] All database queries use prepared statements
- [ ] Schema is normalised with proper relationships
- [ ] Indexes created on frequently queried columns
- [ ] Backup and restore tested successfully
- [ ] Week 7 authentication integrated with database
- [ ] Data persists across server restarts
- [ ] SQL injection tests all fail (good!)
- [ ] Git history shows clear progression
- [ ] `.env` file in `.gitignore` (not committed!)

!!! tip "Keep Practising"
    - Review SQL queries daily
    - Never write SQL without prepared statements
    - Test your backups regularly
    - Always use WHERE with UPDATE and DELETE!

**You're ready for Complete Authentication, Authorization & CSRF Protection!**