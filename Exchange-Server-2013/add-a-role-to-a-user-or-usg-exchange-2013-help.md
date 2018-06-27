---
title: 'Adicionar uma função a um usuário ou USG: Exchange 2013 Help'
TOCTitle: Adicionar uma função a um usuário ou USG
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 50486387
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar uma função a um usuário ou USG

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-03_

Atribuições de função de gerenciamento podem atribuir uma função de gerenciamento a um usuário ou grupo de segurança universal (USG). Atribuindo uma função a um usuário ou USG, habilitar esses usuários executar tarefas dependentes de cmdlets ou scripts e seus parâmetros definidos na função de gerenciamento.

Se você deseja atribuir funções a um grupo de funções de gerenciamento ou uma diretiva de atribuição de função de gerenciamento, consulte os seguintes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)

Se você deseja adicionar membros a um grupo de funções ou atribuir uma política de atribuição de função a um usuário final, consulte os seguintes tópicos:

  - [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md)

  - [Alterar a política de atribuição de uma caixa de correio](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

Para obter mais informações, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atribuições de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Embora você possa atribuir funções diretamente a usuários e USGs, o método recomendado de concedendo permissões a administradores e usuários finais é usar grupos de função de gerenciamento e políticas de atribuição de função de gerenciamento. Ao usar grupos de função e políticas de atribuição, você pode simplificar o modelo de permissões.

  - Atribuições de função são aditivas. Isso significa que todas as funções são somadas quando eles sejam avaliados. Se duas funções são atribuídas a um usuário e uma função contém um cmdlet, mas o outro não, o cmdlet ainda estarão disponível para o usuário.
    
    Por padrão, as atribuições de função não concedem a capacidade de atribuir funções para outros usuários. Para habilitar um usuário atribuir funções a outros usuários ou USGs, consulte [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).

  - Se você criar uma atribuição com um escopo, o escopo substitui o escopo de gravação implícita da função. No entanto, o escopo de leitura implícita da função ainda se aplica. O novo escopo não pode retornar objetos fora do escopo de leitura implícita da função. Para obter mais informações, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

  - Todos os procedimentos neste tópico usam o parâmetro *SecurityGroup* para atribuir funções a um USG. Se você deseja atribuir a função a um usuário específico, use o parâmetro *User* em vez do parâmetro *SecurityGroup* . Todos os outro sintaxe para cada comando é o mesmo.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma atribuição de função com nenhum escopo

Você pode criar uma atribuição de função com nenhum escopo. Quando você fizer isso, o implícita leitura e gravação implícita escopos da função se aplicam.

Use a seguinte sintaxe para atribuir uma função a um USG sem qualquer escopo.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

Este exemplo atribui a função de servidores do Exchange para o USG SeattleAdmins.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Criar uma atribuição de função com um escopo relativo predefinido

Se um escopo relativo predefinido atende aos seus requisitos de negócios, você pode aplicar esse escopo à atribuição de função em vez de criar um escopo personalizado. Para obter uma lista de escopos predefinidos e suas descrições, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Use a seguinte sintaxe para atribuir uma função a um USG com um escopo predefinido.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

Este exemplo atribui a função de servidores do Exchange para o USG SeattleAdmins e aplica o escopo da organização predefinido.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Criar uma atribuição de função com um escopo de baseado em filtro de destinatário

Se você criou um escopo de baseado em filtro de destinatário e deseja usá-la com uma atribuição de função, você precisará incluir o escopo no comando utilizado para atribuir a função a um USG usando o parâmetro *CustomRecipientWriteScope* . Se você usar o parâmetro *CustomRecipientWriteScope* , você não pode usar o parâmetro *RecipientOrganizationalUnitScope* .

Antes de adicionar um escopo para uma atribuição de função, você precisará criar um. Para obter mais informações, consulte [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Use a seguinte sintaxe para atribuir uma função a um USG com um escopo de baseado em filtro de destinatário.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

Este exemplo atribui a função destinatários de email para o USG de administradores do destinatário Seattle e aplica o escopo de destinatários de Seattle.

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Criar uma atribuição de função com um filtro de servidor ou banco de dados ou o escopo da configuração baseada em lista

Se você criou um filtro de servidor ou banco de dados ou o escopo da configuração baseada na lista e deseja usá-la com uma atribuição de função, você precisará incluir o escopo no comando utilizado para atribuir a função a um USG usando o parâmetro *CustomConfigWriteScope* .

Antes de adicionar um escopo para uma atribuição de função, você precisará criar um. Para obter mais informações, consulte [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Use a seguinte sintaxe para atribuir uma função a um USG com um escopo de configuração.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

Este exemplo atribui a função de servidores do Exchange para o USG MailboxAdmins e aplica o escopo de servidores de caixa de correio.

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

O exemplo anterior mostra como adicionar uma atribuição de função com um escopo de configuração do servidor. A sintaxe para adicionar um escopo de configuração do banco de dados é o mesmo. Você especificar o nome de um escopo de banco de dados, em vez de um escopo de servidor.

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Criar uma atribuição de função com um escopo de UO

Se desejar fazer o escopo de escopo de gravação da função a uma unidade organizacional (UO), você pode especificar a UO no parâmetro *RecipientOrganizationalUnitScope* diretamente. Se você usar o parâmetro *RecipientOrganizationalUnitScope* , você não pode usar o parâmetro *CustomRecipientWriteScope* .

Use a seguinte sintaxe para atribuir uma função a um USG e restringir o escopo de gravação de uma função como uma OU específica.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

Este exemplo atribui função destinatários de email para o USG SalesRecipientAdmins e escopos a atribuição a vendas/usuários OU no domínio contoso.com.

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Criar uma atribuição de função com um escopo de destinatário ou configuração exclusivo

Para criar uma atribuição de função exclusiva com um destinatário exclusivo ou o escopo da configuração, os mesmos procedimentos fornecidos nas seções a criar uma atribuição de função com um escopo de baseado em filtro de destinatário e criar uma atribuição de função com um filtro de servidor ou banco de dados ou o escopo da configuração baseada em lista podem ser usados. A única diferença é que, quando você cria uma atribuição de função com um escopo exclusivo, você deve especificar os seguintes parâmetros exclusivos, dependendo se você estiver usando um escopo de destinatário exclusivo ou um escopo exclusivo de configuração:

  - **Escopos de destinatário exclusivos**   Use o parâmetro *ExclusiveRecipientWriteScope* em vez do parâmetro *CustomRecipientWriteScope*.

  - **Escopos exclusivos de configuração**   Use o parâmetro *ExclusiveConfigWriteScope* em vez do parâmetro *CustomConfigWriteScope* .

Quando você executa esse procedimento, os destinatários da função a atribuídos à função podem executar ações contra os objetos incluídos no escopo exclusivo. Para obter mais informações sobre escopos exclusivos, consulte [Noções básicas sobre escopos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

É possível criar uma atribuição de função com escopos exclusivos e regulares.

Este exemplo atribui a função destinatários de email para o USG de administradores de usuário protegido e aplica o escopo exclusivo de usuários protegido.

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

