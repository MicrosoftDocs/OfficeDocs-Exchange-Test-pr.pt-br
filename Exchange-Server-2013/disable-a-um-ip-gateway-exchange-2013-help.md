---
title: 'Desabilitar um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Desabilitar um gateway IP de UM
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 50487095
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar um gateway IP de UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-13_

Por padrão, quando você cria um gateway IP de Unificação de mensagens (UM), o status de UM gateway IP está habilitado. Depois que o gateway IP de UM é criado, você pode desabilitar a operação do gateway, definindo seu status como desabilitada. Depois de desabilitar o gateway IP de UM, o gateway IP (VoIP), VoIP IP Private Branch eXchange (PBX) ou controlador de borda de sessão (SBC) que ele tenha configurado para usar não são mais pode processar chamadas de Unificação de mensagens de entrada.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateway-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que um gateway IP de UM foi criado e está habilitado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md) e [Habilitar um gateway IP de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/enable-um-ip-gateway).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para desabilitar um gateway IP de UM

1.  No EAC, navegue até **Unificação de mensagens** \> **Gateways IP de UM**, selecione o gateway IP de UM que você deseja desabilitar e, em seguida, clique **na seta para baixo**![Ícone Seta para baixo](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Ícone Seta para baixo").

2.  Na página **Aviso**, clique em **Sim**.

## Use o Shell para desabilitar um gateway IP de UM

Este exemplo desabilita um gateway IP de UM chamado `MyUMIPGateway` e impede que ele aceite chamadas de entrada de um gateway VoIP, IP PBX ou SBC.

    Disable-UMIPGateway -Identity MyUMIPGateway

Este exemplo desabilita um gateway IP de UM chamado `MyUMIPGateway` e desconecta todas as chamadas em andamento imediatamente.

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

