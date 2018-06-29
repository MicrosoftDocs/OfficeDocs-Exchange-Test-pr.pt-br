---
title: 'Gateways IP de UM: Exchange 2013 Help'
TOCTitle: Gateways IP de UM
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 50486187
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gateways IP de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2014-06-24_

Um gateway IP de Unificação de Mensagens (UM) representa um gateway VoIP físico, PBX IP ou dispositivo de hardware SBC. Antes que um gateway VoIP, PBX IP ou SBC possa ser usado para responder chamadas de entrada e enviar chamadas de saída para usuários de caixa postal, um gateway IP de UM deve ser criado no serviço de diretório.

**Sumário**

Overview of UM IP gateways

UM IP gateways

IPv6 support for UM IP gateways

Enabling and disabling a UM IP gateway

## Visão geral de gateways IP de UM

Tradicionalmente, *gateway* é um termo que descreve um dispositivo físico que conecta duas redes incompatíveis. Com a Unificação de Mensagens do Exchange e outras soluções de unificação de mensagens, o gateway VoIP é usado para converter entre a Rede Telefônica de Comutação Pública (PSTN)/Multiplex de Divisão de Tempo (TDM) ou rede telefônica baseada em comutação de circuitos e um IP ou rede de dados de comutação de pacotes. Um PBX IP também converte entre uma rede PSTN e uma rede de comutação de pacotes; assim, quando um PBX IP é utilizado, o gateway VoIP não é necessário. Um gateway VoIP só é necessário caso você esteja conectando um dispositivo de hardware PBX herdado à sua implantação de UM.


> [!TIP]
> Uma rede de comutação de pacotes é uma rede em que pacotes (mensagens ou fragmentos de mensagens) são roteados individualmente entre dispositivos como roteadores, comutadores, gateway VoIP, PBXs IP e SBCs. Ela contrasta com uma rede de comutação de circuitos que define uma conexão dedicada entre os dois nós para seu uso exclusivo pela duração da comunicação.



A Unificação de Mensagens do Exchange conta com a capacidade do gateway VoIP de converter TDM ou protocolos baseados em circuitos comutados de telefonia, como Rede Digital de Serviços Integrados (ISDN) ou QSIG, de um PBX para protocolos baseados em VoIP ou IP, como Protocolo de Início de Sessão (SIP), Protocolo de Transporte em Tempo Real (RTP) ou T.38 para transporte de fac-símile em tempo real.

PBXs IP também são usados ao conectar uma rede de telefonia de circuitos comutados a uma rede de dados ou de comutação de pacotes. Eles também são usados para converter protocolos de circuitos comutados para protocolos baseados em VoIP ou IP, como SIP, RTP e RTPC Seguro (SRTP).

Controladores de Borda de Sessão (SBCs) são um tanto diferentes dos gateways VoIP e PBXs IP. Em vez de conectar uma rede com circuitos comutados a uma rede de comutação de pacotes, eles são usados para conectar duas redes de dados por uma rede pública, como a Internet, ou por uma conexão WAN privada. Na Unificação de Mensagens, os SBCs são usados em uma implantação híbrida de UM, na qual a UM usa alguns componentes no local e outros, como caixas de correio, localizados na nuvem.

## Configurações do dispositivo VoIP

Embora haja muitos tipos e fabricantes de PBXs, gateways VoIP, PBXs IP e SBCs, existem basicamente três tipos de configurações de dispositivo VoIP:

  - **PBX IP**   Um dispositivo único que converte entre a rede PSTN/TDM ou de telefonia baseada em circuitos comutados e uma rede IP ou de dados com comutação de pacotes

  - **PBX (herdado) e um gateway VoIP**   Dois componentes distintos que, juntos, convertem entre a rede PSTN/TDM ou de telefonia baseada em circuitos comutados e uma rede IP ou de dados com comutação de pacotes

  - **SBC**   Um ou vários dispositivos que conectam dois tipos de redes baseadas em IP, como uma rede local (LAN) e um datacenter.

Para oferecer suporte à Unificação de Mensagens, um ou ambos os tipos de configurações de dispositivo IP/VoIP são usados ao conectar uma infraestrutura de rede de telefonia a uma infraestrutura de rede de dados ou conectar uma implantação local a uma implantação de UM na nuvem.

## Gateways IP da UM

O gateway IP de UM contém um ou mais grupos de busca de UM e definições de configuração. Grupos de busca de UM são usados para vincular um gateway IP de UM a um plano de discagem de UM. A combinação do objeto de gateway IP de UM e um objeto de grupo de busca de UM estabelece um vínculo entre um gateway VoIP, um IP PBX ou SBC e um plano de discagem de UM. Ao criar vários grupos de busca do UM, você pode associar um gateway IP do UM único com vários planos de discagem do UM.

Depois que você criar um gateway IP de UM, os servidores Exchange vinculados ao gateway IP de UM enviarão uma solicitação de SIP OPTIONS ao gateway VoIP, PBX IP ou SBC para garantir que o dispositivo responda. Se o gateway VoIP, PBX IP ou SBC não responder à solicitação, o servidor Exchange registrará um evento com a ID 1400, declarando que a solicitação falhou. Se isso acontecer, verifique se o gateway VoIP, PBX IP ou SBC está disponível e online, e se a configuração da Unificação de Mensagens está correta.

Um servidor de Caixa de Correio se comunica apenas com gateways VoIP, PBXs IP ou SBCs listados como SIPs confiáveis de mesmo nível. Em alguns casos, se dois gateways VoIP, PBXs IP ou SBCs forem configurados para usar o mesmo endereço IP, um evento com ID 1175 será registrado. A Unificação de Mensagens protege contra solicitações não autorizadas recuperando a URL interna do diretório virtual de serviços Web da Unificação de Mensagens e depois usa a URL para criar a lista de FQDNs para SIPs de mesmo nível confiáveis. Quando dois FQDNs são resolvidos para o mesmo endereço IP, o evento é registrado em log.

## Suporte a IPv6 para gateways IP de UM

O IPv6 (protocolo IP versão 6) é a versão mais recente do protocolo IP. O IPv6 foi projetado para corrigir muitas das deficiências do IPv4, a versão anterior do protocolo IP. Em implantações locais e híbridas do Microsoft Exchange Server 2010, só havia suporte ao IPv6 quando o IPv4 também era usado.

Em implantações locais e híbridas do Exchange 2013, componentes relacionados a UM e serviços de fala são executados somente em servidores de Acesso para Cliente e de Caixa de Correio. Como a arquitetura de UM mudou e agora requer que o Unified Communications Managed API (UCMA) v4.0 dê suporte a IPv4 e IPv6, bem como a outros recursos do Exchange, os servidores de Acesso para Cliente e de Caixa de Correio que têm componentes e serviços de Unificação de Mensagens dão suporte total a redes IPv6 e não exigem o IPv4.

Em implantações locais e híbridas e do Exchange Online, os administradores de UM corporativos e do Exchange Online podem usar IPv6 quando conectarem a UM a dispositivos habilitados para IPv6, incluindo dispositivos como roteadores, gateways IP, PBXs IP e servidores do Microsoft Office Communications Server 2007 R2 e Microsoft Lync. Porém, para interoperabilidade e compatibilidade com versões anteriores, o IPv4 poderá ser usado sem alterações adicionais de configuração se o parâmetro *IPAddressFamily* for definido como `Any` e gateways IP de UM.

A UM do Exchange ainda deve se comunicar diretamente com SIPs de mesmo nível (gateways VoIP, PBXs IP e SBCs) que talvez não tenham suporte a IPv6 em seu software ou firmware. Se eles não tiverem suporte para IPv6, a UM deverá ser capaz de se comunicar diretamente com SIPs de mesmo nível que utilizem IPv4. Para caixas postais hospedadas, a UM se comunica com o equipamento do cliente através de SBCs, do Lync Server 2010 ou do Lync Server 2013. Em ambientes hospedados, clientes que reconhecem o SIP IPv6, como SBCs e servidores Lync, podem ser implantados para lidar com o processo de conversão de IPv6 para IPv4.

Para implantações locais e híbridas, depois que você instalar seus servidores de Acesso para Cliente e Caixa de Correio, bem como para implantações de UM do Exchange Online, será necessário criar gateways IP de UM. Se precisar que seus gateways IP de UM tenham suporte para IPv6, você deverá também:

1.  Criar um novo gateway IP de UM ou configurar um gateway IP de UM existente com um endereço IPv6 para cada um dos gateways IP, PBXs IP ou SBCs presentes em sua rede. Ao criar e configurar os gateways IP de UM necessários, você deverá adicionar o endereço IPv6 ou o FQDN (Nome de domínio totalmente qualificado) para o gateway IP de UM. Se estiver adicionando o FQDN ao gateway IP de UM, você deverá ter criado os registros de DNS corretos para resolver o FQDN de gateway IP de UM para o endereço IPv6. Se tiver um gateway IP de UM existente, você poderá usar o cmdlet **Set-UMIPgateway** para configurar o endereço IPv6 ou o FQDN.

2.  Configure o parâmetro *IPAddressFamily* em cada gateway IP de UM. Para habilitar o gateway VoIP para que aceite pacotes IPv6, você deve definir o gateway IP de UM para aceitar conexões IPv4 e IPv6 ou aceitar somente conexões IPv6, usando o cmdlet **Set-UMIPgateway**.

3.  Após ter configurado seus gateways IP de UM, você deve configurar também os gateways VoIP, os PBXs IP e os SBCs na sua rede para que tenham suporte para IPv6. Para mais detalhes, consulte seu fornecedor de hardware para uma lista de dispositivos que oferecem suporte a IPv6 e como configurá-los corretamente.


> [!TIP]
> A quantidade máxima de gateways IP de UM por plano de discagem é 200. Se você criar mais de 200, o serviço de UM não será iniciado.



## Habilitando e desabilitando um gateway IP de UM

Por padrão, um gateway IP de UM é deixado no estado habilitado após ser criado. No entanto, o gateway IP do UM pode ser habilitado ou desabilitado. Se desabilitar um gateway IP de UM, você poderá configurá-lo para forçar todos os servidores Exchange a abandonar chamadas existentes. Como alternativa, você pode configurá-lo para forçar todos os servidores Exchange associados ao gateway IP de UM a interromper a administração de qualquer chamada nova apresentada pelo gateway VoIP, PBX IP ou SBC.

Se estiver integrando a Unificação de Mensagens ao Office Communications Server R2 ou ao Microsoft Lync Server, você poderá permitir que somente um gateway IP de UM faça chamadas de saída para os usuários e desativar chamadas de saída em todos os outros gateways IP de UM associados a seus planos de discagem do URI do SIP. Use o Shell ou EAC para desabilitar a chamada de saída.

Ao selecionar o gateway IP de UM através do qual as chamadas de saída serão permitidas para implantações locais e híbridas, escolha aquele que provavelmente administrará a maior parte do tráfego. Não permita tráfego de saída por um gateway IP de UM que se conecte a um pool de Diretores do Lync Server. Isso é necessário para garantir que as chamadas de saída enviadas a usuários externos pelo servidor de Caixa de Correio que está executando o serviço de Unificação de Mensagens do Exchange (por exemplo, em situações de uso do recurso Tocar no Telefone) passem de forma confiável pelo firewall corporativo.

