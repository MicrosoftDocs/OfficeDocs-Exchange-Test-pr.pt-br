---
title: 'Criar um catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Criar um catálogo de endereços offline
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 50486426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: MT
---

# Criar um catálogo de endereços offline

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-04-24_

Um catálogo de endereços offline (OAB) no Exchange Server 2013 é uma cópia baixada de um catálogo de endereços que permite que um usuário do Outlook acessar as informações enquanto desconectado do servidor. Os administradores do Exchange podem decidir qual endereço manuais são disponibilizados aos usuários que trabalhar offline e elas também podem configurar o método pelo qual os catálogos de endereços são distribuídos (distribuição baseada na web ou distribuição de pasta pública).

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para criar um OAB com distribuição baseada na web

Este exemplo cria um OAB chamado OAB\_Contoso que usa a distribuição baseada na web para Outlook 2007 ou posteriores clientes usando o diretório virtual padrão.

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/bb123692\(v=exchg.150\)).

