# Load Data from a file using a Notebook

Notebooks are not a new invention, they are a well established tool for working with data using Apache Spark. In this lab we are going to create a notebook that does some minor transformations and then loads the data into a table.

This lab only covers the very basics, to learn more take a look at [Notebooks n Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-engineering/how-to-use-notebook)

### Create the Notebook

The notebook is a getting data so it belongs in the Get Data task. Click New item in the Get data task. From the items that appear on the right select Notebook. 

When the notebook appears it will be called Notebook 1 or something similar. It is good practice to name each item before you get so many you no longer can keep track. Click on the name and in the drop down type in a name. I have entered Load Finance Customers

![The Get data task with New item highlighted with an arrow pointing to Notebook tile. And a screen grab showing how to rename the notebook](<Images/Lab 01/2024-08-06_17-26-24.png>)

Notebooks are made up of blocks or Markdown and code. Markdown is great to document the notebook. Each code block can be run one at a time or all of them.

## Connect the Lakehouse

The notebook needs to be connected to the Lakehouse in order to access the files and tables. In the Explorer pane on the left, click on Lakehouses. When the empty pane appears, click Add. This will show a dialog asking if its an existing lakehouse, click Add.

The next view is the OneLake data hub. A notebook can be connected to a Lakehouse from another workspace so all workspaces that you have access to will be shown. Find your lakehouse and select it. Click add and that lakehouse should now be shown in the explorer pane.

![Images showing the above steps in the previous 2 paragraphs](<Images/Lab 01/2024-08-06_17-48-33.png>)

## Load the files

Firstly we need to load the file data into a dataframe. This is how notebooks handle data. They have made this simple and it does not require knowing spark.

In the lakehouse click on the Finance folder, this will open another pane showing the files. Drag the Customers.csv file into the white space below the current code block. 

This will create a 3 line code block. The first line loads the csv data into a dataframe called df. Line 2 is a comment that explains what line 1 is doing. Line 3 prints out the contents of the dataframe, df.

![Screen grab of the notebook showing the two panes that allow you select a folder and then see the files and the code created created by dragging the file into the notebook. It then shows the results of pressing the play button](<Images/Lab 01/2024-08-06_18-06-34.png>)

We can execute the code block by clicking the play arrow to the top left of the code block. The results will be shown below. The first time you execute code it takes a little longer as it starts up a spark session.

## Use Data Wrangler to add transformations

Our data has some issues. Cust Number contains a space and Location contains two pieces of information, city and region. So we need some simple transformations performed. If we knew Spark we could write the code, but there is a low-code solution called Data Wrangler.

From the top ribbon click on Data Wrangler and from the Spark Dataframes click on df. If no dataframes are listed, run the previous block of code to populate the df dataframe. Data Wrangler should appear.

![Data Wrangler on the top ribbon with a drop down showing a list of dataframes with df highlighted and a screen grab of the Data Wrangler window.](<Images/Lab 01/2024-08-06_18-21-34.png>)

The first transformation we will do is rename the Cust Number column to remove the space from the name. Either right click on the column header or click on the three dots and a menu appears, select rename column. Then in the Operations pane type in the new name. 

The data will show two versions of the column. The red tinted one is the previous version and green the new version. When you are happy that you want the green version click Apply.

![The menu when you right click on the column header with Rename Column highlighted with an arrow pointing to a screen grab of the Operations pane showing the box to type in the new name and red and green columns showing the before and after](<Images/Lab 01/2024-08-06_18-22-59.png>)

At the bottom of the screen there are two panes, Cleaning steps and a code window. The step we just added is called Rename column. If you click on that step you will see the code that is behind it. Data wrangler writes in Panda but will convert to PySpark when you finish

![Screen grab of the two bottom sections, the Cleaning steps pane shows a list of steps and the code window shows snippets of code related to the selected step](<Images/Lab 01/2024-08-07_08-46-50.png>)

The next transformation is to change the Location column into a City and Region column. There are multiple ways to do this. For this lab we are going to use column by example. This feature allows you to enter example answers and it calculates the code. Power Query has a very similar feature.

Make sure in the Cleaning steps the New operation is selected. Then in the Operations pane click on New column by example.

Select Location in the Target columns and type in City for the Derived column name. In the data there is now a new column called City and highlighted green. In the first row of the new column, type in the city from the location column, in this case Newport. Press enter and wait a moment.

![Operations pane showing new column by example with Location selected in the Target Column and City in the Derived column name box with a blue Apply button. Next to that a screen gran of the City column showing example Newport typed in and other cities listed in italic font. Blow both of those a screen grab of the code created](<Images/Lab 01/2024-08-07_09-04-28.png>)

If Data Wrangler can work it out below your entered in value will appear calculated values in italics. In the code window below you can see the comments and code it has written for you. Click Apply when you are happy with the results.

Repeat the above to create a Region column to contain England, Northern Ireland etc.

The last cleaning action we need to do is remove the Location column as we no longer need it. Right click or select the three dots on the Location column. From the menu select Drop columns. The Location column will now be highlighted red. The Operations pane will now show a drop down for target columns, more columns could be selected. Click Apply to remove the Location column.

![alt text](<Images/Lab 01/2024-08-07_09-18-10.png>)

The transformations in Data Wrangler are now complete. Your data should look like this.

![Screen grab of the data show a table with 6 columns, index, CustNumber, Customer, Industry, Region and City](<Images/Lab 01/2024-08-07_09-20-56.png>)

Now we are ready to copy the code back into our notebook. Click on Add code to notebook at the top of the screen. A dialog will show you a preview of the code. Click Add and it will add a new code block to your notebook.

![The Add code to notebook button and a screen grab of the code preview dialog and a screen grab of the code block created](<Images/Lab 01/2024-08-07_09-32-56.png>)

The code has created a function called clean_data to perform the steps we specified. the last 2 lines of the code block creates a new dataframe called df_clean by running that function on the dataframe df. And then displays the results

Click the run button on this new code block to show the results.

![Table of data with 5 columns and 10 rows of data](<Images/Lab 01/2024-08-07_09-43-53.png>)

## Save the data to a table

The final step of this notebook to write this data to a table. This is the one line of code you have to write

```
df_clean.write.mode("overwrite").format("delta").option("overwriteSchema", "true").save("Tables/Finance_Customers")
```

The mode being overwrite and the option to overwrite the schema means that this notebook will overwrite anything already there. The delta format is the format for tables in Microsoft Fabric. The final part shows the path to the table.

Run this code block or click Run All to create the table. Return to the Lakehouse to see the new table.

![Screen grab from the lakehouse showing the Finance_Customers table and a preview of the data](<Images/Lab 01/2024-08-07_10-02-29.png>)

### Exercise 1.05

* Create a notebook and load the customer csv
* Use Data Wrangler to clean the data
* Save the data into the table
* Run your notebook and then find the new table