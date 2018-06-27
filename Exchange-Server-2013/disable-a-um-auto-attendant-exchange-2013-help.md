---
title: 'Desabilitar um atendedor automático: Exchange 2013 Help'
TOCTitle: Desabilitar um atendedor automático
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 50486371
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar um atendedor automático

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-05_

Por padrão, quando um atendedor automático de Unificação de mensagens (UM) é criado, seu status é definido como desabilitado. Depois de criar UM atendedor automático, você pode alterar seu status ao controle se ele pode atender a chamadas de entrada. Por exemplo, você talvez queira desabilitar UM atendedor automático quando você estiver gravando ou regravação prompts personalizados e mensagens.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que um atendedor automático de UM foi criado. Para obter etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md). Além disso, confirme se o status do atendedor automático de UM é definido como habilitado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para desabilitar um atendedor automático

1.  No EAC, navegue até **Unificação de mensagens** \> **planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem que você deseja alterar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM que deseja desabilitar. Na barra de ferramentas, clique **na seta para baixo**![Ícone Seta para baixo](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Ícone Seta para baixo")

3.  Na página **Aviso**, clique em **Sim**.

## Use o Shell para desabilitar um atendedor automático

Este exemplo desabilita um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

