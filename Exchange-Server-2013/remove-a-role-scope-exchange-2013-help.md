---
title: 'Remover um escopo de função: Exchange 2013 Help'
TOCTitle: Remover um escopo de função
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 50486369
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um escopo de função

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-02_

Escopos da função de gerenciamento determinam quais objetos são disponibilizados para um usuário que poderá alterar os objetos usando os cmdlets e parâmetros atribuídos ao usuário. Se você não estiver usando um escopo, ele pode ser removido. Para obter mais informações sobre escopos da função de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Escopos de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Antes de poder remover um escopo, você deve remover o escopo de quaisquer atribuições de função de gerenciamento que podem ser utilizá-lo. Para obter mais informações sobre como remover um escopo de uma atribuição de função, consulte [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para remover um escopo

Para remover um escopo, use a seguinte sintaxe.

    Remove-ManagementScope <scope name>

Por exemplo, para remover o escopo de "Servidores de Dublin", use o seguinte comando.

    Remove-ManagementScope "Dublin Servers"

