---
title: 'Remover uma lista de endereços global: Exchange 2013 Help'
TOCTitle: Remover uma lista de endereços global
ms:assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232077(v=EXCHG.150)
ms:contentKeyID: 50485747
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma lista de endereços global

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-12-16_

A lista de endereços global (GAL) é um diretório que contém entradas de todos os grupos, usuários e contatos de uma organização do Exchange.

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Não é possível remover a GAL padrão.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para remover uma GAL

Este exemplo remove a GAL Fourth Coffee do controlador de domínio ad-server.fourthcoffee.com.

    Remove-GlobalAddressList -Identity "Fourth Coffee" -DomainController ad-server.fourthcoffee.com

Para confirmar que deseja remover a GAL, digite **S** e pressione ENTER.

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Remove-GlobalAddressList](https://technet.microsoft.com/pt-br/library/bb124368\(v=exchg.150\)).

