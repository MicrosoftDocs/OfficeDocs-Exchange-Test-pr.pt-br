---
title: 'Atualização de um catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Atualização de um catálogo de endereços offline
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 50485485
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualização de um catálogo de endereços offline

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-11-15_

Depois de criar um OAB ou modificar as configurações de OAB, as alterações não estarão disponíveis para usuários até que o processo de geração de OAB (OABGen) tenha sido concluído.

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para atualizar um OAB

Este exemplo atualiza o OAB chamado Meu OAB.

    Update-OfflineAddressBook -Identity "My OAB"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Update-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/aa995979\(v=exchg.150\)).

