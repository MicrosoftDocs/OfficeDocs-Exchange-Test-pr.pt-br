---
title: 'Serviços de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Serviços de Unificação de mensagens
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50556312
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Serviços de Unificação de mensagens

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-18_

Servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange permitem que você implantar a Unificação de mensagens (UM) e a funcionalidade de caixa postal para usuários em sua organização.

Procurando tarefas de gerenciamento relacionadas aos serviços de Unificação de mensagens? Consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

**Sumário**

Servidores de Acesso para Cliente e de Caixa de Correio

Configurações do servidor

Operação do servidor

## Servidores de Acesso para Cliente e de Caixa de Correio

Em Exchange 2013, as funções de servidor encontrados no Exchange 2007 e Exchange 2010 são combinados em dois tipos de servidores, e todos os componentes ou os serviços essas funções de servidor são executados no mesmo servidor físico ou em dois servidores separados, chamados de acesso para cliente e caixa de correio.

Nesse novo modelo, o servidor de acesso para cliente é responsável por descoberta automática, Secure Sockets Layer (SSL), autenticação, o redirecionamento e proxy. O servidor de acesso para cliente é o ponto de entrada para as chamadas de entrada ou solicitações de protocolo de iniciação de sessão (SIP) para Unificação de mensagens. A lógica de roteamento e SIP REDIRECIONAR é implementado como um serviço que está incluído automaticamente em um servidor de acesso para cliente. Esse serviço é conhecido como o serviço Microsoft Exchange Unified Messaging roteador de chamada. Ele é executado em cada servidor de acesso para cliente em sua organização.

Quando um servidor de acesso para cliente recebe um SIP INVITE para uma chamada de entrada, o serviço Microsoft Exchange Unified Messaging roteador de chamada redireciona a chamada de entrada para o servidor de caixa de correio. Em seguida, um canal de mídia (RTP ou SRTP) é criado entre a VoIP gateway, IP PBX ou sessão controlador de borda (SBC) e o servidor de caixa de correio que hospeda a caixa de correio do usuário. Embora o servidor de acesso para cliente atua como um redirecionador SIP, ele só trata solicitações SIP de gateways VoIP, IP PBXs ou SBCs. Ele não recebe qualquer tráfego de mídia. Somente o tráfego de mídia que usa o RTP ou SRTP é passado entre o servidor de caixa de correio e os pares SIP como gateways VoIP, IP PBXs ou SBCs. Quando você implanta Exchange 2013 e Unificação de mensagens, você precisa configurar seus gateways VoIP, IP PBXs ou SBCs para apontar para os servidores de acesso para cliente que você instalou para que as chamadas recebidas serão roteadas corretamente para Unificação de mensagens.

Em Exchange 2013, o servidor de caixa de correio manipula os mesmos processos de manuseados em Exchange 2007 e Exchange 2010 a função de servidor Unificação de mensagens. O servidor de caixa de correio executa o serviço de Unificação de mensagens do Microsoft Exchange e os processos de trabalho de Unificação de mensagens.

Quando você estiver instalando os servidores de acesso para cliente e caixa de correio e implantação da Unificação de mensagens, você não precisa associar ou adicionar acesso para cliente ou planos de discagem de servidores de caixa de correio para Unificação de mensagens. Servidores de acesso para cliente e caixa de correio atender a todas as chamadas recebidas e usar os planos de discagem de Unificação de mensagens para localizar usuários.

No entanto, se você estiver integrando a Unificação de mensagens com o Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, o SIP e os canais de mídia RTP ou SRTP para chamadas de entrada são manipulados pelo servidores do Lync e o servidor de caixa de correio. Em um ambiente integrado do Lync, você não precisa gateways VoIP, IP PBXs ou SBCs. Lync, o servidor de caixa de correio que está executando o serviço de Unificação de mensagens do Microsoft Exchange parece com um servidor de UM Exchange 2010. O servidor de caixa de correio e o servidor de acesso para cliente são considerados colegas confiáveis porque os dois servidores devem ser adicionados a um plano de discagem do SIP. Lync roteia a chamada de entrada usando o componente de roteamento de entrada, que utiliza o SIP para se comunicar com o servidor de acesso para cliente e, em seguida, rotear a chamada para um servidor de caixa de correio.

Voltar ao início

## Configurações do servidor

Em Exchange 2013, todos os componentes de Unificação de mensagens e definições de configuração que é aplicado a um único computador executando a função de servidor Unificação de mensagens no Exchange 2010 ainda estão disponíveis. No entanto, alguns desses componentes e definições de configuração são encontrados em um servidor de acesso para cliente e outros estão disponíveis em um servidor de caixa de correio. Em alguns casos, a mesma configuração está disponível em ambos. A lista a seguir mostra os parâmetros e as configurações que estão disponíveis em um servidor de acesso para cliente e um servidor de caixa de correio.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \< Int32 \>\]

  - \[-SipTcpListeningPort \< Int32 \>\]

  - \[-SipTlsListeningPort \< Int32 \>\]

  - \[-Status \< habilitado | Desabilitado | NoNewCalls \>\]

  - \[-UMStartupMode \< TCP | TLS | Dual \>\]

Para o servidor de caixa de correio, você usará o **Set-UMService**, **Get-UMService**, **Enable-UMService**e **Disable-UMService** cmdlets para exibir ou configurar as propriedades UM para o serviço de Unificação de mensagens do Microsoft Exchange. Um conjunto diferente de cmdlets, **Set-UMCallRouterSettings** e **Get-UMCallRouterSettings**, são usados para exibir ou configurar as propriedades do serviço Microsoft Exchange Unified Messaging roteador de chamadas em um servidor de acesso para cliente. Isso garante que o existente **Get-UMServer**, **Set-UMServer**, **Enable-UMServer**e **Disable-UMServer** cmdlets do Exchange 2007 e Exchange 2010 funcionará em uma implantação de coexistência com servidores de caixa de correio Exchange 2013. Isso também garante que os cmdlets funcionará quando os servidores de acesso para cliente e caixa de correio estão instalados nos computadores mesmos ou diferentes.

Voltar ao início

## Operação do servidor

Quando os servidores de acesso para cliente e caixa de correio estão instalados, elas são automaticamente habilitadas para que eles podem responder a entrada e rotear mensagens de caixa postal para os destinatários pretendidos em sua organização Exchange e chama de voz de saída.

Você pode permitir que o serviço de Unificação de mensagens do Microsoft Exchange em um servidor de caixa de correio ou o serviço Microsoft Exchange Unified Messaging roteador de chamadas em um servidor de acesso para cliente para atender chamadas novas ou impedir isso. Por padrão, um servidor de caixa de correio ou de acesso para cliente está em um estado habilitado depois que ele é instalado. Quando você estiver definindo o servidor de caixa de correio ou de acesso para cliente para aceitar entrada chamadas de voz, fax, atendedor automático e Outlook Voice Access, você pode usar o cmdlet **Set-ServerComponentState** .

Configurando o modo de manutenção para um servidor de caixa de correio ou de acesso para cliente Exchange 2013 permite que você coloque o servidor de serviço. Para um servidor de caixa de correio, fora de serviço significa que o servidor não hospedar qualquer banco de dados ativo, todas as filas de transporte estão vazias e o servidor não aceita qualquer chamadas feitas pelos servidores de acesso para cliente, gateways VoIP, IP PBXs, PBXs habilitados para SIP ou SBCs. Para um servidor de acesso para cliente, fora de serviço significa que o servidor não aceita qualquer chamadas de entrada de gateways VoIP, IP PBXs, PBXs habilitados para SIP ou SBCs.

Em Exchange 2007 e Exchange 2010, houve um parâmetro de status que pode ser usado para controlar o status operacional de um servidor de Unificação de mensagens. Exchange 2013, nenhum parâmetro status está disponível para essa finalidade no cmdlet **Set-UMCallRouterSettings** em um servidor de acesso para cliente ou o cmdlet **Set-UMService** para um servidor de caixa de correio.

Embora os servidores de acesso para cliente e caixa de correio forem definidos como habilitada quando eles instalados, nem servidores podem processar corretamente e rotear chamadas de entrada para usuários habilitados até que um UM plano de discagem está vinculada pelo menos um gateway IP de UM.

Depois que um plano de discagem está vinculado com um gateway IP de UM, os servidores de acesso para cliente e caixa de correio localize todos os gateways IP de UM associados ao plano de discagem e gateways VoIP, PBXs IP e SBCs. Para detectar e identificar as alterações de configuração em planos de discagem de Unificação de mensagens ou gateways IP de UM, os servidores de acesso para cliente ou caixa de correio Verifique a configuração de cada 10 minutos.

Se o gateway IP de UM identifica quaisquer alterações na configuração, o servidor de acesso para cliente ou caixa de correio reage adequadamente, e começa a usar ou pára de usar o gateway de VoIP apropriada, IP PBX ou SBC. Depois que os servidores de acesso para cliente e caixa de correio responder a entrada vinculado de chamadas para usuários com um plano de discagem de Unificação de mensagens e eles corretamente estiver se comunicando com gateways VoIP, PBXs IP e SBCs, é possível executar um conjunto de operações de diagnósticos para verificar se ele estão funcionando corretamente e que conectividade entre os servidores Exchange e gateways VoIP, IP PBXs ou SBCs está funcionando corretamente.

Voltar ao início

