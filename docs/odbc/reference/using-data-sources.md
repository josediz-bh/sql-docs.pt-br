---
title: Usando fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951802"
---
# <a name="using-data-sources"></a>Usar fontes de dados
As fontes de dados geralmente são criadas pelo usuário final ou por um técnico com um programa chamado *Administrador ODBC*. O Administrador ODBC solicita ao usuário o driver a ser usado e, em seguida, chama esse driver. O driver exibe uma caixa de diálogo que solicita as informações necessárias para se conectar à fonte de dados. Depois que o usuário inserir as informações, o driver a armazenará no sistema.  
  
 Posteriormente, o aplicativo chama o Gerenciador de driver e passa o nome de uma fonte de dados de computador ou o caminho de um arquivo que contém uma fonte de dados de arquivo. Quando passado um nome de fonte de dados do computador, o Gerenciador de driver pesquisa o sistema para localizar o driver usado pela fonte de dados. Em seguida, ele carrega o driver e passa o nome da fonte de dados para ele. O driver usa o nome da fonte de dados para localizar as informações necessárias para se conectar à fonte de dados. Por fim, ele se conecta à fonte de dados, normalmente solicita ao usuário uma ID de usuário e uma senha, que geralmente não são armazenadas.  
  
 Quando passada uma fonte de dados de arquivo, o Gerenciador de driver abre o arquivo e carrega o driver especificado. Se o arquivo também contiver uma cadeia de conexão, ele passará isso para o driver. Usando as informações na cadeia de conexão, o driver se conecta à fonte de dados. Se nenhuma cadeia de conexão foi passada, o driver geralmente solicita ao usuário as informações necessárias.
