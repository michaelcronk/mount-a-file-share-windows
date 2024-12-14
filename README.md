# Mount a File Share on Windows

## Overview

In this tutorial I will be showing you how to mount a File Share on a Windows machine using the Azure portal. I will be using a Windows Virtual Machine that I created in Azure earlier, if you don't know how to create a Virtual Machine check out [this tutorial](https://github.com/michaelcronk/deploying-a-vm) that shows how to create one.

> <sub>To get started, you first need to have a Microsoft Azure account. If you don't have one, you can create a free account [here.](https://azure.microsoft.com/en-us/free/search/?&ef_id=_k_Cj0KCQiA4NWrBhD-ARIsAFCKwWv39zVXs4ww7bj_IGmTJngZol8ZX835NOuvRgv7ygSk_rEe9lnrcGcaAg2vEALw_wcB_k_&OCID=AIDcmm5edswduu_SEM__k_Cj0KCQiA4NWrBhD-ARIsAFCKwWv39zVXs4ww7bj_IGmTJngZol8ZX835NOuvRgv7ygSk_rEe9lnrcGcaAg2vEALw_wcB_k_&gad_source=1&gclid=Cj0KCQiA4NWrBhD-ARIsAFCKwWv39zVXs4ww7bj_IGmTJngZol8ZX835NOuvRgv7ygSk_rEe9lnrcGcaAg2vEALw_wcB)</sub>

Once you get logged into Azure, we will either create a new resource group or navigate to one that we will want our resource to live in.

Click "Create" within our resource group and search for a storage account in the Azure services search bar, then click create a Storage Account.

![alt text](<imgs/Screenshot 2024-12-13 at 8.23.52 PM.png>)
![alt text](<imgs/Screenshot 2024-12-13 at 8.24.58 PM.png>)

You will now have to do a few things:

1. You have to select what subscription and resource group you will want to add this resource to.
2. Create a name for the Storage Account and select a region for this resource to live in.
3. Select what service you want to use in the storage account, most of the time and for my example you will select "Azure Blob Storage or Azure Data Lake Storage".
4. Then select the performance you want, for our example we will stick with Standard because it keeps the cost low.
5. Finally you will select your redundancy. We will do "Locally-redundant storage" because this example doesn't need multiple backups in multiple locations. Make sure you know what redundancy means and how this may effect your project, ream more about [Azure Redundancy here](https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy).

If you would like to read more about storage accounts, [click here](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview).

![alt text](<imgs/Screenshot 2024-12-13 at 8.25.36 PM.png>)

We will not be changing any other settings within our storage account for our example, so click "Review and Create" and create the storage account.
