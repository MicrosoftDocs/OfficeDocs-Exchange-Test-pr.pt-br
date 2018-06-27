---
title: 'Desabilitar as chamadas de saída nos gateways IP de UM: Exchange 2013 Help'
TOCTitle: Desabilitar as chamadas de saída nos gateways IP de UM
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 50486297
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar as chamadas de saída nos gateways IP de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-13_

Você pode habilitar ou desabilitar as chamadas de saída para um gateway IP de Unificação de mensagens (UM). Quando você desmarcar a opção **Permitir chamadas de saída por meio deste gateway IP de UM** nas propriedades para gateway IP de UM, você pode configurar o gateway IP de UM para não aceitar e enviar chamadas de saída para uma voz sobre IP (VoIP) gateway, IP PBX ou sessão controlador de borda (SBC). Embora as **Permitir chamadas de saída por meio deste gateway IP de UM** determina se o gateway IP de UM é capaz de iniciar chamadas de saída para os usuários, ela não afeta as chamadas de entrada de um gateway VoIP, IP PBX ou SBC ou transferências de chamada.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que um plano de discagem UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para desabilitar as chamadas de saída para um gateway IP de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Gateway IP de UM**, desmarque a caixa de seleção ao lado de **Permitir chamadas de saída por meio deste gateway IP de UM**.

3.  Clique em **Salvar**.

## Use o Shell para desabilitar as chamadas de saída para um gateway IP de UM

Este exemplo desativa as chamadas de saída em um gateway IP de UM chamado `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false

