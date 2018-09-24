---
title: 'Importar prompts personalizados do Exchange 2007 para o Exchange 2013'
TOCTitle: Importe prompts personalizados do Exchange 2007 para o Exchange 2013
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54651972
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importe prompts personalizados do Exchange 2007 para o Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-04-08_

Você pode importar os arquivos de áudio que contém as saudações, informes, menus e prompts personalizados da Unificação de Mensagens (UM) do Exchange 2007 para a Unificação de Mensagens do Exchange 2013. Usando um script de Shell, os prompts são importados para uma caixa de correio do sistema do Exchange chamada {e0dc1c29-89c3-4034-b678-e6c29d823ed9}, que é criada quado você instala o Microsoft Exchange 2013. A caixa de correio do sistema é usada na Unificação de Mensagens para armazenar o plano de discagem de armazenamento e as saudações, informes, menus e prompts personalizados do atendedor automático e os relatórios de UM.

Os arquivos de áudio, no formato .wav ou .wma, são usados conforme a seguir:

  - Nos planos de discagem de UM, os arquivos de áudio são usados para informes e saudações de boas-vindas personalizados. Eles são reproduzidos quando os usuários do Outlook Voice Access ligam para um número do Outlook Voice Access.

  - Nos atendedores automáticos de UM, os arquivos de áudio são usados para menus de navegação, prompts de menu, informes e saudações de horário comercial e horário não comercial. Eles são reproduzidos quando os chamadores ligam para um número de atendimento automático de UM.

Você pode usar o script MigrateUMCustomPrompts.ps1 para migrar uma cópia de todas as saudações personalizadas de UM, informes, menus e prompts do Exchange Server 2007 para a UM do Exchange 2013 para todos os atendedores automáticos e planos de discagem de UM do Exchange 2007.

Por padrão, o script MigrateUMCustomPrompts.ps1 está localizado em \<Arquivos de Programa\>pasta \\Microsoft\\Exchange Server\\V15\\Scripts em um servidor do Exchange 2013 .


> [!NOTE]
> O script MigrateUMCustomPrompts.ps1 está incluído com o Exchange 2013. Ele deve ser executado em um servidor de Caixa de Correio do Exchange 2013 na mesma organização com os seus servidores do Exchange 2007 .



Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Planos de discagem de Unificação de mensagens" e "atendedores automáticos de UM? entradas no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) .

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant).

  - Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o script MigrateUMCustomPrompts.ps1 para migrar uma cópia de todos os prompts personalizados de planos de discagem e atendedores automáticos da UM.

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange Server 2013** \> **Shell de Gerenciamento do Exchange**.

2.  No Shell, no prompt, digite o caminho para o script. Por exemplo, digite **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**, e aperte Enter.

3.  No prompt do Shell, digite **".\\MigrateUMCustomPrompt",** e aperte Enter.

