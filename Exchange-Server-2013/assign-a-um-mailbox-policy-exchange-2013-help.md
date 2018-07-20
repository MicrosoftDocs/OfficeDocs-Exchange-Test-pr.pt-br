---
title: 'Atribuir uma política de caixa de correio de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Atribuir uma política de caixa de correio de Unificação de mensagens
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 50486616
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atribuir uma política de caixa de correio de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-30_

Quando você habilita um usuário para Unificação de mensagens (UM) e caixa postal, você deve selecionar a política de caixa de correio de Unificação de mensagens que será associada à caixa de correio do usuário. Você pode alterar a política de caixa de correio de Unificação de mensagens associada a caixa de correio do usuário depois que o usuário foi habilitado para Unificação de mensagens.

Criar políticas de caixa de correio de Unificação de mensagens para aplicar um conjunto comum de políticas ou configurações de segurança para um conjunto de caixas de correio de usuários habilitados para UM. Você pode usar políticas de caixa de correio de Unificação de mensagens para aplicar configurações como o seguinte:

  - Diretivas de PIN

  - Restrições de discagem

  - Outras propriedades de política de caixa de correio de Unificação de mensagens gerais


> [!TIP]
> Uma diretiva de caixa de correio de Unificação de mensagens padrão é criada sempre que você criar um plano de discagem de UM. Você pode excluir as políticas de caixa de correio de Unificação de mensagens padrão ou criar diretivas de caixa de correio de Unificação de mensagens adicionais com base nas necessidades de sua organização.



Para conhecer tarefas de gerenciamento adicionais relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que o usuário está habilitado para Unificação de mensagens. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para alterar a política de caixa de correio de Unificação de mensagens atribuída a um usuário habilitado para UM

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na visualização de lista, selecione a caixa de correio para a qual você quer mudar a política de caixa de correio da UM.

3.  No painel de detalhes, em **Telefone e Características de Voz** \> **Unificação de Mensagens**, clique em **Ver detalhes**.

4.  Na página de **Correio de UM**, clique em **configurações de caixa de correio de Unificação de mensagens** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

5.  Na página de **Correio de UM** \> ao lado de **política de caixa de correio de Unificação de mensagens**, clique em **Procurar** para localizar a diretiva de caixa de correio de Unificação de mensagens para o usuário.

6.  Clique em **Salvar**.

## Usar o Shell para alterar a política de caixa de correio de Unificação de mensagens atribuída a um usuário habilitado para UM

Este exemplo associa um usuário habilitado para UM, chamado Tony Smith com uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

