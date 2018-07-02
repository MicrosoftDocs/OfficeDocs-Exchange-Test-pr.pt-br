---
title: 'Intervalos de repetição, reenvio e expiração de mensagem: Exchange 2013 Help'
TOCTitle: Intervalos de repetição, reenvio e expiração de mensagem
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51407830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Intervalos de repetição, reenvio e expiração de mensagem

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

No Microsoft Exchange Server 2013, as mensagens que não podem ser entregue com êxito estão sujeitos vários prazos de repetição, reenvio e expiração com base na origem e de destino da mensagem. *Repetir* é uma tentativa de conexão renovado com o destino. *Reenviar* é o ato de enviar mensagens de volta para a fila de envio para o categorizador reprocessar. A mensagem *expira* após todos os esforços de entrega falharam por um período de tempo especificado. Depois que uma mensagem expira, o remetente é notificado de que a falha de entrega. Em seguida, a mensagem é excluída da fila.

Em todos os três casos repetir, reenviar ou expirar, você pode intervir manualmente antes que as ações automáticas são realizadas em todas as mensagens.

Para obter instruções sobre como configurar esses intervalos, consulte [Configurar intervalos de repetição, reenvio e expiração de mensagem](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Opções de configuração de repetição de mensagem

Quando um servidor de transporte não pode se conectar com o próximo salto, a fila é colocada em um status Retry. Tentativas de conexão continuam até que a fila expira ou uma conexão é feita.

## Opções de configuração de repetição automática de mensagens

As opções de configuração que estão disponíveis para os intervalos de repetição de mensagem são descritas na tabela a seguir.

### Opções de configuração que estão disponíveis para a mensagem de intervalos de repetição

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do parâmetro ou chave</th>
<th>Valor padrão</th>
<th>Onde configurar</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Esta chave especifica o número de tentativas de conexão que são tentadas imediatamente quando um servidor de transporte tiver dificuldades para se conectar com o servidor de destino. Esses problemas de conexão geralmente são causados por interrupções de rede muito breve.</p>
<p>A entrada válida para essa chave é um inteiro de 0 a 15.</p>
<p>Normalmente, você não precisa modificar essa chave, a menos que a rede não é confiável e continua a experiência de muitas conexões acidentalmente capitular.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> ou 1 minuto</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Esta chave controla o intervalo de conexão entre cada tentativa de conexão que é especificado pela chave <em>QueueGlitchRetryCount</em> .</p>
<p>Normalmente, você não precisa modificar esse parâmetro, a menos que a rede não é confiável e continua a experiência de muitas conexões acidentalmente capitular.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p>propriedades <strong>Set-TransportService</strong> cmdlet ou do servidor no Centro de administração do Exchange (EAC)</p></td>
<td><p>Este parâmetro especifica o número de tentativas de conexão serão tentados após as tentativas de conexão são controladas pelas chaves <em>QueueGlitchRetryCount</em> e <em>QueueGlitchRetryInterval</em> tiverem falhado. Problemas de conexão que esgotar as chaves <em>QueueGlitchRetryCount</em> e <em>QueueGlitchRetryInterval</em> podem ser causados por servidor reiniciar ou cache falhas de pesquisa DNS.</p>
<p>A entrada válida para esse parâmetro é um inteiro de 0 a 15. Se você definir esse parâmetro como 0, a próxima tentativa de conexão é controlada pelo parâmetro <em>OutboundConnectionFailureRetryInterval</em> .</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Serviço de transporte em servidores de caixa de correio: <code>00:05:00</code> ou 5 minutos</p></li>
<li><p>Servidores de transporte de borda: <code>00:01:00</code> ou 10 minutos</p></li>
</ul></td>
<td><p>Propriedades de cmdlet ou do servidor de <strong>Set-TransportService</strong>no EAC</p></td>
<td><p>Esse parâmetro controla o intervalo de conexão entre cada tentativa de conexão que é especificado pelo parâmetro <em>TransientFailureRetryCount</em> .</p>
<p>Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Serviço de transporte em servidores de caixa de correio: <code>00:10:00</code> ou 10 minutos</p></li>
<li><p>Servidores de transporte de borda: <code>00:30:00</code> ou 30 minutos</p></li>
</ul></td>
<td><p>Propriedades de cmdlet ou do servidor de <strong>Set-TransportService</strong> no EAC</p></td>
<td><p>Este parâmetro especifica o intervalo de repetição de tentativas de conexão de saída que falharam anteriormente. As tentativas de conexão falhou anteriormente são controladas pelos parâmetros <em>TransientFailureRetryCount</em> e <em>TransientFailureRetryInterval</em> .</p>
<p>Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> or15 minutos</p></td>
<td><p>cmdlet <strong>Set-TransportService</strong></p></td>
<td><p>Este parâmetro especifica o intervalo de repetição para mensagens individuais que têm um status Retry. Recomendamos que você não modifique o valor padrão, a menos que o suporte e atendimento ao cliente Microsoft recomendará a fazer isso.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> ou 5 minutos</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Esta chave especifica a frequência as filas tentarem se conectar ao serviço de entrega de transporte de caixa de correio para um banco de dados de caixa de correio de destino não pode ser acessado com êxito.</p>
<p>Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.</p>
<p>A entrada válida para essa chave é de 00:00:01 por meio de 1.00:00:00.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Opções de configuração para repetir manual de mensagem

Quando uma fila de entrega está no status de repetição, você pode forçar manualmente uma tentativa de conexão imediata usando o Visualizador de filas na caixa de ferramentas do Exchange ou o cmdlet **Retry-Queue** no Shell. A tentativa de repetição manual sobrescreve na próxima vez agendada repetir. Se a conexão não for bem-sucedida, timer do intervalo de repetição é redefinido. A fila de entrega deve estar no status Retry para esta ação tenha efeito.

Para obter mais informações, consulte a seção "Repetir filas" no [Gerenciar filas](manage-queues-exchange-2013-help.md).

Voltar ao início

## Opções de configuração para mensagens DSN de atraso

Depois de cada falha de entrega de mensagem, o servidor de transporte de borda ou o serviço de transporte no servidor de caixa de correio gera uma mensagem de notificação (DSN) de status de entrega de atraso e coloca em fila para entrega ao remetente da mensagem não entregue. Essa mensagem DSN atraso é enviada somente depois de um intervalo de tempo limite de notificação de atraso especificado e somente se a mensagem de falha não foi entregue com êxito durante esse horário. Por padrão, o intervalo de tempo limite de notificação de atraso é 4 horas. Este atraso impede o envio de mensagens DSN atraso desnecessários que podem ser causadas por falhas de transmissão de mensagem temporária. O envio de mensagens de notificação de DSN atraso pode ser seletivamente habilitado ou desabilitado para as mensagens originadas dentro ou fora da organização do Exchange.

As opções de configuração que estão disponíveis para mensagens de notificação de DSN atraso são descritas na tabela a seguir.

### Opções de configuração que estão disponíveis para mensagens de notificação de DSN de atraso

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do parâmetro</th>
<th>Valor padrão</th>
<th>Local</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 horas</p></td>
<td><p>propriedades <strong>Set-TransportService</strong> ou do servidor no EAC</p></td>
<td><p>Este parâmetro especifica por quanto tempo o servidor aguardará antes de enviar uma mensagem DSN atraso ao remetente. O valor desse parâmetro deve sempre ser maior que o valor do parâmetro <em>TransientFailureRetryCount</em> multiplicado pelo valor do parâmetro <em>TransientFailureRetryInterval</em> .</p>
<p>Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Este parâmetro especifica se as mensagens DSN atraso podem ser enviadas para remetentes de mensagens que estão fora da organização do Exchange.</p>
<p>As entradas válidas para este parâmetro são <code>$true</code> ou <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Este parâmetro especifica se as mensagens DSN atraso podem ser enviadas para remetentes de mensagens que estão dentro da organização do Exchange.</p>
<p>As entradas válidas para este parâmetro são <code>$true</code> ou <code>$false</code>.</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> Nos servidores de transporte de Hub Exchange 2007, todos os parâmetros <EM>ExternalDSN*</EM> e <EM>InternalDSN*</EM> estão disponíveis no cmdlet <STRONG>Set-TransportServer</STRONG> , não o cmdlet <STRONG>Set-TransportConfig</STRONG> . Se você tiver quaisquer servidores de transporte de Hub Exchange 2007 em sua organização, você precisará fazer alterações nesses valores usando o cmdlet <STRONG>Set-TransportServer</STRONG> em cada servidor de transporte de Hub Exchange 2007.



Voltar ao início

## Opções de configuração para reenvio de mensagem

Reenvio de mensagem envia mensagens não entregues volta à fila de envio sejam reprocessadas pelo categorizador.

## Reenvio de mensagem automática

Falha na entrega de mensagens são reenviadas automaticamente se a fila de entrega está no status de repetição e ficou não foi possível entregar com êxito a todas as mensagens para um período de tempo especificado. Esse período de tempo é controlado pela chave *MaxIdleTimeBeforeResubmit* no arquivo de configuração do aplicativo EdgeTransport.exe.config. Somente as mensagens nas filas de entrega são candidatos para reenvio automático.

Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.

O valor padrão é `12:00:00` ou 12 horas.

## Reenvio de mensagem manual

Você pode manualmente reenviar mensagens que têm o seguinte status no serviço de transporte em um servidor de caixa de correio ou um servidor de transporte de borda:

  - Filas de entrega que têm o status repetir. As mensagens nas filas não devem estar em estado suspenso.

  - Mensagens que estão na fila inacessível e não estejam no estado suspenso.

  - Mensagens que estão na fila de mensagens suspeitas.

Para obter mais informações sobre a fila de mensagens suspeitas e fila inacessível, consulte "Sobre o suspeitas mensagem fila e a fila inacessível" do tópico [Filas](queues-exchange-2013-help.md).

Se desejar manualmente reenviar mensagens localizadas na fila inacessível ou de filas de entrega sem aguardar a hora em que é especificada pelo parâmetro *MaxIdleTimeBeforeResubmit* passar, você precisará usar o cmdlet **Retry-Queue** com o parâmetro *Resubmit* . Para manualmente reenviar mensagens localizadas na fila de mensagens suspeitas, você pode usar o Visualizador de filas ou o cmdlet **Resume-Message** para retomar a mensagem. Para obter mais informações, consulte a seção "Reenviar mensagens nas filas" no [Gerenciar filas](manage-queues-exchange-2013-help.md).

Outra maneira que você manualmente pode reenviar mensagens é para suspender mensagens, exporte as mensagens para arquivos de texto que têm a extensão de nome de arquivo. eml e copie os arquivos. eml para o diretório de reprodução em qualquer servidor de caixa de correio ou servidor de transporte de borda. Esse método de reenvio funciona para mensagens que estão localizadas na fila inacessível ou de filas de entrega. Mensagens que estão localizadas na fila de mensagens suspeitas já estão no estado suspenso. Mensagens que estão localizadas na fila de envio não podem ser suspenso ou exportadas.


> [!TIP]
> Quando você exporta mensagens de uma fila, você não remove as mensagens da fila. Após exportar as mensagens e com êxito reenviá-los usando o diretório de repetição, você deve remover suspendeu mensagens para evitar a entrega da mensagem duplicados.



Para obter mais informações, consulte [Exportar mensagens de filas](export-messages-from-queues-exchange-2013-help.md).

Voltar ao início

## Opções de configuração de expiração de mensagem

O *intervalo de tempo limite de expiração de mensagem* Especifica o comprimento máximo de tempo que o serviço de transporte em um servidor de caixa de correio ou de um servidor de transporte de borda tenta enviar uma mensagem com falha. Se a mensagem não pode ser entregue com êxito antes de expirar o intervalo de tempo limite de expiração, uma NDR que contém a mensagem original ou os cabeçalhos de mensagem é entregue ao remetente.

## Expiração automática de mensagens

O intervalo de tempo limite de expiração da mensagem é controlado pelo parâmetro *MessageExpirationTimeOut* no cmdlet **Set-TransportService** ou nas propriedades do servidor no EAC.

Para especificar um valor, digite-o como um período de tempo: dd.hh:mm:ss, em que d = dias, h = horas, m = minutos e s = segundos.

O valor padrão é `2.00:00:00` ou 2 dias. O intervalo válido de entrada para esse parâmetro é de `00:00:05` por meio de `90.00:00:00`.

## Expiração de mensagem manual

Embora você não é possível forçar manualmente as mensagens para expirar, você pode remover manualmente mensagens de qualquer fila, exceto a fila de envio, com ou sem um NDR.

Para obter mais informações, consulte a seção "Remover mensagens de filas" no [Gerenciar mensagens em filas](manage-messages-in-queues-exchange-2013-help.md).

Voltar ao início

