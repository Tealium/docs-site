---
title: Prepare a CSV file for import
description: This article helps you prepare your files for a successful import using the file import data source.
url: https://docs.tealium.com/server-side/data-sources/file-import/prepare-a-csv-file/
---
## Prepare data to import

We recommend using the file import data source with the following types of data sets:

* Demographic data
* Prospect and lead data
* Historical purchases and refunds
* Offline interactions (support, direct marketing, event attendance, etc.)

To ensure efficient processing of your files, we strongly recommend breaking up large files into smaller files of 100,000 rows each. While larger file sizes are supported, we don’t recommend exceeding file sizes of 50 MB as it may increase the likelihood of errors.


<blockquote>
To get the most out of your imported data, ensure that every row in your CSV file has a column with a unique visitor ID that associates the data to a customer. For more information, see [Visitor Identification using Tealium Data Sources](https://docs.tealium.com/visitor-identification-data-sources/).
</blockquote>


## File naming conventions


<blockquote>
Multiple files uploaded through SFTP or S3 are processed alphabetically by their file names.
</blockquote>


### File name prefix

CSV files must use the following name format: `{prefix}_{version}.csv`. This format consists of the following parts:

|Format| Description|
|---| ---|
|`prefix`| A unique identifier for groups of files that share the same CSV column names. The prefix can contain underscores, but do not include an underscore at the end. For example, `test` or `test_file`.|
|`version`| (Optional) If there are multiple files with the same CSV column names, this value represents a unique identifier for a file with a prefix. This is usually a timestamp, a version number, or both. For example, `test_20251225.csv`, `test_20251226.csv`, and `test_2025-1227.csv`.|


<blockquote>
We strongly recommend using a version number to differentiate CSV file versions.
</blockquote>


The file name prefix you use must be unique. For example, using the prefixes `store-transactions` and `store-transactions-returns` will cause unexpected results because they share the same initial prefix: `store-transactions`.

### File name limitations

File names must adhere to the following rules:

* File names may only contain the following characters: letters (`a-z` or `A-Z`), numbers (`0-9`), hyphens (`-`), underscores (`_`), and periods (`.`).
* File names are case-sensitive. For example, `store-transactions_20230319-a.csv` and `Store-Transactions_20230319-a.csv` are different files, so we recommend that you use lowercase file names to avoid confusion.

### File name examples

#### Multiple files

The following example is for in-store purchases dated March 19, 2023 and separated into two files, `a` and `b`.  

|Prefix| Version| File Name|
|---| ---| ---|
|`storepurchases`| `20230319-a`| `storepurchases_20230319-a.csv`|
|`storepurchases`| `20230319-b`| `storepurchases_20230319-b.csv`|

#### Multiple versions

The following example is for two files with in-store returns from March 14, 2023 and March 15, 2023.  

|Prefix| Version| File Name|
|---| ---| ---|
|`storereturns`| `20230314`| `storereturns_20230314.csv`|
|`storereturns`| `20230315`| `storereturns_20230315.csv`|

## File data format

### File organization

We recommend that you organize your files with the following guidelines:

* **File encoding**  
  We suggest UTF-8 [(without BOM encoding)](https://en.wikipedia.org/wiki/Byte_order_mark#UTF-8).
* **Field separator**  
The field separator must be a comma (`,`).
* **Column names**  
  * The first line of the CSV file must contain the file column names. Each line after that represents an event or a visitor record and must contain at least one [visitor identifier attribute](https://docs.tealium.com/visitor-id-attribute/).
  * Column names may not contain hash (`#`), caret (`^`), or whitespace characters.
  * Column names are case-sensitive and must match the attribute names exactly.
* **Column values**  
  Column values should not exceed 1,000 characters. Any characters over this limit are trimmed.
* **Column order**  
  The order of the columns does not matter, but we recommend placing the visitor ID column first.
* **Extra/Missing columns**  
  Extra columns that are not configured as AudienceStream attributes will be ignored. Mapped columns not present in the CSV file will be skipped.
* **Group rows by visitor ID**  
  Each row has a [visitor ID](https://docs.tealium.com/visitor-id-attribute/) column and file may contain multiple rows for the same visitor. Rows that contain the same visitor ID should be grouped together to optimize the import process.
* **Line endings**  
The following line endings are supported: LF (Line Feed), CR (Carriage Return), and CR LF (Carriage Return Line Feed).

### Data type formats

We recommend that you format the following data types accordingly:

* **Double-quote values with commas**  
If a value contains a comma (`,`), it must be surrounded by double-quotes to ensure the integrity of the CSV columns. We recommend putting all values in double-quotes. Use a doubled double quote (`""`) to indicate a double quote character in the data.
* **Array of strings format**  
Use the following example format for file attributes that are to be mapped to an array of strings:  
  ```
  "[""one"",""two"",""three""]"
  ```
* **Array of numbers format**  
Use the following example format for file attributes that are to be mapped to an array of numbers:  
  ```
  "[1.99,20.99]"
  ```
* **Array of booleans format**  
Use the following example format for file attributes that are to be mapped to an array of booleans:  
  ```
  "[0, 1]","[0, 1]"
  ```
* **Normalize dates**  
  * Date values must be consistent throughout a file for a given field. 
  * Each date value must match the format specified for that column. For example, if the expected format is `yyyy-MM-dd`, the values must contain 4-digit years and 2-digit month and day values, for example, `2021-02-09`.
  * The following date components are supported: Year, Month, Day, Hour, Minutes, Seconds, Milliseconds, AM/PM, ISO, RFC, Era. For more information about supported date components, see [Java SimpleDateFormat Patterns](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html).
  * Dates are stored in Tealium as epoch timestamps in milliseconds.
* **Normalize empty values**  
Some rows might not contain a value for each column. Ensure that these columns are empty and do not contain placeholder values such as "null", "empty", "blank", etc.
* **Omit special characters from currency amounts**  
Columns that represent currency amounts, such as "OrderTotal" or "ProductPrice", must not contain symbols or commas.

|Valid Values| Invalid Values|
|---| ---|
|39.75| $39.75|
|0 | zero|
|1399.00| €1.399,00|

