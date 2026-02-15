# Banking Simulation System

A robust banking simulation backend built with Node.js, Express, and MongoDB. This system implements a double-entry ledger system to ensure data integrity for all financial transactions.

## 🚀 Features

-   **User Authentication**: Secure Sign Up, Login, and Logout functionality using JWT and Cookies.
-   **Account Management**: Create and manage bank accounts (Savings, Current, etc.) with support for multiple currencies.
-   **Double-Entry Ledger**: Every transaction is recorded as both a Credit and a Debit entry, ensuring the sum of all transactions assumes zero error.
-   **Atomic Transactions**: Transactions are processed atomically using MongoDB Sessions to prevent partial state updates.
-   **Idempotency**: Prevents duplicate transactions processing using unique keys.
-   **Transaction History**: View complete transaction logs and account statements.
-   **Email Notifications**: valid email updates for transaction status.

## 🛠️ Tech Stack

-   **Runtime**: Node.js
-   **Framework**: Express.js
-   **Database**: MongoDB (with Mongoose ODM)
-   **Authentication**: JSON Web Tokens (JWT) & bcryptjs
-   **Validation**: Custom middleware & Mongoose validation

## ⚙️ Installation & Setup

1.  **Clone the repository**
    ```bash
    git clone <repository_url>
    cd bankingsimulation
    ```

2.  **Install dependencies**
    ```bash
    npm install
    ```

3.  **Environment Configuration**
    Create a `.env` file in the root directory and add:
    ```env
    PORT=3000
    MONGO_URL=your_mongodb_connection_string
    JWT_SECRET=your_jwt_secret_key
    EMAIL_USER=your_email@example.com
    EMAIL_PASS=your_email_password
    ```

4.  **Run the application**
    ```bash
    # Start the server
    npm start
    
    # Or in development mode (if nodemon is installed)
    npm run dev
    ```

## 🔌 API Endpoints

### 🔐 Authentication

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new user |
| `POST` | `/api/auth/login` | Login and receive a JWT token |
| `POST` | `/api/auth/logout` | Logout and invalidate token |

### 🏦 Accounts

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/account` | Create a new bank account |
| `GET` | `/api/account` | Get all accounts for the logged-in user |
| `GET` | `/api/account/:accountId/balance` | Get real-time balance for a specific account |

### 💸 Transactions

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/transaction` | Transfer funds between accounts |
| `POST` | `/api/transaction/initial-funds` | Deposit initial funds (System use) |

## 📦 Data Models

-   **User**: Stores user profile and authentication details.
-   **Account**: Represents a bank account linked to a user. Tracks status (Active/Frozen).
-   **Transaction**: Records the intent of a fund movement. Tracks status (Pending/Completed/Failed).
-   **Ledger**: The source of truth. Records the actual money movement (Credit/Debit) mapped to a Transaction.

## 🛡️ Security

-   **Password Hashing**: Passwords are hashed using `bcrypt` before storage.
-   **Token Blacklisting**: Logout functionality blacklists tokens to prevent reuse.
-   **Input Validation**: Strict validation on all API inputs.