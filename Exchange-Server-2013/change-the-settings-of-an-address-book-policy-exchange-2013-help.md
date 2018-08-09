---
title: 'Alterar configurações da política de catálogo de endereços: Exchange 2013 Help'
TOCTitle: Alterar as configurações de uma política de catálogo de endereços
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 50486491
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar as configurações de uma política de catálogo de endereços

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-03-30_

Depois de criar uma política de catálogo de endereços (ABP), você pode exibir ou modificar o nome e a lista atribuídas de endereços global (GAL), o catálogo de endereços offline (OAB), lista de salas e listas de endereços.

Para tarefas de gerenciamento adicionais relacionadas a ABPs, consulte [Procedimentos de política de catálogo de endereços](address-book-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de catálogos de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Criar uma ABP para uma organização é um processo de várias etapa que exige planejamento. Para obter mais informações, consulte [Cenário: Implantando políticas de catálogo de endereços](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - Você não pode usar o Centro de administração do Exchange (EAC) para configurar a ABPs. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## O que você deseja fazer?

## Alterar o OAB, lista de salas e GAL para uma ABP

Este exemplo altera o OAB, uma lista de salas e GAL que será usado pelos usuários de caixa de correio que estão atribuídos a ABP chamado todos Fabrikam ABP.

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## Substituir as listas de endereços em uma ABP

As listas de endereços que você especificar para uma ABP existente substituir todas as listas de endereços no ABP.

Este exemplo substitui as listas de endereços existente com as listas de endereços denominadas GovernmentAgencyA-Atlanta e GovernmentAgencyA-Moscow para a ABP chamado a órgão governamental.

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## Adicionar listas de endereços para uma ABP

Para preservar as listas de endereços que já estão definidas em uma ABP, é preciso especificar essas listas de endereços quando você adiciona novas para o ABP.

Este exemplo adiciona a lista de endereços chamada Contoso-Chicago para a ABP chamado Contoso ABP, que já está configurado para usar a lista de endereços chamada Contoso-Seattle.

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## Remover listas de endereços de uma ABP

Para remover as listas de endereços existente que já estão definidas em uma ABP, é necessário especificar as listas de endereços que você deseja manter.

Por exemplo, a ABP chamado Fabrikam ABP usa as listas de endereços chamadas Fabrikam-HR e Fabrikam-Finance. Para remover a lista de endereços da Fabrikam-HR a ABP, especifique a lista de endereços da Fabrikam-Finance que você deseja manter.

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## Para obter mais informações

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-AddressBookPolicy](https://technet.microsoft.com/pt-br/library/hh529945\(v=exchg.150\)).

