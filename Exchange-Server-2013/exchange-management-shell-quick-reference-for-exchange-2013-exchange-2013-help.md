---
title: 'Referência rápida do Shell de gerenciamento do Exchange para o Exchange 2013'
TOCTitle: Referência rápida do Shell de gerenciamento do Exchange para o Exchange 2013
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 50485423
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Referência rápida do Shell de gerenciamento do Exchange para o Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Este tópico descreve os cmdlets utilizados mais frequentemente disponíveis na versão Release to Manufacturing (RTM) e posteriores do Microsoft Exchange Server 2013 e fornece exemplos para seu uso.


> [!NOTE]
> Mais conteúdo será adicionado sobre outras áreas de Exchange 2013, em breve.



Para obter mais informações sobre o shell de Gerenciamento do Exchangeno Exchange 2013 e todos os cmdlets disponíveis, consulte os seguintes tópicos:

  - [Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\))

  - [Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

## O que deseja saber?

## Ações de cmdlet comuns

Os seguintes verbos são suportados pela maioria dos cmdlets e são associados a uma ação específica.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>O verbo New cria uma nova instância de algo, como uma definição de configuração nova, um banco de dados novo ou um conector SMTP novo.</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>O verbo Remove remove uma instância de algo, como uma caixa de correio ou regras de transporte.</p>
<p>Todos os cmdlets Remove oferecem suporte aos parâmetros <em>WhatIf</em> e <em>Confirm</em>. Para obter mais informações sobre esses parâmetros, consulte Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>O verbo Enable habilita uma configuração ou habilita mensagens em um destinatário.</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>O verbo Disable desabilita uma configuração habilitada ou desabilita mensagens em um destinatário.</p>
<p>Todas as tarefas Disable também oferecem suporte aos parâmetros <em>WhatIf</em> e <em>Confirm</em>. Para obter mais informações sobre esses parâmetros, consulte Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>O verbo Set modifica parâmetros específicos de um objeto, como o alias de um contato ou a retenção de itens excluídos de um banco de dados de caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>O verbo Get consulta um objeto específico ou um subconjunto de um tipo de objeto, como uma caixa de correio específica, todos os usuários de caixa de correio ou usuários de caixa de correio em um domínio.</p></td>
</tr>
</tbody>
</table>


## Parâmetros importantes

Os seguintes parâmetros ajudam a controlar como seus comandos são executados e indicam exatamente o que um comando fará antes de afetar dados.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p>O parâmetro <em>Identity</em> identifica o único objeto da tarefa. Normalmente é usado com os cmdlets Enable, Disable, Remove, Set, e Get. <em>Identity</em> também é um parâmetro posicional, o que significa que não é preciso especificar <em>Identity</em> quando especificar o valor do parâmetro na linha de comando.</p>
<p>Por exemplo, <em>Get-Mailbox -Identity user1</em> consulta a caixa de correio de <em>user1</em>. <em>Get-Mailbox user1</em> é equivalente a <em>Get-Mailbox -Identity user1</em>.</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p>O parâmetro <em>WhatIf</em> instrui o cmdlet a simular as ações que ele executará no objeto. Usando o parâmetro <em>WhatIf</em>, pode-se visualizar quais alterações ocorreriam sem realmente aplicar as alterações. O valor padrão é <em>$true</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p>O parâmetro <em>Confirm</em> faz com que o cmdlet pause o processamento e exige que o administrador confirme o que o cmdlet fará antes que o processamento continue. O valor padrão é <em>$true</em>.</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p>O parâmetro <em>Validate</em> faz com que o cmdlet verifique se todos os pré-requisitos para executar a operação são atendidos e se a operação será concluída com êxito.</p></td>
</tr>
</tbody>
</table>


## Dicas e truques

Os seguintes comandos são associados com diversas tarefas que se pode utilizar ao administrar o Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>Esse cmdlet recupera todas as tarefas que podem ser executadas no Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>palavra-chave</em>*</p></td>
<td><p>Esse cmdlet recupera tarefas que têm <em>palavra-chave</em> no cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>task</em> | Get-Member</p></td>
<td><p>Esse cmdlet recupera todas as propriedades e métodos de <em>task</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List</p></td>
<td><p>Esse cmdlet exibe o resultado da consulta em uma lista formatada. É possível canalizar o resultado de qualquer cmdlet Get para Format-List para exibir todo o conjunto de propriedades existentes no objeto retornado por esse comando, ou pode especificar propriedades específicas que se deseja visualizar, separadas por vírgulas, como no exemplo a seguir: <em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>task</em></p></td>
<td><p>Esse cmdlet recupera Exchange informações de ajuda da shell de gerenciamento do Exchange para qualquer tarefa no Exchange 2013, como no exemplo a seguir: <em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List &gt; <em>arquivo.txt</em></p></td>
<td><p>Esse cmdlet exporta o resultado de <em>task</em> para um arquivo de texto: <em>arquivo.txt</em></p></td>
</tr>
</tbody>
</table>


## Permissões


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Gerenciamento da Organização</em>&quot;</p></td>
<td><p>Este comando recupera os membros do grupo da função de gerenciamento <em>Gerenciamento da Organização</em> .</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Criação de Destinatário de Email</em>&quot; -GetEffectiveUsers</p></td>
<td><p>Este comando recupera uma lista de todos os usuários que têm permissões fornecidas pela função de gerenciamento <em>Criação de Destinatário de Email</em>. Isso inclui usuários que são membros de grupos de função ou grupos de segurança universal (USGs) que têm a função de Criação de Destinatário de Email. Isso não inclui usuários que são membros de grupos de função vinculados em outra floresta.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrador</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>Este comando recupera uma lista de cmdlets que o usuário <em>Administrador</em> pode executar.</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>Este comando recupera uma lista de todos os usuários que podem executar o cmdlet <em>Remove-Mailbox</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>Este comando recupera uma lista de todos os usuários que podem modificar a caixa de correio de <em>kima</em>.</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Seattle Users</em>&quot; -RecipientRestrictionFilter { <em>City</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Seattle Admins</em>&quot; -Roles &quot;<em>Mail Recipients</em>&quot;, &quot;<em>Mail Recipient Creation</em>&quot;, &quot;<em>Mailbox Import Export</em>&quot;, -CustomRecipientWriteScope &quot;<em>Seattle Users</em>&quot;</p></td>
<td><p>Este comando cria uma novo escopo de gerenciamento e grupo de funções de gerenciamento para habilitar membros do grupo de funções para gerenciar destinatários em Seattle.</p>
<p>Primeiro, o escopo de gerenciamento <em>Usuários de Seattle</em> é criado, que corresponde somente a destinatários que têm o atributo <em>Seattle</em> na <em>Cidade</em> em seus objetos de usuário.</p>
<p>Então, um novo grupo de funções chamado <em>Seattle Admins</em> é criado e as funções <em>Mail Recipients</em>, <em>Mail Recipient Creation</em> e <em>Importar Exportar Caixa de Correio</em> são atribuídas. O grupo de funções é estendido de forma que seus membros possam gerenciar somente usuários que correspondam ao escopo de filtro de destinatário <em>Usuários de Seattle</em>.</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Vancouver Servers</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Server Management</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Vancouver Server Management</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Vancouver Servers</em>&quot;</p></td>
<td><p>Este comando cria um novo escopo de gerenciamento e copia um grupo de gerenciamento existente para habilitar os membros do novo grupo de funções para gerenciar somente servidores no site Active Directory Vancouver.</p>
<p>Primeiro, o escopo de gerenciamento <em>Servidores de Vancouver</em> é criado, o qual corresponde somente a servidores localizados no site do Active Directory <em>Vancouver</em>. O site Active Directory está armazenado no atributo <em>ServerSite</em> nos objetos do servidor.</p>
<p>Então, um novo grupo de funções chamado <em>Gerenciamento de Servidor Vancouver</em> é criado que é uma cópia do grupo de funções <em>Gerenciamento do Servidor</em>. Este novo grupo de funções, entretanto, é estendido para permitir de todos os seus membros gerenciem somente servidores que correspondam ao filtro de configuração<em>Servidores de Vancouver</em>.</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Organization Management</em>&quot; -Member <em>davids</em></p></td>
<td><p>Este comando adiciona o usuário <em>davids</em> ao grupo de funções <em>Gerenciamento de Organização</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -RoleAssignee &quot;<em>Seattle Admins</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>Este comando remove a função <em>Criação de Destinatário de Email</em> do grupo de funções <em>Seattle Admins</em>. Este comando é útil porque não é necessário saber o nome da atribuição de função de gerenciamento que atribui a função ao grupo de funções.</p></td>
</tr>
</tbody>
</table>


## Shell Remota


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>Esses comandos abrem uma nova sessão shell remota entre um computador de domínio unido local e um servidor Exchange 2013 com o FQDN <em>ExServer.contoso.com</em>. Utilize esse comando se desejar administrar um servidor Exchange 2013 remoto e somente ter o Windows Management Framework, que inclui a interface de linha de comando Windows PowerShell, instalada em seu computador local. Esse comando utiliza suas credenciais de login atuais para autenticar contra o servidor Exchange 2013 remoto.</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>Esses comandos abrem uma nova sessão shell remota entre um computador de domínio unido local e um servidor Exchange 2013 com o FQDN <em>ExServer.contoso.com</em>. Utilize esse comando se desejar adminstrar um servidor Exchange 2013 remoto e somente ter o Windows Management Framework, que inclui a interface de linha de comando Windows PowerShell, instalada em seu computador local. Esse comando utiliza suas credenciais de login atuais para autenticar contra o servidor Exchange 2013 remoto.</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>Esse comando fecha a sessão shell remota entre um computador local e o servidor Exchange 2013 remoto.</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>Esse comando exibe um exemplo da sintaxe, mostrado em itálico, requerido para importar um arquivo em um servidor Exchange 2013 remoto utilizando o parâmetro FileData em um cmdlet. A sintaxe encapsula os dados contidos no arquivo <em>M:\AudioFiles\TonySmith.wma</em> e flui os dados para a propriedade FileData no cmdlet Import-RecipientDataProperty.</p>
<p>O parâmetro FileData aceita dados de um arquivo no computador local utilizando essa sintaxe na maioria dos cmdlets.</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>Este comando exibe um exemplo da sintaxe, mostrada em itálico, requerida para exportar um arquivo de um servidor Exchange 2013 remoto. A sintaxe encapsula os dados armazenados na propriedade FileData no objeto retornado pelo cmdlet, e então, flui os dados ao computador local. Em seguida, os dados são armazenados no arquivo <em>C:\tonysmith.wma</em> file.</p>
<p>A maioria dos cmdlets que tem como saída objetos com uma propriedade FileData utiliza essa sintaxe para exportar dados para um arquivo no computador local.</p></td>
</tr>
</tbody>
</table>

