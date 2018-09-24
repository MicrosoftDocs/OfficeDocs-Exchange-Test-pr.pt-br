---
title: 'Exibir atribuições de função: Exchange 2013 Help'
TOCTitle: Exibir atribuições de função
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 50484932
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir atribuições de função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

As atribuições de função de gerenciamento atribuem uma função de gerenciamento a um destinatário de função. Para mais informações sobre as atribuições de função de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atribuições de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Este tópico usa pipelining e o cmdlet **Format-List**. Para mais informações sobre esses conceitos, consulte os seguintes tópicos:
    
      - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))
    
      - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir uma lista de todas as atribuições de função

Você pode exibir uma lista de todas as atribuições de função configuradas em sua organização executando o cmdlet **Get-ManagementRoleAssignment**. Se você quiser recuperar uma lista de atribuições de função que correspondam a uma cadeia de caracteres parcial que você especificar, use caracteres curinga (\*). Este exemplo recupera uma lista de todas as atribuições de função que comecem com a cadeia de caracteres "Tier 1".

    Get-ManagementRoleAssignment "Tier 1*"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir detalhes de uma atribuição de função específica

Você pode exibir os detalhes de uma atribuição de função canalizando os resultados do cmdlet **Get-ManagementRoleAssignment** para o cmdlet **Format-List**. Use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment <assignment name> | Format-List
```

Este exemplo recupera os detalhes da atribuição de função Atribuição de Suporte Técnico.

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir a lista de atribuições de função atribuída a um destinatário de função específico

Para exibir uma lista de atribuições de função associadas a um grupo de função de gerenciamento, a uma função ou a uma diretiva de atribuição de função, ou associada a um usuário ou USG (grupo de segurança universal), use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role assignee name>
```

Este exemplo recupera todas as atribuições de função associadas ao grupo de função de Gerenciamento de Servidor.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Server Management"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir as atribuições de função associadas a uma função específica

Cada função pode ter várias atribuições de função. Você pode usar o cmdlet **Get-ManagementRoleAssigment** para exibir uma lista de atribuições de função associadas a uma função específica.

Para exibir uma lista de atribuições de função associadas a uma função específica, use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment -Role <role name>
```

Este exemplo recupera todas as atribuições de função associadas à função de Destinatários de Email.

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir uma lista de atribuições de função que usam um escopo específico predefinido

Para exibir uma lista de atribuições de função que usam um escopo específico predefinido, use a sintaxe a seguir.

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

Este exemplo recupera todas as atribuições de função que usam o escopo predefinido da Organização.

```powershell
Get-ManagementRoleAssignment -RecipientWriteScope Organization
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir uma lista de atribuições de função que foram incluídas no escopo de uma OU específica

Para exibir uma lista de atribuições de função que foram incluídas no escopo de uma OU (unidade organizacional), use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>
```

Este exemplo recupera todas as atribuições de função que foram incluídas no escopo da OU América do Norte\\Engenharia\\Usuários no domínio contoso.com.

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir uma lista de atribuições de função que usam um escopo específico personalizado

Para exibir uma lista de atribuições de função que usam um escopo personalizado específico, é preciso antes determinar se o escopo é um escopo de destinatário, um escopo de configuração, um escopo de destinatário exclusivo ou um escopo de configuração exclusivo. Cada tipo de escopo usa um parâmetro diferente no cmdlet de **Get-ManagementRoleAssignment**. A seguir, estão listados cada escopo e seus parâmetros associados:

  - **Escopos de destinatário**   *CustomRecipientWriteScope*

  - **Escopos de configuração**   *CustomConfigWriteScope*

  - **Escopos de destinatário exclusivos**   *ExclusiveRecipientWriteScope*

  - **Escopos de configuração exclusivos**   *ExclusiveConfigWriteScope*

A sintaxe para cada parâmetro é a mesma. Especifique o nome do escopo com o parâmetro que corresponda ao tipo de escopo.

Este exemplo recupera todas as atribuições de função que usam o escopo de destinatário Destinatários de Vancouver.

```powershell
Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"
```

Este exemplo recupera todas as atribuições de função que usam o escopo de configuração exclusivo Site do AD.

```powershell
Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir uma lista de escopos exclusivos ou regulares

Para exibir uma lista de atribuições de função exclusivas ou regulares, use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment -Exclusive < $True | $False >
```

Por exemplo, para visualizar uma lista de escopos exclusivos, execute o seguinte comando:

```powershell
Get-ManagementRoleAssignment -Exclusive $True
```

Este exemplo recupera uma lista de escopos regulares sem qualquer escopo exclusivo.

```powershell
Get-ManagementRoleAssignment -Exclusive $False
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir quem pode modificar um destinatário ou servidor específico

Para exibir uma lista de atribuições de função que podem modificar um destinatário ou servidor específico, use os parâmetros *WritableRecipient* e *WritableServer*. Especifique o nome do destinatário com o parâmetro *WritableRecipient*, e o nome do servidor com o parâmetro *WritableServer*.

Este exemplo recupera uma lista de atribuições de função que podem modificar o destinatário Brian.

```powershell
Get-ManagementRoleAssignment -WritableRecipient "Brian"
```

Você pode combinar os parâmetros *WritableRecipient* e *WritableServer* a outros parâmetros, como o parâmetro *RoleAssignee* e a opção *GetEffectiveUsers* para refinar sua consulta e expandir quaisquer grupos de função ou USGs. Este exemplo recupera todas os usuários que podem modificar o servidor EX02 e que tenham a atribuição de grupo de função de Gerenciamento de Servidor.

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir os usuários que recebem permissões de uma atribuição via um grupo de função ou USG

Para exibir uma lista de usuários que recebem permissões de uma atribuição de função, use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers
```

Este exemplo recupera uma lista de usuários na atribuição de função Atribuição de Suporte Técnico.

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers
```

Você também pode combinar a opção *GetEffectiveUsers* com vários outros parâmetros no cmdlet **Get-ManagementRoleAssignment** para expandir os grupos de função e USGs aos quais as atribuições de função tiverem sido atribuídas. Para um exemplo de como a opção *GetEffectiveUsers* é usada com outros parâmetros, consulte "Exibir quem pode modificar um destinatário ou servidor específico" anteriormente neste tópico.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Exibir uma lista de atribuições de função habilitadas ou desabilitadas

Para exibir uma lista de atribuições de função habilitadas ou desabilitadas, use a sintaxe a seguir.

```powershell
Get-ManagementRoleAssignment -Enabled < $True | $False >
```

Este exemplo recupera uma lista de atribuições de função desabilitadas.

```powershell
Get-ManagementRoleAssignment -Enabled $False
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

