---
title: MSSQLSERVER_30089 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 981d0079cb6b0ce8cf423bf44e382cca119ed477
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68001943"
---
# <a name="mssqlserver_30089"></a>MSSQLSERVER_30089
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|30089|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|IFTS_FDHOST_TERMINATEDABNORMAL|  
|Texto da mensagem|O processo FDHost (host do daemon de filtro de texto completo) foi interrompido de maneira anormal. Isso poderá ocorrer se um componente linguístico configurado incorretamente ou que não está funcionando bem, como um separador de palavras, lematizador ou filtro, gerou um erro irrecuperável durante a indexação de texto completo ou no processamento de uma consulta. O processo será reiniciado automaticamente.|  
  
## <a name="explanation"></a>Explicação  
O host do daemon de filtro de texto completo encontrou um problema que forçou seu encerramento de maneira anormal. A causa do problema pode ser um documento malformatado, um bug no filtro ou no separador de palavras ou um problema no daemon de filtro.  
  
## <a name="user-action"></a>Ação do usuário  
Normalmente, o daemon se recupera do erro. Se ele apresentar falhas constantes, será necessário diagnosticar e solucionar o problema. Tente fazer o seguinte para isolar o problema:  
  
1.  Se um novo componente linguístico foi instalado recentemente, remova-o do sistema.  
  
2.  Consulte o log de rastreamento para identificar qualquer documento novo cuja indexação de texto completo tenha falhado e remova esse documento.  
  
## <a name="see-also"></a>Consulte Também  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[Configurar e gerenciar filtros de pesquisa](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
