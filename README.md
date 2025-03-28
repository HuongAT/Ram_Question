# Ram_Question

SELECT transaction_date,
       Avg(total_amount)
         over(
           ORDER BY transaction_date ROWS BETWEEN 2 preceding AND CURRENT ROW)
       AS
       rolling_3_days_avg
FROM   (SELECT Cast(transaction_time AS DATE) AS transaction_date,
               SUM(transaction_amount)        AS total_amount
        FROM   transactions
        GROUP  BY transaction_date) AS transactions_daily
WHERE  transaction_date = '2021-01-31';  