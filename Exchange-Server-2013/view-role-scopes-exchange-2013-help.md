---
title: 'Exibir escopos de função: Exchange 2013 Help'
TOCTitle: Exibir escopos de função
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 50484990
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir escopos de função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Os escopos de função de gerenciamento determinam quais objetos são disponibilizados a um usuário para que os objetos possam ser alterados por meio dos cmdlets e parâmetros associados a eles. É possível exibir escopos para determinar quais escopos foram adicionados à sua organização, a configuração de um escopo específico ou quais escopos são órfãos.

Para obter mais informações sobre os escopos de funções de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a escopos de função? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Escopos de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Este tópico usa pipelining e o cmdlet **Format-List**. Para mais informações sobre esses conceitos, consulte os seguintes tópicos:
    
      - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))
    
      - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir um escopo específico

Você pode exibir os detalhes de um escopo canalizando a saída do cmdlet **Get-ManagementScope** para o cmdlet **Format-List**.

Para exibir detalhes de um escopo específico, use a sintaxe a seguir.

    Get-ManagementScope <scope name> | Format-List

Este exemplo recupera os detalhes do escopo Servidores de Seattle.

    Get-ManagementScope "Seattle Servers" | Format-List

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementScope](https://technet.microsoft.com/pt-br/library/dd298180\(v=exchg.150\)).

## Listar todos os escopos

Este exemplo obtém uma lista de escopos na sua organização.

    Get-ManagementScope

Este cmdlet recupera escopos exclusivos e regulares. Se você só quiser retornar escopos exclusivos ou escopos regulares, consulte "Listar apenas os escopos exclusivos ou regulares" mais adiante neste tópico.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementScope](https://technet.microsoft.com/pt-br/library/dd298180\(v=exchg.150\)).

## Listar todos os escopos órfãos

*Escopos órfãos* são escopos que não foram associados a nenhuma atribuição de função de gerenciamento.

Este exemplo obtém uma lista de escopos órfãos.

    Get-ManagementScope -Orphan

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementScope](https://technet.microsoft.com/pt-br/library/dd298180\(v=exchg.150\)).

## Listar apenas os escopos exclusivos ou regulares

Por padrão, o cmdlet **Get-ManagementScope** retorna uma lista de escopos que contém escopos exclusivos e regulares. Se você quiser retornar apenas escopos exclusivos ou apenas escopos regulares, use a sintaxe a seguir.

    Get-ManagementScope -Exclusive < $true | $false >

Este exemplo retorna apenas os escopos exclusivos.

    Get-ManagementScope -Exclusive $true

Este exemplo retorna uma lista contendo apenas escopos regulares.

    Get-ManagementScope -Exclusive $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementScope](https://technet.microsoft.com/pt-br/library/dd298180\(v=exchg.150\)).

