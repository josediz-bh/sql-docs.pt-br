---
title: Tarefas do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [Integration Services], tasks
- files [Integration Services], task options
- workflow tasks [Integration Services]
- Integration Services, tasks
- adding package tasks
- tasks [Integration Services], listed
- SSIS tasks
- SSIS, tasks
- control flow [Integration Services], tasks
- tasks [Integration Services]
- grouping tasks
- tasks [Integration Services], about tasks
- SQL Server Integration Services tasks
- data preparation tasks [Integration Services]
- directory operations [Integration Services]
ms.assetid: 75c8901d-6966-4af3-abe5-10af6dd9313b
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9c2a073a222ad9400e7df5f6d4ee0f8c00765cc9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010282"
---
# <a name="integration-services-tasks"></a>Tarefas do Integration Services
  As tarefas são elementos de fluxo de controle que definem unidades de trabalho que são executadas em um fluxo de controle de pacote. Um pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é composto de uma ou mais tarefas. Se o pacote contiver mais de uma tarefa, elas estarão conectadas e sequenciadas no fluxo de controle por restrições de precedência.  
  
 Você também poderá escrever tarefas personalizadas que usam uma linguagem de programação que oferece suporte a COM, como Visual Basic, ou uma linguagem de programação .NET, como C#.  
  
 O Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)], a ferramenta gráfica no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para trabalhar com pacotes, fornece a superfície de design para criar fluxo de controle de pacote e oferece editores personalizados para configurar tarefas. Você também pode programar o modelo de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para criar pacotes programaticamente.  
  
## <a name="types-of-tasks"></a>Tipos de tarefas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os tipos de tarefas a seguir.  
  
 Tarefa de Fluxo de Dados  
 A tarefa que executa fluxos de dados para extrair dados, aplica transformações no nível de coluna e carrega dados.  
  
 Tarefas de preparação de dados  
 Essas tarefas executam os seguintes processos: copiam arquivos e diretórios; baixam arquivos e dados; executam métodos da Web; aplicam operações a documentos XML; e criam perfis de dados para limpeza.  
  
 Tarefas de fluxo de trabalho  
 As tarefas que se comunicam com outros processos para executar pacotes, executar programas ou arquivos em lote, enviar e receber mensagens entre pacotes, enviar mensagens de email, ler dados WMI (Instrumentação de Gerenciamento do Windows) e observar eventos WMI.  
  
 Tarefas do SQL Server  
 As tarefas que acessam, copiam, inserem, excluem e modificam objetos e dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Tarefas de script  
 As tarefas que estendem a funcionalidade de pacotes usando scripts.  
  
 Tarefas Analysis Services  
 As tarefas que criam, modificam, excluem e processam objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Tarefas de manutenção  
 As tarefas que executam funções administrativas como fazer backup e reduzir bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , recriar e reorganizar índices e executar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Tarefas personalizadas  
 Além disso, você pode gravar tarefas personalizadas que usam uma linguagem de programação que dá suporte a COM, como o Visual Basic, ou uma linguagem de programação .NET, como o C#. Para acessar sua tarefa personalizada no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , você poderá criar e registrar uma interface do usuário para a tarefa. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="configuration-of-tasks"></a>Configuração de tarefas  
 Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode conter uma única tarefa, como uma tarefa Execute SQL, que exclui registros de uma tabela de banco de dados quando o pacote é executado. Porém, normalmente os pacotes contêm várias tarefas e cada tarefa é definida para ser executada dentro do contexto do fluxo de controle do pacote. Manipuladores de evento, que são fluxos de trabalho executados como resposta a eventos de tempo de execução, também podem ter tarefas.  
  
 Para obter mais informações sobre como adicionar uma tarefa a um pacote usando o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
 Para obter mais informações sobre como adicionar uma tarefa a um pacote programaticamente, consulte [Adicionando tarefas programaticamente](../building-packages-programmatically/adding-tasks-programmatically.md).  
  
 Toda tarefa pode ser configurada individualmente usando as caixas de diálogo personalizadas de cada tarefa que o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] oferece, ou a janela Propriedades incluída no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Um pacote pode incluir várias tarefas do mesmo tipo, por exemplo, seis tarefas Execute SQL, e cada tarefa pode ser configurada de forma diferente. Para obter mais informações, consulte [Definir as propriedades de tarefas ou contêineres](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="tasks-connections-and-groups"></a>Conexões e grupos de tarefas  
 Se a tarefa contiver mais de uma tarefa, elas estarão conectadas e sequenciadas no fluxo de controle por restrições de precedência. Para obter mais informações, consulte [Precedence Constraints](precedence-constraints.md).  
  
 As tarefas podem ser agrupadas e executadas como uma única unidade de trabalho ou repetidas em um loop. Para obter mais informações, consulte [Contêiner Loop Foreach](foreach-loop-container.md), [Contêiner Loop For](for-loop-container.md)e [Contêiner Sequência](sequence-container.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
  