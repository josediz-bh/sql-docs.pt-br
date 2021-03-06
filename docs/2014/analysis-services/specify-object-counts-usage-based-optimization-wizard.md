---
title: Especificar contagens de objetos (Assistente de otimização com base no uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0503192c3c948110f8301c8eb375e1c8203e42f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068241"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>Especificar Contagens de Objetos (Assistente de Otimização com Base no Uso)
  Use a página **Especificar Contagens de Objetos** para calcular a contagem de objetos no cubo automaticamente ou para inserir contagens estimadas manualmente. O Assistente de Otimização com Base no Uso usa a contagem de objetos para estimar requisitos de armazenamento.  
  
## <a name="options"></a>Opções  
 **Objetos de Cubo**  
 Exibe as dimensões e os atributos do cubo. Somente os atributos que não têm sua `AggregationUsage` propriedade definida como nenhum na página **revisar uso de agregação** do assistente são mostrados porque esses são os únicos atributos que precisam de contagens especificadas.  
  
 **Contagem estimada**  
 Exibe o número estimado de linhas no grupo de medidas e as contagens de membros de atributo estimadas nas dimensões do banco de dados. Você pode digitar um valor a ser usado como a contagem estimada ou calcular os valores da contagem estimada. Para calcular os valores da contagem, digite 0 no campo e clique em **Contagem**. Os campos que já exibem uma contagem não são atualizados.  
  
 **Contagem de partições**  
 (Opcional) Digite o número estimado de linhas no grupo de medidas e as contagens de membros de atributo estimadas nas partições.  
  
 **Contar**  
 Calcula e popula novamente os valores na coluna **Contagem estimada** para todos os campos vazios. Os campos que já exibem uma contagem não são atualizados.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de design de agregação](aggregation-design-wizard-f1-help.md)   
 [Analysis Services assistentes &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
