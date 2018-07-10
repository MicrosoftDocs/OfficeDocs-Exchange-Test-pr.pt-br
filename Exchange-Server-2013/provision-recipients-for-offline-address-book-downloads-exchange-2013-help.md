---
title: 'Destinatários de provisão para downloads do catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Destinatários de provisão para downloads do catálogo de endereços offline
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50484987
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Destinatários de provisão para downloads do catálogo de endereços offline

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2013-02-15_

Se você usar vários catálogos de endereços offline (OABs) em sua organização, haverá diversas formas de especificar quais destinatários baixam quais OABs:

  - **Por banco de dados de caixa de correio**   É possível usar o EAC ou o Shell a fim de provisionar destinatários para downloads de OAB vinculando um banco de dados de caixa de correio a um OAB padrão para os clientes Office Outlook 2007, Outlook 2010 e Outlook 2013.

  - **Por destinatário**   É possível usar o cmdlet **Set-Mailbox** no Shell para especificar qual OAB é baixando, vinculando o OAB diretamente à caixa de correio de um destinatário.

  - **Por vários destinatários**  É possível usar um comando de pipeline no Shell para especificar o OAB que vários destinatários baixam, com base em atributos comuns.

  - **Por política de catálogo de endereços**   Você pode atribuir uma política de catálogo de endereços (ABP) para uma conta de usuário de caixa de correio para especificar qual OAB é baixado à caixa de correio de um destinatário. Se você atribuir uma ABP a uma conta de usuário que já tenham um OAB atribuído, o OAB atribuído explicitamente à caixa de correio prevalecerá. Para obter mais informações, consulte [Atribuir uma política de catálogo de endereços para usuários de email](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Não é possível usar o EAC (Centro de administração do Exchange) para realizar esses procedimentos. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para provisionar destinatários para downloads de OAB vinculando seu banco de dados de caixa de correio a um banco de dados de pasta pública ou a um OAB padrão

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Banco de dados de caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

Este exemplo configura a distribuição baseada na Web de My OAB para o banco de dados de caixa de correio padrão.

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)).

## Usar o Shell para especificar qual OAB será baixado, vinculando o OAB diretamente à caixa de correio do destinatário

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

Para especificar qual OAB será baixado, vinculando o OAB diretamente à caixa de correio do destinatário, use a sintaxe a seguir.

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>


> [!TIP]
> O parâmetro <EM>Identity</EM> identifica a caixa de correio e pode assumir os seguintes valores: GUID, ADObjectID, DN (nome diferenciado), <EM>domínio\conta</EM>, nome UPN, LegacyExchangeDN, SmtpAddress e alias.



Este exemplo especifica que o usuário Kim baixará o OAB My OAB.

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Usar o Shell para especificar o OAB que vários destinatários baixarão

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

Este exemplo especifica que todas as caixas de correio de usuário nos Estados Unidos para Contoso farão o download do OAB da Contoso nos EUA.

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

Para obter a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-User](https://technet.microsoft.com/pt-br/library/aa996896\(v=exchg.150\)) e [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

