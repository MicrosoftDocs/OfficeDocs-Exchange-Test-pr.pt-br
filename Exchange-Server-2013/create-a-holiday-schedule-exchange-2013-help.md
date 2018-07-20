---
title: 'Criar um cronograma de feriados: Exchange 2013 Help'
TOCTitle: Criar um cronograma de feriados
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 50484933
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um cronograma de feriados

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-19_

Você pode definir as datas e os horários em que sua organização estará fechada em feriados e outras ocasiões. Entre as datas de início e as datas de término que você especificar, os chamadores que entrarem em contato com o atendedor automático da UM (Unificação de Mensagens) ouvirão uma saudação de feriado que é especificada quando você configura a agenda de feriado. Depois que o chamador ouvir a saudação de feriado que você especificou, as saudações do horário não comercial e os prompts do menu serão tocados para o chamador.

É possível também criar um agendamento de feriado em uma agenda de feriados existente. Ao criar vários agendamentos de feriados, a Unificação de Mensagens permite sobrepor os horários agendados de feriados. Por exemplo, você pode definir uma agenda de feriados de 15 de dezembro a 31 de dezembro quando sua organização estará fechada para obras, e pode definir outra agenda de feriados de 24 de dezembro a 26 de dezembro. Quando os chamadores ligarem para o atendedor automático de 15 de dezembro a 23 de dezembro e de 27 de dezembro a 31 de dezembro, a saudação de feriado que você especificou para esta agenda será apresentada. Por exemplo, "No momento estamos fechados para obras." Quando os chamadores ligarem para o atendedor automático de 24 de dezembro a 26 de dezembro, outra saudação de feriado será apresentada, como "A empresa está fechada para que nossos funcionários possam aproveitar o natal com suas famílias."

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

## Usar o EAC para especificar uma agenda de feriados para um atendedor automático de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. No modo de exibição de lista, selecione o plano de discagem de UM que deseja alterar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Atendedores Automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja definir o calendário de feriados. Na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendedor Automático de UM**, \> **Horário Comercial**, em **Agenda de feriados**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **Novo Feriado**, configure o seguinte:
    
      - **Nome**   Digite um nome para o horário de feriado.
    
      - **Saudação de feriado** Navegue até o arquivo .wav que você deseja usar como sua saudação. Este é um campo necessário.
    
      - **Data de início** Use essa lista para selecionar o dia em que você deseja que o feriado comece. A agenda do feriado iniciará à meia-noite da data especificada nessa lista.
    
      - **Data de término** Use esta lista para selecionar a data em que você deseja que o feriado termine. A agenda do feriado terminará às 23:59 do dia especificado nessa lista.

5.  Após ter configurado a agenda do feriado, clique em **OK** e em **Salvar**.

## Use o Shell para especificar uma agenda de feriado para um atendedor automático da UM

Este exemplo configura um atendedor automático de UM chamado `MyUMAutoAttendant` com o horário comercial configurado para das 10h45 às 13h15 (domingo), das 09h00 às 17h00 (segunda-feira) e das 09h00 às 16h30 (sábado) e horários de feriado e suas saudações associadas configuradas como "Ano Novo" em 2 de janeiro de 2013 e "Prédio Fechado para Obras" de 24 de abril de 2013 até 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

