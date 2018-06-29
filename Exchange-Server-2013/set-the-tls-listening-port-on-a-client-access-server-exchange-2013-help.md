---
title: 'Definir a porta de escuta TLS em um servidor de acesso para cliente: Exchange 2013 Help'
TOCTitle: Definir a porta de escuta TLS em um servidor de acesso para cliente
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50556313
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir a porta de escuta TLS em um servidor de acesso para cliente

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-17_

Você pode configurar a porta de segurança de camada de transporte (TLS) que é usada para escutar solicitações SIP em um servidor de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada. Por padrão, quando você instala um servidor de acesso para cliente, o número de porta de escuta SIP TLS é definido como 5061.

Você pode ter que configurar a porta de escuta TLS como 5061 se desejar:

  - Defina a configuração de segurança de VoIP em um plano de discagem de UM como SIP Protegido.

  - Defina a configuração de segurança de VoIP em um plano de discagem de UM como Protegido.

  - Integrar ao MicrosoftOffice Communications Server 2007 R2 ou ao Microsoft Lync Server.

  - Use mutual Transport Layer Security (TLS mútuo) para criptografar dados de rede entre os servidores de acesso para cliente, os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange e gateways VoIP, PBXs Private Branch eXchanges () habilitados para o protocolo de iniciação de sessão (SIP), IP PBXs ou controladores de borda de sessão (SBCs).

Se você quiser usar o TLS mútuo entre um gateway IP de UM e um plano de discagem operando em modo SIP protegido ou protegido, quando você cria UM novo gateway IP, você deve configurá-lo com um nome de domínio totalmente qualificado (FQDN) e, em seguida, configure o gateway IP de UM para ouvir na porta TLS 5061. Você deve também verificar que quaisquer gateways VoIP, PBXs habilitados para SIP, IP PBXs, ou SBCs também foram configurados para escutar solicitações TLS mútuas na porta 5061.

Você só pode configurar o servidor de Acesso para Cliente em portas TCP e TLS. Você não pode configurar as portas para um servidor de Caixa de Correio Exchange 2013. No entanto, você pode usar o cmdlet **Set-UMService** para configurar as portas de escuta TCP e TLS para os servidores de UM do Exchange 2010.

Para conhecer tarefas adicionais relacionadas a servidores de Unificação de Mensagens e de Acesso para Cliente, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Acesso para Cliente (servidor de roteamento de chamadas de UM)", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se você instalou corretamente os servidores de Acesso para Cliente e de Caixa de Correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar a porta de escuta TLS em um servidor de acesso para cliente

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na exibição de lista, selecione o servidor Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **configurações de UM serviço**, em **porta de escuta TLS**, digite o número da porta TLS e clique em **Salvar**.

## Usar o Shell para configurar a porta de escuta TLS em um servidor de acesso para cliente

Este exemplo define a porta de escuta TLS em um servidor de acesso para cliente chamado `MyClientAccessServer` para 5561.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561

