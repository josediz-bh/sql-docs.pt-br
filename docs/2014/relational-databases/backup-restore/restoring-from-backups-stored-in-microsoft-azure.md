---
title: Restaurando de Backups armazenados no Windows Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 90fe4fd8aacb3d945aab6d2b0872f2aff958f01f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008912"
---
# <a name="restoring-from-backups-stored-in-windows-azure"></a>Restaurando de backups armazenados no Windows Azure
  Este tópico descreve o que você deve considerar ao restaurar um banco de dados usando um backup armazenado no serviço de armazenamento de Blob do Windows Azure. Isso se aplica aos backups criados através do Backup do SQL Server para URL ou pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 É recomendável analisar este tópico se você tiver backups armazenados no serviço de armazenamento de Blob do Windows Azure que pretende restaurar e, em seguida, analisar os tópicos que descrevem as etapas de restauração de um banco de dados, que é o mesmo para backups locais e do Windows Azure.  
  
## <a name="overview"></a>Visão geral  
 As ferramentas e os métodos que são usados para restaurar um banco de dados de um backup local se aplicam à restauração de um banco de dados de um backup na nuvem.  As seções a seguir descrevem essas considerações e todas as diferenças que você deve saber quando usa os backups armazenados no serviço de armazenamento de Blob do Windows Azure.  
  
### <a name="using-transact-sql"></a>Usando Transact-SQL  
  
-   Como o SQL Server precisa se conectar a uma fonte externa para recuperar os arquivos de backup, a Credenciais do SQL é usada para autenticação para a conta de armazenamento. Em virtude disso, a instrução RESTORE requer a opção WITH CREDENTIAL. Para obter mais informações, consulte [SQL Server Backup and Restore with Windows Azure Blob Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
-   Se você estiver usando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para gerenciar seus backups para a nuvem, poderá examinar todos os backups disponíveis no armazenamento usando a função de sistema **smart_admin.fn_available_backups** . Essa função de sistema retorna todos os backups disponíveis para um banco de dados em uma tabela. Como os resultados são retornados em uma tabela, você pode filtrá-los ou classificá-los. Para obter mais informações, consulte [smart_admin &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql).  
  
### <a name="using-sql-server-management-studio"></a>Usando o SQL Server Management Studio  
  
-   A tarefa de restauração é usada restaurar um banco de dados usando o SQL Server Management Studio. A página da mídia de backup agora inclui a opção **URL** para mostrar os arquivos de backup armazenados no serviço de armazenamento de Blob do Windows Azure. Você também deve fornecer a Credencial do SQL usada para autenticação para a conta de armazenamento. A grade **Conjuntos de backup a serem restaurados** é populada com os backups disponíveis no armazenamento de Blob do Windows Azure. Para obter mais informações, consulte [Restoring from Windows Azure storage Using SQL Server Management Studio](sql-server-backup-to-url.md#RestoreSSMS).  
  
### <a name="optimizing-restores"></a>Otimizando restaurações  
 Para reduzir o tempo de gravação da restauração, adicione o direito de usuário **Executar tarefas de manutenção de volume** à conta de usuário do SQL Server. Para obter mais informações, consulte [Inicialização de arquivos de bancos de dados](http://go.microsoft.com/fwlink/?LinkId=271622). Se a restauração ainda estiver lenta com a inicialização instantânea de arquivo ativada, examine o tamanho do arquivo de log na instância onde foi feito o backup do banco de dados. Se o log é muito grande em tamanho (vários GBs), espera-se que a restauração seja lenta. Durante a restauração, o arquivo de log deve ser zerado, o que leva uma quantidade significativa de tempo.  
  
 Para reduzir o tempo de restauração, recomendamos o uso de backups compactados.  Para os tamanhos de backup superiores a 25 GB, use o [utilitário AzCopy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx) para baixar à unidade local e execute a restauração. Para outras práticas recomendadas de backup e recomendações, consulte [SQL Server Backup to URL Best Practices and Troubleshooting](sql-server-backup-to-url-best-practices-and-troubleshooting.md).  
  
 Você também pode ativar o sinalizador de rastreamento 3051 ao fazer a restauração para gerar um log detalhado. Este arquivo de log é colocado no diretório de log e nomeado usando o formato: BackupToUrl-\<instancename>-\<dbname>-action-\<PID>.log. O arquivo de log inclui informações sobre cada viagem de ida e volta para o armazenamento do Windows Azure, inclusive o controle de tempo que pode ser útil para diagnosticar o problema.  
  
### <a name="topics-on-performing-restore-operations"></a>Tópicos sobre a execução de operações de restauração  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](complete-database-restores-full-recovery-model.md)  
  
-   [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)  
  
-   [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)  
  
-   [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  