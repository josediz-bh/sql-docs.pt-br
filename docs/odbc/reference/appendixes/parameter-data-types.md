---
title: Tipos de dados de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: 5140c69184332b1760859421b7e802a5163a0f09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100601"
---
# <a name="parameter-data-types"></a>Tipos de dados do parâmetro
Embora cada parâmetro especificado com **SQLBindParameter** seja definido usando um tipo de dados SQL, os parâmetros em uma instrução SQL não têm nenhum tipo de dados intrínseco. Portanto, os marcadores de parâmetro podem ser incluídos em uma instrução SQL somente se seus tipos de dados puderem ser inferidos de outro operando na instrução. Por exemplo, em uma expressão aritmética, como? + COLUNA1, o tipo de dados do parâmetro pode ser inferido do tipo de dados da coluna nomeada representada pela COLUNA1. Um aplicativo não poderá usar um marcador de parâmetro se o tipo de dados não puder ser determinado.  
  
 A tabela a seguir descreve como um tipo de dados é determinado para vários tipos de parâmetros, de acordo com o SQL-92. Para obter uma especificação mais abrangente sobre como inferir o tipo de parâmetro quando outras cláusulas SQL são usadas, consulte a especificação do SQL-92.  
  
|Local do parâmetro|Tipo de dados assumido|  
|---------------------------|-----------------------|  
|Um operando de um operador aritmético ou de comparação binária|O mesmo que o outro operando|  
|O primeiro operando em uma cláusula **between**|O mesmo que o segundo operando|  
|O segundo ou terceiro operando em uma cláusula **between**|Mesmo que o primeiro operando|  
|Uma expressão usada com **no**|O mesmo que o primeiro valor ou a coluna de resultado da subconsulta|  
|Um valor usado com **no**|O mesmo que a expressão ou o primeiro valor se houver um marcador de parâmetro na expressão|  
|Um valor de padrão usado com **like**|VARCHAR|  
|Um valor de atualização usado com **Update**|O mesmo que a coluna de atualização|
