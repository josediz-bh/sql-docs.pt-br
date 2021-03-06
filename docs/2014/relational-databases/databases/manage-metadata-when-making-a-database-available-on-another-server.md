---
title: Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- cross-database queries [SQL Server]
- logins [SQL Server], recreating on another server instance
- triggers [SQL Server], DLL
- user-defined error messages [SQL Server]
- permissions [SQL Server], metadata access
- Full-Text Engine [SQL Server]
- metadata [SQL Server], databases available to other instances
- jobs [SQL Server Agent], recreating on another server instance
- failover [SQL Server], managing metadata
- event notifications [SQL Server], metadata
- database mirroring [SQL Server], metadata
- startup options [SQL Server]
- restoring [SQL Server], onto another server instance
- linked servers [SQL Server], metadata
- WMI Provider for Server Events, metadata
- attaching databases [SQL Server]
- log shipping [SQL Server], metadata
- encryption [SQL Server], metadata
- server configuration [SQL Server]
- distributed queries [SQL Server], metadata
- extended stored procedures [SQL Server], metadata
- credentials [SQL Server], metadata
- copying databases
ms.assetid: 5d98cf2a-9fc2-4610-be72-b422b8682681
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b87c66eab08243a6339f1eb2bc1912e469f2b80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76929912"
---
# <a name="manage-metadata-when-making-a-database-available-on-another-server-instance-sql-server"></a>Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor (SQL Server)
  Este tópico é pertinente nas seguintes situações:  
  
-   Configuração das réplicas de disponibilidade de um grupo de disponibilidade do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .  
  
-   Ao configurar o espelhamento de banco de dados de um banco de dados.  
  
-   Ao preparar a alteração de funções entre servidores primário e secundário em uma configuração de envio de logs.  
  
-   Ao restaurar um banco de dados para outra instância de servidor.  
  
-   Ao anexar uma cópia de um banco de dados a outra instância do servidor.  
  
 Alguns aplicativos dependem de informações, entidades e/ou objetos que estão fora do escopo de um único banco de dados de usuário. Normalmente, um aplicativo tem dependências no banco de dados **mestre** e **msdb** e também no banco de dados de usuário. Qualquer coisa armazenada fora de um banco de dados de usuário que seja necessária para o funcionamento correto daquele banco de dados deve estar disponível na instância do servidor de destino. Por exemplo, os logons de um aplicativo são armazenados como metadados no banco de dados **mestre** e devem ser recriados no servidor de destino. Se um plano de manutenção de um banco de dados ou aplicativo depender de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent cujos metadados estão armazenados no banco de dados **msdb** , será necessário recriar esses trabalhos na instância do servidor de destino. De maneira semelhante, os metadados de um gatilho em nível de servidor são armazenados no **mestre**.  
  
 Ao mover o banco de dados de um aplicativo para outra instância de servidor, você deve recriar todos os metadados das entidades e objetos dependentes no **mestre** e no **msdb** na instância do servidor de destino. Por exemplo, se um aplicativo de banco de dados usar gatilhos em nível de servidor, apenas a anexação ou a restauração do banco de dados no novo sistema não será suficiente. O banco de dados não funcionará conforme o esperado, a menos que você recrie os metadados para esses gatilhos manualmente no banco de dados **mestre** .  
  
##  <a name="information_entities_and_objects"></a>Informações, entidades e objetos que são armazenados fora dos bancos de dados de usuário  
 O restante deste tópico resume os problemas potenciais que podem afetar um banco de dados que está sendo disponibilizado em outra instância de servidor. Talvez você precise recriar um ou mais dos tipos de informações, entidades ou objetos apresentados na lista a seguir. Para ver um resumo, clique no link do item.  
  
-   [Definições de configuração do servidor](#server_configuration_settings)  
  
-   [Credenciais](#credentials)  
  
-   [Consultas entre bancos de dados](#cross_database_queries)  
  
-   [Propriedade de banco de dados](#database_ownership)  
  
-   [Consultas distribuídas/servidores vinculados](#distributed_queries_and_linked_servers)  
  
-   [Dados criptografados](#encrypted_data)  
  
-   [Mensagens de erro definidas pelo usuário](#user_defined_error_messages)  
  
-   [Notificações de eventos e eventos de Instrumentação de Gerenciamento do Windows (WMI) (em nível de servidor)](#event_notif_and_wmi_events)  
  
-   [Procedimentos armazenados estendidos](#extended_stored_procedures)  
  
-   [Mecanismo de texto completo para propriedades de SQL Server](#ifts_service_properties)  
  
-   [Trabalhos](#jobs)  
  
-   [Logons](#logins)  
  
-   [Permissões](#permissions)  
  
-   [Configurações de replicação](#replication_settings)  
  
-   [Service Broker aplicativos](#sb_applications)  
  
-   [Procedimentos de inicialização](#startup_procedures)  
  
-   [Gatilhos (em nível de servidor)](#triggers)  
  
##  <a name="server_configuration_settings"></a>Definições de configuração do servidor  
 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores instala seletivamente e inicia serviços e recursos chave. Isso ajuda a reduzir a área da superfície de um sistema sujeita a ataque. Na configuração padrão de novas instalações, muitos recursos não estão habilitados. Se o banco de dados depende de qualquer serviço ou recurso que esteja desativado por padrão, esse serviço ou recurso deve ser habilitado na instância do servidor de destino.  
  
 Para obter mais informações sobre essas configurações e como habilitá-las ou desabilitá-las, veja [Opções de configuração de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="credentials"></a>Fornecidas  
 Uma credencial é um registro que contém as informações de autenticação necessárias para conectar-se a um recurso fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A maioria das credenciais consiste em um logon e uma senha do Windows.  
  
 Para obter mais informações sobre esse recurso, veja [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../security/authentication-access/credentials-database-engine.md).  
  
> [!NOTE]  
>  Contas proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usam credenciais. Para saber a identificação da credencial de uma conta proxy, use a tabela do sistema [sysproxies](/sql/relational-databases/system-tables/dbo-sysproxies-transact-sql) .  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="cross_database_queries"></a>Consultas entre bancos de dados  
 Por padrão, as opções de banco de dados DB_CHAINING e TRUSTWORTHY estão OFF. Se qualquer uma delas estiver configurada como ON para o banco de dados original, talvez seja necessário habilitá-las no banco de dados na instância do servidor de destino. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 As operações de anexação e desanexação desabilitam o encadeamento de propriedades de bancos de dados para o banco de dados. Para obter informações sobre como habilitar o encadeamento, veja [Opção cross db ownership chaining de configuração de servidor](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
 Para obter mais informações, veja também [Configurar um banco de dados espelho para usar a propriedade confiável &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="database_ownership"></a>Propriedade do banco de dados  
 Quando um banco de dados é restaurado em outro computador, o logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usuário Windows que iniciou a operação de restauração torna-se automaticamente o novo proprietário do banco de dados. Quando o banco de dados é restaurado, o administrador de sistema ou o novo proprietário do banco de dados pode alterar a propriedade do banco de dados.  
  
##  <a name="distributed_queries_and_linked_servers"></a> Consultas distribuídas e servidores vinculados  
 Há suporte para consultas distribuídas e servidores vinculados para aplicativos OLE DB. Consultas distribuídas acessam dados de várias fontes de dados heterogêneos no mesmo ou em diferentes computadores. Uma configuração de servidores vinculados permite ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executar comandos em relação a fontes de dados de OLE DB em servidores remotos. Para obter mais informações sobre esses recursos, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../linked-servers/linked-servers-database-engine.md).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="encrypted_data"></a>Dados criptografados  
 Se o banco de dados que está sendo disponibilizado em outra instância do servidor contiver dados criptografados e se a chave mestra do banco de dados estiver protegida pela chave mestra do serviço no servidor original, talvez seja necessário recriar a criptografia da chave mestra do serviço. A *chave mestra do banco de dados* é uma chave simétrica usada para proteger as chaves privadas dos certificados e as chaves assimétricas em um banco de dados criptografado. Quando criada, a chave mestra do banco de dados é criptografada com o algoritmo DES Triplo e uma senha fornecida pelo usuário.  
  
 Para permitir a descriptografia automática da chave mestra do banco de dados em uma instância do servidor, uma cópia dessa chave é criptografada usando a chave mestra do serviço. Esta cópia criptografada é armazenada no banco de dados e no **mestre**. Normalmente, a cópia armazenada no **mestre** é silenciosamente atualizada sempre que a chave mestra é alterada. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta primeiramente descriptografar a chave mestra do banco de dados com a chave de serviço mestra da instância. Se essa descriptografia falhar, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o repositório de credenciais em busca das credenciais de chave mestra que têm o mesmo GUID de família do banco de dados cuja chave mestra é necessária. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta descriptografar a chave mestra de banco de dados com cada credencial compatível até que a descriptografia obtenha êxito ou não haja mais credenciais. Uma chave mestra não criptografada pela chave mestra de serviço deve ser aberta usando a instrução OPEN MASTER KEY e uma senha.  
  
 Quando um banco de dados criptografado é copiado, restaurado ou anexado a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra do banco de dados criptografada pela chave mestra do serviço não é armazenada no **mestre** na instância do servidor de destino. Na instância do servidor de destino, você deve abrir a chave mestra do banco de dados. Para abrir a chave mestra, execute esta instrução: OPEN MASTER KEY DECRYPTION BY PASSWORD **='***password***'**. Recomendamos que, em seguida, a descriptografia automática da chave mestra do banco de dados seja habilitada executando a seguinte instrução: ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY. Essa instrução ALTER MASTER KEY fornece à instância do servidor uma cópia da chave mestra do banco de dados que é criptografada com a chave mestra do serviço. Para obter mais informações, veja [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) e [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
 Para obter informações sobre como habilitar a descriptografia automática da chave mestra de um banco de dados espelho, veja [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md).  
  
 Para obter mais informações, consulte também:  
  
-   [Hierarquia de criptografia](../security/encryption/encryption-hierarchy.md)  
  
-   [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [Criar chaves simétricas idênticas em dois servidores](../security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="user_defined_error_messages"></a>Mensagens de erro definidas pelo usuário  
 Mensagens de erro definidas pelo usuário residem na exibição do catálogo [sys.messages](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages) . Essa exibição do catálogo é armazenada no **mestre**. Se um aplicativo de banco de dados depender de mensagens de erro definidas pelo usuário e o banco de dados for disponibilizado em outra instância do servidor, use [sp_addmessage](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql) para adicionar essas mensagens definidas pelo usuário à instância do servidor de destino.  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="event_notif_and_wmi_events"></a>Notificações de eventos e eventos de Instrumentação de Gerenciamento do Windows (WMI) (em nível de servidor)  
  
### <a name="server-level-event-notifications"></a>Notificações de eventos em nível de servidor  
 Notificações de eventos em nível de servidor são armazenadas no **msdb**. Portanto, se um aplicativo de banco de dados depender de uma notificação de eventos em nível de servidor, essa notificação de evento deve ser recriada na instância do servidor de destino. Para exibir as notificações de eventos em uma instância do servidor, use a exibição de catálogo [sys.server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql) . Para obter mais informações, consulte [Event Notifications](../service-broker/event-notifications.md).  
  
 Além disso, notificações de eventos são entregues usando [!INCLUDE[ssSB](../../includes/sssb-md.md)]. As rotas para mensagens recebidas não estão incluídas no banco de dados que contém um serviço. Em vez disso, rotas explícitas são armazenadas no **msdb**. Se o serviço usar uma rota explícita no banco de dados **msdb** para encaminhar mensagens de entrada para o serviço, quando você anexar um banco de dados em uma instância diferente, será necessário recriar essa rota.  
  
### <a name="windows-management-instrumentation-wmi-events"></a>Eventos da Instrumentação de Gerenciamento do Windows (WMI)  
 O Provedor WMI para Eventos do Servidor permite usar o WMI para monitorar eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Qualquer aplicativo que dependa de eventos em nível de servidor expostos por meio do provedor WMI do qual um banco de dados dependa deve ser definido no computador da instância do servidor de destino. O provedor de eventos WMI cria notificações de eventos com um serviço de destino definido no **msdb**.  
  
> [!NOTE]  
>  Para obter mais informações, veja [Provedor WMI para conceitos de eventos de servidor](../wmi-provider-server-events/wmi-provider-for-server-events-concepts.md).  
  
 **Para criar um alerta WMI usando SQL Server Management Studio**  
  
-   [Criar um alerta de eventos WMI](../../ssms/agent/create-a-wmi-event-alert.md)  
  
### <a name="how-event-notifications-work-for-a-mirrored-database"></a>Como notificações de eventos funcionam para um banco de dados espelho  
 A entrega de notificações de eventos entre bancos de dados envolvendo um banco de dados espelho é remota, por definição, porque o banco de dados espelho pode efetuar failover. [!INCLUDE[ssSB](../../includes/sssb-md.md)]fornece suporte especial para bancos de dados espelhados, na forma de *rotas espelhadas*. Uma rota espelhada tem dois endereços: um para a instância do servidor principal e um para a instância do servidor espelho.  
  
 Com a configuração de rotas espelhadas, você faz com que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] reconheça o espelhamento do banco de dados. As rotas espelhadas permitem que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] redirecione conversações transparentemente para a instância de servidor principal atual. Por exemplo, considere um serviço, Service_A que é hospedado por um banco de dados espelho, Database_A. Assuma que você precisa de outro serviço, Service_B, que é hospedado pelo Database_B, para dialogar com o Service_A. Para que esse diálogo seja possível, o Database_B deve conter uma rota espelhada para o Service_A. Além disso, o Database_A deve conter uma rota de transporte TCP não espelhada para o Service_B, que, ao contrário de uma rota local, permaneça válida após um failover. Essas rotas permitem que ACKs sejam retornados após um failover. Como o serviço do remetente é sempre nomeado da mesma maneira, a rota deve especificar a instância do agente.  
  
 O requisito de rotas espelhadas se aplica independentemente do fato de o serviço no banco de dados espelho ser o serviço iniciador ou o serviço de destino:  
  
-   O serviço de destino está no banco de dados espelho, o serviço iniciador deve ter uma rota espelhada para retorno ao destino. No entanto, o destino pode ter uma rota normal de retorno ao iniciador.  
  
-   Se o serviço iniciador estiver no banco de dados espelho, o serviço de destino deverá ter uma rota espelhada de retorno ao iniciador para entregar confirmações e respostas. No entanto, o iniciador pode ter uma rota normal para o destino.  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="extended_stored_procedures"></a>Procedimentos armazenados estendidos  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use a [integração CLR](../clr-integration/common-language-runtime-integration-overview.md) .  
  
 Procedimentos armazenados estendidos são programados usando a API de Procedimento Armazenado Estendido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um membro da função de servidor fixa **sysadmin** pode registrar um procedimento armazenado estendido em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e conceder permissão aos usuários para executar o procedimento. Os procedimentos armazenados estendidos só podem ser adicionados ao banco de dados **mestre** .  
  
 Os procedimentos armazenados estendidos executam diretamente no espaço de endereço de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e podem produzir vazamentos de memória ou outros problemas que reduzem o desempenho e a confiabilidade do servidor. Você deve pensar em armazenar procedimentos armazenados estendidos em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja separada da instância que contém os dados referenciados. Você também deve considerar o uso de consultas distribuídas para acessar o banco de dados.  
  
> [!IMPORTANT]  
>  Antes de adicionar procedimentos armazenados estendidos ao servidor e conceder permissões de EXECUTE a outros usuários, o administrador do sistema deve examinar detalhadamente cada procedimento armazenado estendido para verificar se ele não contém código nocivo ou mal-intencionado.   
  
 Para obter mais informações, veja [GRANT Object Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql), [DENY Object Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-object-permissions-transact-sql) e [REVOKE Object Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-object-permissions-transact-sql).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="ifts_service_properties"></a>Mecanismo de texto completo para propriedades de SQL Server  
 As propriedades são definidas no Mecanismo de Texto Completo por meio de [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql). Verifique se a instância do servidor de destino tem as configurações necessárias para essas propriedades. Para obter mais informações sobre essas propriedades, veja [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextserviceproperty-transact-sql).  
  
 Além disso, se o componente de [separadores de palavras e lematizadores](../search/configure-and-manage-word-breakers-and-stemmers-for-search.md) ou o componente de [filtros de pesquisa de texto completo](../search/configure-and-manage-filters-for-search.md) tiver versões diferentes nas instâncias de servidor original e de destino, o índice e as consultas de texto completo poderão se comportar de maneira diferente. O [dicionário de sinônimos](../search/full-text-search.md) também é armazenado em arquivos específicos da instância. Você deve transferir uma cópia desses arquivos para um local equivalente na instância do servidor de destino ou recriá-los na nova instância.  
  
> [!NOTE]  
>  Quando você anexa um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contém arquivos de catálogo de texto completo a uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , os arquivos de catálogo são anexados de seus locais anteriores junto com os outros arquivos de banco de dados, assim como ocorre no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../search/upgrade-full-text-search.md).  
  
 Para obter mais informações, consulte também:  
  
-   [Fazer backup e restaurar índices e catálogos de texto completo](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   [Espelhamento de banco de dados e catálogos de texto completo &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="jobs"></a>Sejam  
 Se o banco de dados depender de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, será necessário recriá-los na instância do servidor de destino. Os trabalhos dependem de seus ambientes. Se você planeja recriar um trabalho existente na instância do servidor de destino, a instância do servidor de destino talvez precise ser modificada para corresponder ao ambiente daquele trabalho na instância do servidor original. Os seguintes fatores ambientais são significativos:  
  
-   O logon usado pelo trabalho  
  
     Para criar ou executar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, é necessário primeiro adicionar todos os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exigidos pelo trabalho à instância do servidor de destino. Para obter mais informações, veja [Configurar um usuário para criar e gerenciar trabalhos do SQL Server Agent](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md).  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
     A conta de inicialização do serviço define a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado, bem como suas permissões de rede. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado como uma conta de usuário especificada. O contexto do serviço do Agent afeta as configurações do trabalho e seu ambiente de execução. A conta deve ter acesso aos recursos, como compartilhamentos de rede, exigidos pelo trabalho. Para obter informações sobre como selecionar e modificar a conta de inicialização de serviço, veja [Selecionar uma conta para o serviço SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md).  
  
     Para operar corretamente, a conta de inicialização do serviço deve ser configurada para ter o domínio, o sistema de arquivos e as permissões do Registro corretos. Além disso, um trabalho pode precisar de um recurso de rede compartilhado que deve ser configurado para a conta de serviço. Para obter informações, veja [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que está associado a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tem seu próprio hive do Registro e seus trabalhos normalmente são dependentes de uma ou mais configurações no hive do Registro. Para se comportar da maneira pretendida, um trabalho requer essas configurações do Registro. Se você usar um script para recriar um trabalho em outro serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, seu Registro talvez não tenha as configurações corretas para aquele trabalho. Para que trabalhos recriados se comportem corretamente em uma instância do servidor de destino, os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent original e de destino devem ter as mesmas configurações do Registro.  
  
    > [!CAUTION]  
    >  A alteração de configurações do Registro no serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent de destino para tratar um trabalho recriado poderá ser problemática se as configurações atuais forem necessárias para outros trabalhos. Além disso, a edição incorreta do Registro pode danificar seriamente o sistema. Antes de fazer alterações no Registro, é recomendável fazer backup dos dados importantes no computador.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
     Um proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent define o contexto de segurança de uma etapa de trabalho especificada. Para que um trabalho seja executado na instância do servidor de destino, todos os proxies requeridos por ele devem ser recriados manualmente naquela instância. Para obter mais informações, veja [Criar um Proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md) e [Solucionar problemas de trabalhos multisservidor que usam proxies](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md).  
  
 Para obter mais informações, consulte também:  
  
-   [Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
  
-   [Gerenciamento de logons e trabalhos após a troca de função &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md) (para espelhamento de banco de dados)  
  
-   [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (quando você instala uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instância do)  
  
-   [Configurar SQL Server Agent](../../ssms/agent/sql-server-agent.md) (quando você instala uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
  
-   [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
 **Para exibir os trabalhos existentes e suas propriedades**  
  
-   [Monitorar Atividade do Trabalho](../../ssms/agent/monitor-job-activity.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_job](/sql/relational-databases/system-stored-procedures/sp-help-job-transact-sql)  
  
-   [View Job Step Information](../../ssms/agent/view-job-step-information.md)  
  
-   [dbo. sysjobs &#40;&#41;Transact-SQL](/sql/relational-databases/system-tables/dbo-sysjobs-transact-sql)  
  
 **Para criar um trabalho**  
  
-   [Criar um trabalho](../../ssms/agent/create-a-job.md)  
  
-   [Criar um trabalho](../../ssms/agent/create-a-job.md)  
  
#### <a name="best-practices-for-using-a-script-to-re-create-a-job"></a>Práticas recomendadas para usar um script para recriar um trabalho  
 Recomendamos iniciar gerando o script de um trabalho simples, recriando o trabalho no outro serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e executando-o para ver se ele funciona conforme pretendido. Isto permitirá identificar incompatibilidades e tentar resolvê-las. Se um trabalho com script não funcionar conforme pretendido no novo ambiente, é recomendável criar um trabalho equivalente que funcione corretamente naquele ambiente.  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="logins"></a>Logons  
 O logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Esse logon é usado no processo de autenticação que verifica se a entidade pode conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um usuário de banco de dados para o qual o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente não está definido ou está definido incorretamente em uma instância do servidor não pode fazer logon na instância. Esse usuário é um *usuário órfão* do banco de dados nessa instância do servidor. Um usuário de banco de dados pode se tornar órfão após um banco de dados ser restaurado, anexado ou copiado em uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para gerar um script para alguns ou todos os objetos na cópia original do banco de dados, é possível usar o Assistente para Gerar Scripts e, na caixa de diálogo **Escolher Opções de Script** , configurar a opção **Logons de Script** como **True**.  
  
> [!NOTE]  
>  Para obter informações sobre como configurar logons para um banco de dados espelhado, veja [Configurar contas de logon para espelhamento de banco de dados ou para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md) e [Administração de logons e trabalhos após a troca de funções &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="permissions"></a> Permissões  
 Os seguintes tipos de permissão podem ser afetados quando um banco de dados é disponibilizado em outra instância do servidor.  
  
-   Permissões GRANT, REVOKE ou DENY em objetos do sistema  
  
-   Permissões GRANT, REVOKE ou DENY em instância de servidor (*permissões em nível de servidor*)  
  
### <a name="grant-revoke-and-deny-permissions-on-system-objects"></a>Permissões GRANT, REVOKE e DENY em objetos do sistema  
 Permissões para objetos do sistema, como procedimentos armazenados, procedimentos armazenados estendidos, funções e exibições, são armazenadas no banco de dados **mestre** e devem ser configuradas na instância do servidor de destino.  
  
 Para gerar um script para alguns ou todos os objetos na cópia original do banco de dados, é possível usar o Assistente para Gerar Scripts e, na caixa de diálogo **Escolher Opções de Script** , configurar a opção **Gerar Script de Permissões em Nível de Objeto** como **True**.  
  
> [!IMPORTANT]  
>  Se você gerar script de logons, as senhas não serão geradas no script. Se você tiver logons que usam a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será necessário modificar o script no destino.  
  
 Os objetos do sistema são visíveis na exibição de catálogo [sys.system_objects](/sql/relational-databases/system-catalog-views/sys-system-objects-transact-sql) . As permissões em objetos do sistema são visíveis na exibição de catálogo [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) do banco de dados **mestre** . Para obter informações sobre como consultar essas exibições de catálogo e conceder as permissões de objeto do sistema, veja [Permissões de objeto do sistema GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-system-object-permissions-transact-sql). Para obter mais informações, veja [Permissões de objeto do sistema REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-system-object-permissions-transact-sql) e [Permissões de objeto do sistema DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-system-object-permissions-transact-sql).  
  
### <a name="grant-revoke-and-deny-permissions-on-a-server-instance"></a>Permissões GRANT, REVOKE e DENY em uma instância de servidor  
 Permissões no escopo de servidor são armazenados no banco de dados **mestre** e devem ser configuradas na instância do servidor de destino. Para obter informações sobre as permissões de servidor de uma instância de servidor, consulte a exibição de catálogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) , para obter informações sobre entidades de servidor, consulte a exibição de catálogo [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql), e para obter informações sobre associação de funções de servidor, consulte a exibição de catálogo [sys.server_role_members](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql) .  
  
 Para obter mais informações, veja [Permissões de servidor GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql), [Permissões de servidor REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-server-permissions-transact-sql) e [Permissões de servidor REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-server-permissions-transact-sql).  
  
#### <a name="server-level-permissions-for-a-certificate-or-asymmetric-key"></a>Permissões em nível de servidor para um certificado ou chave assimétrica  
 As permissões em nível de servidor não podem ser concedidas diretamente a um certificado ou chave assimétrica. Em vez disso, as permissões em nível de servidor são concedidas a um logon mapeado que é criado exclusivamente para um certificado ou chave assimétrica específica. Portanto, cada certificado ou chave assimétrica que exija permissões em nível de servidor, precisa de seu próprio *logon mapeado por certificado* ou *logon mapeado por chave assimétrica*. Para conceder permissões em nível de servidor para um certificado ou chave assimétrica, conceda as permissões a seu logon mapeado.  
  
> [!NOTE]  
>  Um logon mapeado só é usado para autorização de código assinada com o certificado ou chave assimétrica correspondente. Logons mapeados não podem ser usados para autenticação.  
  
 O logon mapeado e suas permissões residem no **mestre**. Se um certificado ou chave assimétrica residir em outro banco de dados que não seja o **mestre**, ele deverá ser recriado no **mestre** e mapeado para um logon. Se você mover, copiar ou restaurar o banco de dados para outra instância de servidor, será necessário recriar seu certificado ou chave assimétrica no banco de dados **mestre** da instância do servidor de destino, mapeá-lo para um logon e conceder as permissões em nível de servidor necessárias ao logon.  
  
 **Para criar um certificado ou uma chave assimétrica**  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
 **Para mapear um certificado ou uma chave assimétrica para um logon**  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 **Para atribuir permissões ao logon mapeado**  
  
-   [CONCEDER permissões de servidor &#40;&#41;Transact-SQL](/sql/t-sql/statements/grant-server-permissions-transact-sql)  
  
 Para obter mais informações sobre certificados e chaves assimétricas, consulte [Encryption Hierarchy](../security/encryption/encryption-hierarchy.md).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="replication_settings"></a>Configurações de replicação  
 Se você restaurar um backup de um banco de dados replicado para outro servidor ou banco de dados, as configurações de replicação não poderão ser preservadas. Nesse caso, é necessário recriar todas as publicações e assinaturas depois que os backups forem restaurados. Para facilitar esse processo, crie scripts para suas configurações de replicação atuais e também para a habilitação e desabilitação da replicação. Para ajudar a recriar as configurações de replicação, copie esses scripts e altere as referências ao nome do servidor para funcionarem para a instância do servidor de destino.  
  
 Para obter mais informações, veja [Fazer backup e restaurar bancos de dados replicados](../replication/administration/back-up-and-restore-replicated-databases.md), [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md) e [Replicação e envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="sb_applications"></a>Service Broker aplicativos  
 Muitos aspectos de um aplicativo do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são movidos com o banco de dados. No entanto alguns aspectos do aplicativo devem ser recriados ou reconfigurados no novo local.  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="startup_procedures"></a>Procedimentos de inicialização  
 Um procedimento de inicialização é um procedimento armazenado marcado para execução automática e é executado sempre que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado. Se o banco de dados depender de qualquer procedimento de inicialização, o procedimento deverá ser definido na instância do servidor de destino e ser configurado para ser executado automaticamente na inicialização.  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
##  <a name="triggers"></a>Gatilhos (em nível de servidor)  
 Os gatilhos DDL ativam procedimentos armazenados em resposta a diversos eventos DDL (Linguagem de Definição de Dados). Esses eventos correspondem, principalmente, a instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que começam com as palavras-chave CREATE, ALTER e DROP. Determinados procedimentos armazenados do sistema que executam operações do tipo DDL também podem disparar gatilhos DDL.  
  
 Para obter mais informações sobre esse recurso, consulte [DDL Triggers](../triggers/ddl-triggers.md).  
  
 [&#91;Início&#93;](#information_entities_and_objects)  
  
## <a name="see-also"></a>Consulte Também  
 [Bancos de dados independentes](contained-databases.md)   
 [Copiar bancos de dados em outros servidores](copy-databases-to-other-servers.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [Fazer failover para um &#40;secundário de envio de logs SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)   
 [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
