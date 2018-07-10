---
title: 'Remover uma função: Exchange 2013 Help'
TOCTitle: Remover uma função
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 50485256
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

As funções de gerenciamento que não forem mais necessárias podem ser removidas da sua organização. Você pode remover apenas as funções de gerenciamento que você criou. Funções de gerenciamento internas não podem ser removidas. Para mais informações sobre as funções de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para remover uma função de gerenciamento, é preciso remover todas as suas atribuições de função de gerenciamento. Para obter mais informações sobre como remover uma atribuição de função, consulte [Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Remover uma função de gerenciamento sem funções filhas

Para remover uma função sem funções filhas, use a sintaxe a seguir.

    Remove-ManagementRole <role name>

Este exemplo remove a função Administradores de Servidores de Seattle.

    Remove-ManagementRole "Seattle Server Administrators"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351170\(v=exchg.150\)).

## Remover uma função de gerenciamento com funções filhas

Se uma função que você deseja remover tiver funções filhas, será preciso remover as funções filhas também. Se tentar remover uma função que possua funções filhas você receberá uma mensagem de erro, a não ser que use a opção *Recurse*. Ao usar a opção *Recurse* para remover uma função, a função especificada e todas as suas funções filhas serão excluídas.


> [!WARNING]
> Ao usar a opção <EM>Recurse</EM>, todas as funções filhas da função especificada que você deseja remover também serão removidas. Certifique-se de quais funções serão apagadas antes de executar o comando.



Para garantir que você remova apenas as funções que deseja remover, use a opção *WhatIf* com seu comando para verificar se está tudo certo. Use a sintaxe a seguir.

    Remove-ManagementRole <role name> -Recurse -WhatIf

A opção *WhatIf* realiza o comando sem confirmar as alterações e relata quais funções teriam sido removidas. Para obter mais informações sobre a opção *WhatIf*, consulte [Comutadores WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

Depois de confirmar que apenas as funções que você deseja remover serão removidas, execute o mesmo comando sem a opção *WhatIf*. Este exemplo remove a função Administradores de Londres e todas as suas funções filhas.

    Remove-ManagementRole "London Administrators" -Recurse

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351170\(v=exchg.150\)).

## Remover uma função de gerenciamento sem escopo

Para remover uma função sem escopo, use os mesmos procedimentos em Remove a management role with no child roles e Remove a management role with child roles, anteriormente neste tópico. A única diferença é que, ao remover uma função sem escopo, é preciso especificar a opção *UnScopedTopLevel* ao executar o comando. Este exemplo remove uma função sem escopo e todas as suas funções filhas.

    Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel

Da mesma forma que com outras funções, use a opção *WhatIf* para verificar se você está removendo as funções corretas.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351170\(v=exchg.150\)).

