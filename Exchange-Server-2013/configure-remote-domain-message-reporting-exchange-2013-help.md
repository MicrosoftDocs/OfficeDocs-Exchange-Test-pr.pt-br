---
title: 'Configurar os relatórios de mensagem do domínio remoto: Exchange 2013 Help'
TOCTitle: Configurar os relatórios de mensagem do domínio remoto
ms:assetid: 73dc686a-e7a3-44c7-b82f-f52ff9273199
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649325(v=EXCHG.150)
ms:contentKeyID: 50485817
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar os relatórios de mensagem do domínio remoto

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell de gerenciamento do Exchange para configurar o modo como os emails são enviados e recebidos por meio de domínios remotos. A seguir demonstra como usar o Shell de gerenciamento do Exchange configure a maneira Exchange alças entrega e relatórios de falha na entrega.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Você só pode usar o Shell para executar esse procedimento.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios remotos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para configurar os relatórios de mensagem

Você pode usar o cmdlet **Set-RemoteDomain** para configurar as propriedades de um domínio remoto.

Este exemplo desabilita as notificações de entrega para o domínio remoto chamado Contoso. Essa configuração estiver habilitada por padrão.

    Set-RemoteDomain Contoso -DeliveryReportEnabled $false

Este exemplo desabilita relatórios de entrega para o domínio remoto. Essa configuração estiver habilitada por padrão.

    Set-RemoteDomain Contoso -NDREnabled $false

