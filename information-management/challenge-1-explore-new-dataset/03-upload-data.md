# 04 - Upload Data

## The DBFS

DBFS is short for _Databricks File System_. With your free account, Databricks also grants you free storage to upload your data sets you want work with.

The DBFS is structured just like your local Windows of Mac file system. It uses folders and subfolders to store the files. When we upload new data using the Databricks UI, the data will be stored in the subfolder `FileStore/tables`. We can choose any subfolder underneath this path to store our data, but for our purposes it is fine to simply store everything in this folder.

## Upload new data set to Databricks

We can upload new files by navigating to the "Data" tab in our menu on the left. Once we clicked on "Data", we see a list of existing databases and the tables in this database \(if any tables exist\). In the upper-right corner, we see a button "Add Data", which takes us to a new dialog.

![List of databases and contained tables](../../.gitbook/assets/add_data.png)

In this new dialog, we have several options to create a new table from data \(we'll create a table later on\). Although the dialog is for creating tables, we can skip that and only upload new data. To do that, select the "Upload Files"  button as shown below.

![](../../.gitbook/assets/create_new_table.png)

Now you can either drag & drop your file from your Window \(or Mac\) explorer to the gray box, or you can clock "browse" to select the file from your hard drive.

Once the upload starts, you see a small green progress bar, and when it is finished, you see a bold green check mark as shown in the screenshot below.

![](../../.gitbook/assets/upload_data.png)



