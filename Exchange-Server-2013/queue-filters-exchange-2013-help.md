---
title: 'Filtros de fila: Exchange 2013 Help'
TOCTitle: Filtros de fila
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 50487072
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtros de fila

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Filtragem gera diferentes modos de exibição das filas. Você pode usar as propriedades da fila como opções de filtro. Ao especificar critérios de filtro, você pode rapidamente localizar filas e agir neles. Os cenários a seguir são exemplos de como você pode usar para gerenciar o fluxo de emails de filtragem de fila:

  - Você recebe uma mensagem do Microsoft System Center Operations Manager que indica que um comprimento de fila excedeu o limite estabelecido. Você deseja investigar se um problema de fluxo de email de todo o servidor existe.
    
    Você pode criar um filtro para exibir todas as filas que têm uma contagem de mensagem que exceda o que você considere típica. Se um problema de fluxo de email é indicado, selecione todas as filas nos resultados de filtro e suspender as filas de espera enquanto você continuar a investigar.

  - Suspender a várias filas para investigar a causa de problemas de fluxo de email. Determinar que o problema foi causado por uma configuração incorreta de conector e agora é fixo.
    
    Você pode criar um filtro para exibir todas as filas que têm um status de Suspended e, em seguida, selecione todas as filas nos resultados de filtro e retomar as filas.

## Propriedades da fila para usar ao filtrar filas

Você pode usar as propriedades de fila para criar um filtro e localizar filas que satisfazem os critérios especificados. Você pode criar filtros no Visualizador de filas ou usando o parâmetro *Filter* nos cmdlets de gerenciamento de fila. Observe que os cmdlets de gerenciamento de fila suportar mais propriedades filtráveis do que o Visualizador de filas. A tabela a seguir lista as propriedades de fila pelo qual você pode filtrar e os valores válidos para essas propriedades.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriedade de fila do Visualizador de fila</th>
<th>Propriedade de fila do shell</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>Esta propriedade identifica o número de mensagens que foram retornados para a fila de envio devido a erros transitórios que foram encontrados durante a resolução de destinatário. Para obter mais informações sobre mensagens adiadas, consulte <a href="recipient-resolution-exchange-2013-help.md">Resolução de destinatário</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo de entrega</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p>Os valores válidos para <strong>DeliveryType</strong> são explicados na seção &quot;NextHopSolutionKey&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Essa propriedade é a identidade da fila na forma de <em>&lt;Server&gt;\&lt;Queue&gt;</em>. Para obter mais informações, consulte a seção &quot;Identidade da fila&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>Essa propriedade é um número calculado que indica a rapidez mensagens estão entrando na fila. Para obter mais informações, consulte a seção &quot;IncomingRate, OutgoingRate e Velocity&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="odd">
<td><p><strong>Último erro</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Esta propriedade indica a cadeia de caracteres de texto do último erro que foi registrada para a fila.</p></td>
</tr>
<tr class="even">
<td><p><strong>Hora da última tentativa</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>Esta propriedade indica a data/hora da última tentativa de conexão para uma fila que tem um status de <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>Essa propriedade está reservada para uso interno da Microsoft e não será usada em organizações de Exchange 2013 local.</p></td>
</tr>
<tr class="even">
<td><p><strong>Contagem de mensagem</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>Esta propriedade indica o número de mensagens na fila.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>Essa propriedade designa o próximo salto da fila como <code>Internal</code> ou <code>External</code> e baseia-se no valor da propriedade <strong>DeliveryType</strong> da fila. Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>Essa propriedade é o GUID do próximo salto e baseia-se no valor da propriedade <strong>DeliveryType</strong> da fila. Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="odd">
<td><p><strong>Domínio do próximo salto</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>Essa propriedade é o nome do próximo salto e baseia-se no valor da propriedade <strong>DeliveryType</strong> da fila. Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p><strong>Hora da próxima tentativa</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>Esta propriedade indica a data/hora da próxima tentativa de conexão de uma fila que tem um status de <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>Essa propriedade é um número calculado que indica a rapidez as mensagens estão deixando a fila. Para obter mais informações, consulte a seção &quot;IncomingRate, OutgoingRate e Velocity&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>Essa propriedade está reservada para uso interno da Microsoft e não será usada em organizações de Exchange 2013 local.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Status</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Esta propriedade indica o status atual da fila. Uma fila pode ter um dos seguintes valores de status ativo, se conectando, nenhum, suspensas, pronto, ou tente novamente. Para obter mais informações, consulte a seção &quot;Status de fila&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>Essa propriedade contém o FQDN do domínio de destino, se o domínio estiver configurado para segurança de domínio.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>Essa propriedade contém um número calculado que indica como efetivamente a fila está descarregando. Para obter mais informações, consulte a seção &quot;IncomingRate, OutgoingRate e Velocity&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
</tbody>
</table>

