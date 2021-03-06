---
title: Método Execute21 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8434345dcc4436865e4981a19ef1164d35a852f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964209"
---
# <a name="execute21-method-rds"></a>Método Execute21 (RDS)
Executa a solicitação e cria um conjunto de registros ADO para uso no ADO 2,1.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *ConnectionString*  
 Uma cadeia de caracteres usada para se conectar ao provedor de OLE DB em que a solicitação será enviada para execução. Se um manipulador for especificado usando *handlerString*, ele poderá editar ou substituir a cadeia de conexão.  
  
 *HandlerString*  
 A cadeia de caracteres identifica o manipulador a ser usado com essa execução. A cadeia de caracteres contém duas partes. A primeira parte contém o nome (ProgID) do manipulador a ser usado. A segunda parte da cadeia de caracteres contém argumentos a serem passados para o manipulador. Como a cadeia de caracteres de argumentos é interpretada é específica do manipulador. As duas partes são separadas pela primeira instância de uma vírgula na cadeia de caracteres (embora a cadeia de caracteres de argumentos possa conter vírgulas adicionais). Os argumentos são opcionais.  
  
 *QueryString*  
 Um comando no idioma de comando com suporte do provedor de OLE DB identificado na cadeia de conexão. Para provedores baseados em SQL, ele pode conter uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução de comando, mas para provedores não SQL (por exemplo, MSDataShape), isso pode não ser [!INCLUDE[tsql](../../../includes/tsql-md.md)] uma instrução de consulta.  
  
 Além disso, se um manipulador estiver sendo usado (e for altamente recomendável que um manipulador seja usado), o manipulador poderá alterar ou substituir o valor especificado aqui. Por exemplo, o manipulador normalmente substitui o *QueryString* por uma cadeia de caracteres de consulta de seu arquivo. ini. Por padrão, o arquivo Msdfmap. ini é usado.  
  
 *lMarshalOptions*  
 Usado para definir as opções de marshaling no conjunto de linhas/conjunto de registros que está sendo retornado.  
  
 *TableID*  
 Uma variante do tipo VT_EMPTY ou VT_BSTR. Se esse valor for do tipo VT_EMPTY, ele será ignorado. Se for do tipo VT_BSTR, o conjunto de registros será criado usando **adCmdTableDirect** usando o valor especificado aqui e o parâmetro *QueryString* será ignorado.  
  
 *lExecuteOptions*  
 Um bitmask das opções de execução:  
  
 1 =*ReadOnly* o conjunto de registros será aberto usando **adLockReadOnly**.  
  
 2 =*nobatch* , o conjunto de registros será aberto usando **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* o chamador garante que as informações de parâmetro para todos os parâmetros sejam fornecidas em *pParameters*.  
  
 8 = as informações de parâmetro*GetInfo* para a consulta serão obtidas do provedor de OLE DB e retornadas no parâmetro *pParameters* . A consulta não é executada e nenhum conjunto de registros é retornado.  
  
 16 = GetHiddenColumns o conjunto de registros será aberto usando **adLockBatchOptimistic** e todas as colunas ocultas serão incluídas no conjunto de registros.  
  
 Embora *ReadOnly*, *nobatch* e *GetHiddenColumns* sejam opções mutuamente exclusivas, não é um erro definir mais de um deles. Se várias opções forem definidas, *GetHiddenColumns* terá precedência sobre todas as outras opções, seguidas por *ReadOnly*. Se nenhuma opção for especificada, por padrão, o conjunto de registros será aberto usando **adLockBatchOptimistic** , mas as colunas ocultas não serão incluídas no conjunto de registros.  
  
 *pParameters*  
 Uma variante que contém uma matriz segura de definições de parâmetro. Se a opção *GetInfo* tiver sido especificada em *lExecuteOptions*, esse parâmetro será usado para retornar as definições de parâmetro obtidas do provedor de OLE DB. Caso contrário, esse parâmetro pode estar vazio.  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *handlerString* pode ser nulo. O que ocorre nesse caso depende de como o servidor RDS está configurado. Uma cadeia de caracteres do manipulador de "MSDFMAP. Handler" indica que o manipulador fornecido pela Microsoft (Msdfmap. dll) deve ser usado. Uma cadeia de caracteres de manipulador de "MASDFMAP. Handler, Sample. ini" indica que o manipulador Msdfmap. dll deve ser usado e que o argumento "Sample. ini" deve ser passado para o manipulador. MSDFMAP. dll interpretará o argumento como uma direção para usar o Sample. ini para verificar a conexão e as cadeias de caracteres de consulta.  
  
> [!NOTE]
>  O método **Execute21** é uma versão do [método Execute (RDS)](../../../ado/reference/rds-api/execute-method-rds.md). Onde você precisa usar o método **Execute** para se comunicar com o ADO 2,1, o método **Execute21** pode ser chamado em seu lugar. Os recursos do método **Execute** no ADO 2,5 e versões posteriores são um superconjunto dos recursos fornecidos para o mesmo método no ADO 2,1.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


