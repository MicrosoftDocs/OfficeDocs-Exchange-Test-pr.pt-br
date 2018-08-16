---
title: 'Mover banco de dados de caixa de correio com portabilidade de banco de dados'
TOCTitle: Mover um banco de dados de caixa de correio usando a portabilidade de banco de dados
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51407903
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover um banco de dados de caixa de correio usando a portabilidade de banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-16_

É possível utilizar a portabilidade de banco de dados para mover um banco de dados de caixa de correio do Microsoft Exchange Server 2013 entre servidores de caixa de correio do Exchange 2013 na mesma organização. Isso pode ajudar a reduzir o tempo de recuperação total para vários cenários de falha. Para saber mais, consulte [Portabilidade do banco de dados](database-portability-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos, mais o tempo que leva para restaurar os dados, mover os arquivos de banco de dados e aguardar a replicação do Active Directory ser concluída.

  - Entrada "Recuperação da caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Não é possível utilizar o EAC para mover caixas de correio de usuário para um banco de dados recuperado ou de sinal de linha utilizando a portabilidade de banco de dados.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para transferir caixas de correio de usuários para um banco de dados recuperado ou de sinal de linha usando a portabilidade de bancos de dados

1.  Verifique se o banco de dados está no estado de desligamento normal. Se o banco de dados não estiver no estado 'desligamento normal', execute uma recuperação simples
    

    > [!TIP]
    > Quando você executar a recuperação simples, qualquer arquivo de log não confirmado será confirmado no banco de dados. Se você não tiver todos os arquivos de log necessários, não poderá concluir o processo de recuperação simples. Prossiga até a etapa&nbsp;2.

    
    Para confirmar todos os arquivos de log não confirmados no banco de dados, em um prompt de comando, execute o seguinte comando:
    
        ESEUTIL /R <Enn>
    

    > [!TIP]
    > E<EM>nn</EM>&gt; especifica o prefixo de arquivo de log para o banco de dados no qual você pretende repetir os arquivos de log.. O prefixo de arquivo de log especificado pelo &lt;E<EM>nn</EM>&gt; é um parâmetro necessário para o Eseutil /r.



2.  Crie um banco de dados em um servidor usando a seguinte sintaxe:
    
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>

3.  Defina o atributo *This database can be over written by restore* usando a seguinte sintaxe.
    
        Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true

4.  Mova os arquivos de banco de dados originais (arquivos .edb, arquivos de log e catálogo de pesquisa no Exchange) para o arquivo de banco de dados quando você criar um novo banco de dados acima.

5.  Monte o banco de dados usando a seguinte sintaxe:
    
        Mount-Database <DatabaseName>

6.  Depois que o banco de dados estiver montado, modifique as configurações de conta do usuário com o cmdlet[Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) para que a conta aponte para a caixa de correio no novo servidor de caixa de correio. Para mover todos os usuários do banco de dados antigo para o novo banco de dados, use a seguinte sintaxe.
    
        Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>

7.  Acione a entrega de todas as mensagens restantes em filas usando a seguinte sintaxe.
    
        Get-Queue <QueueName> | Retry-Queue -Resubmit $true

Depois que a replicação do Active Directory tiver sido concluída, todos os usuários poderão acessar suas caixas de correio no novo servidor do Exchange. Muitos clientes são redirecionados através da descoberta automática. Os usuários Microsoft Office Outlook Web App os usuários são redirecionados automaticamente.

## Como saber se funcionou?

Para verificar se você moveu a caixa de correio com êxito, faça o seguinte:

  - Abra a caixa de correio utilizando o Outlook Web App.

  - Abra a caixa de correio utilizando o Microsoft Outlook.

