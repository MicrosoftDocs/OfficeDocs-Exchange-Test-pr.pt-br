---
title: 'Ativar um prompt do menu de horário comercial personalizado: Exchange 2013 Help'
TOCTitle: Ativar um prompt do menu de horário comercial personalizado
ms:assetid: 89053e84-3490-4dc6-ade3-9b6c5dbf4020
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232116(v=EXCHG.150)
ms:contentKeyID: 50556223
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar um prompt do menu de horário comercial personalizado

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-19_

Você pode personalizar o prompt do menu a ser usado por um atendedor automático de Unificação de mensagens (UM) durante o horário comercial. Depois de criar um atendedor automático de UM, um prompt de sistema padrão ("Bem-vindo à Unificação de mensagens") é usado como prompt do menu que os chamadores ouvem após o horário comercial é reproduzida a saudação de boas-vindas. Embora o prompt do sistema não deve ser substituído ou alterado, você pode personalizar as saudações e prompts de menu que são usados com os atendedores automáticos. Depois de criar um arquivo de áudio prompt do menu horário comercial personalizado, você deve habilitar as entradas de navegação de menu em UM atendedor automático para horário comercial.

Se apenas quiser incluir o nome de sua organização ou empresa como parte do prompt de sistema padrão, você poderá inserir o nome na caixa **Nome da Empresa** no atendedor automático da UM. Para detalhes, consulte [Insira um nome de empresa](enter-a-business-name-exchange-2013-help.md).


> [!IMPORTANT]
> Você deve configurar o horário comercial no atendedor automático. Para obter detalhes, consulte <A href="configure-business-hours-exchange-2013-help.md">Configurar o horário comercial</A>.



Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Crie um arquivo .wav ou .wma a ser usado para o prompt de menu.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar um prompt do menu de horário comercial personalizado

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja habilitar um prompt do menu de horário comercial personalizado e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM**, \> **navegação de Menu**, em **horário comercial navegação de menu**, clique em **Alterar** e clique em **Procurar** para localizar o arquivo prompt do menu de horário comercial personalizado.
    

    > [!IMPORTANT]
    > O arquivo utilizado para o prompt de menu deve ser um arquivo .wav ou .wma.



4.  Depois de ter localizado o arquivo, clique em **Abrir** e em **Salvar**.

## Use o Shell para ativar um prompt do menu de horário comercial personalizado

Este exemplo habilita um prompt do menu principal de horário comercial e usa um prompt nomeado `businesshoursprompts.wav` no attendant a Unificação de mensagens automático `MyUMAutoAttendant`personalizado.

    Command Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursMainMenuCustomPromptEnabled $true -BusinessHoursMainMenuCustomPromptFilename BusinessHoursPrompts.wav

Este exemplo configura um atendedor automático de UM chamado `MyUMAutoAttendant` que tenha configurado para ser 10:45 a 13:15 (domingo), o horário comercial 09:00 às 17:00 (segunda-feira) e 09:00 às 16:30 (sábado) e tempos de feriados e suas saudações associadas configuradas para ser "`New Year`" em 2 de janeiro de 2013 e "`Building Closed for Construction`" de 24 de abril de 2013 por meio de 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Este exemplo configura um atendedor automático de UM chamado `MyAutoAttendant` e habilita o horário comercial menus de navegação para que quando os chamadores pressionar 1, eles estiver encaminhados para outro atendedor automático de UM chamado `SalesAutoAttendant`. Quando eles pressionarem 2, eles estiver encaminhados para o número de ramal 12345 para `Support`e quando eles pressionarem 3, elas são enviadas para outro atendedor automático que reproduz um arquivo de áudio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

