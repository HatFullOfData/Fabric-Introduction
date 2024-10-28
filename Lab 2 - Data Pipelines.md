# Lab 2 - Data Pipelines and Orchestration

## Overview

In this lab we introduce the concept of data pipelines. Data pipelines allow you build simple to complex workflows including logic such as loops and conditionals. They are the orchestration tool.

The introduction exercise we are going to work through is copying a file that contains a product list into the lakehouse and then running a dataflow or notebook to update the products table.

## Topics

* [Create Pipeline](#create-pipeline)
* [Copy Data Activity](#copy-data-activity)
* [Edit Copy Data Activity](#edit-copy-data-activity)
* [First pipeline run](#running-the-pipeline)
* [Add Notebook or Dataflow Activity](#next-activity)
* [Run complete pipeline](#run-the-data-pipeline)
* [Schedule the pipeline](#schedule-pipeline-runs)

## Create Pipeline

A data pipeline is a get data task so we start by clicking on on New Item on the Get Data task box. From the pane on the right click on Data pipeline. When the dialog appears, enter in a name for the data pipeline and click Create.

![The Get Data task, the data pipeline tile and the dialog to enter in the](<Images/Lab 02/2024-09-17_12-02-37.png>)

This creates a new pipeline ready to add activities to.

## Copy Data Activity

The most common activity in a pipeline is to copy data and files using the Copy Data activity. We are going to copy a file from GitHub into the lakehouse. We will use the wizard to walk through setting up the source and destination.

From the home ribbon click on Copy data and select Use copy assistant. In the select data source search for http and then select the http tile that appears.

![Copy data stages to connect to the source data](<Images/Lab 02/2024-09-17_12-46-08.png>)

Enter in the url to the file we want to copy (see below). It will create a new connection. The Authentication can be anonymous so all the defaults can be left. Click next until you get a Preview data button. Click the button to confirm that you can see the contents of the csv. Then click Next

```
https://raw.githubusercontent.com/Laura-GB/DemoData/main/Products.csv
```

The next part of the wizard is to choose the destination for the file. In the next pane find your lakehouse in the OneLake data hub section and click on it. The next stage specifies where in the Lakehouse the file should go.

Tick files in the root folder section so it will create a file. If you want the file in a folder click Browse to select the right folder. Enter in a filename, remembering to include the extension .csv and click Next. The next pane confirms the file structure, click next to keep the defaults.

![Stage for setting up the destination connection and location](<Images/Lab 02/2024-09-17_12-53-09.png>)

On the Review + Save pane we are almost finished. You can see the file is going from CSV to CSV. There is one option to select if the activity should happen now. Click Save + Run or OK to add the action to the data pipeline.

## Edit Copy Data Activity

Data pipelines can include many activities so it is good practice to rename activities so future you can quickly understand what past you built.

Click on the Copy data activity. Across the bottom of the screen will appear the dialog to edit the activity. Enter in a better name and it is good practice to enter in a description.

![Copy data activity and the pane to edit it](<Images/Lab 02/2024-09-17_13-47-23.png>)

In the same pane you can review and edit the Source and Destination details that you set up in the wizard.

## Running the Pipeline

Although the pipeline is not complete it is worth testing that the activity works. On the home ribbon click Run. If you have not saved your pipeline it will prompt to Save and Run, otherwise it will just execute. The progress will be shown at the bottom of the window.

Once the pipeline has completed and the Copy Products activity has a green tick, check in the lake house to see the new file has been added.

![Running the pipeline and the progress pane and the new file in the lakehouse](<Images/Lab 02/2024-09-17_13-56-48.png>)

## Next Activity

Once the file has been copied into the lakehouse successfully we need to run either a notebook or dataflow to load that data into the products table.

Start by creating the dataflow or notebook in the Get Data task.

### Notebook Version

On the home ribbon click Notebook to add a notebook activity to the data pipeline. In the bottom pane, on the General tab enter in a meaningful name and description and then on the settings tab select Workspace and Notebook from the drop downs

![Adding a notebook activity](<Images/Lab 02/2024-09-17_14-41-14.png>)

Lastly you need to link the activities so they happen in the right order. drag the tick from Copy Products file activity to the Notebook activity.

### Dataflow Version

On the home ribbon click Dataflow to add the dataflow activity to the data pipeline. In the bottom pane enter in a suitable name and description and on the settings tab select workspace and dataflow.

![Adding a dataflow activity](<Images/Lab 02/2024-09-17_14-54-23.png>)

Lastly link the 2 activities by dragging the tick from Copy data activity to the Dataflow.

## Run the Data Pipeline

Once you have the activities loaded into data pipeline you can run the data pipeline. The progress will be shown at the bottom of the screen

![Pipeline progress](<Images/Lab 02/2024-09-17_15-39-45.png>)

## Schedule Pipeline Runs

The reason pipelines are good for orchestration is you can connect tasks to happen in the right order and you can schedule the pipeline to run by the minute, hour, day or week.

![Scheduling pane for a pipeline](<Images/Lab 02/2024-09-17_16-29-01.png>)

On the home ribbon click Schedule. In the pane that appears on the right toggle the Scheduled run to On and then enter in the required details for the scheduling. Remember that pipeline runs will use capacity so make sure you need those runs to happen. When you have entered all the details click Apply. The top description will now update to show how long to the next refresh.

