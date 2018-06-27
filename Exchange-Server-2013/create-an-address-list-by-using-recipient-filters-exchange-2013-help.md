---
title: 'Criar uma lista de endereços usando filtros de destinatários: Exchange 2013 Help'
TOCTitle: Criar uma lista de endereços usando filtros de destinatários
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 50486103
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma lista de endereços usando filtros de destinatários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

Este tópico explica como criar uma lista de endereços usando filtros de destinatários. Para saber mais sobre listas de endereços, consulte [Listas de endereços](address-lists-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Para usar o parâmetro *RecipientFilter* para criar um filtro personalizado, você deve especificar uma cadeia de caracteres para o filtro. O Shell usa OPATH para a sintaxe de filtragem. OPATH é uma linguagem de consulta projetada para fontes de dados do objeto de consulta.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para criar uma lista de endereços usando filtros de destinatários

Este exemplo cria uma lista de endereços para todos os usuários com caixas de correio Exchange residentes em Washington ou Oregon.

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

Este exemplo cria uma lista de endereços para todos os usuários com caixas de correio Exchange que têm `AgencyB` como o valor do parâmetro *CustomAttribute15* .

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-AddressList](https://technet.microsoft.com/pt-br/library/aa996912\(v=exchg.150\)).

