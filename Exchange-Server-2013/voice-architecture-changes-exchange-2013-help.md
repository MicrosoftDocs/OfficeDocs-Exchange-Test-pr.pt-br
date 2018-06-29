---
title: 'Mudanças de arquitetura de voz: Exchange 2013 Help'
TOCTitle: Mudanças de arquitetura de voz
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 50485614
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mudanças de arquitetura de voz

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

A arquitetura do Microsoft Exchange Server 2013 é diferente da arquitetura do Exchange Server 2007 e Exchange Server 2010. No Exchange 2007 e no Exchange 2010, os tipos de servidores foram separados em várias funções de servidor: Transporte de Hub, Acesso para Cliente, Caixa de Correio e Unificação de Mensagens. No Exchange 2013, as funções de servidor são combinadas em dois tipos de servidores, e todos os componentes ou serviços dessas funções de servidor são executadas no mesmo servidor físico ou em dois servidores separados chamados Acesso para Cliente e Caixa de Correio. No novo modelo, o servidor de Acesso para Cliente executando o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange redireciona o tráfego do protocolo SIP que é gerado por uma chamada de entrada para um servidor de Caixa de Correio. Então, um canal de mídia (protocolo RTP ou RTP seguro (SRTP)) é estabelecido do gateway VoIP ou da central privada de comutação telefônica (PBX) por IP para o servidor de Caixa de Correio que hospeda a caixa de correio do usuário. No Exchange 2013, o servidor de Caixa de Correio tem os mesmos processos que a função de servidor Unificação de Mensagens no Exchange 2007 e no Exchange 2010. O servidor de Caixa de Correio executa tanto o serviço Unificação de Mensagens do Microsoft Exchange quanto processos de trabalho de UM. O servidor de Acesso para Cliente executa o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange, que recebe uma chamada de entrada e a encaminha ao servidor de Caixa de Correio.

**Conteúdo**

Support for the new Exchange architecture

UM ports

UM dial plans

UM Call Router performance counters

## Suporte para a nova arquitetura do Exchange

No Exchange 2013, o servidor de Acesso para Cliente é responsável pela Descoberta Automática, SSL, autenticação, redirecionamento e proxy. O servidor de Acesso para Cliente é o ponto de entrada para quaisquer chamadas de entrada ou solicitações SIP para Unificação de Mensagens (UM). A lógica de roteamento e REDIRECIONAMENTO SIP são implementados como um serviço que é automaticamente incluído em um servidor de Acesso para Cliente. Esse serviço é conhecido como o Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange. Ele é instalado e executado em cada servidor de Acesso para Cliente em sua organização. Quando um servidor de Acesso para Cliente recebe um CONVITE SIP para uma chamada de entrada, o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange redireciona a chamada de entrada para o servidor de Caixa de Correio. Então, um canal de mídia (RTP ou SRTP) é criado entre o gateway VoIP, PBX IP ou controlador de borda de sessão (SBC) e o servidor de Caixa de Correio. Apesar de o servidor de Acesso para Cliente agir como um redirecionador SIP, ele trata somente de solicitações SIP de gateway VoIP, PBXs IP ou SBCs. Ele não recebe qualquer tráfego de mídia. O tráfego de mídia que usa RPT ou SRTP é encaminhado somente entre o servidor de Caixa de Correio e pares SIP, como gateways VoIP, PBXs IP ou SBCs—não para o servidor de Acesso para Cliente. Quando você implanta o Exchange 2013 e UM, você tem que configurar seus gateways VoIP, PBXs IP ou SBC para apontar para os servidores de Acesso para Cliente que você instalou, para que as chamadas de entrada sejam roteadas corretamente para UM.

Em alguns casos, implantar vários servidores de Acesso para Cliente é um requisito, e os servidores de Acesso para Cliente são implantados separadamente em hardware físico diferente dos servidores de Caixa de Correio. Os servidores de Acesso para Cliente podem ser agrupados em uma matriz, usando-se um balanceador de carga de hardware ou software L4 ou L5. No entanto, não há matrizes de servidor de Acesso para Cliente baseadas em objeto do Exchange do Active Directory. Usar um balanceador de carga de hardware ou software na frente de servidores de Acesso para Cliente é uma prática aceita em implantações maiores do Exchange.

Quando um servidor de Acesso para Cliente é instalado, o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange fica em execução. O serviço faz o seguinte:

  - Quando inicializado, ele lê um arquivo de configuração local chamado msexchangeumcallrouter.config.

  - Executa a geração de gramática de fala usando a caixa de correio de arbitragem de uma organização.

  - Oferece suporte a conexões de protocolos TCP e/ou TLS. Essa configuração pode ser definida.

  - Irá parar somente se houver um erro de configuração ou se não puder registrar as portas necessárias.

No Exchange 2013, o servidor de Caixa de Correio não é responsável por responder a solicitações SIP de chamadas de entrada. Ele é responsável somente por receber tráfego SIP de um servidor de Acesso para Cliente e, então, estabelecer uma conexão RTP ou SRTP ao gateway VoIP, PBX IP ou SBC.

Depois de um servidor de Acesso para Cliente redirecionar uma chamada de entrada para um servidor de Caixa de Correio, um canal de mídia é estabelecido entre o gateway VoIP, PBX IP ou SBC e o servidor de Caixa de Correio. Depois de o canal de mídia ser estabelecido, o serviço de Unificação de Mensagens do Microsoft Exchange, no servidor de Caixa de Correio reproduz a saudação da caixa postal do usuário, processa as regras de atendimento de chamadas para o usuário e convida o chamador a deixar uma mensagem de voz. O servidor de Caixa de Correio, então, grava a mensagem de voz, cria uma transcrição da mensagem e a deposita na caixa de correio do usuário. Entretanto, se você estiver integrando o Exchange ao Office Communications Server 2007 R2 ou Lync Server, tanto SIP quanto os canais de mídia RTP ou SRTP para chamadas de entrada serão tratados pelos servidores Lync e o servidor de Caixa de Correio. Em um ambiente integrado do Lync, você não tem gateways VoIP, PBXs IP ou SBCs. Para o Lync, o servidor de Caixa de Correio que está executando o serviço Unificação de Mensagens do Microsoft Exchange se parece apenas com um servidor de UM do Exchange 2010. O servidor de Caixa de Correio e o servidor de Acesso para Cliente em execução no serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange são considerados pares confiáveis, porque ambos os servidores devem ser adicionados a um plano de discagem SIP. O Lync roteia a chamada de entrada, usando o componente Roteamento de Entrada, que usa SIP para se comunicar com o servidor de Acesso para Cliente e, depois, rotear a chamada para um servidor de Caixa de Correio.

Os administradores de UM do Exchange 2010 podem configurar um conjunto de propriedades para Unificação de Mensagens em cada servidor de UM. No Exchange 2013, componentes de UM e configurações de UM são encontrados tanto nos servidores de Acesso para Cliente e de Caixa de Correio. Todas as configurações aplicadas a um único computador com a função de servidor Unificação de Mensagens no Exchange 2010 ainda estão disponíveis. Entretanto, algumas dessas propriedades e configurações são definidas em um servidor de Acesso para Cliente com o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange, e outras estão disponíveis em um servidor de Caixa de Correio com o serviço de Unificação de Mensagens do Microsoft Exchange. Em alguns casos, a mesma configuração está disponível em ambos. A seguinte lista mostra os cmdlets e os parâmetros disponíveis nos servidores de Acesso para Cliente e servidores de Caixa de Correio e onde alterações foram feitas em um cmdlet para dar suporte a cenários de implantação com versões anteriores da Unificação de Mensagens.

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    Disponível nos servidores de Caixa de Correio do Exchange 2013 e também funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    Disponível nos servidores de Acesso para Cliente do Exchange 2013, mas não disponível para os servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    Disponível nos servidores de Caixa de Correio do Exchange 2013 e também funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   Não disponível nos servidores de Acesso para Cliente do Exchange 2013 e não disponível para os servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMService -SipTcpListeningPort \<Int32\>**    Não configurável nos servidores de Caixa de Correio do Exchange 2013, mas funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMService -SipTlsListeningPort \<Int32\>**    Não configurável nos servidores de Caixa de Correio do Exchange 2013, mas funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**    Disponível nos servidores de Acesso para Cliente do Exchange 2013, mas não funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**    Disponível nos servidores de Acesso para Cliente do Exchange 2013, mas não funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMService - Status \<Habilitado | Desabilitado | NoNewCalls\>**   Não disponível nos servidores de Caixa de Correio do Exchange 2013, mas funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMCallRouterSettings - Status \<Habilitado | Desabilitado | NoNewCalls\>**   Não disponível nos servidores de Acesso para Cliente do Exchange 2013 e não funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMService -UMStartupMode \<TCP | TLS | Duplo\>**   Disponível nos servidores de Caixa de Correio do Exchange 2013 e funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Duplo\>**    Disponível nos servidores de Acesso para Cliente do Exchange 2013, mas não funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Enable-UMService**    Não disponível nos servidores de Caixa de Correio do Exchange 2013, mas funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

  - **Disable-UMService**    Não disponível nos servidores de Caixa de Correio do Exchange 2013, mas funciona nos servidores de Unificação de Mensagens do Exchange 2007 e do Exchange 2010.

Para o servidor de Caixa de Correio, você irá usar os cmdlets **Set/Get/Enable/Disable-UMService** para exibir ou configurar propriedades de UM para o serviço de Unificação de Mensagens do Microsoft Exchange nos servidores de Caixa de Correio do Exchange 2013 ou nos servidores de Unificação de Mensagens do Exchange 2007 ou Exchange 2010. Um conjunto diferente de cmdlets, **Set/Get-UMCallRouterSettings**, são usados para exibir ou configurar as propriedades do serviço Roteador de Chamadas de Unificação de Mensagens em um servidor de Acesso para Cliente. Isso garante que os cmdlets **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** e **Disable-UMServer** existentes do Exchange 2007 e do Exchange 2010 funcionem em um ambiente de coexistência com servidores de Caixa de Correio do Exchange 2013. Isso também garante que os cmdlets irão funcionar quando os servidores de Caixa de Correio e de Acesso para Cliente sejam instalados no mesmo servidor ou em servidores diferentes.

Voltar ao início

## Portas de UM

O serviço Roteador de Chamadas de Unificação de Mensagens encontrado em um servidor de Acesso para Cliente usa SIP sobre o protocolo TCP ou o TLS mútuo para se comunicar com servidores de Caixa de Correio que estejam com o serviço Unificação de Mensagens do Microsoft Exchange. Para evitar conflitos de portas TCP/UDP, o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange e o serviço Unificação de Mensagens do Microsoft Exchange têm como padrão e escutam portas TCP diferentes. Elas podem aceitar conexões protegidas e desprotegidas, dependendo de se o TLS mútuo é usado com tráfego SIP e RTP. Por padrão, um servidor de Acesso para Cliente escuta solicitações SIP tanto na porta 5060 do TCP, no modo Desprotegido, e na porta 5061 do TCP, no modo SIP Protegido, quando o mútuo TLS é usado. Essas portas são configuráveis usando-se o cmdlet **Set-UMCallRouterSettings**. O serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange no servidor de Acesso para Cliente não trata o tráfego de mídia (RTP ou SRTP), então somente portas TCP são usadas, nenhuma UDP. Por padrão, um servidor de Caixa de Correio escuta solicitações SIP tanto na porta 5062 do TCP, no modo Desprotegido, e na porta 5063 do TCP, no modo SIP Protegido, quando o mútuo TLS é usado. Estas portas não são configuráveis usando-se cmdlets do Shell de Gerenciamento do Exchange. No servidor de Caixa de Correio com o serviço Unificação de Mensagens do Microsoft Exchange, as portas TCP não podem ser configuradas no servidor Exchange, usando o Shell ou definindo as configurações no registro. O serviço de Unificação de Mensagens do Microsoft Exchange, no servidor de Caixa de Correio, irá aceitar conexões de um servidor de Acesso para Cliente, nas portas SIP 5062 e 5063. Depois de o servidor de Acesso para Cliente redirecionar a solicitação SIP para um servidor de Caixa de Correio, um canal de mídia RTP ou SRTP é criado usando-se um gateway VoIP, PBX IP ou SBC e o processo de trabalho de Unificação de Mensagens do Microsoft Exchange no servidor de Caixa de Correio.

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
<td><p>SIP (servidor de Acesso para Cliente – serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange)</p></td>
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
<td><p>5065 e 5067 para TCP (inseguro). 5066 e 5068 para TLS mútuo (seguro). Esse é o caso quando <em>UMStartupMode</em> é definido como <em>Dual</em>. Se <em>UMStartUpMode</em> for definido para <em>TCP</em> ou <em>TLS</em>, as portas 5065 e 5066 serão usadas. O <em>UMStartupMode</em> padrão é <em>TCP</em>.</p></td>
<td><p>Não se aplica</p></td>
<td><p>As portas não podem ser alteradas.</p></td>
</tr>
<tr class="even">
<td><p>RTP (servidor de Caixa de Correio - processo de trabalho de UM)</p></td>
<td><p>Não se aplica</p></td>
<td><p>Portas entre 1024 e 65535.</p></td>
<td><p>O intervalo de portas que pode ser alterado através do registro (entretanto, esta não é uma configuração suportada):</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## planos de discagem da UM

Mapear ou associar planos de discagem de UM a servidores de UM não é obrigatório no Exchange 2013 do jeito que era no Exchange 2007 e no Exchange 2010. Os servidores de Acesso para Cliente ou de Caixa de Correio com serviços de UM não precisam estar vinculados a um plano de discagem, porque espera-se que todos os servidores de Acesso para Cliente ou de Caixa de Correio recebam todas as chamadas de entrada de gateways VoIP, PBXs IP ou SBCs. A exceção é que planos de discagem SIP que são usados com Lync 2013, Lync Server 2010 e Office Communications Server 2007 R2 devem ser associados aos servidores de Acesso para Cliente e de Caixa de Correio que você implantar. Ambos os tipos de servidores Exchange devem ser adicionados a cada plano de discagem SIP, para serem incluídos como pares confiáveis do Communications Server 2007 R2 ou Lync Server. Do contrário, o Communications Server 2007 R2 ou o Lync Server irá rejeitar chamadas de saída de usuários.

A tabela a seguir resume o relacionamento entre servidores de Acesso para Cliente e de Caixa de Correio e planos de discagem de UM.

### Planos de discagem de UM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topologia</th>
<th>Plano de discagem</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acesso para Cliente e Caixa de Correio no mesmo servidor (sem planos de discagem não SIP do Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Os planos de discagem não precisam mais estar associados a um servidor de Acesso para Cliente ou de Caixa de Correio. Você não tem permissão para adicionar os servidores de Acesso para Cliente ou de Caixa de Correio a um plano de discagem. Se você executar o cmdlet <strong>Set-UMService</strong>, ele irá gerar um erro, se você tentar associar um servidor de Caixa de correio a um plano de discagem não SIP.</p></td>
</tr>
<tr class="even">
<td><p>Acesso para Cliente e Caixa de Correio em servidores diferentes (sem planos de discagem não SIP do Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Os planos de discagem não precisam mais estar associados a servidores de Acesso para Cliente ou de Caixa de Correio. Você não tem permissão para adicionar servidores de Acesso para Cliente ou de Caixa de Correio a um plano de discagem. Se você executar o cmdlet <strong>Set-UMService</strong>, ele irá gerar um erro, se você tentar associar um servidor de Caixa de correio a um plano de discagem não SIP.</p></td>
</tr>
<tr class="odd">
<td><p>Acesso para Cliente e Caixa de Correio no mesmo servidor físico (com planos de discagem SIP do Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Para um único plano de discagem SIP, adicione todos os servidores de Acesso para Cliente e Caixa de Correio ao plano de discagem SIP. Para vários planos de discagem SIP, adicione todos os servidores de Acesso para Cliente e Caixa de Correio a cada um dos planos de discagem SIP. Isso fará com que os dois servidores sejam pares confiáveis do Office Communications Server 2007 R2 ou do Lync Server. Você deve usar o mesmo certificado na sua implantação do Office Communications Server 2007 R2 ou do Lync Server, como você faz em cada servidor de Acesso para Cliente e de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>Acesso para Cliente e Caixa de Correio em servidores físicos diferentes (com planos de discagem SIP do Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Para um único plano de discagem SIP, adicione todos os servidores de Acesso para Cliente e Caixa de Correio ao plano de discagem SIP. Para vários planos de discagem SIP, adicione todos os servidores de Acesso para Cliente e Caixa de Correio a cada um dos planos de discagem SIP. Isso fará com que os dois servidores sejam pares confiáveis do Office Communications Server 2007 R2 ou do Lync Server. Se os certificados sendo usados nos servidores de Acesso para Cliente e Caixa de Correio forem diferentes, você deverá usar o mesmo certificado na sua implantação do Office Communications Server 2007 R2 ou do Lync Server que você usa em cada servidor de Acesso para Cliente ou de Caixa de Correio em sua organização.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Contadores de desempenho do Roteador de Chamada de UM

Versões anteriores do Exchange incluídas na função de servidor Unificação de Mensagens, com o serviço de Unificação de Mensagens do Microsoft Exchange. Por causa das mudanças de arquitetura no Exchange 2013, o servidor de Acesso para Cliente executa o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange, e o servidor de Caixa de Correio executa o serviço Unificação de Mensagens do Microsoft Exchange. Os mesmos contadores de desempenho para o serviço de Unificação de Mensagens do Microsoft Exchange estão disponíveis para os administradores, como nas versões anteriores de UM do Exchange. Entretanto, também há contadores de desempenho adicionais que você pode usar no servidor de Acesso para Cliente, para verificar o status o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange e para solução de problemas.

Para suportar o novo serviço Roteador de Chamadas de Unificação de Mensagens de Acesso para Cliente no Exchange 2013, os seguintes contadores de desempenho estão disponíveis.

### Contadores de desempenho

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Categoria do contador de desempenho</th>
<th>Nome do contador</th>
<th>Descrição</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% de Chamadas de Entrada Rejeitadas pelo Serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange na Última Hora</p></td>
<td><p>Mostra a porcentagem de chamadas de entrada que foram rejeitadas pelo serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange na última hora.</p></td>
<td><p>Deve sempre ser menor do que 5%, mas deveria sempre ser 0.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Chamadas Desconectadas por Erro Interno Irrecuperável para o Serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange</p></td>
<td><p>Mostra o número de chamadas desconectadas após um erro interno do sistema.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total de Chamadas de Entrada Rejeitadas pelo Serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange</p></td>
<td><p>Mostra o número total de chamadas de entrada rejeitadas pelo serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange desde que o serviço foi iniciado.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total de chamadas recebidas pelo Serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange</p></td>
<td><p>Mostra o número total de chamadas de entrada recebidas pelo serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange desde que o serviço foi iniciado.</p></td>
<td><p>Deve ser 0 ou maior.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% de Chamadas de Entrada Rejeitadas pelo Serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange na Última Hora</p></td>
<td><p>Mostra a porcentagem de chamadas de entrada que foram rejeitadas pelo serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange na última hora.</p></td>
<td><p>Deve ser menor do que 5%.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

