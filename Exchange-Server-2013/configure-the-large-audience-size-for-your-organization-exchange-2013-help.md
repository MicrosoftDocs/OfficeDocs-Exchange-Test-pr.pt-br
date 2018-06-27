---
title: 'Configurar o tamanho grande público para sua organização: Exchange 2013 Help'
TOCTitle: Configurar o tamanho grande público para sua organização
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 50486112
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o tamanho grande público para sua organização

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-04-08_

É possível usar o Shell de Gerenciamento do Exchange para definir várias configurações sobre a forma como o MailTips será usado em sua organização.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Dicas de Email" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para configurar o tamanho grande público para sua organização

Você pode usar o cmdlet **Set-OrganizationConfig** para configurar o tamanho de grande público para sua organização. Quando os remetentes endereçar mensagens para destinatários mais do que o tamanho você configurar, que são mostrados a dica de email grande público. Por padrão, o tamanho grande público é definido como 25. Este exemplo configura o tamanho grande público para 50 em sua organização.

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

