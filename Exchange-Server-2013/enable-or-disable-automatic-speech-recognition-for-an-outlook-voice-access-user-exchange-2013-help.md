---
title: 'Habilitar ou desabilitar ASR para usuário do Outlook Voice Access'
TOCTitle: Ativar ou desativar o reconhecimento automático de fala para um usuário do Outlook Voice Access
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50556203
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar ou desativar o reconhecimento automático de fala para um usuário do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode configurar o ASR (Reconhecimento Automático de Fala) para um usuário habilitado para Unificação de Mensagens e caixa postal. Quando o ASR está habilitado na caixa de correio de um usuário do Outlook Voice Access, o usuário pode se movimentar pelos menus da caixa de correio com comandos de voz. ASR fica habilitado por padrão. Se o ASR estiver desabilitado, o usuário deverá utilizar dual tone multi-frequency (DTMF), também conhecido como discagem por tom, entradas para mover pelos menus.


> [!TIP]
> O EAC não pode ser usado para configurar esse recurso. Use o Shell para habilitar ou desabilitar o ASR para um usuário de caixa postal.



Para tarefas de gerenciamento adicionais relacionadas a usuários de email de Unificação de mensagens ou voz, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de você executar esses procedimentos, verifique se a caixa de correio de usuário foi habilitada para UM. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para habilitar ou desabilitar o ASR para um usuário habilitado para UM

Este exemplo habilita o ASR para um usuário habilitado para UM denominado `tonysmith`.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

Este exemplo desabilita o ASR para um usuário habilitado para UM denominado `tonysmith`.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

