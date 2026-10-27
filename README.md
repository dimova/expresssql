# Spiral Sounds

Online classic vinyl store — an Express + SQLite backend serving a static front end, with user authentication and a shopping cart.

## Tech Stack

- [Node.js](https://nodejs.org/) / [Express](https://expressjs.com/)
- [SQLite](https://www.sqlite.org/) via `sqlite` / `sqlite3`
- `express-session` for session-based authentication
- `bcryptjs` for password hashing
- `validator` for input validation

## Prerequisites

- [Node.js](https://nodejs.org/) (includes npm)
- A `database.db` SQLite file in the project root containing the `products`, `users`, and `cart_items` tables

## Installation

```bash
npm install
```

## Running the App

```bash
npm start
```

This runs `node server.js` and starts the server at **http://localhost:8000**.

## Environment Variables

| Variable                   | Description                                      | Default                   |
| --------------------------- | ------------------------------------------------- | -------------------------- |
| `SPIRAL_SESSION_SECRET`    | Secret used to sign the session cookie            | `jellyfish-baskingshark`  |

Set this in a `.env` file or your shell environment before starting the app in production:

```bash
SPIRAL_SESSION_SECRET=your-secret-here
```

## Project Structure

```
server.js             # App entry point, middleware & route wiring
routes/               # Express routers (products, auth, me, cart)
controllers/          # Route handler logic
middleware/           # Custom middleware (e.g. requireAuth)
db/db.js              # SQLite connection helper
public/               # Static front end (HTML, CSS, JS, images)
logTable.js           # Dev utility to print a DB table's contents to the console
database.db           # SQLite database file (not committed, see .gitignore)
```

## API Overview

| Method | Endpoint                | Auth required | Description                 |
| ------ | ------------------------ | -------------- | ---------------------------- |
| GET    | `/api/products`         | No             | List products                |
| GET    | `/api/products/genres`  | No             | List product genres          |
| POST   | `/api/auth/register`    | No             | Register a new user          |
| POST   | `/api/auth/login`       | No             | Log in and create a session  |
| GET    | `/api/auth/logout`      | No             | Log out / destroy session    |
| GET    | `/api/auth/me`          | No             | Get the current session user |
| GET    | `/api/cart`             | Yes             | List items in the cart       |
| POST   | `/api/cart/add`         | Yes             | Add an item to the cart      |
| GET    | `/api/cart/cart-count`  | Yes             | Get number of items in cart  |
| DELETE | `/api/cart/:itemId`     | Yes             | Remove one item from cart    |
| DELETE | `/api/cart/all`         | Yes             | Clear the cart                |

Authenticated routes require an active session cookie (obtained via `/api/auth/login`).

## Dev Utility

To inspect the contents of a database table during development, edit the `tableName` variable in [logTable.js](./logTable.js) and run:

```bash
node logTable.js
```

## License

ISC

## Author

Tom Chant
