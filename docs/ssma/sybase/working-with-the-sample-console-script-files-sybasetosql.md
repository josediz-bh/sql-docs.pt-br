---
title: Trabalhando com os arquivos de script de console de exemplo (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Sample Console Script Files
ms.assetid: ef221118-b442-4ca6-9409-6ee1d9f8d948
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fe9e05f0078f0d1a9d3ab5ea6e2763ac28207085
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091788"
---
# <a name="working-with-the-sample-console-script-files-sybasetosql"></a>Trabalhar com os arquivos de script de console de exemplo (SybaseToSQL)
Alguns arquivos de exemplo foram fornecidos junto com o produto para a referência e o uso do usuário. Esta seção descreve a maneira de personalizar facilmente esses scripts para atender às necessidades do usuário final.  
  
## <a name="sample-console-script-files"></a>Arquivos de script de console de exemplo  
Os seguintes arquivos de script de console de exemplo que abrangem diferentes cenários foram fornecidos para referência de usuário:  
  
-   ServersConnectionFileSample. xml  
  
-   VariableValueFileSample. xml  
  
-   AssessmentReportGenerationSample. xml  
  
-   SqlStatementConversionSample. xml  
  
-   ConversionAndDataMigrationSample. xml  
  
-   **ServersConnectionFileSample. xml:**  
  
    -   Este exemplo fornece os diferentes modos de conexão disponíveis para o banco de dados de origem e destino, e o usuário pode selecionar qualquer modo de acordo com o requisito. Este exemplo contém as definições de servidor.  
  
    -   O usuário pode se conectar ao banco de dados necessário simplesmente alterando os valores para as definições de servidor de origem e de destino necessárias. No exemplo fornecido, todos os valores foram fornecidos como valores de variáveis que estão disponíveis no **VariableValueFileSample. xml**.  Todos os outros parâmetros de conexão podem ser removidos do arquivo de conexão do servidor de trabalho do usuário.  
  
    -   Para obter mais informações sobre como se conectar ao servidor de origem e de destino, consulte [criando os arquivos de conexão do servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md).  
  
-   **VariableValueFileSample. xml:**  
    Todas as variáveis que foram usadas nos arquivos de script de console de `ServersConnectionFileSample.xml` exemplo e foram agrupadas neste arquivo. Para executar os scripts de console de exemplo, o usuário precisa simplesmente substituir os valores de variáveis de exemplo por aqueles definidos pelo usuário e passar esse arquivo como um argumento de linha de comando adicional junto com o arquivo de script.  
  
    Para obter mais informações sobre o arquivo de valor de variável, consulte [criando arquivos de valor de variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md).  
  
-   **AssessmentReportGenerationSample. xml:**  
    Este exemplo permite que o usuário gere um relatório de avaliação XML que pode ser usado pelo usuário para análise antes de começar a converter e migrar dados.  
  
    No `generate-assessment-report` comando, o usuário precisa mandatorily alterar o valor da variável (consulte **VariableValueFileSample. xml**) no `object-name` atributo para o nome do banco de dados que está sendo usado pelo usuário. Dependendo do tipo de objeto especificado, o `object-type` valor também precisará ser alterado.  
  
    Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar `metabase-object` vários nós, conforme ilustrado no exemplo 4 do `generate-assessment-report` comando do arquivo de script do console de exemplo.  
  
    Para obter mais informações sobre como gerar relatórios, consulte [gerando relatórios &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
    > [!NOTE]  
    > -   Certifique-se de que o argumento de linha de comando do arquivo de valor da variável seja passado para o aplicativo de console e VariableValueFileSample. xml seja atualizado com os valores especificados pelo usuário.  
    > -   Verifique se o argumento de linha de comando do arquivo de conexão do servidor foi passado para o aplicativo de console e se o ServersConnectionFileSample. xml está atualizado com os valores de parâmetro de servidor corretos.  
  
-   **SqlStatementConversionSample. xml:**  
    Este exemplo permite que o usuário gere o script `t-sql` correspondente para o comando de `sql` banco de dados de origem fornecido como entrada.  
  
    No `convert-sql-statement` comando, o usuário precisa mandatorily alterar o valor da variável (consulte **VariableValueFileSample. xml**) no `context` atributo para o nome do banco de dados que está sendo usado pelo usuário. O usuário também será solicitado a alterar o valor `sql` do atributo para o comando do `sql` banco de dados de origem que precisa ser convertido.  
  
    O usuário também pode fornecer arquivos SQL a serem convertidos. Isso foi ilustrado no exemplo `convert-sql-statement` 4 do comando do arquivo de script do console de exemplo.  
  
    > [!NOTE]  
    > Certifique-se de que o argumento de linha de comando do arquivo de valor da variável seja passado para o aplicativo de console e VariableValueFileSample. xml seja atualizado com os valores especificados pelo usuário.  
  
-   **ConversionAndDataMigrationSample. xml:**  
     Este exemplo permite que o usuário execute uma migração de ponta a ponta da conversão para a migração de dados. A lista de valores de atributo obrigatórios que eles terão que ser alterados está listada abaixo:  
  
    **Nome do comando**  
  
    `map-schema`  
  
    Mapeamento de esquema do banco de dados de origem para o esquema de destino.  
  
    **Attribute**  
  
    -   `source-schema:`Especifica o banco de dados de origem que exige a conversão.  
  
    -   `sql-server-schema`: Especifica o banco de dados de destino que deve ser migrado para  
  
    **Nome do comando**  
  
    `convert-schema`  
  
    -   Executa a conversão de esquema da origem para o esquema de destino.  
  
    -   Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar `metabase-object` vários nós, conforme ilustrado no exemplo 4 do `convert-schema` comando do arquivo de script do console de exemplo.  
  
    **Attribute**  
  
    `object-name`: Especifique o nome do banco de dados/objeto de origem que exige a conversão. Verifique se o correspondente `object-type` é alterado com base no tipo de objeto especificado no`object-name`  
  
    **Nome do comando**  
  
    `synchronize-target`  
  
    -   Sincroniza os objetos de destino com o banco de dados de destino.  
  
    -   Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar `metabase-object` vários nós, conforme ilustrado no exemplo 3 do `synchronize-target` comando do arquivo de script do console de exemplo.  
  
    **Attribute**  
  
    `object-name:`Especifique o nome do banco de dados/objeto do SQL Server que requer a criação. Verifique se o correspondente `object-type` é alterado com base no tipo de objeto especificado no`object-name`  
  
    **Nome do comando**  
  
    `migrate-data`  
  
    -   Migra os dados de origem para o destino.  
  
    -   Se o usuário tiver que avaliar vários objetos/bancos de dados, ele poderá especificar `metabase-object` vários nós, conforme ilustrado no exemplo 2 do `migrate-data` comando do arquivo de script do console de exemplo.  
  
    **Attribute**  
  
    `object-name:`Especifica o nome do banco de dados/tabelas de origem que exige a migração. Verifique se o correspondente `object-type` é alterado com base no tipo de objeto especificado no`object-name`  
  
## <a name="see-also"></a>Consulte Também  
[Criando arquivos de valor de variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
[Criando os arquivos de conexão do servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
[Gerando relatórios &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)  
  
