---
title: 'Permitir que as chamadas de saída nos gateways IP de UM: Exchange 2013 Help'
TOCTitle: Permitir que as chamadas de saída nos gateways IP de UM
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 50486572
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que as chamadas de saída nos gateways IP de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-13_

Você pode habilitar chamadas de saída para um gateway IP de Unificação de mensagens (UM) se chamadas de saída tiverem sido desativadas. Quando você seleciona a opção **Permitir chamadas de saída por meio deste gateway IP de UM** nas propriedades para gateway IP de UM, você pode configurar o gateway IP de UM para aceitar e enviar as chamadas de saída para um Voice através do gateway IP (VoIP), Private Branch eXchange (PBX) habilitado para o protocolo de iniciação de sessão (SIP), IP PBX ou controlador de borda de sessão (SBC). Embora as **Permitir chamadas de saída por meio deste gateway IP de UM** determina se o gateway IP de UM é capaz de iniciar chamadas de saída para usuários, não afeta as transferências de chamada ou chamadas recebidas por um gateway VoIP, PBX habilitado para SIP, IP PBX ou SBC.

*Outdialing* é o termo usado para descrever uma situação na qual um usuário em um plano de discagem de UM inicia uma chamada para um usuário habilitado em outro plano de discagem ou para um número de telefone externo.

Para permitir a discagem externa para usuários habilitados para UM, você deve:

  - Verifique se que o gateway IP de UM permite que as chamadas de saída.

  - Crie grupos de regras de discagem, criando a regra de discagem associado ao gateway IP de UM do plano de discagem de entradas em UM.

  - Adicione que os grupos de regras de discagem correto à lista de restrições de discagem em **autorização de discagem** em UM plano de discagem, atendedor automático ou política de caixa de correio de Unificação de mensagens.

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

## Usar o EAC para habilitar chamadas de saída para um gateway IP de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Gateway IP de UM**, marque a caixa de seleção ao lado de **Permitir chamadas de saída por meio deste gateway IP de UM**.

3.  Clique em **Salvar**.

## Use o Shell para habilitar chamadas de saída para um gateway IP de UM

Este exemplo habilita as chamadas de saída em um gateway IP de UM chamado `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true

