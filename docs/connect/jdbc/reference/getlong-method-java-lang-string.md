---
title: Método getLong (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getLong (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 92e30537-5fd9-4b67-8b0f-486c6e840e03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd37233f280cd70f7af4742cf5647eb23e74b710
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921323"
---
# <a name="getlong-method-javalangstring"></a>Método getLong (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como **long** na linguagem de programação Java, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long getLong(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **long**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getLong é especificado pelo método getLong na interface java.sql.CallableStatement.  
  
 Esse método só é compatível com os tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que podem retornar com segurança um valor inteiro como **bigint**, **int**, **smallint**, **tinyint** e **bit**. Seu uso em quaisquer outros tipos de dados fará com que uma exceção seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getLong &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
