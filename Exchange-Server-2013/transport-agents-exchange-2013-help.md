---
title: 'Agentes de transporte: Exchange 2013 Help'
TOCTitle: Agentes de transporte
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 50486912
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agentes de transporte

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Agentes de transporte permitem que você instalar o software personalizado que é criado pela Microsoft, pelos fornecedores de terceiros ou por sua organização, em um servidor Exchange. Este software pode processar as mensagens de email que passam pelo pipeline de transporte. No Microsoft Exchange Server 2013, o pipeline de transporte é composto os seguintes processos:

  - O serviço de Front End Transport em servidores de acesso para cliente

  - O serviço de transporte em servidores de caixa de correio

  - O serviço de transporte de caixa de correio em servidores de caixa de correio

  - O serviço de transporte em servidores de transporte de borda

Para obter mais informações sobre o pipeline de transporte, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md)

Como a versão anterior do Exchange, o transporte Exchange 2013 fornece extensibilidade por meio do Microsoft Exchange Server 2013 SDK de agentes de transporte. A versão Exchange 2013 do SDK baseia-se na Microsoft.NET Framework versão 4.0 e permita terceiros implementar as seguintes classes predefinidas:

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

Quando cumpriu contra bibliotecas no SDK, os assemblies resultantes são registrados com Exchange 2013, que carrega os operadores e invoca seus manipuladores de evento durante estágios específicos do processamento de mensagens ou sessões de SMTP. Esses estágios ou eventos, fazem parte das definições de agente. As informações de registro do agente são armazenadas em um arquivo de configuração XML.

A lista a seguir explica os requisitos para o uso de agentes de transporte em Exchange 2013.

  - O serviço de transporte em servidores de transporte de borda e servidores de caixa de correio totalmente oferece suporte a todas as classes predefinidas no SDK e, portanto, qualquer agentes de transporte de terceiros escritos para o servidor de transporte de Hub ou de transporte de borda funções no Microsoft Exchange Server 2010 devem funcionar no serviço de transporte no Exchange 2013.

  - O serviço Front End Transport suporta apenas a classe **SmtpReceiveAgent** no SDK e agentes de terceiros não podem operar no evento **OnEndOfData** SMTP.

  - O serviço de transporte de caixa de correio não suporta o SDK nisso, portanto, você não pode usar quaisquer agentes de terceiros no serviço de transporte de caixa de correio.

Suporte para agentes de transporte herdado com base em versões do .NET Framework antes da versão 4.0 não está habilitada por padrão, mas você pode ativá-lo. Para obter instruções, consulte [Habilitar o suporte para agentes de transporte de legado](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

**Sumário**

Atualizações para o gerenciamento de agentes de transporte

Agentes de transporte e eventos de SMTP

Prioridade de agentes de transporte

Agentes de transporte interno

Solucionar problemas de agentes de transporte

## Atualizações para o gerenciamento de agentes de transporte

Devido às atualizações para o pipeline de transporte Exchange 2013, os cmdlets do agente de transporte precisa distinguir entre o serviço de transporte e o serviço Front End Transport, especialmente se o servidor de acesso para cliente e o servidor de caixa de correio são instalados no mesmo computador. Para obter mais informações, consulte [Gerenciar agentes de transporte](manage-transport-agents-exchange-2013-help.md).

Cmdlets de gerenciamento do agente de transporte manipular um arquivo de configuração, localizado em `%ExchangeInstallPath%TransportRoles\Shared`. Para o serviço de transporte em servidores de caixa de correio e servidores de transporte de borda, o arquivo é `agents.config`. Para o serviço Front End Transport em servidores de acesso para cliente, o arquivo é `fetagents.config`. Ambos os arquivos usam o mesmo formato de Exchange 2010. Para obter mais informações sobre como gerenciar agentes de transporte, consulte [Gerenciar agentes de transporte](manage-transport-agents-exchange-2013-help.md).

Voltar ao início

## Agentes de transporte e eventos de SMTP

Agentes de transporte utilize os eventos de SMTP. Esses eventos são disparados conforme as mensagens são movidas através do pipeline de transporte. Eventos de SMTP oferecem agentes de transporte acesso a mensagens em pontos específicos durante a conversa SMTP e roteamento de mensagens por meio da organização.

Observe que não existem novos eventos de recebimento SMTP no Exchange 2013. Recebimento SMTP existe no serviço de Front End Transport em servidores de acesso para cliente, o serviço de transporte em servidores de transporte de borda e servidores de caixa de correio e o serviço de entrega de transporte de caixa de correio em servidores de caixa de correio. Categorizador existe somente no serviço de transporte em servidores de caixa de correio e servidores de transporte de borda. Para obter mais informações sobre os serviços de transporte e o categorizador, consulte [Roteamento de mensagens](mail-routing-exchange-2013-help.md).

As tabelas a seguir listam os eventos de SMTP que fornecem acesso às mensagens no pipeline de transporte.

### Eventos de recebimento SMTP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sequência</th>
<th>Evento SMTP</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>Este evento é disparado pela conexão inicial de um host de SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>HELO</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>EHLO</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>STARTTLS</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>AUTH</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>Esse evento é acionado quando a autenticação com o host SMTP remoto que está sendo processada.</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>Esse evento é acionado quando o host SMTP remoto concluiu a autenticação.</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>XSESSIONPARAMS</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>MAIL FROM</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>Este evento é acionado quando o comando <code>RCPT TO</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>Este evento é acionado quando o <code>DATA</code> (texto) ou o comando de <code>BDAT</code> (dados binários) é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Esse evento é acionado quando o host SMTP remoto concluiu enviando os cabeçalhos de mensagem de email. Isso é indicado por uma linha em branco (<code>&lt;CRLF&gt;</code>) que separa os cabeçalhos de mensagem e o corpo da mensagem.</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>Este evento é acionado quando uma sessão de SMTP de entrada é retransmitida ou <em>intermediadas por proxy</em> pelo serviço Front End Transport em um servidor de acesso para cliente para o serviço de transporte em um servidor de caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Este evento é acionado quando o host SMTP remoto emite um fim de comando de dados. Para sessões de texto iniciadas pelo comando <code>DATA</code> , o final do indicador de dados é <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>. Para sessões de binárias iniciadas pelo comando <code>BDAT</code> , o final do indicador de dados é <code>BDAT LAST</code>.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>Esse evento é acionado se o comando <code>HELP</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>Esse evento é acionado se o comando <code>NOOP</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>Esse evento é acionado se o host de recebimento SMTP emite um código de notificação (DSN) de status de entrega temporário ou permanente para o host de envio SMTP.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>Esse evento é acionado se o comando <code>RSET</code> é emitido pelo host de SMTP de envio.</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>Este evento é disparado pela desconexão da conversa SMTP pelo recebimento ou envio de host SMTP. Geralmente, isso acontece quando o comando <code>QUIT</code> é emitido pelo host SMTP remoto.</p></td>
</tr>
</tbody>
</table>


\* \* Esses eventos podem ocorrer a qualquer momento após **OnConnectEvent** , mas antes de **OnDisconnectEvent**.

### Eventos de categorizador

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sequência</th>
<th>Evento categorizador</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>Este evento é acionado quando uma mensagem chega na fila de envio no serviço de transporte no servidor de transporte de borda ou servidor de caixa de correio de recebimento.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>Este evento é acionado depois de todos os destinatários foram resolvidos, mas antes do próximo salto foi determinado para cada destinatário. O evento de roteamento <strong>OnResolvedMessage</strong> permite eventos subsequentes substituir o comportamento padrão de roteamento usando o método por destinatário <strong>SetRoutingOverride</strong> .</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>Este evento é acionado depois que as mensagens foram categorizadas, listas de distribuição foram expandidas e destinatários foram resolvidos.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>Esse evento é acionado quando o categorizador conclui o processamento da mensagem.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Prioridade de agentes de transporte

Há dois fatores que determinam a ordem em que os agentes de transporte agem nas mensagens no pipeline de transporte:

1.  O evento SMTP onde o agente de transporte está registrado, e quando esse evento SMTP encontra mensagens.

2.  O valor de prioridade é atribuído ao agente de transporte, se houver vários agentes registrados para o mesmo evento SMTP. A prioridade mais alta é 1. Um valor inteiro maior indica uma prioridade mais baixa do agente.

Por exemplo, suponha que você configurou os agentes de transporte a seguir:

  - Agente de transporte uma com uma prioridade de 1 e C de agente de transporte com uma prioridade 2 são registrados ao evento **OnEndOfHeaders** SMTP.

  - B de agente de transporte com uma prioridade de 4 está registrado ao evento **OnMailCommand** SMTP.

B de agente de transporte é aplicado às mensagens primeiro porque o evento **OnMailCommand** encontra mensagens antes do evento **OnEndOfHeaders** . Quando as mensagens atingem o evento **OnEndOfHeaders** , uma de agente de transporte é aplicado antes de C de agente de transporte, porque o agente de transporte uma tem uma prioridade maior (valor mais baixo de inteiro) que C. de agente de transporte

## Agentes de transporte interno

Exchange 2013 inclui muitos agentes de transporte internas que fornecem recursos como antispam, regras de transporte e diário. A maioria dos agentes de transporte interno em servidores de acesso para cliente e servidores de caixa de correio de Exchange 2013 são invisível e não gerenciável pelos cmdlets de gerenciamento do agente de transporte. Praticamente todos os agentes de transporte interno que estão visíveis e gerenciável estão no serviço de transporte nos servidores de caixa de correio e nos servidores de transporte de borda.

Os agentes de transporte interno mais interessantes nos servidores de caixa de correio são descritos na tabela a seguir. Observe que essa tabela não inclui muitos dos agentes de transporte invisível e difíceis de gerenciar.

### Interessante agentes de transporte internas nos servidores de caixa de correio

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do Agente</th>
<th>Gerenciável?</th>
<th>Prioridade</th>
<th>Eventos de SMTP ou categorizador</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente de regras de transporte</p></td>
<td><p>Sim</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de malware</p></td>
<td><p>Sim</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de roteamento de mensagens de texto</p></td>
<td><p>Sim</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de entrega de mensagens de texto</p></td>
<td><p>Sim</p></td>
<td><p>4</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p>Agente de diário</p></td>
<td><p>Não</p></td>
<td><p>Não é configurável</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de descriptografia do relatório de diário</p></td>
<td><p>Não</p></td>
<td><p>Não é configurável</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de descriptografia do RMS</p></td>
<td><p>Não</p></td>
<td><p>Não é configurável</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de criptografia do RMS</p></td>
<td><p>Não</p></td>
<td><p>Não é configurável</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de descriptografia do protocolo do RMS</p></td>
<td><p>Não</p></td>
<td><p>Não é configurável</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


Nos servidores de transporte de borda, a maioria dos agentes de transporte interno está visíveis e gerenciáveis pelos cmdlets de gerenciamento do agente de transporte ou por outros cmdlets específica de recursos.

Os agentes de transporte interno mais interessantes nos servidores de transporte de borda são descritos na tabela a seguir. Observe que essa tabela não inclui os agentes de transporte invisíveis ou não gerenciável.

### Agentes de transporte interno interessantes nos servidores de transporte de borda

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do Agente</th>
<th>Gerenciável?</th>
<th>Prioridade</th>
<th>Eventos de SMTP ou categorizador</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente de filtragem de conexão</p></td>
<td><p>Sim</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnMailCommand</strong>, <strong>OnRcptComand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de entrada de reconfiguração de endereço</p></td>
<td><p>Sim</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de regras de borda</p></td>
<td><p>Sim</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de filtro de conteúdo *</p></td>
<td><p>Sim</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de ID de remetente *</p></td>
<td><p>Sim</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de filtro de remetente *</p></td>
<td><p>Sim</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de filtro de destinatário</p></td>
<td><p>Sim</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de análise de protocolo *</p></td>
<td><p>Sim</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnEndOfHeaders</strong>, <strong>OnEndOfData</strong>, <strong>OnReject</strong>, <strong>OnRsetCommand</strong>, <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de filtragem de anexo</p></td>
<td><p>Sim</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de saída de reconfiguração de endereço</p></td>
<td><p>Sim</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* Você também pode instalar e configurar esses agentes antispam em servidores de caixa de correio. Para obter mais informações, consulte [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Voltar ao início

## Solucionar problemas de agentes de transporte

Para ajudá-lo a solucionar problemas com os agentes de transporte, você pode usar os seguintes recursos:

  - **Get-TransportPipeline**   Este cmdlet mostra os eventos de SMTP e os agentes de transporte correspondente que encontrar mensagens no Exchange server. Para obter mais informações, consulte [Agentes de transporte de modo de exibição no pipeline de transporte](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md).

  - **Rastreamento de pipeline**   O rastreamento de pipeline cria um instantâneo exato de uma mensagem antes e depois que ele encontra cada agente de transporte. Isso permite que você encontre um agente de transporte que está causando resultados inesperados. Para obter mais informações, consulte [Rastreamento de pipeline](pipeline-tracing-exchange-2013-help.md).

Voltar ao início

