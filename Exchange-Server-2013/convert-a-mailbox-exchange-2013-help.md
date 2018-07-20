---
title: 'Converter uma caixa de correio: Exchange Online Help'
TOCTitle: Converter uma caixa de correio
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 50486810
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Converter uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-04-26_

Converter uma caixa de correio em um tipo diferente de caixa de correio é muito semelhante à experiência no Exchange 2010. Você ainda deve usar o cmdlet Set-Mailbox no Shell para fazer a conversão.

Você pode converter as seguintes caixas de correio de um tipo para outro:

  - Caixa de correio do usuário em caixa de correio de recurso (sala ou equipamento)

  - Caixa de correio compartilhada em caixa de correio do usuário

  - Caixa de correio compartilhada em caixa de correio de recurso

  - Caixa de correio de recurso em caixa de correio do usuário

  - Caixa de correio de recurso em caixa de correio compartilhada

Se a sua organização usa um ambiente híbrido do Exchange, você precisa gerenciar suas caixas de correio usando as ferramentas de gerenciamento do Exchange local. Para converter uma caixa de correio em um ambiente híbrido, talvez seja necessário mover a caixa de correio de volta para o Exchange local, converter o tipo de caixa de correio e movê-la novamente para o Office 365.


> [!IMPORTANT]
> Se você está convertendo uma caixa de correio do usuário em uma caixa de correio compartilhada, remova todos os dispositivos móveis da caixa de correio antes da conversão ou bloqueie o acesso móvel à caixa de correio após a conversão. De fato, depois que a caixa de correio é convertida em uma caixa de correio compartilhada, a funcionalidade móvel não ocorre adequadamente. Confira mais informações sobre o bloqueio de acesso em <A href="https://go.microsoft.com/fwlink/p/?linkid=847873">Remover um antigo funcionário do Office 365</A>.



## Usar o Shell para converter um caixa de correio

Tempo estimado para conclusão: 5 minutos.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

Este exemplo converte a caixa de correio compartilhada MarketingDepartment1 em uma caixa de correio de usuário.

    Set-Mailbox MarketingDept1 -Type Regular

Você pode usar os seguintes valores para o parâmetro *Type*

  - Regular

  - Sala

  - Equipment

  - Compartilhado

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se converteu com êxito a caixa de correio, execute o seguinte comando do Shell:

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

O valor de *RecipientTypeDetails* deve ser *UserMailbox*.

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


