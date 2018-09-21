---
title: 'Atualizar uma lista de endereços: Exchange 2013 Help'
TOCTitle: Atualizar uma lista de endereços
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 50485083
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: MT
---

# Atualizar uma lista de endereços

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-14_

Listas de endereços são uma coleção de destinatário e outros objetos do Active Directory. Você aplicar uma lista de endereços quando a regra de filtro de lista de endereços foi editada. Para atualizar a associação da lista de endereços para incluir novos destinatários e remover aqueles que não são mais atendam aos critérios de filtragem, você deve aplicar a lista de endereços.

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: esse processo pode levar muito tempo para concluir, dependendo do número de destinatários na lista de endereços.

  - Algumas listas de endereços contêm milhares ou dezenas de milhares de destinatários, dependendo do tamanho da organização e os filtros que você adicionou à lista de endereços. Atualizar as listas de endereços pode demorar até muitos dos recursos do computador. Portanto, convém atualizar a lista de endereços durante o horário de pico.

  - Se a lista de endereços contiver mais de 3.000 destinatários, é recomendável que você usar o Shell de gerenciamento do Exchange para atualizar a lista de endereços.

Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para atualizar uma lista de endereços

1.  Navegue até **Organização** \> **Listas de endereços**.

2.  Na exibição de lista, selecione a lista de endereços que você deseja atualizar.

3.  No painel de detalhes, clique em **Atualizar**.

## Use o Shell para atualizar uma lista de endereços

Este exemplo atualiza a lista de endereços do estado de Washington.

```powershell
Update-AddressList "Washington State"
```

Se você tiver mais de uma lista de endereços com o mesmo nome, você deve especificar o caminho completo para a lista de endereços que você deseja atualizar. Por exemplo, se você deseja atualizar a lista de endereços da América do Norte de vendas, mas há também uma lista de endereços de vendas na Europa, use o seguinte comando:

```powershell
Update-AddressList "North America\Sales"
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Update-AddressList](https://technet.microsoft.com/pt-br/library/aa997982\(v=exchg.150\)).

