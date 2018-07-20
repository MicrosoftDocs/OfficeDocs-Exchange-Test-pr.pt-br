---
title: 'Permissões de gerenciamento de função: Exchange 2013 Help'
TOCTitle: Permissões de gerenciamento de função
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 50486641
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de gerenciamento de função

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

As permissões necessárias para executar tarefas para configurar funções de gerenciamento variam dependendo o procedimento que está sendo executado ou o cmdlet que você deseja executar. Para obter mais informações sobre funções de gerenciamento, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!TIP]
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).

## Permissões de gerenciamento de função

Você pode usar os recursos na tabela a seguir para gerenciar os grupos de função de gerenciamento, funções, diretivas de atribuição, atribuições, escopos que definem as permissões que você pode aplicar a administradores e usuários finais. Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Funções de gerenciamento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Funções de gerenciamento sem escopo</p></td>
<td><p>função de gerenciamento de <a href="unscoped-role-management-role-exchange-2013-help.md">Função de gerenciamento de função sem escopo</a></p></td>
</tr>
<tr class="odd">
<td><p>Grupos de função</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Políticas de atribuição</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Atribuições de função</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Escopos de gerenciamento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Entradas de função de gerenciamento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Permissões herdadas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Active Directory dividir permissões</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>

> [!IMPORTANT]
> Para executar o comando <CODE>setup.exe</CODE> com os parâmetros <EM>PrepareAD</EM> e <EM>ActiveDirectorySplitPermissions</EM> , a conta utilizada deve ser um membro dos grupos de administradores de esquemas e administradores da empresa.


</td>
</tr>
</tbody>
</table>

