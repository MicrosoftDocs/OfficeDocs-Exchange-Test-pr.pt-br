---
title: 'Limitação de mensagem: Exchange 2013 Help'
TOCTitle: Limitação de mensagem
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 50487063
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Limitação de mensagem

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

*Limitação de mensagem* refere-se a um grupo de limites definidos no número de conexões que podem ser processados por um computador do Microsoft Exchange Server 2013 e mensagens. Esses limites impedir o acidental ou intencional esgotamento de recursos do sistema no servidor Exchange.

**Sumário**

Escopo de limitação de mensagem

Custo da mensagem e limitação de fluxo de email

Limitação nos servidores de mensagem

Limitação nos conectores de envio de mensagem

Limitação nos conectores de recebimento de mensagem

Políticas de limitação de mensagem

## Escopo de limitação de mensagem

Limitação de mensagem envolve a uma variedade de limites de taxas, taxas de conexão de SMTP e valores de tempo limite de sessão SMTP de processamento de mensagens. Esses limites funcionam juntos para proteger um servidor Exchange seja sobrecarregado pela aceitação e a entrega de mensagens. Embora um registro de posterior grande de mensagens e conexões pode ser aguardando processamento, os limites de limitação de mensagem permitem que o servidor do Exchange processar as mensagens e conexões de forma ordenada.

Além da mensagem de limitação, você também pode colocar limites de tamanho nos componentes individuais de mensagens, como o número de destinatários, o tamanho do cabeçalho da mensagem ou o tamanho dos anexos individuais. Para obter mais informações sobre os limites de tamanho de mensagem, consulte [Limites de tamanhos de mensagens](message-size-limits-exchange-2013-help.md).

Outro recurso que ajuda a evitar sobrecarregar os recursos do sistema de um servidor de transporte do Exchange é *pressão de retorno*. Pressão de retorno é um recurso no serviço de transporte nos servidores de caixa de correio e nos servidores de transporte de borda de monitoramento de recurso do sistema. Quando um recurso de sistema monitorado, como a utilização do disco rígido ou a utilização de memória, excede o limite especificado, o servidor reduz a taxa em que ele aceita mensagens e novas conexões e se concentra em fornecer mensagens existentes. Quando a utilização dos recursos do sistema monitorado retorna aos níveis normais, o servidor lentamente aumenta a taxa em que ele aceita novas conexões e, em seguida, estabelece um nível normal.

Voltar ao início

## Custo da mensagem e limitação de fluxo de email

Para fornecer mais consistente taxa de transferência de mensagem e a latência de entrega de mensagem previsível, Exchange 2013 estabelece um custo acumulado para mensagens. Essa qualidade do recurso de serviço (QoS) foi adicionada ao Microsoft Exchange Server 2010 SP1This custo baseia-se nos seguintes critérios:

  - Tamanho da mensagem

  - Número de destinatários

  - Frequência da transmissão

servidores de transporte de Exchange 2013 rastrear o custo médio de entrega de mensagens enviadas por usuários individuais. Usando os custos de mensagem, Exchange 2013 fornece um grupo de configurações que podem controlar o efeito que um usuário ou a conexão tem em uma organização do Exchange. Esse grupo de configurações é conhecido como uma *diretiva de limitação*. Quando um usuário repetidamente envia mensagens dispendiosas, como mensagens com anexos grandes ou que são enviadas para vários destinatários, o Exchange 2013-servidores de transporte baseado em usam uma política de limitação para atribuir uma prioridade mais baixa para mensagens de custo mais alto do usuário enquanto continua a entregar mensagens de menor custo. Esse novo comportamento adiciona um aspecto "de qualidade de serviço" à mensagem funcionalidade no Exchange 2013 de limitação.


> [!TIP]
> Limitação de mensagem não afeta a prioridade da mensagem da perspectiva de um usuário. Mensagens ainda mantêm a prioridade original definida pelo usuário. Por exemplo, mensagens de mantém uma configuração de importante ou urgente e assim por diante.



Para suportar essa funcionalidade, Exchange 2013 usa mecanismos a seguir:

  - **Agente de priorização interno**   Este operador é disparado no evento **OnResolvedMessage** e atribui uma prioridade mais baixa para mensagens do mesmo remetente que têm um alto custo acumulado. Esse custo é medido durante um período de um minuto e afeta a mensagens que têm mais de 500 destinatários ou que são maiores do que 1 megabyte (MB).

  - **Prioridade de cota com base em enfileiramento de mensagens para o tipo de fila MapiDelivery**   Esse mecanismo faz com que o Exchange para entregar mensagens em uma fila de prioridade normal com mais frequência que mensagens em uma fila de baixa prioridade. Por padrão, a proporção de mensagem normal para baixo é de 20:1. No entanto, novas mensagens de uma fila de prioridade mais baixa nunca são entregues antes que novos itens de uma fila de prioridade mais alta. Por exemplo, considere o seguinte cenário:
    
    1.  Mensagens de prioridade normal vinte são entregues. Por padrão, a próxima mensagem entregue é uma mensagem de prioridade mais baixa.
    
    2.  Duas novas mensagens são recebidas pelo servidor de transporte: uma mensagem de uma fila de prioridade mais alta e uma mensagem de uma fila de prioridade mais baixa.
    
    Neste cenário, a mensagem da fila de prioridade mais alta é entregue pela primeira vez. Em seguida, a mensagem da fila de prioridade mais baixa é entregue.

  - **Acelerar as conexões simultâneas com base na integridade do banco de dados de mensagens**   Esse mecanismo monitora a integridade de integridade do banco de dados (MDB) de mensagens do Exchange e restringe conexões simultâneas para servidores de transporte do Exchange com base em um valor de medida de integridade atribuído. O MDB é monitorado pela API do Monitor de integridade do recurso no serviço de transporte no servidor de caixa de correio e recebe um valor de integridade de -1 a 100. Esse valor baseia-se as estatísticas de desempenho de RPC incluídos com cada resposta RPC do processo de Store.exe no serviço de transporte de caixa de correio. A estrutura de integridade do recurso usa o contador de desempenho de taxa de **Solicitações/segundo** e o contador de desempenho da **Latência média de RPC** para calcular um valor de integridade para o banco de dados. Para ajudar a manter uma experiência interativa de usuário consistente, o Exchange reduz o número de conexões simultâneas como o valor de integridade diminui à medida. Os seguintes intervalos de valor de integridade estão disponíveis:
    
      - **-1:**  esse valor indica que o estado de integridade MDB é desconhecido. Esse valor é atribuído quando o banco de dados é iniciado. Neste cenário, o banco de dados é considerado íntegro.
    
      - **0:**  esse valor é atribuído se o banco de dados está em um estado íntegro. Nesse estado, o banco de dados não deve ser contatado.
    
      - **1 a 99:**  esses valores representam um estado de integridade justo. Um valor mais baixo representa um banco de dados menor íntegro.
    
      - **100:**  esse valor representa um banco de dados íntegro.

O serviço de limitação do Microsoft Exchange fornece a estrutura de limitação de fluxo de email. O serviço de limitação do Microsoft Exchange controla as configurações para um usuário específico de limitação de fluxo de emails e armazena as informações de limitação na memória. Configurações de limitação de fluxo de email são também conhecido como um *orçamento*. Reiniciar o serviço de limitação do Microsoft Exchange também redefine a limitação orçamentos de fluxo de emails.

Você pode usar os cmdlets de política de limitação que estão disponíveis no Exchange 2013 para definir as configurações do orçamento individual de uma política de limitação. Um orçamento é a quantidade de acesso que um usuário ou aplicativo disponham de uma configuração específica. Um orçamento representa quantas conexões que um usuário pode ter ou quanto atividade de um usuário pode ser permitida para cada período de um minuto. Por exemplo, um orçamento pode ser configurado para definir a quantidade de tempo que um usuário pode gastar usando um recurso específico no Exchange, como ActiveSync, Outlook Web App ou serviços Web do Exchange. Esse limite é armazenado em uma política de limitação e define o orçamento.

Configurações de tempo para um orçamento são definidas como uma porcentagem de um minuto. Portanto, um limite de 100 por cento representa 60 segundos. Por exemplo, suponha que você deseja especificar as configurações de diretiva de Outlook Web App que limitam a quantidade de tempo durante o qual um usuário pode executar um código de Outlook Web App em um servidor de acesso para cliente e a quantidade de tempo que o usuário pode se comunicar com o servidor de acesso para cliente para 600 milissegundos por um período de um minuto. Para realizar isso, você precisará definir o valor para % 1 de um minuto (600 milissegundos) para ambos dos parâmetros a seguir:

  - **OWAPercentTimeInCAS:**  1

  - **OWAPercentTimeInMailboxRPC:**  1

Um usuário que tem essa diretiva aplicada tem um orçamento de OWAPercentTimeInCAS de 600 milissegundos e de OWAPercentageTimeInMailboxRPC de 600 milissegundos. Neste cenário, quando o usuário está conectado ao Outlook Web App, o usuário pode executar um código de acesso para cliente por até 600 milissegundos. Após o período-milissegundo 600, a conexão é considerada acima do orçamento e o Exchange server não permite nenhuma providência Outlook Web App até um minuto após o limite de orçamento for atingido. Após o período de um minuto, o usuário pode executar o código de acesso do cliente Outlook Web App por outro milissegundos 600.

Voltar ao início

## Limitação nos servidores de mensagem

Você pode definir a mensagem limitação opções nos seguintes locais:

  - No serviço de transporte

  - Em um conector de envio

  - Em um conector de recebimento

Você pode definir todas as a mensagem limitação opções que estão disponíveis no serviço de transporte em servidores de caixa de correio, no serviço de transporte de caixa de correio em servidores de caixa de correio, ou no serviço Front End Transport em servidores de acesso para cliente usando o Shell de gerenciamento do Exchange. Você também pode definir algumas das mesmas opções, definindo as propriedades do servidor de transporte no Centro de administração do Exchange (EAC).

A tabela a seguir mostra a limitação de opções que estão disponíveis nos servidores de transporte de mensagem.

### Limitação opções nos servidores de transporte de mensagem

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>Este parâmetro especifica o número máximo de threads de entrega que o serviço de transporte pode ter aberto ao mesmo tempo de entrega de mensagens para caixas de correio. O intervalo válido de entrada para esse parâmetro é de 1 a 256. Recomendamos que você não modifique o valor padrão, a menos que o suporte e atendimento ao cliente Microsoft recomendará a fazer isso.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>Este parâmetro especifica o número máximo de threads de envio que o serviço de transporte pode ter aberto ao mesmo tempo para enviar mensagens de caixas de correio. O intervalo válido de entrada para esse parâmetro é de 1 a 256.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>Este parâmetro especifica a taxa máxima que conexões têm permissão para ser aberto com o serviço de transporte. Se o número de conexões é tentada com o serviço de transporte ao mesmo tempo, o parâmetro <em>MaxConnectionRatePerMinute</em> limita a taxa de que as conexões são abertas para que os recursos do servidor não estão sobrecarregados.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> ou</p>
<p>Propriedades do servidor de transporte</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>Este parâmetro especifica o número máximo de conexões de saída que podem ser abertos por vez. Se você inserir um valor de <code>unlimited</code>, nenhum limite é imposto no número de conexões de saída. O valor desse parâmetro deve ser maior ou igual ao valor do parâmetro <em>MaxPerDomainOutboundConnections</em> .</p>
<p>Esse valor também pode ser configurado usando o EAC em <strong>servidores</strong> &gt; <strong>servidores</strong> &gt; <strong>Propriedades</strong> &gt; <strong>limites de transporte</strong> &gt; <strong>restrições de conexão de saída</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> ou</p>
<p>Propriedades do servidor de transporte</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>Este parâmetro especifica o número máximo de conexões simultâneas a qualquer domínio único. Se você inserir um valor de <code>unlimited</code>, nenhum limite é imposto no número de conexões de saída por domínio. O valor desse parâmetro deve ser maior ou igual ao valor do parâmetro <em>MaxOutboundConnections</em> .</p>
<p>Esse valor também pode ser configurado usando o EAC em <strong>servidores</strong> &gt; <strong>servidores</strong> &gt; <strong>Propriedades</strong> &gt; <strong>limites de transporte</strong> &gt; <strong>restrições de conexão de saída</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>Este parâmetro especifica o número máximo de mensagens processadas por minuto pelo diretório de retirada e pelo diretório de repetição. Cada diretório de forma independente pode processar arquivos de mensagem com a taxa especificada por esse parâmetro.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Limitação nos conectores de envio de mensagem

A tabela a seguir mostra a limitação de opção que está disponível nos conectores de envio de mensagem. Você precisará usar o Shell de gerenciamento do Exchange para configurar essa opção.

### Limitação de opção disponível nos conectores de envio de mensagem

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 minutos</p></td>
<td><p>Este parâmetro especifica o tempo máximo que uma conexão de SMTP aberto com um servidor de destino de mensagens pode permanecer inativa antes que a conexão seja fechado.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Limitação nos conectores de recebimento de mensagem

A tabela a seguir mostra a mensagem limitação opções que estão disponíveis nos conectores de recebimento configurados no serviço de transporte em um servidor de caixa de correio ou em um servidor de transporte de borda. Você precisará usar o Shell de gerenciamento do Exchange para configurar essas opções.

### Limitação de opções disponíveis nos conectores de recebimento de mensagem

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>5 minutos no serviço de transporte em servidores de caixa de correio</p>
<p>5 minutos no serviço Front End Transport em servidores de acesso para cliente.</p>
<p>1 minuto em servidores de transporte de borda.</p></td>
<td><p>Este parâmetro especifica o tempo máximo que uma conexão de SMTP aberto com um servidor de origem de mensagens pode permanecer inativa antes que a conexão seja fechado. O valor desse parâmetro deve ser menor que o valor especificado pelo parâmetro <em>ConnectionTimeout</em> .</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>10 minutos no serviço de transporte em servidores de caixa de correio</p>
<p>10 minutos no serviço Front End Transport em servidores de acesso para cliente.</p>
<p>5 minutos nos servidores de transporte de borda.</p></td>
<td><p>Este parâmetro especifica o tempo máximo que uma conexão de SMTP com uma fonte de servidor de mensagens pode permanecer aberta, mesmo se o servidor de mensagens de origem está transmitindo dados. O valor desse parâmetro deve ser maior que o valor especificado pelo parâmetro <em>ConnectionInactivityTimeout</em> .</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>Este parâmetro especifica o número máximo de conexões SMTP de entrada que este conector de recebimento permite ao mesmo tempo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>100 por cento no conector de recebimento padrão no serviço de transporte em um servidor de caixa de correio</p>
<p>% 2 nos outros conectores de recebimento no serviço de transporte em servidores de caixa de correio e no serviço Front End Transport em servidores de acesso para cliente.</p></td>
<td><p>Este parâmetro especifica o número máximo de conexões SMTP que permite a um conector de recebimento ao mesmo tempo a partir de um único servidor de mensagens de origem. O valor é expresso como a porcentagem de conexões restantes disponíveis em um conector de recebimento. O número máximo de conexões que são permitidas pelo conector de recebimento é definido pelo parâmetro <em>MaxInboundConnection</em> .</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>unlimited no conector de recebimento padrão no serviço de transporte em um servidor de caixa de correio</p>
<p>20 nos outros conectores de recebimento no serviço de transporte em servidores de caixa de correio e no serviço Front End Transport em servidores de acesso para cliente.</p></td>
<td><p>Este parâmetro especifica o número máximo de conexões SMTP que permite a um conector de recebimento ao mesmo tempo a partir de um único servidor de mensagens de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>Este parâmetro especifica o número máximo de erros de protocolo SMTP que um conector de recebimento permite o fecha do conector de recebimento antes da conexão com o servidor de mensagens de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 segundos</p></td>
<td><p>Este parâmetro especifica o atraso que é usado em <em>tarpitting</em>. Tarpitting é a prática de atrasar artificialmente respostas de SMTP para os padrões de comunicação SMTP específicos que indicam um ataque de coleta de diretório ou a mensagens indesejadas. Um <em>ataque de coleta de diretório</em> é uma tentativa de coletar os endereços de email válido de uma organização específica a ser usado como um destino para email comercial não solicitado.</p>
<p>O atraso especificado pelo parâmetro <em>TarpitInterval</em> só se aplica a conexões anônimas.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Políticas de limitação de mensagem

Em Exchange 2013, cada caixa de correio tem uma configuração de *ThrottlingPolicy* . O valor padrão para essa configuração estiver em branco (`$null`). Você pode usar o parâmetro *ThrottlingPolicy* no cmdlet **Set-Mailbox** para configurar uma política de limitação para uma caixa de correio.

Uma diretiva padrão de limitação existe para fornecer que um padrão definido a configuração do orçamento para usuários que se conectam ao Exchange. Para definir configurações de orçamento personalizada para um ou mais usuários, crie uma nova política de limitação. Em seguida, aplique a política ao grupo ou usuário apropriado.


> [!IMPORTANT]
> Recomendamos que você não modifique a diretiva padrão de limitação.



Você pode definir todas as a mensagem limitação opções que estão disponíveis nos servidores de caixa de correio no Shell de gerenciamento do Exchange. Os cmdlets a seguir estão disponíveis para gerenciar políticas de limitação:

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

Você pode usar os cmdlets **New-ThrottlingPolicy** e **Set-ThrottlingPolicy** para configurar quanto um usuário pode executar contra Exchange sobre uma conexão específica ou o período de tempo de atividade. Essas configurações formam o orçamento de um usuário. Você pode estabelecer políticas de limitação para controlar o acesso aos recursos do Exchange a seguir:

  - Exchange ActiveSync

  - Serviços Web do Exchange

  - Outlook Web App

  - Unificação de Mensagens

  - IMAP4

  - POP3

  - Conexões de cliente do Outlook (conexões MAPI ou RPC)

  - Configurações de fluxo de email

  - Comandos do PowerShell

  - Usos de CPU

Voltar ao início

