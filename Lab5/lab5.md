1.
SELECT COUNT(DISTINCT b.customer_name)
FROM borrower AS b, customer AS c, loan AS l, branch as br
WHERE b.customer_name = c.customer_name
AND b.loan_number = l.loan_number
AND l.branch_name = br.branch_name
AND c.customer_city = br.branch_city

2.
SELECT c.customer_name, avg(balance)
FROM customer AS c, account AS a, depositor as d
WHERE c.customer_name = d.customer_name
AND a.account_number = d.account_number
GROUP BY c.customer_name

3.
SELECT c.customer_name, avg(balance)
FROM customer AS c, account AS a, depositor AS d
WHERE c.customer_name = d.customer_name
AND a.account_number = d.account_number
AND a.branch_name IN (SELECT account.branch_name
FROM account, branch
WHERE account.branch_name = branch.branch_name
AND branch_city = 'Horseneck')
GROUP BY c.customer_name

4.
SELECT SUM(balance)
FROM account AS a, branch AS b
WHERE b.branch_city = 'Horseneck'
AND a.branch_name = b.branch_name

5.
SELECT branch_city, sum(balance)
FROM branch, account
WHERE branch.branch_name = account.branch_name
GROUP BY branch_city

6.
SELECT branch_name
FROM loan
GROUP BY branch_name
HAVING COUNT(loan_number) >= 2
ORDER BY branch_name

7.
SELECT branch_name, SUM(amount)
FROM loan
GROUP BY branch_name
HAVING COUNT(loan_number) >= 2
ORDER BY branch_name

8.
SELECT branch.branch_name, branch_city
FROM account
RIGHT OUTER JOIN branch ON branch.branch_name = account.branch_name
WHERE account.branch_name IS NULL

9.
SELECT customer_name
FROM customer
WHERE customer_name NOT IN (SELECT customer_name FROM depositor)

10.
(SELECT branch_name
FROM branch
WHERE branch_name NOT IN (SELECT branch_name FROM account))
UNION
(SELECT branch_name
FROM branch
WHERE branch_name NOT IN (SELECT branch_name FROM branch))

11.
SELECT branch_name
FROM branch
WHERE branch_name NOT IN (
  SELECT branch_name FROM depositor WHERE branch_name IN (
    SELECT branch_name FROM loan))

12.
SELECT customer_name
FROM customer
WHERE customer_city IN (SELECT branch_city FROM branch)

13.
SELECT loan_number, amount
FROM loan
WHERE amount >= ALL (SELECT amount FROM loan)

14.
SELECT customer_name, SUM(amount)
FROM loan, borrower
WHERE loan.loan_number = borrower.loan_number
GROUP by customer_name

15.
SELECT customer_name
FROM loan, borrower
WHERE loan.loan_number = borrower.loan_number
AND loan.amount >= ALL (SELECT amount FROM loan)
