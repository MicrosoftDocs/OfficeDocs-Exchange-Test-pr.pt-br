---
title: 'Alterar entrada de função de nível superior sem escopo: Exchange 2013 Help'
TOCTitle: Alterar uma entrada de função em uma função de nível superior sem escopo
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 50485860
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar uma entrada de função em uma função de nível superior sem escopo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

As entradas de função de gerenciamento em funções de gerenciamento de nível superior sem escopo se referem aos scripts e cmdlets não-Exchange e seus parâmetros que você pretende disponibilizar aos atribuídos à função. Ao alterar os parâmetros disponíveis em uma entrada de função, você controla qual dos atribuídos à função podem ser disponibilizados com o script ou o cmdlet não-Exchange. Para obter mais informações sobre entradas de função sem escopo, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> Se você quiser alterar uma entrada de função em uma função de gerenciamento que contenha cmdlets do Exchange, consulte <A href="change-a-role-entry-exchange-2013-help.md">Alterar uma entrada de função</A>.



Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - A capacidade de alterar uma entrada de função a uma função de nível superior sem escopo não está incluída em nenhum grupo de funções de gerenciamento por padrão. É preciso primeiro atribuir a função de Gerenciamento de Função sem Escopo a um usuário ou a um grupo de funções ou USG de que o usuário seja membro, antes de o usuário poder adicionar ou alterar uma entrada de função de nível superior sem escopo. Para mais informações sobre como adicionar uma função a um usuário, USG ou grupo de função, consulte os seguintes tópicos:
    
      - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)
    
      - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell Para adicionar um ou mais parâmetros a uma entrada de função

Para adicionar parâmetros a uma entrada de função de nível superior, é preciso proceder da seguinte forma:

  - Especifique os parâmetros que você deseja adicionar usando o parâmetro *Parameters*.

  - Especifique o parâmetro *AddParameter* para indicar que deseja executar uma operação de adição.

  - Especifique o parâmetro *UnscopedTopLevel* para indicar que você está alterando uma entrada de função em uma função de nível superior sem escopo. Se você não especificar esse parâmetro quando alterar uma entrada de função em uma função sem escopo, ocorre um erro.

Para adicionar parâmetros a uma entrada de função, use a sintaxe a seguir.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

Esse exemplo adiciona os parâmetros *EmailAddress* e *City* ao script **CreateUsers.ps1** na função sem escopo Administradores de Destinatários.

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Usar o Shell para remover um ou mais parâmetros de uma entrada de função

Para remover parâmetros de uma entrada de função, é necessário proceder da seguinte forma:

  - Especifique os parâmetros que você deseja remover usando o parâmetro *Parameters*.

  - Especifique o parâmetro *RemoveParameter* para indicar que deseja executar uma operação de remoção.

  - Especifique o parâmetro *UnscopedTopLevel* para indicar que você está alterando uma entrada de função em uma função de nível superior sem escopo. Se você não especificar esse parâmetro quando alterar uma entrada de função em uma função sem escopo, ocorre um erro.


> [!CAUTION]
> As operações de remoção não podem ser desfeitas. Se você tiver removido por engano um parâmetro de uma entrada de função, será preciso adicioná-lo manualmente outra vez.



Para remover parâmetros de uma entrada de função, use a sintaxe a seguir.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

Esse exemplo remove os parâmetros *Delay*, *Force* e *Credential* do cmdlet **Start-Widget** não-Exchange na função Administradores de Servidor de Camada 1.

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Usar o Shell para remover todos os parâmetros de uma entrada de função

Para remover todos os parâmetros de uma entrada de função, é necessário proceder da seguinte forma:

  - Especifique o valor `$Null` no parâmetro *Parameters*. Você não precisa incluir o parâmetro *RemoveParameter*.

  - Especifique o parâmetro *UnscopedTopLevel* para indicar que você está alterando uma entrada de função em uma função de nível superior sem escopo. Se você não especificar esse parâmetro quando alterar uma entrada de função em uma função sem escopo, ocorre um erro.

A remoção de todos os parâmetros de uma entrada de função é mais útil quando se quer disponibilizar apenas alguns parâmetros em um script ou cmdlet não-Exchange e excluir todos os outros parâmetros.

Se não quiser que a função tenha acesso a um script ou cmdlet não-Exchange, remova a entrada de função associada da função por completo em vez de apenas remover os parâmetros. Para mais informações sobre como remover uma entrada de função de uma função, consulte [Remover uma entrada de função de uma função](remove-a-role-entry-from-a-role-exchange-2013-help.md).


> [!CAUTION]
> As operações de remoção não podem ser desfeitas. Se você removeu por engano todos os parâmetros de uma entrada de função, será preciso adicioná-los manualmente outra vez.



Para remover todos os parâmetros de uma entrada de função, use a sintaxe a seguir.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

Esse exemplo remove todos os parâmetros do script FindMailboxesOverQuota.ps1 na função Administradores de Destinatários.

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Usar o Shell para aplicar um conjunto específico de parâmetros

Se quiser incluir apenas um conjunto específico de parâmetros a uma entrada de função, será necessário proceder da seguinte forma:

  - Especifique somente o parâmetro *Parameters*. Não inclua os parâmetros *AddParameter* ou *RemoveParameter*.

  - Especifique o parâmetro *UnscopedTopLevel* para indicar que você está alterando uma entrada de função em uma função sem escopo. Se você não especificar esse parâmetro quando alterar uma entrada de função em uma função de nível superior sem escopo, ocorrerá um erro.


> [!CAUTION]
> Ao especificar apenas o parâmetro <EM>Parameters</EM>, só os parâmetros que você especificar no comando serão incluídos na entrada de função. Todos os outros parâmetros são removidos.



Para especificar um conjunto específico de parâmetros, use a sintaxe a seguir.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

Esse exemplo inclui apenas os parâmetros *Alias*, *DisplayName*, *WidgetConfig* e *Enabled* no cmdlet **Set-Widget** na função Administradores de Destinatários do Email de Seattle.

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Outras tarefas

Após alterar uma entrada de função ou uma função de nível superior sem escopo, você poderá também:

[Adicionar uma entrada de função a uma função](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

[Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md)

[Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

