---
title: 'Remover uma função de um usuário ou USG: Exchange 2013 Help'
TOCTitle: Remover uma função de um usuário ou USG
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 50486864
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma função de um usuário ou USG

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-02_

Atribuições de função de gerenciamento atribuir uma função de gerenciamento a um usuário ou grupo de segurança universal (USG). Se você remover uma atribuição de função, os usuários atribuídos à função não terá mais acesso aos cmdlets disponíveis sobre essa função. Para obter mais informações sobre atribuições de função de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir este procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atribuições de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Remover uma atribuição de função de gerenciamento

Se você souber o nome da atribuição de função que você deseja remover, use a seguinte sintaxe.

```powershell
Remove-ManagementRoleAssignment <assignment name>
```

Por exemplo, para remover a atribuição de função "Camada 2 ajuda mesa atribuição", use o seguinte comando.

```powershell
Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"
```

Se você não souber o nome da atribuição de função, você pode usar a seguinte sintaxe.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 
```

Por exemplo, se você deseja remover a atribuição da função regular de destinatários de email do usuário davids, use o seguinte comando.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment
```

