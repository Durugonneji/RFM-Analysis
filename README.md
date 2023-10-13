# RFM-Analysis
The given dataset is provided by an e-commerce platform containing customer transaction data including customer ID, purchase date, transaction amount, product information, ID command and location. The platform aims to leverage RFM (recency, frequency, monetary value) analysis to segment customers and optimize customer engagement strategies.

The task is to perform RFM analysis and develop customer segments based on their RFM scores. The analysis is to provide insights into customer behaviour and identification of high-value customers, at-risk customers, and potential opportunities for personalized marketing campaigns.

--to get frequency, recency  and Monetary value
with base as (
    select sum(TransactionAmount)as TotalTransaction,CustomerID,count(OrderID)as Frequency,datediff(day,max(purchaseDate),GETDATE()) as Recency
     
    from [RFM].[dbo].[rfm_data]
    group by CustomerID
)

select CustomerID,NTILE(5) OVER (ORDER BY Frequency DESC) as F,NTILE(5) OVER (ORDER BY Recency DESC) as R,NTILE(5) OVER (ORDER BY TotalTransaction DESC) as M
from base

	   --stuck here
	  
