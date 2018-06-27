---
title: 'Atualizar uma lista de endereços global: Exchange 2013 Help'
TOCTitle: Atualizar uma lista de endereços global
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 50485115
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Atualizar uma lista de endereços global

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

Use o Shell para atualizar uma GAL (lista de endereços global). A GAL é um diretório que contém entradas para todos os grupos, usuários e contatos em uma implementação da organização do Microsoft Exchange.

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para atualizar uma GAL

Este exemplo atualiza uma GAL para a empresa Fourth Coffee.


> [!TIP]
> A execução desse comando apenas inicia o processo de atualização. O processo de atualização da GAL pode demorar várias horas.



    Update-GlobalAddressList -Identity "Fourth Coffee"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Update-GlobalAddressList](https://technet.microsoft.com/pt-br/library/aa998806\(v=exchg.150\)).

