---
title: Atualizar e migrar o Reporting Services | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 42cdcb1245e5280d25a94a81617da92f755ea048
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176936"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

Este tópico é uma visão geral das opções de atualização e migração para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Há duas abordagens gerais para se atualizar uma implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :

-   **Atualização:** Você atualiza os [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componentes nos servidores e instâncias em que eles estão instalados no momento. Isto é geralmente chamado de atualização “no local”. A atualização in-loco não tem suporte de um modo de servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para outro. Por exemplo, você não pode atualizar um servidor de relatório de modo nativo para um servidor de relatório no modo do SharePoint. Você pode migrar seus itens de relatório de um modo para outro. Para obter mais informações, consulte a seção "migração do Native para o SharePoint" mais adiante neste documento e o exemplo de tópico relacionado [Reporting Services o script RS. exe para migrar o conteúdo entre servidores de relatório](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).

-   **Migrar**: você instala e configura um novo ambiente do SharePoint, copia seus itens de relatório e recursos para o novo ambiente e configura o novo ambiente para usar o conteúdo existente. Uma forma de nível inferior de migração é copiar os bancos de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , arquivos de configuração e, se estiver usando o modo do SharePoint, os bancos de dados de conteúdo do SharePoint.

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint|

##  <a name="bkmk_top"></a>Neste tópico:

-   [Problemas conhecidos de atualização e práticas recomendadas](#bkmk_known_issues)

-   [Instalações lado a lado](#bkmk_side_by_side)

-   [Atualização in-loco](#bkmk_inplace_upgrade)

-   [Lista de verificação de pré-atualização](#bkmk_upgrade_checklist)

-   [Cenários de migração e atualização do modo nativo](#bkmk_native_scenarios)

-   [Atualizar uma implantação de expansão de Reporting Services modo nativo](#bkmk_native_scaleout)

-   [Cenários de atualização e migração do modo do SharePoint](#bkmk_sharePoint_scenarios)

-   [Considerações para uma migração](#bkmk_migration_considerations)

-   [Recursos adicionais](#bkmk_additional_resources)

##  <a name="bkmk_known_issues"></a>Problemas conhecidos de atualização e práticas recomendadas
 Para obter uma lista detalhada das edições e versões com suporte que você pode atualizar, consulte [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).

> [!TIP]
>  Para obter as informações mais recentes sobre problemas com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte o seguinte:
> 
>  -   [Notas de versão do SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).
> -   [SQL Server 2014 Reporting Services dicas, truques e solução de problemas](https://go.microsoft.com/fwlink/?LinkID=391254).
> -   Use o Supervisor de Atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Reporting Services problemas de atualização &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md) e [como instalar o supervisor de atualização](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_side_by_side"></a>Instalações lado a lado
 O modo nativo do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] pode ser instalado lado a lado com uma implantação de modo nativo do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

 Não há suporte para implantações lado a lado do modo do SharePoint do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] e nenhuma das versões anteriores de componentes do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_inplace_upgrade"></a>Atualização in-loco
 A atualização é concluída pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usada para atualizar qualquer ou todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inclusive o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A Instalação detecta as instâncias existentes e solicita que você faça a atualização. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação fornece opções de atualização que podem ser especificadas como um argumento de linha de comando ou no Assistente de Instalação.

 Quando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada, é possível selecionar a opção para atualizar de uma das seguintes versões ou instalar uma nova instância do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] que seja executada lado a lado com instalações existentes:

-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]

-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]

-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]

-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]

 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte o seguinte:

||
|-|
|[Atualizar para o SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)|
|[Atualize para o SQL Server 2014 usando o assistente de instalação &#40;a instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|
|[Install SQL Server 2014 from the Command Prompt](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)|

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_upgrade_checklist"></a>Lista de verificação de pré-atualização
 Antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], revise o seguinte:

-   Examine os requisitos para determinar se o hardware e o software do computador podem dar suporte ao [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. Para obter mais informações, consulte [Hardware and Software Requirements for Installing SQL Server 2014](../../../2014/sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

-   Use o Verificador de Configuração do Sistema (SCC) para saber se no computador do servidor de relatórios há condições que podem impedir uma instalação bem-sucedida do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).

-   Consulte as práticas recomendadas e a orientação de segurança para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Security Considerations for a SQL Server Installation](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md).

-   Execute o Supervisor de Atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador do servidor de relatório para identificar quaisquer problemas que possam impedir uma atualização bem-sucedida. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).

-   Faça backup da chave simétrica. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).

-   Faça backup dos bancos de dados do servidor de relatório e arquivos de configuração. Para obter mais informações, consulte [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md).

-   Faça backup de quaisquer personalizações feitas em diretórios virtuais existentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no IIS.

-   Remova certificados SSL inválidos.  Inclusive certificados expirados que você não planeja atualizar antes de atualizar o Reporting Services.  Certificados inválidos causarão falha na atualização, e uma mensagem de erro semelhante à seguinte será gravada no arquivo de Log do Reporting Services: **Microsoft.ReportingServices.WmiProvider.WMIProviderException: um certificado SSL (protocolo SSL) não está configurado no site**.

 Antes de atualizar um ambiente de produção, execute sempre uma atualização de teste em um ambiente de pré-produção que tenha a mesma configuração do ambiente de produção.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

## <a name="overview-of-migration-scenarios"></a>Visão geral de cenários de migração
 Se você estiver atualizando de uma versão com suporte do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], normalmente será possível executar o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atualizar os arquivos de programa, o banco de dados e todos os dados de aplicativo do servidor de relatório.

 No entanto, a **migração** manual de uma instalação do servidor de relatório será necessária se houver alguma das seguintes condições:

-   O Supervisor de Atualização detectou um ou mais bloqueadores de atualização. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).

-   Você quer alterar o tipo de servidor de relatório usado em sua implantação. Por exemplo, você não pode atualizar ou converter um servidor de relatório de modo nativo para um modo do SharePoint. Para obter mais informações, consulte [Migração do modo nativo para o SharePoint &#40;SSRS&#41;](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md).

-   Você quer minimizar a quantidade de tempo que o servidor de relatório fica offline durante o processo de atualização. Sua instalação atual permanecerá online enquanto você copiar dados de conteúdo para uma nova instância do servidor de relatório e testar a instalação sem alterar o estado da instalação existente do servidor de relatório.

-   Você deseja migrar uma implantação do SharePoint 2010 do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o SharePoint 2013. O SharePoint 2013 não oferece suporte à atualização no local a partir do SharePoint 2010. Para obter mais informações, veja [Migrar uma instalação do Reporting Services &#40;Modo do SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_native_scenarios"></a>Cenários de migração e atualização do modo nativo
 **Atualização:** A atualização in-loco para o modo nativo é o mesmo processo para cada uma das versões com suporte listadas anteriormente neste tópico. Execute o assistente de instalação do SQL Server ou uma instalação pela linha de comando. Após a instalação, o banco de dados do servidor de relatório será automaticamente atualizado para o novo esquema de banco de dados do servidor de relatório. Para obter mais informações, consulte a seção [atualização](#bkmk_inplace_upgrade) in-loco neste tópico.

 O processo de atualização começa quando você seleciona uma instância existente do servidor de relatório a ser atualizada.

1.  Se o banco de dados do servidor de relatório estiver em um computador remoto e você não tiver permissão para atualizar esse banco de dados, a Instalação solicitará que você forneça credenciais para fazer a atualização para um banco de dados do servidor de relatório remoto. Certifique-se de fornecer credenciais que tenham permissões `sysadmin` ou de atualização de banco de dados.

2.  A Instalação verifica se existem condições ou configurações que impedem a atualização e lê as definições de configuração. Os exemplos incluem extensões personalizadas implantadas no servidor de relatório. Se a atualização estiver bloqueada, será necessário modificar a instalação para que a atualização não seja mais bloqueada ou migrar para uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obter mais informações, consulte a documentação do Supervisor de Atualização.

3.  Se a atualização puder prosseguir, a Instalação solicitará que você continue o processo de atualização.

4.  A Instalação cria novas pastas para arquivos de programas do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. As pastas de programa para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] uma instalação incluem MSRS12. \< *nome da instância*>.

5.  A Instalação adiciona os arquivos de programas do servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , as ferramentas de configuração e os utilitários de linha de comando que fazem parte do recurso do servidor de relatório.

    1.  Os arquivos de programas da versão anterior são removidos.

    2.  Os utilitários e as ferramentas de configuração do servidor de relatório que são atualizados para a nova versão incluem a ferramenta Configuração do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os utilitários de linha de comando, por exemplo, RS.exe e o Construtor de Relatórios.

    3.  Outras ferramentas de cliente como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e Manuais Online não são atualizadas. Para obter versões novas das ferramentas, você pode adicioná-las quando executar a instalação. As versões anteriores coexistirão com versões do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Se você tiver instalado exemplos, a versão anterior permanecerá. A Instalação não oferece suporte à atualização dos exemplos do SQL Server.

    4.  
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] é um download separado. Para obter mais informações, consulte [Microsoft SQL Server 2014 Data Tools - Business Intelligence para Microsoft Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843).

6.  A instalação reutiliza a entrada do serviço Servidor de Relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no Gerenciador de Controle de Serviços. Essa entrada de serviço inclui a conta de serviço Servidor de Relatório do Windows.

7.  A Instalação reserva novas URLs com base nas configurações existentes do diretório virtual no IIS. A instalação pode não remover diretórios virtuais no IIS; portanto, remova-os manualmente depois que a atualização for concluída.

8.  A Instalação atualiza os bancos de dados do servidor de relatório para o novo esquema e modifica o `RSExecRole` adicionando permissões Proprietário do Banco de Dados à função. Esta etapa ocorre apenas quando você está atualizando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do antes do SP1.

9. A Instalação mescla configurações nos arquivos de configuração. Quando você utiliza como base os arquivos de configuração da versão atual, são adicionadas novas entradas. As entradas obsoletas não são removidas, mas não serão mais lidas pelo servidor de relatório depois que a atualização for concluída. A atualização não excluirá arquivos de log antigos, o arquivo RSWebApplication.config obsoleto ou as configurações de diretório virtual no IIS. A atualização não removerá o Designer de Relatórios do SQL Server 2005, o Management Studio ou outras ferramentas de cliente. Se você não mais precisar deles, certifique-se de remover esses arquivos e ferramentas depois que a atualização for concluída.

 **Migração:** A migração de uma versão anterior de uma instalação de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] modo nativo para o tem as mesmas etapas para todas as versões de s com suporte listadas anteriormente neste tópico. Para obter mais informações, veja [Migrar uma instalação do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_native_scaleout"></a>Atualizar uma implantação de expansão de Reporting Services modo nativo
 Veja a seguir um resumo de como atualizar uma implantação de modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é dimensionada para mais de um servidor de relatório. Esse processo requer o tempo de inatividade da implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :

1.  Faça backup dos bancos de dados do servidor de relatório e das chaves de criptografia. Para obter mais informações, consulte [Operações de backup e restauração do Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) e [Adicionar e remover chaves de criptografia para implantação escalável &#40; 	Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).

2.  Use o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e remova todos os servidores de relatório da implantação em expansão. Para obter mais informações, veja [Configurar uma implantação em expansão do servidor de relatório em modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).

3.  Atualize um dos servidores de relatório para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

4.  Use o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para adicionar os servidores de relatório de volta para a implantação em expansão. Para obter mais informações, veja [Configurar uma implantação em expansão do servidor de relatório em modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).

     Para cada servidor, repita as etapas de atualização e expansão.

##  <a name="bkmk_sharePoint_scenarios"></a>Cenários de atualização e migração do modo do SharePoint
 As seções a seguir descrevem os problemas e as etapas básicas necessárias para atualizar ou migrar de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] versões especificadas do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint para o modo do SharePoint.

 Há dois componentes de instalação para atualizar uma implantação do modo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint.

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Serviço compartilhado do SharePoint.

    > [!TIP]
    >  Use o cmdlet [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do `Get-SPRSServiceApplicationServers` SharePoint para determinar os servidores no farm do SharePoint que estão executando o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint e, portanto, requerem uma atualização.

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Suplemento para produtos do SharePoint. Para obter mais informações, consulte [instalar ou desinstalar o suplemento Reporting Services para sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).

 Para obter etapas detalhadas sobre como migrar uma instalação no modo do SharePoint, consulte [Migrar uma instalação do Reporting Services &#40;modo do SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).

> [!IMPORTANT]
>  Alguns dos cenários a seguir exigem tempo de inatividade do ambiente do SharePoint devido às tecnologias diferentes que precisam ser atualizadas. Se a sua situação não permitir tempo de inatividade, você precisará concluir uma migração em vez de uma atualização in-loco.

### <a name="sssql11-to-sssql14"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Para[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Ambiente inicial:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]., SharePoint 2010.

 **Ambiente final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010 ou SharePoint 2013.

-   **SharePoint 2010:** A atualização in-loco do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tem suporte, mas o cenário de atualização requer tempo de inatividade do ambiente do SharePoint.

     Se você deseja que o ambiente final execute o SharePoint 2013, precisará concluir uma atualização da anexação do banco de dados do SharePoint 2010 para o SharePoint 2013.

-   **SharePoint 2013:** O SharePoint 2013 não oferece suporte à atualização in-loco do SharePoint 2010. No entanto, há suporte para o procedimento de **atualização da anexação do banco de dados**  . O comportamento é diferente de atualizar para o SharePoint 2010, onde um cliente pode escolher entre as duas abordagens básicas de atualização, atualização in-loco e atualizações de anexação do banco de dados.

     Se você tiver uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada com o SharePoint 2010, não poderá atualizar o servidor do SharePoint in-loco. No entanto, você pode migrar bancos de dados de conteúdo e bancos de dados de aplicativo de serviço do farm do SharePoint 2010 para um farm do SharePoint 2013.

### <a name="sskilimanjaro-to-sssql14"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]Para[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Iniciando ambiente:** SQL Server 2008 R2, SharePoint 2010.

 **Ambiente final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010.

-   A atualização in-loco tem suporte e não há nenhum tempo de inatividade para seu ambiente do SharePoint.

-   Instale a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint em cada front-end da Web no farm. Você pode instalar o suplemento usando o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou baixando o suplemento.

-   Execute [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a instalação do para atualizar o modo do SharePoint para cada ' servidor de relatório '. O assistente de instalação do SQL Server instalará o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço e criará um novo aplicativo de serviço.

     Se você deseja que o ambiente final execute o SharePoint 2013, precisará concluir uma atualização da anexação do banco de dados do SharePoint 2010 para o SharePoint 2013.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

### <a name="sskatmai-sp2-to-sssql14"></a>
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Ambiente inicial:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2, SharePoint 2007.

 **Ambiente final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010.

-   Este cenário de atualização in-loco exige tempo de inatividade do ambiente do SharePoint porque ambas as tecnologias SharePoint e SQL Server precisam ser atualizadas. Você pode querer concluir uma migração em vez de fazer uma atualização in-loco.

-   Atualize primeiro o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para Service Pack 2 (SP2), se isso já não tiver sido concluído.

-   Atualize o SharePoint para 2010. Quando você executar o instalador de pré-requisito do SharePoint 2010, ele atualizará o suplemento do Reporting Services para os produtos do SharePoint 2010.

-   Instale a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint em todos os front-ends da Web do SharePoint. O instalador de pré-requisito do SharePoint instalou a versão do SQL Server 2008 R2 do suplemento, mas você precisa da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para trabalhar com um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .

-   > [!WARNING]
    >  Após a atualização do SharePoint, seu ambiente do Reporting Services estará em um estado de não funcionamento até que o SQL Server seja atualizado.

-   Atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando você executar o assistente de instalação do SQL Server, verá uma caixa de diálogo "**Autenticação do Modo SharePoint do SQL Server Reporting Services**". O serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será instalado e as credenciais da página de autenticação serão usadas para criar um novo pool de aplicativos do SharePoint.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

### <a name="sql-server-2005-sp2-to-sssql14"></a>SQL Server 2005 SP2 para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Iniciando ambiente:** SQL Server 2005 SP2, SharePoint 2007.

 **Ambiente final:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010.

-   Este cenário de atualização in-loco exige tempo de inatividade do ambiente do SharePoint porque ambas as tecnologias SharePoint e SQL Server precisam ser atualizadas. Você pode querer concluir uma migração em vez de fazer uma atualização in-loco.

-   Atualize primeiro o SQL Server 2005 para Service Pack 2 (SP2), se isso já não tiver sido concluído.

-   Atualize o SharePoint para SharePoint 2010. Quando você executar o instalador de pré-requisito do SharePoint 2010, ele atualizará o suplemento do Reporting Services para os produtos do SharePoint 2010.

-   > [!WARNING]
    >  Após a atualização do SharePoint, seu ambiente do Reporting Services estará em um estado de não funcionamento até que o SQL Server seja atualizado.

-   Instale a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint em todos os front-ends da Web do SharePoint. O instalador de pré-requisito do SharePoint instalou a versão do SQL Server 2008 R2 do suplemento, mas você precisa da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para trabalhar com um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .

-   Atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando você executar o assistente de instalação do SQL Server, verá uma caixa de diálogo "Autenticação do Modo SharePoint do SQL Server Reporting Services". O serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será instalado e as credenciais da página de autenticação serão usadas para criar um novo pool de aplicativos do SharePoint.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_migration_considerations"></a>Considerações para uma migração
 Ao mover dados de aplicativo, você deve estar atento às seguintes preocupações e restrições:

-   A proteção da chave de criptografia inclui um hash que incorpora a identidade da máquina.

-   Os nomes de banco de dados de servidor de relatório são fixos e não podem ser alterados em um novo computador.

### <a name="encryption-key-considerations"></a>Considerações sobre a chave de criptografia
 Sempre faça backup das chaves de criptografia antes de mover um banco de dados de servidor de relatório para um novo computador.

 A migração de uma instalação do servidor de relatório para outro computador invalidará o hash que protege as chaves de criptografia usadas para ajudar a proteger dados confidenciais armazenados no banco de dados do servidor de relatório. Cada instância do servidor de relatório que usa o banco de dados tem sua cópia da chave de criptografia, que é criptografada com a identidade da conta de serviço, conforme definida no computador atual. Se você mudar de computador, o serviço não terá mais acesso à sua chave, mesmo que o mesmo nome de conta seja usado no novo computador.

 Para restabelecer a criptografia reversível no novo computador do servidor de relatório, restaure a chave da qual fez backup anteriormente. O conjunto de chave completo que é armazenado no banco de dados do servidor de relatório consiste em um valor de chave simétrica e em informações sobre a identidade de serviço usada para restringir o acesso à chave, para que ela possa ser usada somente pela instância do servidor de relatório em que foi armazenada. Durante a restauração da chave, o servidor de relatório substitui as cópias existentes da chave pelas novas versões. A nova versão inclui os valores de identidade da máquina e de serviço, conforme definido no computador atual. Para obter mais informações, consulte estes tópicos:

-   Modo do SharePoint: confira a seção “Gerenciamento de chaves” de [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)

-   Modo Nativo: veja [Fazer backup e restaurar as chaves de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

### <a name="fixed-database-name"></a>Nome fixo do banco de dados
 Você não pode renomear o banco de dados de servidor de relatório. A identidade do banco de dados é registrada em procedimentos armazenados do servidor de relatório quando o banco de dados é criado. A renomeação dos bancos de dados primário ou temporário do servidor de relatório provoca erros que ocorrem quando os procedimentos são executados, invalidando a instalação do servidor de relatório.

 Se o nome do banco de dados da instalação existente não for adequado para a nova instalação, avalie a possibilidade de criar um novo banco de dados com o nome desejado e, em seguida, carregue os dados de aplicativo existentes usando as técnicas descritas na seguinte lista:

-   Grave um script do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que chame métodos SOAP do serviço Web Servidor de Relatórios para copiar dados entre bancos de dados. Use o utilitário RS.exe para executar o script. Para obter mais informações sobre essa abordagem, veja [Script e PowerShell com o Reporting Services](../tools/scripting-and-powershell-with-reporting-services.md).

-   Grave o código que chama o provedor WMI para copiar dados entre bancos de dados. Para obter mais informações sobre essa abordagem, veja [Acessar o provedor WMI do Reporting Services](../tools/access-the-reporting-services-wmi-provider.md).

-   Se houver poucos itens, você poderá republicar relatórios, modelos de relatório e fontes de dados compartilhadas do Designer de Relatórios, do Designer de Modelo e do Construtor de Relatórios no novo servidor de relatório. Você deve recriar atribuições de função, assinaturas, agendas compartilhadas, agendas de instantâneo de relatório, propriedades personalizadas definidas em relatórios ou outros itens, segurança de item de modelo e propriedades definidas no servidor de relatório. Você perderá os dados do histórico de relatório e do log de execução de relatório.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

##  <a name="bkmk_additional_resources"></a>Recursos adicionais

> [!NOTE]
>  Para obter mais informações sobre a atualização da anexação do banco de dados do SharePoint, consulte o seguinte:

-   [Visão geral do processo de atualização para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688).

-   [Limpar preparações antes de uma atualização para o SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689).

-   [Atualize os bancos de dados do sharepoint 2010 para o sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste tópico:](#bkmk_top)

## <a name="see-also"></a>Consulte Também
 Os [relatórios de atualização](../../reporting-services/install-windows/upgrade-reports.md) são [atualizados para o SQL Server 2014 usando o assistente de instalação &#40;a instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)


