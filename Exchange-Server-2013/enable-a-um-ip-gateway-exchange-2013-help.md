---
title: 'Habilitar um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Habilitar um gateway IP de UM
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 50485177
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar um gateway IP de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-05_

Por padrão, quando um gateway IP da Unificação de Mensagens (UM) é criado, seu status é definido como habilitado. Porém, pode ser necessário desabilitar o gateway IP da UM para deixá-lo offline e não permitir que ele receba chamadas de entrada ou saída. Após criar um gateway IP da UM, você pode controlar sua operação e funcionalidade definindo sua variável de status como habilitado ou desabilitado.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se o gateway IP da UM foi criado e desabilitado. Para instruções detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar um gateway IP da UM

1.  No EAC, navegue até \> **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja habilitar e clique na **Seta para cima**![Ícone Seta para cima](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Ícone Seta para cima").

2.  Na página **Aviso**, clique em **Sim**.

## Usar o Shell para habilitar um gateway IP da UM

Este exemplo habilita um gateway IP da UM chamado `MyUMIPGateway`.

    Enable-UMIPGateway -Identity MyUMIPGateway

