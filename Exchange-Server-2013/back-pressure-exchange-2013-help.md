---
title: 'Pressão de retorno: Exchange 2013 Help'
TOCTitle: Pressão de retorno
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52058784
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pressão de retorno

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Pressão de retorno é um recurso de monitoramento dos recursos do sistema do serviço de Transporte do Microsoft Exchange que existe nos servidores de Caixa de Correio e de Transporte de Borda no Exchange 2013.

O Exchange pode detectar quando recursos vitais, como espaço em disco rígido disponível e memória estão sob pressão e pode agir para tentar evitar a indisponibilidade do serviço. A pressão de retorno evita que os recursos do sistema fiquem totalmente sobrecarregados, e o servidor do Exchange tente processar as mensagens existentes antes de aceitar novas mensagens. Quando a utilização dos recursos do sistema volta para um nível normal, o servidor do Exchange retoma gradativamente a operação normal e passa a aceitar novas mensagens outra vez.

No Exchange 2013, quando o serviço de Transporte em um servidor de Caixa de Correio ou em um servidor de Transporte de Borda está sob pressão de recursos, as conexões de entrada são aceitas, mas as mensagens de entrada nessas conexões são aceitas a uma taxa mais lenta ou são rejeitadas. Quando um host SMTP tenta se conectar a um servidor do Exchange que está sob pressão de recursos, a conexão tem êxito. No entanto, quando o host emite o comando **MAIL FROM** para enviar uma mensagem, dependendo do recurso que está sob pressão, o serviço de Transporte atrasa a confirmação do comando **MAIL FROM** ou rejeita a conexão.

**Sumário**

Resources monitored

Actions taken by Exchange Transport when under resource pressure

Back pressure configuration options in the EdgeTransport.exe.config file

Back pressure logging information

## Recursos monitorados

Os seguintes recursos do sistema são monitorados como parte do recurso de pressão de retorno:

  - Espaço livre no disco rígido que armazena o banco de dados da fila de mensagens.

  - Espaço livre no disco rígido que armazena os logs de transações do banco de dados da fila de mensagens.

  - O número de transações não confirmadas do banco de dados da fila de mensagens que existem na memória.

  - A memória usada pelo processo EdgeTransport.exe.

  - A memória usada por todos os outros processos.

  - O número de mensagens na fila de envio.

Para cada recurso de sistema monitorado em um servidor de Caixa de Correio ou de Transporte de Borda ou em um servidor de Transporte de Borda, os três níveis de utilização de recursos a seguir são aplicados:

  - **Normal**   O recurso não está com uso excessivo. O servidor aceita novas conexões e mensagens.

  - **Médio**   O recurso está com uso um pouco acima do normal. A pressão de retorno é aplicada ao servidor de forma limitada. Mensagens de remetentes no domínio autoritativo podem fluir. No entanto, dependendo do recurso específico sob pressão, o servidor usa tarpitting para atrasar as respostas do servidor ou rejeita comandos **MAIL FROM** de entrada de outras origens.

  - **Alto**   O recurso está com uso muito acima do normal. A pressão de retorno total é aplicada. Todo o fluxo de mensagens é interrompido e o servidor rejeita todos os novos comandos **MAIL FROM** de entrada.

As seções a seguir explicam como o Exchange trata a situação quando um recurso específico está sob pressão.

## Espaço livre em disco rígido para o banco de dados de fila de mensagens

Por padrão, o banco de dados de fila de mensagem está armazenado em %ExchangeInstallPath%TransportRoles\\data\\Queue. O Exchange monitora a utilização do espaço em disco rígido para este local. O alto nível de utilização do espaço no disco rígido é calculado com a seguinte fórmula:

100 \* (*tamanho do disco rígido* - *constante fixa*) / *tamanho do disco rígido*

O valor da *constante fixa* é 500 megabytes (MB).

Os resultados dessa fórmula são expressos como uma porcentagem do espaço total do disco rígido que está sendo usado. Os resultados da fórmula são sempre arredondados para o número inteiro menor mais próximo. Por padrão, o nível médio de utilização do disco rígido é 2 por cento inferior ao nível alto. Por padrão, o nível normal de utilização do disco rígido é 4 por cento inferior ao nível alto.

Voltar ao início

## Espaço livre em disco rígido para os logs de transação do banco de dados de fila de mensagens

Por padrão, os logs de transação do banco de dados de fila de mensagem estão armazenados em %ExchangeInstallPath%TransportRoles\\data\\Queue. O Exchange monitora a utilização do espaço em disco rígido para este local. O arquivo de configuração de aplicativo %ExchangeInstallPath%Bin\\EdgeTransport.exe.config contém uma chave *DatabaseCheckPointDepthMax* com o valor padrão de 384 MB. Essa chave controla o tamanho total permitido de todos os logs de transações não confirmadas existentes no disco rígido. Essa chave é usada na fórmula que calcula a utilização do disco rígido.


> [!TIP]
> O valor da chave <EM>DatabaseCheckPointDepthMax</EM> se aplica a todos os bancos de dados ESE (Mecanismo de Armazenamento Extensível) relacionados a transporte existentes no servidor de Caixa de Correio ou de Transporte de Borda. Isso inclui o banco de dados de fila de mensagens e o banco de dados do filtro IP.



Por padrão, o alto nível de utilização do disco rígido é calculado com a seguinte fórmula:

100 \* (*tamanho do disco rígido* - Min(5 GB, 3\**DatabaseCheckPointDepthMax*)) / *tamanho do disco rígido*

Os resultados da fórmula são sempre arredondados para o número inteiro menor mais próximo. Por padrão, o nível médio de utilização do disco rígido é 2 por cento inferior ao nível alto. O nível normal de utilização do disco rígido é 4 por cento inferior ao nível alto.

Voltar ao início

## Número de transações do banco de dados de fila de mensagens não confirmadas em memória

Uma lista das alterações feitas no banco de dados de fila de mensagens é mantida na memória, até que essas alterações possam ser confirmadas no log de transações. Em seguida, essa lista é confirmada no próprio banco de dados de fila de mensagens. Essas transações pendentes do banco de dados da fila de mensagens que são mantidas na memória são conhecidas como *partições de memória de versão*. O número de partições de memória de versão pode aumentar até níveis inaceitavelmente altos, devido a um volume inesperadamente alto de mensagens de entrada, ataques de spam, problemas com a integridade do banco de dados de fila de mensagens, ou desempenho do disco rígido.

Quando o Exchange começa a receber mensagens, essas mensagens são agrupadas em lotes e, em seguida, preparadas como partições de memória de versão. Se uma mensagem de entrada tiver um anexo grande, pode ser separada em vários lotes. Esses lotes que estão sendo processados são conhecidos como *pontos de lote*. O número de pontos de lote de saída pode exceder os limites definidos, especialmente quando existe um volume inesperadamente alto de mensagens de entrada, com anexos grandes.

Quando partições de memória de versão ou pontos de lote estão sob pressão, o servidor do Exchange começa a limitar as conexões de entrada, atrasando a confirmação de mensagens de entrada. O Exchange reduzirá o fluxo mensagens de entrada por meio de tarpitting, o que introduz um atraso nos comandos **MAIL FROM**. Se a condição de pressão de recursos continuar, o Exchange gradualmente aumenta o atraso de tarpitting. Quando a utilização do recurso volta ao normal, o Exchange gradualmente começa a reduzir o atraso de confirmação e volta à operação normal. Por padrão, o Exchange começa a atrasar a confirmação de mensagens em 10 segundos quando está sob pressão de recursos. Se os recursos permanecerem sob pressão, o atraso é aumentado em 5 segundos de forma incremental, até 55 segundos.

O Exchange mantém um histórico da utilização dos recursos de partições de memória de versão e pontos de lote. Se a utilização do recurso não voltar ao nível normal por um número específico de intervalos de sondagem, conhecido como profundidade do histórico, o Exchange interromperá o atraso de tarpitting e começará a rejeitar mensagens de entrada, até que a utilização do recurso volte ao normal. Por padrão, as profundidades de histórico para partições de memória de versão e pontos de lote estão nos intervalos de sondagem 10 e 300, respectivamente.

Voltar ao início

## Memória usada pelo processo EdgeTransport.exe

Por padrão, o alto nível de utilização da memória pelo processo EdgeTransport.exe é calculado com a seguinte fórmula:

75 por cento da memória física total ou 1 terabyte, o que for menor

Esse cálculo não inclui a memória virtual disponível no disco rígido no arquivo de paginação, ou a memória usada por outros processos. Os resultados dessa fórmula são expressos como uma porcentagem da memória total usada pelo processo EdgeTransport.exe. Os resultados da fórmula são sempre arredondados para o número inteiro menor mais próximo.

Por padrão, o nível médio de utilização da memória pelo arquivo EdgeTransport.exe é calculado como 73 por cento da memória física total ou 2 por cento a menos do que o valor do nível alto, o que for menor. Por padrão, o nível normal de utilização da memória pelo arquivo EdgeTransport.exe é calculado como 71 por cento da memória física total ou 4 por cento a menos do que o valor do nível alto, o que for menor.

Se a utilização de memória do processo EdgeTransport.exe for maior do que o nível normal especificado, a *coleta de lixo* será forçada. Coleta de lixo é um processo que verifica se há objetos não utilizados existentes na memória e recupera a memória usada por esses objetos.

O Exchange mantém um histórico da utilização da memória do processo EdgeTransport.exe. Se a utilização não voltar ao nível normal por um número específico de intervalos de sondagem, conhecido como profundidade do histórico, o Exchange começará a rejeitar mensagens de entrada, até que a utilização do recurso volte ao normal. Por padrão, a profundidade do histórico para a utilização de memória do EdgeTransport.exe é de 30 intervalos de sondagem.

Voltar ao início

## Memória usada por todos os processos

Por padrão, o alto nível de utilização da memória por todos os processos é 94 por cento da memória física total. Esse valor não inclui a memória virtual disponível no disco rígido no arquivo de paginação.

Quando o nível de utilização de memória especificado é atingido, ocorre a *filtragem de mensagens*. Filtragem de mensagens é a ação de remover elementos desnecessários das mensagens em fila que estão no cache da memória. Mensagens completas ficam em cache na memória para melhoria do desempenho. A remoção do conteúdo MIME das mensagens em fila da memória reduz a memória usada à custa de latência maior porque as mensagens são lidas diretamente do banco de dados de fila de mensagens. Por padrão, a filtragem de mensagens está habilitada.

Voltar ao início

## Número de mensagens na fila de Envio

A fila de Envio está associada ao serviço de Transporte nos servidores de Caixa de Correio do Exchange 2013 e nos servidores de Transporte de Borda. O categorizador processa cada mensagem na fila de Envio. Essa categorização resulta na mensagem em uma fila de entrega. Para obter mais informações, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md) e [Filas](queues-exchange-2013-help.md). Uma grande quantidade de mensagens na fila de Envio indica que o categorizador está com dificuldades para processar as mensagens.

Quando a fila de Envio está sob pressão, o servidor do Exchange começa a limitar as conexões de entrada, atrasando a confirmação de mensagens de entrada. O Exchange reduzirá o fluxo mensagens de entrada por meio de tarpitting, o que introduz um atraso nos comandos **MAIL FROM**. Se a condição de pressão da fila de Envio continuar, o Exchange gradualmente aumenta o atraso de tarpitting. Quando a utilização da fila de Envio volta ao normal, o Exchange gradualmente começa a reduzir o atraso de confirmação e volta à operação normal. Por padrão, o Exchange começa a atrasar a confirmação de mensagens em 10 segundos quando está sob pressão da fila de Envio. Se a fila de Envio permanecer sob pressão, o atraso aumenta em 5 segundos de forma incremental, até 55 segundos.

O Exchange mantém um histórico da utilização da fila de Envio. Se a utilização da fila de Envio não voltar ao nível normal por um número específico de intervalos de sondagem, conhecido como profundidade do histórico, o Exchange interromperá o atraso de tarpitting e começará a rejeitar mensagens de entrada, até que a utilização da fila de Envio volte ao normal. Por padrão, a profundidade do histórico da fila de Envio é de 300 intervalos de sondagem.

## Providências tomadas pelo Transporte do Exchange quando está sob pressão de recursos

A tabela a seguir resume as medidas tomadas pelo transporte do Exchange quando um recurso específico está sob pressão.

### Medidas de pressão de retorno tomadas pelos servidores de Caixa de Correio e Transporte de Borda em resposta à pressão de recursos

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso sob pressão</th>
<th>Nível de utilização</th>
<th>Medidas tomadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Espaço em disco rígido para o banco de dados de fila de mensagens</p></td>
<td><p>Médio</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Espaço em disco rígido para o banco de dados de fila de mensagens</p></td>
<td><p>Alta</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envio de Transporte de Caixa de Correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Espaço em disco rígido para os logs de transações do banco de dados de fila de mensagens</p></td>
<td><p>Médio</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Espaço em disco rígido para os logs de transações do banco de dados de fila de mensagens</p></td>
<td><p>Alta</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envio de Transporte de Caixa de Correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Partições de memória de versão</p></td>
<td><p>Médio</p></td>
<td><p>Introduzir ou incrementar o atraso de tarpitting em mensagens de entrada. Se o nível normal não for atingido para a profundidade de histórico da partição de memória de versão inteira, execute as seguintes ações:</p>
<ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Partições de memória de versão</p></td>
<td><p>Alta</p></td>
<td><p>Introduzir ou incrementar o atraso de tarpitting em mensagens de entrada. Se o nível normal não for atingido para a profundidade de histórico da partição de memória de versão inteira, execute as seguintes ações:</p>
<ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envio de Transporte de Caixa de Correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Ponto de lote</p></td>
<td><p>Médio</p></td>
<td><p>Introduzir ou incrementar o atraso de tarpitting em mensagens de entrada. Se o nível normal não for atingido para a profundidade de histórico do ponto de lote inteiro, execute as seguintes ações:</p>
<ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Ponto de lote</p></td>
<td><p>Alta</p></td>
<td><p>Introduzir ou incrementar o atraso de tarpitting em mensagens de entrada. Se o nível normal não for atingido para a profundidade de histórico do ponto de lote inteiro, execute as seguintes ações:</p>
<ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envio de Transporte de Caixa de Correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memória usada pelo processo EdgeTransport.exe</p></td>
<td><p>Médio</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
<li><p>Forçar a coleta de lixo</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memória usada pelo processo EdgeTransport.exe</p></td>
<td><p>Alta</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envio de Transporte de Caixa de Correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memória usada por todos os processos</p></td>
<td><p>Médio</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
<li><p>Forçar a coleta de lixo</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memória usada por todos os processos</p></td>
<td><p>Alta</p></td>
<td><ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envio de Transporte de Caixa de Correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
<li><p>Liberar cache DNS avançado da memória</p></li>
<li><p>Iniciar a filtragem de mensagens</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Número de mensagens na fila de Envio</p></td>
<td><p>Médio</p></td>
<td><p>Introduzir ou incrementar o atraso de tarpitting em mensagens de entrada. Se o nível normal não for atingido para a profundidade de histórico de toda a fila de Envio, execute as seguintes ações:</p>
<ul>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
<li><p>Forçar a coleta de lixo</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Número de mensagens na fila de Envio</p></td>
<td><p>Alta</p></td>
<td><p>Introduzir ou incrementar o atraso de tarpitting em mensagens de entrada. Se o nível normal não for atingido para a profundidade de histórico de toda a fila de Envio, execute as seguintes ações:</p>
<ul>
<li><p>Rejeitar mensagens de entrada de outros servidores Exchange</p></li>
<li><p>Rejeitar envios de mensagem de bancos de dados de caixa de correio pelo serviço Envios de transporte de caixa de correio em servidores de Caixa de Correio</p></li>
<li><p>Rejeitar mensagens de entrada de servidores que não são do Exchange</p></li>
<li><p>Rejeitar envios de mensagem de diretórios de Retirada e Repetição</p></li>
<li><p>Liberar cache DNS avançado da memória</p></li>
<li><p>Iniciar a filtragem de mensagens</p></li>
</ul></td>
</tr>
</tbody>
</table>


Voltar ao início

## Opções de configuração de pressão de retorno no arquivo EdgeTransport.exe.config

Todas as opções de configuração para pressão de retorno estão disponíveis no arquivo XML de configuração de aplicativo %ExchangeInstallPath%Bin\\EdgeTransport.exe.config.


> [!WARNING]
> Essas configurações são listadas apenas como referência. É altamente desaconselhável fazer qualquer modificação nas configurações de pressão de retorno do arquivo EdgeTransport.exe.config. Modificações nas configurações da pressão de retorno podem resultar em desempenho inadequado ou perda de dados. É recomendável que você investigue e corrija a causa raiz de quaisquer eventos de pressão de retorno que possam surgir.



### Opções de configuração da pressão de retorno

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome da chave</th>
<th>Valor padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 segundos)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Esse valor indica que a fórmula padrão será usada.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. Esse valor indica que o valor real é 2 por cento menor do que o valor do parâmetro <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. Esse valor indica que o valor real é 2 por cento menor do que o valor do parâmetro <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Esse valor indica que a fórmula padrão será usada.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. Esse valor indica que o valor real é 2 por cento menor do que o valor do parâmetro <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. Esse valor indica que o valor real é 2 por cento menor do que o valor do parâmetro <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. Esse valor indica que o cálculo padrão será usado.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. Esse valor indica que o valor real é 2 por cento menor do que o valor do parâmetro <em>PercentagePrivateBytesUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. Esse valor indica que o valor real é 2 por cento menor do que o valor do parâmetro <em>PercentagePrivateBytesUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0,1 segundos)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 minutos)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 segundos)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 segundos)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 segundos)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Informações do log da pressão de retorno

A lista a seguir descreve as entradas do log de eventos geradas por eventos específicos da pressão de retorno no Exchange:

  - **Entrada do log de eventos para um aumento em qualquer nível de utilização de recursos**
    
    Tipo de Evento: Erro
    
    Origem do Evento: MSExchangeTransport
    
    Categoria do Evento: Gerenciador de Recursos
    
    ID do Evento: 15004
    
    Descrição: A pressão do recurso aumentou de *Nível de Utilização Anterior* para *Nível de Utilização Atual*.

  - **Entrada do log de eventos para uma diminuição em qualquer nível de utilização de recursos**
    
    Tipo de Evento: Informações
    
    Origem do Evento: MSExchangeTransport
    
    Categoria do Evento: Gerenciador de Recursos
    
    ID do Evento: 15005
    
    Descrição: A pressão do recurso diminuiu de *Nível de Utilização Anterior* para *Nível de Utilização Atual*.

  - **Entrada do log de eventos para espaço em disco disponível extremamente baixo**
    
    Tipo de Evento: Erro
    
    Origem do Evento: MSExchangeTransport
    
    Categoria do Evento: Gerenciador de Recursos
    
    ID do Evento: 15006
    
    Descrição: O serviço de Transporte do Microsoft Exchange está rejeitando mensagens porque o espaço em disco disponível está abaixo do limite configurado. Uma ação administrativa pode ser necessária para liberar espaço em disco, para que o serviço continue suas operações.

  - **Entrada do log de eventos para memória disponível extremamente baixa**
    
    Tipo de Evento: Erro
    
    Origem do Evento: MSExchangeTransport
    
    Categoria do Evento: Gerenciador de Recursos
    
    ID do Evento: 15007
    
    Descrição: O serviço de Transporte do Microsoft Exchange está rejeitando envios de mensagens porque o serviço continua a consumir mais memória do que o limite configurado. Por este motivo, talvez seja necessário reiniciar o serviço para que continue a operação normal.

Voltar ao início

