The COS Select feature uses structured query language (SQL) to filter objects stored in COS in order to extract a specific object and get the desired data. By filtering object data using this feature, you can reduce the amount of data transferred by COS, which helps lower the cost and delay in data extraction.

The COS Select feature currently allows you to extract objects stored in CSV and JSON formats, as well as CSV- and JSON-formatted objects compressed by gzip and bzip2. In addition, you can save your extraction results in CSV and JSON formats and specify how to separate the result records.

You can pass in an SQL expression to COS in your request. COS Select currently only supports certain SQL expressions. For more information, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).

You can run SQL queries using the COS console, APIs, SDKs, or COSCMD. Note that certain restrictions apply to file extraction if you use the COS Console: up to 128 MB of files can be extracted, and up to 40 MB of data can be returned. To extract more data, use other methods.

>
>- For more information on data types supported by COS Select and current reserved fields, see [Data Types](https://intl.cloud.tencent.com/document/product/436/32476) and [Reserved Fields](https://intl.cloud.tencent.com/document/product/436/32475).
>-Currently, the extraction function only supports public cloud regions in mainland China.

## Use Limits

The following restrictions apply to COS Select:

- You must have the `cos:GetObject` permission to the queried object. A root account has this permission by default.
- Only objects in standard storage class can be extracted.
- The maximum length of an SQL expression is 256 KB.
- The maximum length of a single record in the extraction result is 1 MB.

SQL clauses currently supported by COS Select include:

- SELECT statement
- FROM clause
- WHERE clause
- LIMIT clause

> For more information on SQL clauses, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473).

Functions currently supported by COS Select include:

- Aggregate functions, such as AVG function, COUNT function, MAX function, MIN function, and SUM function.
- Condition functions, such as COALESCE function and NULLIF function.
- Conversion functions, such as CAST function.
- Date functions, such as DATE_ADD function, DATE_DIFF function, EXTRACT function, TO_STRING function, TO_TIMESTAMP function, and UTCNOW function.
- String functions, such as CHAR_LENGTH function, CHARACTER_LENGTH function, LOWER function, SUBSTRING function, TRIM function, and UPPER function.

> For more information on SQL functions, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).

COS Select currently supports the following operators:

- Logical operators: `AND, NOT, OR`
- Comparison operators: `<, >, <=, >=, =, <>, !=, BETWEEN, IN`
- Pattern matching operators: `LIKE`
- Mathematical operators: `+, -, *, %`

> For more information on operators, see [Operators](https://intl.cloud.tencent.com/document/product/436/32477).



## Initiating an extraction request

You can initiate an extraction request using the console, API, or SDK:

- If you use the console, see [Data Extraction](https://intl.cloud.tencent.com/document/product/436/32538).
- If you use the API, see SELECT Object Content.
- If you use the SDK, go to [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474) and select the required SDK API.

## FAQ

If a problem occurs when you execute on a query, COS Select will return an error code and associated error message. For the list of error codes and descriptions, see [Special Error Codes](https://cloud.tencent.com/document/product/436/37641#errorcode).                      
