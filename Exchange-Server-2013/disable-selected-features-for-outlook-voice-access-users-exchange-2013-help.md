---
title: 'Desabilitar recursos selecionados para usuários do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Desabilitar recursos selecionados para usuários do Outlook Voice Access
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50556164
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar recursos selecionados para usuários do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

O Outlook Voice Access contém duas interfaces: a TUI (interface do usuário de telefone) e a VUI (interface do usuário de voz). Por padrão, quando os usuários discam para o Outlook Voice Access, eles podem acessar seu calendário, email e contatos pessoais, além de pesquisar no diretório. O Shell pode ser usado para impedir que os usuários acessem um ou mais desses recursos quando usarem o Outlook Voice Access para acessar suas caixas de correio. Ao modificar recursos do Outlook Voice Access em uma diretiva de caixa de correio de UM (Unificação de Mensagens), as alterações afetam a todos os usuários que estejam associados à diretiva de caixa de correio de UM.

Você pode desabilitar o acesso dos usuários aos seguintes recursos do Outlook Voice Access em uma diretiva de caixa de correio de UM:

  - Calendário

  - Directory

  - Email

  - Contatos pessoais

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

Você também pode usar o Shell para desabilitar recursos do Outlook Voice Access na caixa de correio de um único usuário habilitado para a UM. Ao fazer isso, os recursos serão desabilitados apenas para esse usuário. Embora não seja possível desabilitar todos os recursos do Outlook Voice Access encontrados em uma política de caixa de correio de UM para um único usuário, você pode desabilitar o acesso ao calendário e ao email dele.

Para conhecer tarefas de gerenciamento adicionais relacionadas a caixas de correio de UM, consulte [Caixa postal para usuários](voice-mail-for-users-exchange-2013-help.md).


> [!TIP]
> Apenas o Shell pode ser usado para modificar os recursos do Outlook&nbsp;Voice Access para usuários habilitados para a UM em uma política de caixa de correio de UM ou na caixa de correio de um único usuário habilitado para a UM.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um usuário foi habilitado para UM. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para desabilitar recursos selecionados do Outlook Voice Access para usuários habilitados para a UM em uma diretiva de caixa de correio de UM

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

Este exemplo impede que os usuários associados a uma política de caixa de correio de UM chamada `MyUMMailboxPolicy` acessem seus calendários ao discar para o Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

Este exemplo impede que os usuários associados à política de caixa de correio de UM chamada `MyUMMailboxPolicy` acessem o diretório ao discar para o Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

Este exemplo impede que os usuários associados à política de caixa de correio de UM chamada `MyUMMailboxPolicy` acessem o email ao discar para o Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

Este exemplo impede que os usuários associados à política de caixa de correio de UM chamada `MyUMMailboxPolicy` acessem contatos pessoais ao discar para o Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## Usar o Shell para desabilitar recursos selecionados do Outlook Voice Access na caixa de correio de um único usuário habilitado para a UM

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

Este exemplo desabilita o acesso ao calendário em uma caixa de correio de UM chamada tony@contoso.com quando o usuário disca para o Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

Este exemplo desabilita o acesso ao email em uma caixa de correio de UM chamada tony@contoso.com quando o usuário disca para o Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

