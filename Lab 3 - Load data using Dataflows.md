
# Load Data from a File Using a Dataflow

Microsoft Fabric includes multiple methods of loading data into tables. In this section we will load the contacts file using a Gen2 Dataflow. Dataflows are not new to Power BI, but have been updated to include writing the results to a destination.

## Create a Dataflow

A dataflow is a Get Data action, so click New item in the Get data task. In the list of options that appear on the right, select Dataflow Gen2. Wait a moment while it loads.

Good practice is to rename items to meaningful names as we go, lets be honest we never go back and do it. At the top of the screen is the dataflow name, probably Dataflow 1 or similar. Click there and in the form enter a new meaningful name. I've used Load Finance Contacts

![alt text](<Images/Lab 01/2024-08-06_10-06-42.png>)

## Add data to the Dataflow

The empty data flow will show you a set of possibilities, none of the options match what we need so we need to click Get Data from another source. This will show us the a dialog with the complete range of connections that could be made. We need to connect to a file in a Lakehouse so therefore in OneLake.

Click on OneLake data hub on the left and then expand the explorer. Click on the name of your workspace, you might need to search for it. Then click on your Lakehouse. It takes a moment to connect.

![Showing the steps described in the previous and next paragraphs](<Images/Lab 01/2024-08-06_10-19-33.png>)

When the Choose data dialog appears, expand the folders File and then Finance. Put a tick next to CustContacts.csv and click Create. It will take a moment and then it will show you the data in a Power Query window.

## Transforming the data

Dataflows use Power Query to transform data into the structure we need. Our file needs very little transformation with just promoting the first line to be column names and tweaking the names slightly. This is an online version of Power Query you find in Power BI desktop and Excel.

The first step is to promote the column names. Select the transform ribbon and click Use first row as headers. The data should now show ContactID, First name etc as the column names

![Transform ribbon with Use first row as headers highlighted and the result after its clicked](<Images/Lab 01/2024-08-06_12-21-28.png>)

The next step is to tweak the column names. Tables in a Lakehouse cannot have spaces in the names so we need to remove them. Double click on the First name column header and it will go to edit mode. Make the changes and then press return. Repeat for the Last name column. I renamed them to FirstName and LastName

![Showing the column headers with Last name mid way through being edited. And the Query settings pane with the two new steps added](<Images/Lab 01/2024-08-06_12-23-49.png>)

Every step in the transformation is listed in the Query settings pane on the right. You can see the two 2 steps we added at the bottom of the list. Cicking the X on a step will delete it. Be aware there is no undo.

## Setting a destination

Dataflows Gen2 include adding a destination. So the final step in the dataflow creation is to add that destination.

In the bottom right hand corner of the dataflow window click on the + next Data destination. From the menu select Lakehouse. The next pane should give you connction details, assuming it shows Lakehouse, click Next. 

Then select your workspace on the left, you might need to search and then select your Lakehouse. Enter a sensible name for the table, I've used Finance_Contacts as I know I will get another table from dataverse called contacts. Click Next to move to the next step.

![alt text](<Images/Lab 01/2024-08-06_12-40-14.png>)

It will then list the columns of your new table. Make sure the data types and column names are correct. If they are not what you want you need to return back to the dataflow and fix them. Click Save settings to finish setting up the destination. We are now ready to Publish.

## Publish the dataflow

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
