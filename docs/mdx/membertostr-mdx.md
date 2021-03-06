---
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a33aede54557491dea50a557ed581929c5383e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001470"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  Retorna uma cadeia de caracteres formatada com MDX (Multidimensional Expressions) que corresponde a um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Esta função retorna uma cadeia de caracteres que contém o nome exclusivo de um membro. Normalmente, ele é usado para passar o UniqueName de um membro para uma função externa.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a cadeia de caracteres [geography]. [Geografia]. [País]. & [Estados Unidos]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
