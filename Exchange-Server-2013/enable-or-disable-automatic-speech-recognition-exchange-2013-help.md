---
title: 'Ativar ou desativar o reconhecimento automático de fala: Exchange 2013 Help'
TOCTitle: Ativar ou desativar o reconhecimento automático de fala
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52058469
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar ou desativar o reconhecimento automático de fala

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-12_

Você pode ativar o atendedor automático de Unificação de mensagens (UM) para o reconhecimento automático de fala (ASR). Depois que você fala habilita um atendedor automático de UM, os chamadores podem verbalmente responder a prompts de atendedor automático e mover o sistema de menus do atendedor automático. Por padrão, um atendedor automático não está habilitado para fala quando você criá-lo. Depois que você fala habilita o atendedor automático, os chamadores podem usar apenas os comandos de voz para navegar pelo sistema de menu do atendedor automático e entradas de toque não podem ser usadas.

Embora não seja obrigatório, é recomendável que você configure um Atendedor de automático de fallback de DTMF (Multifreqüência) de tom dual para cada atendedor automático habilitado para fala para que os chamadores podem usar entradas de toque, se o atendedor automático habilitado para fala não reconhecer nem entender as palavras que eles dizem. Se um atendedor automático de fallback de DTMF estiver configurado, os chamadores podem usar entradas de DTMF, também conhecido como entradas de toque para navegar pelo sistema de menu do atendedor automático, um nome de usuário de ortografia ou usar um prompt de menu personalizado. Não recomendamos que você fala habilita um atendedor automático de fallback de DTMF.

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

## Use o EAC para habilitar a fala um atendedor automático

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM que deseja habilitar fala e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendente automático de UM** \> **Geral**, marque a caixa de seleção ao lado de **Configurar o atendedor automático para responder aos comandos de voz** para habilitar o reconhecimento de fala. Para desabilitar o reconhecimento automático de fala, desmarque essa caixa de seleção.

4.  Clique em **Salvar**.

## Use o Shell para habilitar a fala um atendedor automático

Este exemplo habilita a ASR em um atendedor automático de UM chamado `MySpeechEnabled AA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

