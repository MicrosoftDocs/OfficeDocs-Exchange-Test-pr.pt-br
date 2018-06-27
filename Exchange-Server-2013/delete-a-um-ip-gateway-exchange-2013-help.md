---
title: 'Excluir um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Excluir um gateway IP de UM
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 50485627
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Excluir um gateway IP de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-21_

Quando você exclui um gateway IP de Unificação de Mensagens (UM), servidores do Exchange não podem mais aceitar chamadas de voz de gateway VoIP, central privada de comutação telefônica (PBX) habilitada para protocolo SIP, PBX IP ou controlador de borda de sessão (SBC) associado com o gateway IP de UM.


> [!IMPORTANT]
> Você só deve excluir um gateway IP da UM quando entender plenamente as implicações de desabilitar as comunicações com um gateway VoIP, PBX IP ou SBC.



Para tarefas adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para excluir um gateway IP da UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja excluir e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

2.  Na página **Aviso**, clique em **Sim**.

## Usar o Shell para excluir um gateway IP de UM

Este exemplo exclui o gateway IP de UM com o nome `MyUMIPGateway`.

    Remove-UMIPGateway -Identity MyUMIPGateway

