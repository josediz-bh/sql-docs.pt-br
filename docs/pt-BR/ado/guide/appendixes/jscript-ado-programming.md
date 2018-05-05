---
title: Programação de ADO JScript | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38b1f948d81aeba279c002dcd23988668bab41f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="jscript-ado-programming"></a>Programação de ADO do JScript
## <a name="creating-an-ado-project"></a>Criando um projeto de ADO  
 Microsoft JScript não oferece suporte a bibliotecas de tipo, portanto não é necessário para a referência ADO em seu projeto. Consequentemente, não há recursos associados como conclusão de linha de comando têm suporte. Além disso, por padrão, constantes enumerado do ADO não são definidos no JScript.  
  
 No entanto, o ADO fornece que incluir com dois arquivos que contém as definições a seguir para ser usado com JScript:  
  
-   Para uso em scripts do lado do servidor Adojavas.inc, que é instalado nas pastas de biblioteca do ADO.  
  
-   Para uso em scripts do lado do cliente Adcjavas.inc, que é instalado nas pastas de biblioteca do ADO.  
  
 Você pode copiar e colar definições de constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo scripts de servidor, copie o arquivo de Adojavas.inc para uma pasta no seu site da Web e faz referência a ele na página ASP como este:  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Criando objetos ADO em JScript  
 Você deve usar o **CreateObject** chamada de função:  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Exemplo de JScript  
 O código a seguir é um exemplo genérico da programação do lado do servidor JScript em um arquivo de Active Server Page (ASP) que abre uma **registros** objeto:  
  
```  
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```