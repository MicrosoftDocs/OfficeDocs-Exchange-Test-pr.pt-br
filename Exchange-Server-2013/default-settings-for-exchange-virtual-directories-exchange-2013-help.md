---
title: 'Configurações padrão dos diretórios virtuais do Exchange: Exchange 2013 Help'
TOCTitle: Configurações padrão para os diretórios virtuais do Exchange
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52058877
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurações padrão para os diretórios virtuais do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Exchange Server 2013 configura automaticamente vários diretórios virtuais do Internet Information Services (IIS) durante a instalação. Este tópico contém informações sobre as configurações de autenticação do IIS padrão e configurações de Secure Sockets Layer (SSL) padrão para os servidores de caixa de correio e de acesso para cliente.

## Servidor de Acesso para Cliente

A tabela a seguir lista as configurações padrão em um servidor de acesso para cliente autônomo Exchange 2013.

### Autenticação do IIS padrão de servidor de acesso para cliente e configurações de SSL

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Diretório virtual</th>
<th>Método de autenticação</th>
<th>Configurações de SSL</th>
<th>Método de gerenciamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Site padrão</p></td>
<td><ul>
<li><p>Anônimo</p></li>
</ul></td>
<td><ul>
<li><p>Obrigatório</p></li>
</ul></td>
<td><p>Console de gerenciamento do IIS</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>Console de gerenciamento do IIS</p></td>
</tr>
<tr class="odd">
<td><p>Descoberta Automática</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
<li><p>Autenticação básica</p></li>
<li><p>Autenticação do Windows</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>Exchange Shell de gerenciamento (Shell)</p></td>
</tr>
<tr class="even">
<td><p>ECP</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
<li><p>Autenticação básica</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>Exchange Centro de administração (EAC) ou o Shell</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
<li><p>autenticação</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>Você pode usar os métodos a seguir para atribuir ABPs aos usuários de caixas de correio individuais:</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>Autenticação básica</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>EAC ou Shell</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>autenticação</p></li>
</ul></td>
<td><ul>
<li><p>Não necessária</p></li>
</ul></td>
<td><p>EAC ou Shell</p></td>
</tr>
<tr class="even">
<td><p>OWA</p></td>
<td><ul>
<li><p>Autenticação básica</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>EAC ou Shell</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
</ul></td>
<td><ul>
<li><p>Não necessária</p></li>
</ul></td>
<td><p>Você pode usar os métodos a seguir para atribuir ABPs aos usuários de caixas de correio individuais:</p></td>
</tr>
<tr class="even">
<td><p>RPC</p></td>
<td><ul>
<li><p>Autenticação básica</p></li>
<li><p>Autenticação do Windows</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>Você pode usar os métodos a seguir para atribuir ABPs aos usuários de caixas de correio individuais:</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>Por padrão, todos os métodos de autenticação estão desabilitados.</p></td>
<td><ul>
<li><p>Obrigatório</p></li>
</ul></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Servidor de Caixa de Correio

A tabela a seguir lista as configurações padrão em um servidor de caixa de correio autônomo Exchange 2013.

### Autenticação do IIS padrão de servidor de caixa de correio e as configurações SSL

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Diretório virtual</th>
<th>Método de autenticação</th>
<th>Configurações de SSL</th>
<th>Método de gerenciamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Site padrão</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
</ul></td>
<td><ul>
<li><p>Exigido de SSL</p></li>
<li><p>Requer criptografia de 128 bits</p></li>
</ul></td>
<td><p>Este diretório virtual não pode ser configurado pelo usuário.</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Autenticação anônima</p></li>
</ul></td>
<td><ul>
<li><p>Não necessária</p></li>
</ul></td>
<td><p>Você pode usar os métodos a seguir para atribuir ABPs aos usuários de caixas de correio individuais:</p></td>
</tr>
</tbody>
</table>

