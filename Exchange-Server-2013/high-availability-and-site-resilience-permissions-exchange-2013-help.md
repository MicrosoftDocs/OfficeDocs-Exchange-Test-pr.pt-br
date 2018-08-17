---
title: 'Permissões de resiliência de site e disponibilidade altas: Exchange 2013 Help'
TOCTitle: Permissões de resiliência de site e disponibilidade altas
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 50485861
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de resiliência de site e disponibilidade altas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-11-12_

As permissões exigidas para configurar alta disponibilidade variam dependendo do procedimento que está sendo executado ou do cmdlet que você deseja executar. Para obter mais informações sobre alta disponibilidade, consulte [Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md).

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!NOTE]
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).

## Permissões de grupo de disponibilidade de banco de dados

Você pode usar os recursos na tabela a seguir para adicionar, remover e configurar definições para grupos de disponibilidade do banco de dados (DAGs).

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
<td><p>Associação ao grupo de disponibilidade do banco de dados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Função de grupos de disponibilidade de banco de dados</a></p></td>
</tr>
<tr class="even">
<td><p>Propriedades do grupo de disponibilidade do banco de dados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Função de grupos de disponibilidade de banco de dados</a></p></td>
</tr>
<tr class="odd">
<td><p>Grupos de disponibilidade do banco de dados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Função de grupos de disponibilidade de banco de dados</a></p></td>
</tr>
<tr class="even">
<td><p>Redes de disponibilidade do banco de dados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Função de grupos de disponibilidade de banco de dados</a></p></td>
</tr>
</tbody>
</table>


## Permissões de cópia de banco de dados de caixa de correio

Você pode usar os recursos na tabela a seguir para adicionar, remover, configurar e ativar cópias de banco de dados de caixa de correio.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alternância de banco de dados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="databases-role-exchange-2013-help.md">Função de bancos de dados</a></p></td>
</tr>
<tr class="even">
<td><p>Cópias de banco de dados de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Função de cópias de banco de dados</a></p></td>
</tr>
<tr class="odd">
<td><p>Alternância de servidor</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="databases-role-exchange-2013-help.md">Função de bancos de dados</a></p></td>
</tr>
<tr class="even">
<td><p>Atualizar uma cópia de banco de dados de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Função de cópias de banco de dados</a></p></td>
</tr>
</tbody>
</table>

