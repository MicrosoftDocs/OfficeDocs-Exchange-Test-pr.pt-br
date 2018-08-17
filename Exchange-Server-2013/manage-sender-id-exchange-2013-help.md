---
title: 'Gerenciar o ID de remetente: Exchange 2013 Help'
TOCTitle: Gerenciar o ID de remetente
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 50485262
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar o ID de remetente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

A funcionalidade de ID de remetente é fornecida pelo agente ID do Remetente. A ID de Remetente valida a origem do email, verificando o endereço IP do remetente em relação ao proprietário alegado do domínio de remetente. A filtragem da ID de remetente é executada nas mensagens de entrada que vêm da Internet, mas não são autenticadas. Essas mensagens são manipuladas como mensagens externas.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar ID do Remetente

Para desabilitar a Identificação de Remetente, execute o seguinte comando:

    Set-SenderIDConfig -Enabled $false

Para habilitar a Identificação de Remetente, execute o seguinte comando:

    Set-SenderIDConfig -Enabled $true


> [!NOTE]
> Quando você desabilita a ID de Remetente, o agente de ID de Remetente subjacente permanece habilitado. Para desabilitar o agente de ID de Remetente, execute o comando: <CODE>Disable-TransportAgent "Sender ID Agent"</CODE>.



## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a ID de Remetente, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderIDConfig | Format-List Enabled

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para configurar a ação de ID do Remetente para mensagens falsificadas

Para configurar a ação da ID de Remetente para mensagens falsificadas, execute este comando:

    Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>

Este exemplo configura a ID de Remetente para rejeitar quaisquer mensagens em que o endereço IP do servidor de envio não esteja listado como servidor de envio SMTP autoritativo no registro de Estrutura de Política de Remetente (SPF) DNS para o domínio de envio.

    Set-SenderIDConfig -SpoofedDomainAction Reject

## Como saber se funcionou?

Para verificar se você configurou com êxito a ação da ID de Remetente para as mensagens falsificadas, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderIDConfig | Format-List SpoofedDomainAction

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para configurar a ação da ID de Remetente para erros transitórios

Para configurar a ação da ID de Remetente para erros transitórios, execute este comando:

    Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>

Este exemplo configura o agente da ID de Remetente para carimbar as mensagens para as quais o status da ID de Remetente não pode ser determinado devido a um erro temporário no servidor DNS. A mensagem será processada por outros agentes antispam e o agente Filtro de Conteúdo usará a marca ao determinar o valor SCL da mensagem.

    Set-SenderIDConfig -TempErrorAction StampStatus

Observe que `StampStatus` é o valor padrão para o parâmetro *TempErrorAction*.

## Como saber se funcionou?

Para verificar se você configurou com êxito a ação da ID de Remetente para erros transitórios, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderIDConfig | Format-List TempErrorAction

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para configurar exceções de domínio de destinatário e remetente

Para substituir os valores existentes, execute o seguinte comando:

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

Este exemplo configura o agente da ID de Remetente para ignorar a verificação da ID de Remetente para as mensagens enviadas para kim@contoso.com e john@contoso.com e para ignorar a verificação da ID de Remetente para mensagens enviadas do domínio fabrikam.com.

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

Para adicionar ou remover entradas sem modificar quaisquer valores existentes, execute este comando:

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Este exemplo configura o agente da ID de Remetente com as seguintes informações:

  - Adicionar chris@contoso.com e michelle@contoso.com à lista de destinatários existentes que ignoram a verificação da ID de Remetente.

  - Remover tailspintoys.com da lista de domínios existentes que ignoram a verificação da ID de Remetente.

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## Como saber se funcionou?

Para verificar se você configurou com êxito as exceções de domínios de destinatário e remetente, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains

2.  Verifique se os valores exibidos são os valores que você configurou.

