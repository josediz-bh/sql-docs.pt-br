---
title: Tratamento de erros no VBScript | Microsoft Docs
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
- VB
helpviewer_keywords:
- VBScript error handling [ADO]
- errors [ADO], VBScript
ms.assetid: 31bc3743-32d3-4bc7-ac61-ee6ed0fdec70
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e826c41916dfda8e1339112f646cca5c4d2b171a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors-in-vbscript"></a>Tratamento de erros no VBScript
Há pouca diferença entre os métodos usados no Visual Basic e os usados com o VBScript. A principal diferença é que o VBScript não suportam o conceito de continuar a execução em um rótulo de tratamento de erros. Em outras palavras, você não pode usar `On Error GoTo` no VBScript. Em vez disso, use `On Error Resume Next` e, em seguida, verifique se ambos **Err. Number** e **contagem** propriedade o **erros** coleção, conforme mostrado no exemplo a seguir:  
  
```  
<!-- BeginErrorExampleVBS -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE>Error Handling Example (VBScript)</TITLE>  
</HEAD>  
<BODY>  
  
<h1>Error Handling Example (VBScript)</h1>  
  
<%  
  
   Dim cnn1  
   Dim errLoop  
   Dim strError  
  
   On Error Resume Next  
  
   ' Intentionally trigger an error.  
   Set cnn1 = Server.CreateObject("ADODB.Connection")  
   cnn1.Open "nothing"  
  
   If cnn1.Errors.Count > 0 Then  
      ' Enumerate Errors collection and display  
      ' properties of each Error object.  
      For Each errLoop In cnn1.Errors  
         strError = "Error #" & errLoop.Number & "<br>" & _  
            "   " & errLoop.Description & "<br>" & _  
            "   (Source: " & errLoop.Source & ")" & "<br>" & _  
            "   (SQL State: " & errLoop.SQLState & ")" & "<br>" & _  
            "   (NativeError: " & errLoop.NativeError & ")" & "<br>"  
         If errLoop.HelpFile = "" Then  
            strError = strError & _  
               "   No Help file available" & _  
               "<br><br>"  
         Else  
            strError = strError & _  
               "   (HelpFile: " & errLoop.HelpFile & ")" & "<br>" & _  
               "   (HelpContext: " & errLoop.HelpContext & ")" & _  
               "<br><br>"  
         End If  
  
         Response.Write("<p>" & strError & "</p>")  
      Next  
   End If  
  
%>  
  
</BODY>  
</HTML>  
<!-- EndErrorExampleVBS -->  
```