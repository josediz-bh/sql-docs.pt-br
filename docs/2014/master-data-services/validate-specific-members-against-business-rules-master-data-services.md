---
title: Validar membros específicos em relação a regras de negócio (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9aeceb89eb5a0b2dfb9fc57fecb0b055f8fc6292
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116402"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Validar membros específicos em relação a regras de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], aplique regras de negócio seletivamente quando desejar atualizar ou validar subconjuntos de membros com base em regras de negócio.  
  
> [!NOTE]  
>  Se você deseja aplicar regras de negócio a todos os membros em uma versão de um modelo, consulte [Validate a Version against Business Rules &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão **Atualizar** para o objeto de modelo ao qual está aplicando regras de negócio.  
  
### <a name="to-apply-business-rules-selectively"></a>Para aplicar regras de negócio seletivamente.  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **Entidades** e clique no nome da entidade que contém os membros aos quais você deseja aplicar regras.  
  
5.  Clique em **Aplicar regras de negócio**. As regras de negócio são aplicadas apenas aos membros exibidos na grade.  
  
## <a name="see-also"></a>Consulte também  
 [Validar uma versão em relação a regras de negócios &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  