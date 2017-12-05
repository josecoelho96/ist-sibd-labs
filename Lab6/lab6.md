1.
SELECT branch_name
FROM branch
WHERE branch_city = 'Brooklyn'

2.
SELECT branch_name, account_number
FROM  account
NATURAL JOIN branch
WHERE branch_city = 'Brooklyn'

3.
SELECT branch_name, account_number, customer_name
FROM  account
NATURAL JOIN branch
NATURAL JOIN depositor
WHERE branch_city = 'Brooklyn'

4.
Yes, Johnson (he has accounts in both branches)

5.
WORKED!
SELECT DISTINCT customer_name
FROM depositor as d
WHERE NOT EXISTS(
  SELECT branch_name
  FROM branch AS b
  WHERE branch_city = 'Brooklyn'
  AND branch_name NOT IN (
    SELECT branch_name
    FROM account AS a, depositor AS d2
    WHERE a.account_number = d2.account_number
    AND d2.customer_name =  d.customer_name
  ))

6.
It's black magic. I really don't understand it. ._.

7.
SELECT DISTINCT customer_name
FROM depositor as d
WHERE NOT EXISTS(
  SELECT branch_name
  FROM branch AS b
  WHERE branch_city = 'Brooklyn'
  AND NOT EXISTS(
    SELECT branch_name
    FROM account AS a, depositor AS d2
    WHERE a.account_number = d2.account_number
    AND d2.customer_name =  d.customer_name
    AND b.branch_name = a.branch_name))

8.

