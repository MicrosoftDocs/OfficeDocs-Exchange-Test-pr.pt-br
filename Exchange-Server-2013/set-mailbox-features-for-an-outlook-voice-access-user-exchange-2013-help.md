---
title: 'Configurar caixas de correio do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar os recursos de caixa de correio para um usuário do Outlook Voice Access
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50556259
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar os recursos de caixa de correio para um usuário do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Configurações de TUI (interface) do usuário de telefone são usadas quando um usuário acessa o sistema de Unificação de mensagens (UM) usando Outlook Voice Access. Quando você modifica as definições de configuração de TUI um habilitado para UM usuário, você deve modificar propriedades e seus valores na caixa de correio do usuário habilitado para UM.

Você pode alterar as seguintes configurações de TUI para um usuário habilitado para Unificação de mensagens:

  - Permitir o acesso do assinante

  - Permitir o acesso TUI no calendário

  - Permitir o acesso TUI para email

  - Permitir que o reconhecimento automático de fala

Para tarefas de gerenciamento adicionais relacionadas aos usuários de Unificação de mensagens, consulte [Configurar os recursos de caixa de correio para um usuário do Outlook Voice Access](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se o destinatário Exchange existente está habilitado para Unificação de mensagens e caixa postal. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para modificar as configurações de TUI um único habilitado para UM usuário

Este exemplo habilita o acesso de calendário e email usando o TUI para um usuário habilitado para UM, chamado Tony Smith.

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True


> [!TIP]
> Configurações de TUI para usuários também estão disponíveis em políticas de caixa de correio de Unificação de mensagens. Modificando configurações de TUI em uma diretiva de caixa de correio UM afeta todos os usuários que estão associados a diretiva de caixa de correio de Unificação de mensagens. Para obter mais informações sobre como modificar as configurações de TUI em uma política de caixa de correio de Unificação de mensagens, consulte <A href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Configurar os recursos de caixa de correio para usuários do Outlook Voice Access</A>.


