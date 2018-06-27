---
title: 'Permitir ou impedir transferindo chamadas de um atendedor automático: Exchange 2013 Help'
TOCTitle: Permitir ou impedir transferindo chamadas de um atendedor automático
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52058498
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir ou impedir transferindo chamadas de um atendedor automático

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode permitir que os chamadores transferir chamadas para usuários por meio de um atendedor automático ou impedir isso. Por padrão essa opção está habilitada e permite que os chamadores transferir chamadas para usuários habilitados para UM no plano de discagem de Unificação de mensagens (UM) que está associado a UM atendedor automático.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou impedir transferências de chamada aos usuários um atendedor automático

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja configurar a transferência de chamada e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **acesso de operador e catálogo de endereços**, em **Opções para entrar em contato com os usuários**, marque a caixa de seleção ao lado de **Permitir que os chamadores para usuários de discagem** para habilitar chamadas a ser transferido. Para impedir que transferências de chamada, desmarque a caixa de seleção.

4.  Clique em **Salvar**.


> [!TIP]
> Se você desmarcar essa caixa de seleção e também, desmarque a caixa de seleção <STRONG>Permitir que chamadores deixar mensagens de voz para usuários</STRONG>, as <STRONG>Opções para pesquisar o catálogo de endereços</STRONG> será desabilitada.



## Usar o Shell para habilitar ou impedir transferências de chamada aos usuários um atendedor automático

Este exemplo impede que as transferências de chamada em um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

Este exemplo habilita as transferências de chamada em um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

