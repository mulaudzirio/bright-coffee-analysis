SELECT TRANSACTION_DATE,
  TO_CHAR(TO_DATE(TRANSACTION_DATE, 'YYYY/MM/DD'), 'YYYYMM') AS month_id,
  COUNT(TRANSACTION_ID) AS number_of_sales,
  COUNT( product_id) AS unique_products_sold,
  SUM(transaction_qty * TO_NUMBER(REPLACE(unit_price, ',', '.'))) AS total_amount,
  product_category,
  product_detail,
  product_type,
  store_ID,
  CASE
    WHEN transaction_time BETWEEN TIME '06:00:00' AND TIME '11:59:59' THEN 'Morning'
    WHEN transaction_time BETWEEN TIME '12:00:00' AND TIME '16:59:59' THEN 'Afternoon'
    WHEN transaction_time BETWEEN TIME '17:00:00' AND TIME '19:59:59' THEN 'Evening'
    ELSE 'Night'
  END AS time_buckets

FROM
  BRIGHT_COFFEE.PUBLIC.BRIGHT_C0FFEEEE
  
GROUP BY 
 TRANSACTION_DATE,
  TO_CHAR(TO_DATE(TRANSACTION_DATE, 'YYYY/MM/DD'), 'YYYYMM'),
  product_category,
  product_detail,
  product_type,
  store_ID,
  CASE
    WHEN transaction_time BETWEEN TIME '06:00:00' AND TIME '11:59:59' THEN 'Morning'
    WHEN transaction_time BETWEEN TIME '12:00:00' AND TIME '16:59:59' THEN 'Afternoon'
    WHEN transaction_time BETWEEN TIME '17:00:00' AND TIME '19:59:59' THEN 'Evening'
    ELSE 'Night'
  END;



  
