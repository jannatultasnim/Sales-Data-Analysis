# Sales-Data-Analysis
This sales data analysis project has been done using jupyter notebook, pandas and matplotlib
and 12 Different datasets has been used for the analysis each data sets contains monthy sales data info along with the product name, order id, order amount, shipping addresses, order date and time
This analysis on the sales data will help business to get answers of few important questions:
1. which month has the highest sales rate?
2. Which city has the highest number of sales?
3. Which time should we display our product advertisement to increase the likelyhood of customer buying products
4. what products are most often sold togather?
5. What product sold the most and why do u think it sold the most?
------------------------------------------------------------------------------
First import these 2 pyhton library
import pandas as pd
import matplotlib.pyplot as plt
import os #reference https://stackoverflow.com/questions/10377998/how-can-i-iterate-over-files-in-a-given-directory
from itertools import combinations
from collections import Counter

Task1-------------------------------------------------------------------------: 
Merging All the datasets of each months sales data in to a single dataset

df  = pd.read_csv('./Sales_Data/Sales_April_2019.csv')

#CREATE EMPTY DATAFRAME

#reference https://stackoverflow.com/questions/55652704/merge-multiple-dataframes-pandas

all_month_data = pd.DataFrame()

#Loop over the files in a directory

files = [file for file in os.listdir('./Sales_Data')]

for file in files:

    df  = pd.read_csv('./Sales_Data/'+file)

    all_month_data = pd.concat([all_month_data,df])

​

all_month_data.to_csv('all-month-data.csv',index=False)
------------------------------------------------------------------------------------------
Read the updatated data set created on the first task

all_new_data = pd.read_csv('all-month-data.csv')

all_new_data.head(6)
Task 2=====================================================================================:
Clean the Data set
#all_data = all_data[all_data.isnull().any(axis=1)]
Task 3=====================================================================================:

#Add month column
all_new_data['Month']=all_new_data['Order Date'].str[:2]
all_new_data.head()

add sales cloumn to our data frame

#convert quantity column and price each column in to correct data type

#using pd.to_numeric method 

all_new_data['Quantity Ordered']=pd.to_numeric(all_new_data['Quantity Ordered'])

all_new_data['Price Each']=pd.to_numeric(all_new_data['Price Each'])
all_new_data['Sales']=all_new_data['Quantity Ordered']*all_new_data['Price Each']
all_new_data

Task 4 ===================================================================================:
add a city column in our sales dataset

#use the .apply() method with lambda funtion

#create city column

def get_city(address):

    return address.split(',')[1]

def get_state(address):

    return address.split(',')[2].split(' ')[1]

all_new_data['City'] = all_new_data['Purchase Address'].apply(lambda x: f"{get_city(x)} ({get_state(x)})")

all_new_data.head()
==========================================================================
convert the order date column in to date type object:

all_new_data['Order Date']=pd.to_datetime(all_new_data['Order Date'])
all_new_data.head()
===========================================================================
Months with sales reates bar chart

![image](https://user-images.githubusercontent.com/59441768/152639499-213fab15-6c85-4ad6-ac43-543f73731f2b.png)

city with highest sales


![image](https://user-images.githubusercontent.com/59441768/152639589-4eddda5a-3272-40ad-b4a5-fc7f9bb4037c.png)


time should we display our product advertisement to increase the likelyhood of customer buying products


![image](https://user-images.githubusercontent.com/59441768/152639673-7422dcc1-e769-4420-ad41-44453954c7ce.png)


product sold the most and why


![image](https://user-images.githubusercontent.com/59441768/152639694-2e0b94a8-30a4-4f84-9594-17a01d55e5d6.png)


![image](https://user-images.githubusercontent.com/59441768/152639710-42544eba-ff08-48d3-9557-4949feb115b9.png)



