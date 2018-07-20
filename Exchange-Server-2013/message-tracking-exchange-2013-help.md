---
title: 'Controle de mensagens: Exchange 2013 Help'
TOCTitle: Controle de mensagens
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51407901
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Controle de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

No Microsoft Exchange Server 2013, o log de controle de mensagens é um registro detalhado de toda a atividade de mensagens à medida que as mensagens são transferidas para e do serviço de Transporte em Servidores de Caixa de Correio, caixas de correio em Servidores de Caixa de Correio, e servidores de Transporte de Borda. Você pode usar os logs de controle de mensagens para perícia de mensagens, análise de fluxo de mensagens, relatórios e solução de problemas.

No Exchange 2013, você pode usar o cmdlet **Set-TransportService** ou o cmdlet **Set-MailboxServer** para todas as tarefas de configuração de controle de mensagens, pois o servidor de Caixa de Correio do Exchange 2013 contém o serviço de Transporte e as caixas de correio. Você pode usar quaisquer um desses cmdlets para realizar as seguintes alterações na configuração do controle de mensagens:

  - Habilitar ou desabilitar o controle de mensagens. O padrão é habilitado.

  - Especificar a localização dos arquivos de log de controle de mensagens.

  - Especificar um tamanho máximo para os arquivos individuais de log de controle de mensagens. O padrão é 10 MB.

  - Especificar o tamanho máximo do diretório que contém os arquivos de log de controle de mensagens. O padrão é 1.000 MB.

  - Especificar a idade dos arquivos de log de controle de mensagens: o padrão é 30 dias.

  - Habilitar ou desabilitar o log de assunto de mensagens nos logs de controle de mensagens. O padrão é habilitado.


> [!TIP]
> Também é possível utilizar o EAC (Centro de administração do Exchange) para habilitar ou desabilitar o controle de mensagens e para especificar o local dos arquivos de log de controle de mensagens.



Por padrão, o Exchange usa o log circular para limitar os logs de controle de mensagens com base no tamanho e na idade do arquivo, para ajudar a controlar o espaço em disco usado pelos arquivos de log de controle de mensagens.

**Sumário**

Pesquisar no log de controle de mensagens

Estrutura dos arquivos de log de controle de mensagens

Os campos nos arquivos de log de controle de mensagens

Tipos de eventos no log de controle de mensagens

Os valores de origem no log de controle de mensagens

Entradas de exemplo no log de ​​controle de mensagens

Problemas de segurança relacionados ao log de controle de mensagens

## Pesquisar no log de controle de mensagens

Os logs de controle de mensagens contêm grandes quantidades de dados à medida que as mensagens passam pelo servidor de Caixa de Correio do Exchange 2013 Quando se trata de pesquisar os logs de controle de mensagens, você tem opções diferentes.

  - **Get-MessageTrackingLog**   Os administradores podem usar este cmdlet para pesquisar o log de controle de mensagens e ver informações sobre as mensagens usando uma grande variedade de critérios de filtro. Para saber mais, confira [Logs de rastreamento de mensagens de pesquisa](search-message-tracking-logs-exchange-2013-help.md).

  - **Relatórios de entrega para administradores**   Os administradores podem usar a guia **Relatórios de entrega** no EAC (Centro de administração do Exchange) ou os cmdlets subjacentes **Search-MessageTrackingReport** e **Get-MesageTrackingReport** para pesquisar os logs de controle de mensagens e ver informações sobre as mensagens enviadas por uma caixa de correio específica na organização ou recebidas por ela. Para saber mais, confira [Notificações de entrega para administradores](delivery-reports-for-administrators-exchange-2013-help.md).

  - **Relatórios de entrega para usuários**   Os usuários podem usar a guia **Relatórios de entrega** no Outlook Web App para pesquisar os logs de controle de mensagens e ver informações sobre as mensagens enviadas para ou por suas próprias caixa de correio. Para saber mais, confira o artigo sobre [relatórios de entrega para usuários](https://go.microsoft.com/fwlink/?linkid=279920).

Voltar ao início

## Estrutura dos arquivos de log de controle de mensagens

Por padrão, os arquivos de log de controle de mensagem estão em %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking.

A convenção de nomenclatura para os arquivos de log no diretório de log de controle de mensagens é `MSGTRK`*yyyymmdd-nnnn*`.log`, `MSGTRKMA`*yyyymmdd-nnnn*`.log`, `MSGTRKMD`*yyyymmdd-nnnn*`.log` e `MSGTRKMS`*yyyymmdd-nnnn*`.log`. Os diferentes logs são usados pelos seguintes serviços:

  - **MSGTRK**   Estes logs estão associados ao serviço de Transporte.

  - **MSGTRKMA**   Estes logs estão associados às aprovações e rejeições usadas pelo transporte moderado. Para saber mais, confira [Gerenciar a aprovação de mensagens](manage-message-approval-exchange-2013-help.md).

  - **MSGTRKMD**   Estes logs estão associados às mensagens entregues a caixas de correio pelo serviço de Entrega de Transporte de Caixa e Correio.

  - **MSGTRKMS**   Estes logs estão associados a mensagens enviadas das caixas de correio pelo serviço de Envio de Transporte de Caixa de Correio.

Os espaços reservados nos nomes de arquivos de log representam as seguintes informações:

  - O espaço reservado *yyyymmdd* é a data UTC (Tempo Universal Coordenado) em que o arquivo de log foi criado. *yyyy* = ano, *mm* = mês e *dd* = dia.

  - O espaço reservado *nnnn* é um número de instância que começa com o valor 1 diariamente para cada prefixo do nome do arquivo de log de controle de mensagens.

As informações são gravadas em cada arquivo de log até que o tamanho do arquivo atinja o valor máximo especificado para cada arquivo de log. Em seguida, um novo arquivo de log que contém um número de instância incrementado é aberto. Esse processo repete-se ao longo do dia. A funcionalidade de rotação de arquivos de log exclui os arquivos de log mais antigos quando alguma das condições a seguir é verdadeira:

  - Um arquivo de log atinge sua idade máxima especificada.

  - O diretório de logs de controle de mensagens atinge seu tamanho máximo especificado.
    

    > [!IMPORTANT]
    > O tamanho máximo do diretório do log de controle de mensagens é calculado como o tamanho total de todos os arquivos de log que tenham o mesmo prefixo de nome. Outros arquivos que não seguem a convenção de prefixo de nome não são considerados no cálculo do tamanho total do diretório. Renomear arquivos de log antigos ou copiar outros arquivos para o diretório do log de controle de mensagens pode fazer com que o diretório exceda o tamanho máximo especificado.<BR>Em servidores de Caixa de Correio do Exchange 2013, o tamanho máximo do diretório de log de ​​controle de mensagens é três vezes maior que o valor especificado. Embora os arquivos de log de controle de mensagens gerados pelos quatro serviços diferentes tenham quatro prefixos de nomes diferentes, a quantidade e a frequência dos dados gravados nos arquivos de log <STRONG>MSGTRKMA</STRONG> são insignificantes quando comparados aos outros três prefixos de arquivo de log.



Os arquivos de log de controle de mensagens são arquivos de texto que contêm dados no formato de arquivo de CSV (valores separados por vírgula). Cada arquivo de log de controle de mensagens possui um cabeçalho com as seguintes informações:

  - **\#Software:**  o nome do software que criou o arquivo de log de controle de mensagens Geralmente, o valor é Microsoft Exchange Server.

  - **\#Version:**  o número da versão do software que criou o arquivo de log de controle de mensagens. Atualmente, o valor é 15.0.0.0.

  - **\#Log-Type:**    valor do tipo de log, que é o Log de Controle de Mensagens.

  - **\#Date:** a data e a hora UTC em que o arquivo de log foi criado. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, em que aaaa*yyyy* = ano, mm*mm* = mês, dd*dd* = dia, T indica o início de componente de hora, hh*hh* = hora, mm*mm* = minuto, ss*ss* = segundo, fff*fff* = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.

  - **\#Fields:**    os nomes de campos delimitados por vírgulas usados nos arquivos de log de controle de mensagens.

Voltar ao início

## Os campos nos arquivos de log de controle de mensagens

O log de controle de mensagens armazena cada evento de mensagem em uma única linha no log. As informações de evento de mensagens são organizadas por campos, que são separados por vírgulas. Geralmente, o nome do campo é suficientemente descritivo para determinar o tipo de informação que ele contém. Contudo, alguns campos podem estar em branco ou o tipo de informação armazenada no campo pode mudar com base no tipo de evento de mensagem e no tipo de arquivo de log de controle de mensagens em que o evento foi gravado. As descrições gerais dos campos que são utilizados para classificar cada evento de controle de mensagens são explicadas na tabela seguinte.


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
<td><p><strong>date-time</strong></p></td>
<td><p>A data e a hora UTC do evento de controle de mensagens. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, em que aaaa<em>yyyy</em> = ano, mm<em>mm</em> = mês, dd<em>dd</em> = dia, T indica o início de componente de hora, hh<em>hh</em> = hora, mm<em>mm</em> = minuto, ss<em>ss</em> = segundo, fff<em>fff</em> = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>O endereço IPv4 ou IPv6 do servidor de mensagens ou cliente de mensagens que enviou a mensagem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>O nome de host ou FQDN do servidor de mensagens ou cliente de mensagens que enviou a mensagem.</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>O endereço IPv4 ou IPv6 do servidor Exchange de origem ou de destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>O nome de host ou FQDN do servidor de destino.</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>Informações extras associadas ao campo <strong>source</strong>. Por exemplo, informações do agente de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>O nome do Conector de envio ou do Conector de recebimento de origem ou de destino. Por exemplo, <em>ServerName</em>\<em>ConnectorName</em> ou <em>ConnectorName</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>O componente de transporte do Exchange responsável pelo evento de controle de mensagens. Os valores encontrados nesse campo são descritos na seção Os valores de origem no log de controle de mensagens mais adiante neste tópico.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>O tipo de evento de mensagem. Os tipos de eventos são descritos na seção Tipos de eventos no log de controle de mensagens mais adiante neste tópico.</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>Um identificador de mensagem atribuído pelo servidor Exchange que está processando atualmente a mensagem.</p>
<p>O valor <strong>internal-message-id</strong> de uma mensagem específica é diferente no log de controle de mensagens de cada um dos servidores Exchange envolvidos na transmissão da mensagem. Um valor de exemplo é <code>73014444033</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>O valor do campo de cabeçalho <strong>Message-Id:</strong> encontrado no cabeçalho da mensagem. Se o campo de cabeçalho <strong>Message-Id:</strong> não existir ou estiver vazio, será atribuído um valor arbitrário. Esse valor é constante durante o tempo de vida da mensagem. Para mensagens criadas no Exchange, o valor está no formato <code>&lt;GUID@ServerFQDN&gt;</code>, incluindo os colchetes (<code>&lt; &gt;</code>). Por exemplo, <code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>. Outros sistemas de mensagens podem usar sintaxe ou valores diferentes.</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>Um valor de ID de mensagem exclusivo que persiste nas cópias da mensagem que podem ser criadas devido à bifurcação ou à expansão do grupo de distribuição. <code>1341ac7b13fb42ab4d4408cf7f55890f</code> é um exemplo de valor.</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>Os endereços de email dos destinatários da mensagem. Vários endereços de email são separados pelo caractere de ponto-e-vírgula (;).</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>Esse campo contém o status de cada destinatário separado pelo caractere de ponto-e-vírgula (;). Os valores de status são apresentados para os destinatários na mesma ordem que os valores no campo <strong>recipient-address</strong>. Valores de status de exemplo incluem <code>250 2.1.5 Recipient OK</code> ou <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>O tamanho da mensagem incluindo anexos, em bytes.</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>O número de destinatários existentes na mensagem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>Esse campo é usado com os eventos <strong>EXPAND</strong>, <strong>REDIRECT</strong> e <strong>RESOLVE</strong> para exibir outros endereços de email de destinatários associados à mensagem.</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>Esse campo contém informações adicionais para tipos específicos de eventos. Por exemplo:</p>
<p><strong>DSN</strong>   Contém o link de relatório, que é o valor <strong>Message-Id</strong> da DSN (notificação de status de entrega) associada se uma DSN for gerada após esse evento. Se essa for uma mensagem de DSN, o campo <strong>Reference</strong> conterá o valor <strong>Message-Id</strong> da mensagem original para a qual essa DNS foi gerada.</p>
<p><strong>EXPAND</strong>   O campo Reference contém o valor <strong>related-recipient-address</strong> das mensagens relacionadas.</p>
<p><strong>RECEIVE</strong>   O campo Reference pode conter o valor <strong>Message-Id</strong> da mensagem relacionada se a mensagem foi gerada por outros processos, por exemplo, regras de registro no diário ou de Caixa de Entrada.</p>
<p><strong>SEND</strong>   O campo Reference contém o valor <strong>Internal-Message-Id</strong> de qualquer mensagem de DSN.</p>
<p><strong>THROTTLE</strong>   O campo Reference contém o motivo pelo qual a mensagem foi limitada.</p>
<p><strong>TRANSFER</strong>   O campo Reference contém a Internet-Message-Id da mensagem que está sendo bifurcada.</p>
<p>Para as mensagens geradas por regras de caixa de entrada, o campo <strong>Reference</strong> contém o valor <strong>Internal-Message-Id</strong> da mensagem de entrada que fez com que a regra de caixa de entrada gerasse a mensagem de saída.</p>
<p>Para outros tipos de eventos, o campo <strong>Reference</strong> pode conter o valor <strong>Internal-Message-Id</strong> para mensagens bifurcadas.</p>
<p>Para outros tipos de eventos, o campo <strong>Reference</strong> geralmente está em branco.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>O assunto da mensagem encontrado no campo de cabeçalho <code>Subject:</code>. O acompanhamento dos assuntos das mensagens é controlado pelo parâmetro <em>MessageTrackingLogSubjectLoggingEnabled</em> nos cmdlets <strong>Set-TransportService</strong> ou <strong>Set-MailboxServer</strong>. Por padrão, o acompanhamento dos assuntos da mensagem está habilitado.</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p>O endereço de email especificado no campo de cabeçalho <code>Sender:</code> ou no campo de cabeçalho <code>From:</code>, se <code>Sender:</code> não existir.</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>O endereço de email de retorno especificado por <code>MAIL FROM:</code> no envelope da mensagem. Embora esse campo nunca esteja vazio, ele pode ter o valor nulo do endereço do remetente, representado como <code>&lt;&gt;</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>Informações adicionais sobre a mensagem. Por exemplo:</p>
<ul>
<li><p>A data e a hora UTC de origem da mensagem para eventos <strong>DELIVER</strong> e <strong>SEND</strong>. A data e a hora de origem é o momento em que a mensagem entrou pela primeira vez na organização do Exchange. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, em que aaaa<em>yyyy</em> = ano, mm<em>mm</em> = mês, dd<em>dd</em> = dia, T indica o início de componente de hora, hh<em>hh</em> = hora, mm<em>mm</em> = minuto, ss<em>ss</em> = segundo, fff<em>fff</em> = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.</p></li>
<li><p>Erros de autenticação. Por exemplo, você pode ver o valor <code>11a</code> e o tipo de autenticação usados quando ocorrem erros de autenticação.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>A direção da mensagem. Os valores de exemplo incluem <code>Incoming</code>, <code>Undefined</code> e <code>Originating</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>Esse campo não é usado em organizações locais do Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>O endereço IPv4 ou IPv6 do cliente original.</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>O endereço IPv4 ou IPv6 do servidor original.</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>Esse campo contém dados relacionados a tipos específicos de eventos. Por exemplo, o agente de Regra de Transporte usa esse campo para gravar o GUID da regra de transporte ou a política de DLP que atuou na mensagem. Para saber mais sobre esses valores de agente de Regra de Transporte, confira a seção &quot;Log de Dados&quot;, no tópico <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">Exibir relatórios de detecção de política DLP</a>,</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Tipos de eventos no log de controle de mensagens

Vários tipos de eventos no campo **event-id** são usados para classificar os eventos de mensagens no log de controle de mensagens. Alguns eventos de mensagens aparecem em apenas um tipo de arquivo de log de controle de mensagens, enquanto outros aparecem em todos os tipos de arquivos de log de controle de mensagens. Os tipos de eventos usados para classificar cada evento de mensagem são explicados na tabela a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do evento</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>Esse evento é usado por agentes de transporte para registrar dados personalizados.</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>Uma mensagem enviada pelo diretório de Retirada ou pelo diretório de Repetição que não pode ser entregue nem retornada.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>A entrega da mensagem foi atrasada.</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>Uma mensagem foi entregue a uma caixa de correio local.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>Uma mensagem foi removida sem uma notificação de status de entrega (também conhecida como uma DSN, mensagem de devolução, notificação de falha na entrega ou NDR). Por exemplo:</p>
<ul>
<li><p>Mensagens de solicitação de aprovação de moderação concluídas.</p></li>
<li><p>Mensagens de spam silenciosamente descartadas sem uma NDR.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>Uma notificação de status de entrega (DSN) foi gerada.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>Uma mensagem duplicada foi entregue ao destinatário. A duplicação poderá ocorrer se um destinatário for membro de vários grupos de distribuição aninhados. As mensagens duplicadas são detectadas e removidas pelo repositório de informações.</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>Durante a expansão do grupo de distribuição, um destinatário duplicado foi detectado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>Um destinatário alternativo para a mensagem já era um destinatário.</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>Um grupo de distribuição foi expandido.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>Falha na entrega da mensagem. Os valores de exemplo incluem <strong>SMTP</strong>, <strong>DNS</strong>, <strong>QUEUE</strong> e <strong>ROUTING</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>A mensagem de sombra foi descartada após a cópia primária ser entregue para o próximo salto. Para saber mais, confira <a href="shadow-redundancy-exchange-2013-help.md">Redundância de sombra</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>A mensagem de sombra foi recebida pelo servidor no DAG (grupo de disponibilidade do banco de dados) local ou site do Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>Uma mensagem de sombra foi criada.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>Falha ao criar uma mensagem de sombra. Os detalhes são armazenados no campo <strong>source-context</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>Uma mensagem foi enviada a um destinatário moderado e, portanto, ela foi enviada à caixa de correio de arbitragem para aprovação. Para saber mais, confira <a href="manage-message-approval-exchange-2013-help.md">Gerenciar a aprovação de mensagens</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>Uma mensagem foi carregada com êxito durante a inicialização.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>Um moderador para um destinatário moderado nunca aprovou ou rejeitou a mensagem e, portanto, ela expirou. Para saber mais sobre destinatários moderados, confira <a href="manage-message-approval-exchange-2013-help.md">Gerenciar a aprovação de mensagens</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>Um moderador para um destinatário moderado aprovou a mensagem e, portanto, ela foi entregue ao destinatário moderado.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>Um moderador para um destinatário moderado rejeitou a mensagem e, portanto, ela não foi entregue ao destinatário moderado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>Não foi possível entregar nenhuma solicitação de aprovação enviadas a todos os moderadores de um destinatário moderado e isso resultou em NDRs (notificações de falha na entrega).</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>Uma mensagem foi detectada na Caixa de Saída de uma caixa de correio no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>Uma mensagem foi detectada na Caixa de Saída de uma caixa de correio no servidor local, e uma cópia de sombra da mensagem precisa ser criada.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>Uma mensagem foi colocada na fila de mensagens suspeitas ou removida dessa fila.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>A mensagem foi processada com êxito.</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>Uma mensagem de reunião foi processada pelo serviço de Entrega de Transporte de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>Uma mensagem foi recebida pelo componente de recebimento SMTP do serviço de transporte ou os diretórios de Retirada ou Repetição (origem: <code>SMTP</code>), ou uma mensagem foi enviada de uma caixa de correio para o serviço de Envio de Transporte de Caixa de Correio (origem: <code>STOREDRIVER</code>).</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>Uma mensagem foi redirecionada para um destinatário alternativo após uma pesquisa do Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>Os destinatários de uma mensagem foram resolvidos para um endereço de email diferente após uma pesquisa do Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>Uma mensagem foi reenviada automaticamente a partir da Rede Segura. Para saber mais, confira <a href="safety-net-exchange-2013-help.md">Rede de Segurança</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>Uma mensagem reenviada a partir da Rede Segura foi adiada.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>Uma mensagem reenviada da Rede Segura falhou.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>Uma mensagem foi enviada por SMTP entre serviços de transporte.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>O serviço de Envio de Transporte de Caixa de Correio transmitiu com êxito a mensagem para o serviço de Transporte. Para eventos <strong>SUBMIT</strong>, a propriedade <strong>source-context</strong> contém os seguintes detalhes:</p>
<ul>
<li><p><strong>MDB</strong>   A GUID do banco de dados da caixa de correio.</p></li>
<li><p><strong>Mailbox</strong>   A GUID da caixa de correio.</p></li>
<li><p><strong>Event</strong>   O número de sequência do evento.</p></li>
<li><p><strong>MessageClass</strong>   O tipo da mensagem. Por exemplo, <code>IPM.Note</code>.</p></li>
<li><p><strong>CreationTime</strong>   A data e a hora do envio da mensagem.</p></li>
<li><p><strong>ClientType</strong>   Por exemplo, <code>User</code>, <code>OWA</code> ou <code>ActiveSync</code>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>A transmissão de mensagens do serviço de Envio de Transporte da Caixa de Correio para o serviço de Transporte foi adiada.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>A transmissão de mensagem do serviço de Envio de Transporte da Caixa de Correio para o serviço de Transporte falhou.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>A transmissão de mensagem foi suprimida.</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>A mensagem foi limitada.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>Os destinatários foram movidos para uma mensagem bifurcada devido à conversão do conteúdo, limites de destinatário de mensagem ou agentes. As origens incluem <strong>ROUTING</strong> ou <strong>QUEUE</strong>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Os valores de origem no log de controle de mensagens

Os valores no campo **source** no log de controle de mensagens indicam o componente de transporte que é responsável pelo evento de controle de mensagens. A tabela a seguir descreve os valores do campo **source**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor de origem</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>A origem do evento foi intervenção humana. Por exemplo, um administrador usou o Visualizador de Filas para excluir uma mensagem ou enviou arquivos de mensagens usando o diretório de Repetição.</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>A origem do evento foi um agente de transporte</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>A origem do evento foi a estrutura de aprovação que é usada com destinatários moderados. Para saber mais, confira <a href="manage-message-approval-exchange-2013-help.md">Gerenciar a aprovação de mensagens</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>A origem do evento foi mensagens não processadas que havia no servidor no momento da inicialização. Isso está relacionado ao tipo de evento <strong>LOAD</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>A origem do evento foi DNS.</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>A origem do evento foi uma DSN (notificação de status de entrega). Por exemplo, uma NDR (notificação de falha na entrega).</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>A origem do evento foi um conector Externo. Para saber mais, confira <a href="foreign-connectors-exchange-2013-help.md">Conectores externos</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>A origem do evento foi uma regra de caixa de entrada. Para saber mais, confira o artigo sobre <a href="https://go.microsoft.com/fwlink/p/?linkid=285479">regras de caixa de entrada</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>A origem do evento foi um processador de mensagens de reuniões que atualiza calendários com base em atualizações de reunião.</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>A origem do evento foi um ORAR (Destinatário Alternativo Solicitado pelo Remetente). Você pode habilitar ou desabilitar o suporte para ORAR em conectores de Recebimento usando o parâmetro <em>OrarEnabled</em> nos cmdlets <strong>New-ReceiveConnector</strong> ou <strong>Set-ReceiveConnector</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>A origem do evento foi o diretório de Retirada. Para saber mais, confira <a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Diretório de retirada e repetição</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>A origem do evento foi o identificador de mensagens suspeitas. Para saber mais sobre mensagens suspeitas e a fila de mensagens suspeitas, confira <a href="queues-exchange-2013-help.md">Filas</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>A origem do evento foi uma pasta pública habilitada para email.</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>A origem do evento foi uma fila.</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>A origem do evento foi a redundância de sombra. Para saber mais, confira <a href="shadow-redundancy-exchange-2013-help.md">Redundância de sombra</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>A origem do evento foi o componente de resolução de roteamento do categorizador no serviço de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>A origem do evento foi a Rede Segura. Para saber mais, confira <a href="safety-net-exchange-2013-help.md">Rede de Segurança</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>A mensagem foi enviada pelo componente de envio ou recebimento SMTP do serviço de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>A origem do evento foi um envio MAPI de uma caixa de correio no servidor local.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Entradas de exemplo no log de ​​controle de mensagens

Uma mensagem sem eventos enviada entre dois usuários gera várias entradas no log de controle de mensagens. Você pode ver os resultados usando o cmdlet **Get-MessageTrackingLog**. Para saber mais, confira [Logs de rastreamento de mensagens de pesquisa](search-message-tracking-logs-exchange-2013-help.md).

Este é um exemplo condensado das entradas de log de controle de mensagens criadas quando o usuário chris@contoso.com envia com êxito uma mensagem de teste para o usuário michelle@contoso.com. Os dois usuários têm caixas de correio no mesmo servidor.

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

Voltar ao início

## Problemas de segurança relacionados ao log de controle de mensagens

Nenhum conteúdo de mensagem é armazenado no log de controle de mensagens. Por padrão, a linha de assunto de uma mensagem de email é armazenada no log de controle de mensagens. Se quiser desabilitar o log de assunto das mensagens para atender aos requisitos de segurança ou privacidade mais rigorosos. Antes de habilitar ou desabilitar o log de assunto das mensagens, verifique qual é a política da sua organização quanto à revelação das informações da linha de assunto. Para saber mais, confira [Configurar o rastreamento de mensagem](configure-message-tracking-exchange-2013-help.md).

Voltar ao início

