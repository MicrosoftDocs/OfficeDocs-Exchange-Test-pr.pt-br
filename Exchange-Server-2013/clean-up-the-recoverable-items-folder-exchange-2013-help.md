---
title: 'Limpar a pasta itens recuperáveis: Exchange 2013 Help'
TOCTitle: Limpar a pasta itens recuperáveis
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50556221
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Limpar a pasta itens recuperáveis

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-09-30_

(Este tópico foi projetado para administradores de Exchange.)

A pasta itens recuperáveis (conhecido em versões anteriores do Exchange como *o dumpster*) existe para proteger contra exclusões acidentais ou mal-intencionados e para facilitar os esforços de descoberta comumente feitos antes ou durante litígio ou investigações. Para saber mais sobre a pasta itens recuperáveis, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

Como limpar a pasta itens recuperáveis na caixa de correio do usuário depende se a caixa de correio for colocada em retenção In-loco ou retenção de litígio ou tiver habilitado a recuperação de item único:

  - Se uma caixa de correio não é colocada em retenção In-loco ou retenção de litígio ou não tem a recuperação de item único habilitada, você pode simplesmente excluir itens da pasta itens recuperáveis. Depois que está sendo excluído, você não pode usar a recuperação de item único para recuperar os itens.

  - Se a caixa de correio for colocada em retenção In-loco ou retenção de litígio ou tem recuperação de item único habilitada, é importante preservar os dados de caixa de correio até que a suspensão seja removida ou recuperação de item único está desabilitada. Nesse caso, você precisará executar etapas mais detalhadas para limpar a pasta itens recuperáveis.

Para saber mais sobre o bloqueio In-loco e retenção de litígio, consulte [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md). Para saber mais sobre a recuperação de item único, consulte "Recuperação de Item único" em [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

Para saber mais sobre a pasta itens recuperáveis, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir este procedimento: 30 minutos. Isso pode variar dependendo do tamanho da pasta itens recuperáveis

  - Você precisa ter as seguintes funções de gerenciamento para usar o cmdlet de **Search-Mailbox** para pesquisar e excluir mensagens na caixa de correio do usuário.
    
      - **Pesquisa de Caixa de Correio**   Essa função permite procurar mensagens em várias caixas de correio da sua organização. Os administradores não têm essa função atribuída por padrão. Para atribuir a si mesmo esta função para que você possa pesquisar caixas de correio, adicione a si mesmo como um membro do grupo de funções do Gerenciamento de Descoberta. Consulte [Atribuir permissões de descoberta eletrônica no Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).
    
      - **Caixa de correio importar e exportar**   Essa função permite que você excluir mensagens da caixa de correio do usuário. Por padrão, essa função não é atribuída a qualquer grupo de funções. Para excluir mensagens de caixas de correio dos usuários, você pode adicionar a função caixa de correio importar e exportar para o grupo de funções de gerenciamento da organização. Para obter mais informações, consulte a seção "Adicionar uma função a um grupo de funções" no [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md) .

  - Como incorretamente limpando a pasta itens recuperáveis pode resultar em perda de dados, é importante que você esteja familiarizado com a pasta itens recuperáveis e o impacto da remoção de seu conteúdo. Antes de executar este procedimento, é recomendável que você examine as informações em [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para executar estes procedimentos. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Usar o Shell para excluir itens da pasta itens recuperáveis para caixas de correio que não são colocados em espera ou não têm a recuperação de item único habilitada

Este exemplo exclui permanentemente os itens da pasta de itens recuperáveis de Gurinder Singh e também copia os itens na pasta GurinderSingh-RecoverableItems na caixa de correio de pesquisa de descoberta (uma caixa de correio descoberta criada pelo Exchange instalação).

    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent


> [!TIP]
> Para excluir itens da caixa de correio sem copiá-los para outra caixa de correio, use o comando anterior sem os parâmetros <EM>TargetMailbox</EM> e <EM>TargetFolder</EM> .



Para obter informações detalhadas de sintaxes e parâmetros, consulte [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\)).

## Usar o Shell para limpar a pasta itens recuperáveis para caixas de correio que são colocados em espera ou que tenham a recuperação de item único habilitada

Se uma caixa de correio atinge sua cota de itens recuperáveis, recomendamos que você aumentar a cota e não excluir itens da pasta. Você também pode monitorar eventos no log de aplicativos relacionados à cota de aviso de itens recuperáveis e execute as ações necessárias (por exemplo, aumentando a cota ou investigando o crescimento da pasta itens recuperáveis para caixas de correio que chegam a cota de aviso).

Se as restrições de armazenamento ou outros problemas similares impedem a aumentar a cota de itens recuperáveis, e você precisa excluir mensagens da pasta itens recuperáveis de uma caixa de correio em bloqueio In-loco ou retenção de litígio ou tem recuperação de item único habilitada, recomendamos que você primeiro copiar dados da pasta de itens recuperáveis do usuário para outra caixa de correio. Se você estiver excluindo itens devido a restrições de armazenamento em um volume, você pode copiar itens para uma caixa de correio localizada em um volume que tem o armazenamento adequado.

Este procedimento copia os itens da pasta de itens recuperáveis de Gurinder Singh para a pasta GurinderSingh-RecoverableItems na caixa de correio de pesquisa de descoberta. Antes de copiar e excluir itens da pasta itens recuperáveis, primeiro execute várias etapas para certificar-se de itens não são excluídos da pasta itens recuperáveis. Depois de copiar itens para uma caixa de correio de descoberta ou backup e limpar a pasta, você poderá reverter para as configurações anteriores da caixa de correio.

1.  Recupere as seguintes configurações de cota. Certifique-se observar os valores, portanto, você poderá reverter para essas configurações depois limpando a pasta itens recuperáveis:
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    

    > [!TIP]
    > Se o parâmetro <EM>UseDatabaseQuotaDefaults</EM> é definido como <CODE>$true</CODE>, as configurações de cota anterior não serão aplicadas. As configurações de cota correspondente configuradas no banco de dados de caixa de correio são aplicadas, mesmo se configurações individuais de caixa de correio são preenchidas.

    
        Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults

2.  Recupere as configurações de acesso de caixa de correio para a caixa de correio. Certifique-se observar essas configurações para uso futuro.
    
        Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled

3.  Recupere o tamanho atual da pasta itens recuperáveis. Observe o tamanho, de modo que você pode elevar as citações na etapa 6.
    
        Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize

4.  Recupere a configuração atual de Assistente de pasta gerenciada do ciclo de trabalho. Certifique-se observar a configuração para uso futuro.
    
        Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle

5.  Desabilite o acesso do cliente à caixa de correio para certificar-se de que não há alterações podem ser feitas aos dados de caixa de correio para a duração deste procedimento.
    
        Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false

6.  Para certificar-se de que nenhum item será excluído da pasta itens recuperáveis, aumentar a cota de itens recuperáveis, aumentar a cota de aviso de itens recuperáveis e definir o período de retenção de item excluído como um valor maior que o tamanho atual da pasta de itens recuperáveis do usuário. Isso é particularmente importante para preservar as mensagens para caixas de correio colocadas em retenção In-loco ou retenção de litígio. É recomendável elevar essas configurações para duas vezes seu tamanho atual.
    
        Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false

7.  Desative o Assistente de pasta gerenciada no servidor de caixa de correio.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    

    > [!IMPORTANT]
    > Se a caixa de correio reside em um banco de dados de caixa de correio em um grupo de disponibilidade do banco de dados (DAG), você deve desativar o Assistente de pasta gerenciada em cada membro DAG que hospeda uma cópia do banco de dados. Se o banco de dados executar failover para outro servidor, isso impede que o Assistente de pasta gerenciada nesse servidor excluindo dados de caixa de correio.



8.  Desabilitar a recuperação de item único e remova a caixa de correio de litígio.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    

    > [!IMPORTANT]
    > Após executar este comando, pode demorar até uma hora para desabilitar a recuperação de item único ou litígio. Recomendamos que você execute a próxima etapa somente depois este período.



9.  Copie os itens da pasta itens recuperáveis para uma pasta na caixa de correio de pesquisa de descoberta e exclua o conteúdo da caixa de correio de origem.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    Se você precisar excluir somente as mensagens que correspondam às condições especificadas, use o parâmetro *SearchQuery* para especificar as condições. Este exemplo exclui mensagens que tenham a cadeia de caracteres "Your bank statement" no campo **assunto**.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    

    > [!TIP]
    > Não é obrigatório para copiar itens para a caixa de correio de pesquisa de descoberta. Você pode copiar mensagens para qualquer caixa de correio. No entanto, para impedir o acesso aos dados de caixa de correio potencialmente confidenciais, é recomendável copiar mensagens para uma caixa de correio que tem acesso restrito aos gerentes de registros autorizado. Por padrão, o acesso à caixa de correio de pesquisa de descoberta padrão é restrito aos membros do grupo de funções de gerenciamento de descoberta. Para obter detalhes, consulte <A href="in-place-ediscovery-exchange-2013-help.md">Descoberta Eletrônica In-loco</A>.



10. Se a caixa de correio foi colocada em retenção de litígio ou tinha a recuperação de item único habilitada anteriormente, habilitá-los novamente.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    

    > [!IMPORTANT]
    > Após executar este comando, pode demorar até uma hora para habilitar a recuperação de item único ou litígio. Recomendamos que você deseja habilitar o Assistente de pasta gerenciada e permite o acesso de cliente (etapas 11 e 12) somente após este período.



11. Reverta as cotas de seguintes para os valores indicados na etapa 1:
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    Neste exemplo, a caixa de correio é removida da retenção, o período de retenção de item excluído é redefinido para o valor padrão de 14 dias e a cota de itens recuperáveis está configurada para usar o mesmo valor como o banco de dados de caixa de correio. Se os valores que você anotou na etapa 1 forem diferentes, você deve usar os parâmetros anteriores para especificar cada valor e defina o parâmetro *UseDatabaseQuotaDefaults* como `$false`. Se os parâmetros de*and UseDatabaseRetentionDefaultsRetainDeletedItemsFor*foram definidos anteriormente como um valor diferente, você deve revertê-las para os valores indicados na etapa 1.
    
        Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true

12. Ative o Assistente de pasta gerenciada, definindo o ciclo de trabalho de volta para o valor que você anotou na etapa 4. Este exemplo define o ciclo de trabalho para um dia.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

13. Habilite acesso para cliente.
    
        Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/pt-br/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/pt-br/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/pt-br/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\))

## Como saber se funcionou?

Para verificar que você tenha limpos com êxito a pasta itens recuperáveis de uma caixa de correio, use o cmdlet [Get-MailboxFolderStatistics](https://technet.microsoft.com/pt-br/library/aa996762\(v=exchg.150\)) a verificação do tamanho da pasta itens recuperáveis.

Este exemplo recupera o tamanho da pasta itens recuperáveis e contagem de um item e suas subpastas na pasta e cada subpasta.

    Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto

