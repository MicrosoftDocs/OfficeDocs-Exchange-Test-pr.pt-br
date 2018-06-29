---
title: 'Log de protocolo para POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Log de protocolo para POP3 e IMAP4
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50556157
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log de protocolo para POP3 e IMAP4

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Você pode usar o log de protocolo para analisar as conexões POP3 e IMAP4 em seu ambiente do Exchange. Isso pode ser útil se você estiver solucionando problemas relacionados ao desempenho de POP3 ou IMAP4.

## Habilitando logs de protocolos POP3 e IMAP4

Você pode habilitar, desabilitar ou alterar o log de protocolo usando o Shell de Gerenciamento do Exchange. Se você habilitar o log de protocolo usando o Shell, as configurações padrão de log de protocolo serão usadas. Na maioria dos casos, as configurações padrão serão suficientes.

Outra opção é habilitar, desabilitar e modificar as opções de log de protocolo editando os arquivos de configuração Microsoft.Exchange.Pop3.exe.config e Microsoft.Exchange.Imap4.exe.config localizados em seu servidor de Acesso para Cliente do MicrosoftExchange Server 2013. Para obter mais informações sobre como gerenciar as configurações dos protocolos POP3 e IMAP4, consulte [Configurar o log de protocolo para POP3 e IMAP4](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md).

## Revisando o log de protocolo

Os arquivos de log de protocolo são arquivos de texto que contêm dados no formato de arquivo CSV (valor separado por vírgula). O log de protocolo armazena cada evento de protocolo em uma única linha. As informações armazenadas em cada linha são organizadas por campos. Esses campos são separados por vírgulas. A tabela a seguir descreve os campos usados para classificar cada evento de protocolo.

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
<td><p>data-hora</p></td>
<td><p>A data e a hora do evento de protocolo. O valor é formatado como <em>aaaa-mm-ddhh:mm:ss.fffZ</em>, onde <em>aaaa</em> = ano, <em>mm</em> = mês, <em>dd</em> = dia, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, <em>fff</em> = frações de um segundo e <em>Z</em> significa Zulu. Zulu é outra forma de indicar UTC (Tempo Universal Coordenado).</p></td>
</tr>
<tr class="even">
<td><p>connector-id</p></td>
<td><p>Esse campo não é usado para o log dos protocolos POP3 e IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>id da sessão</p></td>
<td><p>Uma GUID que identifica exclusivamente a sessão SMTP que está associada a um evento de protocolo.</p></td>
</tr>
<tr class="even">
<td><p>número de seqüência</p></td>
<td><p>Contador que começa em 0 e é incrementado para cada evento na mesma sessão.</p></td>
</tr>
<tr class="odd">
<td><p>ponto de extremidade local</p></td>
<td><p>O ponto de extremidade local de uma sessão POP3 ou IMAP4. Isso consiste em um endereço IP e um número de porta TCP, formatados da seguinte maneira: <em>&lt;endereço IP&gt;</em>:<em>&lt;porta&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p>ponto de extremidade remoto</p></td>
<td><p>O ponto de extremidade remoto de uma sessão POP3 ou IMAP4. Isso consiste em um endereço IP e um número de porta TCP, formatados da seguinte maneira: <em>&lt;endereço IP&gt;</em>:<em>&lt;porta&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p>evento</p></td>
<td><p>Um único caractere que representa o evento de protocolo. Os valores possíveis para o evento são:</p>
<ul>
<li><p>+   Conectar</p></li>
<li><p>-   Desconectar</p></li>
<li><p>&gt;   Enviar</p></li>
<li><p>&lt;   Receber</p></li>
<li><p>*   Informações</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>dados</p></td>
<td><p>Informações de texto associadas ao evento POP3 ou IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>contexto</p></td>
<td><p>Esse campo não é usado para o log dos protocolos POP3 e IMAP4.</p></td>
</tr>
</tbody>
</table>

