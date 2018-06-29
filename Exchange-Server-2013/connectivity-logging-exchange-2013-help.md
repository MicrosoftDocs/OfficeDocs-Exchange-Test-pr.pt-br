---
title: 'Log de conectividade: Exchange 2013 Help'
TOCTitle: Log de conectividade
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 50486570
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log de conectividade

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Log de conectividade registra a atividade de conexão de saída que é usada para transmitir mensagens de um serviço de transporte no Exchange server. A finalidade do log de conectividade não é controlar a transmissão de mensagens de email individuais. Em vez disso, o log de conectividade rastreia a atividade de conexão da fonte para o destino, independentemente de quantas mensagens são transmitidas. Log de conectividade está disponível no serviço Front End Transport nos servidores de acesso para cliente, o serviço de transporte em servidores de caixa de correio e o serviço de transporte de caixa de correio em servidores de caixa de correio. A lista a seguir descreve o tipo de informações registradas no log de conectividade:

  - Origem

  - Destino

  - Informações de resolução de DNS

  - Informações detalhadas sobre falhas de conexão

  - Número de mensagens e bytes transmitidos

Você pode usar os cmdlets **Set-TransportService**, **Set-FrontEndTransportService** e **Set-MailboxTransportService** no Shell de gerenciamento do Exchange para executar todas as tarefas de configuração de log de conectividade. As seguintes opções estão disponíveis para os logs de conectividade:

  - Habilitar ou desabilitar o log de conectividade. O padrão é ativado.

  - Especifique o local dos arquivos de log de conectividade.

  - Especifique um tamanho máximo para os arquivos de log individuais de conectividade. O tamanho padrão é 10 megabytes (MB).

  - Especifique um tamanho máximo para o diretório que contém os arquivos de log de conectividade. O tamanho padrão é 1000 MB.

  - Especifique uma idade máxima para os arquivos de log de conectividade. A idade padrão é 30 dias.

Por padrão, o Exchange usa o log circular para limitar os logs de conectividade com base no tamanho do arquivo e o arquivo para ajudar a controlar o espaço em disco rígido usado pelos arquivos de log de conectividade.

**Sumário**

Estrutura dos arquivos de log de conectividade

Informações gravadas no log de conectividade

## Estrutura dos arquivos de log de conectividade

Por padrão, os arquivos de log de conectividade existem nos seguintes locais:

  - **Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

A convenção de nomenclatura para os arquivos de log de conectividade é CONNECTLOG*yyymmdd-nnnn*. log. Os espaços reservados representam as seguintes informações:

  - O espaço reservado *yyyymmdd* é a data de tempo Universal Coordenado (UTC) que o arquivo de log foi criado. O espaço reservado *yyyy* = ano, *mm* = mês e *dd* = dia.

  - O marcador *nnnn* é um número de instância que começa com o valor 1 para cada dia.

Informação é gravada no arquivo de log até que o tamanho do arquivo atinge seu valor máximo de especificado e um novo arquivo de log que tem um número de instância incrementada é aberto. Esse processo é repetido ao longo do dia. O log circular exclui os arquivos de log mais antigos quando o diretório de log de conectividade atinge seu tamanho máximo de especificado, ou quando um arquivo de log atinge sua idade máxima de especificado.

Os arquivos de log de conectividade são arquivos de texto que contêm dados no formato de arquivo (CSV) de valores separados por vírgulas. Cada arquivo de log de conectividade tem um cabeçalho que contém as seguintes informações:

  - **\#Software**   Nome do software que criou o arquivo de log de conectividade. Normalmente, o valor é o Microsoft Exchange Server.

  - **\#Version**   Número de versão do software que criou o arquivo de log de conectividade. Atualmente, o valor é 15.0.0.0.

  - **Tipo de log \#**   Valor de tipo de log, que é o Log de conectividade de transporte.

  - **\#Date**   A data e a hora UTC do momento em que o arquivo de log foi criado. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, em que aaaa*yyyy* = ano, mm*mm* = mês, dd*dd* = dia, T indica o início de componente de hora, hh*hh* = hora, mm*mm* = minuto, ss*ss* = segundo, fff*fff* = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.

  - **\#Fields**   Nomes de campo usados nos arquivos de log de conectividade delimitada por vírgula.

Voltar ao início

## Informações gravadas no log de conectividade

O log de conectividade armazena cada evento de conexão de serviço de transporte de saída em uma única linha no log de conectividade. As informações armazenadas em cada linha são organizadas por campos. Esses campos são separados por vírgulas. A tabela a seguir descreve os campos usados para classificar a cada evento de conexões de saída.

### Os campos usados para classificar a cada evento de conexão

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
<td><p>UTC Data / hora do evento conexão. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, em que aaaa<em>yyyy</em> = ano, mm<em>mm</em> = mês, dd<em>dd</em> = dia, T indica o início de componente de hora, hh<em>hh</em> = hora, mm<em>mm</em> = minuto, ss<em>ss</em> = segundo, fff<em>fff</em> = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>GUID que seja exclusivo para cada sessão SMTP, mas é o mesmo para cada evento associado a essa sessão SMTP. Para sessões MAPI no serviço de transporte de caixa de correio, o campo de sessão está em branco.</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p><strong>SMTP</strong> para conexões SMTP, <strong>MAPI</strong> conexões de serviço de transporte de caixa de correio no banco de dados de caixa de correio local.</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>Nome do destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>Caractere único que representa o início, meio ou extremidade da conexão. Os valores possíveis para o campo direção são:</p>
<ul>
<li><p><strong>+</strong>   Conectar</p></li>
<li><p><strong>-</strong>   Desconectar</p></li>
<li><p><strong>&gt;</strong>   Enviar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>Informações de texto associadas ao evento de conexão. Os valores a seguir são exemplos de valores do campo de descrição:</p>
<ul>
<li><p>Número e tamanho das mensagens que foram transmitidos</p></li>
<li><p>Informações de resolução de registro de recurso MX de DNS para domínios de destino</p></li>
<li><p>Informações de resolução de DNS para servidores de caixa de correio de destino</p></li>
<li><p>Mensagens de estabelecimento da conexão</p></li>
<li><p>Mensagens de falha de conexão</p></li>
</ul></td>
</tr>
</tbody>
</table>


Quando o serviço de transporte estabelece uma conexão para um destino, o serviço de transporte pode ser preparado para enviar uma mensagem ou várias mensagens. A conexão e processos de transmissão de mensagem geram vários eventos gravados em várias linhas no log de conectividade. Conexões simultâneas para destinos diferentes criam conectividade entradas de log relacionadas à destinos diferentes que são entrelaçados. No entanto, você pode usar o data / hora, sessão, fonte e campos de direção para organizar as entradas do log de conectividade para cada conexão do início ao fim.

Voltar ao início

