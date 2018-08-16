---
title: 'Configurar distribuição do catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Configurar propriedades de distribuição do catálogo de endereços offline
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 50486091
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: MT
---

# Configurar propriedades de distribuição do catálogo de endereços offline

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-14_

Para cada ponto de distribuição de OAB (catálogo) de endereços offline no Exchange, você pode configurar duas URLs — uma URL interna que pode ser acessada apenas a partir de sua rede corporativa interna e uma URL externa que possa ser acessada pela Internet.

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para configurar as propriedades de distribuição do OAB

Este exemplo define o intervalo de polling para distribuição do OAB no diretório virtual do OAB OAB (Site padrão) para seis horas.

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

Este exemplo define o ponto de distribuição externa para https://contoso.com/OAB para o OAB diretório virtual padrão do OAB (Site padrão).

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-OabVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb124707\(v=exchg.150\)).

## Para Obter Mais Informações

[Catálogos de endereços offline](offline-address-books-exchange-2013-help.md)

