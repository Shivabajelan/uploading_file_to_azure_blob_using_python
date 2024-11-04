# uploading_file_to_azure_blob_using_python

# Azure Blob Storage File Uploader
This Python script automates the upload of unstructured data, such as PDF or PNG files, to Azure Blob Storage. With a few parameters and a file path, you can securely upload files to your Azure storage container using Python.

## Prerequisites
To use this script, ensure you have:

* An Azure Storage Account with a container created.
* The **azure-storage-blob** package installed.
 If not, install it via:

"pip install azure-storage-blob" in the terminal.

## Setup and Usage
**Step 1: Configure Your Azure Storage Credentials**

Before running the script, set up your Azure credentials:

- Account Key
- Account Name
- Connection String
- Container Name
Note: Do not hardcode sensitive information directly in your scripts. Instead, retrieve them securely from environment variables or a secrets manager.

**Step 2: Update the Script with Your Parameters**

In the script, replace the following placeholders with your own Azure credentials:

**python Code:**

storage_account_key = "<Your-Account-Key>"
storage_account_name = "<Your-Account-Name>"
connection_string = "<Your-Connection-String>"
container_name = "<Your-Container-Name>"

**Step 3: Upload a File**

To upload a file, call the UploadToBlobStorage function and provide:

* file_path: Local path of the file you want to upload.
* file_name: Desired path and name of the file in Azure Blob Storage.

![image](https://github.com/user-attachments/assets/65f0e39e-b78d-4d61-9d5d-cd9a35264026)


# Define Azure Storage credentials
storage_account_key = "<Your-Account-Key>"
storage_account_name = "<Your-Account-Name>"
connection_string = "<Your-Connection-String>"
container_name = "<Your-Container-Name>"

# Define function to upload files to Azure Blob Storage
def UploadToBlobStorage(file_path, file_name):
    # Connect to Blob Service
    blob_service_client = BlobServiceClient.from_connection_string(connection_string)
    blob_client = blob_service_client.get_blob_client(container=container_name, blob=file_name)

    # Read the file in binary mode and upload
    with open(file_path, "rb") as data:
        blob_client.upload_blob(data)
    print(f"File {file_name} is uploaded to Azure Blob Storage {container_name} successfully")

# Call the function with your file path and desired blob name
UploadToBlobStorage('path/to/your/local/file.pdf', 'MyFolder/YourFileName.pdf')
Security Note
To avoid hardcoding sensitive information, consider storing credentials securely in environment variables or a secrets manager.

Example using environment variables:

python
Copy code
import os

connection_string = os.getenv("AZURE_STORAGE_CONNECTION_STRING")
This script provides a quick and efficient way to upload files to Azure Blob Storage, making it easier to manage unstructured data storage with Python.
