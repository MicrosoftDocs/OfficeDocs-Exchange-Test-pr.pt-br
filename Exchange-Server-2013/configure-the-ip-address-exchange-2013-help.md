---
title: 'Configurar o endereço IP: Exchange 2013 Help'
TOCTitle: Configurar o endereço IP
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 50485036
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o endereço IP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-11_

Antes de criar um gateway IP de Unificação de Mensagens (UM), você precisará definir primeiro o endereço IP ou o FQDN (nome de domínio totalmente qualificado) no gateway VoIP, no PBX IP ou no SBC (controlador de borda da sessão) que você estiver usando. Em seguida, ao criar o gateway IP de UM, defina o endereço IP ou o FQDN. Você pode alterar o endereço IP ou o FQDN depois.

É possível configurar o endereço IP ou o FQDN usando o EAC ou o Shell. No EAC, a caixa **Endereço** na página **Gateway IP da UM** pode aceitar um endereço IP IPv4, um endereço IPv6 ou um FQDN. Você pode também usar o parâmetro *Address* no cmdlet **Set-UMIPGateway** no Shell para definir um endereço IP IPv4, um endereço IPv6 ou um FQDN. Depois de criar um gateway IP da UM com um FQDN, você deverá criar os registros HOST A apropriados na zona de pesquisa direta do DNS. Se a configuração do DNS para o gateway IP de UM for alterada, desabilite e habilite o gateway IP de UM para garantir que suas informações de configuração sejam atualizadas corretamente.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o endereço IP em um gateway IP de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Gateway IP e UM**, na caixa **Endereço** , digite o endereço IP do gateway VoIP, do PBX IP ou do SBC.

3.  Clique em **Salvar** para salvar as alterações.


> [!IMPORTANT]
> Se você usar um FQDN em vez de um endereço IP no gateway IP da UM, verifique se foram criados registros DNS corretos.



## Use o Shell para configurar o endereço IP em um gateway IP de UM

Esse exemplo configura um gateway IP de UM, denominado `MyUMIPGateway`, com um endereço IP 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Esse exemplo configura um gateway IP de UM, denominado `MyUMIPGateway`, com um endereço IP 10.10.10.10 e recebendo solicitações de SIP na porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

Este exemplo impede que o gateway IP de UM com o nome `MyUMIPGateway` aceite chamadas de entrada e saída, define um endereço IPv6 e permite que o gateway IP de UM use endereços IPv4 e IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

