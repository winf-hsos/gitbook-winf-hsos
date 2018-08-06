---
description: 'In this lesson, you''ll learn how to upload a file to Databricks DBFS.'
---

# 04 - Upload Data

## The DBFS

DBFS is short for _Databricks File System_. With your free account, Databricks also grants you free storage for your data sets.

The DBFS is structured just like your local Windows of Mac file system. It has folders and subfolders to store and organize files. When we upload new file using the Databricks UI, by default the data will be stored in the subfolder `FileStore/tables`. We can choose any subfolder underneath this path to store our data, but for our purposes, it is fine to simply store everything in this folder.

{% hint style="info" %}
For more information on the DBFS, check out the [official documentation](https://docs.databricks.com/user-guide/dbfs-databricks-file-system.html#dbfs).
{% endhint %}

## Upload new data set to Databricks

We can upload a new file if we if naviagte to the "Data" tab in our menu on the left. Once we click on "Data", we see a list of existing databases and the contained tables \(if any tables exist\). In the upper-right corner, we see a button "Add Data", which takes us to a new dialog.

![List of databases and contained tables.](../../.gitbook/assets/add_data.png)

In this new dialog, we have several options to create a new table from data. Although the dialog is for creating tables, we can skip that and only upload new data \(we'll create a table later on\). To upload a new file, select the "Upload Files"  button as shown below.

![Several options to add new data.](../../.gitbook/assets/create_new_table.png)

Now you can either drag & drop your file from your Window \(or Mac\) explorer to the gray box, or you can click "browse" to select the file from your hard drive.

Once the upload starts, you see a small green progress bar, and when it is finished, you see a bold green check mark as shown in the screenshot below.

![The green checkmark indicates successful upload of the file.](../../.gitbook/assets/upload_data.png)

When the upload completes, a small text appears right underneath the gray box that prints the destination path of the uploaded file. Make sure you copy this path, as we'll need this when we want to access this file from a notebook.

{% hint style="info" %}
Make sure you copy the path where data is stored in DBFS! You will need this information later on. In the image above, the path is `/FileStore/tables/winemag_data_130k_v2-246fd.csv`

Should you forget or lose the path, you can browse through the files when you click on "DBFS" instead of "Upload File". When you click on a file, the path is shown as text.
{% endhint %}

