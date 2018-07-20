---
title: 'Configure a porta de escuta: Exchange 2013 Help'
TOCTitle: Configure a porta de escuta
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50556163
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configure a porta de escuta

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode configurar a porta TCP que é usada para escutar as solicitações de protocolo SIP em um gateway IP da Unificação de Mensagens (UM). Por padrão, quando você cria um gateway IP da UM, o número da porta de escuta TCP do SIP é definido como 5060. A porta de escuta TCP do SIP não pode ser configurada ou alterada usando o EAC. Você deve configurar a porta de escuta de protocolo SIP TCP usando o cmdlet **Set-UMIPGateway**.

Pode ser necessário configurar o número da porta de escuta TCP como 5061 se desejar:

  - Defina a configuração de segurança de VoIP em um plano de discagem de UM como SIP Protegido.

  - Defina a configuração de segurança de VoIP em um plano de discagem de UM como Protegido.

  - Integrar ao MicrosoftOffice Communications Server 2007 R2 ou ao Microsoft Lync Server.

  - Use o protocolo TLS mútuo para criptografar os dados de rede entre servidores do Exchange e um gateway VoIP, PBX (Private Branch eXchange) habilitado para SIP, PBX IP ou SBC (Controlador de borda de sessão).

Se quiser usar o protocolo TLS mútuo entre um gateway IP de UM e um plano de discagem que opera no modo Protegido por SIP ou Protegido, quando você criar esse gateway, será preciso configurá-lo com um FQDN (nome de domínio totalmente qualificado) e usar o Shell para configurar o gateway IP de UM para que escute na porta TCP 5061. É preciso também verificar se algum gateway VoIP, PBXs habilitados para protocolo SIP, PBXs IP ou SBCs também foram configurados para escutar solicitações de protocolo TLS mútuo na porta 5061.


> [!IMPORTANT]
> Ao criar um gateway IP da UM com um FQDN, você deverá criar os registros HOST (A) apropriados na zona de pesquisa direta do DNS. Se você criar um gateway IP da UM usando um FQDN e a configuração DNS para o gateway IP da UM for alterada, você deverá desabilitar e, em seguida, habilitar o gateway IP da UM para certificar-se de que as informações de configuração do gateway IP da UM estejam atualizadas corretamente.



Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para configurar a porta de escuta TCP

Este exemplo configura um gateway IP da UM chamado `MyUMIPGateway` com FQDN de mTLS.MyUMIPGateway.contoso.com e escuta as solicitações de SIP na porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

Este exemplo configura um gateway IP da UM chamado `MyUMIPGateway` com FQDN de SIPSecured.MyUMIPGateway.contoso.com e escuta as solicitações de SIP na porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

Este exemplo configura um gateway IP da UM chamado `MyUMIPGateway` com FQDN de MyOCSUMIPGateway.contoso.com e escuta as solicitações de SIP na porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

