---
title: 'Filas: Exchange 2013 Help'
TOCTitle: Filas
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51407930
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Uma *fila* é um local de armazenamento temporário para mensagens que estão aguardando entrar no próximo estágio de processamento ou entrega para um destino. Cada fila representa um conjunto lógico de mensagens que o servidor do Exchange processa em uma determinada ordem. No Microsoft Exchange Server 2013, as filas armazenam mensagens antes, durante e depois da entrega. Há filas nos servidores de Caixa de Correio e nos servidores de Transporte de Borda. Os servidores de Caixa de Correio e os servidores de Transporte de Borda são chamados de *servidores de transporte* neste tópico.

Como as versões anteriores do Exchange, o Exchange 2013 usa um único banco de dados ESE (Extensible Storage Engine) para o armazenamento da fila.

Você pode gerenciar filas e as mensagens nas filas usando o Shell de Gerenciamento do Exchange e o Visualizador de Filas na Caixa de Ferramentas do Exchange. Você pode usar essas interfaces para exibir o status e o conteúdo de filas e propriedades detalhadas das mensagens. Essas interfaces também podem ser usadas para executar ações que modificam filas ou as mensagens nas filas.

**Sumário**

  - Types of queues

  - Queue database files

  - Queue properties
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate, and Velocity
    
      - Queue status
    
      - Other queue properties

  - Message properties
    
      - Message status
    
      - Other message properties

  - Manage queues and messages in queues

## Tipos de filas

Os seguintes tipos de filas são usados no Exchange 2013:

  - **Filas persistentes**   As *filas persistentes* existem em cada servidor de transporte em cada organização do Exchange. Assim como nas versões anteriores do Exchange, há três filas persistentes no Exchange 2013:
    
      - **Fila de envio**   A Fila de envio é usada pelo categorizador para reunir todas as mensagens que devem ser resolvidas, direcionadas e processadas pelos agentes de transporte no servidor de transporte. Todas as mensagens recebidas por um servidor de transporte entram para processamento na fila de Envio. Nos servidores de Caixa de Correio, as mensagens são enviadas por um conector Receber, pelos diretórios Retirada ou Repetição, ou pelo serviço Envio de Transporte de Caixa de Correio. Nos servidores de Transporte de Borda, as mensagens geralmente são enviadas por um conector Receber, mas os diretórios Retirada e Repetição também estão disponíveis.
        
        O categorizador recupera mensagens desta fila e, entre outras coisas, determina o local do destinatário e a rota para esse local. Após a categorização, a mensagem é movida para uma fila de entregas ou para a fila de inacessíveis. Cada servidor de transporte tem apenas uma fila de Envio. As mensagens que estão na fila de Envio não podem estar em outras filas ao mesmo tempo. Para obter mais informações sobre o categorizador e o pipeline de transporte, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md).
    
      - **Fila Inacessível**   A fila Inacessível contém mensagens que não podem ser direcionadas a seus destinos. Normalmente, um destino inacessível é causado por alterações na configuração que modificaram o caminho de roteamento para entrega. Independente do destino, todas as mensagens que tenham destinatários inacessíveis residem nessa fila. Cada servidor de transporte tem apenas uma fila Inacessível.
        
        As mensagens na fila Inacessível são automaticamente reenviadas quando há uma alteração no direcionamento. Então, após de corrigir o erro de condição ou configuração que fez as mensagens entrarem na fila Inacessível, você não precisa fazer mais nada para remover as mensagens da fila Inacessível para entrega.
        
        A fila Inacessível geralmente fica vazia. Se a fila Inacessível não contiver mensagens, ela não aparece no Visualizador de Fila ou nos resultados de **Get-Queue**.
    
      - **Fila de mensagens suspeitas**   A fila de mensagens suspeitas é uma fila especial usada para isolar mensagens determinadas como prejudiciais ao sistema do Exchange 2013 após um servidor ou serviço de transporte falhar. As mensagens podem ser realmente perigosas em seu conteúdo e formato. Por outro lado, elas podem ser os resultados de um agente gravado inadequadamente que causou a falha do servidor Exchange quando ele processou as mensagens supostamente inválidas.
        
        A fila de mensagens suspeitas geralmente fica vazia. Se a fila de mensagens suspeitas não contiver mensagens, ela não aparece no Visualizador de Fila ou nos resultados de **Get-Queue**. As mensagens na fila de mensagens suspeitas nunca são reiniciadas ou expiradas automaticamente. As mensagens permanecem na fila de mensagens suspeitas até que sejam reiniciadas ou removidas manualmente por um administrador.

  - **Filas de entrega**   As filas de Entrega armazenam as mensagens que estão sendo entregues a qualquer destino local ou remoto usando SMTP. Todas as mensagens são transmitidas entre os servidores do Exchange usando SMTP. Os destinos que não são SMTP também usam filas de entrega se o destino for alimentado por um conector de Agente de Entrega. . Cada fila de entrega contém mensagens que estão sendo direcionadas para o mesmo destino. É praticamente inevitável que várias filas de entrega existam em um servidor de transporte. As filas de entrega são criadas dinamicamente quando necessárias e são excluídas automaticamente quando a fila está vazia e o tempo de validade passou. O tempo de validade da fila é controlado pelo parâmetro *QueueMaxIdleTime* no cmdlet **Set-TransportService**. O valor padrão é três minutos.

  - **Filas de sombra**   As filas de Sombra armazenam cópias redundantes de uma mensagem enquanto esta está em trânsito. Para obter mais informações, consulte [Redundância de sombra](shadow-redundancy-exchange-2013-help.md).

  - **Rede Segura**   A Rede Segura mantém cópias de mensagens que foram entregues com êxito pelo servidor de transporte. Apesar de não ser acessível pelas ferramentas de gerenciamento de fila, a Rede Segura é apenas mais uma fila no banco de dados de filas. Para obter mais informações, consulte [Rede de Segurança](safety-net-exchange-2013-help.md).

Voltar ao início

## Arquivos de bancos de dados de filas

Todas as filas diferentes são armazenadas em um único banco de dados ESE. Por padrão, este banco de dados de filas está localizado no servidor de transporte em `%ExchangeInstallPath%TransportRoles\data\Queue`.

Como todos os bancos de dados ESE, o banco de dados de filas usa arquivos de log para aceitar, controlar e manter dados. Para melhorar o desempenho, todas as transações de mensagem são gravadas primeiramente em arquivos de log e na memória e, em seguida, no arquivo do banco de dados. O arquivo de ponto de verificação controla as entradas do log de transações que foram confirmadas no banco de dados. Durante um encerramento normal do serviço de Transporte do Microsoft Exchange, alterações não confirmadas do banco de dados encontradas nos logs de transações são sempre confirmadas no banco de dados.

O log circular é usado no banco de dados de filas. Isso significa que o histórico das transações confirmadas encontradas nos logs de transações não é mantido. Todos os logs de transações mais antigos do que o ponto de verificação atual são imediata e automaticamente excluídos. Portanto, os logs de transações não podem ser repetidos para a recuperação do banco de dados de filas a partir do backup.

O Exchange 2013 usa as *tabelas de geração* para armazenar e limpar mensagens no banco de dados de filas. Em vez de processar e excluir registros de mensagens individuais de uma tabela grande, o banco de dados de filas armazena mensagens em tabelas baseadas em tempo e apenas exclui a tabela toda após todas as mensagens da tabela terem sido processadas com sucesso. Por exemplo, todas as mensagens na fila de 13h00 a 14h00, independente da fila ou do destino, são armazenadas na tabela `1p-2p_msgs`. Às 14h00, novas mensagens são armazenadas na tabela `2p-3p_msgs`. Às 16h00, uma nova tabela chamada `4p-5p_msgs` é criada, e toda a tabela `1p-2p_msgs` é excluída, mas apenas se todas as mensagens da tabela tiverem sido processadas com sucesso. Esta abordagem de excluir toda a mensagem de tabelas em vez de mensagens individuais ajuda a melhorar o desempenho de E/S da unidade que armazena o banco de dados de filas.

A tabela a seguir lista os arquivos que constituem o banco de dados de filas.

### Arquivos que constituem o banco de dados de filas

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Arquivo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>Este arquivo do banco de dados de filas armazena todas as mensagens em fila.</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>Este arquivo temporário do banco de dados é usado para verificar o esquema do banco de dados de filas na inicialização.</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>Este log de transações registra todas as alterações no banco de dados de filas. As alterações nos bancos de dados são gravadas primeiramente no log de transações e, em seguida, confirmadas no banco de dados. O Trn.log is é o arquivo ativo atual do log de transações. O Trntmp.log é o próximo arquivo configurado do log de transações criado antecipadamente. Caso o arquivo existente Trn.log do log de transações atinja seu tamanho máximo, o Trn.log será renomeado como Trn<em>nnnn</em>.log, onde <em>nnnn</em> é um número sequencial. O Trntmp.log será renomeado como Trn.log e se tornará o arquivo ativo atual do log de transações.</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>Este arquivo de ponto de verificação controla as entradas do log de transações confirmadas no banco de dados. Este arquivo está sempre no mesmo local do arquivo mail.que.</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>Estes arquivos do log de transações de reserva agem como espaços reservados. São usados apenas quando a unidade de disco rígido que contém o log de transações está sem espaço para parar normalmente o banco de dados de filas.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Opções para configuração de bancos de dados de filas

Configure o banco de dados de filas adicionando ou alterando chaves no arquivo de configuração do aplicativo XML em `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. Esse arquivo é associado ao serviço de Transporte do Microsoft Exchange. As alterações feitas ao arquivo EdgeTransport.exe.config entram em vigor após a reinicialização do serviço de Transporte do Microsoft Exchange.

A seção `<appSettings>` do arquivo EdgeTransport.exe.config é onde você pode adicionar novas chaves ou alterar as chaves existentes. Se não houver uma chave específica, você pode adicioná-la manualmente para alterar seu valor.

As chaves do banco de dados de filas disponíveis no arquivo EdgeTransport.exe.config são descritas na tabela a seguir.

### Chaves do banco de dados de filas de mensagens disponíveis no arquivo EdgeTransport.exe.config

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
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>Esta chave especifica a quantidade de operações de E/S do banco de dados que podem ser agrupadas antes de serem executadas. Por padrão, essa chave não existe no arquivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>Esta chave especifica o tempo máximo em milissegundos que o banco de dados aguardará para várias operações de E/S do banco de dados serem agrupadas antes de serem executadas. As operações de E/S do banco de dados são executadas sem aguardar mais, caso as seguintes condições forem verdadeiras:</p>
<ul>
<li><p>A quantidade de operações de E/S do banco de dados especificada pela chave <em>QueueDatabaseBatchSize</em> não foi atingida.</p></li>
<li><p>O tempo especificado pela chave <em>QueueDatabaseBatchTimeout</em> passou.</p></li>
</ul>
<p>Por padrão, essa chave não existe no arquivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>Esta chave especifica a quantidade de conexões ESE do banco de dados que podem ser abertas.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>Esta chave especifica a memória usada para armazenar em cache os registros de transação antes de serem gravados no arquivo de registro de transações.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>Esta chave especifica o tamanho máximo de um arquivo de registro de transações. Quando o tamanho máximo do arquivo de log for atingido, um novo arquivo de log é aberto.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Esta chave especifica o diretório padrão para os arquivos de registro de banco de dados de filas. Para obter instruções de como alterar o local do banco de dados de filas, consulte <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Alterar o local do banco de dados de fila</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>Esta chave especifica a quantidade máxima de itens de trabalho de limpeza em segundo plano que podem ser enfileirados no pool de threads do mecanismo do banco de dados a qualquer momento.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>Verdadeiro</p></td>
<td><p>A chave habilita ou desabilita a desfragmentação online programada do banco de dados de filas de email. Por padrão, essa chave não existe no arquivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> ou 1:00 A.M.</p></td>
<td><p>Esta chave especifica a hora do dia no formato de 24 horas para iniciar a desfragmentação online do banco de dados de filas de email. Para especificar um valor, insira-o no formato de tempo: <em>hh:mm:ss</em>, onde<em>h</em> = horas, <em>m</em> = minutos e <em>s</em> = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> ou 3 horas</p></td>
<td><p>Esta chave especifica por quanto tempo a tarefa de desfragmentação online pode ser executada. Mesmo que a tarefa de desfragmentação não seja concluída no tempo especificado, o banco de dados de filas será deixado em um estado consistente. Para especificar um valor, insira-o no formato de tempo: <em>hh:mm:ss</em>, onde<em>h</em> = horas, <em>m</em> = minutos e <em>s</em> = segundos.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Esta chave especifica o diretório padrão para os arquivos de bancos de dados de filas. Para obter instruções de como alterar o local do banco de dados de filas, consulte <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Alterar o local do banco de dados de fila</a>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.



Voltar ao início

## Propriedades da fila

Uma fila tem várias propriedades que descrevem o propósito e o status da fila. Algumas propriedades de fila são aplicadas à fila quando ela é criada, e não mudam. Outras contêm indicadores de status, tamanho, tempo ou outros indicadores que são atualizados com frequência.

Voltar ao início

## NextHopSolutionKey

O componente de direcionamento do categorizador no serviço de Transporte do Microsoft Exchange seleciona o destino de uma mensagem e este destino é usado para criar a fila de entrega. O destino é gravado em cada destinatário como o atributo **NextHopSolutionKey**. Cada valor exclusivo do atributo **NextHopSolutionKey** corresponde a uma fila de entrega separada.

O atributo **NextHopSolutionKey** contém os seguintes campos:

  - **DeliveryType**   O valor deste campo representa os resultados da categorização da mensagem e como o serviço de Transporte pretende transmitir a mensagem para o próximo salto, que pode ser o destino final da mensagem ou um salto intermediário no caminho. O serviço de Transporte usa uma lista predefinida de valores para **DeliveryType** com base no destino de direcionamento alvo ou no grupo de entrega.

  - **NextHopDomain**   Este campo usa valores específicos com base no valor do campo **DeliveryType**. Para filas de entrega, o valor deste campo é efetivamente o nome da fila. O valor de **NextHopDomain** nem sempre é um nome de domínio. Por exemplo, o valor poderia ser o nome do site do Active Directory de destino ou do grupo de disponibilidade do banco de dados (DAG). Pense neste campo como o nome do próximo salto, em que o valor é o nome do destino de direcionamento ou o grupo de entrega de destino.

  - **NextHopConnector**   Este campo usa valores específicos com base no valor do campo **DeliveryType**. O valor é sempre expresso como uma GUID. Se este campo não for usado, o valor será uma GUID só com zeros. O valor de **NextHopConnector** nem sempre é uma GUID de um conector. Por exemplo, o valor poderia ser a GUID do site do Active Directory de destino ou o DAG. Pense neste campo como a GUID do próximo salto, em que o valor é a GUID do destino de direcionamento ou o grupo de entrega de destino.

O Exchange 2013 também adiciona a propriedade **NextHopCategory** à fila com base no valor de **DeliveryType**. O valor de **NextHopCategory** é `External` ou `Internal`. O valor `External` indica que o próximo salto da fila está fora da organização do Exchange. O valor `Internal` indica que o próximo salto da fila está dentro da organização do Exchange. Observe que uma mensagem para um destinatário externo pode exigir um ou mais saltos internos antes de a mensagem ser entregue externamente.

Os valores de **DeliveryType**, **NextHopCategory**, **NextHopDomain** e **NextHopConnector** estão descritos na tabela a seguir.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de entrega no Visualizador de Fila</th>
<th>DeliveryType no Shell</th>
<th>Descrição</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Agente de entrega</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>A fila armazena mensagens para entrega a destinatários em um espaço de endereço que não seja SMTP. As mensagens são entregues usando um conector de Agente de entrega configurado no servidor local.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor é o espaço do endereço de destino configurado no conector do Agente de entrega.</p></td>
<td><p>Este valor é a GUID do conector do Agente de entrega. Por exemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>A fila armazena as mensagens para entrega a destinatários em um espaço de endereço SMTP. As mensagens são entregues usando um conector de Envio configurado no servidor local. O conector de Envio está configurado para usar o direcionamento de DNS.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor é o espaço de endereço de destino configurado no conector de Envio. Por exemplo, <code>contoso.com</code>.</p></td>
<td><p>Esse valor é o GUID do conector de Envio. Por exemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>A fila armazena mensagens para entrega a destinatários em um espaço de endereço que não seja SMTP. As mensagens são entregues usando um conector Estrangeiro configurado no servidor local.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor é o espaço do endereço de destino configurado no conector Estrangeiro.</p></td>
<td><p>Este valor é a GUID do conector Estrangeiro. Por exemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>A fila armazena as mensagens para entrega a destinatários em um espaço de endereço SMTP. As mensagens são entregues usando um conector de Envio configurado no servidor local. O conector de Envio está configurado para usar o direcionamento de host inteligente.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor é a lista de hosts inteligentes que estão configurados no conector de Envio. Os hosts inteligentes podem ser configurados como FQDNs, endereços IP ou ambos. Os valores podem ser um dos seguintes:</p>
<ul>
<li><p><strong>FQDN</strong>   A sintaxe é <code>&lt;FQDN1,FQDN2,...&gt;</code>. Por exemplo, <code>smarthost01.contoso.com</code> ou <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>.</p></li>
<li><p><strong>Endereço IP</strong>   A sintaxe é <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>. Por exemplo, <code>[10.10.10.100]</code> ou <code>[10.10.10.100],[10.10.10.101]</code>.</p></li>
<li><p><strong>FQDN e endereço IP</strong>   A sintaxe é <code>&lt;[IPAddress1],FQDN1,...&gt;</code> e depende de como os hosts inteligentes estão listados no conector de Envio. Por exemplo, <code>[172.17.17.7],relay.tailspintoys.com</code> ou <code>mail.contoso.com,[192.168.1.50]</code>.</p></li>
</ul></td>
<td><p>Esse valor é o GUID do conector de Envio. Por exemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Entrega SMTP à Caixa de Correio</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>A fila armazena as mensagens para entrega aos destinatários de caixa de correio do Exchange 2013. O banco de dados de caixas de correio de destino está em um dos seguintes locais:</p>
<ul>
<li><p>O servidor de Caixa de Correio do Exchange 2013 local.</p></li>
<li><p>Um servidor de Caixa de Correio do Exchange 2013 no mesmo DAG.</p></li>
<li><p>Um servidor de Caixa de Correio do Exchange 2013 no mesmo site do Active Directory em ambientes que não são DAG.</p></li>
</ul></td>
<td><p>Interno</p></td>
<td><p>Este valor é o nome do banco de dados de caixas de correio de destino. Por exemplo, <code>Mailbox Database 0471695037</code>.</p></td>
<td><p>Este valor é a GUID do banco de dados de caixas de correio de destino. Por exemplo, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Retransmissão SMTP para servidores de origem do conector de envio</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>A fila armazena mensagens para entrega a destinatários que são SMTP ou não são SMTP. As mensagens são entregues usando um conector de Envio, um conector de Agente de entrega ou um conector Estrangeiro configurado em um servidor de transporte remoto. O servidor de transporte remoto poderia ser um servidor de Caixa de Correio do Exchange 2013 ou um servidor de Transporte de hub do Exchange 2007 ou do Exchange 2010 de uma versão anterior do Exchange. O servidor remoto pode estar localizado no site do Active Directory local ou em um site do Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor é o nome do conector de Envio, do conector do Agente de entrega ou do conector Estrangeiro de destino. Por exemplo, <code>Contoso.com Send Connector</code>.</p></td>
<td><p>Este valor é a GUID do conector de Envio, do conector do Agente de entrega ou do conector Estrangeiro de destino. Por exemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Retransmissão SMTP para o grupo de disponibilidade do banco de dados</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>A fila armazena mensagens para entrega aos destinatários de caixa de correio do Exchange 2013, em que o banco de dados de caixas de correio de destino está localizado em um DAG remoto. O DAG remoto pode estar no site do Active Directory local ou em um site do Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor é o nome do DAG de destino. Por exemplo, <code>DAG1</code>.</p></td>
<td><p>Este valor é a GUID do DAG de destino. Por exemplo, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Retransmissão SMTP para o grupo de entrega de caixa de correio</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>A fila armazena mensagens para entrega a destinatários de caixa de correio antigas, em que a caixa de correio de destino está ativada em um servidor de Caixa de Correio do Exchange 2007 ou do Exchange 2010. A mensagem está relacionada a um servidor de Transporte de Hub que está em execução na mesma versão do Exchange que a caixa de correio de destino. O servidor de Transporte de Hub de destino pode estar no site do Active Directory local ou em um site do Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>O nome da fila usa a sintaxe: <code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>, em que <em>&lt;ADSiteName&gt;</em> é o nome do site do Active Directory de destino e <em>&lt;ExchangeVersion&gt;</em> é a versão do Exchange no servidor de Caixa de Correio.</p></td>
<td><p>Este valor fica em branco.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Retransmissão de SMTP para Site do Active Directory Remoto</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>A fila armazena mensagens para entrega a um destino remoto e a topologia de direcionamento requer que a mensagem seja direcionada por um site específico do Active Directory. O site é um salto intermediário no caminho para o destino final. Esta situação ocorre sob as seguintes condições:</p>
<ul>
<li><p>A mensagem precisa ser direcionada por um site de hub.</p></li>
<li><p>A mensagem requer a entrega por um conector de Envio configurado em um servidor de Transporte de Borda que está inscrito em um site remoto do Active Directory.</p></li>
</ul></td>
<td><p>Interno</p></td>
<td><p>Este valor é o nome do site do Active Directory de destino. Por exemplo, <code>NorthAmericanSite</code>.</p></td>
<td><p>Este valor é a GUID do site do Active Directory de destino. Por exemplo, <code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Retransmissão SMTP a servidores especificados do Exchange</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>A fila armazena as mensagens para entrega a um grupo de distribuição configurado para um servidor de expansão específico. A expansão pode ser um servidor de Caixa de Correio do Exchange 2013 ou um servidor de Transporte de Hub do Exchange 2007 ou do Exchange 2010. O servidor pode estar em um site local ou remoto do Active Directory.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor é o FQDN do servidor de expansão de destino. Por exemplo, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Este valor é <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Retransmissão SMTP no site do Active Directory para o servidor de Transporte de Borda</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>A fila armazena as mensagens para entrega em um espaço de endereço SMTP. As mensagens são entregues usando um conector de Envio configurado em um servidor de Transporte de Borda inscrito no site local do Active Directory.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor é o nome do conector de Envio que envia o correio de saída da Internet da organização para a Internet. Este conector de Envio é criado automaticamente pela inscrição de Borda e é chamado <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>. <em>&lt;ADSiteName&gt;</em> é o nome do site local do Active Directory no qual o servidor de Transporte de Borda está inscrito.</p></td>
<td><p>Esse valor é o GUID do conector de Envio. Por exemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Pulsação</strong></p></td>
<td><p><strong>Pulsação</strong></p></td>
<td><p>Este valor está reservado para uso interno da Microsoft. Para obter mais informações sobre a pulsação, consulte <a href="shadow-redundancy-exchange-2013-help.md">Redundância de sombra</a>.</p></td>
<td><p>n/d</p></td>
<td><p>n/d</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p><strong>Redundância de Sombra</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>A fila armazena mensagens em uma fila de sombra. Uma fila de sombra armazena cópias redundantes de mensagens em trânsito no caso de as mensagens originais não serem entregues com êxito. Para obter mais informações, consulte <a href="shadow-redundancy-exchange-2013-help.md">Redundância de sombra</a>.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor é a FQDN do servidor primário para o qual a fila de sombra está armazenando as cópias redundantes das mensagens primárias. Por exemplo, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Este valor é <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Indefinido</strong></p></td>
<td><p><strong>Indefinido</strong></p></td>
<td><p>este valor é usado apenas na fila de Envio e na fila de mensagens suspeitas.</p></td>
<td><p>Interno</p></td>
<td><p>Para a fila de Envio, este valor é <code>Submisssion</code>. Para a fila de mensagens suspeitas, este valor é <code>Poison Message</code>.</p></td>
<td><p>Este valor é <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inacessíveis</strong></p></td>
<td><p><strong>Inacessível</strong></p></td>
<td><p>Este valor é usado apenas na fila Inacessíveis.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor é <code>Unreachable Domain</code>.</p></td>
<td><p>Este valor é <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
</tbody>
</table>


Observe que o Exchange 2013 é compatível com valores antigos do **DeliveryType** para compatibilidade com versões anteriores do Exchange. Esses valores estão disponíveis no Visualizador de Fila e no Shell, mas não são usados pelo Exchange 2013. Esses valores antigos de **DeliveryType** são:

  - **MapiDelivery**   A fila armazena mensagens para um servidor de Transporte de Hub do Exchange 2007 ou do Exchange 2010 para uma caixa de correio em um servidor de Caixa de Correio do Exchange 2007 ou do Exchange 2010 no site local do Active Directory.

  - **SmtpRelayWithinAdSite**   A fila armazena mensagens para entrega por um servidor de Transporte de Hub do Exchange 2007 ou do Exchange 2010 a outro servidor de Transporte de hub no mesmo site do Active Directory. O servidor de Transporte de Hub de destino pode ser o servidor de origem para um conector ou um servidor de expansão de grupo.

  - **SmtpRelaytoTiRg**   A fila armazena mensagens para entrega por um servidor de Transporte de hub do Exchange 2007 ou do Exchange 2010 para um grupo de direcionamento do Exchange Server 2003. O servidor de destino pode ser o servidor de origem para um conector, um servidor de expansão de grupo de distribuição ou um servidor bridgehead do Exchange 2003.

Voltar ao início

## IncomingRate, OutgoingRate e Velocity

O Exchange 2013 mede a taxa de mensagens que entram e saem de uma fila e armazena esses valores nas propriedades da fila. Você pode usar essas taxas como um indicador da integridade do servidor de transporte e da fila. As propriedades são:

  - **IncomingRate**   Esta propriedade é a taxa em que as mensagens entram na fila.
    
    Este valor é calculado a partir da quantidade de mensagens que entram na fila a cada 5 segundos em média durante os últimos 60 segundos. A fórmula pode ser expressa como `(i1+i2+i3+i4+i5+i6)/6`, em que i*n* é igual à quantidade de mensagens em 5 segundos.

  - **OutgoingRate**   Esta propriedade é a taxa em que as mensagens saem da fila.
    
    Este valor é calculado a partir da quantidade de mensagens que saem da fila a cada 5 segundos em média durante os últimos 60 segundos. A fórmula pode ser expressa como `(o1+o2+o3+o4+o5+o6)/6`, em que o*n* é igual à quantidade de mensagens que saem a cada 5 segundos.

  - **Velocity**   Esta propriedade é a taxa de drenagem da fila, e é calculada subtraindo-se o valor de **IncomingRate** do valor de **OutgoingRate**.
    
    Se o valor de **Velocity** for maior que 0, as mensagens estão deixando a fila com mais rapidez do que estão entrando.
    
    Se o valor de **Velocity** for igual a 0, as mensagens estão saindo da fila com mais rapidez do que estão entrando. Este também é o valor que você vê quando a fila está inativa.
    
    Se o valor de **Velocity** for menor que 0, as mensagens estão entrando na fila com mais rapidez do que estão saindo.

Basicamente, um valor positivo de **Velocity** indica que a integridade da fila está efetivamente drenada, e um valor negativo de **Velocity** indica uma fila que não está. Entretanto, você também precisa considerar os valores das propriedades **IncomingRate**, **OutgoingRate** e **MessageCount**, além da magnitude do valor **Velocity** para a fila. Por exemplo, um valor negativo grande de **Velocity**, um valor grande de **MessageCount**, um valor pequeno de **OutgoingRate** e um valor grande de **IncomingRate** em uma fila são indicadores precisos de que a fila não está drenando adequadamente. Entretanto, uma fila com um valor negativo de **Velocity** que está muito perto de zero, além de valores muito pequenos de **IncomingRate**, **OutgoingRate** e **MessageCount** não indica um problema com a fila.

Voltar ao início

## Status da fila

O status atual de uma fila é armazenado na propriedade **Status** da fila. Uma fila pode ter um dos seguintes valores de status:

  - **Ativo**   A fila está ativamente transmitindo mensagens.

  - **Conectando**   A fila está em processo de conexão com o próximo salto.

  - **Pronto**   A fila recentemente transmitiu mensagens, mas agora está vazia.

  - **Repetir**   A última tentativa de conexão automática ou manual falhou, e a fila está aguardando para repetir a conexão.

  - **Suspenso**   A fila foi suspensa manualmente por um administrador para evitar a entrega das mensagens. As novas mensagens podem entrar na fila, e as mensagens que estão sendo transmitidas para o próximo salto terão a entrega concluída e sairão da fila. Caso contrário, as mensagens não sairão da fila até que esta seja manualmente resumida por um administrador. Observe que a suspensão de uma fila não altera o status das mensagens individuais na fila.
    
    Você pode suspender uma fila que tenha um status Ativo ou Repetir. Você também pode suspender a fila Inacessível e a fila de Envio.
    
    Se você suspender a fila Inacessível, as mensagens não serão reenviadas automaticamente para o categorizador quando atualizações da configuração forem detectadas. Para reenviar automaticamente essas mensagens, você precisa resumir manualmente a fila Inacessíveis. Se você suspender a fila de Envio, as mensagens só serão escolhidas pelo categorizador depois que a fila continuar.

Voltar ao início

## Outras propriedades de fila

Há outras propriedades de fila que são auto-explicativas. Use a maioria dessas propriedades de fila como opções de filtragem. Com a especificação de critérios de filtro, é possível localizar filas com rapidez e executar ações sobre elas. Para obter uma descrição completa das propriedades de fila que podem ser usadas como filtros, consulte [Filtros de fila](queue-filters-exchange-2013-help.md).

Uma propriedade de fila importante que deve ser mencionada aqui é a **MessageCount**, que mostra quantas mensagens estão em uma fila. Esta propriedade é um indicador importante da integridade da fila. Por exemplo, uma fila de entrega que contém uma quantidade grande de mensagens, que continua a crescer e nunca diminui pode indicar um problema de pipeline de direcionamento ou de transporte que requer sua atenção.

Voltar ao início

## Propriedades da mensagem

Uma mensagem em uma fila tem muitas propriedades. Muitas dessas refletem as informações usadas para criar a mensagem. Alguns desses status de mensagens e algumas propriedades de informações são altamente influenciadas pelas propriedades correspondentes na fila. Entretanto, uma mensagem individual pode ter um valor diferente do que a propriedade correspondente na fila. Outras propriedades contêm indicadores de status, tempo ou outros indicadores que são atualizados com frequência.

Voltar ao início

## Status de mensagens

O status atual de uma mensagem é armazenado na propriedade **Status** da mensagem. Uma mensagem pode ter um dos seguintes valores de status:

  - **Ativa   **Se estiver em uma fila de entrega, a mensagem será entregue ao seu destino. Se a mensagem estiver na fila de Envio, está sendo processada pelo categorizador.

  - **Bloqueado**   Este valor está reservado para uso interno da Microsoft e não é usado nas organizações locais do Exchange.

  - **PendingRemove**   A mensagem foi excluída pelo administrador, mas já está sendo transmitida para o próximo salto. A mensagem será excluída se a entrega terminar em um erro que faça com que a mensagem entre novamente na fila. Caso contrário, a entrega continuará.

  - **PendingSuspend**   A mensagem foi suspensa pelo administrador, mas já está sendo transmitida para o próximo salto. A mensagem será suspensa caso a entrega termine em um erro que faça com que a mensagem entre novamente na fila. Caso contrário, a entrega continuará.

  - **Pronto**   A mensagem está aguardando na fila e está pronta para ser processada.

  - **Repetir**   A última tentativa de conexão automática ou manual para a fila em que esta mensagem está falhou. A mensagem está aguardando pela próxima repetição de conexão de fila automática.

  - **Suspenso**   A mensagem foi manualmente suspensa pelo administrador. Todas as mensagens contidas na fila de mensagens suspeitas estão permanentemente no estado suspenso.

Voltar ao início

## Outras propriedades de mensagens

Há outras propriedades de mensagens que são auto-explicativas. Você pode usar a maioria das propriedades de mensagens como opções de filtragem. Ao especificar critérios de filtro, é possível localizar mensagens rapidamente e executar ações sobre elas. Para obter uma descrição completa das propriedades de mensagens que podem ser usadas como filtros, consulte [Filtros de mensagens](message-filters-exchange-2013-help.md).

Voltar ao início

## Gerenciar filas e mensagens nas filas

O Visualizador de Filas e quase todos os cmdlets de gerenciamento de filas e mensagens estão restritos a um único servidor do Exchange. Você pode visualizar ou operar filas ou mensagens individuais, ou várias filas e mensagens, mas apenas em um servidor específico.

O Exchange 2013 contém o cmdlet **Get-QueueDigest** que proporciona uma visualização agregada de alto nível do estado das filas em todos os servidores dentro de um escopo específico; por exemplo, um DAG, um site do Active Directory, uma lista de servidores ou toda a floresta do Active Directory. Observe que as filas em um servidor de Transporte de Borda inscrito na rede de perímetro não são incluídas nos resultados. Além disso, **Get-QueueDigest** está disponível em um servidor de Transporte de Borda, mas os resultados são restritos a filas no servidor de Transporte de Borda.


> [!NOTE]
> Por padrão, o cmdlet <STRONG>Get-QueueDigest</STRONG> exibe as filas de entrega que contenham dez ou mais mensagens e os resultados são de um a dois minutos atrás. Para instruções sobre como alterar estes valores padrões, consulte <A href="configure-get-queuedigest-exchange-2013-help.md">Configurar Get-QueueDigest</A>.



A tabela a seguir descreve as tarefas de gerenciamento que você pode realizar nas filas ou nas mensagens das filas.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tarefa</th>
<th>Descrição</th>
<th>Ferramenta a ser utilizada</th>
<th>Instruções</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Visualizar e filtrar filas em um servidor</p></td>
<td><p>Esta ação exibe uma ou mais filas em um servidor de transporte. Você pode usar os resultados para realizar tarefas nas filas.</p></td>
<td><p>O Visualizador de Filas ou o cmdlet <strong>Get-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gerenciar filas</a></p></td>
</tr>
<tr class="even">
<td><p>Visualizar e filtrar filas em servidores específicos em DAGs específicos, sites específicos do Active Directory ou em toda a floresta do Active Directory.</p></td>
<td><p>Esta ação exibe um resumo das filas em um escopo definido (servidores, DAGs, sites do Active Directory ou em toda a floresta do Active Directory).</p></td>
<td><p>Apenas o cmdlet <strong>Get-QueueDigest</strong></p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gerenciar filas</a></p></td>
</tr>
<tr class="odd">
<td><p>Filas suspensas</p></td>
<td><p>Esta ação impede temporariamente a entrega de mensagens que estão atualmente na fila. A fila continua a aceitar novas mensagens, mas nenhuma mensagem deixa a fila.</p></td>
<td><p>O Visualizador de Fila ou o cmdlet <strong>Suspend-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gerenciar filas</a></p></td>
</tr>
<tr class="even">
<td><p>Resumir filas</p></td>
<td><p>Esta ação reverte o efeito da ação de suspensão da fila e permite a retomada da entrega das mensagens da fila.</p></td>
<td><p>O Visualizador de Fila ou o cmdlet <strong>Resume-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gerenciar filas</a></p></td>
</tr>
<tr class="odd">
<td><p>Repetir filas</p></td>
<td><p>Esta ação imediatamente tenta conectar ao próximo salto. Sem intervenção manual, quando a conexão com o próximo salto falha, há um número específico de novas tentativas de conexão após determinado intervalo de tempo entre cada tentativa.</p>
<p>Independente de a tentativa de conexão ser manual ou automática, qualquer tentativa redefine o tempo da próxima tentativa. Para obter mais informações, consulte <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">Intervalos de repetição, reenvio e expiração de mensagem</a>.</p></td>
<td><p>O Visualizador de Fila ou o cmdlet <strong>Retry-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gerenciar filas</a></p></td>
</tr>
<tr class="even">
<td><p>Reenviar as mensagens nas filas</p></td>
<td><p>Esta ação faz com que as mensagens na fila sejam reenviadas à fila de Envio e voltem para o processo de categorização.</p></td>
<td><p><strong>Retry-Queue</strong> com o parâmetro <em>Resubmit</em></p>
<p>Observe que você pode usar o Visualizador de Fila para reenviar mensagens, mas apenas da fila de mensagens suspeitas. Para reenviar uma mensagem suspeita, retome a mensagem no Visualizador de Fila ou usando o cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gerenciar filas</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspender mensagens nas filas</p></td>
<td><p>Esta ação impede temporariamente a entrega de uma mensagem. Você pode usar a ação Suspender mensagem para evitar a entrega de uma mensagem para todos os destinatários de uma fila específica ou para todos os destinatários de todas as filas.</p></td>
<td><p>O Visualizador de Fila ou o cmdlet <strong>Suspend-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gerenciar mensagens em filas</a></p></td>
</tr>
<tr class="even">
<td><p>Retomar mensagens nas filas</p></td>
<td><p>Esta ação reverte o efeito da ação de suspensão de mensagens e permite a retomada da entrega das mensagens na fila. Você pode usar a ação continuar mensagem para retomar a entrega de uma mensagem para todos os destinatários de uma fila específica ou para todos os destinatários de todas as filas.</p></td>
<td><p>O Visualizador de Fila ou o cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gerenciar mensagens em filas</a></p></td>
</tr>
<tr class="odd">
<td><p>Remover mensagens das filas</p></td>
<td><p>Esta ação impede permanentemente a entrega de uma mensagem. Você pode usar a ação remover mensagem para evitar a entrega de uma mensagem para todos os destinatários de uma fila específica ou para todos os destinatários de todas as filas. Também é possível configurar a ação Remover mensagem para enviar uma notificação de falha na entrega ao remetente quando a mensagem for removida.</p></td>
<td><p>O Visualizador de Fila ou o cmdlet <strong>Remove-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gerenciar mensagens em filas</a></p></td>
</tr>
<tr class="even">
<td><p>Exportar mensagens de filas</p></td>
<td><p>Esta ação copia uma mensagem para o caminho de arquivo que você especificar. As mensagens não são excluídas da fila, mas uma cópia da mensagem é salva em um arquivo. Isso permite que os administradores ou funcionários de uma organização examinem as mensagens posteriormente. Antes de exportar uma mensagem, é preciso suspendê-la na fila para que a entrega normal não continue durante o processo de exportação.</p></td>
<td><p>Apenas o cmdlet <strong>Export-Message</strong>.</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">Exportar mensagens de filas</a></p></td>
</tr>
</tbody>
</table>


Voltar ao início

