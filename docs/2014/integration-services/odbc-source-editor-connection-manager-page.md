---
title: Editor de origem ODBC (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.odbcsource.connection.f1
ms.assetid: e2c8dc83-6394-4d6c-9232-97e94be72431
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3092f4ad0b59797bfcc64299eaa23fbd3459448c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121093"
---
# <a name="odbc-source-editor-connection-manager-page"></a>Editor de Origem ODBC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ODBC** para selecionar o gerenciador de conexões ODBC para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 Para obter mais informações sobre essa fonte ODBC, consulte [Fonte ODBC](data-flow/odbc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página do Gerenciador de Conexões do Editor de Origem ODBC**  
  
-   No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
## <a name="options"></a>Opções  
  
### <a name="connection-manager"></a>Gerenciador de conexões  
 Selecione na lista um gerenciador de conexões ODBC existente ou clique em **Novo** para criar uma nova conexão. A conexão pode ser com qualquer banco de dados com suporte ODBC.  
  
### <a name="new"></a>Nova  
 Clique em **Nova**. É aberta a caixa de diálogo **Configurar Editor do Gerenciador de Conexões ODBC** , na qual você pode criar um novo gerenciador de conexões ODBC.  
  
### <a name="data-access-mode"></a>Modo de acesso a dados  
 Especifique o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:  
  
|Opção|Description|  
|------------|-----------------|  
|Nome da tabela|Recupere os dados de uma tabela ou exibição na fonte de dados ODBC. Quando você selecionar esta opção, selecione um valor na lista para o seguinte:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível na lista ou digite uma expressão regular para identificar a tabela.|  
||Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.|  
|Comando SQL|Recupere os dados da fonte de dados ODBC usando uma consulta SQL. Você deve escrever a consulta na sintaxe do banco de dados de origem com o qual está trabalhando. Quando selecionar esta opção, insira uma consulta de uma das seguintes maneiras:|  
||Insira o texto da consulta SQL no campo **Texto do comando do SQL** .|  
||Clique em **Procurar** para carregar a consulta SQL de um arquivo de texto.|  
||Clique em **Analisar consulta** para verificar a sintaxe do texto da consulta.|  
  
### <a name="preview"></a>Visualização  
 Clique em **Visualizar** para exibir até as primeiras 200 linhas dos dados extraídos da tabela ou exibição selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades personalizadas da origem ODBC](data-flow/odbc-source-custom-properties.md)   
 [Editor de Origem ODBC &#40;Página Colunas&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)   
 [Editor de origem ODBC &#40;página de saída de erro&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  