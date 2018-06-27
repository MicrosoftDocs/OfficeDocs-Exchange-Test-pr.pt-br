---
title: 'Serviços, portas e protocolos de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Serviços, portas e protocolos de Unificação de mensagens
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54651968
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Serviços, portas e protocolos de Unificação de mensagens

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

Microsoft Exchange 2013 Unified Messaging (UM) requer que várias portas TCP e protocolo de datagrama de usuário (UDP) ser usado para estabelecer a comunicação entre servidores que executam o Exchange 2013 e outros dispositivos. Permitindo o acesso por essas portas IP, você habilitar a Unificação de mensagens para funcionar corretamente. Este tópico discute as portas TCP e UDP usadas em Exchange 2013 Unificação de mensagens.

## Serviços e protocolos de mensagens unificados

Exchange 2013 Serviços e recursos do Unified Messaging contam com estáticas e dinâmicas portas TCP e UDP para garantir o funcionamento correto dos servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange. Quando Exchange 2013 for instalado, as regras de Firewall de entrada estática Windows são adicionadas aos Exchange. Se você alterar as portas TCP que são usadas pelos servidores de caixa de correio e acesso para cliente, você também pode precisar reconfigurar as regras de Firewall Windows para permitir que a Unificação de mensagens para funcionar corretamente.


> [!IMPORTANT]
> On Exchange 2013 acesso para cliente e caixa de correio servidores que executam serviços e componentes de Unificação de mensagens, a instalação do Exchange cria regras de firewall de entrada que permitem a comunicação de entrada sem restrições porta TCP. As seguintes regras de entrada para os serviços de Unificação de mensagens são adicionadas:



1.  **SESWorker (GFW) (TCP-entrada)**

2.  **UMCallRouter (GFW) (TCP-entrada)**

3.  **UMCallRouter (TCP-entrada)**

4.  **UMService (GFW) (TCP-entrada)**

5.  **UMService (TCP-entrada)**

6.  **UMWorkerProcess – RPC (TCP-entrada)**

7.  **UMWorkerProcess (GFW) (TCP-entrada)**

8.  **UMWorkerProcess (TCP-entrada)**

## Protocolo de inicialização de sessão

Protocolo de iniciação de sessão (SIP) é um protocolo usado para iniciar, modificar e finalizar uma sessão de usuário interativo que envolve os elementos de multimídia, como vídeo, voz, mensagens instantâneas, jogos online e realidade virtual. É um dos principais protocolos de sinalização de voz sobre IP (VoIP), juntamente com h. 323. A maioria das soluções de VoIP baseada em padrões use h. 323 ou SIP. No entanto, vários designs proprietárias e protocolos também existem. Normalmente, os protocolos de VoIP suportam recursos como chamada em espera, conferência chamar e transferência de chamada.

Clientes do SIP como gateways VoIP e IP Private Branch eXchanges (PBXs) podem usar a porta TCP e UDP 5060 se para conectar aos servidores do SIP, incluindo servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada. SIP é usada apenas para configurar e derrubar chamadas de voz ou vídeos. Todas as comunicações de voz e vídeos ocorrerem via protocolo de transporte em tempo real (RTP).

## Protocolo de transporte em tempo real

RTP define um formato de pacote padrão para fornecimento de áudio e vídeo através de uma rede específica, como a Internet. RTP executa apenas os dados de voz/vídeo através da rede. A configuração da chamada e sua interrupção geralmente são realizadas pelo SIP.

RTP não exige uma porta TCP ou UDP standard ou estática para se comunicarem. Comunicações de RTP ocorrem em uma número par a porta UDP, e a porta número ímpar de superior próxima é usada para comunicações TCP. Embora existam sem atribuições de intervalo de porta padrão, RTP geralmente está configurada para usar portas entre 1024 e 65535 e os servidores de caixa de correio executando o acompanhamento de serviço de Unificação de mensagens do Microsoft Exchange essa convenção. É difícil para RTP atravessar firewalls, pois ela usa um intervalo de portas dinâmicas.

## Serviços de Unificação de mensagens Web

Os serviços de Unificação de mensagens Web instalados em servidores de caixa de correio usam IP para comunicação de rede entre um cliente, o servidor de caixa de correio e computadores que executam outras funções de servidor Exchange 2013. Vários recursos de clienteOutlook Web App e Outlook 2013Exchange 2013 confiam nos serviços de Unificação de mensagens Web para que funcionem corretamente.

Os seguintes recursos de cliente de Unificação de mensagens dependem de serviços da Web Unificação de mensagens:

  - Opções de email disponíveis com Exchange 2013Outlook Web App, incluindo tocar no recurso de telefone e a capacidade de redefinir um PIN de voz.

  - Tocar no recurso de telefone encontrado em um cliente Outlook.

## Portas de UM

O serviço de Microsoft Exchange Unified Messaging roteador de chamada foi encontrado em um servidor de acesso para cliente usa SIP sobre protocolo de controle de transmissão (TCP) ou mutual Transport Layer Security (TLS mútuo) para se comunicar com os servidores de caixa de correio que estão executando o serviço de Unificação de mensagens do Microsoft Exchange. Para evitar conflitos de porta TCP/UDP User Datagram Protocol (), o serviço de Unificação de mensagens do Microsoft Exchange e o Microsoft Exchange Unified Messaging serviço roteador de chamadas como padrão e ouvir em diferentes portas TCP. Eles podem aceitar ambos desprotegido e protegido conexões, dependendo se o TLS mútuo é usado com o tráfego SIP e RTP. Por padrão, um servidor de acesso para cliente escuta para solicitações SIP em ambos os porta TCP 5060 no modo não seguro e a porta TCP 5061 no modo SIP seguro quando for usado o TLS mútuo. Essas portas são configuráveis usando o cmdlet **Set-UMCallRouterSettings** . O serviço Microsoft Exchange Unified Messaging roteador de chamadas no servidor de acesso para cliente não lida com tráfego mídia (RTP ou SRTP), portanto, somente as portas TCP e nenhuma outra porta UDP é usada. Por padrão, um servidor de caixa de correio Escuta para solicitações SIP em ambos os porta TCP 5062 no modo não seguro e a porta TCP 5063 no modo SIP seguro quando for usado o TLS mútuo. Essas portas não são configuráveis usando cmdlets do Shell de gerenciamento do Exchange. O serviço de Unificação de mensagens do Microsoft Exchange no servidor de caixa de correio aceitará conexões de um servidor de acesso para cliente nas portas SIP 5062 e 5063. Depois que o servidor de acesso para cliente redireciona a solicitação SIP para um servidor de caixa de correio, um canal de mídia RTP ou SRTP é criado usando um gateway VoIP, IP PBX ou SBC e o processo de trabalho de Unificação de mensagens do Microsoft Exchange no servidor de caixa de correio.

A tabela a seguir resume as portas e protocolos do Exchange 2013 e indica se as portas podem ser alteradas.

### Portas de escuta de UM

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolo</th>
<th>Porta TCP</th>
<th>Porta UDP</th>
<th>As portas podem ser alteradas?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (servidor de acesso para cliente – Microsoft Unified Messaging serviço roteador de chamadas)</p></td>
<td><p>5060 (inseguro), 5061 (seguro). O serviço escuta as duas portas.</p></td>
<td><p>Não se aplica</p></td>
<td><p>Sim, usando-se o cmdlet <strong>Set-UMCallRouterSettings</strong>.</p></td>
</tr>
<tr class="even">
<td><p>SIP (Servidor de Caixa de Correio – serviço de Unificação de Mensagens do Microsoft Exchange)</p></td>
<td><p>5062 (inseguro), 5063 (seguro). O serviço escuta as duas portas.</p></td>
<td><p>Não se aplica</p></td>
<td><p>As portas não podem ser alteradas.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (servidor de Caixa de Correio - processo de trabalho de UM)</p></td>
<td><p>5065 e 5067 para TCP (sem segurança). 5065 e 5067 para TLS mútuo (protegido). Se você definiu para modo Dual 5066 e 5068 também são usados.</p></td>
<td><p>Não se aplica</p></td>
<td><p>As portas não podem ser alteradas.</p></td>
</tr>
<tr class="even">
<td><p>RTP (servidor de Caixa de Correio - processo de trabalho de UM)</p></td>
<td><p>Não se aplica</p></td>
<td><p>Portas entre 1024 e 65535.</p></td>
<td><p>Portas podem ser alteradas no arquivo de configuração msexchangeum.config. O arquivo msexchangeum.config está localizado na pasta \Program Files\Microsoft\Exchange\V15\bin em um servidor de Unificação de mensagens do Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Portas do Lync Server e Unificação de mensagens

Exchange 2013 A Unificação de mensagens oferece suporte a passagem de conversão de endereço de rede (NAT) e permite a mídia RTP para um servidor de caixa de correio para ser encapsulada através de um firewall NAT. No entanto, para que isso funcione, você também deve ter Microsoft Office Communications Server 2007 R2 e Microsoft Lync Server 2010 ou Microsoft Lync 2013 implantado em seu ambiente. Se você implantar tanto Exchange 2013 e Communications Server 2007 R2 ou Microsoft Lync Server 2010 ou Lync 2013 em sua rede, essa implantação permitirá que os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange para se comunicar com pontos de extremidade fora de um firewall NAT. O servidor de caixa de correio está associado um Communications Server 2007 R2, Microsoft Lync Server 2010 ou um pool Lync 2013 e obtém os tokens de autenticação apropriado de A / o serviço de autenticação de V em um computador atendendo a esse determinado pool do Communications Server 2007 ou do Lync Server.

A / V Authentication service é usada para permitir a mídia de voz RTP atravessar firewalls e dispositivos NAT. Isso é necessário porque os gateways de mídia processar a sinalização apenas e não é possível transportar voz com segurança através de um dispositivo NAT ou firewall. Ao configurar um servidor de mediação no Communications Server 2007 R2, o Lync Server 2010 ou Lync 2013, especifique A / servidor de borda de V em que A / o serviço de autenticação V está em execução para que o servidor de mediação saibam onde encaminhar os pacotes de mídia de entrada.

Para obter mais informações sobre como implantar o Communications Server 2007 R2 ou o Lync Server 2010 ou 2013 e Exchange 2013 Unificação de mensagens, consulte o seguinte:

  - [Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

