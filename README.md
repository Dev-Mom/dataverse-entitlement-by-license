# Struggling with Dataverse capacity management & overages? 
By default, all Dataverse storage capacity is kept in one giant tenant-level pool available for use by any (premium) Power Platform application or environment. While this does help ensure storage capacity can quickly and easily go where it's needed, it can also make it difficult to determine where the storage *should* go based on licensing entitlements. 

This can be especially problematic for organizations housing multiple departments, operating companies, etc. within a single tenant, who need to allocate storage capacity based on license entitlements **...until now!!** :boom:

Use this Power Automate flow to programmatically retrieve all Power Platform licenses, how much Dataverse capacity each gets, and account details like domain and department for each assigned licensee. 

Then, feed it all into Excel or Power BI to calculate how much Dataverse capacity each department, operating company, etc. is paying for! 
> [!NOTE]
> + This flow uses premium connectors
> + This flow requires an account with the Power Platform admin role
> + I encourage you to review the raw JSON output of the **GetTenantStorageCapacity** API call. This flow filters the results to *Database* capacity, but the results also include *Log* and *File* capacity as well. 

## Instructions for getting the flow up and running: 
1. Download the _TenantDBCapacityByLicense.zip_ file and import as a legacy Power Automate flow package.

<kbd> ![image](https://github.com/user-attachments/assets/c09b3f6e-b2da-472b-8adc-ce4fc81634a9) </kbd>
2. For the first connection resource, create a new HTTP with Microsoft Entra ID (preauthorized) connection and set the Base URL and Resource URI to `https://licensing.powerplatform.microsoft.com`

<kbd><img width="979" height="355" alt="image" src="https://github.com/user-attachments/assets/87751643-d616-4d85-8ac2-7e8a8572eca3" /></kbd>
<kbd>![image](https://github.com/user-attachments/assets/00b94e6f-ae29-4194-b721-c91eb3563924)</kbd>
<kbd>![image](https://github.com/user-attachments/assets/89533526-1ddc-4c26-8f00-796c5f177341)</kbd>

3. Repeat for the second connection resource. But this time set the Base URL and Resource URI to `https://graph.microsoft.com`

4. Once the flow is imported, edit the _GetTenantStorageCapacity_ action and update the Url with your respective Tenant Id.

5. Save the flow and run it! 

## The flow will produce 2 object arrays: PowerPlatformLicenses & LicenseAssignments. 

:thumbsup: The first will contain all the Power Platform licenses purchased within your tenant and the Dataverse DB capacity values allocated to each one.

:thumbsup: The second will contain all the users who are assigned those licenses, including pertinent Entra profile properties like department and domain values.

It's everything you need to calculate how much Dataverse capacity should be allocated to each division, department, etc. based on the Power Platform licenses they own! 👀

Then, you can take full advantage of Microsoft's new, handy-dandy [Dataverse capacity allocation features](https://learn.microsoft.com/en-us/power-platform/admin/capacity-storage#allocate-capacity-for-an-environment). 

<kbd><img width="936" height="591" alt="image" src="https://github.com/user-attachments/assets/267d6437-eda8-4d05-b959-1bf8a387ac4b" /></kbd>

