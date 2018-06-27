---
title: 'Remover uma lista de endereços: Exchange 2013 Help'
TOCTitle: Remover uma lista de endereços
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 50485388
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma lista de endereços

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-14_

Este tópico explica como remover uma lista de endereços. Você não pode remover a lista de endereços global padrão (GAL).

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de Endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Não é possível remover uma lista de endereços pai que contenha listas de endereços filhas. No entanto, você pode remover as listas de endereços pai e filhas pressionando a tecla CTRL e selecionando essas listas. Se tentar remover uma lista de endereços pai sem remover as listas de endereços filhas, você receberá um erro.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para remover uma lista de endereços

1.  Navegue até **Organização** \> **Listas de endereços**.

2.  No modo de exibição de lista, selecione a lista de endereços que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  No aviso, clique em **Sim** para remover a lista de endereços.

## Usar o Shell para remover uma lista de endereços

Este exemplo remove a lista de endereços Sales Department, que não contém listas de endereços filhas.

    Remove-AddressList -Identity "Sales Department"

Digite **S** para confirmar que você deseja remover essa lista de endereços e pressione ENTER.

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Remove-AddressList](https://technet.microsoft.com/pt-br/library/bb124342\(v=exchg.150\)).

## Usar o Shell para remover uma lista de endereços que contenha listas de endereços filhas

Este exemplo remove a lista de endereços pai Departments e todas as suas listas de endereços filhas.

    Remove-AddressList -Identity Departments -Recursive

Digite **S** para confirmar que você deseja remover a lista de endereços pai e suas listas de endereços filhas e pressione ENTER.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-AddressList](https://technet.microsoft.com/pt-br/library/bb124342\(v=exchg.150\)).

