---
title: srv_paramset (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramset
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 00645f619a89010bb4e2b112d50e00cbc6f40dce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127153"
---
# <a name="srv_paramset-extended-stored-procedure-api"></a>srv_paramset (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Define o valor de um parâmetro de retorno de chamada do procedimento armazenado remoto. Esta função foi substituída pela função **srv_paramsetoutput**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que identifica uma conexão de cliente específica (nesse caso, o identificador que recebeu a chamada do procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *n*  
 Indica o número do parâmetro a ser definido. O primeiro parâmetro é 1.  
  
 *data*  
 É um ponteiro para o valor dos dados a ser enviado de volta ao cliente como o parâmetro de retorno do procedimento armazenado remoto.  
  
 *Len*  
 Especifica o comprimento dos dados a serem retornados. Se o tipo de dados do parâmetro tiver um tamanho constante e não permitir valores nulos (por exemplo, *srvbit* ou *srvint1*), *len* será ignorado.  
  
## <a name="returns"></a>Retornos  
 SUCCEED se o valor do parâmetro tiver sido definido com êxito; caso contrário, FAIL. FAIL será retornado quando não houver procedimentos armazenados remotos atuais, quando não existir o *n*-ésimo parâmetro de procedimento armazenado remoto, quando o parâmetro não for um parâmetro de retorno e quando o argumento *len* não for válido.  
  
 Se *len* for 0, NULL será retornado. Definir *len* como 0 é o único modo de retornar NULL ao cliente.  
  
 Essa função retornará os valores a seguir, se o parâmetro for um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] dos tipos de dados.  
  
|Novos tipos de dados|Comprimento dos dados de retorno|  
|--------------------|------------------------|  
|`BITN`|**NULL:** *Len* = 0, data = IG, RET = 0<br /><br /> **Zero:** N/A<br /><br /> **>= 255:** N/A<br /><br /> **<255:** N/A|  
|`BIGVARCHAR`|**NULL:** *Len* = 0, data = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = Valid, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`BIGCHAR`|**NULL:** *Len* = 0, data = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = Valid, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`BIGBINARY`|**NULL:** *Len* = 0, data = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = Valid, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`BIGVARBINARY`|**NULL:** *Len* = 0, data = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = Valid, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|NCHAR|**NULL:** *Len* = 0, data = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = Valid, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|NVARCHAR|**NULL:** *Len* = 0, data = IG, RET = 1<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = max8k, data = Valid, RET = 0<br /><br /> **<255:** *Len* = <8K, data = Valid, RET = 1|  
|`NTEXT`|**NULL:** *Len* = IG, data = IG, RET = 0<br /><br /> **Zero:** *Len* = IG, data = IG, RET = 0<br /><br /> **>= 255:** *Len* = IG, data = IG, RET = 0<br /><br /> 255: *Len* = IG, data = IG, RET = 0 ** \<**|  
|RET = Valor de retorno de srv_paramset||  
|IG = Valor será ignorado||  
|valid = Qualquer ponteiro válido para dados||  
  
## <a name="remarks"></a>Comentários  
 Os parâmetros contêm dados passados entre os clientes e o aplicativo com procedimentos armazenados remotos. O cliente pode especificar certos parâmetros como parâmetros de retorno. Esses parâmetros de retorno podem conter valores que o aplicativo servidor Open Data Services devolve ao cliente. Usar parâmetros de retorno equivale a passar parâmetros por referência.  
  
 Você não pode definir o valor de retorno para um parâmetro que não foi invocado como um parâmetro de retorno. Use **srv_paramstatus** para determinar como o parâmetro foi invocado.  
  
 Esta função define o valor de retorno para um parâmetro, mas não envia o valor de retorno ao cliente. Todos os parâmetros de retorno, independentemente se seus valores retornados foram ou não com **srv_paramset**, serão automaticamente enviados ao cliente quando **srv_senddone** for chamado com o sinalizador de status SRV_DONE_FINAL definido.  
  
 Quando uma chamada de procedimento armazenado remoto é feita com parâmetros, os parâmetros podem ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto for feita com alguns parâmetros transmitidos pelo nome e outros pela posição, ocorrerá um erro. O manipulador de SRV_RPC ainda é chamado, mas aparece como se não houvesse parâmetros e **srv_rpcparams** retorna 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_paramsetoutput &#40;API de procedimento armazenado estendido&#41;](srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
