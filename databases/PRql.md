https://prql-lang.org/
https://prql-lang.org/examples/

A re-imagining of SQL in a sensible order. Compiles to SQL. Would love to play around with it more, I've wanted something like this for a long time.

ex query:

```prql
from employees                                # Each line transforms the previous result.
filter start_date > @2021-01-01               # Clear date syntax.
derive [                                      # `derive` adds columns / variables.
  gross_salary = salary + payroll_tax,
  gross_cost = gross_salary + benefits_cost   # Variables can use other variables.
]
filter gross_cost > 0
group [title, country] (                      # `group` runs a pipeline over each group.
  aggregate [                                 # `aggregate` reduces a column to a row.
    average salary,
    sum     salary,
    average gross_salary,
    sum     gross_salary,
    average gross_cost,
    sum_gross_cost = sum gross_cost,          # `=` sets a column name.
    ct = count,
  ]
)
sort [sum_gross_cost, -country]               # `-country` means descending order.
filter ct > 200
take 20
```

which compiles to the equivalent of this SQL query:

```sql
SELECT TOP 20
  title,
  country,
  AVG(salary) AS average_salary,
  SUM(salary) AS sum_salary,
  AVG(salary + payroll_tax) AS average_gross_salary,
  SUM(salary + payroll_tax) AS sum_gross_salary,
  AVG(salary + payroll_tax + benefits_cost) AS average_gross_cost,
  SUM(salary + payroll_tax + benefits_cost) AS sum_gross_cost,
  COUNT(*) AS ct
FROM
  employees
WHERE
  start_date > DATE('2021-01-01')
  AND salary + payroll_tax + benefits_cost > 0
GROUP BY
  title,
  country
HAVING
  COUNT(*) > 200
ORDER BY
  sum_gross_cost,
  country DESC
```

`derive` means, given the previous results, create these new columns. Being able to do multiple `derive`/`filter` pairs would be so nice!

In golang, I think the best way to integrate this tool would be to use it at code generation time? Looks like the work has not been done there yet, this project is v new.