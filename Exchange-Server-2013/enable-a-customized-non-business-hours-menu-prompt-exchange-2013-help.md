---
title: 'Ativar um prompt do menu personalizada fora do horário comercial: Exchange 2013 Help'
TOCTitle: Ativar um prompt do menu personalizada fora do horário comercial
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50556139
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar um prompt do menu personalizada fora do horário comercial

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-03-22_

Você pode personalizar o prompt do menu para ser usado por um atendedor automático da UM fora do horário comercial. Depois de criar um atendedor automático da UM, um prompt do sistema padrão (\&quot;Bem-Vindo à Unificação de Mensagens\&quot;) é usado como o prompt de menu que os chamadores ouvem após a saudação de boas vindas de horários não comerciais ser reproduzida. Embora os prompts do sistema não devam ser substituídos ou alterados, você pode personalizar as saudações e os prompts do menu usados com atendedores automáticos da UM. Depois de criar um arquivo de áudio personalizado de prompt do menu de horário não comercial, você deve habilitar as entradas de navegação do menu no atendedor automático da UM para horários não comerciais.

Se apenas quiser incluir o nome de sua organização ou empresa como parte do prompt de sistema padrão, você poderá inserir o nome na caixa **Nome da Empresa** no atendedor automático da UM. Para detalhes, consulte [Insira um nome de empresa](enter-a-business-name-exchange-2013-help.md).


> [!IMPORTANT]
> Você deve configurar o horário comercial no atendedor automático. Quando você configura o horário comercial, o horário não comercial é definido automaticamente. Para detalhes, consulte <A href="configure-business-hours-exchange-2013-help.md">Configurar o horário comercial</A>.



Para tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Crie um arquivo .wav ou .wma a ser usado para o prompt de menu.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para ativar um prompt do menu personalizado de horário não comercial

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM para o qual você deseja habilitar um prompt de menu personalizado de horário não comercial e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendedor Automático da UM**, \> **Navegação do Menu**, em **navegação de menu de horário não comercial**, clique em **Alterar** e depois clique em **Navegar** para localizar o arquivo personalizado de prompt de menu de horário não comercial.
    

    > [!IMPORTANT]
    > O arquivo utilizado para o prompt de menu deve ser um arquivo .wav ou .wma.



4.  Depois de ter localizado o arquivo, clique em **Abrir** e em **Salvar**.

## Usar o Shell para habilitar um prompt do menu personalizado de horário não comercial

Este exemplo habilita um atendedor automático da UM chamado `MyUMAutoAttendant` com o horário comercial configurado como das 10h45 às 13h15 (domingo), das 09h00 às 17h00 (segunda-feira) e das 09h00 às 16h30 (sábado) e horários de feriado e suas saudações associadas configuradas como "`New Year`" em 1 de janeiro de 2013 e "`Building Closed for Construction`" de 24 de abril de 2013 a 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

Este exemplo configura um atendedor automático da UM chamado `MyAutoAttendant` e habilita os menus de navegação de horário não comercial para que, quando os chamadores pressionarem 1, eles sejam encaminhados para outro atendedor automático da UM chamado `SalesAutoAttendant`. Quando pressionarem 2, eles serão encaminhados para o ramal 12345 do `Support` e quando pressionarem 3, eles serão enviados para outro atendedor automático de UM que executa um arquivo de áudio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

