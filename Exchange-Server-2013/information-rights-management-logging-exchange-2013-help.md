---
title: 'Log de gerenciamento de direitos de informação: Exchange 2013 Help'
TOCTitle: Log de gerenciamento de direitos de informação
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 50486865
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log de gerenciamento de direitos de informação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

No Microsoft Exchange Server 2013, as operações de gerenciamento de direitos de informação (IRM) são registradas nos logs IRM. Logs IRM ajudarão-lo a monitorar e solucionar problemas de interações entre o cliente do Rights Management Services (RMS) em um servidor Exchange 2013 e cluster Active Directory Rights Management Services (AD RMS) em sua organização.

Para saber mais sobre o IRM, consulte [Gerenciamento de Direitos de Informação](information-rights-management-exchange-2013-help.md).

**Conteúdo**

Estrutura dos logs IRM

Processo de registro em log

Informações gravadas logs de IRM

Gerenciar o IRM logs

Procurando tarefas de gerenciamento relacionadas ao IRM? Consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## Estrutura dos logs IRM

Por padrão, os logs do IRM estão localizados em C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs.

A convenção de nomenclatura para arquivos de log do IRM é \<*Processo*\>\_\<*Identificador de processo* ou *Identificador AppPool do IIS*\>\_IRMLOG*aaaammdd*-*nnnn*.log, em que:

  - \<*Process*\>= processo que cria o arquivo de log. Por exemplo, no serviço de transporte, isso será EdgeTransport.

  - \<*Identificador de processo* ou *Identificador AppPool do IIS\>* =ID numérico do processo.

  - *aaaammdd* = data Tempo Universal Coordenado (UTC) quando o arquivo de log foi criado.

  - *nnnn* = número de instância, que começa em 1 para cada dia.

Um nome de arquivo de log do IRM é EdgeTransport\_1056\_IRMLOG20101201-1.log.

A tabela a seguir mostra os logs gerados em funções de servidor diferentes.

### Logs em funções de servidor

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Função de servidor</th>
<th>Nome do arquivo de log do IRM</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serviço de Transporte</p></td>
<td><p>EdgeTransport_&lt;<em>Identificador de processo</em>&gt;_IRMLOG<em>aaaammdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Esse log é usado para registrar todas as transações de RMS feitas pelo pipeline de transporte no serviço de transporte (por exemplo, as regras de proteção de transporte e descriptografia do relatório de diário). O identificador do processo (PID) do processo de edgetransport.exe é usado para gerar o nome do arquivo de log.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio</p></td>
<td><p>msftefd_&lt;<em>Identificador de processo</em>&gt;_IRMLOG<em>aaaammdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Esse log é usado para registrar todas as transações de RMS que ocorrem durante as solicitações de pesquisa e índice. Exchange 2013 Servidores de caixa de correio usam o processo de msftefd.exe para indexação de conteúdo. O PID do processo msftefd.exe é usado para gerar o nome do arquivo de log.</p></td>
</tr>
<tr class="odd">
<td><p>Acesso para cliente</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>aaaammdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Esse log é usado para registrar todas as transações do IRM no Microsoft OfficeOutlook Web App.</p></td>
</tr>
<tr class="even">
<td><p>Todas as funções de servidor Exchange 2013</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>aaaammdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Esse log é usado para registrar todas as transações RMS IMS emitidas pelo PowerShell do Windows, por exemplo, durante a emissão do cmdlet <strong>Test-IRMConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Processo de registro em log

As informações são gravadas no arquivo de log até que o tamanho do arquivo chegue ao valor máximo especificado. Quando o tamanho máximo for atingido, um arquivo de log com um número de instância incremental será criado. Esse processo se repete ao longo do dia. O log circular exclui os arquivos de log mais antigos quando o diretório de log do IRM atingir o tamanho máximo especificado ou quando um arquivo de log chegar à idade máxima especificada na configuração do registro em log em cada servidor.

Voltar ao início

## Informações gravadas logs de IRM

Os arquivos de log do IRM são arquivos de texto que contêm dados no formato CSV (valor separado por vírgula). Cada log do IRM possui um cabeçalho com as seguintes informações:

  - **\#Software**   O nome do software que criou o arquivo de log do IRM. Geralmente, o valor é `Microsoft Exchange Server`.

  - **\#Version:**    Número da versão do software que criou o arquivo de log do IRM.

  - **\#Log-type**   Valor do tipo de log, `Rms Client Manager Log`.

  - **\#Date:**    A data e a hora UTC do momento em que o arquivo de log foi criado. A data e a hora UTC é representada no formato de data e hora ISO 8601: *aaaa*-*mm*-*dd*T*hh*:*mm*:*ss.fff*Z, em que:
    
      - aaaa = ano
    
      - *mm* = mês
    
      - *dd* = dia
    
      - T = designador de tempo usado para mostrar o início do componente de hora
    
      - *hh* = hora
    
      - *mm* = minuto
    
      - *ss* = segundo
    
      - *fff* = frações de um segundo
    
      - Z = Zulu, outra maneira de denotar UTC

  - **\#Fields**   Os nomes de campos delimitados por vírgulas usados nos arquivos de log do IRM.
    
    O log do IRM armazena cada evento de transação do RMS em uma única linha, organizada em campos separados por vírgula. A tabela a seguir lista os campos em logs do IRM para todas as funções de servidor com recursos do IRM habilitados.
    
    ### Campos usados em logs do IRM
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Campo</th>
    <th>Descrição</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>Lista o carimbo de data/hora UTC.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>Lista o recurso de cliente do RMS usado. Os valores válidos incluem:</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>Verificação da assinatura</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>Lista o tipo de evento. Os valores válidos incluem:</p>
    <ul>
    <li><p><code>Acquire</code>   Uma licença ou um modelo do RMS é solicitado.</p></li>
    <li><p><code>Success</code>   Uma licença ou um modelo do RMS é adquirido com êxito.</p></li>
    <li><p><code>Exception</code>   Ocorreu um erro.</p></li>
    <li><p><code>Queued</code>   Uma solicitação está pendente.</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>Reservado para uso interno da Microsoft.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>Lista o URL de servidor do RMS acessado durante a operação.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>Usado pelo processo de chamada para vincular várias transações do RMS. Os valores válidos incluem:</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>Identifica uma transação exclusiva. Todos os eventos que ocorrem durante uma transação têm o mesmo ID de transação.</p></td>
    </tr>
    </tbody>
    </table>


Voltar ao início

## Gerenciar o IRM logs

Em cada função de servidor com recursos do IRM habilitados, o registro em log do IRM é habilitado por padrão. Para cada função de servidor, é possível modificar a seguinte configuração de log do IRM usando-se o cmdlet **Set** da função de servidor correspondente. Por exemplo, para configurar o registro em log do IRM, você usa o cmdlet **Set-MailboxServer**.

### Parâmetros de configuração para logs do IRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>Habilita o registro em log das transações do IRM. O registro em log do IRM está habilitado por padrão. Para desabilitar o registro em log do IRM para uma função de servidor, defina o parâmetro como <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>Especifica a idade máxima de cada arquivo de log do IRM. Os arquivos de log anteriores à idade especificada são excluídos. O valor padrão é <code>30.00:00:00</code> (30 dias).</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>Especifica o tamanho máximo de todos os logs do IRM no diretório do log de conectividade. Quando um diretório atingir o tamanho máximo de arquivo, o servidor excluirá primeiro os arquivos de log mais antigos. O valor-padrão é <code>250 MB</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>Especifica o tamanho de arquivo máximo para um único arquivo de log. Quando um arquivo atinge o tamanho especificado, um arquivo de log é criado, e o número da instância é incrementado. O valor-padrão é <code>10 MB</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>Especifica o local de log do IRM. O caminho padrão é % ExchangeInstallPath%Logging\IRMLogs.</p></td>
</tr>
</tbody>
</table>


Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/pt-br/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/pt-br/library/jj215682\(v=exchg.150\))

Voltar ao início

