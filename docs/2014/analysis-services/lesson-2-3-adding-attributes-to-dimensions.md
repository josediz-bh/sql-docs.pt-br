---
title: Adicionando atributos a dimensões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a30424ce322ed356870465422c4f82fb8d7d88d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079028"
---
# <a name="adding-attributes-to-dimensions"></a>Adicionando atributos em dimensões
  Agora que você definiu dimensões, pode populá-las com atributos que representam cada elemento de dados na dimensão. Os atributos geralmente são baseados em campos de uma exibição da fonte de dados. Ao adicionar atributos a uma dimensão, você pode incluir campos de qualquer tabela na exibição da fonte de dados.  
  
 Nesta tarefa, você usará o Designer de Dimensão para adicionar atributos às dimensões Cliente e Produto. A dimensão de Cliente incluirá atributos baseados em campos de ambas as tabelas de Cliente e Geografia.  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>Adicionando atributos à dimensão Cliente  
  
#### <a name="to-add-attributes"></a>Para adicionar atributos  
  
1.  Abra o Designer de Dimensão da dimensão Cliente. Para fazer isso, clique duas vezes na dimensão **Cliente** no nó **Dimensões** do Gerenciador de Soluções.  
  
2.  No painel **Atributos** , observe os atributos Customer Key e Geography Key que foram criados pelo Assistente para Cubos.  
  
3.  Na barra de ferramentas da guia **Estrutura da Dimensão** , verifique se o ícone Zoom para exibir as tabelas do painel **Exibição da Fonte de Dados** está definido para 100%.  
  
4.  Arraste as seguintes colunas da tabela **Customer** do painel **Exibição da Fonte de Dados** para o painel **Atributos** :  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Sexo**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Telemóvel**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  Arraste as seguintes colunas da tabela **Geography** do painel **Exibição da Fonte de Dados** para o painel **Atributos** :  
  
    -   **City**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  No menu Arquivo , clique em **Salvar Tudo**.  
  
## <a name="adding-attributes-to-the-product-dimension"></a>Adicionando atributos à dimensão Produto  
  
#### <a name="to-add-attributes"></a>Para adicionar atributos  
  
1.  Abra o Designer de Dimensão da dimensão Produto. Clique duas vezes na dimensão **Produto** no Gerenciador de Soluções.  
  
2.  No painel **Atributos** , observe o atributo Product Key que foi criado pelo Assistente para Cubos.  
  
3.  Na barra de ferramentas da guia **Estrutura da Dimensão** , verifique se o ícone Zoom para exibir as tabelas do painel **Exibição da Fonte de Dados** está definido para 100%.  
  
4.  Arraste as seguintes colunas da tabela **Product** do painel **Exibição da Fonte de Dados** para o painel **Atributos** :  
  
    -   **StandardCost**  
  
    -   **Color**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **Tamanho**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **Classes**  
  
    -   **Estilo**  
  
    -   **ModelName**  
  
    -   **Início**  
  
    -   **Término**  
  
    -   **Status**  
  
5.  No menu Arquivo , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Revisando as propriedades de dimensão e cubo](lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de propriedades de atributo de dimensão](multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
