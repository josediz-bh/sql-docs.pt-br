---
title: Criar um alerta de banco de dados do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5d5783646a4ba6e5cad78b0cdcada16a8d27501c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68024824"
---
# <a name="create-a-sql-server-database-alert"></a>Criar um alerta de banco de dados do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  É possível usar o Monitor do Sistema para criar um alerta a ser emitido quando um valor limite de um contador do Monitor do Sistema for atingido. Em resposta ao alerta, o Monitor do Sistema inicia um aplicativo, tal como um aplicativo cliente escrito para manipular a condição de alerta. Por exemplo, você pode criar um alerta a ser emitido quando o número de deadlocks exceder um valor específico.  
  
 Também podem ser definidos alertas por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Alertas](../../ssms/agent/alerts.md).  
  
 Para obter mais informações sobre como usar o Monitor do Sistema para configurar um alerta de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Configurar um alerta de banco de dados do SQL Server &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
