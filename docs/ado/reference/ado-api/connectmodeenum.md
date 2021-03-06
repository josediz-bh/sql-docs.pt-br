---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: debf6f9dc4ac1326caf9fbf32b65f15f34a19094
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933453"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica as permissões disponíveis para modificar dados em uma [conexão](../../../ado/reference/ado-api/connection-object-ado.md), abrir um [registro](../../../ado/reference/ado-api/record-object-ado.md)ou especificar valores para a propriedade [Mode](../../../ado/reference/ado-api/mode-property-ado.md) dos objetos **Record** e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica permissões somente leitura.|  
|**adModeReadWrite**|3|Indica permissões de leitura/gravação.|  
|**adModeRecursive**|0x400000|Usado em conjunto com os outros * \*valores\* de ShareDeny* (**adModeShareDenyNone**, **adModeShareDenyWrite**ou **adModeShareDenyRead**) para propagar as restrições de compartilhamento para todos os subregistros do **registro**atual. Ele não afeta se o **registro** não tiver nenhum filho. Um erro de tempo de execução será gerado se for usado somente com **adModeShareDenyNone** . No entanto, ele pode ser usado com **adModeShareDenyNone** quando combinado com outros valores. Por exemplo, você pode usar "**adModeRead** ou **adModeShareDenyNone** ou **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite que outras pessoas abram uma conexão com qualquer permissão. O acesso à leitura/gravação não pode ser negado a outras pessoas.|  
|**adModeShareDenyRead**|4|Impede que outras pessoas abram uma conexão com permissões de leitura.|  
|**adModeShareDenyWrite**|8|Impede que outras pessoas abram uma conexão com permissões de gravação.|  
|**adModeShareExclusive**|12|Impede que outras pessoas abram uma conexão.|  
|**adModeUnknown**|0|Padrão. Indica que as permissões ainda não foram definidas ou não podem ser determinadas.|  
|**adModeWrite**|2|Indica permissões somente gravação.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectMode. READ|  
|AdoEnums. ConnectMode. READWRITE|  
|(Não há equivalente a AdoEnums. ConnectMode. recursivo)|  
|AdoEnums. ConnectMode. SHAREDENYNONE|  
|AdoEnums. ConnectMode. SHAREDENYREAD|  
|AdoEnums. ConnectMode. SHAREDENYWRITE|  
|AdoEnums. ConnectMode. SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode. desconhecido|  
|AdoEnums. ConnectMode. WRITE|  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Propriedade Mode (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Método Open (Registro do ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
