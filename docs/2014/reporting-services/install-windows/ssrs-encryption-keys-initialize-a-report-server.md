---
title: Inicializar um servidor de relatório (Gerenciador de Configurações do SSRS) | Microsoft Docs
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
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 70953e800019fd91afde599daa060abf3beda581
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119054"
---
# <a name="initialize-a-report-server-ssrs-configuration-manager"></a>Inicializar um servidor de relatório (Gerenciador de configurações do SSRS)
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], um servidor inicializado é aquele que pode criptografar e descriptografar dados em um banco de dados de servidor de relatório. A inicialização é um requisito para a operação do servidor de relatório. A inicialização ocorre quando o serviço Servidor de Relatório é iniciado pela primeira vez. Também ocorre quando você associa o servidor de relatório à implantação existente ou quando recria manualmente as chaves como parte do processo de recuperação. Para obter mais informações sobre como e por que as chaves de criptografia são usadas, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md) e [Armazenar dados criptografados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md).  
  
 Em parte, as chaves de criptografia têm como base as informações de perfil do serviço Servidor de Relatório. Se você alterar a identidade de usuário usada para executar o serviço Servidor de Relatório, deverá atualizar as chaves adequadamente. Se você estiver usando a ferramenta Configuração do Reporting Services para alterar a identidade, essa etapa será tratada para você automaticamente.  
  
 Se a inicialização falhar por algum motivo, o servidor de relatório retornará um `RSReportServerNotActivated` erro em resposta a solicitações do usuário e serviço. Nesse caso, poderá ser necessário solucionar o problema da configuração do sistema ou do servidor. Para saber mais, veja a [SSRS: solução de problemas e erros com o Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/1633.aspx)no TechNet Wiki.  
  
## <a name="overview-of-the-initialization-process"></a>Visão geral do processo de inicialização  
 O processo de inicialização cria e armazena uma chave simétrica usada para criptografia. A chave simétrica é criada pelos Serviços de Criptografia do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e subsequentemente usada pelo serviço Servidor de Relatório para criptografar e descriptografar dados. A própria chave simétrica é criptografada com uma chave assimétrica.  
  
 As seguintes etapas descrevem o processo de inicialização:  
  
1.  Na inicialização inicial, o serviço Servidor de Relatório lê o arquivo RSReportServer.config para obter o identificador da instalação e as informações de conexão com o banco de dados.  
  
2.  O serviço Servidor de Relatório solicita uma chave pública aos Serviços de Criptografia. O Windows cria uma chave privada e uma pública e envia a chave pública ao serviço Servidor de Relatório.  
  
3.  O serviço Servidor de Relatório conecta-se ao banco de dados do servidor de relatório e armazena os valores do identificador de instalação e da chave pública.  
  
4.  O serviço Servidor de Relatório chama novamente os Serviços de Criptografia, desta vez para solicitar uma chave simétrica. O Windows cria a chave simétrica.  
  
5.  O serviço Servidor de Relatório conecta-se novamente ao banco de dados do servidor de relatório e adiciona a chave simétrica aos valores do identificador de instalação e da chave pública que foram armazenados na etapa 3. Antes de armazená-la, o serviço Servidor de Relatório usa sua chave pública para criptografar a chave simétrica. Quando a chave simétrica for armazenada, o servidor de relatório será considerado inicializado e disponível para uso.  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>Inicializando um servidor de relatório para implantação de expansão  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte a um modelo de implantação de expansão que compartilha um único banco de dados de servidor de relatório entre várias instâncias do servidor de relatório. Para associar-se a uma implantação de expansão, um servidor de relatório deve criar e armazenar sua cópia da chave simétrica no banco de dados compartilhado. Embora uma única chave simétrica seja usada pelos servidores que usam o banco de dados, cada servidor de relatório tem sua cópia da chave. Cada cópia varia no fato de que ela é criptografada exclusivamente usando a chave pública de seu proprietário.  
  
 O primeiro conjunto de etapas para a inicialização de um servidor de relatório para implantação de expansão é idêntico às três primeiras etapas que descrevem a inicialização para uma combinação de servidor único e banco de dados.  
  
 O processo de inicialização para uma implantação de expansão difere em como o servidor de relatório obtém a chave simétrica. Quando o primeiro servidor é inicializado, obtém a chave simétrica do Windows. Quando o segundo servidor é inicializado durante a configuração para implantação de expansão, ele obtém a chave simétrica do serviço Servidor de Relatório que já está inicializado. A primeira instância do servidor de relatório usa a chave pública da segunda instância para criar uma cópia criptografada da chave simétrica para a segunda instância do servidor de relatório. A chave simétrica nunca é exposta como texto sem-formatação em qualquer ponto nesse processo.  
  
## <a name="how-to-initialize-a-report-server"></a>Como inicializar um servidor de relatório  
  
-   Para inicializar um servidor de relatório, use a ferramenta Configuração do Reporting Services. A inicialização ocorre automaticamente quando você cria e configura o banco de dados do servidor de relatório. Para obter mais informações, consulte [Configure a Report Server Database Connection  &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Para inicializar um servidor de relatório para implantação de expansão, você pode usar a página Inicialização da ferramenta Configuração do Reporting Services ou o utilitário **RSKeymgmt**. Para seguir instruções passo a passo, consulte [Configurar uma implantação escalável do servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](configure-a-native-mode-report-server-scale-out-deployment.md).  
  
> [!NOTE]  
>  **RSKeymgmt** é um aplicativo de console executado em uma linha de comando em um computador que hospeda uma instância do servidor de relatório que já faz parte de uma implantação escalável. Ao executar o utilitário, você especifica argumentos para selecionar uma instância do servidor de relatório que deseja inicializar.  
  
 Um servidor de relatório será inicializado apenas se houver uma correspondência entre o identificador da instalação e a chave pública. Se a correspondência obtiver êxito, será criada uma chave simétrica que permite criptografia reversível. Se a correspondência falhar, o servidor de relatório será desabilitado, caso no qual poderá ser necessário aplicar uma chave de backup ou excluir os dados criptografados se uma chave de backup não estiver disponível ou não for válida. Para obter mais informações sobre as chaves de criptografia usadas por um servidor de relatório, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md).  
  
> [!NOTE]  
>  Você também pode usar o provedor WMI (Instrumentação de Gerenciamento do Windows) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para inicializar um servidor de relatório de forma programática. Para obter mais informações, consulte [acessar o provedor de WMI do Reporting Services](../tools/access-the-reporting-services-wmi-provider.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>Como confirmar a inicialização de um servidor de relatório  
 Para confirmar a inicialização do servidor de relatório, execute ping no serviço Web Servidor de Relatórios digitando **http://\<servername>/reportserver** na janela de comando. Se ocorrer o erro `RSReportServerNotActivated`, a inicialização falhou.  
  
## <a name="see-also"></a>Consulte também  
 [Armazenar dados de servidor de relatório criptografados &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  