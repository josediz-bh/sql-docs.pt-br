---
title: Consultas FOR XML AUTO retornam referências de tabela derivadas nos modos de compatibilidade 90 ou posteriores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- FOR XML AUTO [SQL Server]
ms.assetid: 10c32f06-f7e1-40e0-8f79-6d921f2bef1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b42d8fd7694aaa3962d049cb0e9663479778958
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095187"
---
# <a name="for-xml-auto-queries-return-derived-table-references-in-90-or-later-compatibility-modes"></a>Consultas FOR XML AUTO retornam referências de tabela derivada no modo de compatibilidade 90 ou posterior
  Quando o nível de compatibilidade do banco de dados está definido como 90 ou posterior, as consultas FOR XML que executam no modo AUTO retornam referências para aliases de tabela derivada. Quando o nível de compatibilidade está definido como 80, as consultas FOR XML AUTO retornam referências para as tabelas base que definem uma tabela derivada.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
 Por exemplo, considere a seguinte tabela:  
  
```  
CREATE TABLE Test(id int);  
INSERT INTO Test VALUES(1);  
INSERT INTO Test VALUES(2);  
```  
  
 A consulta a seguir, que inclui uma tabela derivada, produz resultados diferentes no nível de compatibilidade 80, 90 ou posterior:  
  
```  
SELECT * FROM   
   (SELECT a.id AS a, b.id AS b   
    FROM Test a JOIN Test b ON a.id=b.id)  
AS DerivedTest   
FOR XML AUTO;  
```  
  
 No nível de compatibilidade 80, a consulta retorna os seguintes resultados: Os resultados referenciam os aliases de tabela base `a` e `b` da tabela derivada em vez do alias de tabela derivada.  
  
```  
<a a="1"><b b="1"/></a><a a="2"><b b="2"/></a>  
```  
  
 No nível de compatibilidade 90 ou posterior, a consulta retorna referências para o alias de tabela derivada `DerivedTest` em vez de retornar para as tabelas base da tabela derivada.  
  
```  
<DerivedTest a="1" b="1"/><DerivedTest a="2" b="2"/>  
```  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seu aplicativo conforme necessário para adequar os resultados de consultas FOR XML AUTO que incluam tabelas derivadas e que executem no nível de compatibilidade 90 ou posterior.   
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
