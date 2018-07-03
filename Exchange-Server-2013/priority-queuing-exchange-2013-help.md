---
title: 'Enfileiramento prioritário: Exchange 2013 Help'
TOCTitle: Enfileiramento prioritário
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51407870
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Enfileiramento prioritário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

*Filas com prioridade* é um recurso do Microsoft Exchange Server 2013 que permite que a prioridade definida pelo remetente de uma mensagem influencie no processamento da mensagem pelo serviço de Transporte no servidor da Caixa de Correio.

A prioridade da mensagem é atribuída pelo remetente no Microsoft Outlook quando o rementente cria e envia a mensagem. O remetente pode definir qualquer um dos valores de prioridade a seguir no Outlook:

  - Baixa prioridade

  - Prioridade normal

  - Alta prioridade

A prioridade padrão para uma mensagem criada no Outlook ou no Outlook Web App é a Prioridade normal. A prioridade da mensagem é armazenada do campo de cabeçalho `X-Priority`, no cabeçalho da mensagem.

Cada mensagem enviada ou recebida em uma organização do Exchange 2013 deve ser categorizada pelo serviço de transporte em um servidor da Caixa de Entrada antes de ser roteada e entregue. O categorizador no serviço de Transporte em um servidor de Caixa de Correio escolhe uma mensagem de cada vez da Fila de Envio e resolve o destinatário, o roteamento e a conversão de conteúdo da mensaem antes de colocar a mensagem em uma fila de entrega. Para obter mais informações, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md).

Filas de envio são criadas dinamicamente com base no destino da mensagem. Para obter mais informações, consulte [Filas](queues-exchange-2013-help.md).

Todas as mensagens com o mesmo destino são colocadas na mesma fila de entrega. A fila com prioridades afeta a transmissão das mensagens de uma fila de entrega para o servidor de mensagens de destino. Quando a fila com prioridades é habilitada, mensagens com Alta prioridade são transmitidas aos seus destinos antes das mensagens com Prioridade normal, e estas são transmitidas antes das que têm Baixa prioridade. A entrega de mensagens classificada de acordo com a prioridade da mensagem pode ajudar os você a definir requisitos de SLA (acordo de nível de serviço) para tempo de entrega de mensagens.

## Opções para configurar as filas com prioridade

O suporte para filas com prioridade é controlado por chaves no arquivo de configuração aplicativo XML `%ExchangeInstallPath%bin\EdgeTransport.exe.config` . Para instruções sobre como configurar as filas com prioridade, veja [Habilitar e configurar o enfileiramento prioritário](enable-and-configure-priority-queuing-exchange-2013-help.md).

A tabela a seguir explica cada chave com mais detalhes.

### Chaves das filas prioridade no arquivo EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>Esta chave habilita ou desabilita as filas com prioridade no serviço de Transporte no servidor da Caixa de Correio. A entrada válida para esta chave é <code>true</code> ou <code>false</code>.</p>
<p>Quando esta chave é <code>false</code>, as filas com prioridade são desabilitadas e todos os limites de mensagem das filas com prioridade que existem no arquivo EdgeTransport.exe.config são ignorados.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>Esta chave especifica o tamanho máximo permitido de uma mensagem de Alta prioridade. Se uma mensagem de Alta prioridade for maior do que o valor especificado por esta chave, a mensagem é automaticamente rebixada de Alta prioridade para Prioridade normal.</p>
<p>O valor desta chave deve ser significativamente menor do que o valor do parâmetro <em>MaxSendMessageSize</em> no cmdlet <strong>Set-TransportConfig</strong> . O valor padrão deste parâmetro é <code>10 MB</code>. A diferença entre esses dois valores ajuda a garantir tempos de entrega consistentes e previsíveis para mensagens de Alta prioridade.</p>
<p>Quando você inserir um valor, qualifique-o com uma das seguintes unidades:</p>
<ul>
<li><p>KB (kilobytes)</p></li>
<li><p>MB (megabytes)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>Baixa</strong>   <code>8:00:00</code> (8 horas)</p>
<p><strong>Normal</strong>   <code>4:00:00</code> (4 horas)</p>
<p><strong>Alta</strong>   <code>00:30:00</code> (30 minutos)</p></td>
<td><p>Estas chaves especificam o intervalo de tempo limite para mensagens de notificação de status (DSN) de atraso de entrega com base na prioridade da mensagem.</p>
<p>Após cada falha na entrega da mensagem, o serviço de Transporte gera um mensagem DSN de atraso e coloca-a na fila para entrega ao remetente da mensagem não entregue. Essa notificação de status de entrega é enviada somente após um intervalo de tempo limite de notificação de atraso e somente se a mensagem que falhou não tiver sido entregue com êxito durante esse período. Esse atraso impede o envio de mensagens de notificação de status de entrega desnecessárias que podem ser causadas por falhas temporárias na transmissão de mensagens.</p>
<p>Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>Baixa</strong>   <code>2.00:00:00</code> (2 dias)</p>
<p><strong>Normal</strong>   <code>2.00:00:00</code> (2 dias)</p>
<p><strong>Alta</strong>   <code>8:00:00</code> (8 horas)</p></td>
<td><p>Estas chaves especificam a quantidade máxima de tempo durante a qual o serviço de Transporte tenta entregar uma mensagem com falha. Se a mensagem não puder ser entregue com êxito antes do final do intervalo de tempo-limite de expiração, uma notificação de falha na entrega com a mensagem original ou os cabeçalhos da mensagem será entregue ao remetente.</p>
<p>Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>Baixa</strong>   2</p>
<p><strong>Normal</strong>   15</p>
<p><strong>Alta</strong>   3</p></td>
<td><p>Estas chaves especificam o número máximo de conexões que podem ser abertas pelo serviço de Transporte para qualquer domínio remoto simples. As conexões de saída para os domínios remotos ocorrem através do uso das filas de entrega e Enviar conectores que existem no servidor da Caixa de Correio.</p>
<p>A soma destas três chaves deve ser menor ou igual ao valor do parâmetro <em>MaxPerDomainOutboundConnections</em> no cmdlet <strong>Set-TransportService</strong> . O valor padrão deste parâmetro é <code>20</code>.</p></td>
</tr>
</tbody>
</table>


## Como as filas com prioridades afetam outros limites da mensagem nos servidores da Caixa de Correio.

Todas as mensagens que passam pelo serviço de Transporte estão sujeitas a uma variedade de limites de repetição da mensagem, novo envio e expiração. Para obter mais informações, consulte [Limites de tamanhos de mensagens](message-size-limits-exchange-2013-help.md).

Alguns limites de mensagem disponíveis no cmdlet **Set-TransportService** possuem limites de mensagem para filas com prioridade correspondentes disponíveis no arquivo de configuração do aplicativo EdgeTransport.exe.config. A tabela a seguir mostra esses limites de mensagens correspondentes.

### Limites de mensagem no cmdlet Set-TransportService cmdlet que correspondem aos limites de mensagem das filas com prioridade no arquivo EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro ou chave</th>
<th>Valor padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 horas)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 horas)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 dias)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 dias)</p></td>
</tr>
</tbody>
</table>


Quando a fila com prioridades é desabilitada, todos os limites de mensagens para fila com prioridades do arquivo de configuração EdgeTransport.exe.config são ignorados. Todos os limites de mensagen no cmdlet **Set-TransportService** são aplicáveis a todas as mensagens que circulam no serviço de Transporte no servidor da Caixa de Correio.

Quando as filas com prioridade são habilitadas, os limites de mensagem das filas com prioridade no arquivo de configuração EdgeTransport.exe.config substituem os limites de mensagem correspondentes no cmdlet **Set-TransportService** . Todas as outras mensagens no cmdlet **Set-TransportService** ainda são aplicáveis às mensagens de Baixa prioridade, Prioridade normal e Alta prioridade que circulam pelo serviço de transporte no servidor de Caixa de Correio.

## Configurações do usuário para filas com prioridade

O cmdlet **Set-Mailbox** possui o parâmetro *DowngradeHighPriorityMessagesEnabled* . O valor padrão é `$false`. Quando este parâmetro é definido para `$true`, qualquer mensagem de Alta prioridade enviada da caixa de correio é automaticamente rebaixada para Prioridade normal.

