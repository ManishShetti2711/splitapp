Split App - Expense Sharing Backend

   A simple backend system to track shared group expenses and automate settlements between users — built with Node.js, Express, and MongoDB.

   Inspired by apps like Splitwise, this API allows groups (like roommates, travel buddies, or friends) to:
- Add shared expenses
- Track individual balances
- Calculate optimized settlements


   Live Demo (Railway)

  Deployed API Base URL:  
 https://splitapp-production-1be8.up.railway.app


   How to Run Locally

 Prerequisites
- Node.j
- MongoDB Atlas (or local MongoDB)

 1. Clone the repo

```bash
git clone https://github.com/ManishShetti2711/spiltapp.git
cd spiltapp
```

 2. Install dependencies

```bash
npm install
```

 3. Create `.env` file

```env
PORT=3000
mongodb+srv://manishshetti27:ManishShetti2711@cluster0.9uzucgr.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0
```

 4. Run the server

```bash
node app.js
```

Server will be running at: `http://localhost:3000`


API Documentation:

   Add Expense (POST)
URL: `https://splitapp-production-1be8.up.railway.app/expenses`
Method: POST
Body (JSON):

```json
{
  "amount": 600,
  "description": "Dinner",
  "paid_by": "Manish",
  "participants": ["Manish", "Anish", "Tanish"],
  "split_type": "equal"
}
```

  Get All Expenses (GET)
URL: `https://splitapp-production-1be8.up.railway.app/expenses`
Method: GET

  Update Expense (PUT)
URL: `https://splitapp-production-1be8.up.railway.app/expenses/<id>`
Method: PUT
Replace `<id>` with a real MongoDB ObjectId.

  Delete Expense (DELETE)
URL: `https://splitapp-production-1be8.up.railway.app/expenses/<id>`
Method: DELETE


 Settlements & People:

  Get All People
URL: `https://splitapp-production-1be8.up.railway.app/people`
Method: GET

  Get Balances
URL: `https://splitapp-production-1be8.up.railway.app/balances`
Method: GET

  Get Settlements
URL: `https://splitapp-production-1be8.up.railway.app/settlements`
Method: GET



 Expense Management

| Method | Endpoint             | Description               |
|--------|----------------------|---------------------------|
| GET    | `/expenses`          | Get all expenses          |
| POST   | `/expenses`          | Add new expense           |
| PUT    | `/expenses/:id`      | Update an expense         |
| DELETE | `/expenses/:id`      | Delete an expense         |

Sample Payload (POST /expenses):
```json
{
  "amount": 600,
  "description": "Dinner",
  "paid_by": "Manish",
  "participants": ["Manish", "Anish", "Tanish"],
  "split_type": "equal"
}
```



 Settlement & People

| Method | Endpoint             | Description                     |
|--------|----------------------|---------------------------------|
| GET    | `/people`            | List all people in the group    |
| GET    | `/balances`          | Get balances for each person    |
| GET    | `/settlements`       | Get optimized transactions      |

---

 Settlement Logic Explained

1. Calculate Net Balance for Each Person:
   - Total paid by person - total owed based on split.

2. Example Output from `/balances`:
```json
{
  "Manish": 150,
  "Anish": -50,
  "Tanish": -100
}
```

3. Minimize Transactions:
   - Apply greedy algorithm to pair debtors and creditors.
   - Example from `/settlements`:
```json
[
  { "from": "Tanish", "to": "Manish", "amount": 100 },
  { "from": "Anish", "to": "Manish", "amount": 50 }
]
```

Postman Collection

  Includes:
- All endpoints
- Sample test data: Manish, Anish, Tanish
- Edge case testing
- Validations

Gist Link:  

https://gist.github.com/ManishShetti2711/cf41b1a48de7e990b60a61277c77a55c



Known Limitations

- Names like `Manish`, `Tanish`, etc., are assumed unique (not validated case-insensitively).
- No user authentication or session management (for simplicity).
- No pagination for expenses list.
- Uses in-memory greedy settlement — not guaranteed to be minimal in complex graphs.


Future Improvements (Optional)

- Add user authentication (JWT or OAuth)
- Support recurring expenses
- Add categories and spending analytics
- Create a frontend dashboard (React or plain HTML)



Author

Manish Chiwadshetti  
[GitHub](https://github.com/ManishShetti2711)
