# Lab 1 - Fabric Introduction

## Overview

This Lab includes prepping a workspace using task flow, adding a Lakehouse, loading files and loading data from those files into tables using a Notebook and Dataflows.

## Topics

* [Create the Workspace](#create-the-workspace)
* [Taskflow](#taskflow)
* [Create a Lakehouse](#create-a-lakehouse)
* [Upload files and folders](#upload-files)
* [Load data from a file using a Notebook](#load-data-from-a-file-using-a-notebook)
* [Load data from a file using a Dataflow](#load-data-from-a-file-using-a-dataflow)
* [Load data from a folder of files using a Dataflow](#load-a-folder-of-files-using-a-dataflow)


## Create the workspace

To make life simpler we are each going to have our own workspace to build in.

Click on Workspace in the left hand list of icons in the window, and click + New Workspace. When the form appears on the right, enter in a unique name for your workspace. Finally click Apply and you should navigate to an empty workspace. Make sure the workspace has a premium diamond next to the name.

![List of Workspaces with the + New Workspace button highlighted and the Create a workspace form with the name populated and the Apply button highlighted](<Images/Lab 01/2024-08-02_15-56-06.png>)

**Note** Your company might not allow the creation of workspaces, hence we are using a demo tenancy.

### Exercise 1.01 Create Workspace

* Create a workspace with a unique name

## Taskflow

A recent addition to the Power BI service is Task flows. They allow you to build the logic of your project visually and they help tag the different Fabric elements.

### Adding Tasks

From the drop down Add a task, click on the task type you require. The task will appear in the task flow area. Be aware that all the tasks created after the first one will be stacked in the top left corner.

Arrange the task boxes into the right layout.

![The add task drop down showing all the options with the value Store highlighted and then an arrow pointing to a screen grab of the Store tasks created ](<Images/Lab 01/2024-08-02_16-29-26.png>)

### Linking Tasks

Task flows are there to show the relationship of the different Fabric elements. This is shown using connectors

A connector can be added between tasks boxes by click on the edge and dragging to another box. A dotted line should appear and will become a solid line when you click on the destination box.

![Two tasks with a dotted arrow between them](<Images/Lab 01/2024-08-02_16-44-13.png>)

### Exercise 1.02 Create Task Flow

* Add tasks and connectors to create 3 tasks

![Three tasks, Get data connected to Store connected to Visualize](<Images/Lab 01/2024-08-02_16-50-50.png>)

### References

[Task flows on Microsoft Learn](https://learn.microsoft.com/en-us/fabric/get-started/task-flow-overview)

## Create a Lakehouse

We will use a lakehouse to store files and tables. So a lakehouse is part of the Store task box.

Click on the + New item in the Store task. From the pane that appears on the right, click on Lakehouse. In the New lakehouse dialog type in a unique name and click create. Once it finishes creating the lakehouse it will navigate you to explore the lake house

![The Create an item pane showing recommended items to put in Store with an arrow going from Lakehouse to the New lakehouse diaglog. The name box is highlighted and contains LGB_Lakehouse and an arrow going from the create button to a screen grab of the explorer pane in the new lakehouse](<Images/Lab 01/2024-08-02_17-00-49.png>)

## Workspace Objects

When a Lakehouse is created, it also creates a Semantic Model and an SQL Endpoint. They are show as child objects in the workspace and are also in the Store task. We will work with both these items later in the workshop.

![Store task showing it has 3 items and a screen grab of the listing of three items in the workspace.](<Images/Lab 01/2024-08-06_10-00-33.png>)

### Exercise 1.03 Create a Lakehouse

* Create a lakehouse in the Store task
* Check the workspace taskflow and list of items

### References

[Lakehouse Overview on Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-overview)

## Upload Files and Folders

In our scenario the finance system exports csv files for the list of customers, customer contacts and monthly sales. The customers and contacts are single files, the monthly sales is a folder of files, one per month. The following section will walk through loading those files into tables.

### Create a Sub Folder
Your lakehouse might have many files being loaded from different systems, so for the sake of future us we will create a sub folder for the Accounts files.

Click on the three dots next to Files, to reveal a menu. From the menu select New Folder, then type in the folder name. Click Create to create the subfolder.

![Explorer pane with side menu showing on the Files, New folder highlighted and an arrow point to the New subfolder dialog with Accounts typed into Folder Name. The create button highlights and an arrow point to another view of the Explorer pane showing Files now has a subfolder Accounts](<Images/Lab 01/2024-08-02_17-17-34.png>)

### Upload individual files
For Customers and Contacts we have two csv files to upload into the Finance folder, which we will then in the next section of this lab load into tables.

Click the three dots on the Finance sub folder and select Upload and then Upload Files. In the Upload files pane, on the right hand side, click the folder icon and select the relevant file or files. Click the Upload button to load those files into the Finance folder.

![Explorer pane with FInance folder selected, three dots menu with Upload selected and Upload files highlighted, with an arrow pointing to Upload Files pane showing a file entered and the Upload button](<Images/Lab 01/2024-08-05_13-31-24.png>)

**Note** When uploading newer versions of the files you will need to tick the Overwrite if files exist box for the Upload button to work.

### Upload a folder

For the invoices raised by finance we have a folder of files to upload into the finance folder. Again these will be uploaded into a table later in this lab.

Click on the three dots on the Finance folder to show the menu. from the manu select Upload and then Upload Folder. In the Upload Folder pane on the right, click on the folder button and select your folder. It might give you a do you warning asking if you trust the cntents of the folder, click upload to say yes. And finally click upload to create the folder and upload the files.

![Explorer pane with Finance folder selected, three dots menu with Upload selected and Upload folder highlighted, with an arrow pointing to Upload Folder pane showing a folder entered and the Upload button](<Images/Lab 01/2024-08-06_09-20-15.png>)

### Exercise 1.04

* Create a sub folder called Finance
* Upload files Customers.csv and CustContacts.csv
* Upload the Sales folder

## Load Data from a file using a Notebook

Notebooks are not a new invention, they are a well established tool for working with data using Apache Spark. In this lab we are going to create a notebook that does some minor transformations and then loads the data into a table.

This lab only covers the very basics, to learn more take a look at [Notebooks n Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-engineering/how-to-use-notebook)

### Create the Notebook

The notebook is a getting data so it belongs in the Get Data task. Click New item in the Get data task. From the items that appear on the right select Notebook. 

When the notebook appears it will be called Notebook 1 or something similar. It is good practice to name each item before you get so many you no longer can keep track. Click on the name and in the drop down type in a name. I have entered Load Finance Customers

![The Get data task with New item highlighted with an arrow pointing to Notebook tile. And a screen grab showing how to rename the notebook](<Images/Lab 01/2024-08-06_17-26-24.png>)

Notebooks are made up of blocks or Markdown and code. Markdown is great to document the notebook. Each code block can be run one at a time or all of them.

### Connect the Lakehouse

The notebook needs to be connected to the Lakehouse in order to access the files and tables. In the Explorer pane on the left, click on Lakehouses. When the empty pane appears, click Add. This will show a dialog asking if its an existing lakehouse, click Add.

The next view is the OneLake data hub. A notebook can be connected to a Lakehouse from another workspace so all workspaces that you have access to will be shown. Find your lakehouse and select it. Click add and that lakehouse should now be shown in the explorer pane.

![Images showing the above steps in the previous 2 paragraphs](<Images/Lab 01/2024-08-06_17-48-33.png>)

### Load the files

Firstly we need to load the file data into a dataframe. This is how notebooks handle data. They have made this simple and it does not require knowing spark.

In the lakehouse click on the Finance folder, this will open another pane showing the files. Drag the Customers.csv file into the white space below the current code block. 

This will create a 3 line code block. The first line loads the csv data into a dataframe called df. Line 2 is a comment that explains what line 1 is doing. Line 3 prints out the contents of the dataframe, df.

![Screen grab of the notebook showing the two panes that allow you select a folder and then see the files and the code created created by dragging the file into the notebook. It then shows the results of pressing the play button](<Images/Lab 01/2024-08-06_18-06-34.png>)

We can execute the code block by clicking the play arrow to the top left of the code block. The results will be shown below. The first time you execute code it takes a little longer as it starts up a spark session.

### Use Data Wrangler to add transformations

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

### Save the data to a table

The final step of this notebook to write this data to a table. This is the one line of code you have to write

```
df_clean.write.mode("overwrite").format("delta").option("overwriteSchema", "true").save("Tables/Finance_Customers")
```

The mode being overwrite and the option to overwrite the schema means that this notebook will overwrite anything already there. The delta format is the format for tables in Microsoft Fabric. The final part shows the path to the table.

Run this code block or click Run All to create the table. Return to the Lakehouse to see the new table.

![Screen grab from the lakehouse whowing the Finance_Customers table and a preview of the data](<Images/Lab 01/2024-08-07_10-02-29.png>)

### Exercise 1.05

* Create a notebook and load the customer csv
* Use Data Wrangler to clean the data
* Save the data into the table
* Run your notebook and then find the new table

## Load Data from a File Using a Dataflow

Microsoft Fabric includes multiple methods of loading data into tables. In this section we will load the contacts file using a Gen2 Dataflow. Dataflows are not new to Power BI, but have been updated to include writing the results to a destination.

### Create a Dataflow

A dataflow is a Get Data action, so click New item in the Get data task. In the list of options that appear on the right, select Dataflow Gen2. Wait a moment while it loads.

Good practice is to rename items to meaningful names as we go, lets be honest we never go back and do it. At the top of the screen is the dataflow name, probabbly Dataflow 1 or similar. Click there and in the form enter a new meaningful name. I've used Load Finance Contacts

![alt text](<Images/Lab 01/2024-08-06_10-06-42.png>)

### Add data to the Dataflow

The empty data flow will show you a set of possibilities, none of the options match what we need so we need to click Get Data from another source. This will show us the a dialog with the complete range of connections that could be made. We need to connect to a file in a Lakehouse so therefore in OneLake.

Click on OneLake data hub on the left and then expand the explorer. Click on the name of your workspace, you might need to search for it. Then click on your Lakehouse. It takes a moment to connect.

![Showing the steps described in the previous and next paragraphs](<Images/Lab 01/2024-08-06_10-19-33.png>)

When the Choose data dialog appears, expand the folders File and then Finance. Put a tick next to CustContacts.csv and click Create. It will take a moment and then it will show you the data in a Power Query window.

### Transforming the data

Dataflows use Power Query to transform data into the structure we need. Our file needs very little transformation with just promoting the first line to be column names and tweaking the names slightly. This is an online version of Power Query you find in Power BI desktop and Excel.

The first step is to promote the column names. Select the transform ribbon and click Use first row as headers. The data should now show ContactID, First name etc as the column names

![Transform ribbon with Use first row as headers highlighted and the result after its clicked](<Images/Lab 01/2024-08-06_12-21-28.png>)

The next step is to tweak the column names. Tables in a Lakehouse cannot have spaces in the names so we need to remove them. Double click on the First name column header and it will go to edit mode. Make the changes and then press return. Repeat for the Last name column. I renamed them to FirstName and LastName

![Showing the column headers with Last name mid way through being edited. And the Query settings pane with the two new steps added](<Images/Lab 01/2024-08-06_12-23-49.png>)

Every step in the transformation is listed in the Query settings pane on the right. You can see the two 2 steps we added at the bottom of the list. Cicking the X on a step will delete it. Be aware there is no undo.

### Setting a destination

Dataflows Gen2 include adding a destination. So the final step in the dataflow creation is to add that destination.

In the bottom right hand corner of the dataflow window click on the + next Data destination. From the menu select Lakehouse. The next pane should give you connction details, assuming it shows Lakehouse, click Next. 

Then select your workspace on the left, you might need to search and then select your Lakehouse. Enter a sensible name for the table, I've used Finance_Contacts as I know I will get another table from dataverse called contacts. Click Next to move to the next step.

![alt text](<Images/Lab 01/2024-08-06_12-40-14.png>)

It will then list the columns of your new table. Make sure the data types and column names are correct. If they are not what you want you need to return back to the dataflow and fix them. Click Save settings to finish setting up the destination. We are now ready to Publish.

### Publish the dataflow

The final step is to publish the dataflow. Publishing includes refreshing the dataflow, i.e. running the dataflow to copy the data into a table.

Click on the publish button. This will close the dataflow. The dataflow is first published which can take a minute, then it will run. With this small a dataset it should only take a few minutes.

![Screen grab of the Publish button in the dataflow and then a screen grab of the new table and the data in the table](<Images/Lab 01/2024-08-06_16-45-24.png>)

If you navigate back to the lakehouse and look in tables, there should a new table called Finance_Contacts. If you click on the name you will get a preview of the data

### Exercise 1.06

* Load the contacts from csv file into a table called Finance_Contacts using a dataflow
* Find the table in the lakehouse and check the data

## Load a folder of files using a Dataflow

The Invoice data is exported out as a monthly csv file. These have been loaded into the Lakehouse in a folder. We could use a notebook or dataflow to combine these. For this lab we are going to use a dataflow.

### Create dataflow

The dataflow is also a get data activity so we start by clicking on New Item in the Get data task. We then select Dataflow Gen2 from the options on the right. In the next window we need to find the Lakehouse. Clicking on OneLake data hub should bring up a list including your lakehouse. You can use the search box if required.

When you click on your lakehouse it will navigate you to the choose data data window. Expand Files and Finance and tick Sales. Click Create to load the the list of files as a query.

![The Get data task and the Dataflow Gen2 tile, followed by a screen shot of the OneLake data hub and the Choose data window. Finally a screen shot of the file list created](<Images/Lab 01/2024-08-07_10-15-57.png>)

Don't forget to rename the dataflow by clicking on the Dataflow name at the top of the window and typing in a new name. Make it meaningful, e.g. Load Finance Invoices

![Screen grab of the rename drop down on the dataflow name](<Images/Lab 01/2024-08-07_10-47-04.png>)

### Combine file contents

We have the list of files. What we want is to combine the content of the files to make one table. For this to work we need to change the Content column data type to Binary. You do this by clicking on the ABC/123 at the top of the Content column and from the datatypes, select Binary.

The icon on the top right of the column changes to 2 down arrows. Click this icon to open the Combine files dialog. Click OK to complete the combine and give you a complete list of data. It creates helper queries to perform the merge.

![screen grab showing the data type options for the Content column, the Combine files dialo box and the query results](<Images/Lab 01/2024-08-07_10-21-22.png>)

The final step we need to do is rename the columns that have spaces in their names. Double click on each name and edit, pressing return to confirm new names.

The final query results should have 5 columns, Invoice, InvoiceDate, Customer, Contact and InvoiceAmount.

![Final query with 5 columns, Invoice, InvoiceDate, Customer, Contact and InvoiceAmount](<Images/Lab 01/2024-08-08_14-50-47.png>)

### Set Destination and Publish the dataflow

The dataflow transformations are complete. We now need to add a destination and publish the dataflow.

Click the plus next to Data destination in the bottom left and select Lakehouse. Click next on the connections screen. In the Choose destination traget window, find your lakehouse and click next. Check the column data types in the Choose destination settings and finally click Save settings.

![The steps to add a destination to the dataflow](<Images/Lab 01/2024-08-07_10-25-05.png>)

Finally click publish button to save the dataflow. It will close and takes a few minutes to publish and refresh. Check the table in the Lakehouse.

![alt text](<Images/Lab 01/2024-08-08_15-28-39.png>)

## Congratulations

In this lab we loaded files and created three items to load those files into tables. Later in this workshop we will use those tables to build a report and load into Dataverse.

Well Done!