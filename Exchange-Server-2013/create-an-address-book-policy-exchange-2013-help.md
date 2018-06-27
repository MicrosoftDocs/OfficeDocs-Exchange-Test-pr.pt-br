---
title: 'Criar uma política de catálogo de endereços: Exchange 2013 Help'
TOCTitle: Criar uma política de catálogo de endereços
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 50485845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política de catálogo de endereços

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

Políticas de catálogo de endereços (ABPs) permitem segmentar usuários em grupos específicos para fornecer visualizações personalizadas da GAL (lista de endereços global) da sua organização. Ao criar uma ABP, atribua uma GAL, um OAB (catálogo de endereços offline), uma lista de salas e uma ou mais listas de endereços para a política. Você pode então atribuir a ABP para usuários de caixa de correio, fornecendo acesso a uma GAL personalizada no Outlook e Outlook Web App. O objetivo é fornecer um mecanismo mais simples para realizar segmentação GAL para as organizações locais que exigem várias GALs. Para saber mais sobre ABPs, consulte [Políticas de catálogo de endereços](address-book-policies-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a ABPs, consulte [Procedimentos de política de catálogo de endereços](address-book-policy-procedures-exchange-2013-help.md).

Interessado em cenários que utilizam este procedimento? Consulte [Cenário: Implantando políticas de catálogo de endereços](scenario-deploying-address-book-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de catálogos de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Criar um ABP para uma organização é um processo com múltiplas etapas que exige planejamento. Para mais informações, consulte [Cenário: Implantando políticas de catálogo de endereços](scenario-deploying-address-book-policies-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para criar ABPs. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Usar o Shell para criar uma ABP

Este exemplo cria uma ABP com as seguintes configurações:

  - **Nome:** All Fabrikam ABP

  - **GAL:** All Fabrikam

  - **OAB:** Fabrikam-All-OAB

  - **Lista de salas:** All Fabrikam Rooms

  - **Listas de endereços:** All Fabrikam, All Fabrikam Mailboxes, All Fabrikam DLs e All Fabrikam Contacts

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

Para informações detalhadas sobre sintaxes e parâmetros, consulte [New-AddressBookPolicy](https://technet.microsoft.com/pt-br/library/hh529913\(v=exchg.150\)).

## Para mais informações

[Atribuir uma política de catálogo de endereços para usuários de email](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

