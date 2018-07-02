---
title: 'Configurar um atendedor automático de fallback de DTMF: Exchange 2013 Help'
TOCTitle: Configurar um atendedor automático de fallback de DTMF
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 50486354
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um atendedor automático de fallback de DTMF

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-30_

Você pode configurar um Atendedor de automático de Unificação de mensagens (UM) habilitados para fala que tenha um Atendedor de automático de fallback de DTMF (Multifreqüência) de tom dual. Um atendedor automático de fallback de DTMF é usado quando UM atendedor automático habilitado para fala não é possível entender ou reconhece as entradas de fala fornecidas por um chamador. Se um atendedor automático de fallback de DTMF tiver sido configurado, o chamador deve usar entradas de DTMF, também conhecido como entradas de toque para navegar pelo sistema de menu do atendedor automático, um nome de usuário de ortografia ou usar um prompt de menu personalizado. Se nenhum atendedor automático de fallback de DTMF foi configurada e o número máximo de entradas de fala for excedido, porque o sistema não entender o que o chamador dito, o sistema irá responder com esse prompt: "Desculpe, eu não pôde ajudar. Entre em contato novamente mais tarde."

Por padrão, um atendedor automático não está habilitado para fala quando você criá-lo. Depois que você fala habilita o atendedor automático, os chamadores podem usar apenas os comandos de voz para navegar pelo sistema de menu do atendedor automático e entradas de toque não podem ser usadas. Embora não seja obrigatório, é recomendável que você configure um atendedor automático de fallback de DTMF para cada atendedor automático habilitado para fala para que os chamadores podem usar entradas de toque, se o atendedor automático habilitado para fala não reconhecer nem entender as palavras que eles dizem. Também recomendamos que você não fala habilita um atendedor automático de fallback de DTMF.

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

## Usar o EAC para configurar um atendedor automático habilitado para fala com um atendedor automático de fallback de DTMF

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione do atendedor automático para o qual você deseja criar um atendedor automático de fallback de DTMF. Na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendente automático de UM** \> **Geral**, marque a caixa de seleção ao lado de **usar este atendedor automático quando os comandos de voz não funcionam corretamente** e, em seguida, clique em **Procurar**.

4.  Na página **Selecionar um atendedor automático de UM**, selecione o atendedor automático que você deseja usar como um fallback de DTMF atendedor automático e clique em **Salvar**.


> [!IMPORTANT]
> Você deve primeiro fala habilita o atendedor automático antes que você pode procurar um atendedor automático de fallback de DTMF que tenha configurado.



## Usar o Shell para configurar um atendedor automático habilitado para fala com um atendedor automático de fallback de DTMF

Este exemplo configura um atendedor automático de UM chamado `MySpeechEnabledAA` para usar um atendedor automático de fallback de DTMF chamado `MyDTMFAA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

