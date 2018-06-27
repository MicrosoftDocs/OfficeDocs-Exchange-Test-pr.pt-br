---
title: 'Restaurar uma caixa de correio excluída: Exchange 2013 Help'
TOCTitle: Restaurar uma caixa de correio excluída
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50556186
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurar uma caixa de correio excluída

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2012-11-29_

Use o Shell para se conectar a uma caixa de correio excluída a uma conta de usuário do Active Directory. Uma caixa de correio se tornará *excluída* no banco de dados de caixa de correio de origem quando ele é movido para um banco de dados de caixa de correio diferente. Exchange totalmente não excluir a caixa de correio do banco de dados de caixa de correio de origem quando a movimentação está concluída. Em vez disso, a caixa de correio no banco de dados de caixa de correio de origem é transferida para um estado excluída. Isso permite que você restaure a caixa de correio de origem no caso de erros ocorrem durante a movimentação que causar uma falha ou corrupção da caixa de correio no banco de dados de destino. Se isso acontecer, você pode restaurar a caixa de correio de origem e tente a movimentação novamente.

Uma caixa de correio excluída é mantida no banco de dados de origem até que o período de retenção de caixa de correio excluída expirar ou o cmdlet de **Remove-StoreMailbox** é usado para limpar a caixa de correio excluída. Até que uma caixa de correio excluída é permanentemente excluída do banco de dados de caixa de correio do Exchange, você pode usar o Shell para restaurar o conteúdo da caixa de correio excluída a uma caixa de correio existente ou uma caixa de correio de arquivo morto.

Para saber mais sobre caixas de correio excluída e realize outras tarefas de gerenciamento relacionadas, consulte os seguintes tópicos:

  - [Caixas de correio desconectadas](disconnected-mailboxes-exchange-2013-help.md)

  - [Conectar-se ou restaurar uma caixa de correio excluída](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Gerenciar solicitações de restauração de caixa de correio](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Os procedimentos neste tópico só podem ser executados no Shell. Você não pode usar o EAC para restaurar as caixas de correio excluída.

  - Execute o seguinte comando para verificar se a caixa de correio excluída por software que você deseja se conectar a uma conta de usuário ainda existe no banco de dados de caixa de correio e não for uma caixa de correio desabilitada.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    
    A caixa de correio excluída deve existir no banco de dados de caixa de correio e o valor da propriedade *DisconnectReason* deve ser `SoftDeleted`. Se a caixa de correio foi removida do banco de dados, o comando não retornará nenhum resultado.
    
    Como alternativa, execute o seguinte comando para exibir todas as caixas de correio excluída na sua organização.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Usar o Shell para restaurar uma caixa de correio excluída de forma reversível

Você pode usar o Shell para restaurar uma caixa de correio excluída para uma caixa de correio existente usando o cmdlet **New-MailboxRestoreRequest** . Quando você restaura uma caixa de correio excluída, seu conteúdo é copiado para uma caixa de correio existente, o que é chamada de caixa de *correio de destino*. Quando uma solicitação de restauração de caixa de correio for concluída com êxito, a solicitação é mantida por 30 dias, por padrão, antes de ele é removido. Você pode remover com antecedência usando o cmdlet **Remove-MailboxRestoreRequest** .

Depois que uma caixa de correio excluída é restaurada, a caixa de correio é mantida no banco de dados de caixa de correio até que ele é excluído permanentemente por um administrador ou removida quando o período de retenção de caixa de correio excluída expira.

Para criar uma solicitação de restauração de caixa de correio, você precisará usar o nome para exibição, GUID, da caixa de correio ou herdada diferenciados (DN) do nome da caixa de correio excluída. Use o cmdlet **Get-MailboxStatistics** para exibir os valores das propriedades **DisplayName**, **MailboxGuid**e **LegacyDN** para a caixa de correio excluída por software que você deseja restaurar. Por exemplo, execute o seguinte comando para retornar essas informações para todas as caixas de correio desabilitadas e excluída em sua organização.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database

Este exemplo restaura uma caixa de correio do excluída, que é identificada pelo nome da exibição no parâmetro *SourceStoreMailbox* e está localizada em MBXDB01 caixa de correio banco de dados, na caixa de correio de destino chamado Debra Garcia. O parâmetro *AllowLegacyDNMismatch* é usado para a caixa de correio de origem possa ser restaurada uma caixa de correio que não tem o mesmo valor DN Herdado como caixa de correio excluída.

    New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

Este exemplo restaura arquivamento excluída da caixa de correio do Pilar Pinilla, que é identificada pelo GUID da caixa de correio, para sua caixa de correio de arquivo morto atual. O parâmetro *AllowLegacyDNMismatch* não é necessário porque uma caixa de correio principal e sua caixa de correio correspondente do arquivo morto tem o mesmo DN Herdado.

    New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você tiver restaurado com êxito uma caixa de correio excluída na caixa de correio de destino, execute o cmdlet **Get-MailboxRestoreRequest** ou o cmdlet **Get-MailboxRestoreRequestStatistics** para exibir informações sobre a solicitação de restauração. Se a solicitação de restauração foi criada com êxito, a propriedade *Status* terá um valor de **Queued**, **InProgress**ou **Completed**. Quando a solicitação de restauração for concluída, o conteúdo da caixa de correio excluída aparecerá na caixa de correio de destino.

Para obter mais informações, consulte:

  - [Gerenciar solicitações de restauração de caixa de correio](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/pt-br/library/ff829912\(v=exchg.150\))

