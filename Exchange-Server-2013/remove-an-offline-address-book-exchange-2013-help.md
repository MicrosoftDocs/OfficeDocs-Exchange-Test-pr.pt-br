---
title: 'Remover um catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Remover um catálogo de endereços offline
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 50486756
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um catálogo de endereços offline

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-12-16_

Este tópico explica como remover um catálogo de endereços offline (OAB).

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Depois de remover um OAB que está vinculado a um usuário ou a um banco de dados de caixa de correio, o destinatário baixará o OAB padrão até que você atribua um novo OAB para esse usuário. Se você remover o OAB padrão, você deve atribuir um OAB diferente como o OAB padrão. Para obter instruções sobre como alterar o OAB padrão, consulte [Alterar o catálogo de endereços offline padrão](change-the-default-offline-address-book-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para remover um OAB

Este exemplo remove um OAB chamado Meu OAB.

    Remove-OfflineAddressBook -Identity "My OAB"

Digite **Y** para confirmar que você deseja remover o OAB e pressione ENTER.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/bb123594\(v=exchg.150\)).

