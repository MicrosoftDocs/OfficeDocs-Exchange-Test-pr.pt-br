---
title: 'Autoridades de certificação raiz confiáveis para confianças de federação: Exchange 2013 Help'
TOCTitle: Autoridades de certificação raiz confiáveis para confianças de federação
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 50486727
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoridades de certificação raiz confiáveis para confianças de federação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-07-26_

Para estabelecer uma confiança de federação entre sua organização do Microsoft Exchange Server 2013 e o [sistema de autenticação do Azure Active Directory](https://go.microsoft.com/fwlink/p/?linkid=135986), você precisa de um certificado digital instalado no servidor Exchange usado para criar a relação de confiança. É altamente recomendável usar um certificado autoassinado. Um certificado autoassinado é criado e instalado automaticamente ao usar o Assistente para **Habilitar a confiança de Federação** no Centro de administração do Exchange (EAC).

Se você não quiser usar o certificado autoassinado recomendado, você deve solicitar e instalar um certificado x. 509 Secure Sockets Layer (SSL) de uma autoridade de certificação (CA) confiável pela Microsoft. Embora certificados emitidos por outras CAs também podem ser usados para estabelecer uma confiança de federação com o sistema de autenticação AD do Azure, eles não são certificados pela Microsoft Data.

A tabela a seguir lista as CAs atualmente consideradas confiáveis pela Microsoft. Essas CAs foram testadas quanto a uso com o Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome amigável da CA</th>
<th>Emitido por</th>
<th>Finalidades pretendidas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Autoridade de certificação Comodo</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Autoridade de certificação raiz CyberTrust Baltimore</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Autoridade de certificação raiz global Digicert</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>EV alta garantia Digicert</p></td>
<td><p>Autoridade de certificação raiz global Digicert</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax Secure Certification Authority</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>Autoridade de certificação GlobalSign</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Autoridade de certificação de soluções de rede</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Autoridade de certificação Comodo</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>Autoridade de Certificação de Sistemas de Confiança SECOM</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Autoridade de certificação Comodo</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Autoridade de certificação principal pública Classe 3</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>Rede confiável VeriSign</p></td>
<td><p>Autenticação de servidor, autenticação de cliente</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre requisitos de certificação para Federação, consulte [Federação](federation-exchange-2013-help.md).

