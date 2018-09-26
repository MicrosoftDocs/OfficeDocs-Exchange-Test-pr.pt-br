---
title: 'Alterar a política de atribuição de uma caixa de correio: Exchange 2013 Help'
TOCTitle: Alterar a política de atribuição de uma caixa de correio
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 50484862
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar a política de atribuição de uma caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-08_

Você pode alterar a política de atribuição de função de gerenciamento atribuída a uma caixa de correio. Quando você alterar a política de atribuição de uma caixa de correio, a alteração entrará em vigor assim que o usuário atualiza a conexão, como na próxima vez que ele acesse suas caixas de correio ou abra a página de opções da caixa de correio. Para obter mais informações sobre políticas de atribuição no Microsoft Exchange Server 2013, consulte [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas às permissões? Confira [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para alterar a política de atribuição de uma caixa de correio

1.  No Exchange Centro de administração (EAC), navegue até **destinatários** \> **caixas de correio**.

2.  Selecione o usuário ou a caixa de correio de recurso que você deseja alterar a política de atribuição no e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Selecione **os recursos de caixa de correio**.

4.  Na lista de **política de atribuição de função**, selecione a política de atribuição que você deseja atribuir à caixa de correio e clique em **Salvar**.

## Use o Shell para alterar a política de atribuição de uma caixa de correio

Para alterar a política de atribuição é atribuída a uma caixa de correio, use a seguinte sintaxe.

```powershell
Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>
```

Este exemplo define a política de atribuição para o Unified Messaging Users na caixa de correio Brian.

```powershell
Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"
```

## Usar o Shell para alterar a política de atribuição em um grupo de caixas de correio atribuída uma política de atribuição específica


> [!NOTE]
> Você não pode usar o EAC para alterar a política de atribuição em um grupo de caixas de correio de uma só vez.



Esse procedimento faz uso de canalização, o cmdlet **Where** e o parâmetro *WhatIf* . Para obter mais informações sobre esses conceitos, consulte os tópicos a seguir:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

  - [Comutadores WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Se você quiser alterar a política de atribuição de um grupo de caixas de correio que estão atribuídos a uma diretiva específica, use a seguinte sintaxe.

```powershell
Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>
```

Este exemplo localiza todas as caixas de correio atribuídas aos usuários Redmond - política de atribuição de correio de voz não e altera a diretiva de atribuição para usuários de Redmond - habilitados de caixa postal.

```powershell
Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"
```

Este exemplo inclui o parâmetro *WhatIf* para que você possa ver todas as caixas de correio que serão alteradas sem confirmar as alterações.

```powershell
Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) ou [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

