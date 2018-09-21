---
title: 'Restaurar dados usando um banco de dados de recuperação: Exchange 2013 Help'
TOCTitle: Restaurar dados usando um banco de dados de recuperação
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 50486752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurar dados usando um banco de dados de recuperação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-10-01_

Um banco de dados de recuperação (RDB) é um tipo especial de banco de dados de caixa de correio que permite que você monte e extraia dados de um banco de dados restaurado como parte de uma operação de recuperação. RDBs permitem a recuperação de dados de um backup ou da cópia de um banco de dados, sem afetar o acesso do usuário a dados atuais.

Após criar um RDB, você pode restaurar um banco de dados para o RDB usando um aplicativo de backup ou copiando o banco de dados e seus arquivos de log para uma estrutura de arquivos RDB. Então, você pode usar o cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)) para extrair dados do banco de dados recuperado. Após a extração, os dados podem ser exportados para uma pasta ou mesclados em uma caixa de correio existente.

Para tarefas de gerenciamento adicionais relacionadas a RDBs, consulte [Bancos de dados de recuperação](recovery-databases-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto, mais o tempo que leva para colocar o banco de dados em um estado de desligamento normal e para extrair os dados.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recuperação da caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Alguns aplicativos de backup têm a capacidade de restaurar dados do Exchange diretamente para um banco de dados de recuperação. O Backup do Windows Server pode restaurar somente backups em nível de arquivo para um banco de dados de recuperação. Ele não pode ser usado para restaurar backups em nível de aplicativo para um banco de dados de recuperação.

  - O banco de dados e os arquivos de log que contêm os dados recuperados devem ser restaurados ou copiados para a estrutura de pastas do RDB.

  - O banco de dados deve estar em estado de desligamento normal. Como o RDB é um local de restauração alternativo para todos os bancos de dados, todos os bancos de dados restaurados estarão em estado de desligamento anormal. Você deverá usar o comando **Eseutil /R** para colocar bancos de dados restaurados em um estado de desligamento normal.

## Usar o Shell para recuperar dados usando um banco de dados de recuperação

1.  Copie um banco de dados recuperado e seus arquivos de log ou restaure um banco de dados e seus arquivos de log para o local usado para o seu banco de dados de recuperação.

2.  Use o Eseutil para deixar esse banco de dados em um estado de desligamento normal. No exemplo anterior, o EXX é o prefixo de geração de log do banco de dados (por exemplo, E00, E01, E02 e assim por diante).
    
    ```powershell
Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
```
    
    O exemplo a seguir ilustra uma geração de log do prefixo E01 e um banco de dados de recuperação e um caminho do arquivo de log do E:\\Databases\\RDB1:
    
    ```powershell
Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1
```

3.  Criar um banco de dados de recuperação. Dê um nome único ao banco de dados de recuperação, mas use o nome e o caminho do arquivo do banco de dados para o parâmetro EdbFilePath e a localização dos arquivos de log recuperados para o parâmetro LogFolderPath.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    
    O exemplo a seguir ilustra a criação de um banco de dados recuperado que será usado para recuperar o DB1.edb e seus arquivos de log, localizados em E:\\Databases\\RDB1.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"

4.  Reinicie o serviço Repositório de Informações do Microsoft Exchange:
    
    ```powershell
Restart-Service MSExchangeIS
```

5.  Monte o banco de dados de recuperação:
    
    ```powershell
Mount-database <RDBName>
```

6.  Verifique se o banco de dados montado contém a(s) caixa(s) de correio que deseja restaurar:
    
    ```powershell
Get-MailboxStatistics -Database <RDBName> | ft -auto
```

7.  Use o cmdlet New-MailboxRestoreRequest para restaurar uma caixa de correio ou itens do banco de dados de recuperação para uma caixa de correio de produção.
    
    O exemplo a seguir restaura a caixa de correio de origem com o MailboxGUID 1d20855f-fd54-4681-98e6-e249f7326ddd do banco de dados do correio DB1 para a caixa de correio de destino com o alias Morris.
    
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    
    O exemplo a seguir restaura o conteúdo da caixa de correio de origem que tem o nome de exibição Morris Cornejo no banco de dados de caixa de correio DB1 para a caixa de correio de arquivo morto para Morris@contoso.com.
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  Verificar periodicamente o status da solicitação de restauração de Caixa de Correio usando [Get-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829907\(v=exchg.150\)).
    
    Uma vez que a restauração tenha o status de Concluída, remova a solicitação de restauração usando [Remove-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829910\(v=exchg.150\)). Por exemplo:
    
    ```powershell
Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
```

## Como saber se funcionou?

Para verificar se você recuperou com êxito os dados da caixa de correio, abra a caixa de correio de destino usando o Outlook ou o Outlook Web App e verifique se os dados recuperados estão presentes.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


