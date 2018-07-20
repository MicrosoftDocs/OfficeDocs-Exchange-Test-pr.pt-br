---
title: 'Impedir que o indicador de espera de mensagem (MWI) em um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Impedir que o indicador de espera de mensagem (MWI) em um gateway IP de UM
ms:assetid: 7af6d094-199f-4134-a25d-9fc7e9c05fe1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673536(v=EXCHG.150)
ms:contentKeyID: 50485982
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedir que o indicador de espera de mensagem (MWI) em um gateway IP de UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Você pode impedir notificações de caixa postal aos usuários para chamadas recebidas por um gateway IP de Unificação de mensagens (UM). Se você habilitar essa configuração, o gateway IP de UM pode receber e enviar mensagens SIP notificar para usuários. Indicador de espera de mensagem (MWI) é habilitado por padrão e permite que a mensagem aguardando as notificações sejam enviadas aos usuários, mas você pode desativá-la dependendo das suas necessidades.

Um indicador de espera de mensagem notifica o usuário sobre uma mensagem de voz novos ou não ouvidas. Ela será exibida na caixa de entrada nos clientes como Outlook e Outlook Web App. Ele também pode ser uma mensagem de texto (SMS) enviada a um telefone celular registrado, uma chamada de saída feita a partir de um servidor Exchange para um número que é configurado para tocar novas mensagens ou uma lâmpada iluminada no telefone de área de trabalho do usuário.


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

## Usar o EAC para impedir que o indicador de espera de mensagem

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Gateway IP de UM**, desmarque a caixa de seleção ao lado de **mensagem em permitir indicador de espera**.

3.  Clique em **Salvar**.

## Use o Shell para impedir que o indicador de espera de mensagem

Este exemplo impede que a mensagem aguardando indicador apareça para os usuários que estão associados com o gateway IP de UM chamado `MyUMIPGateway` com um endereço IP 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $false

