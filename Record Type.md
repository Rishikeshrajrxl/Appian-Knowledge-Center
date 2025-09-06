**Synch Record Type**
 - Each synced record type can sync up to 4 million rows from a source.
 - Each synced record type can have up to 100 fields, including [custom record fields](https://docs.appian.com/suite/help/24.1/custom-record-fields.html).
 - Text columns containing strings longer than 4,000 characters will be truncated in Appian.
 - ==If you need more than 4 million rows of data from a source, you can use [source filters](https://docs.appian.com/suite/help/24.1/records-filter-source-data.html) to divide up that large data source into multiple record types. Each record type can have a specific purpose. For example, if you have an Order database table with 6 million rows of data, you could create two record types: one with Open Orders and another with Closed Orders.==
- Unique fields have a lower character limit than standard fields and cannot exceed 765 characters.

