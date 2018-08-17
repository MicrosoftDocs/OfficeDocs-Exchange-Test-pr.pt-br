---
title: 'Gerenciar políticas de atribuição de função: Exchange 2013 Help'
TOCTitle: Gerenciar políticas de atribuição de função
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 50487053
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar políticas de atribuição de função

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-09_

Se você quiser personalizar as permissões que você atribuir a um grupo de usuários finais, crie uma nova política de atribuição de função de gerenciamento personalizado. A política de atribuição que você criar pode ser personalizada para atender a requisitos específicos do seu usuário final. Para obter mais informações sobre políticas de atribuição no Microsoft Exchange Server 2013, consulte [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas ao gerenciamento de permissões? Confira [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de atribuição" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Adicionar uma política de atribuição

Depois que você criou a nova política de atribuição, você atribuir usuários a ela. Para obter mais informações, consulte [Alterar a política de atribuição de uma caixa de correio](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

## Usar o EAC para criar uma nova política de atribuição


> [!NOTE]
> Você só pode criar políticas de atribuição explícita usando o Centro de administração do Exchange (EAC). Se você quiser criar uma nova política de atribuição padrão, você deve usar o Exchange Management Shell. Para obter mais informações, consulte a seção "Usar o Shell para criar uma política de atribuição padrão" mais adiante neste tópico.



1.  No EAC, navegue até **permissões** \> **Funções de usuário** e, em seguida, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na janela de política de atribuição de função, forneça um nome para a nova política de atribuição.

3.  Marque a caixa de seleção ao lado do função ou funções que deseja adicionar à diretiva de atribuição. Você pode selecionar várias funções, incluindo as funções de usuário final que você adicionou. Se você selecionar uma função que possui funções filhas, as funções filhas são automaticamente selecionadas.

4.  Clique em **Salvar** para salvar as alterações na política de atribuição.

## Usar o Shell para criar uma política de atribuição explícita

Para criar uma política de atribuição explícita que pode ser atribuída manualmente a caixas de correio, use a seguinte sintaxe.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>

Este exemplo cria a política de atribuição explícita limitado configuração de caixa de correio e atribui as funções `MyBaseOptions`, `MyAddressInformation`e `MyDisplayName` a ela.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638101\(v=exchg.150\)).

## Usar o Shell para criar uma política de atribuição padrão

Para criar uma política de atribuição padrão atribuída às novas caixas de correio, use a seguinte sintaxe.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault

Este exemplo cria a política de atribuição padrão limitado configuração de caixa de correio e atribui as funções `MyBaseOptions`, `MyAddressInformation`e `MyDisplayName` a ela.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638101\(v=exchg.150\)).

## Remover uma política de atribuição

Se não precisar mais uma diretiva de atribuição de função de gerenciamento, você poderá ser removido.

## O que você precisa saber antes de começar?

  - Todos os usuários atribuídos à política de atribuição devem ser alterados para outra política de atribuição. Para obter mais informações sobre como alterar uma política de atribuição de uma caixa de correio, consulte [Alterar a política de atribuição de uma caixa de correio](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

  - Todas as atribuições de função de gerenciamento entre a política de atribuição e as funções de gerenciamento atribuídas devem ser removidas. Para obter mais informações sobre como remover uma atribuição de função de uma diretiva de atribuição, consulte a seção usar o Shell para remover uma função de uma diretiva de atribuição mais adiante neste tópico.

  - Se você deseja remover uma política de atribuição padrão, ela deve ser a última diretiva de atribuição na organização Exchange 2013.

## Usar o EAC para remover uma política de atribuição

1.  No EAC, navegue até **permissões** \> **Funções de usuário**.

2.  Selecione a política de atribuição que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Usar o Shell para remover uma política de atribuição

Para remover uma diretiva de atribuição, use a seguinte sintaxe.

    Remove-RoleAssignmentPolicy <role assignment policy>

Este exemplo remove a diretiva de atribuição de usuários de Nova York temporário.

    Remove-RoleAssignmentPolicy "New York Temporary Users"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638190\(v=exchg.150\)).

## Exibir uma lista de políticas de atribuição ou detalhes da política de atribuição

Você pode exibir as políticas de atribuição de função de gerenciamento de várias maneiras, dependendo das informações que você deseja e se você estiver usando o EAC ou o Shell.

No EAC, você pode exibir a lista de políticas de atribuição e as funções atribuídas a eles. No Shell, você pode exibir todas as políticas de atribuição na sua organização, liste as caixas de correio atribuídas uma política específica e muito mais.

## Usar o EAC para exibir uma lista de políticas de atribuição

1.  No EAC, navegue até **permissões** \> **Funções de usuário**. Todas as diretivas de atribuição na organização são listadas aqui.

2.  Para exibir os detalhes de uma política de atribuição específica, selecione a política de atribuição que você deseja exibir. A descrição e as funções atribuídas à diretiva de atribuição são exibidas no painel de detalhes.

## Use o Shell para exibir uma lista de políticas de atribuição

Você pode exibir uma lista de todas as diretivas de atribuição na sua organização especificando não quaisquer políticas de atribuição, quando você executa o cmdlet **Get-RoleAssignmentPolicy** .

Esse procedimento faz uso de canalização e o cmdlet **Format-Table** . Para obter mais informações sobre esses conceitos, consulte os tópicos a seguir:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

Para retornar uma lista de todas as diretivas de atribuição na sua organização, use o seguinte comando.

    Get-RoleAssignmentPolicy

Para retornar uma lista de propriedades específicas para todas as políticas de atribuição na sua organização, você pode canalizar os resultados para o cmdlet **Format-Table** e especifique as propriedades que você deseja na lista de resultados. Use a seguinte sintaxe.

    Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>

Este exemplo retorna uma lista de todas as diretivas de atribuição na sua organização e inclui as propriedades **Name** e **IsDefault** .

    Get-RoleAssignmentPolicy | Format-Table Name, IsDefault

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638195\(v=exchg.150\)).

## Use o Shell para exibir os detalhes de uma política de atribuição único

Você pode exibir os detalhes de uma política de atribuição específica usando o cmdlet **Get-RoleAssignmentPolicy** e canalizar a saída para o cmdlet **Format-List** .

Esse procedimento faz uso de canalização e o cmdlet **Format-List** . Para obter mais informações sobre esses conceitos, consulte os tópicos a seguir:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

Para exibir os detalhes de uma política de atribuição específica, use a seguinte sintaxe.

    Get-RoleAssignmentPolicy <assignment policy name> | Format-List

Este exemplo exibe os detalhes sobre os usuários de Redmond - nenhuma diretiva de atribuição de mensagens de texto.

    Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638195\(v=exchg.150\)).

## Use o Shell para encontrar a política de atribuição padrão

Você pode encontrar a política de atribuição padrão ao canalizar a saída do cmdlet **Get-RoleAssignmentPolicy** para o cmdlet **Where** . Com o cmdlet **Where** , filtre os dados retornados para exibir somente a diretiva de atribuição que tem sua propriedade *IsDefault* definida como `$True`.

Esse procedimento faz uso de canalização e o cmdlet **Where** . Para obter mais informações sobre esses conceitos, consulte os tópicos a seguir:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

Este exemplo retorna a diretiva de atribuição padrão.

    Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638195\(v=exchg.150\)).

## Usar o Shell para caixas de correio do modo de exibição que são atribuídas a uma diretiva específica

Você pode encontrar que todas as caixas de correio atribuída uma política de atribuição específica ao canalizar a saída do cmdlet **Get-Mailbox** para o cmdlet **Where** . Com o cmdlet **Where** , filtre os dados retornados para exibir somente as caixas de correio que tenham sua propriedade *RoleAssignmentPolicy* definida como o nome da política de atribuição que você especificar.

Esse procedimento faz uso de canalização e o cmdlet **Where** . Para obter mais informações sobre esses conceitos, consulte os tópicos a seguir:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

Use a sintaxe a seguir:

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }

Este exemplo localiza que todas as caixas de correio atribuída a política aos usuários finais de Vancouver.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) ou [Get-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638195\(v=exchg.150\)).

## Alterar a política de atribuição padrão

Você pode alterar a política de atribuição de função de gerenciamento atribuída a novas caixas de correio que são criadas. Alterando a política de atribuição de função padrão não altera a política de atribuição atribuída às caixas de correio existentes. Para alterar a política de atribuição atribuída às caixas de correio existentes, consulte [Alterar a política de atribuição de uma caixa de correio](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).


> [!NOTE]
> Você não pode usar o EAC para alterar a política de atribuição padrão. Você precisará usar o Shell.



## Use o Shell para alterar a política de atribuição padrão

Para alterar a política de atribuição padrão, use a seguinte sintaxe.

    Set-RoleAssignmentPolicy <assignment policy name> -IsDefault

Este exemplo define a política de atribuição de usuários finais de Vancouver como a política de atribuição padrão.

    Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault


> [!IMPORTANT]
> Novas caixas de correio são atribuídas a política de atribuição padrão, mesmo que a diretiva não tiver sido atribuída a funções de gerenciamento. Caixas de correio atribuídas diretivas de atribuição sem funções de gerenciamento atribuídas não podem acessar quaisquer recursos de configuração de caixa de correio no Microsoft Outlook Web App.



Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-RoleAssignmentPolicy](https://technet.microsoft.com/pt-br/library/dd638090\(v=exchg.150\)).

## Adicionar uma função a uma política de atribuição

## Usar o EAC para adicionar uma função a uma política de atribuição

1.  No EAC, navegue até **permissões** \> **Funções de usuário**.

2.  Selecione a política de atribuição que você deseja adicionar uma ou mais funções para e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Marque a caixa de seleção ao lado do função ou funções que deseja adicionar à diretiva de atribuição. Você pode selecionar várias funções, incluindo as funções de usuário final que você adicionou. Se você selecionar uma função que possui funções filhas, as funções filhas são automaticamente selecionadas.

4.  Clique em **Salvar** para salvar as alterações na política de atribuição.

## Use o Shell para adicionar uma função a uma política de atribuição

Para criar uma atribuição de função de gerenciamento entre uma função e uma diretiva de atribuição, use a seguinte sintaxe.

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

Este exemplo cria a atribuição de função usuários de Seattle - caixa postal entre a função de MyVoicemail e a diretiva de atribuição de usuários de Seattle.

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Remover uma função de uma diretiva de atribuição

Se você não desejar que os usuários finais tenham permissões para gerenciar determinados recursos de sua caixas de correio ou grupo de distribuição, você pode remover a função de gerenciamento que concede as permissões de diretiva de atribuição de função de gerenciamento ao qual o usuário é atribuído. Se outros usuários recebem a mesma política de atribuição, eles também perder a capacidade de gerenciar esse recurso.

## Usar o EAC para remover uma função de uma diretiva de atribuição

1.  No EAC, navegue até **permissões** \> **Funções de usuário**.

2.  Selecione a política de atribuição que você deseja remover uma ou mais funções de e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") .

3.  Desmarque a caixa de seleção ao lado do função ou funções que você deseja remover da política de atribuição. Se você desmarcar a caixa de seleção para uma função que possui funções filhas, as caixas de seleção para as funções filhas também são limpas.

4.  Clique em **Salvar** para salvar as alterações na política de atribuição.

## Use o Shell para remover uma função de uma diretiva de atribuição

Você pode remover funções de diretivas de atribuição Recuperando a atribuição de função de gerenciamento associada usando o cmdlet **Get-ManagementRoleAssignment** e, em seguida, tubulação retornada de atribuição de função para o cmdlet **Remove-ManagementRoleAssignment** .

Para obter mais informações sobre atribuições de função comuns e de delegação, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Esse procedimento usa o pipelining. Para obter mais informações sobre o pipelining, consulte [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\)).

Para remover uma função de uma diretiva de atribuição, use a seguinte sintaxe.

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

Este exemplo remove a função de gerenciamento de MyVoicemail, que permite que os usuários gerenciem suas opções de caixa postal, da política de atribuição de usuários de Seattle.

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351205\(v=exchg.150\)).

