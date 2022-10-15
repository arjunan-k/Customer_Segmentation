# <p align = 'center'>CUSTOMER SEGMENTATION ANALYSIS FOR RETAIL SALES</p>
![pic](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Images/Customer%20Segmentation.png?raw=true)
## PROJECT OVERVIEW
In this project, I have explored a sales dataset and performed various analyses and drew insights from customer's past purchase behavior by RFM technique customer segmentation using SQL and built a sales dashboard in Tableau. At the end, provided business solutions by analysing the segments of customers and products to improve the sales.
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
## For the complete code, Click here -> [SQL QUERY](https://github.com/arjunan-k/Customer_Segmentation/blob/main/Customer_Segmentation.md)
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


# <p align = 'center'>BUSINESS SOLUTIONS FOR THE CUSTOMER & PRODUCT SEGMENTATION</p>
After Customer Segmentation and Products Grouping using SQL, We will be having different segments of customers and groups of sold together products. 
So our aim is to bring back Customers and increase sales of brought together Products. 
I will be providing general business solution for retail sales along with our Vehicle Product Sales in data.

## CUSTOMER SEGMENTATION

### **1. Lost Customer**
  * Reach out to those customers and identify the reasons why they left?.
  * Discuss the problems they faced like Product Damage and Refund Issues.
  * Shifted their home - Provide items/products to their new location.

### **2. Slipping Away** (Big Spender)
* Hit them with new offers and discounts.
* Shifted their home - Provide items to their new location.
* Provide ease of purchasing - Digital Transactions Service. 

### **3. New Customer**
* Add points on each of their transactions to give them gift and vouchers after a certain limit.
* Ask for feedbacks and suggestions in customer service experience.
* Provide home/any location delivery.

### **4. Potential Churner**
* Hit them with new offers and discounts.
* Provide coupons for products they usually buy.
* Ask for feedbacks and suggestions.

### **5. Active Customer** (Buy often at low price)
* Provide Credit Billing Service, So they can purchase much better without worrying about money.
* Provide them more affordable discounts and products available in small quantity items(Low Price).
* Hit them with coupons for products they usually buy.

### **6. Loyal Customer** (Buy regularly at high price)
* Follow them monthly during their usual purchase dates.
* Provide them whatever they wish to buy, even if we are not providing such products.
* Provide home/any location delivery.


## PRODUCTS SOLD TOGETHER
* Add Combo Offers to such products.
* Set Remainder in Customers Profile, In case they miss to purchase their brought together products.
* Assign Sales Support Persons with good knowledge about that product in that brought together section to guide the customers.
* Arrange such products Closer.
* Show them other Replacement Options by other companies.
* Provide such items near Billing Sections, so that they can remember easily.

# <p align = 'center'>THANK YOU</p>
