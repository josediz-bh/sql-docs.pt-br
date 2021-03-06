---
title: Dá suporte ao método | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cce5ab3b735d3c641da4a6234e860d0528f107c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936700"
---
# <a name="supports-method"></a>Método Supports
Determina se um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) especificado dá suporte a um tipo específico de funcionalidade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor **booliano** que indica se todos os recursos identificados pelo argumento *CursorOptions* têm suporte do provedor.  
  
#### <a name="parameters"></a>parâmetros  
 *CursorOptions*  
 Uma expressão **longa** que consiste em um ou mais valores [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use o método de **suporte** para determinar os tipos de funcionalidade aos quais um objeto **Recordset** dá suporte. Se o objeto **Recordset** der suporte aos recursos cujas constantes correspondentes estão em *CursorOptions*, o método de **suporte** retornará **true**. Caso contrário, retornará **false**.  
  
> [!NOTE]
>  Embora o método de **suporte** possa retornar **true** para uma determinada funcionalidade, ele não garante que o provedor possa disponibilizar o recurso em todas as circunstâncias. O método de **suporte** simplesmente retorna se o provedor pode dar suporte à funcionalidade especificada, supondo que determinadas condições sejam atendidas. Por exemplo, o método de **suporte** pode indicar que um objeto **Recordset** dá suporte a atualizações, embora o cursor seja baseado em uma junção com várias tabelas, algumas colunas que não são atualizáveis.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método de suporte (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Exemplo do método de suporte (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Propriedade CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
