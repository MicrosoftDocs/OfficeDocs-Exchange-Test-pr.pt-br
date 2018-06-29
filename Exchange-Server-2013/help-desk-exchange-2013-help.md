---
title: 'Suporte Técnico: Exchange 2013 Help'
TOCTitle: Suporte Técnico
ms:assetid: e7958752-22e4-4155-a2fc-948099dec6f7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876949(v=EXCHG.150)
ms:contentKeyID: 50486871
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suporte Técnico

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O técnico O grupo de função de gerenciamento é um dos vários grupos de função internos que constituem o modelo de permissões RBAC (controle de acesso baseado na função) no Microsoft Exchange Server 2013. Aos grupos de funções são atribuídas uma ou mais funções de gerenciamento que contêm as permissões necessárias para executar um determinado conjunto de tarefas. Os membros de um grupo de função recebem acesso para as funções de gerenciamento atribuídas ao respectivo grupo. Para saber mais sobre grupos de função, confira o artigo [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

Usuários que sejam membros do grupo de função Suporte Técnico podem realizar gerenciamento de destinatário limitado nos destinatários do Exchange 2013.

Por padrão, o grupo de funções Suporte Técnico permite que o membros exibam e modifiquem as opções do Outlook Web App de qualquer usuário na organização. Essas opções podem incluir a modificação do nome de exibição do usuário, endereço, número de telefone, etc. Elas não incluem opções disponíveis nas opções do Outlook Web App, como a modificação do tamanho de uma caixa de correio ou a configuração do banco de dados de caixa de correio no qual a caixa de correio está localizada.

Os membros desse grupo de funções pode somente modificar as mesmas opções do Outlook Web App que o usuário pode modificar. Isso significa que, se um usuário pode modificar seu nome de exibição, um membro do grupo de funções Suporte Técnico também pode modificar o nome de exibição daquele usuário. Entretanto, se um usuário não pode modificar seu nome de exibição, um membro do grupo de funções Suporte Técnico não pode modificar o nome de exibição daquele usuário.


> [!WARNING]
> As limitações na qual Outlook Web App opções que um membro do grupo de função Help Desk pode modificar são impostas pelo Exchange Centro de administração (EAC). Se um membro do grupo de função Help Desk tem acesso ao Exchange Shell de gerenciamento, poderá modificar qualquer opção Outlook Web App para qualquer usuário. Considere cuidadosamente quem você tornar um membro do grupo de função Help Desk e se eles devem também ser oferecidos acesso para o Shell.



O grupo de funções Suporte Técnico não permite qualquer outra tarefa porque há muito tipos diferentes de organização. Em vez disso, você pode adicionar funções de gerenciamento a esse grupo de funções para criar um grupo de funções Suporte Técnico que satisfaça as necessidade de sua organização. Por exemplo, if desejar que membros do grupo de funções Suporte Técnico sejam capazes de gerenciar caixas de correio, contatos de email, usuários habilidados para email, atribua a função de gerenciamento Destinatários de Email a este grupo de funções. Para obter mais informações sobre como adicionar funções de gerenciamento a esse grupo de funções, consulte a seção "Personalização de Grupo de Função" posteriormente neste tópico.

Para obter mais informações sobre o RBAC, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## Associação de grupo de função

Se você quiser adicionar ou remover membros desse grupo de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

Por padrão, somente membros do grupo de funções de Gerenciamento de Organização podem adicionar ou remover membros desse grupo de funções. Para saber mais sobre como adicionar representantes de grupos de funções adicionais, confira a seção "Adicionar ou remover um representante do grupo de funções" em [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Você pode usar o comando a seguir para exibir uma lista de usuários ou USGs (Grupos de Segurança Universal) que sejam membros deste grupo de função.

    Get-RoleGroupMember "Help Desk"

Para mais informações sobre os membros de um grupo de função, consulte [View the members of a role group](manage-role-group-members-exchange-2013-help.md) em [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

## Personalização de grupo de função

Por padrão, funções de gerenciamento são atribuídas a esse grupo de funções. As funções incluídas são listadas na seção "Funções de Gerenciamento Atribuídas a este Grupo de Funções". Você pode adicionar ou remover as atribuições de funções para ou de esse grupo de funções, de acordo com as necessidades da sua organização.

Os grupos de funções fornecidos com o Exchange 2013 são projetados para corresponder às tarefas mais granulares. Atribuindo funções a um grupo de funções, você habilita os membros desse grupo de funções a executar as tarefas associadas à função. Por exemplo, a função Registro no Diário habilita o gerenciamento do agente e das regras de Registro no Diário. Para mais informações sobre como as funções são atribuídas a grupos de funções, confira [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

As funções atribuídas a esse grupo de funções recebem escopos de gerenciamento padrão. Os escopos de gerenciamento determinam que objetos do Exchange podem ser exibidos ou modificados pelos membros de um grupo de funções. Você pode alterar os escopos associados com atribuições entre funções e grupos de funções. Por exemplo, você pode querer fazer isso se desejar que somente membros de um grupo de funções possam alterar destinatários que estejam em uma unidade organizacional específica ou em um local específico. Para mais informações sobre escopos de gerenciamento, confira [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Para mais informações sobre como personalizar esse grupo de funções, confira os seguintes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md)

Se desejar criar um grupo de funções e designar algumas funções atribuídas a este grupo de funções para o novo grupo de funções, consulte a seção "Criar um Grupo de Funções" em [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

## Funções de Gerenciamento atribuídas a este grupo de função

A tabela a seguir lista todas as funções de gerenciamento que são atribuídas a este grupo de funções e os seguintes atributos de cada atribuição de função:

  - **Atribuição regular**   Habilita os membros do grupo de funções a acessar as entradas de função de gerenciamento disponibilizadas pela função de gerenciamento associada.

  - **Atribuição de delegação**   Habilita os membros do grupo de função a atribuir a função especificada a outros grupos de funções, diretivas de atribuição de função, usuários ou USGs.

  - **Escopo de leitura do destinatário**   Determina quais membros dos objetos de destinatários do grupo de funções tem permissão para ler do Active Directory.

  - **Escopo de gravação do destinatário**   Determina quais membros dos objetos de destinatários do grupo de funções tem permissão para fazer modificações no Active Directory.

  - **Escopo de leitura da configuração**   Determina quais configurações e membros dos objetos de destinatários do grupo de funções tem permissão para ler do Active Directory.

  - **Escopo de gravação da configuração**   Determina quais membros dos objetos de destinatários e organizacionais do grupo de funções tem permissão para fazer modificações no Active Directory.

Para mais informações sobre atribuições de função e escopos de gerenciamento, consulte os seguintes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

### Funções de Gerenciamento atribuídas a este grupo de função

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Função de gerenciamento</th>
<th>Atribuição comum</th>
<th>Atribuição de delegação</th>
<th>Escopo de leitura do destinatário</th>
<th>Escopo de gravação do destinatário</th>
<th>Escopo de leitura da configuração</th>
<th>Escopo de gravação do destinatário</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="user-options-role-exchange-2013-help.md">Função de opções do usuário</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Função destinatários de somente leitura</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>

