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

## Results

### 1. Database design (ER diagram)

-- Find which tables are connected using foreign keys
SELECT
    TABLE_NAME AS child_table,
    COLUMN_NAME AS foreign_key,
    REFERENCED_TABLE_NAME AS parent_table,
    REFERENCED_COLUMN_NAME AS parent_key
FROM information_schema.KEY_COLUMN_USAGE
WHERE TABLE_SCHEMA = DATABASE()
    AND REFERENCED_TABLE_NAME IS NOT NULL
ORDER BY TABLE_NAME;


### 2. Branch with the highest total balance
```sql
SELECT b.BranchName, SUM(a.Balance) AS Total_Balance
FROM Branches b JOIN Accounts a ON b.BranchID = a.BranchID
GROUP BY b.BranchName
ORDER BY Total_Balance DESC;
```
<img width="1020" height="245" alt="image" src="https://github.com/user-attachments/assets/da9ab47d-ba5f-42b7-b391-14ffb8c99e7c" />


Salt Lake Branch holds the highest total balance (4,185,000).

### 3. Loans by status
```sql
SELECT LoanStatus, COUNT(LoanID) AS Total_Loans
FROM Loans
GROUP BY LoanStatus;
```
<img width="1015" height="237" alt="image" src="https://github.com/user-attachments/assets/e3a210d9-81d2-4e42-a146-4f43787d30df" />

36 Active, 8 Closed, 3 Pending and 3 Defaulted loans.

### 4. Most common loan type
```sql
SELECT LoanType, COUNT(LoanID) AS Total_Loans
FROM Loans
GROUP BY LoanType
ORDER BY Total_Loans DESC;
```
<img width="1010" height="222" alt="image" src="https://github.com/user-attachments/assets/21c2e09d-7b8d-415a-bfa4-a2aee69317f8" />

Home Loan is the most common type (15 of 50 loans).

### 5. Customers earning above average (subquery)
```sql
SELECT * FROM Customers
WHERE AnnualIncome > (SELECT AVG(AnnualIncome) FROM Customers);
```
<img width="1021" height="425" alt="image" src="https://github.com/user-attachments/assets/b3bfdad5-480a-4e20-ab3c-7982b62d458a" />

The average annual income is 1,209,000; this query lists everyone above it.

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
