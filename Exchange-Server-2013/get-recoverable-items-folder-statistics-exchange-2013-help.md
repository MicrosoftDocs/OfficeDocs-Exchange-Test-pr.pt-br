---
title: 'Obtenha as estatísticas de pasta de itens recuperáveis: Exchange 2013 Help'
TOCTitle: Obtenha as estatísticas de pasta de itens recuperáveis
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52058894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Obtenha as estatísticas de pasta de itens recuperáveis

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-01-22_

A pasta itens recuperáveis contém itens excluídos pelo Microsoft Outlook e usuários do Microsoft OfficeOutlook Web App ou pelo Assistente de caixa de correio. A duração que itens excluídos permaneçam nesta pasta baseia-se as configurações de retenção de item excluído definidas para o banco de dados de caixa de correio ou a caixa de correio. Por padrão, um banco de dados de caixa de correio está configurado para reter itens excluídos 14 dias, e a cota de aviso de itens recuperáveis e a cota de itens recuperáveis são definidas como 20 gigabytes (GB) e 30 GB respectivamente. No entanto, se o bloqueio In-loco ou retenção de litígio estiver habilitada para a caixa de correio, os itens recuperáveis pasta pode acumular itens além do período de retenção especificado excluídos e também pode manter diferentes versões de itens de caixa de correio modificado.

Quando a pasta itens recuperáveis alcança a cota de aviso de itens recuperáveis, um evento de aviso é registrado no log de eventos do aplicativo. Se a caixa de correio não está em retenção de litígio, os itens, em seguida, são removidos no primeiro a entrar, base primeiro PEPS (). No entanto, se a caixa de correio está em retenção de litígio, a caixa de correio nunca é esvaziada e ao atingir a cota de itens recuperáveis, a funcionalidade de caixa de correio é afetada.

Portanto, é importante monitorar o log de eventos para alertas gerados quando caixas de correio alcançar as cotas de itens recuperáveis. Você também pode usar este procedimento para relatar estatísticas para a pasta itens recuperáveis, particularmente caixas de correio colocadas em retenção de litígio.

Para saber mais, consulte os seguintes tópicos:

  - [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md)

  - [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas de caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Você não pode usar o Centro de administração do Exchange (EAC) para obter as estatísticas de pasta de itens recuperáveis para uma caixa de correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## O que você deseja fazer?

## Obtenha as estatísticas de pasta de itens recuperáveis para uma caixa de correio

Este exemplo obtém as estatísticas de pasta para a pasta de itens recuperáveis de Soumya Singhi e exibe a saída em um formato de lista.

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List

Este exemplo obtém as estatísticas de pasta para a pasta de itens recuperáveis de Soumya Singhi e exibe o nome da pasta, o caminho da pasta, o número de itens da pasta, e o tamanho da pasta em um formato de tabela.

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-MailboxFolderStatistics](https://technet.microsoft.com/pt-br/library/aa996762\(v=exchg.150\)).

## Obtenha as estatísticas de pasta de itens recuperáveis para todas as caixas de correio em retenção de litígio

Este exemplo recupera uma lista de todas as caixas de correio colocadas em retenção de litígio e recupera as estatísticas de pasta de caixa de correio para a pasta itens recuperáveis e suas subpastas para cada caixa de correio. As propriedades de **FolderAndSubfolderSize** e **Identity** (identidade de pasta de caixa de correio) são exibidas em formato de tabela.

    Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) e [Get-MailboxFolderStatistics](https://technet.microsoft.com/pt-br/library/aa996762\(v=exchg.150\)).

## Obtenha a cota de itens recuperáveis para uma caixa de correio

Este exemplo exibe a cota e a cota de aviso para a pasta itens recuperáveis para uma caixa de correio do usuário. O exemplo também recupera informações sobre um litígio ou um bloqueio In-loco é colocado na caixa de correio.

    Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

Este exemplo exibe a cota e a cota de aviso para a pasta itens recuperáveis para todas as caixas de correio do usuário em sua organização. O exemplo também recupera informações sobre a isenção.

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

