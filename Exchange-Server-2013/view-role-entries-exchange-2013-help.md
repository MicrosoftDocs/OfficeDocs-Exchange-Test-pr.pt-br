---
title: 'Exibir entradas de função: Exchange 2013 Help'
TOCTitle: Exibir entradas de função
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 50486767
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir entradas de função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Cada entrada da função de gerenciamento representa um único cmdlet ou script. Os parâmetros incluídos em uma entrada de função determinam quais parâmetros do cmdlet ou um script que um usuário pode acessar.

A identidade de entradas de função consiste no nome da função de gerenciamento que a entrada de função é associada, e o script a entrada de função referente à ou o cmdlet. Para obter mais informações sobre entradas de função no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas às entradas de função? Confira [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Este tópico faz uso de canalização, o cmdlet **Format-List** , objetos e propriedades. Para obter mais informações sobre esses conceitos, consulte os tópicos a seguir:
    
      - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))
    
      - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)
    
      - [Dados estruturados](https://technet.microsoft.com/pt-br/library/aa996386\(v=exchg.150\))

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir uma lista de entradas de função

Você pode usar o cmdlet **Get-ManagementRoleEntry** para recuperar uma lista de entradas de função. Quando você usa o cmdlet **Get-ManagementRoleEntry** , você deve especificar um valor que contém tanto o nome da função que contém as entradas de função que você deseja a lista e também o nome do cmdlet da entrada da função que você deseja listar. Combinando o nome de função e o nome do cmdlet com o caractere curinga (\*), você pode retornar listas extensas ou específicas de entradas de função.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)).

## Exibir uma lista de todas as entradas de função em uma função

Para exibir uma lista de entradas de função em uma função específica, use a seguinte sintaxe.

    Get-ManagementRoleEntry <role name>\*

Este exemplo recupera todas as entradas de função na função `Recipient Administrators` .

    Get-ManagementRole "Recipient Administrators\*"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)).

## Exibir uma lista das funções que contêm uma entrada de função específica

Para exibir uma lista de todas as funções que contêm uma entrada de função específica, use a seguinte sintaxe.

    Get-ManagementRoleEntry *\<cmdlet name>

Este exemplo recupera todas as funções que contêm a entrada da função **Set-Mailbox** .

    Get-ManagementRoleEntry *\Set-Mailbox

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)).

## Exibir uma lista de funções que contêm entradas de função semelhante alvo

Para exibir uma lista das funções de destino que contêm cmdlets com nomes semelhantes, use a seguinte sintaxe.

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

Este exemplo retorna uma lista de entradas de função que contêm a cadeia de caracteres `Mailbox` que estão em funções que contêm a cadeia de caracteres `Tier 1` em seus nomes.

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)).

## Exibir uma entrada de função única

Para exibir os detalhes de uma entrada de função única, use a seguinte sintaxe.

    Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List

Este exemplo recupera os detalhes da entrada da função **Set-Mailbox** na função `Recipient Administrators` .

    Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List

Se a entrada de função que você exibir tiver muitos parâmetros para listar usando o cmdlet **Format-List** , consulte "Exibir os parâmetros em uma entrada de função única" neste tópico.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)).

## Exibir os parâmetros em uma entrada de função única

Algumas entradas de função têm mais parâmetros do que podem ser exibidos, Canalizando os resultados do cmdlet **Get-ManagementRoleEntry** para o cmdlet **Format-List** . Se você precisar exibir todos os parâmetros em uma entrada de função, você precisa acessar diretamente a propriedade **Parameters** do objeto de entrada de função.

Para exibir os parâmetros armazenados na propriedade **Parameters** de um objeto de entrada de função, use a seguinte sintaxe.

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

Este exemplo recupera os parâmetros de entrada da função **Set-Mailbox** na função destinatários de email.

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd335210\(v=exchg.150\)).

