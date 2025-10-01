# X-Track Excel Analyser 📊

X-Track is a powerful, browser-based data analysis tool that transforms raw spreadsheet data into insightful, interactive visualizations. Built with modern web technologies and powered by Supabase, it provides a seamless experience from user authentication to dynamic chart generation.


---

## ✨ Key Features

-   **Secure User Authentication**: Full login and signup functionality handled by Supabase Auth.
-   **Versatile File Upload**: Supports popular spreadsheet formats including `.xlsx`, `.xls`, `.csv`, and `.txt`.
-   **Instant Data Preview**: Displays a clean, scrollable table preview of the uploaded data.
-   **Dynamic Chart Generation**: Visualize data on the fly with a variety of chart types.
-   **Multiple Chart Options**: Includes:
    -   Bar Chart
    -   Column Chart
    -   Line Chart
    -   Area Chart
    -   Pie Chart
    -   3D Scatter Plot
-   **Modern & Responsive UI**: A sleek, dark-themed interface with a video background, designed to be intuitive on any device.
-   **Client-Side Processing**: All file parsing and chart rendering are done securely in the browser, ensuring user data privacy.

---

## 🛠️ Tech Stack

-   **Frontend**: HTML5, CSS3, JavaScript
-   **Charting Library**: [Plotly.js](https://plotly.com/javascript/)
-   **File Parsing**: [SheetJS (xlsx.js)](https://sheetjs.com/)
-   **Backend as a Service (BaaS)**: [Supabase](https://supabase.io/)
    -   **Authentication**: Manages user signups and logins.
    -   **Database**: Stores user profile information.


---

## 📂 Project Structure

The project is organized into four main pages:

-   `home.html`: The main landing page that introduces the application.
-   `login.html`: Handles user authentication (both login and signup forms).
-   `users.html`: The user dashboard for uploading files.
-   `analysis.html`: The core analysis page where data is previewed and visualized.

---

## 🚀 Setup and Installation

To run this project locally, you'll need to set up a free Supabase project for the backend.

### 1. Supabase Configuration

1.  **Create a Supabase Project**: Go to [supabase.io](https://supabase.io/) and create a new project.
2.  **Create a `users` Table**: In your Supabase project's SQL Editor, run the following query to create the table for storing user data:

    ```sql
    CREATE TABLE public.users (
      id UUID PRIMARY KEY REFERENCES auth.users(id),
      name TEXT,
      mobile TEXT,
      email TEXT,
      created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL
    );
    ```

3.  **Enable Authentication**: Ensure that Email authentication is enabled in your Supabase project's authentication settings. You can leave email confirmation enabled or disabled based on your preference.

4.  **Get API Keys**: Navigate to `Project Settings` > `API` and find your **Project URL** and `anon` **public key**.

### 2. Local Configuration

1.  **Clone the Repository**:
    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```
2.  **Add Supabase Credentials**: Open the `login.html` and `users.html` files. In the `<script>` tag at the bottom of each file, replace the placeholder credentials with your Supabase URL and Key:

    ```javascript
    // In both login.html and users.html
    const SUPABASE_URL = "YOUR_SUPABASE_URL";
    const SUPABASE_KEY = "YOUR_SUPABASE_ANON_KEY";
    const supabaseClient = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);
    ```

### 3. Running the Project

This project does not require a special server. You can run it by simply opening the `home.html` file in your web browser. For the best experience, use a live server extension.

-   **Using VS Code Live Server**: If you use Visual Studio Code, you can install the "Live Server" extension, right-click on `home.html`, and select "Open with Live Server".

---

## ⚙️ How It Works

1.  **Authentication**: A new user signs up on the `login.html` page. Their credentials are sent to Supabase Auth. A corresponding entry is also created in the `public.users` table. Existing users can log in to create a session.
2.  **File Upload**: Once logged in, the user is redirected to `users.html`. They can choose a file from their local machine.
3.  **Data Parsing**: The application uses the SheetJS library to read the file's contents directly in the browser. The parsed data (as a JSON array) is stored in the browser's `sessionStorage`.
4.  **Analysis & Visualization**: The user is redirected to `analysis.html`. The page retrieves the data from `sessionStorage` and displays it in a preview table.
5.  **Chart Plotting**: The user selects a chart type and maps the data columns to the chart's axes (e.g., X, Y, Z, Legends, Values). Clicking "Plot Chart" uses Plotly.js to render the selected visualization in the chart area.
6.  **Logout**: The logout button clears the Supabase session and `sessionStorage`, redirecting the user back to the login page.

---

## 📜 License

This project is licensed under the MIT License. See the `LICENSE` file for more details.
