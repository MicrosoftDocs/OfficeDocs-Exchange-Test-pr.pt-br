---
title: 'Log de agente de anti-spam: Exchange 2013 Help'
TOCTitle: Log de agente de anti-spam
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 50486780
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log de agente de anti-spam

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Logs de agente registram as ações executadas em uma mensagem por específicos agentes antispam no Microsoft Exchange Server 2013. Somente os seguintes agentes podem gravar as informações no log de agente:

  - Agente de Filtragem de Conexão

  - Agente de Filtro de Conteúdo

  - Agente de regras de borda

  - Agente de Filtro de Destinatários

  - Agente de Filtro por Remetente

  - Agente de ID de Remetente


> [!TIP]
> O agente de filtragem de conexão e o agente de regras de borda não estão disponíveis nos servidores de caixa de correio.



As informações gravadas no log de agente dependem do agente, o evento SMTP e a ação executada na mensagem.

Você pode usar o cmdlet **Set-TransportService** no Shell de gerenciamento do Exchange para executar todas as tarefas de configuração de log de agente. As seguintes opções estão disponíveis para os logs de agente:

  - Habilitar ou desabilitar o log de agente. O padrão é ativado.

  - Especifique o local dos arquivos de log de agente. O valor padrão é % ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

  - Especifique um tamanho máximo para os arquivos de log do agente individuais. O tamanho padrão é 10 megabytes (MB).

  - Especifique um tamanho máximo para o diretório que contém os arquivos de log do agente. O tamanho padrão é 250 MB.

  - Especifique uma idade máxima para os arquivos de log do agente. A idade padrão é 7 dias.

Exchange usa o log circular para limitar os logs de agente com base no tamanho do arquivo e o arquivo para ajudar a controlar o espaço em disco rígido usado pelos arquivos de log.

**Sumário**

Visão geral dos agentes de transporte

Estrutura dos arquivos de log do agente

Informações gravadas no log de agente

Pesquisar os logs de agente

## Visão geral dos agentes de transporte

Operadores somente podem atuar sobre mensagens em pontos específicos a sequência de comando SMTP usado para transportar as mensagens através do serviço de transporte em um servidor de caixa de correio ou um servidor de transporte de borda. Esses pontos de acesso na sequência de comando SMTP são chamados de *eventos de SMTP*. Cada agente tem um valor de prioridade que pode ser atribuído. No entanto, os eventos de SMTP sempre devem ocorrer em uma ordem específica. Portanto, a prioridade do agente depende do evento SMTP. Se dois agentes podem atuar em uma mensagem durante o evento de SMTP mesmo, o agente que tem a prioridade mais alta atuará na mensagem pela primeira vez.

A tabela a seguir lista os eventos de SMTP na ordem da ocorrência e os agentes que gravam informações no log de agente em ordem de prioridade em ordem decrescente para cada evento de SMTP.

### Eventos de SMTP na ordem da ocorrência e os agentes que gravam informações para o agente de log em ordem de prioridade para cada evento de SMTP

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento SMTP</th>
<th>Agente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>Agente de Filtragem de Conexão</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Agente de Filtragem de Conexão</p>
<p>Agente de Filtro por Remetente</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>Agente de Filtragem de Conexão</p>
<p>Agente de Filtro de Destinatários</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Agente de Filtragem de Conexão</p>
<p>Agente de ID de Remetente</p>
<p>Agente de Filtro por Remetente</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Agente de regras de borda</p>
<p>Agente de filtragem de conteúdo</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> O agente de filtragem de conexão e o agente de regras de borda não estão disponíveis nos servidores de caixa de correio.



Para obter mais informações sobre agentes, eventos de SMTP e prioridade do agente, consulte [Agentes de transporte](transport-agents-exchange-2013-help.md).

Voltar ao início

## Estrutura dos arquivos de log do agente

Os logs de agente existirem na pasta % ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

A convenção de nomenclatura para os arquivos de log do agente é AGENTLOG*yyyymmdd-nnnn*. log. Os espaços reservados representam as seguintes informações:

  - O espaço reservado *yyyymmdd* é a data de tempo Universal Coordenado (UTC) que o arquivo de log foi criado. O espaço reservado *yyyy* = ano, *mm* = mês e *dd* = dia.

  - O marcador *nnnn* é um número de instância que começa com o valor 1 para cada dia.

Informação é gravada no arquivo de log até que o tamanho do arquivo atinge seu valor máximo de especificado e um novo arquivo de log que tem um número de instância incrementada é aberto. Esse processo é repetido ao longo do dia. O log circular exclui os arquivos de log mais antigos quando o diretório de log de agente atinge seu tamanho máximo de especificado, ou quando um arquivo de log atinge sua idade máxima de especificado.

Os arquivos de log do agente são arquivos de texto que contêm dados no formato de arquivo (CSV) de valores separados por vírgulas. Cada arquivo de log de agente tem um cabeçalho que contém as seguintes informações:

  - **\#Software**   Nome do software que criou o arquivo de log de agente. Normalmente, o valor é o Microsoft Exchange Server.

  - **\#Version**   Número de versão do software que criou o arquivo de log de agente. Atualmente, o valor é 15.0.0.0.

  - **Tipo de log \#**   Valor de tipo de log, que é o Log de agente.

  - **\#Date**   A data e a hora UTC do momento em que o arquivo de log foi criado. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, em que aaaa*yyyy* = ano, mm*mm* = mês, dd*dd* = dia, T indica o início de componente de hora, hh*hh* = hora, mm*mm* = minuto, ss*ss* = segundo, fff*fff* = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.

  - **\#Fields**   Nomes de campo usados nos arquivos de log do agente delimitada por vírgula.

Voltar ao início

## Informações gravadas no log de agente

O log de agente armazena cada transação de agente em uma única linha no log. As informações armazenadas em cada linha são organizadas por campos. Esses campos são separados por vírgulas. O nome do campo é geralmente descritivo para determinar o tipo de informação que ele contém. No entanto, alguns dos campos podem estar em branco. Ou o tipo das informações armazenadas no campo pode ser alteradas com base no agente ou a ação executada na mensagem pelo agente. A tabela a seguir descreve os campos usados para classificar cada transação de agente.

### Os campos usados para classificar cada transação de agente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do campo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Timestamp</strong></p></td>
<td><p>UTC Data / hora do evento agente. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, em que aaaa<em>yyyy</em> = ano, mm<em>mm</em> = mês, dd<em>dd</em> = dia, T indica o início de componente de hora, hh<em>hh</em> = hora, mm<em>mm</em> = minuto, ss<em>ss</em> = segundo, fff<em>fff</em> = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>Identificador exclusivo de sessão SMTP. Esse identificador é representado como um número hexadecimal de 16 dígitos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>Local endereço IP e porta número que aceitou a mensagem. Sessões SMTP normalmente usam a porta 25.</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>Endereço IP e porta número do servidor SMTP anterior que conectado a este servidor para entregar a mensagem. Quando fluem de emails da Internet através de um servidor de transporte de borda na rede de perímetro, o valor de <strong>RemoteEndpoint</strong> no registro do agente no servidor de caixa de correio será o endereço IP do servidor de transporte de borda. Mesmo que a mensagem é transmitida por SMTP, o número da porta usado pelo servidor de envio será um número aleatório maior 1.024.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>Endereço IP do servidor SMTP remoto que primeiro conectados à organização do Exchange para entregar a mensagem. Em um servidor de transporte de borda, o valor de <strong>RemoteEndpoint</strong> e <strong>EnteredOrgFromIP</strong> são os mesmos. Agentes antispam usam o endereço IP em <strong>EnteredOrgFromIP</strong> para examinar uma mensagem.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p>Valor do campo de cabeçalho <code>MessageID</code> . Se este valor estiver em branco, o servidor de transporte do Exchange atribui um valor arbitrário, mas somente se a mensagem será aceita. Depois que um valor é atribuído, o valor de <code>MessageID</code> é constante para o tempo de vida da mensagem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>Endereço de email do remetente especificado em <code>MAIL FROM</code> no envelope da mensagem. Esse valor é usado para a mensagem entre os servidores de mensagens SMTP de transporte. Este valor serve como uma comparação com o valor de <strong>P2FromAddresses</strong> para determinar se o endereço do remetente no cabeçalho da mensagem é falsificado.</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>Endereço de email do remetente especificado no campo de cabeçalho <code>From</code> ou no campo de cabeçalho <code>Sender</code> no cabeçalho da mensagem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>Endereço de email dos destinatários. Embora a mensagem original pode conter vários destinatários, somente um destinatário é exibido por linha no registro do agente.</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>Número total de destinatários da mensagem original.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>Nome do agente que recebeu a ação. Os valores possíveis são:</p>
<ul>
<li><p>Agente de Filtro de Conteúdo</p></li>
<li><p>Agente de Filtro de Destinatários</p></li>
<li><p>Agente de Filtro por Remetente</p></li>
<li><p>Agente de ID de Remetente</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>Evento de SMTP onde a ação foi realizada pelo agente. O valor da <strong>Event</strong> depende do agente. Os eventos de SMTP disponíveis para cada agente são descritos na tabela primeira anteriormente neste tópico. Os valores possíveis para <strong>Event</strong> são:</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>Ação executada na mensagem pelo agente. Os valores possíveis para <strong>Action</strong> são:</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Desconectar</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>Aprimorado a resposta SMTP conforme definido no RFC 2034.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>Motivo da ação fornecido pelo agente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>Detalhes descritivos para a ação fornecido pelo agente.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Pesquisar os logs de agente

Você pode usar o cmdlet **Get-AgentLog** e o script **Get-AntiSpamFilteringReport.ps1** para pesquisar os logs de agente.

O script de **Get-AntiSpamFilteringReport.ps1** está localizado em `%ExchangeInstallPath%Scripts`. Você precisará executar o script no Shell da pasta Scripts. Para alterar o seu local no Shell para a pasta Scripts, execute o seguinte comando:

    Cd $env:ExchangeInstallPath\Scripts

Para executar o script na pasta Scripts, use a seguinte sintaxe:

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

Para obter detalhes sobre como usar o script, execute o seguinte comando:

    Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1

Voltar ao início

