---
title: 'Alterar o agendamento de geração do catálogo de endereços offline'
TOCTitle: Alterar o agendamento de geração do catálogo de endereços offline
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 50486713
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# Alterar o agendamento de geração do catálogo de endereços offline

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-12-05_

Um catálogo de endereços offline (OAB) é uma cópia de um catálogo de endereços que tenha sido baixado, para que um usuário do Outlook possa acessar as informações que ele contém enquanto desconectado do servidor. Você pode configurar a frequência com que o OAB é gerado usando os parâmetros *OABGeneratorWorkCycle* e *OABGeneratorWorkCycleCheckpoint* no cmdlet Set-MailboxServer.

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para executar este procedimento. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para configurar as propriedades do OAB

Neste exemplo, o catálogo de endereços offline é gerado a cada seis horas por dia no servidor de caixa de correio, MBXServer01.

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/pt-br/library/aa996330\(v=exchg.150\)).

