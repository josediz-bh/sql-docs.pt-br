---
title: SQUARE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQUARE
- SQUARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: 007b6b12-da86-4229-8f5c-fdd4fa839f5f
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ef602ecc617f9811b5c40abd1e512a6109fc8ec
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74249795"
---
# <a name="square-transact-sql"></a>SQUARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o quadrado do valor flutuante especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQUARE ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em float.  
  
## <a name="return-types"></a>Tipos de retorno  
 **float**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o volume de um cilindro com raio de `1` centímetro e altura de `5` centímetros.  
  
```  
DECLARE @h float, @r float;  
SET @h = 5;  
SET @r = 1;  
SELECT PI()* SQUARE(@r)* @h AS 'Cyl Vol';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Cyl Vol  
--------------------------  
15.707963267948966  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna o quadrado de cada valor na coluna `volume` da tabela `containers`.  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE Containers (  
    ID int NOT NULL,  
    Name varchar(20),  
    Volume float(24));  
  
INSERT INTO Containers VALUES (1, 'Cylinder', '125.22');  
INSERT INTO Containers VALUES (2, 'Cube', '23.98');  
  
SELECT Name, SQUARE(Volume) AS VolSquared   
FROM Containers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Name           VolSquared
-------------  ----------
Cylinder       15680.05
Cube             575.04
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

