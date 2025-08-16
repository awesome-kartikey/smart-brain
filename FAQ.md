# Frequently Asked Questions (FAQ)

**Q1: Face detection isn't working. What could be wrong?**

*   **Check Clarifai API Key:** Ensure you have correctly added your Clarifai API key to the `.env` file in the `smart-brain-api` directory and restarted the backend server. An incorrect or missing key is the most common cause.
*   **Check Backend Server:** Make sure the backend API server (`smart-brain-api`) is running without errors. Check the terminal where you ran `npm start` for any logs.
*   **Check Frontend Console:** Open your browser's developer console (usually F12). Look for any errors, especially network errors (like 400 or 500) when submitting an image. This might indicate a problem with the API request or response.
*   **Clarifai Model Status:** Occasionally, the specific Clarifai model ('face-detection' in this case) might be temporarily unavailable or updated. You can check the model status on the Clarifai website.
*   **Image URL Validity:** Ensure the image URL you provided is public, directly links to an image file (e.g., `.jpg`, `.png`), and doesn't point to a webpage or a restricted resource.

**Q2: How do I set up the PostgreSQL database?**

1.  **Install PostgreSQL:** Download and install PostgreSQL for your operating system if you haven't already.
2.  **Start Server:** Make sure the PostgreSQL server is running.
3.  **Create Database:** Use a tool like `psql` (command-line) or a GUI client (like pgAdmin, DBeaver) to connect to your PostgreSQL instance. Create a new database using the command: `CREATE DATABASE your_db_name;` (Replace `your_db_name` with the name you specified in the backend's `.env` file).
4.  **Connect to Database:** Connect to the newly created database (`\c your_db_name` in `psql`).
5.  **Create Tables:** Execute the SQL commands found in the `smart-brain/sql queries.txt` file within your connected database. This will create the `users` and `login` tables.

**Q3: Where do I get a Clarifai API key?**

You can obtain a free API key from the [Clarifai website](https://www.clarifai.com/). Sign up for an account, create a new application, and navigate to the API Keys section within your application's settings to find your key.

**Q4: I'm getting CORS errors in the browser console. How do I fix this?**

CORS (Cross-Origin Resource Sharing) errors typically occur when the frontend (running on e.g., `localhost:3000`) tries to make requests to the backend (running on e.g., `localhost:8000`) and the backend doesn't explicitly permit it.

*   **Ensure Backend is Running:** Verify that your `smart-brain-api` server is running.
*   **Check `cors` Middleware:** The backend (`server.js`) uses the `cors` middleware (`app.use(cors());`). This should generally allow requests from any origin during development. Ensure this line is present and correct in `server.js`. If you deployed the backend, you might need to configure CORS more specifically for your frontend's domain.
*   **Restart Servers:** Sometimes, simply restarting both the backend and frontend servers can resolve temporary issues.

**Q5: What are the `.env` files for? Why isn't one included in the repository?**

The `.env` file (dotenv) is used to store environment-specific variables, particularly secrets like database passwords and API keys.

*   **Security:** It keeps sensitive information out of your version-controlled codebase (Git). You should **never** commit `.env` files containing secrets.
*   **Configuration:** It allows different configurations for development, testing, and production environments without changing the code.
*   **`.gitignore`:** The `.gitignore` file in `smart-brain-api` explicitly lists `.env` to prevent accidental commits. You need to create this file yourself based on your local setup (see Setup Instructions).

**Q6: I'm having trouble logging in or registering.**

*   **Check API Server:** Is the `smart-brain-api` server running? Check its terminal for errors.
*   **Database Connection:** Did the API server connect to the database successfully? Look for connection error messages when the API server starts. Verify your database credentials in the API's `.env` file.
*   **Check Browser Console:** Look for network errors or messages in the browser's developer console when you attempt to sign in or register.
*   **Correct Credentials:** Double-check that you are entering the correct email and password. Remember passwords are case-sensitive.
*   **Unique Email:** Ensure the email you are trying to register with isn't already in use. The database enforces unique emails.

**Q7: Can I use a different database like MySQL?**

The backend currently uses `knex` configured with the `pg` client, specifically for PostgreSQL. To use MySQL, you would need to:

1.  Install the MySQL driver for Node.js: `npm install mysql` in the `smart-brain-api` directory.
2.  Update the `knex` configuration in `smart-brain-api/server.js`:
    *   Change `client: 'pg'` to `client: 'mysql'`.
    *   Adjust the `connection` details object to match MySQL's requirements (host, user, password, database). Note that some specific connection options like SSL might differ.
3.  Adapt the SQL queries in `smart-brain/sql queries.txt` for MySQL syntax if there are any PostgreSQL-specific features used (though the current schema is fairly standard).