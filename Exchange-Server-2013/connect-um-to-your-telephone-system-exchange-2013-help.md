---
title: 'Conectar UM ao seu sistema telefônico: Exchange 2013 Help'
TOCTitle: Conectar UM ao seu sistema telefônico
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50556241
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectar UM ao seu sistema telefônico

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-30_

Unified Messaging (UM) combina mensagens de voz e mensagens de email em uma caixa de correio que pode ser acessada a partir de vários dispositivos diferentes. Os usuários podem ouvir suas mensagens da caixa postal a partir de seus emails de entrada ou usando o Outlook Voice Access de qualquer telefone.

Quando você estiver implantando a Unificação de mensagens em uma organização do Microsoft Exchange, você deve instalar, implantar e configurar uma única ou vários voz sobre gateways IP (VoIP) para se conectar ao Private Branch eXchanges (PBXs) em sua rede de telefonia ou instalar, implantar e configurar habilitados para SIP Session Initiation Protocol ou IP PBXs. Se você estiver atualizando o seu sistema de caixa postal atual, você vai precisa para implantar os dispositivos que se conectam à rede de telefonia, instalar servidores de caixa de correio e acesso para cliente do Exchange e, em seguida, criar os componentes necessários de Unificação de mensagens que permitem que sua rede de telefonia para se conectar à sua rede de dados. Isso permite que as chamadas de entrada da rede de telefonia para se conectar ao seus gateways VoIP, IP PBXs ou PBXs habilitados para SIP e esses dispositivos para se conectar à sua organização do Exchange.

Se você estiver instalando, implantando e configurando o Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, você não usar gateways VoIP, IP PBXs ou PBXs habilitados para SIP para conectar-se diretamente para Unificação de mensagens do Exchange. Em vez disso, um gateway VoIP e de servidor de mediação do Lync ou um gateway VoIP avançado que tem a funcionalidade de um servidor de mediação e um gateway VoIP permitirá que você se conecte a UM do Exchange. Usuários de Unificação de mensagens que estão habilitados para o Enterprise Voice podem recuperar, ouvir e responder às mensagens de voz e fazer chamadas de saída. Eles também têm acesso a outros recursos relacionados ao Lync, inclusive mensagens instantâneas (IM) e presença, usando um cliente do Lync ou Office Communicator.

As informações a seguir o ajudarão a configurar e implantar a Unificação de mensagens e habilitar os recursos de caixa postal para usuários em sua organização:

  - [Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)   Saiba como conectar os gateways VoIP ou IP PBXs a Unificação de mensagens.

  - [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)   Saiba mais sobre suportados gateways VoIP, IP PBXs e PBXs.

  - [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)  Aprenda a configurar seus gateways VoIP, IP PBXs e PBXs.

