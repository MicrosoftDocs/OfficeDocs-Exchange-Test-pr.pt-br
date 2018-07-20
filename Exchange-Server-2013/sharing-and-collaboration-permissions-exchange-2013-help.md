---
title: 'Permissões de compartilhamento e colaboração: Exchange 2013 Help'
TOCTitle: Permissões de compartilhamento e colaboração
ms:assetid: b7fa4b7c-1266-45bd-a14b-f66be0459cc5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150556(v=EXCHG.150)
ms:contentKeyID: 50486471
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de compartilhamento e colaboração

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

As permissões necessárias para configurar os recursos de compartilhamento e colaboração variam dependendo o procedimento que está sendo executado ou o cmdlet que você deseja executar. Para obter mais informações sobre o compartilhamento e colaboração, consulte [Colaboração](collaboration-exchange-2013-help.md) e [Compartilhamento](sharing-exchange-2013-help.md).

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!TIP]
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).

## Permissões de recurso de compartilhamento e colaboração

Você pode usar os recursos na tabela a seguir para configurar os recursos de compartilhamento e colaboração. Os grupos de função que são necessárias para configurar cada recurso são listados.

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
<td><p>Aplicativos de parceiros - configurar</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Pastas públicas, habilitadas para email</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Pastas públicas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="public-folder-management-exchange-2013-help.md">Gerenciamento de Pasta Pública</a></p></td>
</tr>
<tr class="even">
<td><p>Caixas de correio de site</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Política de provisionamento de caixa de correio do site</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
</tbody>
</table>

