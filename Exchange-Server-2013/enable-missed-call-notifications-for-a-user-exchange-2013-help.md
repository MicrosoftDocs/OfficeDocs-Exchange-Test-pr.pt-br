---
title: 'Habilite as notificações de chamada perdida para um usuário: Exchange 2013 Help'
TOCTitle: Habilite as notificações de chamada perdida para um usuário
ms:assetid: aa0cbb60-5422-474f-af16-621aade31c1f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232159(v=EXCHG.150)
ms:contentKeyID: 52058509
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilite as notificações de chamada perdida para um usuário

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-12-09_

É possível habilitar ou desabilitar notificações de chamada perdida para uma diretiva de caixa de correio de Unificação de mensagens (UM) usando o Shell ou o EAC. Uma notificação de chamada perdida é uma mensagem de email é enviada a um usuário quando o usuário não atende uma chamada de entrada e o chamador não deixa uma mensagem de voz. Esta é uma mensagem de email diferentes que a mensagem que contém a mensagem de voz é da esquerda para um usuário.

Quando você desabilitar notificações de chamadas perdidas em uma diretiva de caixa de correio UM, impede que todos os usuários associados a diretiva de caixa de correio de Unificação de mensagens de receber uma mensagem de email quando não atender uma chamada de entrada e o chamador não deixa uma mensagem de voz. Por padrão, as notificações de chamadas perdidas estão habilitadas para cada política de caixa de correio de Unificação de mensagens que é criada. Também por padrão, uma diretiva de caixa de correio UM é criada sempre que você criar um plano de discagem de UM.


> [!TIP]
> Quando você estiver integrando a Unificação de mensagens e Microsoft Lync Server, perdidas chamada notificações não estão disponíveis para os usuários que têm uma caixa de correio localizada em um servidor Exchange 2007 ou caixa de correio do Exchange 2010, quando um usuário se desconecta antes que a chamada será enviada a um servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange.



Para tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Gerenciar uma política de caixa de correio de Unificação de mensagens](manage-a-um-mailbox-policy-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar as notificações de chamadas não atendidas para uma diretiva de caixa de correio de Unificação de mensagens

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **Geral**, marque a caixa de seleção ao lado de **Permitir notificações de chamadas de perdidas**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar as notificações de chamadas não atendidas para uma diretiva de caixa de correio de Unificação de mensagens

Este exemplo habilita as notificações de chamadas não atendidas para uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $true

