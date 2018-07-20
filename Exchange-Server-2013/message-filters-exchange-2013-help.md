---
title: 'Filtros de mensagens: Exchange 2013 Help'
TOCTitle: Filtros de mensagens
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 50486136
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtros de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Filtragem gera diferentes modos de exibição das mensagens nas filas. Ao especificar critérios de filtro, você pode localizar mensagens rapidamente e agir neles. Quando uma mensagem de email é enviada para vários destinatários, a mensagem pode estar localizada em várias filas. Quando você filtra por propriedades da mensagem, você pode localizar mensagens em todas as filas. Os cenários a seguir são exemplos de como você pode usar para gerenciar o fluxo de emails de filtragem de mensagens:

  - Fila de envio no servidor de caixa de correio ou servidor de transporte de borda que recebe o email da Internet tem um alto volume de mensagens que estão na fila de entrega. Muitas das mensagens com o mesmo assunto. Portanto, você suspeitar de que o spam está sendo enviada para a sua organização. Você pode criar um filtro para exibir todas as mensagens que atendam aos critérios de assunto. Se você determinar que as mensagens são spam, você pode selecionar todas elas e excluí-los da fila de entrega sem enviar uma notificação de falha na.

  - Um usuário relata que o fluxo de emails está lento. Examinar as filas e consulte que muitas mensagens que tenham assuntos aleatórios parecem ser provenientes de um único domínio. Você pode criar um filtro para exibir todas as mensagens na fila do domínio. Se você determinar que as mensagens são spam, você pode selecionar todas elas e excluí-los a partir das filas sem enviar uma notificação de falha na.

## Propriedades da mensagem como filtros

Você pode usar as propriedades da mensagem para criar um filtro e localizar mensagens que atendam aos critérios especificados. Você pode criar filtros no Visualizador de filas ou usando o parâmetro *Filter* nos cmdlets de gerenciamento de mensagem. Observe que os cmdlets de gerenciamento de mensagem suportar mais propriedades filtráveis do que o Visualizador de filas. A tabela a seguir lista as propriedades da mensagem pelos quais você pode filtrar e os valores que estão associados essas propriedades.

### Propriedades de mensagem para usar ao filtrar mensagens

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriedade de mensagem do Visualizador de fila</th>
<th>Propriedade de mensagem do shell</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Data de recebimento</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>A data/hora de quando a mensagem foi colocada na fila.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>Esta propriedade identifica o motivo pelo qual a mensagem foi adiada. Se a mensagem não foi adiada, essa propriedade tem o valor <code>None</code>. Uma mensagem adiada é retornada para a fila de envio devido a erros transitórios que foram encontrados durante a resolução de destinatário. Para obter mais informações sobre mensagens adiadas, consulte <a href="recipient-resolution-exchange-2013-help.md">Resolução de destinatário</a>. Os valores possíveis são:</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Tempo de expiração</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>Essa propriedade contém a data/hora quando a mensagem expirará e excluída da fila se a mensagem não pode ser entregue.</p></td>
</tr>
<tr class="even">
<td><p><strong>Endereço de</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>Essa propriedade contém o endereço SMTP do remetente.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Essa propriedade é a identidade da mensagem no formato de <em>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</em>. Para obter mais informações, consulte a seção &quot;Identidade da mensagem&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p><strong>ID de mensagem da Internet</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>Essa propriedade contém o valor do campo de cabeçalho <code>Message-ID:</code> localizada no cabeçalho da mensagem. O valor é expresso como um endereço de email que contenha um GUID e o FQDN do servidor SMTP de envio. Por exemplo:</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Último erro</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Essa propriedade contém o texto do último erro que foi registrado para uma mensagem. Por exemplo, <code>A matching connector cannot be found to route the external recipient</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>Essa propriedade contém a quantidade de tempo decorrido entre quando a mensagem primeiro inseridos fila de envio no servidor, e quando a mensagem foi colocada na fila. O valor usa a sintaxe <em>hh:mm:ss.ff</em>, onde <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo e <em>ff</em> = frações de um segundo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Nome da fonte de mensagem</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>Essa propriedade contém uma cadeia de caracteres de texto que indica o nome do componente de transporte que enviou a mensagem para a fila. Por exemplo, se a mensagem foi enviada através de um conector de recebimento, o valor será: <code>SMTP:</code><em>&lt;ConnectorName&gt;</em>. Se a mensagem for uma notificação de status de entrega (DSN), o valor é <code>DSN</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>Priority</code></p></td>
<td><p>Essa propriedade contém a prioridade da mensagem é atribuída pelo usuário no Outlook ou Outlook Web App. Os valores possíveis são <code>Low</code>, <code>Normal</code>e <code>High</code>. Para obter mais informações, consulte <a href="priority-queuing-exchange-2013-help.md">Enfileiramento prioritário</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ID da fila</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>Essa propriedade é a identidade da fila que contém a mensagem. A identidade da fila usa a sintaxe <em>&lt;Server&gt;\&lt;Queue&gt;</em>. Para obter mais informações, consulte a seção &quot;Identidade da fila&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>Esta propriedade identifica o número de vezes que a entrega da mensagem para o destino foi tentada, automática ou manualmente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>O valor da propriedade spam confidence level (SCL) Especifica o SCL da mensagem. Entradas SCL válidas são números inteiros de 0 a 9. Um valor de propriedade SCL vazio indica que a mensagem ainda não foram processada pelo agente de filtro de conteúdo.</p>
<p>Essa propriedade contém o valor de (SCL) nível do spam confidence da mensagem. Entradas SCL válidas são números inteiros de 0 a 9 e -1. Para obter mais informações, consulte <a href="spam-confidence-level-threshold-exchange-2013-help.md">Limite do Nível de Confiança de Spam</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tamanho (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>Esta propriedade indica o tamanho da mensagem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IP de origem</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>Essa propriedade contém o endereço IP do servidor que enviou a mensagem para o servidor do Exchange que contém a mensagem na fila. O endereço pode ser o endereço IP de um servidor SMTP remoto, ou o endereço IP do servidor Exchange local.</p></td>
</tr>
<tr class="even">
<td><p><strong>Status</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Esta propriedade indica o status atual da mensagem. Uma mensagem pode ter um dos seguintes valores de status:</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>Para obter mais informações, consulte a seção &quot;Propriedades de mensagem&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a> .</p></td>
</tr>
<tr class="odd">
<td><p><strong>Assunto</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>Esta propriedade indica o assunto de uma mensagem que for encontrado no campo de cabeçalho <code>Subject:</code> no cabeçalho da mensagem.</p></td>
</tr>
</tbody>
</table>

