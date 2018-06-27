---
title: 'Alterar o catálogo de endereços offline padrão: Exchange 2013 Help'
TOCTitle: Alterar o catálogo de endereços offline padrão
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 50485732
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar o catálogo de endereços offline padrão

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

Por padrão, quando você instalar a função de servidor Caixa de Correio, um OAB padrão baseado na Web chamado Catálogo de Endereços Offline Padrão é criado. Você pode definir um OAB um sua própria organização do Exchange como o OAB padrão. Esse novo OAB padrão é associado a todos os bancos de dados de caixa de correio recém-criados. Você pode ter apenas um OAB padrão em sua organização. Se você excluir o OAB padrão, o MicrosoftExchange não atribuirá automaticamente outro OAB como padrão. Você deverá designar manualmente outro OAB como padrão.

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para alterar o OAB padrão

Este exemplo define o OAB denominado Meu OAB como OAB padrão.

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/aa996330\(v=exchg.150\)).

