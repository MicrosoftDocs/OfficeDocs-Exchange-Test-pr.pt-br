---
title: 'Integração com a Unificação de MENSAGENS do sistema de telefone: Exchange 2013 Help'
TOCTitle: Integração com a Unificação de MENSAGENS do sistema de telefone
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50556286
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Integração com a Unificação de MENSAGENS do sistema de telefone

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Para implantar com êxito a Unificação de mensagens (UM), você deve ter uma boa compreensão dos conceitos de telefonia básica e componentes de telefonia. Depois que você compreender as Noções básicas de telefonia, é possível integrar a Unificação de MENSAGENS em uma organização do Exchange. Componentes e conceitos básicos incluem o seguinte:

  - Redes comutadas e comutação de pacotes

  - PBX (Central Privada de Comutação Telefônica)

  - PBX IP

  - Voice over Internet Protocol (VoIP)

  - Gateways VoIP

Em um local, híbrida ou ambiente Office 365, conectando e configurar os componentes de telefonia necessários é a etapa de mais complexa e importante na implantação com êxito a Unificação de MENSAGENS, com ou sem o Lync Server Enterprise Voice. Você precisará conectar e configurar gateways VoIP, avançados gateways VoIP, PBXs, IP PBXs e controladores de borda de sessão (SBCs) para uma rede de telefonia tradicional e se conectar a uma rede de telefonia se vai usar Microsoft Lync Server e Unificação de MENSAGENS.

Planejar e implantar uma nova implantação da UNIFICAÇÃO de mensagens ou atualizando um sistema de correio de voz herdado pode significar desafios para as organizações. Exige conhecimento significativo sobre VoIP gateways, PBXs, IP PBXs, Microsoft Lync Server e Unificação de mensagens. Dependendo da sua experiência técnica com sistemas de correio de voz e do Exchange, talvez você queira obter a assistência de uma especialista em Unificação de mensagens. Uma especialista em Exchange Unified Messaging ajudará a certificar-se de que haja uma transição suave de um sistema de correio de voz herdado ou de terceiros para Unificação de mensagens do Exchange. Para obter mais informações sobre como entrar em contato com uma especialista em Unificação de mensagens, consulte [Microsoft Exchange Server 2013 Unified Messaging (UM) especialistas](http://go.microsoft.com/fwlink/p/?linkid=262708).

## Integrando a sua rede de telefonia

A Unificação de mensagens requer que você integre sua implantação do Exchange Server com a sua rede de telefonia existente ou integrar a Unificação de MENSAGENS com o Microsoft Lync Server para sua organização. Para implantar e gerenciar o correio de voz da Unificação de MENSAGENS com êxito, você precisará fazer uma análise cuidadosa da sua infra-estrutura de telefonia existente ou em sua implantação do Microsoft Lync Server Enterprise Voice e conclua as etapas de planejamento necessárias.

## Gateways VoIP

Quando você estiver implantando a Unificação de MENSAGENS em uma organização do Exchange, você deve instalar, implantar e configurar um único ou vários gateways de VoIP para se conectar ao PBXs em sua rede de telefonia, ou instalar, implantar e configurar habilitados para SIP Session Initiation Protocol ou IP PBXs.

Um gateway VoIP é um dispositivo de hardware de terceiros que se conecta a um PBX herdado à sua rede local. O gateway VoIP permite que o sistema PBX se comunicar com os servidores do Exchange em sua organização.

Unificação de MENSAGENS depende da capacidade do gateway de VoIP para traduzir ou converter multiplexação de divisão de tempo (TDM) ou baseada em circuitos comutados protocolos com base, como ISDN e QSIG de um PBX para protocolos baseado em VoIP ou IP, como SIP, protocolo de transporte em tempo real (RTP) ou t. 38 para transporte de Fax em tempo real. O gateway de VoIP é integral para a funcionalidade e a operação da UNIFICAÇÃO de mensagens. Também pode se conectar o gateway VoIP para sistemas de PBX que usam de VoIP, em vez de baseada em circuitos comutados protocolos PSTN (rede) telefônica pública comutada.

Escolhendo o correto VoIP gateway, IP PBX, habilitados para SIP PBX ou SBC é a primeira parte da integração de sua rede de telefonia com UM. Você deve configurar esses dispositivos para trabalhar com a Unificação de MENSAGENS. No local e híbrido implantações, você precisa implantar os servidores de acesso para cliente e caixa de correio necessários e criar e configurar todos os componentes necessários de Unificação de MENSAGENS. Para Office 365 com caixa postal hospedada, você não estiver necessárias para instalar e configurar qualquer servidor. Os componentes permitem que você fazer a conexão do seu telefonia, rede comutada de circuito em sua rede IP de dados e habilitar a caixa postal para os usuários em sua organização. Para obter detalhes e dispositivos de telefonia com suporte, consulte os seguintes recursos:

  - [Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Notas de configuração para controladores de borda de sessão suportados](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

A Unificação de mensagens pode usar o Microsoft Lync Server para combinar mensagens de voz, mensagens instantâneas, presença avançada, conferência de áudio/vídeo e email em uma experiência de comunicação familiar e integrada. Fornecer recursos do Enterprise Voice aos usuários em sua organização, integrando a Unificação de MENSAGENS e Microsoft Lync Server tem os seguintes benefícios:

  - Notificações de presença avançadas entre vários aplicativos que mantém os usuários informados da disponibilidade dos contatos.

  - Integração de mensagens instantâneas, voz mensagens, conferência, email e outros modos de comunicação, que permite que os usuários selecionem o modo mais apropriado para a tarefa. Os usuários também podem alternar de um modo para outro conforme necessário.

  - Disponibilidade de alternativas de comunicação de qualquer local onde uma conexão à Internet esteja disponível.

  - Um cliente inteligente Microsoft Lync) para telefonia, mensagens instantâneas e conferência.

  - Continuidade da experiência do usuário entre diversos dispositivos.

As alças de componente UM do Exchange roteamento de voz roteamento entre o Lync Server e Exchange servidores para integrar o Lync Server com os recursos de Unificação de mensagens de email. O Exchange UM componente de roteamento encontrado no Lync Server também trata do reencaminhamento de caixa postal no PSTN se os servidores do Exchange não estão disponíveis. Se você tiver o Enterprise Voice implantado em sites de filiais e esses sites não têm uma WAN resiliente vincular a um site central, um aparelho de filial persistente que ser implantado no site da filial fornece caixa postal para usuários de filiais, se um link WAN cair. Quando o link de WAN não estiver disponível, o aparelho de filial persistente faz o seguinte:

  - Faz um novo roteamento chamadas não respondidas sobre o PSTN para um servidor do Exchange no site central.

  - Fornece a capacidade de um usuário para recuperar mensagens de voz sobre o PSTN.

  - Coloca em fila notificações de chamadas perdidas e as carrega-los ao servidor do Exchange quando o link de WAN for restaurado.

Para obter mais informações sobre o Microsoft Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).


> [!WARNING]
> Quando você estiver integrando a Unificação de mensagens e o Lync Server em um local ou implantação híbrida, chamada perdida notificações não estão disponíveis para usuários que têm uma caixa de correio localizada no Exchange 2007 ou caixa de correio do Exchange 2010 servidores. Uma notificação de chamada perdida é gerada quando um usuário se desconecta antes que a chamada será enviada para um servidor de caixa de correio.


