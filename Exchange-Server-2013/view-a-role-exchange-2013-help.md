---
title: 'Exibir uma função: Exchange 2013 Help'
TOCTitle: Exibir uma função
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 50485023
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir uma função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

As funções de gerenciamento podem ser listadas de várias maneiras, dependendo das informações que você desejar. Por exemplo, você pode escolher retornar apenas as funções de um tipo específico, funções que contenham apenas cmdlets e parâmetros específicos ou exibir os detalhes de uma função de gerenciamento específica. Para mais informações sobre as funções de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Se quiser exibir uma lista de todas as entradas de função de gerenciamento em uma função, consulte [Exibir entradas de função](view-role-entries-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Este tópico usa pipelining e os cmdlets **Format-List** e **Format-Table**. Para mais informações sobre esses conceitos, consulte os seguintes tópicos:
    
      - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))
    
      - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir uma função de gerenciamento específica

Você pode exibir os detalhes de uma função específica recuperando uma função específica usando o cmdlet **Get-ManagementRole** e canalizando a saída para o cmdlet **Format-List**.

Para exibir detalhes de uma função específica, use a sintaxe a seguir.

```powershell
Get-ManagementRole <role name> | Format-List
```

Este exemplo recupera os detalhes sobre a função de gerenciamento de Destinatários de Email.

```powershell
Get-ManagementRole "Mail Recipients" | Format-List
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

## Listar todas as funções de gerenciamento

Você pode exibir uma lista de todas as funções de gerenciamento em sua organização executando o cmdlet **Get-ManagementRole**. Por padrão, o nome e o tipo de cada função são incluídos nos resultados.

Este exemplo retorna uma lista de todas as funções em sua organização.

```powershell
Get-ManagementRole
```

Para retornar uma lista de propriedades específicas para todas as funções em sua organização, você pode canalizar os resultados do cmdlet **Format-Table** e especificar as propriedades que quiser na lista de resultados. Use a sintaxe a seguir.

```powershell
Get-ManagementRole | Format-Table <property 1>, <property 2...>
```

Este exemplo retorna uma lista de todas as funções em sua organização e inclui a propriedade **Name** e qualquer propriedade com a palavra **Implicit** no começo do nome da propriedade.

    Get-ManagementRole | Format-Table Name, Implicit*

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

## Funções de gerenciamento de lista que contêm um cmdlet específico

Você pode retornar uma lista de funções que contenham um cmdlet especificado usando o parâmetro *Cmdlet* no cmdlet **Get-ManagementRole**.

Para retornar uma lista de funções que contenham o cmdlet especificado, use a sintaxe a seguir.

```powershell
Get-ManagementRole -Cmdlet <cmdlet>
```

Este exemplo retorna uma lista de funções que contenham o cmdlet **New-Mailbox**.

```powershell
Get-ManagementRole -Cmdlet New-Mailbox
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

## Listar funções de gerenciamento que contenham um parâmetro específico

Você pode retornar uma lista de funções que contenham um ou mais parâmetros especificados usando o parâmetro *CmdletParameters* no cmdlet **Get-ManagementRole**. Somente funções que contenham todos os parâmetros que você especificar serão retornadas.

Quando você usa o parâmetro *CmdletParameters*, pode optar por incluir o parâmetro *Cmdlet*. Se incluir o parâmetro *Cmdlet*, apenas funções que contenham os parâmetros que você especificar no cmdlet especificado serão retornadas. Se não incluir o parâmetro *Cmdlet*, funções que contenham os parâmetros que você especificar, independente do cmdlet em que estejam, serão retornadas.

Para retornar uma lista de funções que contenham os parâmetros que você especificar, use a sintaxe a seguir.

    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>

Este exemplo retorna uma lista de funções que contenham os parâmetros *Database* e *Server*, independente dos cmdlets em que existam.

```powershell
Get-ManagementRole -CmdletParameters Database, Server
```

Este exemplo retorna uma lista de funções nas quais o parâmetro *EmailAddresses* exista apenas no cmdlet **Set-Mailbox**.

```powershell
Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses
```

Você também pode usar o caractere curinga (\*) com os parâmetros *Cmdlet* ou *CmdletParameters* para corresponder parcialmente aos nomes de cmdlets ou parâmetros.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

## Listar as funções de gerenciamento de um tipo de função específico

Você pode retornar uma lista de funções baseadas em um tipo de função especificado usando o parâmetro *RoleType* no cmdlet **Get-ManagementRole**.

Para retornar uma lista de funções que correspondam ao tipo de função que você especificou, use a sintaxe a seguir.

```powershell
Get-ManagementRole -RoleType <roletype>
```

Este exemplo retorna uma lista de funções com base no tipo de função `UmMailboxes`.

```powershell
Get-ManagementRole -RoleType UmMailboxes
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

## Listar as funções filhas imediatas de uma função pai

Você pode retornar uma lista de funções que sejam filhas imediatas da função pai especificada usando o parâmetro *GetChildren* no cmdlet **Get-ManagementRole**. Somente funções que contenham a função que você especificar como função pai serão retornadas.

Para retornar uma lista de funções filhas imediatas de uma função pai, use a sintaxe a seguir.

```powershell
Get-ManagementRole <parent role name> -GetChildren
```

Este exemplo retorna uma lista de filhas imediatas da função Recuperação de Desastres.

```powershell
Get-ManagementRole "Disaster Recovery" -GetChildren
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

## Listar todas as funções filhas abaixo de uma função pai

Você pode retornar uma lista de toda a cadeia de funções de uma função pai especificada para a última função filha usando o parâmetro *Recurse* no cmdlet **Get-ManagementRole**. O parâmetro *Recurse* diz ao cmdlet **Get-ManagementRole** para vasculhar cada relação pai e filha que encontrar até atingir a última função filha. A função pai está incluída na lista que é retornada.

Este exemplo retorna uma lista de todas as funções filhas de uma função pai.

```powershell
Get-ManagementRole <parent role name> -Recurse
```

Este exemplo retorna todas as funções filhas da função Destinatários de Email.

```powershell
Get-ManagementRole "Mail Recipients" -Recurse
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRole](https://technet.microsoft.com/pt-br/library/dd351125\(v=exchg.150\)).

