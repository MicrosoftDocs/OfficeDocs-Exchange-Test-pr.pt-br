---
title: 'Permissões de mensagens unificadas: Exchange 2013 Help'
TOCTitle: Permissões de mensagens unificadas
ms:assetid: d326c3bc-8f33-434a-bf02-a83cc26a5498
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638193(v=EXCHG.150)
ms:contentKeyID: 50486728
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de mensagens unificadas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

As permissões necessárias para executar tarefas em servidores de acesso para cliente que estiverem executando o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio que estão executando o Microsoft Exchange Unified Messaging service variam dependendo do procedimento que está sendo executado ou o cmdlet que você deseja executar.

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!TIP]
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).

## Permissões do componente de Unificação de mensagens

Você pode definir configurações para os recursos e componentes de Unificação de mensagens na tabela a seguir.

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
<td><p>atendedores automáticos do UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Regras de atendimento de chamada de Unificação de mensagens</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="odd">
<td><p>Dados de chamada de Unificação de mensagens e relatórios de resumo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Servidor de acesso para cliente (serviço de roteador de chamada de Unificação de mensagens)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="odd">
<td><p>Planos de discagem da UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Grupos de busca de Unificação de mensagens</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="odd">
<td><p>Gateways IP da UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>políticas de caixa de correio de UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="odd">
<td><p>Caixas de correio da UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Prompts de UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="odd">
<td><p>Servidor de caixa de correio (serviço de Unificação de mensagens)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
</tbody>
</table>

