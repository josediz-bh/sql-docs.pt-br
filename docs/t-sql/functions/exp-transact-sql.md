---
title: EXP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EXP_TSQL
- EXP
dev_langs:
- TSQL
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 5a9b8c52-6fb6-4e33-8b02-a878785b2f51
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 638e9960af007710b7c9a891109597db14227092
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071588"
---
# <a name="exp-transact-sql"></a>EXP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o valor exponencial da expressão **float** especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
EXP ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em **float**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **float**  
  
## <a name="remarks"></a>Comentários  
 A constante **e** (2,718281...) é a base dos logaritmos naturais.  
  
 O expoente de um número é a constante **e** elevada à potência do número. Por exemplo, EXP(1,0) = e^1,0 = 2,71828182845905 e EXP(10) = e^10 = 22026,4657948067.  
  
 O exponencial do logaritmo natural de um número é o próprio número: EXP (LOG (*n*)) = *n*. Além disso, o logaritmo natural do exponencial de um número é o próprio número: LOG (EXP (*n*)) = *n*.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-exponent-of-a-number"></a>a. Localizando o expoente de um número  
 O exemplo a seguir declara uma variável e retorna o valor exponencial da variável especificada (`10`) com uma descrição de texto.  
  
```  
DECLARE @var float  
SET @var = 10  
SELECT 'The EXP of the variable is: ' + CONVERT(varchar,EXP(@var))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------------------------------  
The EXP of the variable is: 22026.5  
(1 row(s) affected)  
```  
  
### <a name="b-finding-exponentials-and-natural-logarithms"></a>B. Localizando exponenciais e logaritmos naturais  
 O exemplo a seguir retorna o valor exponencial do logaritmo natural de `20`) e o logaritmo natural do exponencial de `20`. Como estas são funções inversas uma da outra, o valor de retorno em ambos os casos é `20`.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------- ----------------------  
20                     20  
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-finding-the-exponent-of-a-number"></a>C. Localizando o expoente de um número  
 O exemplo a seguir retorna o valor exponencial do valor especificado (`10`).  
  
```  
SELECT EXP(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------  
22026.4657948067  
```  
  
### <a name="d-finding-exponential-values-and-natural-logarithms"></a>D. Localizando valores exponenciais e logaritmos naturais  
 O exemplo a seguir retorna o valor exponencial do logaritmo natural de `20`) e o logaritmo natural do exponencial de `20`. Como estas são funções inversas uma da outra, o valor de retorno em ambos os casos é `20`.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------- -----------------  
20                  20  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [LOG &#40;Transact-SQL&#41;](../../t-sql/functions/log-transact-sql.md)   
 [LOG10 &#40;Transact-SQL&#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

