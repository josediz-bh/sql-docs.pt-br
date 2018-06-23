---
title: Exibir uma lista de bancos de dados em uma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- current databases
- databases currently on server [SQL Server]
- database list [SQL Server]
- viewing database list
- displaying database list
- databases [SQL Server], viewing
- servers [SQL Server], databases listed on
- listing databases
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f7c4e34b8aaffef592927edc718da214939ec8b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006118"
---
# <a name="view-a-list-of-databases-on-an-instance-of-sql-server"></a>Exibir uma lista de bancos de dados em uma instância do SQL Server
  Este tópico descreve como exibir uma lista de bancos de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir uma lista de bancos de dados em uma instância do SQL Server usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Se o chamador de **sys.databases** não for o proprietário do banco de dados e o banco de dados não for o **master** ou **tempdb**, as permissões mínimas necessárias para ver a linha correspondente serão as permissões em nível de servidor ALTER ANY DATABASE ou VIEW ANY DATABASE ou a permissão CREATE DATABASE no banco de dados **master** . O banco de dados ao qual o chamador está conectado sempre pode ser exibido em **sys.databases**.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>Para exibir uma lista de bancos de dados em uma instância do SQL Server  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Para consultar uma lista de todos os bancos de dados na instância, expanda **Bancos de Dados**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>Para exibir uma lista de bancos de dados em uma instância do SQL Server  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo retorna uma lista dos bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A lista inclui os nomes dos bancos de dados, suas IDs de banco de dados e as datas de criação dos bancos de dados.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de catálogo do bancos de dados e de arquivos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  