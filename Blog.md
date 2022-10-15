# <p align = 'center'>CUSTOMER SEGMENTATION ANALYSIS FOR RETAIL SALES</p>
![pic](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Images/Customer%20Segmentation.png?raw=true)
## PROJECT OVERVIEW
In this project, I have explored a sales dataset and performed various analyses and drew insights from customer's past purchase behavior by RFM technique customer segmentation using SQL and built a sales dashboard in Tableau.
## [SQL QUERY](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Customer_Segmentation.md)
## RFM ANALYSIS
![pic](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Images/RFM.png?raw=true)
* RFM is a data modeling method used to analyze customer value. 
* It stands for Recency, Frequency, and Monetary which are the three metrics that describe the customers. 
* It is an indexing technique that uses past purchase behaviour to segment customers.
#### `Recency`
* Last Order Date
#### `Frequency`
* Count of Total Orders
#### `Monetary`
* Total Money Spend

Sneak Peek into the RFM Segmentation Technique.
## For complete code, Click here -> [SQL QUERY](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Customer_Segmentation.md)
```sql
SELECT CUSTOMERNAME, rfm_recency, rfm_frequency, rfm_monetary, 
       CASE
	   WHEN rfm_cell_string in (111, 112 , 121, 122, 123, 132, 211, 212, 114, 141, 221) THEN 'Lost Customer'    -- lost customer.
	   WHEN rfm_cell_string in (133, 134, 143, 244, 334, 343, 344, 144) THEN 'Slipping Away'                    -- big spender, slipping away.
	   WHEN rfm_cell_string in (311, 411, 331, 421, 412) THEN 'New Customer'                                    -- new customer.
	   WHEN rfm_cell_string in (222, 223, 233, 322, 232, 234) THEN 'Potential Churners'                         -- probably leave the service.
	   WHEN rfm_cell_string in (323, 333,321, 422, 332, 432, 423) THEN 'Active'                                 -- customers who buy often at low price.
	   WHEN rfm_cell_string in (433, 434, 443, 444) THEN 'Loyal'                                                -- customers who buy regularly at high price.
       END
FROM #rfm
```
## [Tableau Dashboard](https://public.tableau.com/app/profile/arjunan.k.com/viz/CustomerSegmentationSalesDashboard/SalesDashboard1)
* Sales Dashboard 1

![pic](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Images/Sales%20Dashboard%201.png?raw=true)
* Sales Dashboard 2

![pic](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Images/Sales%20Dashboard%202.png?raw=true)

# <p align = 'center'>Business Solution for Better Retail Sales</p>
* Based on SQL Query
  * Customer Segmentation
  * Commonly Sold Together items.
* Based on Tableau
# <p align = 'center'>Thank You</p>
