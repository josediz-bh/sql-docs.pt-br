---
title: Sincronizar relógios dos servidores de destino (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 769b2b9caba541af3a1ea38e1969d8a6422950be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68188770"
---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>Synchronize Target Server Clocks (SQL Server Management Studio)
  Este tópico descreve como sincronizar os relógios dos servidores de destino no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com o relógio do servidor mestre usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Sincronizar esses relógios do sistema dá suporte às agendas de trabalho.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para sincronizar os relógios do servidor de destino usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar os relógios dos servidores de destino  
  
1.  No **Pesquisador de Objetos,** clique no sinal de adição para expandir o servidor onde você deseja sincronizar os relógios dos servidores de destino com o relógio do servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e selecione **Gerenciar Servidores de Destino**.  
  
3.  Na caixa de diálogo **Gerenciar Servidores de Destino** , clique em **Postar Instruções**.  
  
4.  Na lista **Tipo de instrução** , selecione **Sincronizar relógios**.  
  
5.  Em **Destinatários**, siga um destes procedimentos:  
  
    -   Clique em **Todos os servidores de destino** para sincronizar os relógios de todos os servidores de destino com o relógio do servidor mestre.  
  
    -   Clique em **Estes servidores de destino** para sincronizar os relógios de apenas alguns servidores de destino com o relógio do servidor mestre, selecionando cada um deles.  
  
6.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar os relógios dos servidores de destino  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_resync_targetserver &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql).  
  
  
