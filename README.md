# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.

# PROGRAM:
```
Developed by: VAISHNAVI S
Register no: 212222230165
```
# CODE
```
# loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```
# removing unnecessary data variables
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
```
# detecting and removing outliers in current numeric data
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
# data visualization
# line plots
```
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
# Histogram
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
# count plot
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
# Barplot 
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
# KDE plot
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
# point plot
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
# Pie Chart
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
df4=df.copy()
```
# encoding
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])
```
# scaling
```
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
```
# Heatmap
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUPUT
![Screenshot 2023-05-16 110445](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/310c190d-78d8-45f9-a1c6-98a7b12459d7)

![Screenshot 2023-05-16 110455](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/ca6b68f7-6ecb-469f-a243-e693a5a46c6c)

![Screenshot 2023-05-16 110501](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/06333c1a-97cf-4191-b18d-2dd2614f694d)

![Screenshot 2023-05-16 110532](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/5aa61f6d-4e73-4ba4-afba-2b89480636f7)

![Screenshot 2023-05-16 110548](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/36fca48b-826b-47ff-8a1c-4b4b8b1f7b08)

![Screenshot 2023-05-16 110556](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/df4e89fb-5dbb-4361-a93b-b0190a0655b3)

![Screenshot 2023-05-16 110603](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/331cb8a7-40ad-4ca0-9d56-87ac1faf713c)

![Screenshot 2023-05-16 110611](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/2518038f-a582-4a3f-860f-1cf1d207cbb4)

![Screenshot 2023-05-16 110618](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/6616c4ed-517c-42ee-af42-6f4bce0525a2)

![Screenshot 2023-05-16 110626](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/97bbc0f2-3b8b-47f2-af90-48421852b2ac)

![Screenshot 2023-05-16 110633](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/9ca5f9c8-d086-4260-8f96-4aa4c3b8cdba)

![Screenshot 2023-05-16 110641](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/45a102c3-5e32-4196-9a71-195485611558)

![Screenshot 2023-05-16 110648](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/f90516bc-01fe-4a7b-ac6f-3853b872c8c7)

![Screenshot 2023-05-16 110705](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/f3a350b6-2aea-4db8-9114-735b9f1a424e)

![Screenshot 2023-05-16 110721](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/27e8e191-c739-45a3-8572-c90ecf7d1c39)

![Screenshot 2023-05-16 110735](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/abac0db6-bda3-4e23-b959-a6f43337c114)

![Screenshot 2023-05-16 110748](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/e4639716-f601-4274-9111-4bc72f318933)

![Screenshot 2023-05-16 110808](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/e03495a4-97c5-430a-bfb2-4dd50a4d2630)

![Screenshot 2023-05-16 110818](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/81460a8d-e770-4a7b-9114-5f60f2a4aa14)

![Screenshot 2023-05-16 110831](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/dacf2462-097e-4599-bcef-894f0b58e833)

![Screenshot 2023-05-16 110837](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/297d3e0d-0974-4868-8738-c9e2898834c0)

![Screenshot 2023-05-16 110846](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/c873f9c4-5c97-4be8-80f4-a2da897ac5d6)

![Screenshot 2023-05-16 110944](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/448cddab-7ce9-4256-a687-d2b7e3c12901)

![Screenshot 2023-05-16 110950](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/7c4c9196-7b5c-45a1-b4e7-c5dc87fef7b2)

![Screenshot 2023-05-16 110957](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/414b3f07-9bb4-4d43-81c0-0885062184b8)

![Screenshot 2023-05-16 111009](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/4d9e736a-59b1-4600-899e-79e5eca77b3c)

![Screenshot 2023-05-16 111022](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/7a563208-bc68-4f0c-aed7-e094f00928f5)


![Screenshot 2023-05-16 111030](https://github.com/Vaishnavi-saravanan/Ex-08-Data-Visualization_1/assets/118541897/c0ffc9a8-20eb-4d5d-8a63-3bbe851347ea)

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file
