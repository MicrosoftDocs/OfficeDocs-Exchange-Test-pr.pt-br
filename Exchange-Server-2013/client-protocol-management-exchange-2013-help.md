---
title: 'Gerenciamento de protocolo de cliente: Exchange 2013 Help'
TOCTitle: Gerenciamento de protocolo de cliente
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 50486098
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciamento de protocolo de cliente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O gerenciamento dos protocolos de cliente do Exchange ActiveSync, Outlook Web App, POP3, IMAP4, o serviço Descoberta automática, serviços Web do Exchange e o serviço de disponibilidade ocorre em três áreas diferentes: Centro de administração do Exchange (EAC), o Shell de gerenciamento do Exchange e o Gerenciador de serviços de informações da Internet (IIS). As configurações que são gerenciadas em cada local variam por protocolo de cliente.

## Gerenciando configurações do Outlook Web App

A maioria das configurações que afetam a quais recursos do Outlook Web App estão disponíveis para os usuários pode ser definida no diretório virtual do Outlook Web App ou pode ser configuradas em uma diretiva de caixa de correio do Outlook Web App. Usando políticas de caixa de correio do Outlook Web App, você pode definir os recursos disponíveis a usuários individuais. Configurações de diretiva de caixa de correio substituem configurações do diretório virtual. Para obter mais informações sobre como gerenciar o Outlook Web App, consulte [Outlook Web App](outlook-web-app-exchange-2013-help.md).

## Gerenciando configurações do Exchange ActiveSync

No Exchange 2010, todos os protocolos de acesso do cliente foram implementados e gerenciados em uma função de servidor único, a função de servidor acesso para cliente. Gerenciamento dos protocolos foi executado em uma única instância do IIS, houve um objeto de diretório virtual único no Active Directory para cada protocolo de cliente e um único conjunto de cmdlets foram usadas para configurar o diretório virtual.

Em Exchange 2013, o gerenciamento de protocolo de cliente para o Exchange ActiveSync é dividido entre o servidor de acesso para cliente e o servidor de caixa de correio. Devido a essa alteração de arquitetura, você pode executar as tarefas de gerenciamento de diretório virtual diferente no servidor acesso para cliente e o servidor de caixa de correio. Se esses dois servidores não estão instalados no mesmo computador físico, os parâmetros que você pode usar com o diretório virtual cmdlets será alterado com base na função de servidor no qual você está executando-los.

Para obter mais informações sobre as alterações de arquitetura no Exchange 2013, consulte [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

Existem dois tipos de configurações que podem ser aplicadas ao diretório virtual do Exchange ActiveSync:

  - Configurações aplicáveis à sessão de correio

  - Configurações aplicáveis para o servidor e o diretório virtual

As configurações que se aplicam a uma sessão de correio são configurações de sessão do usuário. Quando um usuário se conecta a um servidor de acesso para cliente, a conexão é intermediadas por proxy no servidor de caixa de correio que contém a caixa de correio do usuário. Um identificador exclusivo do diretório virtual está incluído com a solicitação intermediadas por proxy. Em seguida, o servidor de caixa de correio recupera as configurações do diretório virtual do Active Directory e aplica-se à sessão. As configurações do diretório virtual são armazenados em cache no servidor de caixa de correio para melhorar o desempenho.

Se a conexão for intermediadas por proxy para um site diferente do Active Directory, as configurações do diretório virtual serão carregadas do servidor acesso para cliente no mesmo site como o servidor de caixa de correio, não do servidor de acesso para cliente que originou a conexão.

As tabelas a seguir indicam quais configurações do diretório virtual podem ser gerenciadas em quais servidores. Se você tentar gerenciar uma determinada configuração em um servidor para o qual não aplicável, você receberá uma mensagem de erro indicando que a propriedade que você está tentando definir é somente leitura para o servidor que você está operando em.

**Configurações do diretório virtual do Exchange ActiveSync em servidores de acesso para cliente**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
</tbody>
</table>


**Configurações do diretório virtual do Exchange ActiveSync em servidores de acesso para cliente e caixa de correio**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>Nome</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>Caminho</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
</tbody>
</table>


## Gerenciando configurações de POP3 e IMAP4

Em Exchange 2013, a implementação dos protocolos POP3 e IMAP4 tiver sido segmentada entre as funções de servidor de caixa de correio e acesso para cliente. Devido a nova implementação, conectividade de POP3 e IMAP4 são cada gerenciados por um serviço no servidor de acesso para cliente, bem como por um serviço no servidor de caixa de correio. Os nomes dos serviços que são executados no servidor de acesso para cliente são os mesmos os nomes que existiam no Exchange 2010: serviço IMAP4 do Microsoft Exchange e o serviço Microsoft Exchange POP3. Os nomes dos dois novos serviços que são executados no servidor de caixa de correio são o serviço de back-end do Microsoft Exchange IMAP4 e o serviço de back-end do Microsoft Exchange POP3.

Conforme você gerencia conectividade POP3 e IMAP4 em sua organização, considere o seguinte:

  - Se você estiver executando a função de servidor acesso para cliente e a função de servidor de caixa de correio no mesmo computador, quaisquer alterações feitas às configurações de POP3 ou IMAP4 são aplicadas automaticamente aos serviços POP3 e IMAP4 corretos.

  - Se você estiver executando a função de servidor acesso para cliente e a função de servidor de caixa de correio em computadores separados, será necessário gerenciar as configurações no computador que gerencia a configuração que você deseja alterar.

Use que as tabelas a seguintes indicam quais configurações POP/IMAP são cada função de servidor.

**Configurações de POP3 e IMAP4 no servidor de acesso para cliente**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>Faixa</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>Acesso do cliente</p></td>
</tr>
</tbody>
</table>


**Configurações de POP3 e IMAP4 no servidor de caixa de correio**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>Caixa de Correio</p></td>
</tr>
</tbody>
</table>


**Configurações de POP3 e IMAP4 nos servidores de acesso para cliente e caixa de correio**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="even">
<td><p>Servidor</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Caixa de correio e acesso para cliente</p></td>
</tr>
</tbody>
</table>

