---
title: Construtor SQLServerException (java.lang.String, SQLState, DriverError, java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a9e235417b1a682156d775b8a3458d73eba9e95
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902602"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>Construtor SQLServerException (java.lang.String, SQLState, DriverError, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância da classe [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) quando é dado um objeto **string**, um objeto **sqlstate**, um objeto **drivererror** e um objeto **throwable**.

## <a name="syntax"></a>Sintaxe  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>parâmetros  
 *errText*  
  
 Uma cadeia de caracteres que contém o texto do erro.
  
 *sqlState*  
  
 Um objeto enum que armazena o estado do SQL.
 
 *driverError*  
  
 Um objeto enum que contém o erro do driver.
 
 *causa*  
  
 Um objeto throwable que armazena a causa da exceção.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
