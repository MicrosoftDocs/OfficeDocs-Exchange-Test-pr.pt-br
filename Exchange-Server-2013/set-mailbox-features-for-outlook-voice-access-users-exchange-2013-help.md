---
title: 'Configurar os recursos de caixa de correio para usuários do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar os recursos de caixa de correio para usuários do Outlook Voice Access
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50556144
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar os recursos de caixa de correio para usuários do Outlook Voice Access

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

O Outlook Voice Access contém duas interfaces: uma TUI (interface do usuário de telefone) e uma VUI (interface do usuário de voz). É possível definir as configurações de TUI de um usuário habilitado para UM quando o usuário acessa uma caixa de correio usando o sistema da UM (Unificação de Mensagens) no Exchange 2013. Ao modificar as configurações de TUI de um usuário habilitado para UM em uma diretiva de caixa de correio da UM, as alterações afetam a todos os usuários que estejam associados à diretiva de caixa de correio da UM. Você pode modificar as configurações de TUI a seguir em uma política de caixa de correio da UM:

  - Acesso sem PIN à caixa postal

  - Respostas de voz para outras mensagens

  - Acesso TUI ao calendário

  - Acesso TUI ao diretório

  - Acesso TUI ao email

  - Acesso TUI aos contatos pessoais


> [!TIP]
> Você pode usar o Shell para modificar as configurações da TUI do Outlook Voice Access para usuários habilitados para UM.



Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para modificar as configurações de TUI em uma diretiva de caixa de correio da UM

Esse exemplo define configurações relacionadas de TUI em uma política de caixa de correio de UM chamada `MyUMMailboxPolicy`.

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

