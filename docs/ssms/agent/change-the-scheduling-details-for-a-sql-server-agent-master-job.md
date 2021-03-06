---
title: Alterar os detalhes de agendamento de um trabalho mestre
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: f5414451-4d8e-464b-bd9e-f2b70c6899b3
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 45eddc3b97099eafdba01ec091f3e860f1b2ab8e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242542"
---
# <a name="change-the-scheduling-details-for-a-sql-server-agent-master-job"></a>Change the Scheduling Details for a SQL Server Agent Master Job

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como alterar os detalhes do agendamento para uma definição de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e restrições  
Um trabalho mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não pode ser destino em ambos os servidores, local e remoto.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
A menos que seja membro da função de servidor fixa **sysadmin** , você poderá modificar somente trabalhos de sua propriedade. Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>Para alterar os detalhes do agendamento de uma definição de trabalho  
  
1. No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor que contém o trabalho cujo agendamento você deseja editar.  
  
2. Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3. Clique no sinal de adição para expandir a pasta **Trabalhos** .  
  
4. Clique com o botão direito do mouse no trabalho cujo agendamento você quer editar e selecione **Propriedades**.  
  
5. Na caixa de diálogo **Propriedades do Trabalho –** _job\_name_, em **Selecionar uma Página**, selecione **Agendamentos**. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Agendamentos&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md).  
  
6. Quando terminar, clique em **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>Para alterar os detalhes do agendamento de uma definição de trabalho
  
1. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2. Na barra Padrão, clique em **Nova Consulta**.  
  
3. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- changes the enabled status of the NightlyJobs schedule to 0
    -- and sets the owner to terrid.
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_schedule  
        @name = 'NightlyJobs',  
        @enabled = 0,  
        @owner_login_name = 'terrid' ;  
    GO  
    ```  
  
Para obter mais informações, veja [sp_update_schedule (Transact-SQL)](https://msdn.microsoft.com/97b3119b-e43e-447a-bbfb-0b5499e2fefe).