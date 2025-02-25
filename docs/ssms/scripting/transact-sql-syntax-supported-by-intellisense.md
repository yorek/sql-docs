---
title: Transact-SQL Syntax Supported by IntelliSense
description: Learn which Transact-SQL statements and syntax elements are supported by SQL Server Management Studio IntelliSense in SQL Server 2019 (15.x).
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Transact-SQL IntelliSense"
  - "IntelliSense [SQL Server], Transact-SQL syntax"
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: markingmyname
ms.author: maghan
ms.reviewer: ""
ms.custom: seo-lt-2019
ms.date: "03/16/2017"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---

# Transact-SQL Syntax Supported by IntelliSense
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  This topic describes the [!INCLUDE[tsql](../../includes/tsql-md.md)] statements and syntax elements that are supported by IntelliSense in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].  
  
## Statements Supported by IntelliSense  
 In [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)], IntelliSense supports only the most commonly used [!INCLUDE[tsql](../../includes/tsql-md.md)] statements. Some general [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor conditions might prevent IntelliSense from functioning. For more information, see [Troubleshooting IntelliSense &#40;SQL Server Management Studio&#41;](./troubleshooting-intellisense.md).  
  
> [!NOTE]  
>  IntelliSense is not available for encrypted database objects, such as encrypted stored procedures or user-defined functions. Parameter help and Quick Info are not available for the parameters of extended stored procedures and CLR Integration user-defined types.  
  
### SELECT Statement  
 The [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor provides IntelliSense support for the following syntax elements in the SELECT statement:  
  
:::row:::
    :::column:::
        SELECT
    :::column-end:::
    :::column:::
        WHERE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        FROM
    :::column-end:::
    :::column:::
        ORDER BY
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        HAVING
    :::column-end:::
    :::column:::
        UNION
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        FOR
    :::column-end:::
    :::column:::
        GROUP BY
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        TOP
    :::column-end:::
    :::column:::
        OPTION (hint)
    :::column-end:::
:::row-end:::

### Additional Transact-SQL Statements That Are Supported  
 The [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor also provides IntelliSense support for [!INCLUDE[tsql](../../includes/tsql-md.md)] statements that are shown in the following table.  
  
|Transact-SQL statement|Syntax supported|Exceptions|  
|-----------------------------|----------------------|----------------|  
|[INSERT](../../t-sql/statements/insert-transact-sql.md)|All syntax, except the *execute_statement* clause.|None|  
|[UPDATE](../../t-sql/queries/update-transact-sql.md)|All syntax.|None|  
|[DELETE](../../t-sql/statements/delete-transact-sql.md)|All syntax.|None|  
|[DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)|All syntax.|None|  
|[SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)|All syntax.|None|  
|[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)|Execution of user-defined stored procedures, system stored procedures, user-defined functions, and system functions.|None|  
|[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)|All syntax.|None|  
|[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)|All syntax.|None|  
|[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)|All syntax.|There is no IntelliSense support for the EXTERNAL NAME clause.<br /><br /> In the AS clause, IntelliSense supports only the statements and syntax that are listed in this topic.|  
|[ALTER PROCEDURE](../../t-sql/statements/alter-procedure-transact-sql.md)|All syntax|There is no IntelliSense support for the EXTERNAL NAME clause.<br /><br /> In the AS clause, IntelliSense supports only the statements and syntax that are listed in this topic.|  
|[USE](../../t-sql/language-elements/use-transact-sql.md)|All syntax.|None|  
  
## IntelliSense in Supported Statements  
 IntelliSense in the [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor supports the following syntax elements when they are used in one of the supported [!INCLUDE[tsql](../../includes/tsql-md.md)] statements:  
  
-   All join types, including APPLY  
  
-   PIVOT and UNPIVOT  
  
-   References to the following database objects:  
  
    -   Databases and schemas  
  
    -   Tables, views, table-valued functions, and table expressions  
  
    -   Columns  
  
    -   Procedures and procedure parameters  
  
    -   Scalar functions and scalar expressions  
  
    -   Local variables  
  
    -   Common table expressions (CTE)  
  
-   Database objects that are referenced only in CREATE or ALTER statements in the script or batch, but which do not exist in the database because the script or batch has not yet been run. These objects are as follows:  
  
    -   Tables and procedures that have been specified in a CREATE TABLE or CREATE PROCEDURE statement in the script or batch.  
  
    -   Changes to tables and procedures that have been specified in an ALTER TABLE or ALTER PROCEDURE statement in the script or batch.  
  
    > [!NOTE]  
    >  IntelliSense is not available for the columns of a CREATE VIEW statement until the CREATE VIEW statement has been executed.  
  
 IntelliSense is not provided for the previously listed elements when they are used in other [!INCLUDE[tsql](../../includes/tsql-md.md)] statements. For example, there is IntelliSense support for column names that are used in a SELECT statement, but not for columns that are used in the CREATE FUNCTION statement.  
  
## Examples  
 Within a [!INCLUDE[tsql](../../includes/tsql-md.md)] script or batch, IntelliSense in the [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor supports only the statements and syntax that are listed in this topic. The following [!INCLUDE[tsql](../../includes/tsql-md.md)] code examples show what statements and syntax elements IntelliSense supports. For example, in the following batch, IntelliSense is available for the `SELECT` statement when it is coded by itself, but not when the `SELECT` is contained in a `CREATE FUNCTION` statement.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 This functionality also applies to the sets of [!INCLUDE[tsql](../../includes/tsql-md.md)] statements in the AS clause of a CREATE PROCEDURE or ALTER PROCEDURE statement.  
  
 Within a [!INCLUDE[tsql](../../includes/tsql-md.md)] script or batch, IntelliSense supports objects that have been specified in a CREATE or ALTER statement; however, these objects do not exist in the database because the statements have not been executed. For example, you might enter the following code in the Query Editor:  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 After you type `SELECT`, IntelliSense lists **PrimaryKeyCol**, **FirstNameCol**, and **LastNameCol** as possible elements in the select list, even if the script has not been executed and `MyTable` does not yet exist in `MyTestDB`.  
  
