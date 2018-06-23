---
title: FILESTREAM DDL, funções, procedimentos armazenados e exibições | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ecb49ee-f64e-4d30-a803-e4064a21950a
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9784b7e524d1094ed6cccb1604f71ff6bbc7cf58
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009565"
---
# <a name="filestream-ddl-functions-stored-procedures-and-views"></a>FILESTREAM DDL, funções, procedimentos armazenados e exibições
  Lista as instruções Transact-SQL e os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que oferecem suporte para FILESTREAM.  
  
 Para obter a lista de objetos de banco de dados que oferecem suporte ao recurso FileTable, consulte [FileTable DDL, Functions, Stored Procedures, and Views](../views/views.md).  
  
##  <a name="ddl"></a> Instruções DDL (linguagem de definição de dados) Transact-SQL  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)DROP INDEX  
  
##  <a name="func"></a> Funções de sistema  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT &#40;Transact-SQL&#41;](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql)  
  
-   [PathName &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/pathname-transact-sql)  
  
##  <a name="proc"></a> Procedimentos armazenados do sistema  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection)  
  
##  <a name="cat"></a> Exibições do sistema – exibições do catálogo  
  
-   [sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)  
  
##  <a name="dmv"></a> Exibições do sistema – exibições de gerenciamento dinâmico  
  
-   [sys.dm_filestream_file_io_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql)  
  
-   [sys.dm_filestream_file_io_requests &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql)  
  
##  <a name="api"></a> APIs de programação  
  
-   [Acessar dados do FILESTREAM com OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)  
  
-   [API gerenciada - classe SqlFileStream](http://go.microsoft.com/fwlink/?LinkId=220875)  
  
  