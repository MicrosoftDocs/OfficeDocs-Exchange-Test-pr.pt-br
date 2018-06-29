---
title: 'Usar o Shell de gerenciamento do Exchange para gerenciar filas: Exchange 2013 Help'
TOCTitle: Usar o Shell de gerenciamento do Exchange para gerenciar filas
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51407860
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar o Shell de gerenciamento do Exchange para gerenciar filas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Como nas versões anteriores do Exchange, você pode usar o Shell de Gerenciamento do Exchange no Microsoft Exchange Server 2013 para exibir informações sobre as filas e as mensagens nessas filas e para executar ações de gerenciamento em filas e mensagens. No Exchange 2013, filas existem em servidores de transporte de borda e servidores de caixa de correio. Este tópico refere-se a esses servidores como *servidores de transporte*.

Quando você usar o Shell para exibir e gerenciar filas e mensagens em filas de servidores de transporte, é importante entender como identificar as filas ou mensagens que você deseja gerenciar. Normalmente, os servidores de transporte contêm um grande número de filas e mensagens a serem entregues. Você usa os parâmetros de filtragem disponíveis nos cmdlets de gerenciamento de filas e mensagens para identificar as filas ou mensagens que deseja exibir ou gerenciar.

Observe que você também pode usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para gerenciar filas e mensagens em filas. No entanto, a fila e a mensagem que exibem cmdlets oferecem suporte a mais propriedades filtráveis e opções de filtro do que o Visualizador de Filas. Para obter mais informações sobre como usar o Visualizador de Filas, consulte [Visualizador de Filas](queue-viewer-exchange-2013-help.md).

**Sumário**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## Parâmetros de filtragem de fila

A tabela a seguir descreve os parâmetros de filtragem disponíveis nos cmdlets de gerenciamento de fila.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parâmetros de filtragem</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p>Não é possível usar o parâmetro <em>Identity</em> no mesmo comando do parâmetro <em>Filter</em>. É possível usar os parâmetros <em>Include</em> e <em>Exclude</em> com o parâmetro <em>Filter</em> no mesmo comando.</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>Você deve usar o parâmetro <em>Identity</em> ou o parâmetro <em>Filter</em>, mas não pode usar ambos no mesmo comando.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p>Você deve usar o parâmetro <em>Server</em>, <em>Dag</em>, <em>Site</em> ou <em>Forest</em>, mas não pode usar nenhum deles juntos no mesmo comando. É possível usar o parâmetro <em>Filter</em> com qualquer um dos outros parâmetros de filtragem.</p></td>
</tr>
</tbody>
</table>


Observe que um parâmetro *Server* está disponível em todos os cmdlets de gerenciamento de fila. No cmdlet **Get-QueueDigest**, o parâmetro *Server* é um parâmetro de escopo que especifica os servidores dos quais você deseja exibir informações de resumo sobre filas. Em todos os outros cmdlets de gerenciamento de fila, você usa o parâmetro *Server* para se conectar a um servidor específico e executar comandos de gerenciamento de fila no servidor. Você pode usar o parâmetro *Server*, com ou sem o parâmetro *Filter*, mas não pode usar o parâmetro *Server* com o parâmetro *Identity*. Você usa o FQDN ou o nome do host do servidor de transporte com o parâmetro *Server*.

Voltar ao início

## Identidade da fila

O parâmetro *Identity* nos cmdlets de gerenciamento de fila identifica uma fila específica. Quando você usa o parâmetro *Identity*, não pode especificar nenhum outro parâmetro de filtragem de fila, pois já identificou a fila exclusivamente. O parâmetro *Identity* usa a sintaxe básica *\<Servidor\>*\\*\<Fila\>*.

O espaço reservado *\<Servidor\>* é o nome de host ou FQDN do Exchange Server, por exemplo, `mailbox01` ou `mailbox01.contoso.com`. Se você omitir o qualificador de *\<Servidor\>*, o servidor local está implícito.

O espaço reservado \<*Fila*\> aceita um dos seguintes valores:

  - **Nome de fila persistente** Filas persistentes têm nomes exclusivos e consistentes em todos os servidores de caixa de correio ou transporte de borda. Os nomes de fila persistentes são:
    
      - **Envio**   Esta fila contém mensagens aguardando para serem processadas pelo categorizador.
    
      - **Inacessível**   Esta fila contém mensagens que não podem ser encaminhadas. Esta fila não existe até que as mensagens sejam colocadas nela.
    
      - **Suspeita** Esta fila contém mensagens que são consideradas perigosas para o Exchange Server. Esta fila não existe até que as mensagens sejam colocadas nela.

  - **Nome da fila de entrega**   O nome de uma fila de entrega é o valor da propriedade **NextHopDomain** da fila. Por exemplo, o nome da fila poderia ser o espaço de endereçamento de um conector de envio, o nome de um site do Active Directory ou o nome de um DAG. Para obter mais informações, consulte a seção "NextHopSolutionKey", no tópico [Filas](queues-exchange-2013-help.md).

  - **Inteiro de fila**   Filas de entrega e de sombra são atribuídas um valor inteiro exclusivo no banco de dados de fila. No entanto, você precisa executar o cmdlet **Get-Queue** para localizar o valor inteiro nas propriedades **Identity** ou **QueueIdentity**.

  - **Nome da fila de sombra**   Uma fila de sombra usa a sintaxe `Shadow\`*\<QueueInteger\>*

A tabela a seguir resume a sintaxe que você pode usar com o parâmetro *Identity* nos cmdlets de gerenciamento de fila. Em todos os valores, *\<Servidor\>* é o nome do host ou FQDN do servidor.

### Formatos de identidade da fila

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor do parâmetro de identidade</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> ou <code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>Uma fila persistente no servidor especificado ou no servidor local.</p>
<p><em>&lt;Nome_fila_persistente&gt;</em> é <code>Submission</code>, <code>Unreachable</code> ou <code>Poison</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> ou <code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>Uma fila de entrega no servidor especificado ou no servidor local.</p>
<p><em>&lt;NextHopDomain&gt;</em> é um grupo de roteamento de destino ou entrega das mensagens na fila. Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot;, no tópico <a href="queues-exchange-2013-help.md">Filas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> ou <code>&lt;QueueInteger&gt;</code></p></td>
<td><p>Uma fila de entrega no servidor especificado ou no servidor local.</p>
<p><em>&lt;QueueInteger&gt;</em> é um valor inteiro exclusivo da fila exibida na propriedade <strong>Identity</strong> do cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> ou <code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>Uma fila de sombra no servidor especificado ou no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> ou <code>*</code></p></td>
<td><p>Todas as filas no servidor especificado ou no servidor local. Observe que estes valores só podem ser usados com o cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Parâmetro de filtro de fila

Você pode usar o parâmetro *Filter* em todos os cmdlets de gerenciamento de fila para especificar que deseja exibir ou gerenciar filas baseadas nas propriedades das filas. O parâmetro *Filter* cria uma expressão com operadores de comparação que restringe a operação de fila para filas que atendem aos critérios do filtro. É possível usar o operador lógico `-and` para especificar várias condições que devem ser correspondentes aos resultados.

Para obter uma lista completa de propriedades de fila, que você pode usar com o parâmetro *Filter*, consulte [Filas](queues-exchange-2013-help.md).

Para uma lista de operadores de comparação, que você pode usar com o parâmetro *Filter*, consulte a seção Comparison operators to use when filtering queues or messages neste tópico.

Para exemplos de procedimentos que usam o parâmetro *Filter* para exibir e gerenciar filas, consulte [Gerenciar filas](manage-queues-exchange-2013-help.md).

Voltar ao início

## Incluir e excluir parâmetros

O Exchange 2013 tem os parâmetros *Include* e *Exclude* disponíveis no cmdlet `Get-Queue`. Você pode usar estes parâmetros individualmente, juntos, e com o parâmetro *Filter* para ajustar seus resultados de fila no servidor de transporte local ou especificado. Por exemplo, você pode:

  - Exclua filas vazias de resultados.

  - Exclua filas para destinos externos dos resultados.

  - Inclua filas que têm um valor específico de **DeliveryType** nos resultados.

Os parâmetros *Include* e *Exclude* usam as seguintes propriedades de fila para filtrar filas:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Descrição</th>
<th>Exemplo de código do Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>Este valor inclui ou exclui filas baseadas na propriedade <strong>DeliveryType</strong>. Vários valores, separados por vírgulas, podem ser especificados. Os valores válidos para <strong>DeliveryType</strong> são explicados na seção &quot;NextHopSolutionKey&quot; no tópico <a href="queues-exchange-2013-help.md">Filas</a>.</p></td>
<td><p>Este exemplo retorna todas as filas de entrega no servidor local onde o próximo salto é um conector de envio no servidor local que é configurado para roteamento de host inteligente:</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>Este valor inclui ou exclui filas vazias. Filas vazias têm o valor <code>0</code> na propriedade <strong>MessageCount</strong>.</p></td>
<td><p>Este exemplo retorna todas as filas no servidor local que contém mensagens</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>Este valor inclui ou exclui filas que têm o valor <code>External</code> na propriedade <strong>NextHopCategory</strong>.</p>
<p>Filas externas sempre têm um dos seguintes valores para <strong>DeliveryType</strong>:</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot;, no tópico <a href="queues-exchange-2013-help.md">Filas</a>.</p></td>
<td><p>Este exemplo retorna todas as filas internas no servidor local</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>Este valor inclui ou exclui filas que têm o valor <code>Internal</code> na propriedade <strong>NextHopCategory</strong>. Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot;, no tópico <a href="queues-exchange-2013-help.md">Filas</a>.</p></td>
<td><p>Este exemplo retorna todas as filas internas no servidor local.</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


Observe que você pode duplicar a funcionalidade dos parâmetros *Include* e *Exclude* usando o parâmetro de *Filter*. Por exemplo, o comando `Get-Queue -Exclude Empty` produz o mesmo resultado que `Get-Queue -Filter {MessageCount -gt 0}`. No entanto, a sintaxe dos parâmetros *Include* e *Exclude* é mais simples e fácil de lembrar.

Voltar ao início

## Get-QueueDigest

O Exchange 2013 adiciona um novo cmdlet de fila chamado **Get-QueueDigest**. Esse cmdlet permite exibir informações sobre algumas ou todas as filas em sua organização do Exchange com um único comando. Especificamente, o cmdlet **Get-QueueDigest** permite que você exiba informações sobre filas com base em sua localização nos servidores, em DAGs, nos sites do Active Directory ou em toda a floresta do Active Directory. Observe que filas em um servidor de Transporte de Borda inscrito na rede de perímetro não são incluídas nos resultados. Além disso, **Get-QueueDigest** está disponível em um servidor de Transporte de Borda, mas os resultados estão restritos a filas no servidor de Transporte de Borda.


> [!TIP]
> Por padrão, o cmdlet <STRONG>Get-QueueDigest</STRONG> exibe as filas de entrega que contenham dez ou mais mensagens e os resultados são de um a dois minutos atrás. Para instruções sobre como alterar estes valores padrões, consulte <A href="configure-get-queuedigest-exchange-2013-help.md">Configurar Get-QueueDigest</A>.



Os parâmetros de filtragem e classificação disponíveis no cmdlet **Get-QueueDigest** são descritos na tabela a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Dag</em>, <em>Server</em> ou <em>Site</em></p></td>
<td><p>Esses parâmetros são mutuamente exclusivos e definem o escopo do cmdlet. Você deve especificar um destes parâmetros ou a opção <em>Forest</em>. Normalmente, você usaria o nome do servidor, site do DAG ou Active Directory, mas pode usar qualquer valor que identifique exclusivamente o servidor, DAG ou site. Você pode especificar vários servidores, DAGs ou sites separados por vírgulas.</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>Esta opção é necessária quando você está usando os parâmetros <em>Dag</em>, <em>Server</em> ou <em>Site</em>. Você não especifica um valor com essa opção. Usando essa opção, você tem filas de todos os servidores de caixa de correio do Exchange 2013 na floresta do Active Directory. Você não pode usar a opção <em>Forest</em> para exibir filas em florestas remotas do Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>Este parâmetro aceita os valores <code>None</code>, <code>Normal</code> e <code>Verbose</code>. O valor padrão é <code>Normal</code>. Quando você usa o valor <code>None</code>, o nome de fila é omitido da coluna de <strong>Detalhes</strong> nos resultados.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Este parâmetro permite que você filtre filas com base nas propriedades de fila. Você pode usar qualquer uma das propriedades de fila filtráveis, como descrito no tópico <a href="queue-filters-exchange-2013-help.md">Filtros de fila</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>Este parâmetro agrupa os resultados da fila. Você pode agrupar os resultados por uma das seguintes propriedades:</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Status</p></li>
<li><p>ServerName</p></li>
</ul>
<p>Por padrão, os resultados são agrupados por <code>NextHopDomain</code>. Para obter informações sobre essas propriedades da fila, consulte <a href="queue-filters-exchange-2013-help.md">Filtros de fila</a>.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Este parâmetro limita os resultados da fila para o valor que você especificar. As filas são classificadas em ordem decrescente com base no número de mensagens na fila, e agrupadas pelo valor especificado pelo parâmetro <em>GroupBy</em>. O valor padrão é 1000. Isto quer dizer que, por padrão, o comando exibe as principais 1000 filas agrupadas por <strong>NextHopDomain</strong>, e classificadas pelas filas que contêm a maioria das mensagens com relação às filas que contêm menos mensagens.</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>O parâmetro especifica o número de segundos antes da operação expirar. O valor padrão é <code>00:00:10</code> ou 10 segundos.</p></td>
</tr>
</tbody>
</table>


Este exemplo retorna todas as filas externas não vazias nos servidores de Caixa de Correio do Exchange 2013 chamadas Mailbox01,Mailbox02 e Mailbox03.

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

Voltar ao início

## Parâmetros de filtragem de mensagem

A tabela a seguir descreve os parâmetros de filtragem disponíveis nos cmdlets de gerenciamento de mensagens.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parâmetros de filtragem</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>Todos os parâmetros de filtragem são mutuamente exclusivos, e você pode usá-los juntos no mesmo comando.</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>Você deve usar o parâmetro <em>Identity</em> ou o parâmetro <em>Filter</em>, mas não pode usar ambos no mesmo comando.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p>O parâmetro <em>Identity</em> é obrigatório.</p></td>
</tr>
</tbody>
</table>


Observe que um parâmetro *Server* está disponível em todos os cmdlets de gerenciamento de mensagens para o cmdlet **Export-Message**. Você usa o parâmetro *Server* para se conectar a um servidor específico e executar comandos de gerenciamento de mensagens no servidor. Você pode usar o parâmetro *Server*, com ou sem o parâmetro *Filter*, mas não pode usar o parâmetro *Server* com o parâmetro *Identity*. Você usa o FQDN ou o nome do host do servidor de transporte com o parâmetro *Server*.

Voltar ao início

## Identidade da mensagem

O parâmetro *Identity* nos cmdlets de gerenciamento de mensagens identifica uma mensagem específica em uma ou mais filas. Quando você usa o parâmetro *Identity*, não pode especificar nenhum outro parâmetro de filtragem de mensagem, pois já identificou a mensagem exclusivamente. O parâmetro *Identity* usa a sintaxe básica *\<Servidor\>*\\*\<Fila\>*\\*\<MessageInteger\>*..

O espaço reservado *\<Servidor\>* é o nome de host ou FQDN do Exchange Server, por exemplo, `mailbox01` ou `mailbox01.contoso.com`. Se você omitir o qualificador de *\<Servidor\>*, o servidor local está implícito.

O espaço reservado \<*Fila*\> aceita a identidade da fila como descrito na seção "Identidade da fila" neste tópico. Por exemplo, você pode usar o nome da fila persistente, o valor **NextHopDomain** ou o valor de número inteiro exclusivo da fila no banco de dados de fila.

O espaço reservado *\<MessageInteger\>* representa o valor de inteiro exclusivo que é atribuído à mensagem quando ele entra pela primeira vez no banco de dados de fila no servidor. Se a mensagem é enviada para vários destinatários que exigem várias filas, todas as cópias da mensagem em todas as filas do banco de dados de fila têm o mesmo valor de número inteiro. No entanto, você precisa executar o cmdlet **Get-Message** para localizar o valor inteiro da mensagem nas propriedades **Identity** ou **MessageIdentity**.

A tabela a seguir resume a sintaxe que você pode usar com o parâmetro *Identity* nos cmdlets de gerenciamento de mensagens. Em todos os valores, *\<Servidor\>* é o nome do host ou FQDN do servidor.

### Formatos de identidade da mensagem

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor do parâmetro de identidade</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> ou <code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>Uma mensagem em uma fila específica no servidor especificado ou no servidor local.</p>
<p><em>&lt;MessageInteger&gt;</em> é um valor inteiro exclusivo da mensagem exibida na propriedade <strong>Identity</strong> do cmdlet <strong>Get-Message</strong>.</p>
<p><em>&lt;Fila&gt;</em> representa um dos seguintes valores:</p>
<ul>
<li><p><strong>Nome de fila persistente</strong>   O valor <code>Submission</code>, <code>Unreachable</code> ou <code>Poison</code>.</p></li>
<li><p><strong>Nome da fila de entrega</strong>   O valor da propriedade <strong>NextHopDomain</strong> da fila, que é efetivamente o nome da fila. Esse valor poderia ser um destino de roteamento ou um grupo de entrega. Para obter mais informações, consulte a seção &quot;NextHopSolutionKey&quot;, no tópico <a href="queues-exchange-2013-help.md">Filas</a>.</p></li>
<li><p><strong>Queue integer</strong>   O valor inteiro exclusivo da fila de entrega ou da fila de sombra que é exibido na propriedade <strong>Identity</strong> dos cmdlets <strong>Get-Message</strong> ou <strong>Get-Queue</strong>.</p></li>
<li><p><strong>Identidade da fila de sombra</strong>   Uma identidade da fila de sombra usa a sintaxe <code>Shadow\&lt;QueueInteger&gt;</code>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code> ou <code>*\&lt;MessageInteger&gt;</code> ou <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>Todas as cópias da mensagem em todas as filas do banco de dados de fila no servidor especificado ou no servidor local.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Parâmetro de filtro de mensagem

Você pode usar o parâmetro *Filter* nos cmdlets **Get-Message**, **Remove-Message**, **Resume-Message** e **Suspend-Message** para especificar as mensagens que deseja exibir ou gerenciar com base nas propriedades das mensagens. O parâmetro *Filter* cria uma expressão com operadores de comparação que restringe a operação de mensagem para mensagens que atendem aos critérios do filtro. É possível usar o operador lógico `-and` para especificar várias condições que devem ser correspondentes aos resultados.

Para obter uma lista completa de propriedades de mensagem, que você pode usar com o parâmetro *Filter*, consulte [Filas](queues-exchange-2013-help.md).

Para uma lista de operadores de comparação, que você pode usar com o parâmetro *Filter*, consulte a seção Comparison operators to use when filtering queues or messages neste tópico.

Para exemplos de procedimentos que usam o parâmetro *Filter* para exibir e gerenciar mensagens, consulte [Gerenciar filas](manage-queues-exchange-2013-help.md).

Voltar ao início

## Parâmetro de fila

O parâmetro *Queue* é usado somente no cmdlet **Get-Message**. Você pode usar esse parâmetro para obter todas as mensagens em uma fila específica ou todas as mensagens de várias filas usando o caractere curinga (\*). Quando você usar o parâmetro *Queue*, use o formato de identidade da fila *\<Servidor\>*\\*\<Fila\>* conforme descrito na seção "Identidade da fila" neste tópico.

Voltar ao início

## Operadores de comparação para usar ao filtrar filas ou mensagens

Quando você cria uma expressão de filtro de fila ou mensagem usando o parâmetro *Filter*, deve incluir um operador de comparação para o valor da propriedade corresponder. A tabela seguinte mostra os operadores de comparação que podem ser usados em uma expressão de filtro e como cada operador funciona. Para todos os operadores, os valores em comparação não diferenciam maiúsculas de minúsculas.

### Operadores de comparação

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operador</th>
<th>Função</th>
<th>Exemplo de código do Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>Este operador é usado para especificar que os resultados devem corresponder exatamente ao valor da propriedade fornecido na expressão.</p></td>
<td><p>Para exibir uma lista de todas as filas que tenham o status Repetir (Retry):</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>Para exibir uma lista de todas as mensagens que têm o status Repetir (Retry):</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>Este operador é usado para especificar que os resultados não devem corresponder ao valor da propriedade fornecido na expressão.</p></td>
<td><p>Para exibir uma lista de todas as filas que não possuem o status Ativa (Active):</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>Para exibir uma lista de todas as mensagens que não possuem o status Ativa (Active):</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>Esse operador é usado com propriedades em que o valor é expresso como um número inteiro ou de data/hora. Os resultados do filtro só incluem filas ou mensagens onde o valor da propriedade especificado é maior que o valor fornecido na expressão.</p></td>
<td><p>Para exibir uma lista das filas que atualmente possuem mais de 1.000 mensagens:</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>Para exibir uma lista de mensagens que atualmente têm uma contagem de repetição maior que 3:</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>Esse operador é usado com propriedades em que o valor é expresso como um número inteiro ou de data/hora. Os resultados do filtro só incluem filas ou mensagens onde o valor da propriedade especificado é maior ou igual ao valor que é fornecido na expressão.</p></td>
<td><p>Para exibir uma lista das filas que atualmente possuem 1.000 mensagens ou mais:</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>Para exibir uma lista de mensagens que atualmente têm uma contagem de repetição maior ou igual a 3:</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>Esse operador é usado com propriedades em que o valor é expresso como um número inteiro ou de data/hora. Os resultados do filtro só incluem filas ou mensagens onde o valor da propriedade especificado é menor que o valor fornecido na expressão.</p></td>
<td><p>Para exibir uma lista das filas que atualmente possuem menos de 1.000 mensagens:</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>Para exibir uma lista de mensagens que têm um SCL inferior a 6:</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>Esse operador é usado com propriedades em que o valor é expresso como um número inteiro ou de data/hora. Os resultados do filtro só incluem filas ou mensagens onde o valor da propriedade especificado é menor ou igual ao valor fornecido na expressão.</p></td>
<td><p>Para exibir uma lista das filas que atualmente possuem 1.000 mensagens ou menos:</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>Para exibir uma lista de mensagens que têm um SCL menor ou igual a 6:</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>Este operador é usado com propriedades em que o valor é expresso como uma cadeia de caracteres de texto. Os resultados do filtro só incluem filas ou mensagens onde o valor da propriedade especificado contém a sequência de caracteres de texto fornecida na expressão. Você pode incluir o caractere curinga (*) em uma expressão <strong>-like</strong> aplicada a um campo da cadeia de caracteres de texto, mas não a um campo do tipo enumeração.</p></td>
<td><p>Para exibir uma lista de filas de entrega com destino para qualquer domínio SMTP que termine em Contoso.com:</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>Para exibir uma lista de mensagens cujo assunto contenha o texto &quot;payday loan&quot; (&quot;empréstimo de dia de pagamento&quot;):</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


Você pode especificar um filtro que avalia várias expressões usando o operador de comparação **-and**. As filas ou mensagens devem satisfazer todas as condições do filtro a ser incluído nos resultados.

Este exemplo exibe uma lista de filas que tenham um destino para qualquer nome de domínio SMTP que termina em Contoso.com e que atualmente contém mais de 500 mensagens.

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

Este exemplo exibe uma lista de mensagens enviadas de qualquer endereço de email no domínio contoso.com que tenham um SCL maior que 5.

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

Voltar ao início

## Parâmetros de paginação avançados

Dependendo do fluxo de mensagens atual, as consultas em filas e mensagens podem retornar um conjunto de objetos grande. Você pode usar os parâmetros de paginação avançada para controlar como os resultados da consulta são recuperados e exibidos.

Quando você usar o Shell para exibir filas e as mensagens nas filas, sua consulta recuperará uma página de informações de cada vez. Os parâmetros de paginação avançada controlam o tamanho do conjunto de resultados e também podem ser usados para classificar os resultados. Todos os parâmetros de paginação avançada são opcionais e podem ser combinados a qualquer um dos conjuntos de parâmetros que podem ser usados com os cmdlets **Get-Queue** e **Get-Message**. Se nenhum parâmetro de paginação avançada for especificado, a consulta retornará os resultados na ordem crescente de identidade.

Por padrão, quando uma ordem de classificação é especificada, a propriedade de identidade da mensagem é sempre incluída e classificada na ordem crescente. Este é o relacionamento de ordenação padrão. A propriedade de identidade da mensagem é incluída, pois as outras propriedades que podem ser incluídas em uma ordem de classificação não são exclusivas. Ao incluir explicitamente a propriedade de identidade da mensagem na ordem de classificação, você pode especificar que os resultados exibam a identidade da mensagem armazenada em ordem decrescente.

É possível usar os parâmetros *BookmarkIndex* e *BookmarkObject* para marcar uma posição no conjunto de resultados classificados. Se o objeto indicador não existir mais quando a próxima página de resultados for recuperada, o relacionamento de ordenação padrão verificará se o conjunto de resultados começa com o objeto mais próximo ao indicador. O objeto mais próximo depende da ordem de classificação especificada.

A tabela a seguir descreve os parâmetros de paginação avançada.

### Parâmetros de paginação avançados

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BookmarkIndex</em></p></td>
<td><p>Este parâmetro especifica a posição no conjunto de resultados, onde começam os resultados exibidos. O valor deste parâmetro é um índice baseado em 1 no conjunto de resultados total. Se o valor for menor ou igual a zero, a primeira página de resultados completa será retornada. Se o valor for definido como <code>Int.MaxValue</code>, a última página completa de resultados será retornada.</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>Este parâmetro especifica o objeto no conjunto de resultados onde começam os resultados exibidos. Se você especificar um objeto indicador, esse objeto será usado como o ponto para iniciar a pesquisa. As linhas antes ou depois desse objeto, dependendo do valor do parâmetro <em>SearchForward</em>, são recuperadas. Não é possível combinar o parâmetro <em>BookmarkObject</em> e o parâmetro <em>BookmarkIndex</em> em uma única consulta.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>Este parâmetro especifica se o objeto indicador será incluído no conjunto de resultados. Por padrão, o valor é definido como <code>$true</code> e o objeto indicador é incluído. Você pode executar uma consulta para um tamanho limitado de resultados e, em seguida, especificar o último item no conjunto de resultados como o indicador para a próxima consulta. Neste caso, talvez você queira definir <em>IncludeBookmark</em> como <code>$false</code>, de forma que o objeto não seja incluído nos dois conjuntos de resultados.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Este parâmetro especifica o número de resultados a exibir por página. Se você não especificar um valor, o tamanho do resultado padrão de 1.000 objetos será usado. O Exchange limita o conjunto de resultados a 250.000.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>Este parâmetro é um parâmetro oculto. Ele retorna informações sobre o número total de resultados e o índice do primeiro objeto da página atual. O valor padrão é <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>Este parâmetro especifica se deve pesquisar para frente ou para trás no conjunto de resultados. Esse parâmetro não afeta a ordem em que o conjunto de resultados é retornado. Ele determina a direção de cada pesquisa em relação ao índice ou objeto indicador. Se nenhum índice ou objeto indicador for especificado, o parâmetro <em>SearchForward</em> determinará se a pesquisa começa a partir do primeiro ou do último objeto no conjunto de resultados.</p>
<p>O valor padrão deste parâmetro é <code>$true</code>. Se este parâmetro for definido como <code>$true</code> e um indicador for especificado, a consulta pesquisará para frente a partir desse indicador. Se você usar essa configuração e não houver resultados depois do indicador, a consulta retornará a última página completa de resultados.</p>
<p>Se o parâmetro <em>SearchForward</em> for definido como <code>$false</code> e um indicador for especificado, a consulta pesquisará para trás a partir desse indicador. Se você usar essa configuração e houver menos de uma página completa de resultados depois do indicador, a consulta retornará a primeira página completa de resultados.</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>Este parâmetro especifica uma matriz de propriedades de mensagem usada para controlar a ordem de classificação do conjunto de resultados. As propriedades da ordem de classificação são especificadas na ordem decrescente de precedência. Cada propriedade é separada por uma vírgula, e um sinal de mais (+) é acrescentado para classificar em ordem crescente, ou um sinal de menos (-) para classificar em ordem decrescente.</p>
<p>Se uma ordem de classificação explícita não for especificada por meio desse parâmetro, os registros que correspondem à consulta serão exibidos e classificados pelo campo Identidade do respectivo tipo de objeto. Os resultados são sempre classificados por identidade na ordem crescente, quando uma ordem de classificação não é explicitamente especificada.</p></td>
</tr>
</tbody>
</table>


O exemplo de código a seguir mostra como usar os parâmetros de paginação avançada em uma consulta. Neste exemplo, o comando conecta ao servidor especificado e recupera um conjunto de resultados que contém 500 objetos. Os resultados são exibidos em uma ordem classificada, primeiro na ordem crescente por endereço do remetente e, em seguida, na ordem decrescente de tamanho da mensagem.

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

Se você desejar exibir páginas sucessivas, poderá definir um indicador para o último objeto recuperado em um conjunto de resultados e executar uma consulta adicional. Você precisa usar os recursos de script do Shell para executar este procedimento.

O exemplo a seguir usa script para recuperar a primeira página de resultados, define o objeto indicador, exclui o objeto indicador do conjunto de resultados e, em seguida, recupera os próximos 500 objetos no servidor especificado.

1.  Abra o Shell e digite o seguinte comando para recuperar a primeira página de resultados.
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  Para definir o objeto indicador, digite o seguinte comando para salvar o último elemento da primeira página em uma variável.
    
        $temp=$results[$results.length-1]

3.  Para recuperar os próximos 500 objetos no servidor especificado e excluir o objeto indicador, digite o seguinte comando.
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

Voltar ao início

