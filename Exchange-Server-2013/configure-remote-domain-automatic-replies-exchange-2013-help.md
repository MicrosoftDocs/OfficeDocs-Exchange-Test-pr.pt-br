---
title: 'Configurar as respostas automáticas de domínio remoto: Exchange 2013 Help'
TOCTitle: Configurar as respostas automáticas de domínio remoto
ms:assetid: 3d88a1fb-4b62-419a-a50d-ffd868e229d0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657720(v=EXCHG.150)
ms:contentKeyID: 50485369
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar as respostas automáticas de domínio remoto

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell de Gerenciamento do Exchange, para configurar o jeito como os emails são enviados e recebidos através dos domínios remotos. O exemplo a seguir demonstra como usar o Shell de Gerenciamento do Exchange para configurar o jeito como o Exchange trata as respostas automáticas.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Você só pode usar o Shell para executar esse procedimento.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios remotos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para configurar respostas automáticas

Você pode usar o cmdlet **Set-RemoteDomain** para configurar as propriedades de um domínio remoto.

Este exemplo permite respostas automáticas ao domínio remoto chamado Contoso. Essa configuração será desmarcada por padrão.

    Set-RemoteDomain Contoso -AutoReplyEnabled $true

Este exemplo permite respostas automáticas ao domínio remoto. Essa configuração será desmarcada por padrão.

    Set-RemoteDomain Contoso -AutoForwardEnabled $true

