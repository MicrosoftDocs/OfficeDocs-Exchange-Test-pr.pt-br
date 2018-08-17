---
title: 'Permissões de integridade e desempenho do servidor: Exchange 2013 Help'
TOCTitle: Permissões de integridade e desempenho do servidor
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 50484859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de integridade e desempenho do servidor

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

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



## Permissões de gerenciamento de carga de trabalho do Exchange

A tabela a seguir lista as permissões exigidas para realizar tarefas que gerenciam a integridade e o desempenho da sua organização Exchange 2013. Para obter mais informações, consulte [Gerenciamento de carga de trabalho do Exchange](exchange-workload-management-exchange-2013-help.md).

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
<td><p>Limitação de usuário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="even">
<td><p>Limitação de carga de trabalho do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
</tbody>
</table>


## Permissões de log de eventos do Exchange

A tabela a seguir lista as permissões necessárias para realizar tarefas de gerenciar configurações de log de eventos do Exchange.

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
<td><p>Gerenciamento de log de eventos do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
</tbody>
</table>

