---
title: 'Configurar um nome de domínio totalmente qualificado: Exchange 2013 Help'
TOCTitle: Configurar um nome de domínio totalmente qualificado
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 50486390
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um nome de domínio totalmente qualificado

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-09_

Você pode configurar um gateway IP de Unificação de mensagens (UM) com um endereço IP ou um nome de domínio totalmente qualificado (FQDN). Quando você cria um gateway IP de UM, você deve definir o endereço IP ou o FQDN configurado no gateway VoIP, IP PBX ou controlador de borda de sessão (SBC) que você está usando. Você pode alterar o endereço IP ou FQDN depois que o gateway IP de UM é criado.

Se você criar um gateway IP de UM usando um FQDN, você deve criar os registros de HOST (A) apropriados na sua zona de pesquisa direta de DNS. Se você criar um gateway IP de UM usando um FQDN e a configuração de DNS para o gateway IP de UM é alterada, você deve desabilitar e habilitar o gateway IP de UM certificar-se de que suas informações de configuração são atualizadas corretamente.

Se você deseja usar mutual Transport Layer Security (TLS mútuo) entre um gateway IP de UM e um plano de discagem operacional em um SIP modo protegido ou protegido, você deve configurar UM gateway IP com um FQDN. Você também deve configurá-lo para ouvir na porta 5061 e verificar se o gateway de VoIP, IP PBX, ou o SBC também tiver sido configurado para escutar solicitações TLS mútuas na porta 5061. Para configurar um gateway IP de UM, execute o seguinte comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar um FQDN

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**, selecione o gateway IP da UM que deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **gateway IP de UM**, em **endereço**, digite o FQDN do gateway de VoIP, PBX habilitado para SIP, IP PBX ou SBC.

3.  Clique em **Salvar**.


> [!IMPORTANT]
> Quando você usa um FQDN, em vez de um endereço IP no gateway IP de UM, verifique se que os registros DNS corretos foram criados.



## Use o Shell para configurar um FQDN

Este exemplo configura um gateway IP de UM chamado `MyUMIPGateway` com um FQDN chamado voipgateway.contoso.com.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

Este exemplo configura um gateway IP de UM chamado `MySBC` com um FQDN de sbc.contoso.com e escuta de solicitações SIP na porta TCP 5061.

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

