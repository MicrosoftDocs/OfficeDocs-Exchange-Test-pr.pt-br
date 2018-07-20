---
title: 'Habilitar gravação prompt personalizada usando a interface de usuário de telefone: Exchange 2013 Help'
TOCTitle: Habilitar gravação prompt personalizada usando a interface de usuário de telefone
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54651993
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar gravação prompt personalizada usando a interface de usuário de telefone

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2014-09-17_

Você pode usar o Shell para habilitar a gravação de prompts personalizados e saudações para Unificação de mensagens (UM) planos de discagem e atendedores automáticos usando a interface de usuário de telefone (TUI). Isso pode ser útil quando você deseja alterar uma saudação personalizada ou anúncio usando o EAC ou o Shell ou quando houver uma emergência, como fechamento de uma organização por causa de clima grave. Quando você estiver alterando uma saudação personalizada ou anúncio em um atendedor automático, você deve habilitar a gravação de prompt TUI no plano de discagem que está vinculado do atendedor automático.

Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas "Planos de discagem de UM" e "Atendedores Automáticos de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para habilitar um prompt personalizado ou gravação de saudação usando o TUI

Para registrar os prompts personalizados e saudações por meio da interface do usuário de telefone (TUI), siga estas etapas:

1.  Crie uma conta de usuário de domínio que não pode fazer logon interativamente.

2.  Delega a função de administrador da organização Exchange à conta de usuário do domínio.

3.  Crie uma caixa de correio para o usuário de domínio.

4.  Habilite a caixa de correio do usuário do domínio para Unificação de mensagens.
    

    > [!IMPORTANT]
    > Permitir que somente os administradores que estão gerenciando prompts e saudações acesso ao número de ramal e o PIN da conta de usuário. Use esta conta de usuário somente para gerenciar prompts pelo telefone.



5.  Criar e salvar um arquivo. wav ou. wma para usar para uma saudação personalizada para UM plano de discagem ou atendedor automático.
    

    > [!TIP]
    > Arquivos MP3 não podem ser usados para os prompts personalizados.



6.  Use o EAC ou o Shell para configurar o plano de discagem para usar a saudação de boas-vindas personalizada ou configurar o atendedor automático para usar o business ou não - saudação para horário comercial. Para obter detalhes sobre como configurar um plano de discagem, consulte [Ativar uma saudação personalizada para os usuários do Outlook Voice Access](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md). Para obter detalhes sobre como configurar um atendedor automático, consulte [Habilitar uma saudação para horário comercial personalizado](enable-a-customized-business-hours-greeting-exchange-2013-help.md) ou [Habilitar um personalizada não - saudação para horário comercial](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md).

7.  Execute o seguinte cmdlet:
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true


> [!TIP]
> Antes de você pode habilitar a gravação de um prompt personalizado ou saudação, você deve entrar na caixa de correio que está configurado para gravação solicita. Depois que você registre ao novo prompt ou saudação, você deve sair e entrar novamente antes que você possa ouvir o novo prompt ou saudação quando você usa o TUI.



## Executar a gravação de prompt TUI em um atendedor automático

1.  Verifique se o atendedor automático é vinculado ao plano de discagem que você tiver habilitado para gravação de TUI prompt.

2.  Chame um número de telefone que foi configurado no atendedor automático de UM.

3.  Durante o horário comercial ou não-business saudação para o atendedor automático está sendo reproduzido, pressione a tecla de cerquilha (\#) e pressione a tecla estrela (\*).

4.  Você será solicitado a digitar o número do ramal para o usuário. Insira o número do ramal do usuário habilitado para Unificação de mensagens que tem permissão para executar a gravação de TUI prompt.

5.  Você será solicitado a digitar um PIN. Insira o PIN do usuário.

6.  Siga os prompts de sistema para editar ou atualizar o comunicado saudação ou informativo para o atendedor automático.

## Executar a gravação de prompt TUI em um plano de discagem de UM

1.  Chame um número de Outlook Voice Access, que você pode usar para entrar no Outlook Voice Access.

2.  Enquanto as boas-vindas saudação para o plano de discagem está sendo reproduzido, pressione a tecla de cerquilha (\#) e pressione a tecla estrela (\*).

3.  Se você estiver chamando de um telefone que é usado por um usuário habilitado, você será solicitado um PIN. Em vez de inserir o PIN, pressione a tecla estrela (\*). Você será solicitado a digitar um número de ramal. Insira o número do ramal do usuário habilitado para Unificação de mensagens que tem permissão para executar a gravação de TUI prompt.

4.  Se você estiver chamando de um telefone que não seja usado por um usuário habilitado, você será solicitado automaticamente para um número de ramal. Insira o número do ramal do usuário habilitado para Unificação de mensagens que tem permissão para executar a gravação de TUI prompt.

5.  Você será solicitado a digitar um PIN. Insira o PIN do usuário.

6.  Siga os prompts de sistema para editar ou atualizar a saudação de boas-vindas para o plano de discagem ou o informe.

