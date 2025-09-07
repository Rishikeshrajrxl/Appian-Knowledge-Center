**Synch Record Type**
 - Each synced record type can sync up to **4 million** rows from a source.
 - In newer Appian versions, that limit has increased to **==20 million rows==**.
 - Each synced record type can have up to ==100 fields==, including [custom record fields](https://docs.appian.com/suite/help/24.1/custom-record-fields.html).
 - Text columns containing strings longer than 4,000 characters will be truncated in Appian.
 - ==If you need more than 4 million rows of data from a source, you can use [source filters](https://docs.appian.com/suite/help/24.1/records-filter-source-data.html) to divide up that large data source into multiple record types. Each record type can have a specific purpose. For example, if you have an Order database table with 6 million rows of data, you could create two record types: one with Open Orders and another with Closed Orders.==
- Unique fields have a lower character limit than standard fields and cannot exceed 765 characters.
**Sources of Record**
 *  The source of a record is defined either through the **Data Source Management** settings in the Admin Console or by creating **Connected Systems**, after which it becomes available in Appian record as a data source.

**What comes after selecting different type of sync when creating record**
1. Incase of **Sync record**
	  - It asked to **choose Database table**.
2. Incase of **disable sync record**
	 - It is asked to **choose Data Store and Entity.**
	 - Therefore, creating async record we need to first create a datastore and its entity.

 **Export Records to Excel**
 There are two methods of exporting to Excel:
 1. - Exporting from a [records-powered grid](https://docs.appian.com/suite/help/25.3/Paging_Grid_Component.html#using-records-powered-grids) or a [record list](https://docs.appian.com/suite/help/25.3/record-list.html#add-an-export-to-excel-button). These options are typically used when a user would like to export data from an interface and apply filters from a grid.
 2. Using the [Export Data Store Entity to Excel](https://docs.appian.com/suite/help/25.3/Export_To_Excel_Smart_Service.html) or [Export Process Report to Excel](https://docs.appian.com/suite/help/25.3/Export_Process_Report_Excel_Smart_Service.html) smart services. These smart services are commonly used when exporting data within a process model to use within integrations.
  - In all scenarios, **==exports are limited to 50 columns==**. However, the row limit varies across export method and data source.
**Export limit for record lists and read-only grids**
 **Record Type Data Source**
 - Database : Export Limit -> 100,000 rows
 - Web service : Export Limit  -> N/A
 - Process Model : Export Limit  - > 100,000 rows
The _Export to Excel_ button will be disabled if the list or grid exceeds the maximum amount.
**Export limit from a smart service**
 - Export Data Store Entity to Excel smart service: limit is **none**
 - Export Process Report to Excel : 10,000 rows
==Note: * To prevent the export from timing out, Appian recommends limiting exports to 100,000 rows or fewer.==

**Why is ==export for unsynced service-backed record types disabled== by default?**
 - [Unsynced record types that use a web service](https://docs.appian.com/suite/help/25.3/configure-record-data-source.html#unsynced-web-service) as the source require additional logic to handle [paging, sorting, searching, and filtering](https://docs.appian.com/suite/help/25.3/configure-record-data-source.html#unsynced-web-service). Therefore, the _Export to Excel_ button is not displayed by default on a record list or read-only grid that uses an unsynced service-backed record type.

