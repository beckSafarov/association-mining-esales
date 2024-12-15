## 1. Introduction

“Customer purchase behavior - Electronic Sales Data” is a dataset downloaded from kaggle.com. It shows sales transactions records for an electronics company from September 2023 to 2024. Since the dataset contains detailed information about customer demographics, product types, and purchase behavior, it allows conducting association mining, clustering and classification analysis.

The project conducts an association mining algorithm to identify potential relationships between purchased product types, such as smartphones, tablets, laptops, with the purchased add-ons.

Link to dataset:

https://www.kaggle.com/datasets/cameronseamons/electronic-sales-sep2023-sep2024

## 2. Description of the Exploratory Data Analysis

Dataset consists of 20,000 rows and 16 columns (Appendix 1). Below are the detailed information about some observations and explorations of the dataset.

## 1. Columns and data types.


| Column | Dtype |
| -- | -- |
| customer id | int64 |
| age | int64 |
| gender | object |
| loyalty member | object |
| product type | object |
| sku | object |
| rating | int64 |
| order status | object |
| payment method | object |
| total price | float64 |
| unit price | float64 |
| quantity | int64 |
| purchase date | object |


### Table 1.Columns and data types

2. Distribution of various values. As can be seen below, genders are almost equally distributed between males and females. Most customers (78.3%) do not have Loyalty Memberships, and most orders (67.2%) are completed. Credit Card and Paypal are the most popular payment methods (around 29% each).

<!-- Loyalty Distribution No 21.7% Yes 78.3%  -->
![](https://web-api.textin.com/ocr_image/external/396fc530f91040ca.jpg)

<!-- Gender Distribution Male Female 49.2% 50.8%  -->
![](https://web-api.textin.com/ocr_image/external/58edbd473f376acf.jpg)

<!-- Order Distribution Completed Cancelled 32.8% 67.2%  -->
![](https://web-api.textin.com/ocr_image/external/e2cd96cf33fb94cb.jpg)

<!-- Payment Method Distribution Credit Card PayPal 29% 29.3% Bank Transfer Cash Debit Card 16.9% 12.4% 12.5%  -->
![](https://web-api.textin.com/ocr_image/external/148550eb41470886.jpg)

Figure 1-4. Distributions of Gender, Loyalty, Order and Payment Methods

3. Correlations between different numeric values. The below figure shows that there are no significant correlations between any of the numerical fields, except for the obvious correlations between unit & total pricing, quantity & total pricing, etc.


|  | age | rating  | total price |  unit price | quantity |  add-on total |
| -- | -- | -- | -- | -- | -- | -- |
| age | 1.000000 | 0.002995 | 0.003036 |  -0.004384 | 0.008461 | -0.005357 |
| rating | 0.002995 | 1.000000 | -0.232401 |  -0.343845 | -0.008530 | -0.044301 |
| total price | 0.003036 | -0.232401 | 1.000000 | 0.673984 | 0.653851 | 0.083876 |
| unit price | -0.004384 |  -0.343845 | 0.673984 | 1.000000 | 0.006739 | 0.125209 |
| quantity | 0.008461 |  -0.008530 | 0.653851 | 0.006739 | 1.000000 | 0.003336 |
| add-on total |  -0.005357 |  -0.044301 | 0.083876 | 0.125209 | 0.003336 | 1.000000 |


Figure 5.Correlations between the numerical fields

## 4.Measures of Central Tendency.


|  | age | rating | unit price | total price | add-on total |
| -- | -- | -- | -- | -- | -- |
| count  | 20000.000000 | 20000.000000 | 20000.000000 | 20000.000000 | 20000.000000 |
| mean | 48.994100 | 3.093950 | 578.631867 | 3180.133419 | 62.244848 |
| std | 18.038745 | 1.223764 | 312.274076 | 2544.978675 | 58.058431 |
| min | 18.000000 | 1.000000 | 20.750000 | 20.750000 | 0.000000 |
| 25% | 33.000000 | 2.000000 | 361.180000 | 1139.680000 | 7.615000 |
| 50% | 49.000000 | 3.000000 | 463.960000 | 2534.490000 | 51.700000 |
| 75% | 65.000000 | 4.000000 | 791.190000 | 4639.600000 | 93.842500 |
| max | 80.000000 | 5.000000 | 1139.680000 | 11396.800000 | 292.770000 |


Figure 6.Statistical results of numerical columns

The main findings from the above figure are as follows:

1. Customers are on average 48 years old, and the interquartile range of the age values also shows that most customers tend to belong to older age groups.

2. Product prices range from &#36;20 to &#36;1139, while average price of add-ons are &#36;62

3. Average rating of products are 3/5.

## 3. Dataset Preparation

### 3.1.Cleaning

1. In the payment methods column, inaccurate and redundant category name(Paypal)was renamed to the correct one (PayPal) to accurately demonstrate data distribution in the column(Annex 2)

2. In the add-ons purchased column duplicate values were removed (Annex 3 and 4)

3. In the add-ons purchased column NaN values were removed (Annex 5)

4. Purchased products and add-ons were combined to a list

### 3.2. Transformation

product type column, which shows a product purchased by a customer was merged together with add-ons purchased column into a transactions list (Figure 7). This list consists of rows of transactions that show purchases made by the customer.


| print(transactians) |
| -- |
| Il"Smartphone',"Accessory",'Tablet',"Inpulse Item"],["Laptop", "Snartphone',"Inpulse Item"],["Smartphone",'Accessory'],['Smartphone',"Accessory',"Inpulse Item"],I"Smartwatch","Laptop","Extended Marranty"],I"Seartghone","Ingulse Item', "Laptop', "Tablet", 'Accessory"."Inpulse Item"], I"Smartphone',"Accessery","Extended Marranty"l,I"Smartwatch","Extended Warranty',"Inpulse Item"], I'Smartghene','Accessory'l, I'Snartphone','Accessory','Inpulse Item'1,I'Snartwatch',' ,Accessorv'], {'Smartphone'], I'Smartphone', 'Extended Warranty','Inpulse Item'], I'Saartphone', 'Tablet', 'Inpulse Item', 'Smartwatch','Accessery'1,l'Smartwatch","Accessory",'Extended Marranty","Inpulse Item"],I"Smartwatch","Accessary',"Extended Marranty'],['Smartwatch",'Accessory','Impulse Item'],I'Snartphone','Extended Warranty", 'Impulse Item'], I'Laptop",'Smartphone','Extended Warranty'],I'Smartphone'],Accessory'1,I'Smartphone', "Smartphone', 'Accessery'], ('Smartphone', 'Extnded Marranty', "Inpulse Item', 'Smartphone'], I"Smartwatch", 'Extended W,'Extended Warranty'),['Tablet"], I'Seartp"Extended Marranty'],["Ssartphone",'Inpulse Iten',"Ssartwatch","Accessory",'Extended Marranty','Inpulse Item'],I'Smartphone'l,I"Tablet',"Accessary',"Inpulse Item"],I"Tablet'],I'Snartghone,"Accessary','Inpulse Item'],I'Seartwatch','Accessory'],ary',"Extended Warranty'],I'Smartwatch',"Tablet",'Acce ,'Inpulse Item','Smartphone'].['Laptep', "Extended Marranty', "Laptop', 'Extended Warranty"],I'Laptop', "Accessory', "Extended Marranty', "Inpulse Item', 'Tablet', "Inpulse Itepulse Iten'],["Laptop","Smartphone', ended Marranty'],I'Smartphone','Accessory',"Extended Marranty','Inpulse Item','SmartphoneExtended Marranty','Inpulse Ite'1,I'Tablet','Smartwatch','Accessery','Inoulse Item:],I'Smartphene','Accessery','Extended Harranty'1.<img src="https://web-api.textin.com/ocr_image/external/2450b0e1c179490f.jpg"> |


Figure 7. Forming a transactions list

This list was then encoded into a dataframe that contains boolean encodings of purchased products and add-ons.

[261:from mlxtend.preprocessing import TransactionEncoder

from mlxtend.frequent_patterns import apriori,association_rules

(27): te=TransactionEncoder()

te_arr=te.fit_transform(transactions)

df_encoded=pd.Datafrane(te_arr,columnsete.columns_)

df_encoded

(27):


|  | Accessory | Extended Warranty | Impulse Item | Accessory | Extended Warranty | Headphones | Impulse Item | Laptop | Smartphone | Smartwatch | Tablet |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 0 | False | False | False | True | False | False | True | False | True | False | True |
|  | False | False | False | False | False | False | True | True | True | False | False |
| 2 | False | False | False | True | False | False | False | False | True | False | False |
| 3 | False | False | False | True | False | False | True | False | True | False | False |
|  | False | Ag |  | Fals | True- | False | False | True | False | True | False |
|  |  |  |  |  |  |  |  |  |  |  |  |
| 12130 | True | True | False | True | False | False | False | False | True | False | False |
| 12131 | False | True | False | True | False | Faise | False | False | False | False | True |
| 12132 | False | False | False | False | False | Faise | False | True | False | False | False |
| 12133 | True | True | True | False | True | True | True | True | True | False | False |
| 12134 | True | False | False | False | True | True | False | Faise | False | False | False |


Figure 8. List is encoded into a dataframe

## 4. Justification of ML Algorithms

Three most popular algorithms have been applied and compared in the project:

1.Apriori is an unsupervised ML algorithm proposed in 1994 (Noble, 2024). It is best applied with transactional databases and often used for market basket analysis to support recommendation systems. Its main advantage is in its simplicity and adaptability.

2.FP-Growth is considered to be an efficient and scalable method for mining the complete set of frequent patterns (Javatpoint, 2024). Its main advantage over Apriori algorithm is that it adopts a more sophisticated approach that dramatically reduces computational complexity (Herath, 2024).

3.ECLAD is a depth-first search-based approach for finding frequent itemsets (BetterLife, 2024). It is considered to be faster than Apriori for dense datasets with low minimum support thresholds.

### Parameters

Since the dataset contains 20,000 rows consisting of transactions, on average 2-3 items per row, 1% has been set as the support threshold.

### Evaluation

The algorithms have been evaluated in terms of the number of frequent itemsets, maximum support, maximum confidence, memory usage and runtime.


| Algorithm | Num FrequentItemsets | Max Support | MaxConfidence | Memory Usage  | Runtime |
| -- | -- | -- | -- | -- | -- |
| Apriori | 392 | 0.452163 | 0.825301 | 72.8125 | 0.076691 |
| FP-Growth | 392 | 0.452163 | 0.825301 | 1.46875 | 0.044397 |
| ECLAT | 48 | 0.298915 | 0.462532 | 31.9375 | 4.070816 |


Table 2. Evaluation of algorithms on the support threshold of 1%

## 5. Conclusion

## Itemsets

There was found a strong dependency between Impulse Item & Accessories (lift score 3.8x threshold, confidence 13%), and Smartwatch and Headphones (lift score 3.8x threshold,confidence \~36%) (Appendix 7).

In addition, there was a significant relationship between Smartphone, Tablet and Smartwatch. Lift and conviction scores support that to (Appendix 8)

## Algorithms

Comparing the algorithms, below were the findings:

1.Apriori Algorithm performed far worse than two other algorithms in terms of memory usage

2.FP-Growth algorithm significantly less memory, run fastest and showed exactly the same number of frequent itemsets, maximum support and maximum confidence as the Apriori Algorithm

3.Probably due to the dataset not being dense enough, ECLAD algorithm was the slowest while not producing as many frequent itemsets as the two other algorithms

## Post-processing

The techniques used in the project could be deployed as an API to a cloud server, using AWS S3, Lambda and similar services.

Monitoring process should ensure that support, confidence and lift values remain valid and they drop dramatically, then the rules should most likely be reworked.

If transaction patterns drift considerably, then the model might need retraining.

## Bibliography

1.Noble, J. (2024) What is the apriori algorithm?, IBM. Available at:https://www.ibm.com/topics/apriori-algorithm (Accessed: 06 December 2024).

2.FP growth algorithm in Data Mining - Javatpoint (no date) www.javatpoint.com.Available at: https://www.javatpoint.com/fp-growth-algorithm-in-data-mining (Accessed: 06 December 2024).

3.Herath, S. (2024) FP-growth algorithm in Data Mining, Medium. Available at:https://medium.com/image-processing-with-python/fp-growth-algorithm-in-data-minin g-e1064accf6a3 (Accessed: 06 December 2024).

4.BetterLife. “Eclat Algorithm in Machine Learning - BetterLife - Medium.” Medium, 12Sept. 2023,

quality-life.medium.com/eclat-algorithm-in-machine-learning-fe07d33fcc5b. Accessed 6 Dec. 2024.

## Annex


| df.shape |
| -- |


[6]: (20000,16)

## Annex 1. Gender distribution

[15]: df['payment method'].value_counts(normalize=True)

[15]: payment method

Credit Card 0.29340

Bank Transfer 0.16855

PayPal 0.16420

Paypal 0.12570

Cash 0.12460

Debit Card 0.12355

Name: proportion, dtype: float64

[16]:df['payment method'] = df['payment method'].replace({'Paypal':'PayPal'})

Annex 2. Renaming redundant category names


| age |  gender | loyaltymember | producttype | sku |  rating | orderstatus | paymentmethod | totalprice | unitprice | quantity | purchasedate | shippingtype | add-ons purchased | add-0ntotal |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 53 | Male | No | Smartphone | SKU1004 | 2 | Cancelled | CreditCard | 5538.33 | 791.19 | 7 | 2024-03-20 | Standard | Accessory,Accessory,Accessory | 40.21 |
| 53 | Male | No | Tablet | SKU1002 |  | Completed | PayPal | 741.09 | 247.03 |  | 2024-04-20 | Overnight | Impulse Item | 26.09 |
| 41 | Male | No | Laptop | SKU1005 |  | Completed | CreditCard | 1855.84 | 463.96 |  | 2023-10-17 | Express |  | 0.00 |
| 41 | Male | Yes | Smartphone | SKU1004 |  | Completed | Cash | 3164.76 | 791.19 |  | 2024-08-09 | Overnight | Impulse Item,Impulse Item | 60.16 |
| 75 | Male | Yes | Smartphone | SKU1001 | 5 | Completed | Cash | 41.50 | 20.75 |  | 2024-05-21 | Express | Accessory | 35.56 |


### Annex 3.add-ons purchased column before preprocessing included

### duplicates

[23]: # Cleaning up duplicates in 'add-ons purchased'

<!-- df.loc[t,'add-ons purchased']=df.loc[:,'add-ons purchased'].fillna('').apply( Lambda x:''.join(set(x.split(','))) if x else  -->
![](https://web-api.textin.com/ocr_image/external/275afa124e348da4.jpg)


| [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() | [24]: df.head() |  |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| [24]: | customer년 | age | gender | loyaltymember | producttype | sku  | rating | orderstatus | paymentmethod | totalprice | unitprice | quantity | purchasedate | shippingtype | add-onspurchased | add-ontotal |
|  | 1000 | 53 | Male | No | Smartphone | SKU1004 | 2 | Cancelled | CreditCard | 5538.33 | 791.19 |  | 2024-03-20 | Standard | Accessory | 40.21 |
| 1 | 1000 | 53 | Male | No | Tablet | SKU1002 | 3 | Completed | PayPal | 741.09 | 247.03 |  | 2024-04-20 | Overnight | ImpulseItem | 26.09 |
| 2 | 1002 | 41 | Male | No | Laptop | SKU1005 | 3 | Completed | CreditCard | 1855.84 | 463.96 |  | 2023-10-17 | Express |  | 0.00 |
|  | 1002 | 41 | Male | Yes | Smartphone | SKU1004 | 2 | Completed | Cash | 3164.76 | 791.19 |  | 2024-08-09 | Overnight | ImpulseIter | 60.16 |
|  | 1003 | 75 | Male | Yes | Smartphone | SKU1001 | 5 | Completed | Cash | 41.50 | 20.75 |  | 2024-05-21 | Express | Accessory | 35.56 |


Annex 4. add-ons column after preprocessing: removed duplicates

# Filling up empty column cells with empty string

df.loc[:, 'add-ons purchased"]= df.loc[:, 'add-ons purchased'].fillna()

df[['add-ons purchased']]

<!-- add-ons purchased 0 Accessory Impulse Item 2 3 Impulse Item 4 Accessory --* - 19994 19995 19996 19997 Accessory,Impulse Item,Extended Warranty 19998 Extended Warranty,Accessory  -->
![](https://web-api.textin.com/ocr_image/external/386839d820f19634.jpg)

Annex 5. add-ons column NaN values removed


| [25): | Step 31 Combine product and add-on Jnte one listdfl'transaction']=df.applytLanbda roui [rowl'product type'll+(rowl'add-ons purchased"l.spliti","}if rowl'add-ons purchased']else (1),axis=1#Step 4: Group by customer_id to create transactionstransactions=df.groupby('customer id')["transaction').apply(lanbde xi liten fer sublist in x fr iten in sublist)),tolist()printitransactions) |
| -- | -- |
|  | Il'Smartphone","Accessory', "Tablet",'Inpulse Item'], ['Laptop', "Smartphone', 'Inpulse Item'],["Smartphone',"Accessory'],["Smartphone',"Accessory',"Inpulse Item'), I"Smartwatch","Laptop', "Extended Warranty"), I"Smartphone', 'Inpulse Item',"Laptop', "Tablet','Accessory","Impulse Item'],("Smartphone","Accessory","Extended Marranty"], I"Smartwatch","Extended Marranty","Inpulse Item'], I"Smartphone','Accessory'1,I'Smartphone","Accessory","Inpulse Item'],I"Smartwatch',"Extended Marranty","Snartphone", "Accessory'],I"Smartphone",'Accessory'1.I'Smartphone'],['Smartphone","Extended Marranty',"Inpulse Item'],["Smartphone',"Tablet", 'Inpulse Item', 'Snartwatch',"Accessory'1,['Smartwatch',"Accessory',"Extended Marranty',"Inpulse Iten'],I'Snartwatch',"Accessory","Extended Marranty"], I"Smartwatch','Accessory',"Impulse Item'],I"Smartphone','Extended Marranty",'mpulse Item'],["Laptop',"Smartphone',"Extended Marranty"], I"Smartphone'],'Smartwatch"],I"Smartwatch ssory'],I"Tablet","Smartphone",'AccessorI'Smartwatch','Extended Wy'1,['Smartghone', "Smartphone', 'Accessery'), !'Snartphone', 'Extended Warranty', 'Inpulse Item', 'Smartphone'],['Sarranty', 'Smartwatch', "Smartphone', "Accessory', 'Extended Marranty', "Ssartphane', 'Accessary','Extended Warranty"],I'Tablet'],I'Smartphone','Accessory': 'Extended Warranty'], I'Ssartphone', 'Inpulse Itea', "Snartwatch', 'Accessary', "Extended Warranty', 'Impulse Item'], I'Smartphone'l,['Tablet','Accessory','Impulse Item'], l'Tablet'], I'Ssartphone', 'Accessory', 'Inpulse Item'],['Smartwatch','Accessery'],I'Laptop','Accessory', 'Inpulse Itea'], I'Ssartphane', 'Extended Marranty','Inpulse Item'], I'Laptop', 'Accessory', 'Extended Warranty'],I'Snartwatch', 'Tablet', 'Accessory', 'Extended Warranty', 'Inpulse Item'], I'Snartghone','Accessory', "Impulse Item', 'Smartphone'], I'Laptop', 'Extended Marranty', 'Laptop', 'Extended Marranty*],I'Laptap', 'Accessory', "Extended Marranty', 'InpulseItem','Tablet','Impulse Ite','Smartphone','Inpulse Item'), ('Tablet', 'Impulse Item', 'Laptop', 'Accessery','Inpulse Item'), I"Smartghone','Extended Warranty',"Imm',"Sma"Smartphone","Accessory","Extended Marranty", "Inpulse Item', "Smartphone",Extended Warranty',"Inpulse Iten"],I"Tablet",'Snartwatch',"Accessory',"Impulse Item"],I"Snartphone","Accessory","Extended Warranty"1. |


[83]: List

Annex 6. Transactions containing product type and add-ons purchased

columns


|  | antecedents |  consequents | antecedentsupport | consequentsupport | support |  confidence | Eift | leverage |  conviction  | zhangs_metric |  antecedent_length |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 1459 | (Accessory,Impulse item) | (Smartwatch,Headphones) | 0.078451 | 0.029254 | 0.010466 | 0.133403 | 4.560140 | 0.008171 | 1.120182 | 0.847170 | 2 |
| 1454 | (Smartwatch,Headphones) | (Accessory.Impulse Item) | 0.029254 | 0.078451 | 0.010466 | 0.357746 | 4.560140 | 0.008171 | 1.434868 | 0.804236 | 2 |
| 1500 | (Laptop,Headphones) | (ExtendedWarranty,Impulse Item) | 0.030902 | 0.076143 | 0.010466 | 0.338667 | 4.447749 | 0.008113 | 1.396961 | 0.799886 | 2 |
| 1609 | (ExtendedWianndu | (Laptop, | 0.078149 | nn20009 | 0 01nA68 | 0127448 | AAATTAO | 0.000112 | 1199631 | n020nce |  |


Annex 7.Association Rules for the Electronics Dataset based on Apriori algorithm


|  | antecedents | consequents | antecedentsupport | consequentsupport | support  | confidence | lift | leverage | conviction | zhangs_metric | antecedent_length |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 1459 | (Accessory,Impulse Item) | (Smartwatch,Headphones) | 0.078451 | 0.029254 | 0.010466 | 0.133403 | 4.560140 | 0.008171 | 1.120182 | 0.847170 | 2 |
| 1454 | (Smartwatch,Headphones) | (Accessory,Impulse item) | 0.029254 | 0.078451 | 0.010466 | 0.357746 | 4.560140 | 0.008171 | 1.434868 | 0.804236 | 2 |
| 1500 | (Laptop,Headphones) | (ExtendedWarranty,Impulse iter) | 0.030902 | 0.076143 | 0.010466 | 0.338667 | 4.447749 | 0.008113 | 1.396961 | 0.799886 | 2 |
| 1503 | (ExtendedWarranty,Impuise Item) | (Laptop,Headphones) | 0.076143 | 0.030902 | 0.010466 | 0.137446 | 4.447749 | 0.008113 | 1.123521 | 0.839056 | 2 |
| 1539 | (Smartphone,Headphones) | (ImpulseItem,Impulseitem) | 0.029254 | 0.078863 | 0.010218 | 0.349296 | 4.429158 | 0.007911 | 1.415600 | 0.797555 | 2 |
| - |  |  |  | -- | -- |  |  | - | -- |  | - |
| 1876 | (Smartwatch,ExtendedWarrantyImpulse Item, | (Tablet) | 0.044994 | 0.305562 | 0.016564 | 0.368132 |  1.204768 | 0.002815 | 1.099023 | 0.177972 | 4 |
| 1466 | (impulseItem,Laptop) | (Accessory,Impulse item) | 0.149650 | 0.078451 | 0.014091 | 0.094163 | 1.200281 | 0.002351 | 1.017346 | 0.196227 | 2 |
| 1465 | (Accessory,Impulse Item) | (ImpulseItem,Laptop) | 0.078451 | 0.149650 | 0.014091 | 0.179622 | 1.200281 | 0.002351 | 1.036534 | 0.181067 | 2 |
| 110 | (Accessory) | (Accessory,Laptop) | 0.163082 | 0.149485 | 0.029254 | 0.179384 | 1.200011 | 0.004876 | 1.036434 | 0.199152 |  |


Annex 8.Association Rules for the Electronics Dataset based on Apriori

algorithm



