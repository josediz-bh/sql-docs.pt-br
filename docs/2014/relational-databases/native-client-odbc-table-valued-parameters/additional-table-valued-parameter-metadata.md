---
title: Metadados de parâmetro com valor de tabela adicionais | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b9aea58b56308764f907f8cf54bf74bb0663c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200571"
---
# <a name="additional-table-valued-parameter-metadata"></a>Metadados adicionais de parâmetros com valor de tabela
  Para recuperar metadados para um parâmetro com valor de tabela, um aplicativo chama SQLProcedureColumns. Para um parâmetro com valor de tabela, SQLProcedureColumns retorna uma única linha. Duas colunas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]específicas adicionais, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME, foram adicionadas para fornecer informações de esquema e de catálogo para tipos de tabela associados a parâmetros com valor de tabela. Em conformidade com a especificação ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem antes de todas as colunas específicas do driver adicionadas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]versões anteriores do e depois de todas as colunas exigidas pelo próprio ODBC.  
  
 A tabela a seguir lista as colunas significativas para parâmetros com valor de tabela.  
  
|Nome da coluna|Tipo de dados|Valor/comentários|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint não NULL|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128) não NULL|O nome do tipo do parâmetro com valor de tabela.|  
|COLUMN_SIZE|Integer|NULO|  
|BUFFER_LENGTH|Integer|0|  
|DECIMAL_DIGITS|Smallint|NULO|  
|NUM_PREC_RADIX|Smallint|NULO|  
|NULLABLE|Smallint não NULL|SQL_NULLABLE|  
|COMENTÁRIOS|Varchar|NULO|  
|COLUMN_DEF|WVarchar(4000)|NULO|  
|SQL_DATA_TYPE|Smallint não NULL|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULO|  
|CHAR_OCTET_LENGTH|Integer|NULO|  
|ORDINAL_POSITION|Integer não NULL|A posição ordinal do parâmetro.|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) não NULL|O catálogo que contém a definição de tipo do tipo de tabela do parâmetro com valor de tabela.|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) não NULL|O esquema que contém a definição de tipo do tipo de tabela do parâmetro com valor de tabela.|  
  
 As colunas WVarchar são definidas como Varchar na especificação de ODBC, mas são retornadas de fato como WVarchar em todos os drivers ODBC recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta alteração foi feita quando o suporte a Unicode foi adicionado à especificação de ODBC 3.5, mas não chamado explicitamente.  
  
 Para obter metadados adicionais para parâmetros com valor de tabela, um aplicativo usa as funções de catálogo SQLColumns e SQLPrimaryKeys. Antes de essas funções serem chamadas para parâmetros com valor de tabela, o aplicativo deve definir o atributo de instrução SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_TABLE_TYPE. Esse valor indica que o aplicativo exige metadados para um tipo de tabela em lugar de uma tabela real. Em seguida, o aplicativo passa a TYPE_NAME do parâmetro com valor de tabela como o parâmetro *TableName* . SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME são usados com os parâmetros *CatalogName* e *SchemaName* , respectivamente, para identificar o catálogo e o esquema para o parâmetro com valor de tabela. Quando um aplicativo concluir a recuperação de metadados para parâmetros com valor de tabela, ele deve definir SQL_SOPT_SS_NAME_SCOPE novamente com seu valor padrão SQL_SS_NAME_SCOPE_TABLE.  
  
 Quando SQL_SOPT_SS_NAME_SCOPE for definido como SQL_SS_NAME_SCOPE_TABLE, as consultas a servidores vinculados irão falhar. As chamadas para SQLColumns ou SQLPrimaryKeys com um catálogo que contém um componente de servidor falharão.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
