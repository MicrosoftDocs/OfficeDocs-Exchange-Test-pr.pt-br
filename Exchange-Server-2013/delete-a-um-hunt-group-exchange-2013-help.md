---
title: 'Excluir um grupo de busca de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Excluir um grupo de busca de Unificação de mensagens
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50556145
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Excluir um grupo de busca de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-05_

Depois de excluir um grupo de busca de UM, o gateway IP da UM associado ao grupo de busca de UM não servirá ou atenderá as chamadas de entrada. Se ao excluir o grupo de busca de UM, não deixar nenhum grupo de busca de UM configurados no gateway IP da UM, o gateway IP da UM não poderá gerenciar ou processar as chamadas da UM.

Para tarefas adicionais relacionadas a grupos de busca de UM, consulte [Procedimentos de grupo de busca de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-group-procedures).


> [!WARNING]
> Se desejar alterar as configurações do grupo de busca de UM, será necessário excluir o grupo de busca e criar outro grupo de busca com as configurações adequadas.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Busca de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um grupo de busca de UM foi criado. Para obter etapas detalhadas, consulte [Criar um grupo de busca de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-hunt-group).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para excluir um grupo de busca de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, clique no plano de discagem de UM que você deseja alterar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Grupos de Busca de UM**, selecione o grupo de busca que deseja excluir e, na barra de ferramentas, clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  Na página **Aviso**, clique em **Sim**.

## Usar o Shell para excluir um grupo de busca de UM

Este exemplo exclui um grupo de busca de UM chamado `MyUMHuntGroup`.

    Remove-UMHuntGroup -identity MyUMHuntGroup

