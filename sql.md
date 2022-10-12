```sql
-- Inspecting data
SELECT * FROM sales_data_sample

-- Checking unique values
SELECT DISTINCT STATUS FROM sales_data_sample
SELECT DISTINCT YEAR_ID FROM sales_data_sample
SELECT DISTINCT PRODUCTLINE FROM sales_data_sample
SELECT DISTINCT COUNTRY FROM sales_data_sample
SELECT DISTINCT DEALSIZE FROM sales_data_sample
SELECT DISTINCT TERRITORY FROM sales_data_sample

SELECT DISTINCT MONTH_ID FROM sales_data_sample
WHERE YEAR_ID = 2005
ORDER BY 1

SELECT DISTINCT MONTH_ID FROM sales_data_sample
WHERE YEAR_ID = 2003
ORDER BY 1

-- ANALYSIS
-- Let's start by grouping sales by productline.
SELECT PRODUCTLINE, SUM(SALES) AS REVENUE FROM sales_data_sample
GROUP BY PRODUCTLINE
ORDER BY 2 DESC

SELECT YEAR_ID, SUM(SALES) AS REVENUE FROM sales_data_sample
GROUP BY YEAR_ID
ORDER BY 2 DESC

SELECT DEALSIZE, SUM(SALES) AS REVENUE FROM sales_data_sample
GROUP BY DEALSIZE
ORDER BY 2 DESC


-- What was the best month for sales in a specific year? How much was earned that month?
SELECT MONTH_ID, SUM(SALES) AS REVENUE, COUNT(ORDERNUMBER) AS FREQUENCY FROM sales_data_sample
WHERE YEAR_ID = 2004 --2005 --2003
GROUP BY MONTH_ID
ORDER BY 2 DESC

-- November seems to be the best month, what product do they sell in November?
SELECT MONTH_ID, PRODUCTLINE, SUM(SALES) AS REVENUE, COUNT(ORDERNUMBER) AS No_Orders FROM sales_data_sample
WHERE MONTH_ID = 11 AND YEAR_ID = 2003 --change year to see the rest
GROUP BY MONTH_ID, PRODUCTLINE
ORDER BY 3 DESC

-- Who is our best customer (this could be best answered with RFM)?
SELECT
	CUSTOMERNAME,
	SUM(SALES) AS MonetaryValue,
	AVG(SALES) AS AvgMonetaryValue,
	COUNT(ORDERNUMBER) AS Frequency,
	MAX(ORDERDATE) AS LastOrderDate,
	(SELECT MAX(ORDERDATE) FROM sales_data_sample) AS MaxOrderDate, DATEDIFF(DD, MAX(ORDERDATE), (SELECT MAX(ORDERDATE) FROM sales_data_sample)) AS Recency
FROM sales_data_sample
GROUP BY CUSTOMERNAME

DROP TABLE IF EXISTS #rfm

;WITH rfm AS
(
	SELECT
		CUSTOMERNAME,
		SUM(SALES) AS MonetaryValue,
		AVG(SALES) AS AvgMonetaryValue,
		COUNT(ORDERNUMBER) AS Frequency,
		MAX(ORDERDATE) AS LastOrderDate,
		(SELECT MAX(ORDERDATE) FROM sales_data_sample) AS MaxOrderDate, DATEDIFF(DD, MAX(ORDERDATE), (SELECT MAX(ORDERDATE) FROM sales_data_sample)) AS Recency
	FROM sales_data_sample
	GROUP BY CUSTOMERNAME
)

, rfm_calc AS
(
	SELECT *,
		NTILE(4) OVER(ORDER BY Recency DESC) rfm_recency,
		NTILE(4) OVER(ORDER BY Frequency) rfm_frequency,
		NTILE(4) OVER(ORDER BY MonetaryValue) rfm_monetary
	FROM rfm
)
SELECT 
	*, (rfm_recency + rfm_frequency + rfm_monetary) AS rfm_cell,
	CAST(rfm_recency AS VARCHAR) + CAST(rfm_frequency AS VARCHAR) + CAST(rfm_monetary AS VARCHAR) AS rfm_cell_string
INTO #rfm
FROM rfm_calc

-- Customer Segmentation
SELECT CUSTOMERNAME, rfm_recency, rfm_frequency, rfm_monetary, 
	CASE
		WHEN rfm_cell_string in (111, 112 , 121, 122, 123, 132, 211, 212, 114, 141, 221) THEN 'Lost Customer'    -- lost customer.
		WHEN rfm_cell_string in (133, 134, 143, 244, 334, 343, 344, 144) THEN 'Slipping Away, Cannot Lose'       -- Big spender who haven’t purchased lately, slipping away.
		WHEN rfm_cell_string in (311, 411, 331, 421, 412) THEN 'New Customer'                                    -- New customer.
		WHEN rfm_cell_string in (222, 223, 233, 322, 232, 234) THEN 'Potential Churners'                         -- Probably leave the service.
		WHEN rfm_cell_string in (323, 333,321, 422, 332, 432, 423) THEN 'Active'                                 -- Customers who buy often & recently, but at low price points.
		WHEN rfm_cell_string in (433, 434, 443, 444) THEN 'Loyal'                                                -- Customers who buy regularly at high price points.
	END
FROM #rfm

-- What products are most often sold together?
SELECT * FROM sales_data_sample
WHERE ORDERNUMBER = 10411

-- SELECT ORDERNUMBER, COUNT(*) AS rn
-- FROM sales_data_sample
-- WHERE STATUS = 'Shipped'
-- GROUP BY ORDERNUMBER

SELECT DISTINCT ORDERNUMBER, STUFF(
									(SELECT ',' + PRODUCTCODE FROM sales_data_sample p
									WHERE ORDERNUMBER IN (
															SELECT ORDERNUMBER 
															FROM (
																	SELECT ORDERNUMBER, COUNT(*) AS rn
																	FROM sales_data_sample
																	WHERE STATUS = 'Shipped'
																	GROUP BY ORDERNUMBER
																	) AS q
															WHERE rn = 3
															) 
															AND p.ORDERNUMBER = s.ORDERNUMBER
															FOR XML PATH(''))
										
															, 1, 1, '') AS ProductCodes

FROM sales_data_sample AS s
ORDER BY 2 DESC











```
