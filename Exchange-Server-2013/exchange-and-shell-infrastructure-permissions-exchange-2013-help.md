---
title: 'Permissões de infraestrutura do Exchange e do Shell: Exchange 2013 Help'
TOCTitle: Permissões de infraestrutura do Exchange e do Shell
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 50485327
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de infraestrutura do Exchange e do Shell

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

As permissões exigidas para a realização de tarefas de configuração de vários componentes do Microsoft Exchange Server 2013 dependem do procedimento que está sendo realizado ou do cmdlet que você deseja executar. Consulte cada seção deste tópico para obter mais informações sobre os respectivos recursos.

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!NOTE]  
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]  
> Alguns recursos podem exigir que você tenha permissões de administrador local no servidor que você quer gerenciar. Para gerenciar esses recursos, você deve ser membro do grupo Administradores Locais no servidor.



## Permissões de infraestrutura do Exchange

A tabela a seguir lista as permissões exigidas para realizar tarefas que definem configurações gerais do Exchange 2013.

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões necessárias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Log de auditoria de administrador</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="even">
<td><p>Definições de configuração do Centro de Administração do Exchange</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectividade do Centro de Administração do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Definições de configuração de servidor do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações da Ajuda do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Categorias de mensagem</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Chave do produto (Product Key)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Testar a integridade do sistema</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro em log de auditoria do administrador somente leitura</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p>

> [!NOTE]  
> Você pode também atribuir manualmente a função de gerenciamento de logs de auditoria somente leitura a um grupo de funções de gerenciamento. Para mais informações, consulte <A href="view-only-audit-logs-role-exchange-2013-help.md">Função de Logs de auditoria somente para exibição</A>.


</td>
</tr>
<tr class="even">
<td><p>Gravar em log de auditoria</p></td>
<td><p>Os usuários que são membros de qualquer grupo de funções ou recebem qualquer função de gerenciamento pode gravar no log de auditoria do administrador.</p></td>
</tr>
</tbody>
</table>


## Permissões de infraestrutura do Shell

A tabela a seguir lista as permissões exigidas para realizar tarefas que configuram recursos que controlam a forma como o Shell de Gerenciamento do Exchange é executado.

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configurações de servidor dos Serviços de Domínio Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Agentes de extensão de cmdlet</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Diretórios virtuais do PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Instalação do WinRM e do PowerShell</p></td>
<td><p>Administrador de Servidor Local</p></td>
</tr>
<tr class="odd">
<td><p>Shell Remoto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


## Permissões de certificados e federação

A tabela a seguir lista as permissões necessárias para a realização de tarefas relacionadas às confianças de federação, à configuração OAuth, ao gerenciamento de certificados e à configuração de implantação híbrida.

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento de certificados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Confianças de federação, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Testar as confianças de federação, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuração de implantação híbrida</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectores dentro da organização</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
</tbody>
</table>

