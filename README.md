# Frequent Pattern Mining for Pennsylvania Liquor Control Board

## Introduction

Frequent pattern mining is an analytical technique for finding relationships of items in a transactional database. Frequent patterns of buying behavior can be use to improve shelf arrangement and merchandise promotions. This mining technique is applied to get frequent patterns and association rules on the whole year 2018 transaction and sales data of Pennsylvania Liquor Control Board (PLCB). PLCB is a unique independent government agency acts as a retailer of liquor and wine, selling directyly to consumers via its over 600 states-run stores, as well as online wine shopping service. 

## Data

Data was provided by the PLCB on sales, marketing, products, and location of PLCB stores throughout the state of Pennsylvania. To implement frequent pattern mining, we focused on sales, transactions, and products data. We used the whole year 2018 transactional dataset which has more than 66 million transactions.

## Methods

The data mining algorithm of frequent patterns we applied is the frequnet pattern growth (FP-growth). FP-growth algorithm is efficient especially when dealing with big databases due to its ability of reducing computational loads. This algorithm has two steps: generate a FP-tree by mapping nodes to it from the transaction database, then extract the frequent itemsets from the FP-tree.

We used PySpark for application of this algorithm because of the magnitude of the dataset. The original transactional dataset is 28 GB so the efficiency of PySpark for big data analysis is what we needed, and the frequent pattern mining implementation in PySpark is comprehensive enough for our analysis.

## Results

By using the FP-Growth method on the class of items level, the frequent item sets are discovered. The top 15 frequent item sets are listed in the first plot. Notice that this frequency list did not consider the amount of goods, it only counted how many transactions contains this kind of items. The most popular item is Vodka, followed by Whiskey, Red Table Wine, and White Table Wine.

![plot 1](https://zhenghaoxiao32.github.io/Frequent-Pattern-Mining-for-PLCB/plots/plot1.PNG)

The next table shows the association rules derived from the transaction dataset of whole year 2018 with minimum support set to 0.003 and minimum confidence set to 0.7. Lifts of all the association rules are bigger than 1, indicates that there is a positive correlation among the items in the Antecedent and Consequent columns. 

Antecedent | Consequent | Confidence | Lift
------------ | ------------- | ----------- | -------------
Tequila, Liquor or Cordials, Rum, Whiskey | Vodka | 0.934 | 3.411
Tequila, Liquor or Cordials, Rum, Vodka | Whiskey | 0.917 | 4.333
Gin, Rum, Whiskey | Vodka | 0.899 | 3.282
Tequila, Liquor or Cordials, Rum | Vodka | 0.890 | 3.247
Tequila, Rum, Whiskey | Vodka | 0.879 | 3.211
Gin, Liquor or Cordials, Whiskey | Vodka | 0.876 | 3.199
Tequila, Liquor or Cordials, Rum | Whiskey | 0.873 | 4.123
Gin, Liquor or Cordials, Vodka | Whiskey | 0.860 | 4.065
Gin, Rum, Vodka | Whiskey | 0.848 | 4.006
Tequila, Liquor or Cordials, Whiskey | Vodka | 0.848 | 3.095
Tequila, Liquor or Cordials, Vodka | Whiskey | 0.840 | 3.967
Tequila, Rum, Vodka | Whiskey | 0.837 | 3.953
Tequila, Rum, Whiskey, Vodka | Liquor or Cordials | 0.834 | 10.799
Tequila, Liquor or Cordials, Whiskey, Vodka | Rum | 0.819 | 8.586
Liquor or Cordials, Rum, Whiskey | Vodka | 0.795 | 2.901
Liquor or Cordials, Rum, Vodka | Whiskey | 0.786 | 3.714
Tequila, Rum, Whiskey | Liquor or Cordials | 0.785 | 10.163
Tequila, Rum, Vodka | Liquor or Cordials | 0.761 | 9.852
Gin, Rum | Vodka | 0.757 | 2.766
Tequila, Liquor or Cordials, Vodka | Rum | 0.750 | 7.862
Tequila, Liquor or Cordials, Whiskey | Rum | 0.743 | 7.789
Liquor or Cordials, White Table Wine, Whiskey | Vodka | 0.736 | 2.686
Gin, Liquor or Cordials | Vodka | 0.729 | 2.661
Gin, Liquor or Cordials | Whiskey | 0.716 | 3.381
Gin, Rum | Whiskey | 0.715 | 3.376
Tequila, Rum | Vodka | 0.715 | 2.609
Liquor or Cordials, White Table Wine, Vodka | Whiskey | 0.714 | 3.372
Tequila, Whiskey, Vodka | Liquor or Cordials | 0.710 | 9.194

Within all the 28 association rules, Vodka shows up as a consequent in 11 rules, Whiskey shows up as consequent in 10 rules. Vodka and Whiskey are the top 2 most popular liquids in the itemset with frequencies of 27.4% and 21.2%. However, as the third and fourth most popular liquid, Red Table Wine and White Table Wine does not appeal much in the association rules. In detail, White Table Wine shows up twice as a component of the antecedents, Red Table Wine is absent in those association rules. Besides, there are 4 rules with a lift higher than 8 in which all the consequents are Liquor or Cordials that we should pay specific attention to.  

Aforementioned are results with items descripted by classes, we also wanted to know what the results would be when we apply a more detailed granularity. We combined sub-classes and classes as a more detail tag for the items. Here are the frequent pattern mining results based on this detailed tag: 

![plot 2](https://zhenghaoxiao32.github.io/Frequent-Pattern-Mining-for-PLCB/plots/plot2.PNG)

For sub-classes, accord with the result of classes, the top 5 most frequent items are still Vodka and Whiskey. In the generated association rules below, all the antecedent has two items and all the consequents are Unflavored Vodka and Whiskey. These results indicate that people who already purchased more than one item in their market basket will tend to purchase Vodka or Whiskey.

Antecedent | Consequent | Confidence | Lift
------------ | ------------- | ----------- | -------------
Schnapps Liquor or Cordials, Canadian Whiskey | Unflavored Vodka | 0.698 | 3.185
Unflavored Rum, American Whiskey | Unflavored Vodka | 0.690 | 3.150
Schnapps Liquor or Cordials, Canadian Whiskey | American Whiskey | 0.670 | 6.801
Irish Whiskey, American Whiskey | Unflavored Vodka | 0.664 | 3.033
Schnapps Liquor or Cordials, American Whiskey | Unflavored Vodka | 0.660 | 3.012
Unflavored Gin, American Whiskey | Unflavored Vodka | 0.647 | 2.954
Canadian Whiskey, Flavored Vodka | Unflavored Vodka | 0.645 | 2.944
Spiced Rum, American Whiskey | Unflavored Vodka | 0.639 | 2.919
Flavored Rum, American Whiskey | Unflavored Vodka | 0.635 | 2.900
Canadian Whiskey, American Whiskey | Unflavored Vodka | 0.619 | 2.827
Irish Whiskey, Unflavored Vodka | American Whiskey | 0.609 | 6.180
Flavored Vodka, American Whiskey | Unflavored Vodka | 0.581 | 2.655 
Schnapps Liquor or Cordials, Flavored Vodka | Unflavored Vodka | 0.580 | 2.649 
Spiced Rum, Unflavored Vodka | American Whiskey | 0.505 | 5.124

## Dicussion
We conducted the frequent pattern mining in the whole year 2018 transaction and sales data of PLCB. Two granularities were applied in the analysis: items by class and items by sub-class. Frequent item sets and association rules were mined by using FP-Growth algorithm to answer the question we set at the beginning. The main point we discovered in the association rules may help business decision making is that people who already purchased more than one item in their market basket will tend to purchase Vodka or Whiskey. 

In addition to this main discovery, these high lift rules should also be taking into consideration. Liquor or Cordials are the consequents of these rules, which means the customers have a strong pattern to buy Liquor or Cordials after buying the antecedents. Although Red Table Wine and White Table Wine are popular items themselves, they are not frequently bought together with other drinks. We believe all these findings can be business insights in coupons design, shelf arrangement, discount management to maximize the profit. 

For further work, there are two directions we can do. Firstly, the frequent pattern mining can be done in different scales. To enlarge the scale, a long-term analysis can be done using the sales and transaction data of the past decade. To downsize the scale, we can divide the analysis by location and time. Secondly, the main focus of this work is the most frequent items, which means the interesting but less frequent items are not taking into consideration. Thus, an interesting pattern mining can be done based on the same data to find those association rules that are not so frequent. 

## License
The contents of this repository are covered under the [MIT License](LICENSE).
