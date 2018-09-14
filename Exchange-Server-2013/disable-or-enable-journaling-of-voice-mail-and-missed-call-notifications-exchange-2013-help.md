---
title: 'Desabilitar/habilitar registro de notif. de chamada perdida e caixa postal'
TOCTitle: Desabilitar ou habilitar o registro no diário de notificações de chamada perdida e caixa postal
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 50485578
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar ou habilitar o registro no diário de notificações de chamada perdida e caixa postal

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

No Microsoft Exchange Server 2013, quando você cria uma regra de diário para mensagens de e-mail de diário enviadas para ou de destinatários ou remetentes em uma organização do Exchange, notificações de correio de voz e chamadas não atendidas que são geradas pelo serviço de Unificação de Mensagens são incluídas. Use os procedimentos neste tópico para ativar ou desativar esse recurso para toda a sua organização.

Procurando outras tarefas de gerenciamento relacionadas a registro no diário? Consulte [Gerenciar diário](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/journaling/manage-journaling).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em diário" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para desabilitar ou habilitar o registro no diário de notificações de correio de voz e chamadas não atendidas

Este exemplo desabilita o registro no diário de notificações de caixa postal e chamadas perdidas com a configuração do parâmetro *VoicemailJournalingEnabled* para `$false`.

    Set-TransportConfig -VoicemailJournalingEnabled $false

Este exemplo habilita o registro no diário de notificações de correio de voz e chamadas não atendidas pela configuração do mesmo parâmetro como `$true`.

    Set-TransportConfig -VoicemailJournalingEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-TransportConfig](https://technet.microsoft.com/pt-br/library/bb124151\(v=exchg.150\)).

## Para Obter Mais Informações

[Registro no Diário](journaling-exchange-2013-help.md)

[Gerenciar diário](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/journaling/manage-journaling)

