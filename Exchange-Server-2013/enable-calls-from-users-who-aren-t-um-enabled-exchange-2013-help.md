---
title: 'Habilitar chamadas de usuários não habilitados para UM: Exchange 2013 Help'
TOCTitle: Habilitar chamadas de usuários que não são habilitados para Unificação de mensagens
ms:assetid: 3c39c6df-6d7a-469f-b92b-85b3f14bad31
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb267006(v=EXCHG.150)
ms:contentKeyID: 50485404
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar chamadas de usuários que não são habilitados para Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-05_

Você pode habilitar ou desabilitar chamadas de usuários que não estejam habilitados para UM (Unificação de Mensagens). Por padrão, a Unificação de Mensagens permite que as chamadas de entrada de chamadores não autenticados através de um atendedor automático sejam transferidas para usuários habilitados para UM. Com esta opção habilitada, os usuários de fora da organização podem transferir chamadas para usuários habilitados para UM.

Se essa configuração tiver sido desabilitada para um usuário habilitado para UM, a caixa de correio do usuário ainda poderá ser localizada utilizando uma pesquisa de diretório. Entretanto, se um chamador externo tentar a transferência para o usuário, o sistema dirá: "Desculpe, mas não foi possível transferir a ligação para esse usuário." O chamador será em seguida transferido para o operador, caso um operador tenha sido configurado no atendedor automático. Se nenhum operador tiver sido configurado no atendedor automático, a chamada será transferida para um operador de plano de discagem, se algum tiver sido configurado. Caso nenhum ramal de operador tenha sido configurado no atendedor automático habilitado para fala, no atendedor automático de fallback de DTMF ou no plano de discagem, o sistema responderá informando, "Desculpe. Nem o operador nem o serviço de discagem por tom estão disponíveis”.

Para conhecer tarefas de gerenciamento adicionais relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de você executar esse procedimento, verifique se a caixa de correio de usuário foi habilitada para UM. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para habilitar chamadas de usuários que não estão habilitados para UM

Este exemplo permite que Tony Smith receba mensagens de voz de chamadores que não estão habilitados para UM.

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers SearchEnabled

