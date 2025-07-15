# Artist-Album-sales-analysis

ANALYSIS OF ARTISTS, ALBUMS, MUSIC SALES, REVENUE GENERATED AND CUSTOMER BEHAVIOUR USING SQL

##INTRODUCTION

With the growing digitization of music, understanding consumer preferences and sales performance has become crucial for music businesses. This database simulates real-world sales and customer data for Geng Music Label in different countries. By analyzing it through SQL, we can evaluate both customer trends, artist and album performance globally.
### Problem Statement
- Which artists and albums generate the most revenue.
- Where top customers are located.
- Which genres or tracks are most popular.
- How spending varies across selected countries and orders.

### OBJECTIVES
- Analyze customer distribution and purchasing power across countries.
- Identify top-performing tracks, albums, and artists.
- Evaluate the genre spread and track volume.
- Provide business recommendation to optimize marketing, promotions and investments.

<img width="1374" height="699" alt="Dashboard 1-4" src="https://github.com/user-attachments/assets/3860cf73-cf2a-4519-b99f-27b2dbf7c9cd" />



### TOOLS USED
- SQLLITE
- Tableau



  ### Data Exploratory Data Analyst
  It includes some intresting code used in answering the questions.

1. To find all artist and their album, the subquery below was excuted:
````sql
select *,(select name from artist) Artist from album
````
2. To merge the First and Last name together and also retrive more information my each customer:
````sql
select firstname || '  ' || lastname Name, email, country, country 
from customer
````

3. To retrive all information of customers in only USA, LIMIT TO 10:
````SQL
SELECT * FROM CUSTOMER
WHERE COUNTRY IN (select country from customer
where country = 'USA')
ORDER BY FIRSTNAME DESC, LASTNAME ASC
LIMIT 10
````
4. To find the total number of customer in each country:
````sql
SELECT COUNTRY, COUNT(*)TOTAL
FROM CUSTOMER
GROUP BY COUNTRY 
ORDER BY TOTAL DESC
````
5. Top get 5 Customers who Have Spent the Most on purchases, the query below was used:
````sql
WITH highest as
(select firstname || '  ' || lastname name, round(sum(unitprice * quantity),0) top_purchase 
from customer c
left join invoice I
on c.customerid = i.customerid
join invoiceline iv
on i.InvoiceId = iv.InvoiceId
group by name)


select * from highest 
order by top_purchase desc
limit 5
````
6. Query that retrieves the following, total orders, the total sum spend,
minimum, maximum, and average spend on an order?
````SQL
With TotalOrderSpend AS (                                                  			
Select 			
  InvoiceId,                                                                                 		
  Sum(UnitPrice * Quantity) As TotalInvoice                             		
  From InvoiceLine			
  Group By InvoiceId                                                                                     
  )			
  Select 			
  Count(Invoice.InvoiceId) As Total_Orders,                                                    		
  Round(Sum(TotalOrderSpend.TotalInvoice),2) As Total_Sum_Spend,          			
  Round(Min(TotalOrderSpend.TotalInvoice),2) As Min_Sum_Spend,            			
  Round(Max(TotalOrderSpend.TotalInvoice),2) AS Max_Sum_Spend,           
  Round(Avg(TotalOrderSpend.TotalInvoice),2) As Avg_Sum_Spend
From Invoice 			
Join TotalOrderSpend on Invoice.InvoiceId = TotalOrderSpend.InvoiceId  
````

7. The total number of tracks available on each genre?
````SQL
WITH TOTAL_TRACK AS
(SELECT TRACKID, COUNT(*) COUNT, GENREID, NAME, COMPOSER 
FROM TRACK
GROUP BY NAME)

SELECT *
FROM TOTAL_TRACK 
ORDER BY COUNT DESC
````
8. Get information of invoices billed to the following European countries: in
Italy, Belgium, France, Sweden, Denmark, with their total revenue for each country
````SQL
select country, total, round(sum(unitprice * quantity), 0) total_revenue
from customer c
join invoice I 
on c.CustomerId = i.CustomerId 
join invoiceline iv 
on i.InvoiceId = iv.InvoiceId
where country in ('Italy', 'Belgium', 'France', 'Sweden', 'Denmark')
group by country
order by total_revenue desc
````

##Findings
- Invoice billed to belgium should be reviewed as it is higher than the other countries which is likely affecting its total revenue genarated.
- France Had the highest revenue of £195
- 'Tv show' had  the most tracks under genre.

  
## Recommendation

- Provide loyalty rewards to top-spending customers to enhance retention.
- Market high-performing tracks and albums through focused playlists or promotional campaigns.
- Increase distribution in significant markets, particularly in Europe and North America, where sales are robust.
- Leverage genre trends to inform future artist recruitment and marketing strategies.
- To enhance the analysis, we can incorporate time-based data (such as monthly sales figures) and monitor changes over time.


🙂
