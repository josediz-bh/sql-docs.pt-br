---
title: Configurar opções de inicialização do servidor (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 91a48d4acd771c19617bac26c1393f30334768e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62810359"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a>Configurar opções de inicialização do servidor (SQL Server Configuration Manager)
  Este tópico descreve como configurar as opções de inicialização que serão usadas sempre que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for iniciado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Para obter uma lista de opções de inicialização, veja [Opções de inicialização do serviço Mecanismo de Banco de Dados](database-engine-service-startup-options.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager grava parâmetros de inicialização no Registro. Eles entram em vigor na próxima vez que o [!INCLUDE[ssDE](../../includes/ssde-md.md)]for inicializado.  
  
 Em um cluster, as alterações devem ser feitas no servidor ativo quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está online, e entrarão em vigor quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for reinicializado. A atualização do Registro das opções de inicialização no outro nó acontecerá no próximo failover.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A configuração de opções de inicialização de servidor é restrita a usuários que podem alterar as entradas relacionadas no Registro. Isso inclui os seguintes usuários.  
  
-   Membros do grupo Administradores local.  
  
-   A conta de domínio usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver configurado para ser executado em uma conta de domínio.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-configure-startup-options"></a>Para configurar as opções de inicialização  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, clique em **Serviços do SQL Server**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **página inicial**, digite SQLServerManager12. msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua 12 por um número menor. Clique em SQLServerManager12.msc para abrir o Configuration Manager. Para fixar o Configuration Manager na página inicial ou na barra de tarefas, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **abrir local do arquivo**. No explorador de arquivos do Windows, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **fixar para iniciar** ou **fixar na barra de tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar** , em **aplicativos**, digite **SQLServerManager\<versão>. msc** , como `SQLServerManager12.msc`e pressione **Enter**.  
  
2.  No painel direito, clique com o botão direito do mouse em **SQL Server (***<instance_name>***)** e clique em **Propriedades**.  
  
3.  Na guia **Parâmetros de Inicialização** , na caixa **Especificar um parâmetro de inicialização** , digite o parâmetro e clique em **Adicionar**.  
  
     Por exemplo, para iniciar no modo de usuário único, digite `-m` na caixa **especificar um parâmetro de inicialização** e clique em **Adicionar**. (Ao reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, interrompa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent poderá se conectar primeiro e impedir sua conexão como um segundo usuário.)  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Reinicie o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!WARNING]  
    >  Depois de terminar de usar o modo de usuário único, na caixa parâmetros de inicialização, selecione `-m` o parâmetro na caixa **parâmetros existentes** e clique em **remover**. Reinicie o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para restaurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o modo multiusuário típico.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o SQL Server no modo de usuário único](start-sql-server-in-single-user-mode.md)   
 [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
