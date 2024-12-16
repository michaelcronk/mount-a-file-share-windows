# Mount a File Share on Windows

## Overview

In this tutorial I will be showing you how to mount a File Share on a Windows machine using the Azure portal. I will be using a Windows Virtual Machine that I created in Azure earlier, if you don't know how to create a Virtual Machine check out [this tutorial](https://github.com/michaelcronk/deploying-a-vm) that shows how to create one.

> <sub>To get started, you first need to have a Microsoft Azure account. If you don't have one, you can create a free account [here.](https://azure.microsoft.com/en-us/free/search/?&ef_id=_k_Cj0KCQiA4NWrBhD-ARIsAFCKwWv39zVXs4ww7bj_IGmTJngZol8ZX835NOuvRgv7ygSk_rEe9lnrcGcaAg2vEALw_wcB_k_&OCID=AIDcmm5edswduu_SEM__k_Cj0KCQiA4NWrBhD-ARIsAFCKwWv39zVXs4ww7bj_IGmTJngZol8ZX835NOuvRgv7ygSk_rEe9lnrcGcaAg2vEALw_wcB_k_&gad_source=1&gclid=Cj0KCQiA4NWrBhD-ARIsAFCKwWv39zVXs4ww7bj_IGmTJngZol8ZX835NOuvRgv7ygSk_rEe9lnrcGcaAg2vEALw_wcB)</sub>

## Storage Account Setup

Once you get logged into Azure, we will either create a new resource group or navigate to one that we will want our resource to live.

Click "Create" within our resource group and search for a storage account in the Azure services search bar, then click create a storage account.

![alt text](<imgs/Screenshot 2024-12-13 at 8.23.52 PM.png>)
![alt text](<imgs/Screenshot 2024-12-13 at 8.24.58 PM.png>)

You will now have to do a few things:

1. You have to select what subscription and resource group you will want to add this resource to.
2. Create a name for the storage account and select a region for this resource to live in.
3. Select what service you want to use in the storage account, most of the time and for my example you will select "Azure Blob Storage or Azure Data Lake Storage".
4. Then select the performance you want, for our example we will stick with Standard because it keeps the cost low.
5. Finally you will select your redundancy. We will do "Locally-redundant storage" because this example doesn't need multiple backups in multiple regions or availability zones. Make sure you know what redundancy means and how this may effect your project, ream more about [Azure Redundancy here](https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy).

If you would like to read more about storage accounts in general, [click here](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview).

![alt text](<imgs/Screenshot 2024-12-13 at 8.25.36 PM.png>)

We will not be changing any other settings within our storage account for our example, so click "Review and Create" and create the storage account.

## File Share Setup

Once the storage account is finished setting up, click into the storage account. On the left hand side scroll down to "Data Storage" then select "File Share" and create a file share.

![alt text](<imgs/Screenshot 2024-12-15 at 9.01.02 AM.png>)

Name your file share and select the access tier you will be using for you storage account. If you want to read more on access tiers, [click here](https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview).

For the sake of our example I will be sticking with "Hot", which is used for data that is accessed or modified frequently.

![alt text](<imgs/Screenshot 2024-12-15 at 9.02.02 AM.png>)

**IMPORTANT** - Make sure you setup the correct "Backup" settings when creating your file share. For this example we will disable it totally to keep the ease of deleting all our resources after creation. Read more about backups and how they work [here](https://learn.microsoft.com/en-us/azure/backup/blob-backup-configure-manage?tabs=operational-backup).

Now click "review and create" to create the file share.

## Storage Account Network Access

Before connecting the file share to our VM, we need to first make sure our network connections to the storage account are correct.

For good practice we don't leave our resources open for all of the internet to access.

> **Why We Don't Allow "Access From Every Network"**  
> Leaving your file share open to "allow access from everyone" means anyone on the internet can try to access our files. This creates serious security risks, including:
>
> - **Unauthorized access**: Hackers or malicious users could view, edit, or even delete your files if they get in.
> - **Data breaches**: Sensitive data can be easily leaked or stolen.
> - **Compliance issues**: You might violate regulations or company policies.
>
> What we do instead is restrict access using **network security rules**, such as adding a private IP range, using a firewall, or using Azure Active Directory authentication. This ensures only authorized users and systems can access our files.

## Connecting the File Share
