---
title: 'Gerenciar filtragem de remetente: Exchange 2013 Help'
TOCTitle: Gerenciar filtragem de remetente
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 50486307
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar filtragem de remetente

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-08_

Filtragem de remetente é fornecido pelo agente de filtro de remetente. O agente Filtro de remetente depende do cabeçalho **MAIL FROM:** SMTP para determinar qual ação, se houver, para receber uma mensagem de email de entrada.

Quando a funcionalidade de filtragem de remetente está habilitada em um servidor Exchange, a funcionalidade de filtragem de remetente filtra todas as mensagens que vêm por meio de todos os conectores de recebimento no computador.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar a filtragem de remetente

Para desabilitar a filtragem de remetente, execute o seguinte comando:

    Set-SenderFilterConfig -Enabled $false

Para habilitar a filtragem de remetente, execute o seguinte comando:

    Set-SenderFilterConfig -Enabled $true


> [!TIP]
> Quando você desabilita a filtragem do remetente, o agente de filtro de remetente subjacente ainda está habilitado. Para desabilitar o agente Filtro de remetente, execute o comando: <CODE>Disable-TransportAgent "Sender Filter Agent"</CODE>.



## Como saber se funcionou?

Para verificar que você tiver com êxito habilitou ou desabilitou a filtragem do remetente, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderFilterConfig | Format-List Enabled

2.  Verifique se o valor apresentado é o valor que você configurou.

## Use o Shell para configurar remetentes bloqueados e domínios

Para substituir os valores existentes, execute o seguinte comando:

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

Este exemplo configura o agente Filtro de remetente para bloquear mensagens de kim@contoso.com e john@contoso.com, as mensagens do domínio fabrikam.com e mensagens do northwindtraders.com e todos os seus subdomínios.

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

Para adicionar ou remover entradas sem modificar quaisquer valores existentes, execute este comando:

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Este exemplo configura o agente Filtro de remetente com as seguintes informações:

  - Adicione chris@contoso.com e michelle@contoso.com à lista de remetentes existentes que são bloqueados.

  - Remova tailspintoys.com da lista de domínios existentes de remetentes bloqueados.

  - Adicione blueyonderairlines.com à lista de domínios existentes do remetente e subdomínios que são bloqueados.

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## Como saber se funcionou?

Para verificar se você configurou com êxito remetentes bloqueados, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  Verifique se os valores exibidos são os valores que você configurou.

## Usar o Shell para habilitar ou desabilitar o bloqueio de mensagens com remetentes em branco

Para habilitar ou desabilitar a mensagem de bloqueio com remetentes em branco, execute o seguinte comando:

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

Este exemplo configura o agente de filtro de remetente para bloquear mensagens que não especificar um remetente em MAIL FROM: comando SMTP:

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## Como saber se funcionou?

Para verificar que você com êxito habilitada ou desabilitada bloqueio mensagens com remetentes em branco, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  Verifique se o valor apresentado é o valor que você configurou.

