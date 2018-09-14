---
title: 'Importar e exportar saudações personalizadas, anúncios, menus e prompts'
TOCTitle: Importar e exportar saudações personalizadas, anúncios, menus e prompts
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54651992
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importar e exportar saudações personalizadas, anúncios, menus e prompts

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-04-08_

Você pode importar e exportar os arquivos de áudio gravados para usar em planos de discagem de Unificação de mensagens (UM) e atendedores automáticos. Por exemplo, talvez você queira exportar e salvar uma cópia de um arquivo de áudio, se você estiver atualizando de uma versão anterior do Exchange. Ou, talvez seja necessário importar uma cópia de um prompt de áudio gravado antes de configurar um plano de discagem ou auto attendant.

Os arquivos de áudio são usados para as seguintes finalidades:

  - Nos planos de discagem de UM, os arquivos de áudio são usados para informes e saudações de boas-vindas personalizados. Eles são reproduzidos quando os usuários do Outlook Voice Access ligam para um número do Outlook Voice Access.

  - Nos atendedores automáticos de UM, os arquivos de áudio são usados para menus de navegação, prompts de menu, informes e saudações de horário comercial e horário não comercial. Eles são reproduzidos quando os chamadores ligam para um número de atendimento automático de UM.

São compatíveis com os seguintes formatos de arquivo de áudio saudações personalizadas, anúncios, menus e prompts:

  - os arquivos. wma codificados com o Windows Media Audio 9.2-96 kbps/44 kHz/estéreo 1-pass CBR (gravador de som do Windows)

  - Windows Media Audio 9-8 kbps/8 kHz de voz/Mono e arquivos. wav codificada com o PCM Linear (16 bit/exemplo), o codec de áudio 8 quilohertz (kHz)

Você importar os arquivos de áudio que são usados pelos planos de discagem de Unificação de mensagens e atendedores automáticos de um para a caixa de correio do sistema denominada {e0dc1c29-89c3-4034-b678-e6c29d823ed9} e exporte os arquivos de áudio desta caixa de correio do sistema. Os arquivos de áudio podem ser importados e exportados usando os cmdlets **Import-UMPrompt** e **Export-UMPrompt** .

Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Planos de discagem de Unificação de mensagens" e "atendedores automáticos de UM? entradas no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) .

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o Shell para importar saudações personalizadas, anúncios, menus e prompts para Unificação de mensagens, planos de discagem e atendedores automáticos de um

Este exemplo importa um arquivo chamado welcomegreeting. wav de d:\\UMPrompts para o de plano de discagem de Unificação de mensagens `MyUMDialPlan`de saudação bem-vindo.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

Este exemplo importa o arquivo de saudação de boas-vindas denominado welcomegreeting. wav de d:\\UMPrompts para a Unificação de mensagens auto attendant `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## Use o Shell para exportar saudações personalizadas, anúncios, menus e prompts de UM planos de discagem e atendedores automáticos de um

Este exemplo exporta a saudação de boas-vindas para o de plano de discagem de Unificação de mensagens `MyUMDialPlan` e salvará como o arquivo denominado welcomegreeting.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

Este exemplo exporta a saudação de boas-vindas do horário comercial para a Unificação de mensagens auto attendant `MYUMAutoAttendant` e salvará como o arquivo denominado BusinessHoursWelcomeGreeting.wav.

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

