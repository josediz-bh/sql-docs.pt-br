---
title: Introdução
titleSuffix: SQL Server Big Data Clusters
description: Conheça as etapas e os recursos para implantar Clusters de Big Data do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 11bc21819760bebabd12018030c352bd98f79adb
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531093"
---
# <a name="get-started-with-big-data-clusters-2019"></a>Introdução ao [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo apresenta uma visão geral de como implantar o [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md).

Para ver outros cenários de implantação, confira:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Contêineres do Docker](../linux/sql-server-linux-configure-docker.md)

Este artigo descreve os conceitos e fornece uma estrutura para que você possa entender os outros artigos de implantação nesta seção. Suas etapas de implantação específicas variam de acordo com suas opções de plataforma para o cliente e o servidor.

> [!TIP]
> Para obter rapidamente um ambiente com o Kubernetes e o cluster de Big Data implantados para ajudar você a se familiarizar com suas funcionalidades, use um dos scripts de exemplo indicados na [seção sobre scripts](#scripts). Após a implantação, para gerenciar o cluster, use as [ferramentas de cliente](#tools) na seção a seguir.

Assista a este vídeo de 9 minutos para obter uma visão geral de como implantar clusters de Big data:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Clusters-deployment-overview/player?WT.mc_id=dataexposed-c9-niner]


## <a name="client-tools"></a><a id="tools"></a> Ferramentas de cliente

Os clusters de Big Data exigem um conjunto específico de ferramentas de cliente. Antes de implantar um cluster de Big Data no Kubernetes, você deve instalar as seguintes ferramentas:

| Ferramenta | Descrição |
|---|---|
| **azdata** | Implanta e gerencia clusters de Big Data. |
| **kubectl** | Cria e gerencia o cluster do Kubernetes subjacente. |
| **Azure Data Studio** | Interface gráfica para usar o cluster de Big Data. |
| **Extensão do SQL Server 2019** | A extensão do Azure Data Studio que habilita os recursos do cluster de Big Data. |

Outras ferramentas são necessárias para cenários diferentes. Cada artigo deve explicar as ferramentas de pré-requisito para executar uma tarefa específica. Para obter uma lista completa de ferramentas e links de instalação, confira [Instalar ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md).

## <a name="kubernetes"></a>Kubernetes

Os clusters de Big Data são implantados como uma série de contêineres inter-relacionados que são gerenciados no [Kubernetes](https://kubernetes.io/docs/home). Você pode hospedar o Kubernetes de várias maneiras. Mesmo que você já tenha um ambiente Kubernetes existente, examine os requisitos relacionados para clusters de Big Data.

- **AKS (Serviço de Kubernetes do Azure)** : O AKS permite que você implante um cluster do Kubernetes gerenciado no Azure. Você só gerencia e mantém os nós de agente. Com o AKS, você não precisa provisionar seu próprio hardware para o cluster. Também é fácil usar um [script Python](quickstart-big-data-cluster-deploy.md) ou um [notebook de implantação](notebooks-deploy.md) para criar o cluster do AKS e implantar o cluster de Big Data em uma única etapa. Para obter mais informações sobre como configurar o AKS para uma implantação de cluster de Big Data, confira [Configurar o Serviço de Kubernetes do Azure para implantações de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](deploy-on-aks.md).

- **Vários computadores**: Você também pode implantar o Kubernetes em vários computadores Linux, que podem ser servidores físicos ou máquinas virtuais. A ferramenta [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) pode ser usada para criar o cluster do Kubernetes. Você pode usar um [script de Bash](deployment-script-single-node-kubeadm.md) para automatizar esse tipo de implantação. Esse método funcionará bem se você já tiver uma infraestrutura existente que deseja usar para o cluster de Big Data. Para obter mais informações sobre o uso de implantações **kubeadm** com clusters de Big Data, confira [Configurar o Kubernetes em vários computadores para implantações de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](deploy-with-kubeadm.md).

## <a name="deploy-a-big-data-cluster"></a>Implantar um cluster de Big Data

Depois de configurar o Kubernetes, você implanta um cluster de Big Data com o comando `azdata bdc create`. Ao implantar, você pode usar várias abordagens diferentes.

- Se você estiver implantando em um ambiente de desenvolvimento/teste, poderá optar por usar uma das [configurações padrão](deployment-guidance.md#deploy) fornecidas pelo **azdata**.

- Para personalizar sua implantação, você pode criar e usar seus próprios [arquivos de configuração de implantação](deployment-guidance.md#configfile).

- Para uma instalação completamente autônoma, você pode passar todas as outras configurações em variáveis de ambiente. Para obter mais informações, confira [implantações autônomas](deployment-guidance.md#unattended).


## <a name="deployment-scripts"></a><a id="scripts"></a> Scripts de implantação

Os scripts de implantação podem ajudar a implantar clusters do Kubernetes e de Big Data em uma única etapa. Geralmente, eles também fornecem valores padrão para configurações de cluster de Big Data. Você pode personalizar qualquer script de implantação criando sua própria versão que configura a implantação do cluster de Big Data de forma diferente.

Os seguintes scripts de implantação estão disponíveis no momento:

- [Script Python – Implantar um cluster de Big Data no AKS (Serviço de Kubernetes do Azure)](quickstart-big-data-cluster-deploy.md)
- [Script de Bash – Implantar um cluster de Big Data em um cluster kubeadm de nó único](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>Notebooks de implantação

Você também pode implantar um cluster de Big Data executando um notebook do Azure Data Studio. Para obter mais informações sobre como usar um notebook para implantar no AKS, confira o seguinte artigo:

- [Implantar um cluster de Big Data com os notebooks do Azure Data Studio](notebooks-deploy.md).

## <a name="next-steps"></a>Próximas etapas

Depois de implantar com êxito um cluster de Big Data, [conecte-se ao cluster](connect-to-big-data-cluster.md) e considere [carregar dados de exemplo](tutorial-load-sample-data.md) para uso com várias orientações.
