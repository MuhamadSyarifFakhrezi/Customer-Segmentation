# Customer-Segmentation
## Business Understanding
The supperstore was looking to identify which customer segments to prioritize in their marketing efforts and which to avoid in order to increase their profitability. They needed data-driven insights to answer the following questions:
- Which customer segments are the most profitable?
- Which customer segments are at risk of unsubscribing?
- What marketing strategies work best for each segment?

By analizing the customer behavior, supermarkets may identify patterns and optimize their marketing efforts. Effective segmentation allows companies to allocate resources efficiently, focusing on high value customer and avoiding less profitable segments.

## Objective
The main objective of this project was to segment the customers based on their purchasing behavior characteristics. Using RFM (Recency, Frequency, Monetary) analysis and K-Means Clustering method leveraging RFM values and adding discount feature for more in-depth identification, this project aims to:
- Identify and prioritize high value customer segments.
- Highlight customer segments with low engagement or low profitablility, allowing it to re-evaluate its marketing strategy or reduce efforts towards less productive segments.
- Develop insight to create personalized marketing campaigns.

## Data Understanding
Superstore sales dataset from 2014 to 2017, which contains the following columns:
- Row ID => Unique ID for each row.
- Order ID => Unique Order ID for each Customer.
- Order Date => Order Date of the product.
- Ship Date => Shipping Date of the Product.
- Ship Mode=> Shipping Mode specified by the Customer.
- Customer ID => Unique ID to identify each Customer.
- Customer Name => Name of the Customer.
- Segment => The segment where the Customer belongs.
- Country => Country of residence of the Customer.
- City => City of residence of of the Customer.
- State => State of residence of the Customer.
- Postal Code => Postal Code of every Customer.
- Region => Region where the Customer belong.
- Product ID => Unique ID of the Product.
- Category => Category of the product ordered.
- Sub-Category => Sub-Category of the product ordered.
- Product Name => Name of the Product
- Sales => Sales of the Product.
- Quantity => Quantity of the Product.
- Discount => Discount provided.
- Profit => Profit/Loss incurred.

Data Source: [Dataset.csv](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

## Data Wrangling
- Ensure there are no duplicate data and null values
- Customize the data type
- Grouping features that will be used based on 'customer_id'
- Applied yeo-johnson transformation and standardization method to reduce skewness and outliers

## Exploratory Data Analysis
- How is the current sales performance?
  
![Revenue](https://github.com/user-attachments/assets/56bf7d3f-459a-49e3-94cf-d9f4023e825f)

The line plot above shows the revenue generated from 2014 to 2017 which has increased. Each year has a similiar pattern, with surges in April, October, and December.

![Profit](https://github.com/user-attachments/assets/0463ce8f-bbfd-44fd-8a73-587ef89b6596)

The lowest profitoccured in February 2015, and the highest one in January 2017. But what is interesting here, in months where revenue has always increased every year does not always have a surge in profit, perhaps due to marketing strategies that apply discounted prices or perhaps an increase in operating costs or caused by other factors, this needs to further analysis. Then at the end of 2017 also had sluggish profitability even though the revenue generated increased significantly.

![Categorical Distribution](https://github.com/user-attachments/assets/7c474c46-b3f8-4d66-86ad-4fced7f292fb)

The most customers are consumer, dominated by customers from the eastern and western region. Then the most sold product is the office supplies product category, while the standard delivery is the most commonly used delvivery type.

## RFM Analysis
With RFM anlalysis we can identify customer purchasing behavior in terms of this matrics: 
- Recency = When did the customer last make a purchase.
- Frequency = How often customers make purchases.
- Monetary = How much value for money do customers use to make purchases.

RFM score is defined with a value range of 1-5, with 1 being the lowest and 5 being the highest, with a weighting ratio:
- 20% for recency score.
- 30% for frequency score.
- 50% for monetary score.

From the resulting RFM score, it is then segmented into 4 segments:
- RFM score 3.76 - 5    ---> Top Customers
- RFM score 2.51 - 3.75 ---> High Value Customers
- RFM score 1.26 - 2.5  ---> Medium Value Customers
- RFM score 0 - 1.25    ---> Low Value Customers

![rfm](https://github.com/user-attachments/assets/dd1ce511-54e3-4646-b5c0-d65434389392)

Based on the ratio above, the most customer segments are high value customers. From the segmentation results, the question arises: 'What strategies can be done so that customers in the high value customer segment can turn into top customers?'

![dist_rfm_num](https://github.com/user-attachments/assets/f93ddb5c-c3c7-4d93-9191-e3c07f582553)

From the chart, it can be concluded that the higher the segment hierarchy, the higher the discount value used. Then this discount might be an attraction so that customers can transact more and more often.

## K-Means Clustering
K-Means Clustering is an unsupervised learning algorithm that can be used to group unlabelled data into K clusters (a specified number of clusters/segments) in such a way based on similar characteristics.

The K-Means algorithm has the following limitations:
- Very sensitive to outliers.
- Very sensitive to differences in data scale.
- Can only process numerical data.

Because the data set to be processed has a skewed distribution and there are quite a lot of outliers and has a much different scale, we transformed the data with the yeo-johnson transformation method and standardized it using the power transform from scikit-learn.

### Finding the optimal number of clusters
In the K-Means Clustering algorithm we need to find the optimal cluster in order to produce the best segmentation.
For that we use Elbow Method and Silouette Method.

![Elbow method](https://github.com/user-attachments/assets/891ee3ff-1039-499c-97a1-43851cd3bf53)

Based on the two charts above, seen from the most significant change in the value of inertia or the point of the number of clusters before the change in the value of inertia becomes sloping on the elbow method chart which usually forms an elbow, and reinforced by the silhouette method chart where the higher the silhouette coeffient value, the better the segment division, then the most optimal number of clusters is 4.

# Interpretation of Segmentation Results
We use snake plot to understand the difference between the segments.

![Snake Plot](https://github.com/user-attachments/assets/54f4d88c-703d-495b-9cdd-96a8e306d6c3)

Distribution of each segment:

![K-means](https://github.com/user-attachments/assets/59382539-992e-464f-b4ea-b910a10473eb)

## Summary

| Segment | Label | % | Interpretation | Actionable Insight |
| --- | --- | --- | --- | --- |
| 0 | Top Customers | 28% | Customers who are very loyal, tend to make large transactions, and often use discounts, this segment generates the most revenue. | Focus on increasing customer purchases, for that it is important to do cross selling or up selling strategies. |
| Medium Value Customers | 25% | Customers who rarely make transactions, the last purchase was also very long ago, but generate considerable revenue, and often utilize discounts. | This segment is prone to churn, so you should focus on activating them to make purchases again by designing Reactivation Strategy and Retention Strategy. |
| High Value Customers | 30% | Customers who frequently make transactions and have a huge potential to become ‘top customers’. These are customers who make the most recent purchases, and frequently make purchases, generate enough revenue, and rarely use discounts. | Business teams need to optimize marketing campaign resources for this segment to maintain loyalty and increase their value so that they can turn into top customers. |
| Low Value Customers | 16% | Customers who make the least transactions, last made a purchase a long time ago and generate the least revenue, and very rarely use discounts. | This is a low value segment, therefore resources are better allocated to conduct marketing campaigns on other segments so that resources can be utilized efficiently. |
