---
title: Conectando-se ao SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4f40fd6fa88b001eaa222789d6be35b83f9bf90a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948542"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Conectar-se ao SQL Server (SybaseToSQL)
Para migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para o, você deve se conectar a qualquer uma das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instâncias de destino do. Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe os metadados do banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no Gerenciador de metadados. O SSMA armazena informações sobre a qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância do você está conectado, mas não armazena senhas.  
  
Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.  
  
Os metadados sobre a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do não são sincronizados automaticamente. Em vez disso, se você quiser atualizar os metadados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Gerenciador de metadados, deverá atualizar manualmente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os metadados, conforme descrito na seção "sincronizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados" mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias  
A conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer permissões diferentes dependendo das ações que são executadas por essa conta.  
  
-   Para converter objetos do ASE [!INCLUDE[tsql](../../includes/tsql-md.md)] em sintaxe, atualizar metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para carregar objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de dados no, o requisito mínimo de permissão é a associação na função de banco de dados **db_owner** no banco de dados de destino.  
  
-   Para migrar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para o, a conta deve ser membro da função de servidor **sysadmin** . Isso é necessário para executar os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacotes de migração de dados do agente.  
  
-   Para executar o código gerado pelo SSMA, a conta deve ter permissões de **execução** para todas as funções definidas pelo usuário no esquema de **ssma_syb** do banco de dados **sysdb** . Essas funções fornecem funcionalidade equivalente às funções do sistema ASE e são usadas por objetos convertidos.  
  
Se a conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for executar todas as tarefas de migração, a conta deverá ser membro da função de servidor **sysadmin** .  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server  
Antes de converter objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados do ase em sintaxe, você deve estabelecer uma conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a instância do em que você deseja migrar o banco de dados ase ou bancos.  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do ASE depois de se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]conectar ao. Para obter mais informações, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Server**.  
  
    Se você se conectou anteriormente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ao, o nome do comando será **reconectado a SQL Server**.  
  
2.  Na caixa de diálogo conexão, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome da instância, como MyServer\MyInstance.  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do serviço navegador.  
  
4.  Na caixa **banco de dados** , digite o nome do banco de dados de destino.  
  
    Essa opção não está disponível ao reconectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ao.  
  
5.  Na caixa **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação** e, em seguida, forneça o nome de logon e a senha.  
  
6.  Para conexão segura, dois controles são adicionados, as caixas de seleção **criptografar conexão** e **TrustServerCertificate** . Somente quando a opção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando **criptografar conexão** está marcado (true) e **TrustServerCertificate** está desmarcado (false), ele validará o SQL Server certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Compatibilidade de versão superior**  
  
-   Você [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá se conectar a 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá se conectar a 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, mas não será possível se conectar a versões inferiores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar somente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado for SQL Server 2012.  
  
-   A compatibilidade de versão superior não é válida para SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**TIPO de projeto vs. versão do servidor de destino**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005<br /> (Versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008<br /> (Versão: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />(Versão: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Versão: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Versão: 13. x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||Sim|Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sim|Sim|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sim||  
|SQL Azure||||||Sim|  
  
> [!IMPORTANT]
> A conversão dos objetos de banco de dados é executada de acordo com o tipo de projeto, mas não de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acordo com a versão do à qual você está conectado. No caso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] projeto 2005, a conversão é realizada de acordo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com 2005, mesmo que você esteja conectado a uma versão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou 2014 ou 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Reconectando ao SQL Server  
Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até atualizar os metadados, carregar objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de dados em e migrar os mesmos.  
  
O procedimento para reconectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a é o mesmo que o procedimento para estabelecer uma conexão.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server  
Os metadados sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os bancos de dados não são atualizados automaticamente. Os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados é um instantâneo dos metadados quando você se conecta pela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]primeira vez ao, ou na última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual.  
  
**Para sincronizar metadados**  
  
1.  Certifique-se de que você está [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]conectado ao.  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de **bancos de dados**.  
  
3.  Clique com o botão direito do mouse em bancos de dados ou em um esquema de banco de dados individual ou em seu próprio e selecione **sincronizar com Banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Se você quiser personalizar o mapeamento entre bancos de dados do ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas e bancos de dados e esquemas, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Se você quiser personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   Se você quiser personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando os tipos de dados do Sybase ase e SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Se você não precisar fazer nenhuma delas, poderá converter as definições de objeto de banco de dados do Sybase ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em definições de objeto. Para obter mais informações, consulte [convertendo objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
