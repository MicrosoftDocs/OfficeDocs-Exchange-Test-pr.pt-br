---
title: 'Rastreamento de pipeline: Exchange 2013 Help'
TOCTitle: Rastreamento de pipeline
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52058887
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rastreamento de pipeline

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O rastreamento de pipeline captura cópias de mensagens de email de um remetente específico, como movem através do serviço de transporte em servidores de caixa de correio, o serviço de entrega de transporte de caixa de correio em servidores de caixa de correio e os servidores de transporte de borda.. O rastreamento de pipeline captura informações detalhadas sobre as alterações que cada agente de transporte se aplica às mensagens no pipeline de transporte nos arquivos de instantâneo de mensagem. Examinando o conteúdo dos arquivos de instantâneo de mensagem, você pode determinar se os agentes de transporte aplicou as alterações às mensagens no pipeline de transporte que o esperado. Se você estiver solucionando um problema, você deve determinar quais agentes de transporte está com defeito. Em seguida, é possível focar os esforços de solução de problemas em que esses operadores para resolver o problema. Em seguida, você pode exibir os arquivos de instantâneo de mensagem novamente para verificar se a sua solução é bem-sucedida.


> [!CAUTION]
> <UL>
> <LI>
> <P>O rastreamento de pipeline copia todo o conteúdo das mensagens de email que são enviadas de um endereço de email do remetente. Para evitar a exposição indesejada de informações confidenciais, você precisará definir permissões de segurança apropriados na pasta de rastreamento de pipeline.</P>
> <LI>
> <P>Não habilite o rastreamento de pipeline por longos períodos de tempo. O rastreamento de pipeline cria arquivos que podem acumular rapidamente. Sempre monitore o espaço em disco disponível quando o rastreamento de pipeline está habilitado.</P></LI></UL>



## Configurar o rastreamento de pipeline

Antes de habilitar o rastreamento de pipeline, você precisará especificar o endereço de email do remetente que você deseja monitorar. O rastreamento de pipeline foi projetado para efetuar as mensagens enviadas de um endereço de email específicos. Endereço de email do remetente pode ser internos ou externos à sua organização do Exchange. Como alternativa, é possível habilitar o rastreamento de pipeline para as mensagens de sistema gerados pelo serviço de transporte em que o servidor especificado de caixa de correio ou de transporte de borda, como mensagens de notificação (DSN) de status de entrega, as respostas automáticas, relatórios de diário e outras mensagens geradas pelo sistema, que você também pode modificar o local da pasta de rastreamento de pipeline.

Os parâmetros que você usa para configurar o rastreamento de pipeline estão resumidos na tabela a seguir


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>Espaço em branco (<code>$null</code>)</p></td>
<td><p>Especifique o endereço de email do remetente que você deseja monitorar.</p>
<p>Especifique o valor &quot;&lt;&gt;&quot; para monitorar as mensagens geradas pelo sistema enviadas pelo serviço de transporte especificado no servidor.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>Serviço de transporte</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code>   </p>
<p><strong>Serviço de transporte de caixa de correio</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code>   </p></td>
<td><p>O caminho deve ser no servidor local. Caminhos UNC não são suportados.</p>
<p>O caminho especificado contém a pasta de <code>MessageSnapshots</code> onde estão armazenados os arquivos de rastreamento de pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>Você só pode ativar o rastreamento de pipeline para o serviço de transporte especificado no servidor depois de configurar o endereço do remetente que você deseja monitorar.</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre como ativar o rastreamento de pipeline e configurar o endereço do remetente para o rastreamento de pipeline, consulte [Configurar o rastreamento de pipeline](configure-pipeline-tracing-exchange-2013-help.md).

## Arquivos de instantâneo de mensagem

Instantâneos de mensagem são arquivos que capturam quaisquer alterações feitas a uma mensagem por agentes de transporte no serviço de transporte ou o serviço de entrega de transporte de caixa de correio. Esses arquivos são armazenados na pasta `MessageSnapshots` no caminho de rastreamento de pipeline correspondente para o serviço de transporte.

Na pasta `MessageSnapshots` , Exchange cria uma pasta para cada mensagem enviada pelo remetente monitorado que chegam através do serviço de transporte especificado. Cada pasta é nomeada conforme um GUID que é atribuído à mensagem. Se você habilitar o rastreamento de pipeline para o serviço de transporte e o serviço de transporte de caixa de correio no mesmo servidor de caixa de correio, um GUID diferente é atribuído a mesma mensagem por cada serviço de transporte, portanto, o nome da pasta de uma mensagem na pasta `MessageSnapshots` para o serviço de transporte é diferente do nome da pasta para a mesma mensagem na pasta `MessageSnapshots` para o serviço de transporte de caixa de correio. Se você habilitar o rastreamento de pipeline em mais de um servidor do Exchange, um GUID diferente é atribuído a mesma mensagem durante o tráfego através do serviço de transporte especificado em cada servidor do Exchange.

Na pasta de cada mensagem, o Exchange cria vários arquivos de instantâneo de mensagem que tenham extensões de arquivo. eml. Esses arquivos de instantâneo de mensagem contêm o conteúdo da mensagem como ele encontra cada agente de transporte e o evento SMTP.

Se um agente de transporte está registrado em um evento de SMTP, o Exchange criará um instantâneo de mensagem da mensagem, antes que a mensagem encontra quaisquer agentes de transporte. Isso proporciona uma cópia da mensagem antes que a mensagem encontra agentes de transporte registrados nesse evento. Em seguida, um novo instantâneo de mensagem é criado para cada agente de transporte que a mensagem encontra, independentemente se um agente de transporte modifica o conteúdo da mensagem. No entanto, se nenhum agente estiver registrado em um evento, Exchange não cria qualquer instantâneos de mensagens para esse evento.

Por exemplo, se três agentes registrados no evento **OnEndofData** , mas somente dois dos agentes de transporte modificar uma mensagem, quatro instantâneos de mensagem são criados. O instantâneo de mensagem primeiro captura a mensagem como ele encontra o evento **OnEndofData** antes de quaisquer modificações feitas pelos agentes de transporte registrados nesse evento. Em seguida, um instantâneo de mensagem é criado para cada agente de transporte independentemente se um agente de transporte modifica a mensagem.

Os arquivos de instantâneo de mensagem que são criados são descritos na lista a seguir:

  - **EML** esse arquivo contém o conteúdo não modificado original da mensagem de email antes que ele encontra quaisquer eventos SMTP ou agentes de transporte.

  - **Routingnnnn.eml** esses arquivos contêm o conteúdo da mensagem de email como ele encontra eventos de transporte SMTP e os agentes de transporte registrados nesses eventos na parte de categorização do serviço de transporte. O espaço reservado *nnnn* representa um valor integer que começa com `0001`. O valor é incrementado para todos os agentes de transporte e o evento SMTP registrados nesses eventos na ordem na qual os eventos e os agentes agir na mensagem. O serviço de entrega de transporte de caixa de correio não gera esses arquivos de instantâneo **Routing** .

  - **SmtpReceivennnn.eml** esses arquivos contêm o conteúdo da mensagem de email como ele encontra os eventos de SMTP **OnEndofData** e **OnEndOfHeaders** e os agentes de transporte registrados nesses eventos durante o SMTP recebem a parte do serviço de transporte ou o serviço de entrega de transporte de caixa de correio. O espaço reservado *nnnn* representa um valor integer que começa com `0001`. O valor é incrementado para todos os agentes de transporte e o evento SMTP registrados nesses eventos na ordem na qual os eventos e os agentes agir na mensagem.

Você pode abrir os arquivos de instantâneo de mensagens usando o bloco de notas ou em qualquer editor de texto.

Cada arquivo de instantâneo de mensagem inicia com cabeçalhos que são adicionados ao conteúdo da mensagem e o agente de transporte e o evento de SMTP que o arquivo de instantâneo de mensagem se refere de lista. Esses cabeçalhos começam com `X-CreatedBy: MessageSnapshot-Begin injected headers` e terminarem com `X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers`. Esses cabeçalhos são substituídos em cada arquivo de instantâneo de mensagem por cada agente de transporte subsequentes e o evento SMTP. Este é um exemplo dos cabeçalhos que são adicionados a um arquivo de mensagem de email:

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

Após os cabeçalhos de instantâneo de mensagem, o arquivo contém o conteúdo da mensagem incluindo todos os cabeçalhos de mensagem original. Se um agente de transporte modifica o conteúdo da mensagem, as alterações aparecem integradas com a mensagem. Como a mensagem é processada por cada agente de transporte, as alterações feitas por cada agente são aplicadas ao conteúdo da mensagem. Se um agente de transporte não altera o conteúdo da mensagem, o instantâneo de mensagem que é criado por que esses operadores será idêntico à mensagem instantâneo criado pelo agente de transporte anterior.

