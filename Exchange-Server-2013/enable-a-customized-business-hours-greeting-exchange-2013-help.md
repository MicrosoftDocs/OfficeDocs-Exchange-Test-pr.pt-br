---
title: 'Habilitar uma saudação para horário comercial personalizado: Exchange 2013 Help'
TOCTitle: Habilitar uma saudação para horário comercial personalizado
ms:assetid: a2272b7d-de88-4d3f-81e6-ad81f0ee6c5e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232152(v=EXCHG.150)
ms:contentKeyID: 50556256
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar uma saudação para horário comercial personalizado

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-19_

Você pode habilitar uma saudação para um atendedor automático da Unificação de mensagens (UM) para horário comercial personalizado. Saudação para horário comercial é os primeira coisa que os chamadores ouvem quando um atendedor automático de UM atende a chamada durante o horário comercial. Você provavelmente desejará personalizar a saudação.

A Unificação de mensagens inclui um prompt de sistema padrão para uso durante o horário comercial. Embora o prompt de sistema padrão não deve ser substituído ou alterado, convém fornecer uma saudação personalizada. Você pode criar uma saudação personalizada no formato de arquivo. wav ou. wma a ser usado quando os chamadores ligam para um atendedor automático durante o horário comercial. Por exemplo, "você chegou Woodgrove Bank."

Se você deseja incluir o nome da sua organização ou empresa como parte da saudação padrão, você pode inserir o nome na caixa **nome de negócios** em UM atendedor automático. Para obter detalhes, consulte [Insira um nome de empresa](enter-a-business-name-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Crie um arquivo. wav ou. wma a ser usado para a saudação.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar uma saudação para horário comercial personalizado

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja habilitar uma saudação para horário comercial personalizado e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM**, \> clique em **Alterarsaudações**, em **horário comercial de saudação** e clique em **Procurar** para localizar o arquivo que você criou antes de iniciar esse procedimento de saudação para horário comercial personalizado.
    

    > [!IMPORTANT]
    > O arquivo usado para a saudação deve ser wav. ou .wma.



4.  Depois de ter localizado o arquivo, clique em **Abrir** e em **Salvar**.

## Use o Shell para habilitar uma saudação para horário comercial personalizado

Este exemplo habilita o saudação para horário comercial que usa uma saudação personalizada denominada `GreetingFile.wav` para a Unificação de mensagens auto attendant `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursWelcomeGreetingEnabled $true -BusinessHoursWelcomeGreetingFilename GreetingFile.wav

Este exemplo configura um atendedor automático de UM chamado `MyUMAutoAttendant` para possuírem horários comerciais configurados para ser 10:45 a 13:15 (domingo) 09:00 às 17:00 (segunda-feira) e 09:00 às 16:30 (sábado) e tempos de feriados e suas saudações associadas configuradas para ser "`New Year`" em 2 de janeiro de 2013 e "`Building Closed for Construction`" de 24 de abril de 2013 por meio de 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Este exemplo configura um atendedor automático de UM chamado `MyAutoAttendant` e habilita os mapeamentos de teclas de horário comercial para que, quando os chamadores pressionar 1, eles estiver encaminhados para outro atendedor automático de UM chamado `SalesAutoAttendant`. Quando eles pressionarem 2, eles estiver encaminhados para o número de ramal 12345 para `Support`e quando eles pressionarem 3, elas são enviadas para outro atendedor automático que reproduz um arquivo de áudio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

