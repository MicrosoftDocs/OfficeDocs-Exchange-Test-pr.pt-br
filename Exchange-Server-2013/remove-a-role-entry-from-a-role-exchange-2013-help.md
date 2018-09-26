---
title: 'Remover uma entrada de função de uma função: Exchange 2013 Help'
TOCTitle: Remover uma entrada de função de uma função
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 50485519
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma entrada de função de uma função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

As entradas de função de gerenciamento determinam os cmdlets e os parâmetros disponíveis em uma função de gerenciamento. Ao remover entradas ou parâmetros de função em uma entrada de função, você pode restringir o que os usuários com atribuição da função de gerenciamento podem executar. Para mais informações sobre as entradas de função de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Remover uma entrada de função única inteira de uma função

Ao remover uma entrada de função de uma função, você remove a capacidade de os usuários atribuídos àquela função acessarem o cmdlet our script associado.

Use a sintaxe a seguir para remover uma entrada completa de função de gerenciamento de uma função.

```powershell
Remove-ManagementRoleEntry <management role>\<management role entry>
```

Este exemplo remove o cmdlet **Enable-MailUser** da função Administradores do Servidor de Seattle.

```powershell
Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"
```

Para obter informações detalhadas de sintaxe e parâmetro, consulte [Remove-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351187\(v=exchg.150\)).

## Remover várias entradas inteiras de uma função

Ao remover várias entradas de uma função, você remove a capacidade de os usuários atribuídos àquela função acessarem cmdlets ou scripts associados.

Para remover várias entradas de função de uma função, é preciso recuperar a lista de entradas de função a serem removidas, usando o cmdlet **Get-ManagementRoleEntry**. Em seguida, você precisa canalizar a saída para o cmdlet **Remove-ManagementRoleEntry**. Você pode usar caracteres curinga com o cmdlet **Get-ManagementRoleEntry** para encontrar várias entradas de função. Convém usar a opção *WhatIf* para verificar se você está removendo as entradas de função corretas. Use a sintaxe a seguir.

```powershell
Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf
```

Esse exemplo remove todas as entradas de função que contiverem a palavra diário da função Administradores do Servidor de Seattle.

```powershell
Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf
```

Ao executar o comando com a opção *WhatIf*, o cmdlet retornará uma lista com todas as entradas de função que seriam removidas. Se a lista parecer correta, execute o comando novamente sem a opção *WhatIf* para remover as entradas de função.

```powershell
Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry
```

Para obter a sintaxe detalhada e informações sobre parâmetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)) e [Remove-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351187\(v=exchg.150\)).

## Remover parâmetros de uma entrada de função em uma função

Ao remover parâmetros de uma entrada de função em uma função, esses parâmetros não estarão mais disponíveis para usuário atribuídos à função.

Use a sintaxe a seguir para remover parâmetros de uma entrada de função.

```powershell
Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter
```

Este exemplo remove os parâmetros *MaxSafeSenders*, *MaxSendSize*, *SecondaryAddress* e *UseDatabaseQuotaDefaults* da entrada de função **Set-Mailbox** na função Administradores de Servidor de Seattle.

```powershell
Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter
```

Para obter informações detalhadas de sintaxe e parâmetro, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

