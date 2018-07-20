---
title: 'Permissões de conector de recebimento: Exchange 2013 Help'
TOCTitle: Permissões de conector de recebimento
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 50485287
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de conector de recebimento

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

A tabela a seguir lista os tipos de permissão e uma descrição para cada um.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permissão do conector de recebimento</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>Essa permissão deve ser concedida para a sessão ou ela não poderá enviar mensagens ao conector de recebimento. Se uma sessão não tiver essa permissão, os comandos MAIL FROM e AUTH falharão.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>Essa permissão autoriza a sessão a retransmitir mensagens por meio desse conector. Se essa permissão não for concedida, somente mensagens endereçadas a destinatários em domínios aceitos serão aceitas por esse conector.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>Essa permissão autoriza a sessão a ignorar a verificação de falsificação de endereço do remetente.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>Essa permissão permite que os remetentes tenham endereços de email em domínios autoritativos para estabelecer uma sessão com esse conector de recebimento.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>Essa permissão permite que os servidores de Exchange 2003 enviar mensagens de remetentes internos. Exchange 2010 reconhecerá as mensagens como sendo interno. O remetente pode declarar a mensagem como confiável. Mensagens que entram no sistema Exchange por meio de envios anônimos serão retransmitidas por meio de sua organização Exchange com esse sinalizador em um estado não confiável.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>Essa permissão autoriza a sessão a enviar uma mensagem que tenha todos os cabeçalhos recebidos intactos. Se essa permissão não for concedida, o servidor removerá todos os cabeçalhos recebidos.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>Essa permissão autoriza a sessão a enviar uma mensagem que tenha todos os cabeçalhos da organização intactos. Todos os cabeçalhos da organização começam com <strong>X-MS-Exchange-Organization-</strong>. Se essa permissão não for concedida, o servidor de recebimento removerá todos os cabeçalhos da organização.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>Essa permissão autoriza a sessão a enviar uma mensagem que tenha todos os cabeçalhos da floresta intactos. Todos os cabeçalhos de floresta começam com <strong>X-MS-Exchange-Forest-</strong>. Se essa permissão não for concedida, o servidor de recebimento removerá todos os cabeçalhos de floresta.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>Essa permissão autoriza a sessão a enviar uma mensagem que contenha o comando XEXCH50. Esse comando é necessário para interoperabilidade com o Exchange 2003. O comando XEXCH50 fornece dados como o SCL (nível de confiança de spam) para a mensagem.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>Essa permissão autoriza a sessão a enviar uma mensagem que exceda a restrição de tamanho da mensagem configurada para o conector.</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>Essa permissão permite que a sessão ignora a filtragem anti-spam.</p></td>
</tr>
</tbody>
</table>

