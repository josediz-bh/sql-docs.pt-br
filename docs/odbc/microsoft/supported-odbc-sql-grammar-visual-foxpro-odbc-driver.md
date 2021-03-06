---
title: Gramática SQL ODBC com suporte (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 535f2feaf17d2060c1c65e7aba17951bb3339a5d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080064"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Gramática SQL do ODBC com suporte (Driver ODBC do Visual FoxPro)
O driver ODBC do Microsoft Visual FoxPro oferece suporte ao seguinte:  
  
-   Todas as instruções e cláusulas SQL na gramática SQL mínima do ODBC  
  
-   Uma instrução SQL adicional da gramática SQL principal do ODBC  
  
 A tabela a seguir lista os itens com suporte pelo driver, pelo nível de gramática SQL do ODBC.  
  
|Nível|Elementos|Item|  
|-----------|--------------|----------|  
|Mínimo|DDL (Linguagem de Definição de Dados)|CREATE TABLE e DROP TABLE|  
||DML (Linguagem de Manipulação de Dados)|SELECIONAR, inserir, atualizar e excluir|  
||Expressões|Simples (como>B + C)|  
||Tipos de dados|CHAR, VARCHAR ou LONG VARCHAR|  
  
 Além da gramática SQL ODBC com suporte, o driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro completa para os seguintes comandos do Visual FoxPro:  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [EXCLUIR MARCA](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
