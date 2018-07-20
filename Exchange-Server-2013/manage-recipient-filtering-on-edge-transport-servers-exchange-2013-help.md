---
title: 'Gerenciar filtragem por destinatário nos servidores de transporte de borda: Exchange 2013 Help'
TOCTitle: Gerenciar filtragem por destinatário nos servidores de transporte de borda
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50486986
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar filtragem por destinatário nos servidores de transporte de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

A Filtragem de destinatário é fornecida pelo agente de Filtro de Destinatários. Quando a filtragem de destinatários é habilitada em um servidor do Exchange, ela filtra mensagens de entrada que vêm da Internet, mas não são autenticadas. Essas mensagens são manipuladas como mensagens externas.


> [!TIP]
> Embora o agente Filtro de Destinatários esteja disponíveis em servidores de caixas de correio, você não deve configurá-lo. Quando um filtro de destinatários, em um servidor de caixas de correio, detecta um destinatário inválido ou bloqueado em uma mensagem contendo outros destinatários válidos, a mensagem é rejeitada. Se você instalar o agente antispam em um servidor de caixas de correio, o agente Filtro de Destinatários será habilitado por padrão. Entretanto, ele não estará configurado para bloquear qualquer destinatário. Para obter mais informações, consulte <A href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Habilitar a funcionalidade anti-spam em servidores de caixa de correio</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - O parâmetro *AddressBookEnabled* no cmdlet **Set-AcceptedDomain** habilita ou desabilita a filtragem de destinatário para destinatários em um domínio aceito. Por padrão, a filtragem de destinatário está habilitada para domínios autoritativos e desabilitada para domínios de retransmissão internos e externos. Para exibir o status do parâmetro *AddressBookEnabled* para os domínios aceitos da sua organização, execute o seguinte comando:
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - Se você desabilitar a filtragem de destinatário usando o procedimento neste tópico, a funcionalidade de filtragem de destinatário será desabilitada, mas o agente de Filtro de Destinatário subjacente permanecerá habilitado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para habilitar ou desabilitar a filtragem de destinatários

Para desabilitar a filtragem por destinatário, execute o seguinte comando:

    Set-RecipientFilterConfig -Enabled $false

Para habilitar a filtragem por destinatário, execute o seguinte comando:

    Set-RecipientFilterConfig -Enabled $true


> [!TIP]
> Quando você desabilita a filtragem de destinatário, o agente de Filtro de Destinatário subjacente permanece habilitado ainda. Para desabilitar o agente do Filtro de Destinatário, execute o comando: <CODE>Disable-TransportAgent "Recipient Filter Agent"</CODE>.



## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a filtragem de destinatário, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para habilitar ou desabilitar a lista de Bloqueio de Destinatários

Execute o seguinte comando:

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

Este exemplo habilita a lista de Bloqueio de Destinatários:

    Set-RecipientFilterConfig -BlockListEnabled $true

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a lista de Bloqueio de Destinatários, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para configurar a lista de Bloqueio de Destinatários

Para substituir os valores existentes, execute o seguinte comando:

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

Este exemplo configura a lista de Bloqueio de Destinatários com valuesmark@contoso.com e kim@contoso.com:

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

Para adicionar ou remover entradas sem modificar quaisquer valores existentes, execute este comando:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

Este exemplo adiciona chris@contoso.com à lista de destinatários e remove michelle@contoso.com dessa lista na lista de Bloqueio de Destinatários:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## Como saber se funcionou?

Para verificar se você configurou com êxito a lista de Bloqueio de Destinatários, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  Verifique se os valores exibidos são os valores que você configurou.

## Usar o Shell para habilitar ou desabilitar a Pesquisa de Destinatário

Execute o seguinte comando:

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

Para bloquear mensagens recebidas por destinatários que não existem em sua organização, execute o seguinte comando:

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a Pesquisa de Destinatário, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  Verifique se o valor apresentado é o valor que você configurou.

