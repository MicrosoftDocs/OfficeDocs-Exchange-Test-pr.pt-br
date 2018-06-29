---
title: 'Log de protocolo: Exchange 2013 Help'
TOCTitle: Log de protocolo
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 50485426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log de protocolo

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O log de protocolo registra as conversações SMTP que ocorrem entre servidores de email como parte de entrega de mensagens. Essas conversas SMTP ocorrem nos conectores de Envio e nos de Recebimento que existem no serviço de Transporte de Front-End nos servidores de Acesso para Cliente, no serviço de Transporte em servidores de Caixa de Correio e o serviço de Transporte de Caixa de Correio em servidores de Caixa de Correio. Você pode usar o log de protocolo para diagnosticar problemas de fluxo de mensagens.

Por padrão, o log de protocolo está desabilitado em todos os conectores de envio e de recebimento. O log de protocolo está habilitado ou desabilitado em cada conector individual. Outras opções de registro em log de protocolo são definidas para todos os conectores de Recebimento ou todos os conectores de Envio que existem em cada serviço de transporte individual no servidor. Todos os conectores de Recebimento em um serviço de transporte compartilham os mesmos arquivos de log de protocolo e opções de log de protocolo. Esses arquivos de log de protocolo e opções de log de protocolo são separados dos arquivos de log de protocolo de conector de Envio e das opções de log de protocolo no serviço de transporte no mesmo servidor.

As opções a seguir estão disponíveis para os logs de protocolo de todos os conectores de Envio ou todos os conectores de Recebimento em cada serviço de transporte no servidor Exchange:

  - Especifique o local dos arquivos de log de protocolo do conector de envio ou de recebimento.

  - Especifique o tamanho máximo dos arquivos de log de protocolo do conector de envio ou de recebimento. O tamanho padrão é de 10 megabytes (MB).

  - Especifique o tamanho máximo do diretório que contém os arquivos de log de protocolo do conector de envio ou de recebimento. O tamanho padrão é 250 MB.

  - Especifique a idade máxima dos arquivos de log de protocolo do conector de envio ou de recebimento. A idade padrão é 30 dias.

Por padrão, o Exchange usa log circular para limitar os logs de protocolo com base no tamanho e idade do arquivo, para ajudar a controlar o espaço em disco rígido utilizado pelos arquivos de log.

Um conector de Envio especial chamado de conector de Envio intraorganizacional existe no serviço de Transporte em cada servidor de Caixa de Correio e no serviço de Transporte de Front-End, em cada servidor de Acesso para Cliente. Esse conector foi criado implicitamente, é invisível, e não exige gerenciamento. O conector de Envio intraorganizacional é usado por estes serviços de transporte:

  - **Serviço de transporte em servidores de caixa de correio**
    
      - Retransmite mensagens para o serviço de Transporte e o serviço de Transporte de caixa de correio em outros servidores de Caixa de Correio do Exchange 2013 na organização.
    
      - Retransmite mensagens para outros servidores de Transporte de Hub do Exchange 2007 ou do Exchange 2010 na organização.
    
      - Retransmite mensagens para servidores de Transporte de Borda na rede de perímetro.

  - **Serviço de Transporte de Front-End em servidores de Acesso para Cliente**   Retransmite mensagens para o serviço de Transporte nos servidores de Caixa de Correio do Exchange 2013 na organização.

Um conector de Envio equivalente chamado de conector de Envio de entrega de caixa de correio existe no serviço de Transporte de Caixa de Correio em cada servidor de Caixa de Correio. Esse conector é também criado implicitamente, é invisível e não exige gerenciamento. O conector de Envio de entrega de caixa de correio é usado para retransmitir mensagens para o serviço de Transporte e o serviço de Transporte de Caixa de Correio em outros servidores de Caixa de Correio na organização.

Por padrão, o log de protocolo do conector de Envio de entrega da caixa de correio também é desabilitado. Você pode habilitar ou desabilitar o log de protocolo do conector de Envio dentro de entrega da caixa de correio usando o parâmetro *MailboxDeliveryConnectorProtocolLoggingLevel* no cmdlet **Set-MailboxTransportService**. Se você habilitar o log de protocolo do conector de Envio de entrega da caixa de correio, o log ocorrerá nos logs de protocolo do conector de Envio configurados no serviço de Transporte de Caixa de Correio no servidor de Caixa de Correio.

**Sumário**

Structure of the protocol log files

Information written to the protocol log

## Estrutura dos arquivos de log de protocolo

Por padrão, os arquivos de log de protocolo existem nos seguintes locais:

  - **Arquivos de log de protocolo do conector de Recebimento do serviço de Transporte nos servidores de Caixa de Correio**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **Arquivos de log de protocolo do conector de Recebimento do serviço de Transporte de Caixa de Correio nos servidores de Caixa de Correio**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **Arquivos de log de protocolo do conector de Recebimento do serviço de Transporte de Front-End nos servidores de Acesso para Cliente**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **Arquivos de log de protocolo do conector de Envio do serviço de Transporte nos servidores de Caixa de Correio**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **Arquivos de log de protocolo do conector de Envio do serviço de Transporte de Caixa de Correio nos servidores de Caixa de Correio**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **Arquivos de log de protocolo do conector de Envio do serviço de Transporte de Front-End nos servidores de Acesso para Cliente**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

A convenção de nomenclatura para arquivos de log em cada diretório de log de protocolo é *prefixoaaaammdd-nnnn*.log. Os marcadores representam as seguintes informações:

  - O *prefixo* do marcador é SEND para conectores de envio ou RECV para conectores de recebimento.

  - O marcador *aaaammdd* é a data UTC (Tempo Universal Coordenado) em que o arquivo de log foi criado. O espaço reservado *aaaa* = ano, *mm* = mês e *dd* = dia.

  - O marcador *nnnn* é um número de instância que começa com o valor 1 para cada dia.

Informações são gravadas no arquivo de log até o tamanho do arquivo atingir o valor máximo especificado e um novo arquivo de log com número de instância incrementado ser aberto. Esse processo se repete ao longo do dia. O log circular exclui os arquivos de log mais antigos quando o diretório de log de protocolo atinge o tamanho máximo especificado ou quando um arquivo de log atinge a idade máxima especificada.

Os arquivos de log de protocolo são arquivos de texto que contêm dados no formato de arquivo CSV (valor separado por vírgula). Cada arquivo de log de protocolo possui um cabeçalho com as seguintes informações:

  - **\#Software**   O nome do software que criou o arquivo de log de protocolo. Normalmente, o valor é Microsoft Exchange Server.

  - **\#Version:**   O número da versão do software que criou o arquivo de log de protocolo. Atualmente, o valor é 15.0.0.0.

  - **\#Log-Type**   O valor do tipo de log desse campo é Log de Protocolo de Recebimento SMTP ou Log de Protocolo de Envio SMTP.

  - **\#Date**   A data e a hora UTC do momento em que o arquivo de log foi criado. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd*yyyy-mm-dd*Thh:mm:ss.fff*hh:mm:ss.fff*Z, em que aaaa*yyyy* = ano, mm*mm* = mês, dd*dd* = dia, T indica o início de componente de hora, hh*hh* = hora, mm*mm* = minuto, ss*ss* = segundo, fff*fff* = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.

  - **\#Fields**   Os nomes de campos delimitados por vírgulas usados nos arquivos de log de protocolo.

Voltar ao início

## Informações gravadas no log de protocolo

O log de protocolo armazena cada evento do protocolo SMTP em uma única linha no log de protocolo. As informações armazenadas em cada linha são organizadas por campos. Esses campos são separados por vírgulas. A tabela a seguir descreve os campos usados para classificar cada protocolo.

### Campos usados para classificar cada evento de protocolo

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
<td><p>A data e a hora UTC do evento de protocolo. A data e a hora UTC é representada no formato de data e hora ISO 8601: aaaa-mm-dd<em>yyyy-mm-dd</em>Thh:mm:ss.fff<em>hh:mm:ss.fff</em>Z, em que aaaa<em>yyyy</em> = ano, mm<em>mm</em> = mês, dd<em>dd</em> = dia, T indica o início de componente de hora, hh<em>hh</em> = hora, mm<em>mm</em> = minuto, ss<em>ss</em> = segundo, fff<em>fff</em> = frações de um segundo e Z significa Zulu, que é outra maneira de indicar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>O DN (nome diferenciado) do conector associado ao evento SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>Um GUID exclusivo para cada sessão SMTP, mas que é o mesmo para cada evento associado a essa sessão SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>Contador que começa em 0 e é incrementado para cada evento na mesma sessão SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>Ponto de extremidade local de uma sessão SMTP. Consiste em um endereço IP e um número de porta TCP formatado como <em>&lt;endereço IP&gt;</em>:<em>&lt;porta&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>Ponto de extremidade remoto de uma sessão SMTP. Consiste em um endereço IP e um número de porta TCP formatado como <em>&lt;endereço IP&gt;</em>:<em>&lt;porta&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>Caractere único que representa o evento de protocolo. Os valores possíveis para o evento são:</p>
<ul>
<li><p><strong>+</strong>   Conectar</p></li>
<li><p><strong>-</strong>   Desconectar</p></li>
<li><p><strong>&gt;</strong>   Enviar</p></li>
<li><p><strong>&lt;</strong>   Receber</p></li>
<li><p><strong>*</strong>   Informações</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>Informações de texto associadas ao evento SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>Informações de contexto adicionais que podem estar associadas ao evento SMTP.</p></td>
</tr>
</tbody>
</table>


Uma única conversa SMTP que representa o envio ou o recebimento de uma única mensagem de email que gera vários eventos SMTP. Esses eventos SMTP resultam em várias linhas a serem gravadas no log de protocolo. Várias conversas SMTP, ou seja, o envio ou o recebimento de várias mensagens de email pode ocorrer ao mesmo tempo. São criadas entradas de log de protocolo de diferentes conversas SMTP que estão intercaladas. É possível usar os campos id da sessão e número de sequência para classificar as entradas de log de protocolo pela conversa SMTP.

Voltar ao início

