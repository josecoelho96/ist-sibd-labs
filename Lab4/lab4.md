1.
SELECT DISTINCT customer_name 
FROM account as a, depositor as d 
WHERE a.account_number = d.account_number 
AND balance > 500;

2.
SELECT DISTINCT c.customer_name, customer_city 
FROM customer as c, loan as l, borrower as b 
WHERE l.loan_number = b.loan_number 
AND b.customer_name = c.customer_name 
AND amount > 1000 
AND amount < 2000;

3.
SELECT 0.99*balance 
FROM account 
WHERE branch_name='Perryridge';

4.
SELECT a.account_number, a.balance 
FROM account as a, depositor as d, borrower as b 
WHERE b.loan_number = 'L-15' 
AND b.customer_name =  d.customer_name 
AND a.account_number = d.account_number;

5.
SELECT DISTINCT customer_name 
FROM customer as c, branch as b 
WHERE b.branch_city = c.customer_city;

6.
SELECT b.branch_name, b.assets 
FROM branch as b, account as a, depositor as d 
WHERE d.customer_name = 'Jones' 
AND d.account_number = a.account_number 
AND a.branch_name = b.branch_name;

7.
SELECT d.customer_name, a.branch_name 
FROM account as a, depositor as d 
WHERE d.customer_name like 'J%s' 
AND d.account_number = a.account_number;

8.
SELECT c.customer_name, c.customer_street, l.loan_number, l.amount 
FROM loan as l, borrower as b, customer as c 
WHERE c.customer_street LIKE '____' 
AND c.customer_name = b.customer_name 
AND b.loan_number = l.loan_number;

9.
SELECT d.customer_name 
FROM depositor as d, account as a, borrower  as b, loan as l 
WHERE b.customer_name = d.customer_name 
AND b.loan_number = l.loan_number 
AND d.account_number = a.account_number 
AND a.branch_name = l.branch_name;

