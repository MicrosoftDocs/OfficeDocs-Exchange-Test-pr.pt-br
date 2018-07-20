---
title: 'Supervisor de fax para UM do Exchange: Exchange 2013 Help'
TOCTitle: Supervisor de fax para UM do Exchange
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52058461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supervisor de fax para UM do Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Microsoft Unified Messaging (UM) depende de soluções de parceiros de fax certificados para a funcionalidade avançada de fax, como fax de saída ou roteamento de fax. Por padrão, os usuários não são configurados para permitir mensagens de fax de entrada ao ser entregue a um usuário habilitado para UM. Servidores Exchange enviam as solicitações de fax para uma solução de parceiro de fax de certificados. Servidor do parceiro de fax recebe os dados de fax e depois enviá-la à caixa de correio do destinatário em uma mensagem de email com o fax incluído como um anexo. tif. Para obter detalhes, consulte [Permitir que os usuários de email de voz receber faxes](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md).


> [!IMPORTANT]
> Recomendamos que todos os clientes que planejam implantar a Unificação de mensagens obtenham a assistência de uma especialista em Unificação de mensagens. Uma especialista em Unificação de mensagens ajuda a garantir que haja uma transição suave para Unificação de mensagens de um sistema de correio de voz herdado. Realizando uma nova implantação ou atualizando um sistema de correio de voz herdado exige conhecimento significativo sobre PBXs e Unificação de mensagens. Para obter mais informações sobre como entrar em contato com uma especialista em Unificação de mensagens, consulte o <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) especialistas</A> ou <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft identifique para Unificação de mensagens</A>.



## Exchange Unified Messaging programa de parceiro de Fax

Para se tornar um parceiro de fax certificado para a interoperabilidade com o UM do Exchange, o parceiro deve implementar os requisitos contidos na especificação de interoperabilidade de parceiro de Fax e a solução de fax deve ser certificada por um fornecedor de certificação independente. Para obter mais informações sobre um produto de fax para trabalhar com a Unificação de mensagens do Exchange de certificação, envie uma solicitação para [Parceiros de Fax para Unificação de mensagens](mailto:fax-part@microsoft.com).

## Soluções de parceiros de fax certificadas quanto a interoperabilidade com o Unified Messaging

Se você já implantou Unificação de mensagens do Exchange e estiver procurando por um parceiro de fax que pode permitir que os faxes de entrada para sua organização, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/p/?linkid=190238). Esses fornecedores de software foram certificadas como interoperável com o Exchange Server e incluem soluções de certificados de software para Unificação de mensagens.

## Suporte de IP PBX, gateway de mídia e VoIP

Configurar corretamente os gateways VoIP para sua organização é uma tarefa de implantação de dificultado que deve ser concluída para implantar com êxito o Exchange Unified Messaging com faxes de entrada. Para ajudar a responder perguntas e obter as informações mais atualizadas de configuração de gateway VoIP, consulte [Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md). [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) fornece notas de configuração de gateway VoIP e arquivos que você deve ter para configurar corretamente a sua organização VoIP gateways, PBXs IP e SBCs para trabalhar com a Unificação de mensagens do Exchange.

Teste de interoperabilidade da Unificação de mensagens do Exchange com gateways VoIP é agora integrado com o Microsoft programa de interoperabilidade aberta do Unified Communications. Para obter mais informações, consulte [Microsoft Unified Communications programa de interoperabilidade aberta](http://go.microsoft.com/fwlink/p/?linkid=140722).

O programa de qualificação do [Microsoft Unified Communications programa de interoperabilidade aberta](http://go.microsoft.com/fwlink/p/?linkid=140722) para gateways VoIP e PBXs IP garante que os clientes têm uma instalação sem interrupções e o suporte a enfrentar ao estejam usando IP PBXs e gateways de telefonia qualificado com Microsoft software de comunicação unificada.


> [!IMPORTANT]
> Enviar e receber faxes usando t. 38 ou g. 711 não não suportado em um ambiente onde a Unificação de mensagens e Communications Server 2007 R2 ou Microsoft Lync Server são integrados.



## Implantando e configurando fax

Unificação de MENSAGENS encaminha chamadas de fax de entrada para uma solução de parceiro de fax dedicado, que, em seguida, estabelece a chamada de fax com o remetente de fax e recebe o fax em nome do usuário habilitado para UM. No entanto, para permitir que os usuários habilitados receber mensagens de fax em suas caixas de correio, você deve configurar o servidor de parceiro de fax e, em seguida, configure os planos de discagem de Unificação de MENSAGENS, diretivas de caixa de correio UM e habilitar usuários habilitados receber faxes. Para obter detalhes, consulte [Configurando o envio de fax de entrada](setting-up-incoming-faxing-exchange-2013-help.md).

