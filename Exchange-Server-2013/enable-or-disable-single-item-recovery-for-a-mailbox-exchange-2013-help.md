---
title: 'Habilitar ou desabilitar a recuperação de item único para uma caixa de correio: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar a recuperação de item único para uma caixa de correio
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54651935
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar a recuperação de item único para uma caixa de correio

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-13_

Você pode usar o Shell para habilitar ou desabilitar a recuperação de item único em uma caixa de correio. No Exchange Online, a recuperação de item único é habilitada por padrão quando uma nova caixa de correio é criada. No Exchange 2013, a recuperação de item único é desabilitada quando uma caixa de correio é criada. Se a recuperação de item único está habilitada, as mensagens que são permanentemente excluídas (purgadas) pelo usuário são mantidas na pasta itens recuperáveis da caixa de correio até que o período de retenção de item excluído expire. Isso permite que um administrador recuperar mensagens limpas pelo usuário antes que o período de retenção de item excluído expire. Além disso, se uma mensagem for alterada por um usuário ou um processo, cópias do item original também são mantidas quando a recuperação de item único está habilitada.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "E os armazenamentos legais de retenção" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Você não pode usar o Centro de administração do Exchange (EAC) para habilitar ou desabilitar a recuperação de item único.

  - Em Exchange Online, o período de retenção de item excluído é definido para 14 dias, por padrão. Você pode alterar essa configuração para um máximo de 30 dias. Para obter detalhes, consulte [Alterar quanto tempo os itens permanentemente excluídos são mantidos em uma caixa de correio do Exchange Online](https://technet.microsoft.com/pt-br/library/dn163584\(v=exchg.150\))

  - Em Exchange 2013, a caixa de correio usa as configurações de retenção de item excluído do banco de dados de caixa de correio, por padrão. O período de retenção de item excluído de um banco de dados de caixa de correio é definido como 14 dias, mas você pode substituir o padrão, a definição dessa configuração em uma base por caixa de correio. Para obter detalhes, consulte [Configurar cotas de itens recuperáveis e retenção de Item excluído](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Use o Shell para habilitar a recuperação de item único

Este exemplo habilita a recuperação de item único para a caixa de correio de Summers de abril.

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

Este exemplo habilita a recuperação de item único para a caixa de correio de Pilar Pinilla e define o número de dias que os itens excluídos é mantido como 30 dias.

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Este exemplo habilita a recuperação de item único para todas as caixas de correio do usuário na organização.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

Este exemplo habilita a recuperação de item único para todas as caixas de correio do usuário na organização e define o número de dias que os itens excluídos é mantido como 30 dias

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Usar o Shell para desabilitar a recuperação de item único

Talvez seja necessário desabilitar a recuperação de item único para caixas de correio do usuário. Por exemplo, antes de poder usar **Search-Mailbox –DeleteContent** para excluir permanentemente o conteúdo de uma caixa de correio, você precisa desabilitar a recuperação de item único. Para obter mais informações, consulte [Pesquisar e excluir mensagens - ajuda de Admin](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

Este exemplo desabilita a recuperação de item único para a caixa de correio de Ayla Kol.

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## Como saber se funcionou?

Para verificar que você habilitou a recuperação de item único para uma caixa de correio e exibir o valor de quanto tempo os itens excluídos serão mantidos (em dias), execute o seguinte comando.

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

Você pode usar esse mesmo comando para verificar se a recuperação de item único está desabilitada para uma caixa de correio.

## Mais informações

  - Para saber mais sobre a recuperação de item único, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md). Para recuperar mensagens limpas pelo usuário antes do período de retenção de item excluído expira, consulte [Recuperar mensagens excluídas na caixa de correio de um usuário](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

  - Se uma caixa de correio for colocada em retenção In-loco ou retenção de litígio, as mensagens na pasta itens recuperáveis são mantidas até que a duração da retenção expira. Se a duração da retenção for ilimitada, itens são mantidos até que a suspensão seja removida ou a duração da retenção é alterada.

