---
title: 'Gerenciar grupos de função: Exchange 2013 Help'
TOCTitle: Gerenciar grupos de função
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 50486344
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar grupos de função

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-08_

Este tópico mostra como adicionar, remover, copiar e exibir os grupos de funções de gerenciamento no Microsoft Exchange Server 2013. Ele também mostra como adicionar, remover e listar funções de gerenciamento em grupos de funções e como alterar os escopos de gerenciamento e delegados em grupos de função. Para obter mais informações sobre grupos de função no Exchange 2013, consulte [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a grupos de funções, consulte [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 a 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


## O que você deseja fazer?

## Criar um grupo de função

Se você quiser personalizar as permissões que você pode atribuir a um grupo de usuários, crie um novo grupo de funções de gerenciamento personalizado.

## Usar o EAC para criar um grupo de função

1.  No Exchange Centro de administração (EAC), navegue até **permissões** \> **Funções de administrador** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na janela **novo grupo de função**, forneça um nome para o novo grupo de função.

3.  Você pode selecionar as funções que você deseja ser atribuído ao grupo de funções e os membros que você deseja ser adicionado ao grupo de funções agora ou você pode fazer isso mais tarde.

4.  Selecione o escopo de gravação que você deseja aplicar ao novo grupo de função.

5.  Clique em **Salvar** para criar o grupo de funções.

## Use o Shell para criar um grupo de função

Para criar um grupo de funções, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638181\(exchg.150\)#examples) em [New-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638181\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito um grupo de funções, faça o seguinte:

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Verifique se o novo grupo de função aparece na lista de grupos de função e selecione-o.

3.  Verificar se o escopo que você especificou no novo grupo de função, funções atribuídas e membros estão listados no painel de detalhes do grupo de função.

## Copiar um grupo de funções

## Usar o EAC para copiar um grupo de funções

Se você tiver um grupo de função que contém as permissões que deseja conceder aos usuários, mas você deseja aplicar um escopo de gerenciamento diferentes, remover ou adicionar uma ou duas funções de gerenciamento sem precisar adicionar todas as outras funções manualmente, você poderá copiar o grupo de função existente.


> [!IMPORTANT]  
> Você não pode usar o EAC para copiar um grupo de funções, se você usou o Exchange Management Shell para configurar vários escopos da função de gerenciamento ou escopos exclusivos no grupo de funções. Se você configurou vários escopos ou escopos exclusivos em grupo de funções, você deve usar os procedimentos de Shell neste tópico para copiar o grupo de funções. Para obter mais informações sobre escopos da função de gerenciamento, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Noções básicas sobre escopos da função de gerenciamento</A>.

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja copiar e clique em **Copiar**![Ícone Copiar](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Ícone Copiar").

3.  Na janela **novo grupo de função**, forneça um nome para o novo grupo de função.

4.  Revise as funções que foram copiadas para o novo grupo de função. Adicionar ou remover funções conforme necessário.

5.  Revise o escopo de gravação e alterá-lo conforme necessário.

6.  Revise os membros que foram copiados para o novo grupo de função. Adicionar ou remover membros conforme necessário.

7.  Clique em **Salvar** para criar o grupo de funções.

## Usar o Shell para copiar um grupo de funções sem escopo

1.  Armazene o grupo de função que você deseja copiar em uma variável usando a seguinte sintaxe.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  Criar novo grupo de funções e também adicionar membros ao grupo de funções e especificar quem pode delegar o novo grupo de funções para outros usuários, usando a seguinte sintaxe.
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>
    ```

Por exemplo, os comandos a seguir copiam o grupo de funções Gerenciamento da organização e nomeiam o novo grupo de funções como "Gerenciamento da organização limitado". Também adicionam os membros Isabelle, Carter e Lukas e podem ser delegados por Jenny e Katie.

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie
```

Depois que o novo grupo de função é criado, você pode adicionar ou remover funções, alterar o escopo das atribuições de função na função e muito mais.

Para a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638115\(v=exchg.150\)) e [New-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638181\(v=exchg.150\)).

## Usar o Shell para copiar um grupo de funções com um escopo personalizado

1.  Armazene o grupo de função que você deseja copiar em uma variável usando a seguinte sintaxe.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  Crie novo grupo de função com um escopo personalizado usando a seguinte sintaxe.
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>
    ```

Por exemplo, os comandos a seguir copiam o grupo de funções Gerenciamento da organização e criam um novo grupo de funções chamado Gerenciamento da organização de Vancouver com o escopo de destinatário dos Usuários de Vancouver e o escopo de configuração dos Servidores de Vancouver.

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"
```

Você também pode adicionar membros ao grupo de função ao criá-lo, usando o parâmetro *Members*, como visto anteriormente em Use the Shell to copy a role group with no scope neste tópico. Para obter mais informações sobre escopos de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Depois que o novo grupo de função é criado, você pode adicionar ou remover funções, alterar o escopo das atribuições de função na função e realize outras tarefas.

Para a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638115\(v=exchg.150\)) e [New-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638181\(v=exchg.150\)).

## Usar o Shell para copiar um grupo de funções com um escopo de UO

1.  Armazene o grupo de função que você deseja copiar em uma variável usando a seguinte sintaxe.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  Crie novo grupo de função com um escopo personalizado usando a seguinte sintaxe.
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>
    ```

Por exemplo, os seguintes comandos copiam o grupo de funções Gerenciamento de destinatários e criam um novo grupo de funções chamado Gerenciamento de destinatários de Toronto que permite o gerenciamento de usuários somente na UO de Usuários de Toronto.

```powershell
$RoleGroup = Get-RoleGroup "Recipient Management"
New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"
```

Você também pode adicionar membros ao grupo de função ao criá-lo, usando o parâmetro *Members*, como visto anteriormente em Use the Shell to copy a role group with no scope neste tópico. Para obter mais informações sobre escopos de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Depois que o novo grupo de função é criado, você pode adicionar ou remover funções, alterar o escopo das atribuições de função na função e muito mais.

Para a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638115\(v=exchg.150\)) e [New-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638181\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você tiver copiado com êxito um grupo de funções, faça o seguinte:

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Verifique se o grupo de funções copiada aparece na lista de grupos de função e, em seguida, selecioná-la.

3.  Verificar se os membros, funções atribuídas e escopo que você especificou no grupo de função copiada estão listados no painel de detalhes do grupo de função.

## Remover um grupo de função

Se não precisar mais um grupo de função que você criou, você poderá ser removido. Quando você remove um grupo de funções, atribuições da função de gerenciamento entre o grupo de função e as funções de gerenciamento são excluídas. As funções de gerenciamento não são excluídas. Se um usuário dependem de grupo de funções para o acesso a um recurso, o usuário não terá mais acesso ao recurso. Não é possível remover grupos de função internos.

## Usar o EAC para remover um grupo de função

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  Verifique se que você deseja remover o grupo de função selecionada e, em caso afirmativo, responda **Sim** para o aviso.

## Use o Shell para remover um grupo de função

Para remover um grupo de funções, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638141\(exchg.150\)#examples) em [Remove-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638141\(v=exchg.150\)).

## Exibir grupos de função

Você pode exibir uma lista de grupos de funções ou as informações detalhadas sobre um grupo de função específica que existe em sua organização.

## Usar o EAC para exibir uma lista de grupos de função e detalhes do grupo de função

1.  No EAC, navegue até **permissões** \> **Funções de administrador**. Todos os grupos de função em sua organização são listados aqui.

2.  Selecione um grupo de funções para exibir os membros, funções e escopo atribuídos configurados em um grupo de funções.

## Usar o Shell para exibir uma lista de grupos de função e detalhes do grupo de função

Para exibir uma lista de grupos de função, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638115\(exchg.150\)#examples) em [Get-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638115\(v=exchg.150\)).

## Adicionar uma função a um grupo de função

Adicionando uma função de gerenciamento a um grupo de função é a maneira recomendada e simples para conceder permissões para um grupo de administradores ou usuários especializados. Se você deseja dar aos usuários que são membros de um grupo de funções a capacidade de gerenciar um recurso, você pode adicionar a função de gerenciamento que gerencia o recurso ao grupo de funções. Depois que a função é adicionada, os membros do grupo de função são concedidos as permissões fornecidas pela função.

## Usar o EAC para adicionar uma função de gerenciamento a um grupo de função


> [!IMPORTANT]  
> Você não pode usar o EAC para adicionar funções a um grupo de funções, se você tiver usado o Shell para configurar vários escopos da função de gerenciamento ou escopos exclusivos no grupo de funções. Se você configurou vários escopos ou escopos exclusivos em grupo de funções, você deve usar os procedimentos de Shell neste tópico para adicionar funções ao grupo de funções. Para obter mais informações sobre escopos da função de gerenciamento, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Noções básicas sobre escopos da função de gerenciamento</A>.


1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja adicionar uma função para e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na seção **funções**, selecione as funções que você deseja adicionar ao grupo de funções.

4.  Quando você terminar de adicionar funções ao grupo de funções, clique em **Salvar**.

## Use o Shell para criar uma atribuição de função com nenhum escopo

Você pode criar uma atribuição de função com nenhum escopo entre uma função e um grupo de função. Quando você fizer isso, o implícita leitura e gravação implícita escopos da função se aplicam.

Use a seguinte sintaxe para atribuir uma função sem qualquer escopo para um grupo de funções. Um nome de atribuição de função é criado automaticamente se você não especificar uma.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>
```

Este exemplo atribui a função de gerenciamento de regras de transporte para o grupo de funções de conformidade de Seattle.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Use o Shell para criar uma atribuição de função com um escopo predefinido

Se um escopo predefinido atende aos seus requisitos de negócios, você pode aplicar esse escopo à atribuição de função em vez de criar um novo. Para obter uma lista de escopos predefinidos e suas descrições, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Para obter mais informações sobre atribuições de função, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Use a seguinte sintaxe para atribuir uma função a um grupo de função com um escopo predefinido. Um nome de atribuição de função é criado automaticamente se você não especificar uma.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >
```

Este exemplo atribui a função de controle de mensagens para o grupo de função do suporte ao Enterprise e aplica o escopo da organização predefinido.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Usar o Shell para criar uma atribuição de função com um escopo de baseado em filtro de destinatário

Se você criou um escopo de baseado em filtro de destinatário, você precisa incluir o escopo no comando utilizado para atribuir a função a um grupo de funções, usando o parâmetro *CustomRecipientWriteScope* .

Você também pode incluir um escopo de gravação da configuração quando você cria uma atribuição de função que possui um destinatário o escopo de gravação.

Para mais informações sobre atribuições de função e escopos, confira os seguintes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Use a seguinte sintaxe para atribuir uma função a um grupo de função com um escopo de baseado em filtro de destinatário. Um nome de atribuição de função é criado automaticamente se você não especificar uma.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>
```

Este exemplo atribui a função de controle de mensagens ao grupo de funções Recipient Admins de Seattle e aplica o escopo de destinatários de Seattle.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Use o Shell para criar uma atribuição de função com um escopo de configuração

Se você criou um servidor ou o filtro de configuração do banco de dados ou o escopo com base na lista, você precisa incluir o escopo no comando utilizado para atribuir a função a um grupo de funções, usando o parâmetro *CustomConfigWriteScope* .

Você também pode incluir um escopo de gravação do destinatário quando você cria uma atribuição de função que possui uma configuração de escopo de gravação.

Para mais informações sobre atribuições de função e escopos de gerenciamento, consulte os seguintes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Use a seguinte sintaxe para atribuir uma função a um grupo de função com um escopo de configuração. Um nome de atribuição de função é criado automaticamente se você não especificar uma.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>
```

Este exemplo atribui a função de bancos de dados para o grupo de funções de servidor de Seattle Admins e aplica o escopo de servidores de Seattle.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Use o Shell para criar uma atribuição de função com um escopo de UO

Se desejar fazer o escopo de gravação da função para uma UO de escopo, você pode especificar a UO no parâmetro *RecipientOrganizationalUnitScope* diretamente.

Para mais informações sobre atribuições de função e escopos de gerenciamento, consulte os seguintes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Use o seguinte comando para atribuir uma função a um grupo de funções e restringir o escopo de gravação de uma função como uma OU específica. Um nome de atribuição de função é criado automaticamente se você não especificar uma.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>
```

Este exemplo atribui a função de destinatários de email para o grupo de funções de Seattle Recipient Admins e escopos a atribuição à Sales\\Users OU no domínio Contoso.com.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se adicionou com êxito funções a um grupo de função, faça o seguinte:

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você adicionou funções para. No painel de detalhes do grupo de função, verifique se as funções que você adicionou estão listadas.

## Remover uma função de um grupo de função

A remoção de uma função de um grupo de funções de gerenciamento é a maneira recomendada e simples para revogar permissões concedidas para um grupo de administradores ou usuários especializados. Se não desejar que os administradores ou usuários especializados tenha permissões para gerenciar um recurso, você remove a função de gerenciamento do grupo de funções de gerenciamento que gerencia as permissões. Depois que a função for removida, os membros do grupo de função não terá mais permissões para gerenciar o recurso.


> [!NOTE]  
> Alguns grupos de função, como o grupo de funções Gerenciamento da Organização, restringem quais funções podem ser removidas de um grupo de função. Para obter mais informações, consulte <A href="understanding-management-role-groups-exchange-2013-help.md">Noções básicas sobre grupos de funções de gerenciamento</A>.<BR>Se um administrador for um membro de outro grupo de função que contém funções de gerenciamento que concede permissões para gerenciar o recurso, você precisa remover o administrador de outros grupos de função, ou remover a função que concede permissões para gerenciar o recurso dos outros grupos de função.

## Usar o EAC para remover uma função de gerenciamento de um grupo de função

> [!IMPORTANT]  
> Você não pode usar o EAC para remover funções de um grupo de funções, se você tiver usado o Shell para configurar vários escopos ou escopos exclusivos no grupo de funções. Se você configurou vários escopos ou escopos exclusivos em grupo de funções, você deve usar os procedimentos de Shell neste tópico para remover funções do grupo de funções. Para obter mais informações sobre escopos da função de gerenciamento, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Noções básicas sobre escopos da função de gerenciamento</A>.

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja remover uma função do e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na seção **funções**, selecione as funções que você deseja remover do grupo de funções.

4.  Quando terminar de remover funções do grupo de funções, clique em **Salvar**.

## Use o Shell para remover uma função de um grupo de função

Você pode remover as funções de grupos de função Recuperando a atribuição de função de gerenciamento associada usando o cmdlet **Get-ManagementRoleAssignment** e, em seguida, tubulação retornada de atribuição de função para o cmdlet **Remove-ManagementRoleAssignment** . A menos que você deseja remover atribuições de função de delegação e regular ao mesmo tempo, especifique o parâmetro *Delegating* para especificar se você deseja remover atribuições de função regular ou de delegação.

Para obter mais informações sobre atribuições de função comuns e de delegação, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Esse procedimento usa o pipelining. Para obter mais informações sobre o pipelining, consulte [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\)).

Para remover uma função de um grupo de função, use a seguinte sintaxe.

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment
```

Este exemplo remove a função de grupos de distribuição, que permite que administradores gerenciem grupos de distribuição, do grupo de funções Recipient Administrators de Seattle. Porque queremos removem a atribuição de função que fornece permissões para gerenciar grupos de distribuição, o parâmetro *Delegating* é definido como `$False`, que retorna apenas atribuições da função regular.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351205\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito funções de um grupo de funções, faça o seguinte:

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você removeu funções de. No painel de detalhes do grupo de função, verifique se as funções que você removeu não é mais estão listadas.

## Alterar o escopo de um grupo de funções

As atribuições da função de gerenciamento entre um grupo de funções e uma função contêm os escopos de gerenciamento, que determina quais objetos são disponibilizados para os membros desse grupo de função. Alterando o escopo de gravação em um grupo de função, você pode alterar a quais objetos são disponibilizados aos membros do grupo de função para criar, alterar ou remover. Você não pode alterar o escopo de leitura em um grupo de função.

Exchange 2013 inclui os escopos que são aplicados por padrão para atribuições de função quando nenhum escopos personalizados são criados. Se você quiser usar um escopo personalizado com uma atribuição de função em um grupo de função, você deve criar um primeiro. Para obter mais informações sobre como criar escopos personalizados, que é uma tarefa avançada, consulte [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Para obter mais informações sobre escopos da função de gerenciamento e atribuições em Exchange 2013, consulte os tópicos a seguir:

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

## Usar o EAC para alterar o escopo em um grupo de função

Quando você usar o EAC para alterar o escopo em um grupo de função, você realmente altera o escopo em todas as atribuições de função entre o grupo de função e cada uma das funções de gerenciamento atribuídas ao grupo de funções. Se você quiser alterar o escopo das atribuições de função específica, você deve usar os procedimentos de Shell neste tópico.


> [!IMPORTANT]  
> Você não pode usar o EAC para gerenciar escopos de atribuições de função entre funções e um grupo de funções, se você tiver usado o Shell para configurar vários escopos ou escopos exclusivos essas atribuições de função. Se você configurou vários escopos ou escopos exclusivos nessas atribuições de função, você deve usar os procedimentos de Shell neste tópico para gerenciar escopos. Para obter mais informações sobre escopos da função de gerenciamento, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Noções básicas sobre escopos da função de gerenciamento</A>.

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja alterar o escopo em e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Selecione uma das seguintes opções de **Escopo de Gravação**:
    
      - Um escopo de gravação da caixa suspensa, onde você pode selecionar o escopo de gravação padrão ou um escopo de gravação personalizado.
    
      - **Unidade organizacional**   Selecione essa opção para fornecer uma UO (unidade organizacional) caso você queira adicionar esse grupo de função a uma UO.

4.  Clique em **Salvar** para salvar as alterações feitas no grupo de funções.

## Usar o Shell para alterar o escopo de todas as atribuições de função de um grupo de funções ao mesmo tempo

As atribuições de função entre o grupo de funções e as funções atribuídas a ele podem usar o escopo implícito obtido das próprias funções, do mesmo escopo personalizado ou de diferentes escopos personalizados. Para mais informações sobre atribuições de função, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Os escopos nas atribuições de função são gerenciados usando-se o cmdlet **Set-ManagementRoleAssignment**. Não é possível gerenciar escopos usando o cmdlet de **Set-RoleGroup**.

Para alterar o escopo de todas as atribuições de função entre um grupo de funções e um conjunto de funções de gerenciamento ao mesmo tempo, é preciso primeiro recuperar as atribuições de função do grupo e definir o novo escopo em cada uma das atribuições. Isso pode ser feito utilizando-se o cmdlet **Get-ManagementRoleAssignment** para recuperar as atribuições e enviá-las ao cmdlet **Set-ManagementRoleAssignment**.

Esse procedimento usa os conceitos de pipelining e a opção *WhatIf*. Para mais informações, consulte os seguintes tópicos:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Comutadores WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Para definir o escopo em todas as atribuições de função de um grupo de funções ao mesmo tempo, use a sintaxe na sequência.

```powershell
Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
```

Use apenas os parâmetros de que você precisa para configurar o escopo que deseja usar. Por exemplo, se quiser alterar o escopo do destinatário de todas as atribuições de função no grupo de funções Gerenciamento de Destinatários de Venda para Funcionários de Vendas Diretas, use o seguinte comando.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"
```

> [!NOTE]  
> Você pode usar a opção <EM>WhatIf</EM> para verificar se apenas as atribuições de função que deseja modificar foram alteradas. Execute o comando anterior com a opção <EM>WhatIf</EM> para verificar os resultados e remova a opção <EM>WhatIf</EM> para aplicar as alterações.

Para obter mais informações sobre como alterar as atribuições de função de gerenciamento, consulte [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Usar o Shell para alterar o escopo de cada atribuição de função de um grupo de funções

As atribuições de função entre o grupo de funções e as funções atribuídas a ele podem usar o escopo implícito obtido das próprias funções, do mesmo escopo personalizado ou de diferentes escopos personalizados. Para mais informações sobre atribuições de função, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Os escopos nas atribuições de função são gerenciados usando-se o cmdlet **Set-ManagementRoleAssignment**. Não é possível gerenciar escopos usando o cmdlet de **Set-RoleGroup**.

Esse procedimento usa os conceitos de pipelining e o cmdlet **Format-List**. Para mais informações, consulte os seguintes tópicos:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

Para alterar o escopo de uma atribuição de função entre um grupo de funções e uma função de gerenciamento, localize primeiro o nome da atribuição de função e defina o escopo na atribuição de função.

1.  Para encontrar os nomes de todas as funções de atribuição em um grupo de funções, use o comando a seguir. Ao encaminhar as atribuições de função de gerenciamento ao cmdlet **Format-List**, você poderá exibir o nome completo da atribuição.
    
    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name
    ```

2.  Localize o nome da atribuição de função que você deseja alterar. Use o nome da atribuição de função na próxima etapa.

3.  Para definir o escopo em uma atribuição individual, use a sintaxe a seguir.
    
    ```powershell
    Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
    ```

Use apenas os parâmetros de que você precisa para configurar o escopo que deseja usar. Por exemplo, se quiser alterar o escopo do destinatário da atribuição de função Mail Recipients\_Sales Recipient Management para Todos os Funcionários de Vendas, use o seguinte comando.

```powershell
Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"
```

Para obter mais informações sobre como alterar as atribuições de função de gerenciamento, consulte [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que você alterou com êxito o escopo de uma atribuição de função em um grupo de função, faça o seguinte:

  - Se você usou o EAC para configurar o escopo do grupo de função, faça o seguinte:
    
    1.  No EAC, navegue até **permissões** \> **Funções de administrador**. Todos os grupos de função em sua organização são listados aqui.
    
    2.  Selecione um grupo de funções para exibir o escopo que está configurado no grupo de funções.

  - Se você usou o Shell para configurar o escopo do grupo de função, faça o seguinte:
    
    1.  Execute o seguinte comando no Shell.
        
        ```powershell
        Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
        ```
    
    2.  Verifique se que o escopo de gravação nas atribuições da função foi alterado no escopo especificado.

## Adicionar ou remover um representante do grupo de função

Representantes do grupo de função são usuários ou grupos de segurança universais (USGs) que podem adicionar ou remover membros de um grupo de funções ou alterar as propriedades de um grupo de funções. Adicionando ou removendo representantes do grupo de função, você pode controlar quem tem permissão para gerenciar um grupo de funções.


> [!IMPORTANT]  
> Depois de adicionar um representante para um grupo de funções, o grupo de funções só pode ser gerenciado por representantes no grupo de funções ou por usuários atribuídos, direta ou indiretamente, a função de gerenciamento de gerenciamento de função.<BR>Se um usuário é atribuído, direta ou indiretamente, a função de gerenciamento de função e não será adicionado como um representante do grupo de função, o usuário deve usar a opção <EM>BypassSecurityGroupManagerCheck</EM> nos cmdlets de <STRONG>Add-RoleGroupMember</STRONG>, <STRONG>Remove-RoleGroupMember</STRONG>, <STRONG>Update-RoleGroupMember</STRONG>e <STRONG>Set-RoleGroup</STRONG> para gerenciar um grupo de função.

> [!NOTE]  
> Você não pode usar o EAC para adicionar um delegado a um grupo de funções.

## Use o Shell para adicionar um delegado a um grupo de função

Para alterar a lista de delegados em um grupo de função, você pode usar o parâmetro *ManagedBy* no cmdlet **Set-RoleGroup** . O parâmetro *ManagedBy* substitui a lista de representantes de todo o grupo de função. Se você deseja adicionar representantes à função de grupo, em vez de substituem toda a lista de representantes, use as seguintes etapas:

1.  Armazene o grupo de funções em uma variável usando o seguinte comando.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  Adicione o representante ao grupo de funções armazenado na variável usando o seguinte comando.
    
    ```powershell
    $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    ```
    

    > [!NOTE]  
    > Use o cmdlet <STRONG>Get-Group</STRONG> se você deseja adicionar um USG.

3.  Repita a etapa 2 para cada representante que você deseja adicionar.

4.  Aplica a nova lista de delegados ao grupo de funções real usando o seguinte comando.
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

Este exemplo adiciona o usuário David Strome como um representante do grupo de função Gerenciamento da Organização.

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
$RoleGroup.ManagedBy += (Get-User "David Strome").Identity
Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638182\(v=exchg.150\)).

## Use o Shell para remover um representante de um grupo de função

Para alterar a lista de delegados em um grupo de função, você pode usar o parâmetro *ManagedBy* no cmdlet **Set-RoleGroup** . O parâmetro *ManagedBy* substitui a lista de representantes de todo o grupo de função. Se desejar remover representantes do grupo de funções ao invés de substituir toda a lista de representantes, siga estas etapas:

1.  Armazene o grupo de funções em uma variável usando o seguinte comando.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  Remova o representante do grupo de funções armazenado na variável usando o seguinte comando.
    
    ```powershell
    $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    ```
    
    > [!NOTE]  
    > Use o cmdlet <STRONG>Get-Group</STRONG> se desejar remover um USG.

3.  Repita a etapa 2 para cada representante que você deseja remover.

4.  Aplica a nova lista de delegados ao grupo de funções real usando o seguinte comando.
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

Este exemplo remove o usuário David Strome como um representante do grupo de função Gerenciamento da Organização.

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
$RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638182\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que você alterou com êxito a lista de representantes em um grupo de função, faça o seguinte:

1.  No Shell, execute o comando a seguir.
    
    ```powershell
    Get-RoleGroup <role group name> | Format-List ManagedBy
    ```

2.  Verifique se os representantes listados na propriedade *ManagedBy* incluem somente os representantes que devem ser capazes de gerenciar o grupo de função.