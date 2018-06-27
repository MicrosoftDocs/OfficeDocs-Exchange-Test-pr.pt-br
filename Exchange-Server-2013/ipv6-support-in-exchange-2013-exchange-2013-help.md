---
title: 'Suporte a IPv6 no Exchange 2013: Exchange 2013 Help'
TOCTitle: Suporte a IPv6 no Exchange 2013
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 50485299
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suporte a IPv6 no Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

O IPv6 (protocolo IP versão 6) é a versão mais recente do protocolo IP. O IPv6 foi projetado para corrigir muitas das deficiências do IPv4, a versão anterior do protocolo IP.

No Microsoft Exchange Server 2013, só haverá suporte a IPv6 quando o IPv4 também estiver instalado e habilitado. Se o Exchange 2013 for implantado nessa configuração, e se a rede oferecer suporte a IPv4 e IPv6, todos os servidores Exchange poderão enviar e receber dados de dispositivos, servidores e clientes que usem endereços IPv6.

Este tópico aborda o endereçamento IPv6 no Exchange 2013. Para obter informações adicionais sobre o IPv6, consulte [IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582).

**Sumário**

IPv6 support in Exchange 2013 components

Enable or disable protocols in the operating system

IPv6 address basics

## Suporte a IPv6 nos componentes do Exchange 2013

A tabela a seguir descreve os componentes do Exchange 2013 afetados pelo IPv6.

### Recursos do Exchange 2013 e IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Suporte a IPv6</th>
<th>Comments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Listas de permissões de IP e bloqueios de IP no agente de filtragem de conexão</p></td>
<td><p>Sim</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Fornecedores de listas de permissões de IP e bloqueios de IP no agente de filtragem de conexão.</p></td>
<td><p>Não</p></td>
<td><p>Atualmente, não há um protocolo padrão amplamente aceito pelo setor para a busca de endereços IPv6. A maioria dos provedores de lista de bloqueios de IP não oferece suporte a endereços IPv6. Se você permitir conexões anônimas de endereços IPv6 desconhecidos em um conector de Recebimento, aumentará o risco de spammers conseguirem ignorar os provedores de lista de bloqueios de IP e enviarem spam com êxito para sua organização.</p></td>
</tr>
<tr class="odd">
<td><p>Reputação do remetente no agente análise de protocolo</p></td>
<td><p>Não</p></td>
<td><p>O agente de Análise de Protocolo não calcula o SRL (nível de reputação do remetente) de mensagens originadas de remetentes do IPv6. Para obter mais informações sobre a reputação de remetentes, consulte <a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">Reputação do remetente e o agente de análise de protocolo</a>.</p></td>
</tr>
<tr class="even">
<td><p>ID de Remetente</p></td>
<td><p>Sim</p></td>
<td><p>Para obter mais informações, consulte <a href="sender-id-exchange-2013-help.md">ID de remetente</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Conectores de recebimento</p></td>
<td><p>Sim</p></td>
<td><p>Os endereços IPv6 são aceitos para os seguintes componentes:</p>
<ul>
<li><p>Ligações de endereços IP locais</p></li>
<li><p>Endereços IP remotos</p></li>
<li><p>Intervalos de endereços IP</p></li>
</ul>
<p>É altamente recomendável não configurar Conectores de Recebimento para que aceitem conexões anônimas de endereços IPv6 desconhecidos. Se sua organização tiver que receber mensagens de email de remetentes que utilizem endereços IPv6, crie um conector Receber dedicado que restrinja os endereços IP remotos aos endereços IPv6 específicos utilizados por esses remetentes.</p>
<p>Para obter mais informações, consulte <a href="receive-connectors-exchange-2013-help.md">Conectores de recebimento</a>.</p></td>
</tr>
<tr class="even">
<td><p>Conectores de envio</p></td>
<td><p>Sim</p></td>
<td><p>Os endereços IPv6 são aceitos para os seguintes componentes:</p>
<ul>
<li><p>Endereços IP de host inteligente</p></li>
<li><p>O parâmetro <em>SourceIPAddress</em> para conectores de envio configurados nos servidores de Transporte de Borda</p></li>
</ul>

> [!TIP]
> Se você deseja especificar um endereço IPv6 para o parâmetro <EM>SourceIPAddress</EM>, verifique se os registros MX e AAAA do DNS adequados estão configurados corretamente. Isso ajudará a garantir a entrega da mensagem se um servidor de mensagens remoto tentar qualquer tipo de teste de consulta reversa no endereço IPv6 especificado.


<p>Para obter mais informações, consulte <a href="send-connectors-exchange-2013-help.md">Conectores de envio</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Limites de taxa de mensagem de entrada</p></td>
<td><p>Parcial</p></td>
<td><p>Os limites de taxa de mensagens de entrada que você pode definir em um conector de Recebimento, como os parâmetros <em>MaxInboundConnectionPercentagePerSource</em>, <em>MaxInboundConnectionPerSource</em> e <em>TarpitInterval</em>, se aplicam apenas a um endereço IPv6 global. Os endereços IPv6 de local de link e os endereços IPv6 de local de site não são afetados por nenhum limite de taxa de mensagem de entrada especificado.</p></td>
</tr>
<tr class="even">
<td><p>Unificação de Mensagens</p></td>
<td><p>Sim</p></td>
<td><p>Para obter mais informações, consulte <a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">Suporte a IPv6 na Unificação de mensagens</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Membro do grupo de disponibilidade de banco de dados (DAG)</p></td>
<td><p>Sim</p></td>
<td><p>Endereços IPv6 estáticos são aceitos pelo Windows Server e pelo serviço de cluster. Entretanto, o uso de endereços IPv6 estáticos vai contra as práticas recomendadas. O Exchange 2013 não dá suporte à configuração de endereços IPv6 estáticos durante a instalação.</p>
<p>Os clusters de failover têm suporte ao protocolo ISATAP. Eles suportam apenas endereços IPv6 que permitem registro dinâmico no DNS. Endereços de local de link não podem ser usados em um cluster.</p>
<p>Para obter mais informações sobre requisitos de rede do DAG, consulte a seção &quot;Requisitos de rede&quot; em <a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Planejamento de alta disponibilidade e de resiliência do site</a>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Habilitar ou desabilitar protocolos no sistema operacional

Os servidores Exchange 2013 dão total suporte a redes IPv6. Por isso, mesmo se você não estiver usando IPv6, você não precisará desativar IPv6 nos seus servidores Exchange.

O suporte a IPv6 no Exchange 2013 exige que IPv4 esteja instalado em todos os servidores Exchange 2013. A desinstalação do IPv4 de seus servidores Exchange 2013 não tem suporte.

Para saber mais sobre o suporte a IPv6 no Microsoft Windows, consulte [IPv6 para Microsoft Windows: perguntas frequentes](https://go.microsoft.com/fwlink/p/?linkid=147465).

Voltar ao início

## Noções básicas de endereço IPv6

Um endereço IPv6 tem 128 bits. O endereço é descrito usando a notação hexadecimal com dois-pontos. A notação hexadecimal com dois pontos descreve o endereço de 128 bits usando 8 números hexadecimais de 4 dígitos e 16 bits que são separados por dois-pontos (:). Um exemplo de um endereço IPv6 na notação hexadecimal com dois-pontos é 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A.

Você pode expressar um endereço IPv6 usando os seguintes métodos:

  - **Suprimir zeros à esquerda**   Você pode omitir os zeros à esquerda em qualquer um dos 8 números hexadecimais de 4 dígitos em um endereço IPv6.

  - **Compressão de dois-pontos**   Você pode usar dois-pontos (:) para representar dígitos hexadecimais de 16 bits contíguos que contenham todos os zeros. Todos esses dígitos zeros podem existir no início, meio ou fim do endereço IPv6. Você pode usar a compressão de dois-pontos somente uma vez em um endereço IPv6.

  - **Notação decimal com pontos à direita**   Você pode expressar os últimos 32 bits no fim de um endereço IPv6 na notação decimal com pontos separando os dígitos de 8 bits com um ponto (.). A notação decimal com pontos à direita é freqüentemente usada com endereços compatíveis com IPv4.

A tabela a seguir fornece exemplos da notação de endereços IPv6 e a sintaxe do endereço IPv6 equivalente.

### Notação e sintaxe de endereços IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Notação de endereço IPv6</th>
<th>A sintaxe do endereço IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Endereço IPv6 completo</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Endereço IPv6 que usa zeros à esquerda suprimidos</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>Endereço IPv6 que usa compressão de dois-pontos</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Endereço IPv6 que usa notação decimal com pontos à direita</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


Os endereços IPv6 são categorizados nos seguintes tipos:

  - **Endereço unicast**   Um pacote é entregue para uma interface.

  - **Endereço multicast**   Um pacote é entregue para várias interfaces.

  - **Endereço anycast**   Um pacote é entregue para uma das várias interfaces mais próximas. A distância entre interfaces é definida pelo custo de roteamento.

Os endereços unicast IPv6 têm os seguintes escopos possíveis:

  - **Link local**   O escopo do endereço IPv6 é a sub-rede local. Os endereços de local de link IPv6 são comparáveis aos endereços de local de link IPv4 usados no APIPA (Endereçamento IP Particular Automático).

  - **Local de site**   O escopo do endereço IPv6 é a organização local. Os endereços locais do site foram reprovados pela RFC 3879 e substituídos por endereços locais exclusivos, conforme definido na RFC 4193. Os endereços locais do site IPv6 e os endereços locais exclusivos IPv6 são comparáveis com os endereços IP particulares IPv4.

  - **Global**   O escopo do endereço IPv6 é mundial. Os endereços globais IPv6 são compatíveis aos endereços IP públicos IPv4.

A tabela a seguir fornece uma comparação de elementos IPv4 e IPv6.

### Elementos IPv4 e IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Item</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Endereço IP particular</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>Endereço de local de link</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>Endereços de loopback</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>Endereço não especificado</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>Resolução de endereço</p></td>
<td><p>Protocolo ARP</p></td>
<td><p>ND (Neighbor Discovery)</p></td>
</tr>
<tr class="even">
<td><p>Resolução de nome de host DNS (Sistema de Nomes de Domínio)</p></td>
<td><p>Registro de endereço (registro A)</p></td>
<td><p>Registro AAAA ou registro A6</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre o endereçamento IPv6, consulte [Tipos de endereço IPv6](https://go.microsoft.com/fwlink/p/?linkid=98357).

## Formatos suportados de entrada de endereço IPv6

Os seguintes tipos de formatos de entrada de endereço IPv6 são suportados no Exchange 2013:

  - Um endereço IPv6 único

  - Um intervalo de endereço IPv6

  - Um endereço IPv6 junto com uma máscara de sub-rede

  - Um endereço IPv6 junto a uma máscara de sub-rede que use a notação CIDR (Roteamento entre Domínios sem Classe)

A tabela a seguir oferece exemplos dos formatos de entrada de endereço IPv6 aceitos no Exchange 2013.

### Exemplos de endereço IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo</th>
<th>Exemplo de um endereço IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Endereço único</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Intervalo de endereço</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>Endereço junto com a máscara de sub-rede</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>Endereço junto com máscara de sub-rede que usa notação CIDR</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


No Exchange 2013, os seguintes formatos de entrada têm suporte:

  - Supressão de zeros à esquerda

  - Compactação com dois-pontos duplos

  - Notação decimal com pontos à direita

Voltar ao início

