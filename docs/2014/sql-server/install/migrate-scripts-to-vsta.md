---
title: Migrar scripts para o VSTA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cb44a7b635e24c0c2e3266c1cca98a9c4f6a347c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093992"
---
# <a name="migrate-scripts-to-vsta"></a>Migrar scripts para o VSTA
  Quando você atualiza [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] pacotes para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o migra os scripts em quaisquer tarefas de script ou componentes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] de script para o VSTA (Tools for Applications). O VSTA é o ambiente de script usado pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o ambiente de script do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para aplicativos (Vsa).  
  
 Se os scripts em qualquer uma das tarefas ou componentes de Script fizerem referência a interfaces, talvez você precise modificar essas referências antes de atualizar o pacote. Caso contrário, o pacote não será atualizado ou os scripts não serão validados, dependendo do método de atualização utilizado. Para modificar essas referências, substitua referências a interfaces IDTS*xxx*90 com referências às interfaces IDTS*xxx*100 correspondentes.  
  
 Para obter mais informações sobre como migrar scripts e atualizar pacotes, consulte [atualizar pacotes de Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
## <a name="understanding-migration-failures"></a>Noções básicas sobre falhas de migração  
 Quando você migra os scripts, a migração pode falhar por um dos seguintes motivos:  
  
-   O ponto de entrada do script VSA foi renomeado.  
  
     O ponto de entrada especifica o método na classe `ScriptMain` do projeto VSTA que o runtime do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] chama como ponto de entrada para o código da tarefa Script. A classe `ScriptMain` é a classe padrão gerada pelos modelos de script.  
  
-   Não há nenhum ponto de entrada ou existem vários pontos de entrada no script VSA.  
  
-   Não foi possível adicionar referências de assembly.  
  
-   A classe `ScriptMain` foi modificada para herdar de outras classes além da classe `ScriptObjectModelSSIS`. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] o não oferece suporte a várias heranças.  
  
 Você não pode converter um script VSA que [!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)] usa o para um script do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]VSTA que usa o. No entanto, você pode criar um novo script do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]VSTA que usa o. Para obter mais informações, consulte [Codificando e depurando a tarefa Script](../../integration-services/control-flow/script-task.md) e [Codificando e depurando o componente Script](../../integration-services/data-flow/transformations/script-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Estender pacotes com scripts](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  
