---
title: Habilitando conjuntos de resultados ativos múltiplos
description: Discute como usar o MARS com o SQL Server.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: feeca1a8bac8b4e1ec55cda0e025ca4b26a94c20
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920434"
---
# <a name="enabling-multiple-active-result-sets"></a>Habilitando conjuntos de resultados ativos múltiplos

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

MARS (Conjuntos de resultados ativos múltiplos) é um recurso que funciona com o SQL Server para permitir a execução de vários lotes em uma única conexão. Quando o MARS está habilitado para uso com o SQL Server, cada objeto de comando usado adiciona uma sessão à conexão.  
  
> [!NOTE]
>  Uma única sessão do MARS abre uma conexão lógica para que o MARS utilize, asism como uma conexão lógica para cada comando ativo.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>Habilitar e desabilitar MARS na cadeia de conexão  
  
> [!NOTE]
>  As cadeias de conexão a seguir usam o banco de dados de exemplo **AdventureWorks** incluído com o SQL Server. As cadeias de conexão fornecidas pressupõem que o banco de dados está instalado em um servidor denominado MSSQL1. Modifique a cadeia de conexão como necessário para o seu ambiente.  
  
O recurso MARS está desabilitado por padrão. Ele pode ser habilitado adicionando o par de palavras-chave "MultipleActiveResultSets=True" à sua cadeia de conexão. "True" é o único valor válido para habilitar MARS. O exemplo a seguir demonstra como se conectar a uma instância do SQL Server e como especificar que o MARS deve estar habilitado. 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
É possível desabilitar MARS adicionando o par de palavras-chave "MultipleActiveResultSets=False" à sua cadeia de conexão. "False" é o único valor válido para desabilitar MARS. A cadeia de conexão a seguir demonstra como desabilitar o MARS.  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>Considerações especiais ao usar o MARS  
Em geral, os aplicativos existentes não devem precisar de modificação para usar uma conexão habilitada para MARS. No entanto, se você quiser usar recursos de MARS em seus aplicativos, deverá entender as considerações especiais a seguir.  
  
### <a name="statement-interleaving"></a>Intercalação de instrução  
As operações de MARS são executadas de forma síncrona no servidor. É permitida a intercalação das instruções SELECT e BULK INSERT. No entanto, as instruções em DML (linguagem de manipulação de dados) e DDL (linguagem de definição de dados) são executadas atomicamente. Todas as tentativas de instruções para serem executadas enquanto um lote atômico estiver em execução serão bloqueadas. A execução paralela no servidor não é um recurso do MARS.  
  
Se dois lotes forem enviados em uma conexão MARS, um deles contendo uma instrução SELECT, o outro contendo uma instrução DML, o DML poderá iniciar a execução na execução da instrução SELECT. No entanto, a instrução DML deve ser executada até a conclusão para que a instrução SELECT possa progredir. Se ambas as instruções estiverem em execução em uma mesma transação, todas as alterações feitas por uma instrução DML após a instrução SELECT começar a execução não ficarão visíveis para a operação de leitura.  
  
Uma instrução WAITFOR dentro de uma instrução SELECT não produzirá a transação enquanto estiver em espera, ou seja, até que a primeira linha seja produzida. Isso implica que nenhum outro lote pode ser executado na mesma conexão enquanto uma instrução WAITFOR está em espera.  
  
### <a name="mars-session-cache"></a>Cache de sessão de MARS  
Quando uma conexão é aberta com o MARS habilitado, uma sessão lógica é criada, o que adiciona sobrecarga extra. Para reduzir a sobrecarga e melhorar o desempenho, o **SqlClient** armazena em cache a sessão de MARS dentro de uma conexão. O cache contém no máximo 10 sessões de MARS. Esse valor não é especificado pelo usuário. Se o limite de sessão for atingido, uma nova sessão será criada – um erro não será gerado. O cache e as sessões que ele contém são por conexão e não são compartilhados entre conexões. Quando uma sessão é liberada, ela retorna ao pool, a menos que o limite superior do pool tenha sido atingido. Se o pool de cache estiver cheio, a sessão será fechada. As sessões de MARS não expiram. Somente são limpas quando o objeto de conexão é descartado. O cache de sessão de MARS não fica pré-carregado. Ele é carregado quando o aplicativo requer mais sessões.  
  
### <a name="thread-safety"></a>Acesso thread-safe  
As operações de MARS não são thread-safe.  
  
### <a name="connection-pooling"></a>Pool de conexões  
Conexões habilitadas para MARS são agrupadas como qualquer outra conexão. Se um aplicativo abrir duas conexões, uma com o MARS habilitado e outra com o MARS desabilitado, as duas conexões ficarão em pools separados.
  
### <a name="sql-server-batch-execution-environment"></a>Ambiente de execução em lote do SQL Server  
Quando uma conexão é aberta, um ambiente padrão é definido. Esse ambiente é então copiado para uma sessão MARS lógica.  
  
O ambiente de execução de lote inclui os seguintes componentes:  
  
- Opções Set (por exemplo, ANSI_NULLS, DATE_FORMAT, idioma, TEXTSIZE)  
  
- Contexto de segurança (função de usuário/aplicativo)  
  
- Contexto de banco de dados (banco de dados atual)  
  
- Variáveis de estado de execução (por exemplo, @@ERROR, @@ROWCOUNT, @@FETCH_STATUS @@IDENTITY)  
  
- Tabelas temporárias de alto nível  
  
Com o MARS, um ambiente de execução padrão é associado a uma conexão. Cada lote novo que inicia a execução sob uma determinada conexão recebe uma cópia do ambiente padrão. Sempre que o código for executado em um determinado lote, todas as alterações feitas no ambiente terão o escopo definido para o lote específico. Quando a execução termina, as configurações de execução são copiadas no ambiente padrão. No caso de um único lote que envia vários comandos a serem executados consecutivamente na mesma transação, as semânticas são as mesmas que aquelas descritas pelas conexões que envolvem clientes ou servidores anteriores.  
  
### <a name="parallel-execution"></a>Execução paralela  
O MARS não foi desenvolvido para remover todos os requisitos de várias conexões em um aplicativo. Se um aplicativo precisar de execução paralela real de comandos em um servidor, será necessário usar várias conexões.  
  
Por exemplo, considere o cenário a seguir. Dois objetos de comando são criados, um para processamento de um conjunto de resultados e outro para a atualização de dados; eles compartilham uma conexão comum via MARS. Neste cenário, a `Transaction`.`Commit` falha na atualização até que todos os resultados tenham sido lidos no primeiro objeto de comando, gerando a seguinte exceção:  
  
Mensagem: O contexto da transação está sendo usado por outra sessão.  
  
Origem: Provedor de Dados do Microsoft SqlClient  
  
Esperado: (nulo)  
  
Recebido: Microsoft.Data.SqlClient.SqlException  
  
Há três opções para lidar com esse cenário:  
  
- Inicie a transação depois que o leitor for criado, para que ele não faça parte da transação. Cada atualização torna-se sua própria transação.  
  
- Confirme todo o trabalho após o fechamento do leitor. Isso tem potencial para um lote substancial de atualizações.  
  
- Não usar MARS; em vez disso, use uma conexão separada para cada objeto de comando, como seria feito antes do MARS.  
  
### <a name="detecting-mars-support"></a>Detectar suporte a MARS  
Um aplicativo pode verificar o suporte a MARS lendo o valor `SqlConnection.ServerVersion`. O número principal deve ser 9 para o SQL Server 2005 e 10 para o SQL Server 2008.  
  
## <a name="next-steps"></a>Próximas etapas
- [MARS (conjunto de resultados ativos múltiplos)](multiple-active-result-sets-mars.md)
