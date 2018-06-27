---
title: 'Retenção local de uma caixa de correio em retenção: Exchange 2013 Help'
TOCTitle: Retenção local de uma caixa de correio em retenção
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 50485228
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Retenção local de uma caixa de correio em retenção

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2012-10-14_

Pôr uma caixa de correio em retenção suspende o processamento de uma diretiva de retenção ou diretiva de caixa de correio de pasta gerenciada para essa caixa de correio. A retenção foi feita para situações como férias ou ausência temporária de um usuário.

Durante a retenção, os usuários podem fazer logon em suas caixas de correio e alterar ou excluir itens. Ao realizar uma pesquisa de caixa de correio, os itens excluídos que estejam além do período de retenção de itens excluídos não são retornados nos resultados de pesquisa. Para se certificar de que itens alterados ou excluídos pelos usuários sejam preservados em cenários de retenção legal, coloque uma caixa de correio em retenção legal. Para mais informações, consulte [Criar ou remover um bloqueio In-loco](create-or-remove-an-in-place-hold-exchange-2013-help.md).

Você também pode incluir comentários de retenção nas caixas de correio que colocar em retenção legal. Os comentários são exibidos em versões com suporte do Microsoft Outlook.

Para outras tarefas de gerenciamento relacionadas ao gerenciamento de registros de mensagens (MRM), consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de registros de mensagens" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para colocar uma caixa de correio em retenção. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para pôr uma caixa de correio em retenção

Este exemplo coloca a caixa de correio de Michael Allen em retenção.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Usar o Shell para remover a retenção de uma caixa de correio

Este exemplo remove a retenção da caixa de correio de Michael Allen.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você colocou, com êxito, uma caixa de correio em retenção, use o cmdlet [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) para recuperar a propriedade *RetentionHoldEnabled* da caixa de correio.

Esse comando recupera a propriedade *RetentionHoldEnabled* da caixa de correio de Michael Allen.

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

Esse comando recupera todas as caixas de correio na organização do Exchange, filtra as caixas de correio que foram colocadas em retenção e as lista juntamente com a política de retenção aplicada a cada uma.


> [!IMPORTANT]
> Como <EM>RetentionHoldEnabled</EM> não é uma propriedade filtrável no Exchange 2013, você não pode usar o parâmetro <EM>Filter</EM> com o cmdlet <STRONG>Get-Mailbox</STRONG> para filtrar caixas de correio que foram colocadas em retenção no lado do servidor. Esse comando recupera uma lista de todas as caixas de correio e filtros no cliente funcionando na sessão do Shell. Em ambientes grandes com milhares de caixas de correio, esse comando pode demorar muito tempo para terminar.



    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

