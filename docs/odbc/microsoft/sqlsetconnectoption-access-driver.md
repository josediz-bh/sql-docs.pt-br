---
title: SQLSetConnectOption (driver de acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bea124a78e2a180180c59de3577fe1db7637e110
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897791"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de acesso. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|O SQL_ACCESS_MODE fOption pode ser definido como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impedirá atualizações se SQL_ACCESS_MODE estiver definido como SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Quando o driver do Microsoft Access é usado, a opção SQL_AUTOCOMMIT pode ser definida como SQL_AUTOCOMMIT_ON ou SQL_AUTOCOMMIT_OFF, porque o driver do Microsoft Access dá suporte a transações [1].|  
|SQL_CURRENT_QUALIFIER| Com suporte.|  
|SQL_LOGIN_TIMEOUT|Sem suporte.|  
|SQL_OPT_TRACE| Com suporte.|  
|SQL_OPT_TRACEFILE| Com suporte.|  
|SQL_PACKET_SIZE|Sem suporte.|  
|SQL_QUIET_MODE|Sem suporte.|  
|SQL_TRANSLATE_DLL|Sem suporte.|  
|SQL_TRANSLATION_OPTION|Sem suporte.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION sempre é SQL_TXN_READ_COMMITTED.|  
  
 [1] não há suporte para transações atômicas no driver do Microsoft Access. Ao confirmar uma transação usando o driver do Microsoft Access, existe um atraso finito entre o momento em que a transação é confirmada e a hora em que os valores são gravados no disco. Esse atraso é determinado por um atraso inerente ao mecanismo do Microsoft Jet. O tempo limite da página não será menor que um valor mínimo, mesmo que a opção PageTimeout esteja definida abaixo desse valor. Como resultado, não há nenhuma garantia de que os dados confirmados sejam estáveis, já que as alterações podem ser feitas durante o atraso.
