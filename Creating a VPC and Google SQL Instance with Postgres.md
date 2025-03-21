# Creating a VPC and Google SQL Instance 

These instructions will guide you through creating a Virtual Private Cloud (VPC) network in Google Cloud Platform (GCP) and then deploying a Google Cloud SQL instance with PostgreSQL attached to that private network.

# 1\. Create a VPC Network

1. Navigate to the VPC network page in the Google Cloud Console.  
2. Click "Create VPC Network".  
3. Provide a name for your VPC network. For example, "private-network".  
4. Select "Custom" for the subnet creation mode.  
5. Add a new subnet.  
   * Name your subnet (e.g., "private-subnet").  
   * Choose a region.  
   * Enter an IP range (e.g., "10.10.0.0/24").  
6. Click "Create".

# 2\. Create a Google Cloud SQL Instance

1. Go to the SQL page in the Google Cloud Console.  
2. Click "Create Instance".  
3. Choose "PostgreSQL".  
4. Select the version of PostgreSQL you want to use.  
5. Provide an instance ID.  
6. Set a root password.  
7. Select the region that matches your VPC subnet.  
8. Under "Configure machine type and storage", select the appropriate machine type and storage size.  
9. Under "Connections", select "Private IP".  
10. Choose the VPC network you created (e.g., "private-network").  
11. Click "Create Instance".

# 3\. Connect to the Google Cloud SQL Instance

1. Once the instance is created, go to its details page.  
2. Note the private IP address of the instance.  
3. To connect to the instance, you will need a VM instance in the same VPC or a connection from your local machine through a VPN or Cloud Interconnect.  
4. From a VM in the same VPC, you can use a PostgreSQL client (like `psql`) to connect to the database using the private IP address and the root password.

Example `psql` command:

```
psql -h <private-ip-address> -U postgres -d postgres
```

Replace `<private-ip-address>` with the private IP address of your SQL instance.

# 4\. Create a Colab Enterprise Template

1. Navigate to the Colab Enterprise page in the Google Cloud Console.  
2. Click "Create Template".  
3. Provide a name for your template (e.g., "vpc-postgres-template").  
4. Select the region that matches your VPC subnet.  
5. Under "Network", choose the VPC network you created (e.g., "private-network").  
6. Configure any other necessary settings for your Colab Enterprise template, such as runtime configurations and access controls.  
7. Click "Create".

# 5\. Connecting from Colab Enterprise to the Google Cloud SQL Instance

1. Once the Colab Enterprise template is created, upload the relevant notebook from the github repository.
2. Create a new runtime for the notebook using the template. 
3. Enter the pre-deployed instance name in the notebook configuration section.
3. Follow the rest of the instructions in the notebook to connect to the instance and run the lab. 

