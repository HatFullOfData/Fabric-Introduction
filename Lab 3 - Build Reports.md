# Lab 3 - Build Reports

## Overview

Microsoft Fabric of course includes reports. This workshop is not to teach Power BI and DAX but is to show there are now new methods of creating those reports. Fabric also introduces the concept of Direct Lake a new way to connect to your data in Power BI

## Topics

* [Create New Semantic Model](#create-new-semantic-model)
* [Add Relationships](#add-relationships)
* [Manage Relationships](#manage-relationships)
* [Adding Measures](#adding-measures)
* [Direct Lake Limitations](#limitations)
* [Adding a Report](#adding-a-report)
* [Adding to Visualize Task](#adding-to-visuals-task)

## Create New Semantic Model

Every Lakehouse has a default semantic model. This includes all the tables plus some extra tables that you would not expect or want in your reports. So it has become best practice to create a new semantic model.

In the Lakehouse select New semantic model from the home ribbon. Enter in a name for the model and select the workspace it will be in. It can be in a different workspace than the Lakehouse. Select the tables to include in the model and click confirm.

![New semantic model pane](<Images/Lab 03/2024-09-17_16-59-19.png>)

The model window will now be shown with the tables added. The icon in the corner of a box with waves shows that the connection is direct lake. You can add more tables by clicking on Edit tables.

## Add Relationships

Relationships are just the same as in Power BI. You can create a relationship by dragging a field from one table to another table. This will open the new relationship dialog.

![New relationship dialog and relationship diagram of two tables connected](<Images/Lab 03/2024-09-17_17-12-07.png>)

Make sure the correct columns are selected and the cardinality is correct. Power BI desktop will determine the relationship type, online semantic model editor does not.

## Manage Relationships

Similar to Power BI desktop you can review the relationships all together in one dialog.

![Manage relationships button on the ribbon and the dialog box that opens](<Images/Lab 03/2024-09-17_17-20-50.png>)

## Adding Measures

A good semantic model includes a good set of measures to make the model easy to build reports from.

Click on the new measure button and enter in your calculation. You will get intellisense just like in Power BI desktop to help and shift + enter will give a new line so you can still format nicely.

![Home ribbon and formula bar showing a measure being written](<Images/Lab 03/2024-09-17_17-34-05.png>)

In Power BI desktop there is a Measure ribbon. In the online editor you use the properties pane to make the changes you would expect such as Home table, Description and Formatting options.

![Properties pane showing how to change the home table and formatting options](<Images/Lab 03/2024-09-17_17-24-48.png>)

## Limitations

There are a number of limitations in Direct Lake and building semantic models online. Some of the restrictions will push the report back into Direct QUery mode and some will just break the report.

The most common ones that people notice are no calculated tables or columns. 

The full details of the limitations can be found here 
[Microsoft Direct Lake Overview Known Limitations](https://learn.microsoft.com/en-us/fabric/get-started/direct-lake-overview#known-issues-and-limitations)

## Adding a Report

The above steps just creates a semantic model, it does not create any visuals. They have split the reporting role into building the model and separately building the report.

In the semantic model click on New Report. This will open a report editing window. The features are not as advanced as Power BI desktop but most common tasks can be done.

![Power BI Report edit window with a few visuals](<Images/Lab 03/2024-09-17_17-54-32.png>)

You need to save the report from the file menu for it to be saved into the workspace.

### Adding Reports from the Task flow

You can also add a report from visualize task. Click on New item in the Visualize task and from the right select Report. In the dialog that appears, select the correct semantic model and you can get started building your report.

![Visualize task and the report tile and then the list of semantic models to select from](<Images/Lab 03/2024-09-17_18-01-08.png>)

### Connecting from Power BI Desktop

You can build a report in Power BI desktop that is connected to a semantic model. In a blank report, click OneLake data hub. On the drop down select Power BI semantic models. Then in the dialog select the semantic model.

![Connecting to a semantic model in Power BI desktop](<Images/Lab 03/2024-09-17_18-07-26.png>)

The same limitations apply to keep the Direct lake connection. If you try to add another data source you will get a warning that the connections are going to change to Direct Query.

![Dialog with the message that A DirectQuery connection is required](<Images/Lab 03/2024-09-17_18-08-21.png>)

You can also build a direct query or import report directly from a lakehouse or a warehouse in Fabric.

## Adding to Visuals Task

The semantic models and possibly some of the reports will not be attached to a task in the task flow diagram. Click on the paperclip button in the Visualize task and tick the items you want to add. Then click Select to add those items to the task.

![Visualize task and the dialog to select items to add](<Images/Lab 03/2024-09-17_18-22-29.png>)



