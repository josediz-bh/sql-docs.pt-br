---
title: Números de erro nativos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1bc1f9383ab615a24b0506b86cf0ec5e37b6c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783399"
---
# <a name="native-error-numbers"></a>Números de erro nativos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para erros que ocorrem na fonte de dados (retornada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client retorna o número de erro nativo retornado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ele pelo. Para erros detectados pelo driver, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client retorna um número de erro nativo de 0. Para obter mais informações sobre uma lista de números de erro nativos, consulte a coluna erro da tabela do sistema **sysmessages** no banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dados **mestre** no.  
  
 Para obter informações sobre os códigos de erro de estado, consulte [SQLSTATE &#40;códigos de erro ODBC&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Para erros retornados pela Biblioteca de Rede, o número de erro nativo é do software de rede subjacente.  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
