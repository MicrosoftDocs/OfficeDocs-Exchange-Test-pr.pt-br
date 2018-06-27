---
title: 'Desabilitar a caixa postal de um usuário: Exchange 2013 Help'
TOCTitle: Desabilitar a caixa postal de um usuário
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 50486686
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar a caixa postal de um usuário

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-05_

Você pode desabilitar a Unificação de mensagens (UM) para um usuário habilitado para UM. Quando você fizer isso, o usuário não pode usar os recursos de caixa postal encontrados na Unificação de mensagens. Se você preferir, quando você desabilitar a Unificação de mensagens para um usuário, você pode manter as configurações de Unificação de mensagens para o usuário.

Para conhecer tarefas de gerenciamento adicionais relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que o usuário existente no momento é habilitado para Unificação de mensagens. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para desabilitar a Unificação de mensagens e caixa postal de um usuário

1.  No EAC, clique em **Destinatários**.

2.  Na exibição de lista, selecione o usuário cuja caixa de correio que você deseja desabilitar para Unificação de mensagens.

3.  No painel de detalhes, em **telefone e recursos de voz**, em **Unificação de mensagens**, clique em **Desabilitar**.

4.  Na caixa de **Aviso**, clique em **Sim** para confirmar que Unificação de mensagens será desabilitada para o usuário.

## Usar o Shell para desabilitar a Unificação de mensagens e caixa postal de um usuário

Este exemplo desabilita a Unificação de mensagens e caixa postal de tonysmith@contoso.com o usuário, mas mantém as configurações de caixa de correio de Unificação de mensagens.

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

