---
title: sp_help_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b44f5962e8241afa95b9e68cf75d493dff01ad5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304810"
---
# <a name="sp_help_category-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre as classes especificadas de trabalhos, alertas ou operadores.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @class = ] 'class'`A classe sobre a qual as informações são solicitadas. a *classe* é **varchar (8)**, com um valor padrão de **trabalho**. a *classe* pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**TRABALHO**|Fornece informações sobre uma categoria de trabalho.|  
|**ALERTA**|Fornece informações sobre uma categoria de alerta.|  
|**OPERADOR**|Fornece informações sobre uma categoria de operador.|  
  
`[ @type = ] 'type'`O tipo de categoria para o qual as informações são solicitadas. o *tipo* é **varchar (12)**, com um padrão de NULL e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**LOCAL**|Categoria de trabalho local.|  
|**MULTI -SERVER**|Categoria de trabalho multisservidor.|  
|**NONE**|Categoria para uma classe que não seja **trabalho**.|  
  
`[ @name = ] 'name'`O nome da categoria para a qual as informações são solicitadas. o *nome* é **sysname**, com um padrão de NULL.  
  
`[ @suffix = ] suffix`Especifica se a coluna **category_type** no conjunto de resultados é uma ID ou um nome. o *sufixo* é **bit**, com um padrão de **0**. **1** mostra o **category_type** como um nome e **0** o mostra como uma ID.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando ** \@o sufixo** é **0**, **sp_help_category** retorna o seguinte conjunto de resultados:  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID da categoria|  
|**category_type**|**tinyint**|Tipo de categoria:<br /><br /> **1** = local<br /><br /> **2** = multisservidor<br /><br /> **3** = nenhum|  
|**name**|**sysname**|Nome da categoria|  
  
 Quando ** \@o sufixo** é **1**, **sp_help_category** retorna o seguinte conjunto de resultados:  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID da categoria|  
|**category_type**|**sysname**|Tipo de categoria. Um dos **locais**, **vários servidores**ou **nenhum**|  
|**name**|**sysname**|Nome da categoria|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_category** deve ser executado do banco de dados **msdb** .  
  
 Se nenhum parâmetro for especificado, o conjunto de resultados fornecerá informações sobre todas as categorias de trabalho.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-local-job-information"></a>a. Retornando informações do trabalho local  
 O exemplo a seguir retorna informações sobre trabalhos que são administrados localmente.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. Retornando informações de alerta  
 O exemplo a seguir retorna informações sobre a categoria de alerta Replication.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_category](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_category](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_category](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
