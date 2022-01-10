# Aays-Analytics
Common mistakes made by a Power bi beginner & their best practice solutions 
1. Relying on the detect data type in power query to classify values of your dataset. 

The detect data type is a great feature, however, it does not always classify your data based on the context & you will always have to validate it. Let’s just say you have a table with two columns: Different pin codes & countries that the pins belong to. If you detect the data type of this table, the pin codes would be classified as whole numbers & countries as text. All good, right? Not really. https://www.aaysanalytics.com/azure-analytics-and-power-bi-services.html

 

Best practice: While it’s all right to classify ‘countries’ as text, it’s important to go to the data view & under column tools, make sure you classify this as a “Country” in the data category dropdown, again “Country” and not “County”. 

2. Replicating the data transformation steps of one table on another table by manual hard coding in the power query editor. 

Let’s say we have two tables with different information, but the data transformation steps applied are the same on both tables. The only thing that isn’t the same is the table name, so only one filter must be applied differently. Let’s call the first table ‘seasonal purchases’ & the other ‘non-seasonal purchases’. You have applied all the transformation-related steps & data filters on the seasonal purchases table. Now that you know what steps need to be applied on the non-seasonal purchases table, you go ahead & manually try to do the same operation on it, just by using a different filter while navigating to the table & giving the filter condition “contains non”. While this isn’t wrong, it’s laborious & takes time. 

 

Best Practise: Under the Home section of the power query editor, there is an option named “advanced editor”, click on it & copy the query for the seasonal purchases table. This has all the operations & steps applied on table 1, now select the non-seasonal purchases table, go to the advanced editor & paste the query here. Voila! You have the same data transformation steps applied on this table, now navigate to the step where the table name filter is applied & change the filtering condition & you are good to go. 

3. Loading multiple tables into the dashboard without establishing a relationship between them. 

In the initial phases, when we try to use multiple tables in a power bi report, we perform calculations on individual tables & lookup data from any other table if required, while this might not throw an error, but there are chances the resultant calculations aren’t always appropriate. 

 

Best Practise: It’s crucial to establish relationships between tables & have a robust data model. A complex data model might not always be the best, but it’s always recommended to relate the table based on primary key – foreign key relationship to accurately calculate results & have correct information in the report. Consider that we have two tables in a report: the first table is the customer master that has customer-related details along with product codes purchased by the customers, here the primary key is billing code or billing number. The second table is the product master, where the primary key is the product code. By navigating to the model section of the dashboard & clicking on the “manage relationships” option on the top, we can establish a many-to-one relationship between the customer master & the product master. Product code is a foreign key in the customer master table, so it might have multiple instances of the same code, but since it’s a primary key in the product master, each code will have only one instance (no duplication) & hence the nature of the relationship being “many-to-one”. 

4. Input the data source of the dashboard as the analytics workload space, rather than specifying the exact folder of the analytics workload space. 

Imagine that you are inputting data for your dashboard from the ADLS (Azure Data Lake Store) gen 2, the link to the ADLS is something of this sort: https://adlstest1.dfs.core.windows.net/You input this in the source & put it in the secret key, then filter out the folder in the data transformation steps, based on where your file is located. However, every time you make a change in the data in the power query editor & close & apply the change, it takes 30 minutes or more to reflect that change & refresh data, you wonder why. This is because power bi is having to run across the whole storage & find the folder that has the required data. 

 

Best Practise: Here, it’s important to get the exact path of the blob storage where your file is located & put that into the data source section. Rather than putting the path of the analytics workload space, search where your file is in ADLS, copy the folder path:https://adlstest1.blob.core.windows.net/Purchases/Nonseasonal/2020/Input this as the source & notice the refresh taking 1/4th the amount of time it previously took. This is because the folder path where the table is, is directly given & power BI doesn’t have to run through multiple filtering to get there. 

5. Using bold fonts & brighter colours to highlight essential components of the dashboard. 

Ever wondered why the Facebook logo is blue? Not the bright blue but the calm, subtle sky blue? This is because blue is a colour that’s very close to neutral & it imparts a sense of trust amongst digital users. Initially, we are tempted towards using brighter colours to highlight the key components & use bold font. We assume it makes things clearer & more noticeable. While it does make things noticeable, it’s a bit harsh on the eyes & might not be the best in every situation. 

 

Best Practise: Use colour palettes, it will reduce the number of contrasting colours on the power bi dashboard. Specify legends on the dashboard, so that the user is clear on what colour signifies what category. Make sure the legends are in proper font style & readable font size. I hope these learnings help you the next time you develop a power bi report. 

 
