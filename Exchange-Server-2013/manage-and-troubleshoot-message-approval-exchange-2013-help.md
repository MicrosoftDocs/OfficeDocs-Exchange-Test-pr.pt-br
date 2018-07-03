---
title: 'Gerenciar e solucionar problemas de aprovação de mensagens: Exchange 2013 Help'
TOCTitle: Gerenciar e solucionar problemas de aprovação de mensagens
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52058852
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar e solucionar problemas de aprovação de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode receber o seguinte erro quando você tentar remover uma caixa de correio de arbitragem:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Não é possível remover a caixa de correio de arbitragem &lt;<em>mailbox</em>&gt; porque está sendo usado no fluxo de trabalho de aprovação para destinatários existentes que têm restrições de associação ou moderação habilitado. Você deve desativar os recursos de aprovação nesses destinatários ou especificar uma caixa de correio de arbitragem diferentes para os destinatários antes de remover esta caixa de correio de arbitragem.</p></td>
</tr>
</tbody>
</table>


Uma caixa de correio de arbitragem pode ser usada para lidar com o fluxo de trabalho de aprovação para destinatários moderados e aprovações de associação de grupo de distribuição. Usar o PowerShell para localizar todos os destinatários estão configurados para usar a caixa de correio de arbitragem. Depois de identificar os destinatários, você pode configurá-las para usar uma caixa de correio de arbitragem diferentes, ou você pode desabilitar a moderação para eles.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Aribtration" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Etapa 1: Usar o Shell para localizar todos os destinatários que usam a caixa de correio de arbitragem que você está tentando excluir

Execute os seguintes comandos:

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

Por exemplo, para localizar todos os destinatários que usam a caixa de correio de arbitragem denominada arbitragem Mailbox01, execute os seguintes comandos:

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}


> [!TIP]
> A caixa de correio de arbitragem é especificada usando o nome diferenciado (DN). Se você souber o DN da caixa de correio de arbitragem, você pode executar o comando único: <CODE>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</CODE>.



## Etapa 2: Usar o Shell para especificar uma caixa de correio de arbitragem diferentes ou desabilitar a moderação para os destinatários

Para evitar que os destinatários moderados que usa a caixa de correio de arbitragem que você está tentando excluir, você pode especificar uma caixa de correio de arbitragem diferentes ou é possível desabilitar a moderação para os destinatários.

Se você optar por especificar uma caixa de correio de arbitragem diferentes para os destinatários, execute o seguinte comando:

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

Por exemplo, para reconfigurar o grupo de distribuição chamado todos os funcionários a empregar a caixa de correio de arbitragem denominada Mailbox02 arbitragem para aprovação de associação, execute o seguinte comando:

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

Se você optar por desabilitar moderação para os destinatários, execute o seguinte comando:

    Set-<RecipientType> <Identity> -ModerationEanbled $false

Por exemplo, para desabilitar a moderação para a caixa de correio denominada recursos humanos, execute o seguinte comando:

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## Como saber se funcionou?

O procedimento foi bem-sucedida, se você pode excluir a caixa de correio de arbitragem sem receber o erro que está sendo usado.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

