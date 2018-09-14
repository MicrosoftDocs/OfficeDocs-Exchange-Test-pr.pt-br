---
title: 'Configurar o fuso horário: Exchange 2013 Help'
TOCTitle: Configurar o fuso horário
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50556179
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o fuso horário

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-17_

Por padrão, o atendedor automático da UM (Unificação de Mensagens) usa o fuso horário do servidor de caixa de Correio no qual é criado. Porém, existem situações em que pode ser necessário alterar o fuso horário de um atendedor automático da UM para outro fuso horário. Por exemplo, se você possui dois planos de discagem de UM e cada plano de discagem representa um fuso horário diferente, você deve configurar um atendedor automático de UM para ter o mesmo fuso horário que o servidor de Caixa de Correio e o outro atendedor automático de UM para ter um fuso horário que seja diferente do servidor de Caixa de Correio.

Para tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o fuso horário

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM para o qual você deseja definir o fuso horário e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendedor Automático da UM**, clique em **Horários Comerciais** e depois, em **Fuso Horário**, selecione o fuso horário na lista suspensa.

4.  Para salvar as alterações, clique em **OK** e, em seguida, clique em **salvar**.

## Usar o Shell para configurar o fuso horário

Este exemplo configura o fuso horário com a hora do Pacífico em um Atendedor Automático da UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

