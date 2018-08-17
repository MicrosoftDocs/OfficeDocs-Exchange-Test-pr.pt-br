---
title: 'Aplicar uma política de retenção a caixas de correio: Exchange 2013 Help'
TOCTitle: Aplicar uma política de retenção a caixas de correio
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 50485780
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicar uma política de retenção a caixas de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-10-01_

É possível usar as diretivas de retenção para agrupar uma ou mais marcas de retenção e aplicá-las a caixas de correio para impor configurações de retenção de mensagem. Uma caixa de correio não pode ter mais de uma diretiva de retenção.


> [!CAUTION]  
> As mensagens expiram com base nas configurações definidas nas marcas de retenção vinculadas à diretiva. Essas configurações incluem ações como a movimentação de mensagens para o arquivo morto ou a exclusão permanente. Antes de aplicar uma diretiva de retenção a uma ou mais caixas de correio, recomendamos a você testar a diretiva e inspecionar cada marca de retenção associada a ela.



Para outras tarefas de gerenciamento relacionadas ao gerenciamento de registros de mensagens (MRM), consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Aplicando diretivas de retenção" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para aplicar uma política de retenção a uma só caixa de correio

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  No modo de exibição de lista, selecione a caixa de correio à qual você deseja aplicar a política de retenção e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **Caixa de Correio de Usuário**, clique em **Recursos da caixa de correio**.

4.  Na lista **Política de retenção**, selecione a política que você deseja aplicar à caixa de correio e clique em **Salvar**.

## Usar o EAC para aplicar uma política de retenção a várias caixas de correio

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  No modo de exibição de lista, use as teclas Shift ou Ctrl, para selecionar várias caixas de correio.

3.  No painel de detalhes, clique em **Mais opções**.

4.  Em **Política de Retenção**, clique em **Atualizar**.

5.  Na lista **Política de Retenção de Atribuição em Massa**, selecione a política que você deseja aplicar às caixas de correio e clique em **Salvar**.

## Usar o Shell para aplicar uma diretiva de retenção a uma única caixa de correio

Este exemplo aplica a política de retenção RP-Finance à caixa de correio de Morris.

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Usar o Shell para aplicar uma política de retenção a várias caixas de correio

Este exemplo aplica a nova diretiva de retenção New-Retention-Policy a todas as caixas de correio que tenham a diretiva Old-Retention-Policy antiga.

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

Este exemplo aplica a política de retenção RetentionPolicy-Corp a todas as caixas de correio na organização do Exchange.

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

Este exemplo aplica a política de retenção RetentionPolicy-Corp a todas as caixas de correio na unidade organizacional Finance.

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) e [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você aplicou a política de retenção, execute o cmdlet [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) para recuperar a política de retenção para as caixas de correio.

Este exemplo recupera a política de retenção para caixa de correio de Morris.

    Get-Mailbox Morris | Select RetentionPolicy

Esse comando recupera todas as caixas de correio que têm a política de retenção RP-Finance aplicada.

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

