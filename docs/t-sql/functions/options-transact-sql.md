---
title: "@@OPTIONS (Transact-SQL)"
description: "@@OPTIONS (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "09/18/2017"
ms.prod: sql
ms.technology: t-sql
ms.topic: reference
f1_keywords:
  - "@@OPTIONS"
  - "@@OPTIONS_TSQL"
helpviewer_keywords:
  - "SET statement, current SET options"
  - "@@OPTIONS function"
  - "current SET options"
dev_langs:
  - "TSQL"
---
# &#x40;&#x40;OPTIONS (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns information about the current SET options.  
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql  
@@OPTIONS  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Return Types
 **integer**  
  
## Remarks  
 The options can come from use of the **SET** command or from the **sp_configure user options** value. Session values configured with the **SET** command override the **sp_configure** options. Many tools (such as [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] automatically configure set options. Each user has an @@OPTIONS function that represents the configuration.  
  
 You can change the language and query-processing options for a specific user session by using the SET statement. **\@\@OPTIONS** can only detect the options which are set to ON or OFF.  
  
 The **\@\@OPTIONS** function returns a bitmap of the options, converted to a base 10 (decimal) integer. The bit settings are stored in the locations described in a table in the topic [Configure the user options Server Configuration Option](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md).  
  
 To decode the **\@\@OPTIONS** value, convert the integer returned by **\@\@OPTIONS** to binary, and then look up the values on the table at [Configure the user options Server Configuration Option](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md). For example, if `SELECT @@OPTIONS;` returns the value `5496`, use the Windows programmer calculator (**calc.exe**) to convert decimal `5496` to binary. The result is `1010101111000`. The right most characters (binary 1, 2, and 4) are 0, indicating that the first three items in the table are off. Consulting the table, you see that those are **DISABLE_DEF_CNST_CHK** and **IMPLICIT_TRANSACTIONS**, and **CURSOR_CLOSE_ON_COMMIT**. The next item (**ANSI_WARNINGS** in the `1000` position) is on. Continue working left though the bit map, and down in the list of options. When the left-most options are 0, they are truncated by the type conversion. The bit map `1010101111000` is actually `001010101111000` to represent all 15 options.  
  
## Examples  
  
### A. Demonstration of how changes affect behavior  
 The following example demonstrates the difference in concatenation behavior with two different setting of the **CONCAT_NULL_YIELDS_NULL** option.  
  
```sql  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### B. Testing a client NOCOUNT setting  
 The following example sets `NOCOUNT``ON` and then tests the value of `@@OPTIONS`. The `NOCOUNT``ON` option prevents the message about the number of rows affected from being sent back to the requesting client for every statement in a session. The value of `@@OPTIONS` is set to `512` (0x0200). This represents the NOCOUNT option. This example tests whether the NOCOUNT option is enabled on the client. For example, it can help track performance differences on a client.  
  
```sql  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## See Also  
 [Configuration Functions &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Configure the user options Server Configuration Option](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
