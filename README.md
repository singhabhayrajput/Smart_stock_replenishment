
#                                      The stock replenishment 
It is an operation that consists in ordering more stocks in order to fulfill the customer demand.We have to provide a smart solution to it.

## Solution:

We will automate the replenishment process when it will hit the reorder point (also called reorder trigger level) and order some amount of product which will be targeted to last for 2 months.My solution consider a lot of variables which may not be necessary be cost effective.


## My solution is broken into two parts.

 ### 1.Calculating Reorder Point:

We will use object detection algorithms to count the number of item present in the store.Which will inform to our system about current number of objects present in the store(we will not count manually). When we will hit certain level(minimum level) we will reorder.
For better result we can use tensorflow's object detection API for object counting.

### 2.How Much Reorder:

This part of solution depends on forecasting product sell depending on season,holiday,days following pay day and so on.Here we will consider a lot of variable which can affect total amount of items.
## Algorithm used:
### 1st part:
### Object Detection Algorithm.
### 2nd part:

We will use time series and LSTM for forecasting our product in demand for two months; For this we will use dataset already provided on internet.Which will have its sell history(we will explore it and analyse it).
#### Note:

all dataset used is present in the same directory as this notebook.
Before diving into algorithm
My algorithm contain all the explanation which i have provided in the form of commnet. All you have to do is navigate through me.

### 1st part

### Processing sequence
Segmentation process can be parted into 3 parts:
1 — Pre-processing,
2 — Processing, and
3 — Post-segmentation.


### 1 — Pre-processing:
   First of all, we will convert our colored images to grayscale image, in order
to have only one channel image. Even without converting, we can observe
difference between these images characteristics. The first image         
contains small objects, and some have the same pixels values with the  
background. This aspect can cause the egdes detecting problem. 
So to prevent this, we think about image contrast adjustment, so we have to choose
among all contrast improving methods.


### 2  - Processing:

we have different segmentation techniques that can be grouped into two parts: 
edges based techniques and region based techniques.
Otherwise, we can use threshold techniques to do a segmentation, in this case 
we must follow other processing techniques in order to get satisfactory result.

### 3 — Post-segmentation.

  After the thresholding, we have many connected regions, this can not help us to count 
objects in the image cause the counting of objects is due to number of connected regions, so 
in addition, we have to apply some other techniques before count number of objects in the image.
We will go to follow erosion and dilatation techniques which will help us to connected 
nearest regions in order to have on region per object.


### Result

object counting become very essential for stock replenishment process when you dont know actual counting of your product in the stock and you have to count it every time by number manually. There are different software methods which can track number of product but i have used deep learning method. Benefit of this method is that it can ensure security and live counting,so you dont have to always update in your computer's database when some objects have taken out from stock.
Note
See 1st part show a initial process,advanced process include live cam detection and then updating software.For testing this i dont have enough hardware requirement but idea remain same.



## 2nd part

There are various time series algorithm which predict product sell like ARIMA,SARIMA,XGBOOST,LSTM,Prophet etc.But going thorugh a lot of articles i have found out deep learning predictions are really very accurate when we are dealing with multivariate time series. So in this part i will use LSTM.
###  dataset information:

### CSV Files Description:
sales_train.csv-the training set. Daily historical data from January 2013 to October 2015.
test.csv-the test set.in this we will to forecast the sales for these products for November 2015.
sample_submission.csv-a sample submission file in the correct format.
items.csv-supplemental information about the items/products.
item_categories.csv-supplemental information about the items categories.
shops.csv-supplemental information about the shops.
Field names
ID-an Id that represents a (Shop, Item) tuple within the test set
shop_id-unique identifier of a shop
item_id-unique identifier of a product
item_category_id-unique identifier of item category
item_cnt_day-number of products sold. You are predicting a monthly amount of this measure
item_price-current price of an item
date- date in format dd/mm/yyyy
date_block_num- a consecutive month number, used for convenience. January 2013 is 0, February 2013 is 1,..., October 2015 is 33
item_name-name of item
shop_name-name of shop
item_category_name-name of item category



## Inference

1.Things which do not impact performance at every month[it will be there for every month]: first day of month,saturdays and sundays,last day,monday. So if we see this constant booster is not going have much empact at monthly level(because it will be there for every month but certainly it will have impact on daily level but we are not calculating on daily level we are calculating for 3 months so we can neglect its impact.).

2.Things which impact performance at every month: season[winter,summer],Festival in a particular month,location of shop.

## Result
a)When there is sudden increase in a month it happen at every shop which indicate surely holdiay/Festival season for a retailer. which can be christmas,diwali,eid etc.
b)When there is sudden decrease in a month it happen at every shop which indicate a situation not suited for sell.
c)Every shop has different number of sold product depending on its location,friendeness with customer,easeness for customer and population beside that shop.
