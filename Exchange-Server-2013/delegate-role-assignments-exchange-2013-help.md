---
title: 'Atribuições de função de representante: Exchange 2013 Help'
TOCTitle: Atribuições de função de representante
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 50486943
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atribuições de função de representante

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-02_

Delegação de função de gerenciamento permite que os destinatários de função atribuir uma função de gerenciamento especificada a outros grupos de funções de gerenciamento, diretivas de atribuição de função de gerenciamento, usuários ou grupos de segurança universal (USG). Por padrão, somente os membros do grupo de função de gerenciamento de gerenciamento da organização podem delegar atribuições de função. Quando uma nova instalação do Microsoft Exchange Server 2013 for implantada, apenas a conta de usuário que instalou o Exchange 2013 é um membro do grupo de funções de gerenciamento da organização.

Se você atribuir uma atribuição de função de delegação para um grupo de funções, qualquer membro do grupo de função pode delegar a função de gerenciamento associada outros os destinatários da função.


> [!IMPORTANT]
> Delegar atribuições de função não dá o destinatário terá as permissões concedidas pela função, apenas a capacidade de atribuir a função a outras pessoas. Se você quiser também conceder as permissões concedidas pela função para o destinatário da função, você também deve criar uma atribuição de função regular. Para criar uma atribuição de função regulares, consulte os seguintes tópicos:<BR><A href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</A><BR><A href="manage-role-assignment-policies-exchange-2013-help.md">Gerenciar políticas de atribuição de função</A><BR><A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Adicionar uma função a um usuário ou USG</A>




> [!NOTE]  
> Este tópico discute a delegação de atribuição de função de gerenciamento. Se você deseja delegar quem pode adicionar membros ou remover membros de grupos de função, que é o método recomendado de delegação, consulte <A href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</A>.



Para obter mais informações sobre atribuições de função regular e delegação atribuições de função de gerenciamento, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas ao gerenciamento de permissões? Confira [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir este procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atribuições de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para delegar a uma função de gerenciamento

Você pode criar delegação atribuições de função, usando o mesmos escopos predefinidos, filtro de destinatários ou baseado em filtro de servidor escopos, escopos com base em lista de servidor e a unidade organizacional (UO) escopos que podem ser usados para criar escopos regulares ou exclusivos. A única diferença entre a criação de uma atribuição de função regular e uma atribuição de função de delegação é a adição do comutador *Delegating* ao comando. Para obter mais informações sobre como criar atribuições de função, consulte os tópicos a seguir:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)


> [!NOTE]  
> Não é possível criar uma atribuição de função de delegação para uma diretiva de atribuição de função de gerenciamento.



Este exemplo cria uma atribuição de função de delegação para permitir que membros do grupo Administradores de sênior função atribuir a função destinatários de email para qualquer destinatário da função na organização Exchange.

  ```powershell
  New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating
  ```

Este exemplo cria uma atribuição de função de delegação para permitir que membros do grupo Administradores de sênior função atribuir a função de destinatários de email apenas aos usuários dentro da UO de vendas/Users no domínio contoso.com.

  ```powershell
  New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating
  ```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

