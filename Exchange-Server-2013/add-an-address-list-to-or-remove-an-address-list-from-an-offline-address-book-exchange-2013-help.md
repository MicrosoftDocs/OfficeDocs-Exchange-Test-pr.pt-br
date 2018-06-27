---
title: 'Adicionar uma lista de endereços para ou remover uma lista de endereços do catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Adicionar uma lista de endereços para ou remover uma lista de endereços do catálogo de endereços offline
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 50486076
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar uma lista de endereços para ou remover uma lista de endereços do catálogo de endereços offline

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

Você pode usar o Shell para adicionar ou remover uma lista de endereços do catálogo de endereços offline (OAB). Por padrão, não há um OAB chamado padrão catálogo de Endereços Offline que contém a lista de endereços global (GAL). OABs são geradas com base em listas de endereços que elas contêm. Para criar os OABs personalizados que os usuários podem baixar, é possível adicionar ou remover listas de endereços de OABs.

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Alterações feitas na lista de endereços não estão disponíveis para download do cliente, até após o OAB no qual reside a lista de endereços foi gerado. Para obter mais informações, consulte [Atualização de um catálogo de endereços offline](update-an-offline-address-book-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para adicionar uma lista de endereços para um OAB

Ao usar o parâmetro *AddressLists* , quaisquer listas de endereços que existem atualmente serão substituídas. Quando você usa o parâmetro *AddressLists* para continuar a gerar as listas de endereços em seu OAB, você deve incluir as listas de endereços existente. Neste exemplo, nos quais você tem AddressList1 e AddressList2, adiciona AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/aa996330\(v=exchg.150\)).

## Use o Shell para remover uma lista de endereços de um OAB

Para remover uma lista de endereços de um OAB, omita essa lista de endereços da lista de listas de endereços. Neste exemplo, nos quais você tem AddressList1, AddressList2 e AddressList3, remove AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/aa996330\(v=exchg.150\)).

