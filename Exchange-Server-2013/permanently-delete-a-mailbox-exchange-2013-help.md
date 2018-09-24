---
title: 'Excluir permanentemente uma caixa de correio: Exchange 2013 Help'
TOCTitle: Excluir permanentemente uma caixa de correio
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50556299
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Excluir permanentemente uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-11-16_

Quando você exclui permanentemente caixas de correio ativas e caixas de correio desconectadas, todo o conteúdo de caixa de correio é removido do banco de dados de caixa de correio do Exchange e a perda de dados é permanente. Quando você exclui permanentemente uma caixa de correio ativa, a conta de usuário do Active Directory associada também será excluída.

Uma alternativa para excluir permanentemente uma caixa de correio é desconectá-lo. Depois que você desconecta uma caixa de correio, por padrão, ela é mantida no banco de dados de caixa de correio por 30 dias. Isso lhe dá a oportunidade de reconectar ou restaurar uma caixa de correio antes que ele será limpo do banco de dados.

Para saber mais sobre caixas de correio desconectadas e executar outras tarefas de gerenciamento relacionadas, confira estes tópicos:

  - [Caixas de correio desconectadas](disconnected-mailboxes-exchange-2013-help.md)

  - [Desabilitar ou excluir uma caixa de correio](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Conectar uma caixa de correio desabilitada](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Conectar-se ou restaurar uma caixa de correio excluída](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)


> [!NOTE]
> Você não pode usar o EAC para excluir permanentemente uma caixa de correio ativa ou uma caixa de correio desconectada.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Excluir permanentemente uma caixa de correio ativa

## Use o Shell para excluir permanentemente uma caixa de correio ativa

Execute o seguinte comando para excluir permanentemente uma caixa de correio ativa e a conta de usuário do Active Directory associada.

```powershell
Remove-Mailbox -Identity <identity> -Permanent $true
```


> [!NOTE]
> Se você não incluir o parâmetro <EM>Permanent</EM> , caixa de correio excluída é mantido no banco de dados de caixa de correio por 30 dias, por padrão, antes de serem excluídos permanentemente.



Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-Mailbox](https://technet.microsoft.com/pt-br/library/aa995948\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você tiver excluídos permanentemente uma caixa de correio ativa, faça o seguinte:

1.  Verifique se que a caixa de correio não está mais listada no EAC.

2.  Verifique se que a conta de usuário associada não está mais listada no Active Directory Users and Computers.

3.  Execute o seguinte comando para verificar se a caixa de correio com êxito foi limpo do banco de dados de caixa de correio do Exchange.
    
    ```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {         Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```
    
    Se você limpo com êxito a caixa de correio, o comando não retornará nenhum resultado. Se a caixa de correio não tenha sido removida, o comando retornará informações sobre a caixa de correio.

## Excluir permanentemente uma caixa de correio desconectada

## Usar o Shell para excluir permanentemente uma caixa de correio desconectada

Existem dois tipos de caixas de correio desconectadas: desabilitado e excluída. Você deve especificar um desses tipos ao executar o cmdlet para excluir permanentemente a caixa de correio. Se o tipo que você especificar não corresponder ao tipo real da caixa de correio desconectada, o comando falhará.

Execute o seguinte comando para determinar se uma caixa de correio desconectada estiver desabilitada ou excluída.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

O valor da propriedade *DisconnectReason* para caixas de correio desconectadas será `Disabled` ou `SoftDeleted`.

Você pode executar o seguinte comando para exibir o tipo de todas as caixas de correio desconectadas na sua organização.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason


> [!WARNING]
> Quando você usa o cmdlet <STRONG>Remove-StoreMailbox</STRONG> para excluir permanentemente uma caixa de correio desconectada, todo o seu conteúdo é removido do banco de dados de caixa de correio e a perda de dados é permanente.



Este exemplo exclui permanentemente a caixa de correio desabilitada com GUID 2ab32ce3-fae1-4402-9489-c67e3ae173d3 do banco de dados de caixa de correio MBD01.

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

Este exemplo exclui permanentemente a caixa de correio excluída para promoção de Dan do banco de dados de caixa de correio MBD01.

```powershell
Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted
```

Este exemplo exclui permanentemente todas as caixas de correio excluídas de forma reversível do banco de dados de caixa de correio MBD01.

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Remove-StoreMailbox](https://technet.microsoft.com/pt-br/library/ff829913\(v=exchg.150\)) e [Get-MailboxStatistics](https://technet.microsoft.com/pt-br/library/bb124612\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você tiver excluído permanentemente uma caixa de correio desconectada e se foi limpo com êxito do banco de dados de caixa de correio do Exchange, execute o seguinte comando.

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {     Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```

Se você limpo com êxito a caixa de correio, o comando não retornará nenhum resultado. Se a caixa de correio não tenha sido removida, o comando retornará informações sobre a caixa de correio.

