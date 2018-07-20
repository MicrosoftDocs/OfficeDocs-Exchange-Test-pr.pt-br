---
title: 'Controlar a distribuição automática de caixa de correio usando escopos de banco de dados: Exchange 2013 Help'
TOCTitle: Controlar a distribuição automática de caixa de correio usando escopos de banco de dados
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 50486104
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Controlar a distribuição automática de caixa de correio usando escopos de banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

A distribuição de caixa de correio automática é um recurso do Microsoft Exchange Server 2013 que aleatoriamente seleciona um banco de dados de caixa de correio para armazenar uma caixa de correio nova ou movia quando você não especifica um banco de dados explicitamente. Esse recurso pode ser útil quando você quer permitir que administradores juniores ou a equipe de suporte técnico para criar caixas de correio sem precisar saber quais bancos de dados de caixa de correio devem ser criados.

Você pode usar escopos de gerenciamento de banco de dados para controlar quais bancos de dados de caixa de correio podem ser selecionados pela distribuição de caixa de correio automática. Quando você aplica escopos de banco de dados a um administrador, somente os bancos de dados que correspondem ao escopo do banco de dados definido ficam disponíveis ao administrador. Como a distribuição de caixa de correio automática usa o contexto do usuário atual, ela fica restrita pelos escopos de banco de dados aplicados ao administrador.

Para mais informações sobre distribuição de caixa de correio automática, escopos de banco de dados e atribuições de funções, consulte os seguintes tópicos:

  - [Distribuição de caixa de correio automática](automatic-mailbox-distribution-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas a escopos? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão do procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Escopos de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar um escopo de banco de dados

Nessa etapa, decida quais bancos de dados deseja incluir no escopo de banco de dados. Além disso, decida se deseja especificar uma lista estática de bancos de dados ou se deseja criar um filtro de banco de dados que inclua somente os bancos de dados que correspondem aos critérios especificados.


> [!IMPORTANT]
> Atribuições de função associadas com os escopos de banco de dados são aplicadas somente a usuários que se conectam a servidores que executam o Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior ou Exchange 2013. Se um usuário atribuído a uma atribuição de função associada a um escopo de banco de dados se conecta a um servidor de pré-Exchange 2010 SP1, a atribuição de função não será aplicada ao usuário e o usuário não receber permissões qualquer fornecidos pela atribuição de função.



## Usar um escopo de lista de banco de dados

Use uma lista de banco de dados se quiser definir uma lista estática de bancos de dados de caixa de correio que não devem ser incluídos nesse escopo. Use a seguinte sintaxe para criar um escopo de lista de bancos de dados.

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

Esse exemplo cria um escopo que se aplica somente aos bancos de dados Banco de Dados 1, Banco de Dados 2 e Banco de Dados 3.

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Usar um escopo de filtro de banco de dados

Use um filtro de banco de dados se quiser criar um escopo de banco de dados dinâmico que tenha somente os bancos de dados correspondentes aos critérios especificados. Isso poderá ser útil se você não quiser gerenciar o escopo de banco de dados após ele ter sido criado e você ter definido os valores padrão para a sua organização que podem identificar conjuntos específicos de bancos de dados de caixa de correio.

Para uma lista das propriedades de banco de dados filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

Use a seguinte sintaxe para criar um escopo de filtro de bancos de dados.

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

Este exemplo cria um escopo que inclui todos os bancos de dados que contêm a cadeia de caracteres "ACCT" na propriedade **Name** do banco de dados.

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Etapa 2: Adicionar o escopo de banco de dados a uma atribuição de função de gerenciamento

Depois de criar o escopo, você deve adicioná-lo a uma nova função de gerenciamento existente. Recomendamos usar os grupos de função de gerenciamento para controlar permissões administrativas, para que os exemplos nessa etapa usem um grupo de funções de exemplo chamado Administradores de Contabilidade. Para obter mais informações sobre como criar um grupo de funções, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Após você atribuir a função a um grupo de funções com o escopo de banco de dados, os membros do grupo de funções só poderão criar caixas de correio nos bancos de dados e mover caixas de correio para os bancos de dados incluídos no escopo.

Para uma lista de funções internas que você pode atribuir a grupos de funções, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).

## Adicionar uma nova atribuição de função

Use esse procedimento se tiver criado um grupo de funções e precisar adicionar funções a ele.

Use a seguinte sintaxe para criar uma atribuição de função entre a função de gerenciamento que deseja atribuir e o novo grupo de funções, com o novo escopo de banco de dados.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

Esse exemplo cria uma atribuição de função entre as funções de Destinatários de Email e Criação de Destinatário de Email e o grupo de funções Administradores de Contabilidade, usando o escopo de banco de dados Bancos de Dados de Contabilidade.

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Modificar uma atribuição existente

Use esse procedimento se você tiver um grupo de funções existente que já tenha atribuições de função entre ele e as funções que deseja aplicar ao novo escopo de banco de dados.

Esse procedimento usa canalização. Para mais informações, consulte [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\)).

Use a seguinte sintaxe para modificar uma atribuição de função entre a função de gerenciamento que deseja aplicar ao escopo de banco de dados e um grupo de funções existentes.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

Esse exemplo adiciona o escopo de banco de dados Bancos de Dados de Contabilidade às funções de Destinatários de Email e Criação de Destinatário de Email atribuídas ao grupo de funções Administradores de Contabilidade.

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)) ou [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Etapa 3: Adicionar membros a um grupo de funções (se aplicável)

Se quiser adicionar membros a um grupo de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).


> [!IMPORTANT]
> Se você adicionar membros a esse grupo de funções para restringir quais usuários eles podem criar nas caixas de correio ou mover para as caixas de correio, verifique se eles não são membros de outros grupos de funções que poderão conceder permissões extras.



## Etapa 4: Remover membros de um grupo de funções (se aplicável)

Se tiver adicionado membros a um novo grupo de funções que restringe em quais bancos de dados eles podem criar caixa de correio ou mover caixas de correio, e esses membros forem de outro grupo de funções com permissões adicionais, remova-os do grupo de funções antigo. Para mais informações, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

