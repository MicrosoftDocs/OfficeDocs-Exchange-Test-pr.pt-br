---
title: 'Configurar propriedades da lista de endereços global: Exchange 2013 Help'
TOCTitle: Configurar propriedades da lista de endereços global
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 50485725
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar propriedades da lista de endereços global

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-12-16_

Esse tópico explica como modificar as configurações de uma lista global de endereços (GAL).

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Não é possível editar as configurações da GAL padrão.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para configurar as propriedades da GAL

Este exemplo atribui um novo nome, FourthCoffee, à GAL que tem o GUID 96d0c505-eba8-4103-ad4f-577a1bf4ad7b.

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee


> [!TIP]
> Se você estiver usando as propriedades de filtro condicional predefinidas, o valor do parâmetro <EM>IncludedRecipients</EM> não poderá permanecer em branco.



Este exemplo altera os destinatários que serão incluídos na GAL global Fourth Coffee para aqueles cuja empresa é definida como Fourth Coffee.

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Set-GlobalAddressList](https://technet.microsoft.com/pt-br/library/bb123877\(v=exchg.150\)).

