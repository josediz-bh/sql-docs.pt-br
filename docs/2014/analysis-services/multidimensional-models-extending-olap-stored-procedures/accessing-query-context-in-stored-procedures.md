---
title: Acessando o contexto de consulta em procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93624a612126e9103144b8b53272122e66202b8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702665"
---
# <a name="accessing-query-context-in-stored-procedures"></a>Acessando o contexto de consulta nos procedimentos armazenados
  O contexto de execução de um procedimento armazenado está disponível no código do procedimento armazenado como um objeto do `Context` do modelo de objeto de servidor do ADOMD.NET. Trata-se de um contexto somente leitura e que não pode ser modificado pelo procedimento armazenado. As propriedades a seguir estão disponíveis nesse objeto.  
  
|Propriedade|Type|DESCRIÇÃO|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|O cubo do contexto de consulta atual.|  
|**CurrentDatabaseName**|String|O identificador do banco de dados atual.|  
|**CurrentConnection**|Conexão|Uma referência ao objeto de conexão no contexto atual.|  
|**Passá**|Integer|O número da passagem do contexto atual.|  
  
 Haverá um objeto `Context` quando o modelo de objeto de expressão MDX for usado em um procedimento armazenado. Ele não estará disponível quando o modelo de objeto MDX for usado em um cliente. O objeto `Context` não é passado explicitamente para o procedimento armazenado nem retornado por ele. Ele fica disponível durante a execução do procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de assemblies de modelo multidimensional](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
