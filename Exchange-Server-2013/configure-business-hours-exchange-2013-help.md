---
title: 'Configurar o horário comercial: Exchange 2013 Help'
TOCTitle: Configurar o horário comercial
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 50486163
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o horário comercial

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-19_

Ao configurar horários comerciais para um atendedor automático da Unificação de mensagens (UM), você define os horários do dia em que sua organização estiver aberta e as saudações de horário comercial e os chamadores prompts de menu ouvirá quando ele liga um número de ramal que está configurado no atendedor automático. Se um chamador atingir o atendedor automático durante o horário em que está fora do horário comercial que você define, o chamador escutará as saudações e prompts de horário não comercial.

Várias opções de agendamento padrão estão disponíveis no EAC. Por exemplo, muitas empresas economizem é aberta das 8:00:00 às 17:00 horas, de segunda à sexta-feira. Em alguns casos, as opções padrão não atendem às suas necessidades e você vai querer personalizar o agendamento. Se seu horário comercial variam das agendas definidas pelo sistema, é possível definir uma agenda personalizada para o atendedor automático.

Por padrão, o atendedor automático reproduzirá os prompts de horário comercial e saudações independentemente do tempo de chamadores de dia discam para o atendedor automático.


> [!TIP]
> Quando você definir o agendamento para horário não comercial e de negócios em um atendedor automático de UM, certifique-se do que fuso horário está configurado corretamente.



Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para especificar o horário comercial para um atendedor automático

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja definir o horário comercial e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **horário comercial** em **horário comercial**, clique em **Configurar o horário comercial**.

4.  Na página **Configurar o horário comercial**, selecione o horário em que você deseja usar como seu horário comercial para cada dia da semana.

5.  Clique em **OK** e, em seguida, clique em **Salvar**.

## Use o Shell para especificar o horário comercial para um atendedor automático

Este exemplo define o horário comercial para um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

