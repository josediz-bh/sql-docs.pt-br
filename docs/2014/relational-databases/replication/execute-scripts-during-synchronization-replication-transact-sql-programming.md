---
title: Executar scripts durante a sincronização (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0be050105f1c848201ea2b0cc3780234594c3ae6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120990"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Executar scripts durante a sincronização (Programação Transact-SQL de replicação)
  A replicação dá suporte à execução de scripts sob demanda para Assinantes para publicações transacionais e de mesclagem. Essa funcionalidade copia o script no diretório que executa a replicação e usa **sqlcmd** para aplicar o script no Assinante. Por padrão, se houver uma falha ao aplicar o script para uma assinatura em uma publicação transacional, o Agente de Distribuição se deterá. Você pode especificar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] para ser executado programaticamente usando procedimentos armazenados de replicação.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Para especificar um script para ser executado para todos os Assinantes para uma publicação de instantâneo, transacional ou de mesclagem  
  
1.  Componha e teste o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que será executado sob demanda.  
  
2.  Salve o arquivo de script em um local em que possa ser acessado pelo Snapshot Agent para a publicação.  
  
3.  No Publicador no banco de dados de publicação, execute [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql). Especifique **@publication**, o nome do arquivo do script com caminho UNC completo criado na etapa 2 para **@scriptfile**e um dos seguintes valores para **@skiperror**:  
  
    -   **0** - o agente deixará de executar o script se um erro for encontrado.  
  
    -   **1** - o agente fará log dos erros e continuará executando o script quando forem encontrados erros.  
  
4.  O script especificado será executado para cada Assinante na próxima vez que o agente for executado para sincronizar a assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Sincronizar dados](synchronize-data.md)  
  
  