---
title: 'Mecanismos de autenticação do conector de recebimento: Exchange 2013 Help'
TOCTitle: Mecanismos de autenticação do conector de recebimento
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 50486134
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mecanismos de autenticação do conector de recebimento

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_


Os mecanismos de autenticação do conector de recebimento são as seguintes:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Mecanismo de autenticação</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nenhuma</p></td>
<td><p>Nenhuma autenticação.</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>Anuncie STARTTLS. Requer a disponibilidade de um certificado de servidor para oferecer TLS.</p></td>
</tr>
<tr class="odd">
<td><p>Integrado</p></td>
<td><p>NTLM e Kerberos (autenticação integrada Windows ).</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>Autenticação básica. Requer um logon autenticado.</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>Autenticação básica sobre TLS. Requer um certificado de servidor.</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Exchange Autenticação de servidor (o aplicativo de serviços de segurança genéricos programação GSSAPI (interface) e GSSAPI mútuo).</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>A conexão é considerada protegida externamente usando um mecanismo de segurança que é externo ao Exchange. A conexão pode ser uma associação de segurança (IPsec) do protocolo de Internet ou em uma rede virtual privada (VPN). Como alternativa, os servidores podem residir em uma rede fisicamente controlada confiável. O método de autenticação <code>ExternalAuthoritative</code> requer o grupo de permissão <code>ExchangeServers</code> . Esta combinação de grupo de segurança e o método de autenticação permite que a resolução de endereços de email do remetente anônimo para mensagens que são recebidos por meio deste conector.</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre os mecanismos de autenticação de conector de recebimento, consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)).

