---
title: 'Adicionar uma entrada de função a uma função: Exchange 2013 Help'
TOCTitle: Adicionar uma entrada de função a uma função
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 50485270
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar uma entrada de função a uma função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-04_

Para conceder acesso a um cmdlet, é preciso adicionar a entrada de função de gerenciamento associada a uma função de gerenciamento. Depois de adicionar a entrada de função a uma função, os usuários aos quais a função for atribuída poderão acessar esse cmdlet. Para mais informações sobre as entradas de função de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Não é possível adicionar entradas de função para funções internas. Se você desejar personalizar funções, crie uma nova função. Para obter mais informações sobre como criar uma nova função, consulte [Criar uma função](create-a-role-exchange-2013-help.md).


> [!TIP]
> Este tópico não discute como adicionar entradas de função de gerenciamento sem escopo a uma função de gerenciamento sem escopo. Para obter mais informações sobre como adicionar entradas de função sem escopo, consulte <A href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">Adicionar uma entrada de função a uma função de nível superior sem escopo</A>.



Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Uma entrada de função que você deseje adicionar a uma função de gerenciamento precisa existir na função de gerenciamento pai imediata da função.

  - Este tópico faz uso de canalização. Para mais informações sobre pipeline, consulte [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Adicionar uma única entrada de função de uma função pai

Você pode adicionar uma entrada de função a uma função exatamente como ela aparece na função pai usando a sintaxe a seguir.

    Add-ManagementRoleEntry <child role name>\<cmdlet>

Este exemplo adiciona o cmdlet de **Set-Mailbox** à função de Administradores de Destinatários.

    Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"

Esse comando verifica a função pai, e se a entrada de função existir, é adicionada à função filha. Se a entrada de função já existir na função filha, você pode incluir o parâmetro *Overwrite* para substituir a entrada de função existente.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Add-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351236\(v=exchg.150\)).

## Adicionar uma única entrada de função de uma função pai e incluir apenas parâmetros específicos

Para adicionar uma entrada de função de uma função pai, porém incluindo apenas parâmetros específicos da entrada de função na função filha, use a sintaxe a seguir.

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

Este exemplo adiciona o cmdlet **Set-Mailbox** à função de Suporte Técnico, mas inclui apenas os parâmetros *DisplayName* e *EmailAddresses* na entrada da função filha.

    Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses

Esse comando verifica a função pai, e se a entrada de função existir, é adicionada à função filha. Se a entrada de função já existir na função filha, você pode incluir o parâmetro *Overwrite* para substituir a entrada de função existente.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Add-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351236\(v=exchg.150\)).

## Adicionar várias entradas de função de uma função de pai

Para adicionar mais de uma entrada de função a uma função, é preciso obter uma lista de entradas de função que existam na função pai que você deseja adicionar à função filha, para em seguida adicioná-las à função filha. Para isso, obtenha a lista de entradas de função em uma função pai usando o cmdlet **Get-ManagementRoleEntry**. Canalize a saída do cmdlet **Get-ManagementRoleEntry** para o cmdlet **Add-ManagementRoleEntry**. Para recuperar várias entradas de função, você precisa usar o caractere curinga (\*).

Para adicionar várias entradas de uma função de pai a uma função filha, use a sintaxe a seguir.

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

Este exemplo adiciona todas as entradas de função que contenham a cadeia de caracteres `Mailbox` no nome do cmdlet na função pai Destinatários de Email à função filha Destinatários de Email de Seattle.

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

Se as entradas de função já existirem na função filha, você pode incluir o parâmetro *Overwrite* para substituir as entradas de função existentes.

Para obter mais informações sobre como recuperar uma lista de entradas de função de gerenciamento, consulte [Exibir entradas de função](view-role-entries-exchange-2013-help.md).

Para obter a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)) e [Add-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351236\(v=exchg.150\)).

