---
title: Planos de manutenção de banco de dados substituídos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d41763582632a92b3a38bdbd67ee55b65f95b6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095757"
---
# <a name="database-maintenance-plans-superseded"></a>Planos de manutenção de banco de dados substituídos
    
## <a name="component"></a>Componente  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente do  
  
## <a name="description"></a>DESCRIÇÃO  
 Os planos de manutenção de banco de dados são atualizados e continuam a funcionar. Porém, você não poderá criar novos planos de manutenção de banco de dados usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para exibir os planos de manutenção no Pesquisador de Objetos, expanda Gerenciamento e, em seguida, Herdado. Você pode migrar planos de manutenção de banco de dados existentes para o novo formato selecionando **migrar** no menu de contexto de qualquer plano de manutenção de banco de dados. Como o novo recurso de plano de manutenção não é uma substituição direta para os planos de manutenção de banco de dados, existe a possibilidade de perder algumas funcionalidades após a migração. A migração de um plano de manutenção de banco de dados não exclui o plano anterior, portanto você pode testar sua funcionalidade como um plano de manutenção antes de remover o plano anterior.  
  
 Não há mais suporte para os seguintes recursos dentro dos planos de manutenção de banco de dados:  
  
-   Envio de logs  
  
-   A opção **tentar reparar problemas secundários** da tarefa de **verificação de integridade do banco de dados**  
  
## <a name="corrective-action"></a>Ação corretiva  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impede que o envio de logs seja incluído em um plano de manutenção do banco de dados. Para obter mais informações, consulte o tópico ‘Envio de logs’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
