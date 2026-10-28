# Bank Customer & Loan Analytics (MySQL)

A relational banking database designed from scratch, with 55+ SQL queries answering business questions on customers, accounts, branches, transactions and loans.

## Database design
6 tables linked with primary and foreign keys:

| Table | Rows | Purpose |
|---|---|---|
| customers | 50 | customer profile, city, occupation, annual income |
| accounts | 70 | account type, balance, status, branch |
| banktransactions | 200 | deposits, withdrawals, payments, transfers |
| loans | 50 | loan type, amount, status |
| loan payments | – | repayment records |
| branches | 8 | branch name, city, state |

All data is synthetic, created for practice.

## SQL skills used
JOIN (inner and left), GROUP BY, HAVING, ORDER BY / LIMIT, aggregate functions, subqueries (including nested), NULL checks

## Analysis sections
1. Customer analysis (age, city, income, occupation)
2. Account analysis (types, balances, status)
3. Branch analysis (accounts and balance per branch)
4. Transaction analysis (types, totals, averages)
5. Loan analysis (types, status, defaulters)
6. Subquery-based analysis

## Key findings
- Highest total balance: **Salt Lake branch (4,185,000)**, ahead of Hitech City (3,915,000).
- Current accounts have the highest average balance (about 565,000) versus Savings (190,500).
- **Home Loan** is the most common loan type (15 of 50 loans); total loans issued 119,150,000.
- Loan status: 36 Active, 8 Closed, 3 Pending, **3 Defaulted**.
- 66 of 70 accounts are Active; 2 Inactive, 2 Closed.
- Deposits are the largest transaction type: 105 transactions totalling 7,556,000.
- One customer (Aditya Mehra) has no account.

## Files
```
schema.sql     CREATE TABLE statements
data.sql       INSERT statements
queries.sql    all queries with comments
images/        result screenshots
```

## How to run
```sql
SOURCE schema.sql;
SOURCE data.sql;
SOURCE queries.sql;
```

## Author
Ayush Kumar · [LinkedIn](https://www.linkedin.com/in/ayush-kumar-214742443) · ayushkum5591@gmail.com
