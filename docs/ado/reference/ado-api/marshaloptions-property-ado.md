---
title: Propriedade marshaloptions (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0212f3b4cb663bd56adaa1bdbc3ab6675c3ce888
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932279"
---
# <a name="marshaloptions-property-ado"></a>Propriedade MarshalOptions (ADO)
Indica quais registros do [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) devem ser empacotados de volta para o servidor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) . O valor padrão é **adMarshalAll**.  
  
## <a name="remarks"></a>Comentários  
 Ao usar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)do lado do cliente, os registros que foram modificados no cliente são gravados novamente na camada intermediária ou no servidor Web por meio de uma técnica chamada marshaling, do processo de empacotamento e envio de parâmetros de método de interface entre limites de thread ou processo. A definição da propriedade **marshaloptions** pode melhorar o desempenho quando dados remotos modificados são empacotados para atualização de volta para a camada intermediária ou servidor Web.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Essa propriedade é usada somente em um **conjunto de registros**do lado do cliente.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade marshaloptions (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [Exemplo da propriedade MarshalOptions (VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
