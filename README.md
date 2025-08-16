# SmartBrain Face Detection App

Welcome to SmartBrain! This is a full-stack web application that detects faces in images provided by users via a URL. Users can register, sign in, submit image URLs, and see their submission count increase with each detected image.

## Features

- **User Authentication:** Secure user registration and sign-in functionality.
- **Image Recognition:** Utilizes the Clarifai API to detect faces within images provided via URL.
- **Rank Tracking:** Keeps track of the number of images successfully submitted and analyzed by each user.
- **Interactive UI:** Built with React for a dynamic user experience.
- **Animated Background:** Features particle effects using `particles-bg`.
- **Separate Frontend & Backend:** Clear separation of concerns between the client-side interface and the server-side logic and data management.

## Tech Stack

- **Frontend:**
  - React.js (v18)
  - JavaScript (ES6+)
  - CSS3 & Tachyons (CSS toolkit)
  - `particles-bg` (Animated background)
  - `react-parallax-tilt` (Logo tilt effect)
- **Backend:**
  - Node.js
  - Express.js
  - PostgreSQL (Database)
  - Knex.js (SQL Query Builder)
  - bcrypt-nodejs (Password Hashing)
  - Clarifai API Client
  - `cors` (Cross-Origin Resource Sharing)
  - `dotenv` (Environment variable management)
- **Database:**
  - PostgreSQL

## Setup Instructions

Follow these steps to get the project running locally:

**Prerequisites:**

- Node.js and npm (or yarn) installed.
- PostgreSQL server installed and running.
- A Clarifai API Key ([Get one here](https://www.clarifai.com/)).

**1. Clone the Repository:**

```bash
git clone https://github.com/awesome-kartikey/SmartBrain-Project.git
cd smartbrain-project
```

**2. Setup Backend (`smart-brain-api`):**

- Navigate to the API directory:
  ```bash
  cd smart-brain-api
  ```
- Install dependencies:
  ```bash
  npm install
  ```
- Create a `.env` file in the `smart-brain-api` directory and add your environment variables. Use the example below:

  ```dotenv
  # Database Credentials
  DATABASE_HOST=your_db_host (e.g., localhost)
  DATABASE_USER=your_db_user
  DATABASE_PW=your_db_password
  DATABASE_DB=your_db_name
  DATABASE_PORT=your_db_port (e.g., 5432) # Optional, specify if not default

  # Clarifai API Key
  CLARIFAI_API_KEY=your_clarifai_api_key

  # Server Port (Optional)
  PORT=8000
  ```

- **Database Setup:**

  - Ensure your PostgreSQL server is running.
  - Connect to your PostgreSQL instance (using `psql` or a GUI tool).
  - Create the database specified in your `.env` file (e.g., `CREATE DATABASE your_db_name;`).
  - Connect to the newly created database.
  - Run the SQL commands found in `../smart-brain/sql queries.txt` to create the necessary tables (`users` and `login`):

    ```sql
    -- Connect to your database first, then run these:
    CREATE TABLE users (
      id serial PRIMARY KEY,
      name VARCHAR(100),
      email TEXT UNIQUE NOT NULL,
      entries BIGINT DEFAULT 0,
      joined TIMESTAMP NOT NULL
    );

    CREATE TABLE login (
        id serial PRIMARY KEY,
        hash VARCHAR(100) NOT NULL,
        email TEXT UNIQUE NOT NULL
    );
    ```

- Start the backend server (from the `smart-brain-api` directory):
  ```bash
  npm start
  ```
  The API server should now be running (typically on port 8000, unless specified otherwise in `.env`). Keep this terminal open.

**3. Setup Frontend (`smart-brain`):**

- Open a **new terminal window/tab**.
- Navigate to the frontend directory:
  ```bash
  cd ../smart-brain
  ```
- Install dependencies:
  ```bash
  npm install
  ```
- Start the frontend development server:
  ```bash
  npm start
  ```
  This will typically open the application in your default browser at `http://localhost:3000`.

**4. Ready!**

You should now be able to access the application in your browser, register a new user, sign in, and start detecting faces in images.

## Usage

1.  **Register:** Navigate to the application (usually `http://localhost:3000`). Click on "Register", fill in your name, email, and password, and click the "Register" button.
2.  **Sign In:** After registering or if you already have an account, use the "Sign In" form with your email and password.
3.  **Detect Faces:** Once signed in, you will see the main application page. Paste the URL of an image containing faces into the input field.
4.  **Submit:** Click the "Detect" button.
5.  **View Results:** The application will display the image with bounding boxes drawn around the detected faces. Your entry count (rank) displayed at the top will also increment.


