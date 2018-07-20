---
title: 'Criar uma lista de endereços global: Exchange 2013 Help'
TOCTitle: Criar uma lista de endereços global
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 50485650
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma lista de endereços global

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-12-16_

A GAL (lista de endereços global) é um diretório que contém entradas para todos os grupos, usuários e contatos na implementação do Microsoft Exchange de uma organização. Se sua organização utiliza políticas de catálogo de endereços, você pode desejar criar listas de endereços globais (GALs) adicionais. Para saber mais, consulte [Políticas de catálogo de endereços](address-book-policies-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para criar uma GAL usando as propriedades de filtro condicional

Este exemplo cria uma GAL chamada GAL\_Contoso que inclui destinatários que sejam usuários da caixa de correio e tenham suas empresas listadas como Contoso.

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso


> [!TIP]
> Se você estiver usando propriedades de filtro condicional predefinidas, o parâmetro <EM>IncludedRecipients</EM> não poderá ficar em branco.



Para informações detalhadas sobre sintaxes e parâmetros, consulte [New-GlobalAddressList](https://technet.microsoft.com/pt-br/library/bb123785\(v=exchg.150\)).

## Usar o Shell para criar uma GAL usando um filtro de destinatário

Este exemplo cria uma GAL chamada GAL\_AgencyA que contém os destinatários para os quais o parâmetro *CustomAttribute15* tem um valor `AgencyA`.

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-GlobalAddressList](https://technet.microsoft.com/pt-br/library/bb123785\(v=exchg.150\)).

