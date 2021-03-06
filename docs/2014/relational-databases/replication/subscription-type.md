---
title: Tipo de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d936c1a1086f13d43bc38758f86a0ab80f757f7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63249376"
---
# <a name="subscription-type"></a>Tipo de Assinatura
  A replicação de mesclagem oferece dois tipos de assinatura: servidor e cliente (referenciado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em versões anteriores do como global e local, respectivamente). Os Assinantes com uma assinatura de servidor podem:  
  
-   Republicar dados para outros Assinantes.  
  
-   Servir como parceiros de sincronização alternativos.  
  
-   Resolver conflitos de acordo com uma prioridade definida.  
  
 A maioria dos Assinantes não requer essa funcionalidade e usa uma assinatura de cliente. Assinaturas de cliente ainda permitem detecção e resolução de conflitos, mas não é atribuída uma prioridade aos Assinantes: o primeiro Assinante a enviar uma alteração ao Publicador ganha todos os conflitos que possam surgir daquela alteração.  
  
> [!NOTE]  
>  O tipo da assinatura não pode ser alterado depois que ela é criada.  
  
## <a name="options"></a>Opções  
 **Propriedades da assinatura**  
 Para cada Assinante, selecione **Cliente** ou **Servidor** na caixa de listagem suspensa na coluna **Tipo de Assinatura** . Para Assinantes com assinaturas de servidor, insira um número entre 0 e 99.99 na coluna **Prioridade para a Resolução de Conflitos** (quanto mais alto for o número, mais alta será a prioridade para o Assinante).  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
