---
title: 'Alterar uma atribuição de função: Exchange 2013 Help'
TOCTitle: Alterar uma atribuição de função
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 50485033
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar uma atribuição de função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

As atribuições de função de gerenciamento atribuem uma função de gerenciamento a um destinatário de função. Alterando a atribuição de função, é possível controlar quais objetos os destinatários de função com uma função atribuída podem alterar. Os escopos de função de gerenciamento aplicados a atribuições de função substituem o escopo de gravação implícito da função. Entretanto, o escopo de leitura implícito da função ainda se aplica. Os escopos que você aplica não podem retornar objetos externos ao escopo de leitura implícito da função.

Para mais informações sobre os escopos e as atribuições de função de gerenciamento no Microsoft Exchange Server 2013, consulte estes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas a atribuições de função? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atribuições de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar uma atribuição de função

As atribuições de função são habilitadas por padrão, o que significa que a função associada é aplicada ao destinatário de função para o qual a função é atribuída. Se a atribuição de função estiver desabilitada, a função associada não será aplicada ao destinatário de função.

Para habilitar uma atribuição de função, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <role assignment> -Enabled $true

Para desabilitar uma atribuição de função, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <role assignment> -Enabled $false

Este exemplo desabilita a atribuição de função Atribuição de Suporte Técnico.

    Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Usar o Shell para alterar uma função de gerenciamento ou destinatário de função em uma atribuição de função

Não é possível alterar a função de gerenciamento ou destinatário de função especificado em uma atribuição de função. Se você quiser que uma atribuição de função seja associada a outra função ou destinatário de função, crie uma nova atribuição de função e exclua a atribuição de função antiga. Para mais informações sobre como adicionar e remover atribuições de função, consulte os tópicos a seguir:

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

Se você criou atribuições diretamente para um usuário ou USG (grupo de segurança universal), recomendamos que considere usar os grupos de função de gerenciamento e as diretivas de atribuição de função de gerenciamento. Os grupos de função e diretivas de atribuição permitem a você simplificar seu modelo de permissões e reduzir o número de atribuições de função que você precisa gerenciar. Para mais informações, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## Usar o Shell para alterar um escopo relativo predefinido em uma atribuição de função

Você pode alterar ou adicionar um escopo relativo predefinido em uma atribuição de função. Se você adicionar ou alterar um escopo predefinido, quaisquer escopos de destinatários especificados anteriormente serão removidos da atribuição de função. Para uma lista de escopos predefinidos e suas descrições, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Para alterar ou adicionar um escopo predefinido em uma atribuição de função, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

Este exemplo altera o escopo predefinido na atribuição de função Atribuição de John para MyDistributionGroups.

    Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Usar o Shell para alterar um escopo de filtro de destinatário em uma atribuição de função

Você pode especificar um novo escopo baseado no filtro de destinatário ou alterar o escopo baseado no filtro de destinatário que já está aplicado à atribuição de função. Se você adicionar um escopo de destinatário, quaisquer escopos de destinatários definidos anteriormente serão removidos da atribuição de função.

Para especificar um novo escopo baseado no filtro de destinatário ou substituir um que já exista, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>

Este exemplo adiciona ou altera o escopo baseado no filtro de destinatário para Destinatários de Redmond.

    Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"

Se você quiser manter o mesmo escopo baseado no filtro de destinatário que está aplicado à atribuição de função mas alterar o filtro de destinatário usado para correspondência dos objetos de destinatário, será preciso alterar o filtro de destinatário no próprio escopo. Para mais informações sobre como alterar os escopos, consulte [Alterar um escopo de função](change-a-role-scope-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Usar o Shell para alterar o escopo do filtro de servidor ou de configuração baseada em lista em uma atribuição de função

Você pode especificar um novo escopo de filtro de servidor ou de configuração baseada em lista, ou alterar o escopo que já está aplicado à atribuição de função. Se você adicionar ou alterar o escopo de configuração, quaisquer escopos de configuração especificados anteriormente serão removidos da atribuição de função.

Para especificar um novo escopo de configuração ou substituir um que já exista, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

Este exemplo adiciona ou altera o escopo de configuração para Servidores de Redmond.

    Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"

Se você quiser manter o mesmo escopo de configuração que está aplicado à atribuição de função mas alterar o filtro de servidor ou lista de servidor no escopo, será preciso alterar o próprio escopo de configuração. Para mais informações sobre como alterar os escopos, consulte [Alterar um escopo de função](change-a-role-scope-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Usar o Shell para alterar o escopo de filtro de banco de dados ou de configuração baseada em lista em uma atribuição de função

Você pode tanto especificar um novo escopo de filtro de banco de dados ou de configuração baseada em lista quanto alterar o escopo que já está aplicado à atribuição de função. Se você adicionar ou alterar o escopo de configuração, quaisquer escopos de configuração especificados anteriormente serão removidos da atribuição de função.

Para especificar um novo escopo de configuração ou substituir um que já exista, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

Este exemplo adiciona ou altera o escopo da configuração nos Bancos de dados de Redmond.

    Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"

Se você quiser manter o mesmo escopo de configuração que está aplicado à atribuição de função, mas quiser alterar o filtro de banco de dados ou a lista de banco de dados no escopo, será preciso alterar o próprio escopo de configuração. Para mais informações sobre como alterar os escopos, consulte [Alterar um escopo de função](change-a-role-scope-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Usar o Shell para alterar a unidade organizacional em uma atribuição de função

Você pode adicionar uma nova OU ou alterar uma OU que já esteja aplicada à atribuição de função. Se você especificar uma nova OU, quaisquer escopos de destinatários especificados anteriormente serão removidos da atribuição de função.

Para alterar ou adicionar uma nova OU em uma atribuição de função, use a sintaxe a seguir.

    Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>

Este exemplo adiciona a OU Engenharia\\Usuários no domínio contoso.com à atribuição de função Suporte Técnico de Engenharia.

    Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Usar o Shell para alterar um escopo de configuração ou de destinatário exclusivo

Para alterar os escopos de destinatário exclusivo ou de configuração exclusiva, é possível usar os procedimentos fornecidos nas seções "Usar o Shell para alterar um escopo de filtro de destinatário em uma atribuição de função", "Usar o Shell para alterar o escopo de filtro de servidor ou de configuração baseada em lista em uma atribuição de função" e " Usar o Shell para alterar o escopo de filtro de banco de dados ou de configuração baseada em lista em uma atribuição de função" anteriormente neste tópico. A única diferença é que ao alterar um escopo exclusivo, é preciso especificar os parâmetros exclusivos a seguir, dependendo do fato de estar alterando um escopo de destinatário exclusivo ou um escopo de configuração exclusivo:

  - **Escopos de destinatário exclusivos**   Use o parâmetro *ExclusiveRecipientWriteScope* em vez do parâmetro *CustomRecipientWriteScope*.

  - **Escopos de configuração de banco de dados e de servidor exclusivos**   Use o parâmetro *ExclusiveConfigWriteScope* em vez do parâmetro *CustomConfigWriteScope*.

Como acontece com escopos de configuração e de destinatário regulares, se você adicionar ou alterar o escopo exclusivo, quaisquer escopos de destinatário ou de configuração definidos anteriormente serão substituídos.

Este exemplo altera um escopo de gravação de destinatário exclusivo.

    Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

