---
title: 'Permitir o indicador de espera de mensagem (MWI) em um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Permitir o indicador de espera de mensagem (MWI) em um gateway IP de UM
ms:assetid: 5667e37c-48c6-4659-9dc9-94b1dd8ba232
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd297995(v=EXCHG.150)
ms:contentKeyID: 50485619
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o indicador de espera de mensagem (MWI) em um gateway IP de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-23_

Você pode permitir ou impedir notificações de caixa postal aos usuários para chamadas recebidas por um gateway IP de Unificação de Mensagens (UM). Se essa configuração for habilitada, o gateway IP de UM poderá receber e enviar mensagens SIP NOTIFY aos usuários. O indicador de mensagem em espera é habilitado por padrão e permite que notificações de mensagens em espera sejam enviadas aos usuários, mas você pode desativá-lo conforme suas necessidades.

Um indicador de espera de mensagem notifica um usuário sobre uma mensagem de voz nova ou não ouvida. Ele é exibido na Caixa de entrada em clientes como o Outlook e o Outlook Web App. Também pode ser uma mensagem de texto (SMS) enviada a um celular registrado, uma chamada de saída feita em um servidor do Exchange para um número configurado para a reprodução de novas mensagens ou pode ser uma luz acesa no telefone de mesa de um usuário.


> [!TIP]
> As notificações de MWI também podem ser habilitadas e desabilitadas em uma política de caixa de correio da UM para um grupo de usuários.



Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para permitir o Indicador de Espera de Mensagem

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Gateway IP de UM**, desmarque a caixa de seleção ao lado de **Permitir indicador de mensagem em espera**.

3.  Clique em **Salvar**.

## Usar o Shell para permitir o Indicador de Espera de Mensagem

Este exemplo permite que o indicador de espera de mensagem seja exibido aos usuários associados ao gateway IP de UM denominado `MyUMIPGateway` com um endereço IP de 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $true

