---
title: Editor do Gerenciador de Conexão de HTTP (página servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9c298c6bb6427b42f0302350919081e2c3e5bc08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008947"
---
# <a name="http-connection-manager-editor-server-page"></a>Editor do Gerenciador de Conexões HTTP (página Servidor)
  Use a guia **Servidor** da caixa de diálogo **Editor do Gerenciador de Conexões de HTTP** para configurar o Gerenciador de Conexões de HTTP especificando propriedades como URL e credenciais de segurança. Uma conexão HTTP permite que um pacote acesse um servidor Web usando o HTTP para enviar ou receber arquivos. Depois de configurar o Gerenciador de Conexões de HTTP, você também pode testar a conexão.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Para obter mais informações sobre o gerenciador de conexões de HTTP, consulte [HTTP Connection Manager](connection-manager/http-connection-manager.md). Para saber mais sobre um cenário de utilização geral para o Gerenciador de Conexões de HTTP, consulte [Web Service Task](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opções  
 **Servidor URL**  
 Digite o URL do servidor.  
  
 Para usar o botão **Baixar WSDL** na página **Geral** do **Editor da Tarefa Serviço da Web** para baixar um arquivo WSDL, digite a URL do arquivo WSDL. Essa URL termina com "?wsdl".  
  
 **Usar credenciais**  
 Especifique se você o Gerenciador de Conexões de HTTP deve usar as credenciais de segurança do usuário para autenticação.  
  
 **Nome de usuário**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Senha**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Domínio**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Usar certificado do cliente**  
 Especifique se o Gerenciador de Conexões de HTTP deve usar um certificado do cliente para autenticação.  
  
 **Certificado**  
 Selecione um certificado na lista usando a caixa de diálogo **Selecionar Certificado** . A caixa de texto exibe o nome associado a este certificado.  
  
 **Tempo limite (em segundos)**  
 Forneça um tempo limite para conexão com o servidor Web. O valor padrão desta propriedade é 30 segundos.  
  
 **Tamanho da parte (em KB)**  
 Forneça um tamanho da parte para gravar dados.  
  
 **Testar Conexão**  
 Depois de configurar o Gerenciador de Conexões de HTTP, confirme se a conexão é viável clicando em **Testar Conexão**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexão HTTP &#40;página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  