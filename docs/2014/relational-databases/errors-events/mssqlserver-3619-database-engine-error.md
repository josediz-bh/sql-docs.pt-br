---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a82902d69a1d5214b29f43d19ded58c76293ec4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914022"
---
# <a name="mssqlserver_3619"></a>MSSQLSERVER_3619
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|3619|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SYS_NOLOG|  
|Texto da mensagem|Não foi possível gravar um registro de ponto de verificação na ID do banco de dados %d porque não há espaço no log. Entre em contato com o administrador de banco de dados para truncar o log ou aloque mais espaço para os arquivos de log de banco de dados.|  
  
## <a name="explanation"></a>Explicação  
 O log de transações tem espaço em disco insuficiente.  
  
## <a name="user-action"></a>Ação do usuário  
 Trunque o log para liberar espaço ou aloque mais espaço para o log. Para obter mais informações, consulte “Solucionando problemas em um log de transação completa (erro 9002)” nos Manuais Online do SQL Server.  
  
  
