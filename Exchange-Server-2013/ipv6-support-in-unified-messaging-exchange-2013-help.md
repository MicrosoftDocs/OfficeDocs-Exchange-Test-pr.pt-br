---
title: 'Suporte a IPv6 na Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Suporte a IPv6 na Unificação de mensagens
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 50486128
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suporte a IPv6 na Unificação de mensagens

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-04-07_

Protocolo IP versão 6 (IPv6) é a versão mais recente do Internet Protocol (IP). IPv6 destina-se a corrigir muitas das deficiências IPv4, qual foi a versão anterior do IP. No Microsoft Exchange Server 2010, IPv6 é suportado somente quando o IPv4 também é usado. Não há suporte para um ambiente Exchange IPv6 puro. O uso de endereços IPv6 e intervalos de endereços IP é suportado somente quando o IPv4 e IPv6 estão habilitados no computador executando o Exchange 2010 e a rede suporta as duas versões do endereço IP. No entanto, como IPv4 e IPv6 estão completamente diferentes protocolos, uma rede IPv4 não pode se comunicar diretamente com uma rede IPv6 e vice-versa. Para lidar com a desvantagem, os administradores de rede são necessárias para implantar dispositivos, como roteadores, que podem rotear informações entre redes IPv4 e IPv6. Se Exchange 2010 for implantado usam o IPv4 e IPv6, todas as funções de servidor, exceto Unified Messaging (UM) podem enviar e receber dados dos dispositivos, servidores e clientes que usam os endereços IPv6. Com Exchange 2013, a Unificação de mensagens não mais é uma função de servidor separadas como as funções de servidor de caixa de correio, acesso para cliente e transporte no Exchange 2007 e Exchange 2010. Componentes relacionados a Unificação de mensagens e serviços de fala executados em apenas os servidores de acesso para cliente e caixa de correio.

Em Exchange 2013, porque a arquitetura de Unificação de mensagens mudou e agora requer Unified Communications Managed API (UCMA) v 4.0 para oferecer suporte tanto IPv4 e IPv6, bem como outros recursos do Exchange, os servidores de acesso para cliente e caixa de correio que têm componentes de Unificação de mensagens e serviços dará suporte totalmente redes IPv6.

## Suporte a IPv6

Iniciando com Exchange 2010 Service Pack 1 (SP1), a função de servidor Unificação de mensagens se baseavam em UCMA 2.0 para sua base de sinalização de protocolo de iniciação de sessão (SIP) e fala processamento. UCMA 2.0 é o componente principal para os recursos de fala na Unificação de mensagens. UCMA 2.0 contém uma pilha SIP, uma pilha de mídia e mecanismos de fala para fala ASR (reconhecimento automático), além de síntese de fala que seja gerada pelo texto em fala (TTS).

Em Exchange 2010, executar uma pilha dupla (IPv4 e IPv6) era necessário ter todas as funções de servidor, com exceção de Unificação de mensagens porque UM necessário UCMA 2.0, mas com suporte apenas IPv4, IPv6 não. Para Exchange 2013, UCMA 4.0 é usado pela Unificação de mensagens e é necessário para a instalação Exchange 2013 em servidores de caixa de correio e acesso para cliente. UCMA 4.0 e é necessário para dar suporte a novos recursos para oferecer suporte a IPv6.

Alguns dos motivos por que UM agora usa UCMA 4.0 para suportar os novos recursos em Exchange 2013, incluindo o IPv6, são os seguintes:

  - Algumas agências governamentais exigem suporte a IPv6 para produtos que eles usam.

  - Requer UM agora a compatibilidade com os dispositivos de hardware, como roteadores, gateways IP, IP PBXs e controladores de borda de sessão (SBCs) que executam uma pilha dupla (IPv4 e IPv6) ou apenas IPv6.

  - Em Exchange 2013, o serviço de Unificação de mensagens do Microsoft Exchange é executado no servidor de caixa de correio e o serviço do Microsoft Exchange Unified Messaging roteador de chamada é executado no servidor de acesso para cliente. Funções de servidor acesso para cliente e caixa de correio em Exchange 2013 exigem IPv4 e IPv6.

  - Serviços online permitem que os clientes se conectem ao seu serviço usando um dos orIPv6 IPv4.

  - Espaço de endereço IPv4 público está executando o check-out. Para Exchange Server 2013 Enterprise, isso não é realmente um problema para Unificação de mensagens, desde que a Unificação de mensagens sempre se comunica com peers SIP internos que podem ser implantados com um espaço de endereço IPv4 privado. No entanto, para UM do Exchange hospedada, o equipamento do cliente deve suportar UM hospedada usando IPv4 e IPv6.

Com exceção de Unificação de mensagens e uma pequena parte do transporte, Exchange 2013 podem se conectar aos servidores de Exchange 2010 em uma organização quando um acesso para cliente ou servidor de caixa de correio é executado no modo de pilha dupla com IPv4 e IPv6 ativado. Isso significa que os clientes podem instalar Exchange 2013 em computadores que estão executando o IPv4 e IPv6 endereços de pilha configurados. Isso permite que os clientes de IPv6 e outros servidores do Exchange, incluindo Exchange Server 2010, para se conectarem diretamente ao Exchange 2013.

Unificação de mensagens funciona nos servidores do Windows em execução no modo de pilha dupla. Isso ocorre porque os protocolos como HTTP ignorar o tipo de transporte e UM usa voz sobre IP (VoIP) protocolos (incluindo SIP/RTP/STUN/TURN/ICE), que não são dependentes entre si. Isso inclui a negociação de mídia (RTP/SRTP), na qual UM anuncia e uma lista de endereços IP, se comunica com correspondentes de SIP, gateways IP, IP PBXs ou SBCs.

## O que significa oferece suporte a IPv6 para Unificação de mensagens?

Para habilitar Exchange 2013 Unificação de mensagens para dar suporte a IPv6, enterprise e administradores de Unificação de mensagens online devem ser capazes de tirar vantagem do IPv6 quando se conectarem a Unificação de mensagens a dispositivos compatível com IPv6, incluindo dispositivos, como roteadores, gateways IP, IP PBXs e servidores do Office Communications Server 2007 R2 e Microsoft Lync. No entanto, se IPv6 não está disponível para interoperabilidade e manter a compatibilidade com versões anteriores do Exchange, os administradores não precisam fazer alterações de configuração adicionais e IPv4 pode ser usada em vez disso.

Para Exchange Enterprise 2013, Unificação de mensagens deve se comunicar diretamente com colegas SIP (gateways IP, PBXs IP e SBCs) que podem não suportar IPv6 em seu software ou firmware. Portanto, a Unificação de mensagens deve ser capazes de se comunicarem diretamente com colegas SIP que oferecem suporte a IPv4 e mais importante, com IPv6. Para hospedada Exchange 2013, Unificação de mensagens se comunica com o equipamento de cliente por meio de SBCs ou o Lync Server 2010 ou o Lync Server 15. No hospedados ambientes de Exchange 2013, reconhecimento de IPv6 SIP clientes como SBCs e Lync servidores potencialmente podem ser implantadas e, portanto, lidar com o processo de conversão de IPv6 para IPv4.

## Suporte de Unificação de mensagens do dispositivo para IPv6

Porque os servidores de acesso para cliente e caixa de correio de Exchange 2013 que executam serviços e componentes de Unificação de mensagens oferece suporte a IPv6, gateway IP, IP PBX e fornecedores SBC devem também ser capazes de oferecer suporte a IPv6. Há várias questões que afetam o suporte a dispositivos para IPv6:

  - Há gateways IP, PBXs IP e SBCs poderá oferecer suporte a IPv6, mas ainda não foram testadas com a Unificação de mensagens e o IPv6. Esse suporte pode ser adicionado no futuro, mas ela depende do fornecedor de hardware.

  - Alguns gateways IP possuem atualmente não há suporte a IPv6.

  - Alguns SBCs têm a funcionalidade de IPv6 a IPv4, mas eles não funcionam para Unificação de mensagens porque não aceitam SRTP (Secure Real-time Transport Protocol) / SDES (segurança de protocolo de descrição de sessão).

  - Há PBXs IP que não há suporte para uma pilha dupla e IPv6 puro, mas esses dispositivos ainda não foram testados para funcionar com Exchange 2013.

Atualmente UCMA 4.0 está habilitado para IPv6, que significa que ele pode aceitar conexões IPv6, mas que IPv4 também pode ser aceita, ao operar no modo dual ou ao fazer conexões de saída. Em execução no modo dual permite conexões IPv4 sejam feitas quando forem necessários para se conectar a versões anteriores de UM do Exchange. Para instalações do Lync, isso é feito pelo Lync Server, que obtém as informações de versão do Active Directory para a versão mais recente do Exchange Server. Para dispositivos de telefonia tradicional — incluindo gateways IP, PBXs IP e SBCs — para oferecer suporte a conexões de IPv6, juntamente com o IPv4, devem escutar para ambos os tipos de conexões. Isso ocorre porque cada peer SIP deve ser capaz de aceitar os dois tipos de conexões para manter a compatibilidade com versões anteriores de UM do Exchange. Isso também é necessário para dar suporte a discagem externa para ambos os tipos de conexões.

## Configuração de Unificação de mensagens para dar suporte a IPv6

Depois de instalar os servidores de acesso para cliente e caixa de correio, você precisará criar planos de discagem de Unificação de mensagens, atendentes automáticos, gateways IP e grupos de busca. Para permitir que a Unificação de mensagens dar suporte a IPv6, você deve:

  - Criar um novo gateway IP de UM, ou configurar um gateway IP de UM existente com um endereço IPv6 para cada um dos gateways IP, IP PBXs ou SBCs em sua rede. Quando você estiver criando e configurando gateways IP de UM necessários, você deve adicionar o endereço IPv6 ou o nome de domínio totalmente qualificado (FQDN) para o gateway IP de UM. Se você está adicionando o FQDN para o gateway IP de UM, você deve ter criado os registros DNS corretos para resolver o FQDN do gateway IP de UM para o endereço IPv6. Se você tiver um gateway IP de UM existente, você pode usar o cmdlet **Set-UMIPgateway** para configurar o FQDN ou endereço IPv6. Depois que você cria ou configura gateways IP de UM, você pode usar o cmdlet **Get-UMIPgateway** para exibir as propriedades de um gateway IP de UM para garantir que as configurações de IPv6 estão corretas.

  - Configure o parâmetro *IPAddressFamily* em cada gateway IP de UM. Para habilitar o gateway IP aceitar pacotes IPv6, você deve definir o gateway IP de UM para aceitar conexões de IPv4 e IPv6, ou aceite apenas as conexões de IPv6, usando o cmdlet **Set-UMIPgateway** e definindo o parâmetro *IPAddressFamily* como um destes procedimentos:
    
      - *IPv4* – este é o padrão e é usado se nenhum outro valor for configurado.
    
      - *IPv6* - Isso permite que o IPv6 a ser usado. No entanto, IPv4 não serão usados.
    
      - *Any* – Isso permite que o IPv6 a ser usado, mas se o dispositivo não oferece suporte a IPv6, então IPv4 é usada em vez disso.

  - Depois que você configurou os gateways IP de UM, você também deve configurar os gateways IP, PBXs IP e SBCs em sua rede para dar suporte a IPv6. Para obter detalhes, consulte seu fornecedor de hardware para obter uma lista de dispositivos que oferecem suporte a IPv6 e como configurá-los de corretamente.

  - Opcionalmente, você pode precisar definir os servidores de acesso para cliente e caixa de correio para aceitar o tráfego IPv6 se qualquer um dos servidores estiverem definido apenas para receber tráfego IPv4. No entanto, a configuração padrão é para servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange para aceitar o tráfego de IPv4 e IPv6. Para obter detalhes sobre como definir as configurações de IPv6 em servidores de caixa de correio e acesso para cliente, consulte [Set-UMCallRouterSettings](https://technet.microsoft.com/pt-br/library/jj215758\(v=exchg.150\)) e [Set-UMService](https://technet.microsoft.com/pt-br/library/jj552412\(v=exchg.150\)).
    
    Há dois parâmetros que talvez precisem ser configuradas nos servidores de acesso para cliente e caixa de correio para suporte a IPv6: *IPAddressFamily* e *IPAddressFamilyConfigurable*. Para habilitar um acesso para cliente e um servidor de caixa de correio aceitar pacotes IPv6, você deve definir o servidor de acesso para cliente e caixa de correio para aceitar conexões de IPv4 e IPv6, ou aceite apenas as conexões de IPv6. Para configurar o parâmetro *IPAddressFamily* , o parâmetro *IPAddressFamilyConfigurable* deve ser definido como `$true`.

## Lógica de endereçamento IP de Unificação de mensagens

A lógica por trás de suporte a IPv6 para Unificação de mensagens no Exchange 2013 é da seguinte maneira:

  - Servidores de acesso para cliente e caixa de correio ouvir em interfaces de IPv4 e IPv6 quando a pilha dupla estiver habilitada e os servidores de acesso para cliente e caixa de correio são definidos como *IPv6* ou *Any*. Caso contrário, apenas o IPv4 é usado.

  - Para chamadas de saída, a Unificação de mensagens usa modo dual se o parâmetro *IPAddressFamily* para os gateways IP de UM, os servidores de acesso para cliente e servidores de caixa de correio é definido como *IPv6* ou *Any*. Caso contrário, apenas o IPv4 é usado.

Ao fazer chamadas de saída no modo dual, se o parâmetro *IPAddressFamily* é definido como *IPv6* ou *Any*:

  - UCMA obterá uma lista de endereços no FQDN para um par SIP que ele está tentando acessar.

  - UCMA tentará todos os endereços IPv6, se houver alguma.

  - Se o UCMA determina se um endereço não está disponível, ele será incluem o endereço em uma lista e tente não-lo novamente com base em um intervalo configurado. Isso impede que UM desnecessariamente repetindo endereços ruim conhecidos.

  - Se nenhum endereços IPv6 estão disponíveis, UCMA se voltará aos endereços IPv4 na lista de endereços para pares SIP.

