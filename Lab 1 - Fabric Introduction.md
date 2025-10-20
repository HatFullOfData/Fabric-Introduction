# Lab 1 - Fabric Introduction

## Overview

This Lab includes prepping a workspace using task flow, adding a Lakehouse and loading files. Future labs will use these files to load into tables.

## Topics

* [Create the Workspace](#create-the-workspace)
* [Taskflow](#taskflow)
* [Create a Lakehouse](#create-a-lakehouse)
* [Upload files and folders](#upload-files)

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

[Task flows on Microsoft Learn](https://learn.microsoft.com/en-us/fabric/get-started/task-flow-overview?wt.mc_id=DX-MVP-5003563)

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

[Lakehouse Overview on Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-overview?wt.mc_id=DX-MVP-5003563)

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

