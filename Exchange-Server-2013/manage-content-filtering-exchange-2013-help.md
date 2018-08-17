---
title: 'Gerenciar filtragem de conteúdo: Exchange 2013 Help'
TOCTitle: Gerenciar filtragem de conteúdo
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 50484900
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar filtragem de conteúdo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Filtragem de conteúdo é fornecido pelo agente de Filtro de Conteúdo. O agente de Filtro de Conteúdo filtra todas as mensagens que chegam através de todos os conectores de Recebimento no servidor do Exchange. Somente mensagens provenientes de fontes não autenticadas são filtradas.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recurso antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para habilitar ou desabilitar a filtragem de conteúdo

Para desabilitar a filtragem de conteúdo, execute o seguinte comando:

    Set-ContentFilterConfig -Enabled $false

Para habilitar a filtragem de conteúdo, execute o seguinte comando:

    Set-ContentFilterConfig -Enabled $true


> [!NOTE]
> Quando você desabilita a filtragem de conteúdo, o agente de Filtro de Conteúdo subjacente permanece habilitado. Para desabilitar o agente do Filtro de Conteúdo, execute o comando: <CODE>Disable-TransportAgent "Content Filter Agent"</CODE>.



## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a filtragem de conteúdo, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List Enabled

2.  Verifique se o valor da propriedade *Enabled* é exibido.

## Usar o Shell para habilitar ou desabilitar a filtragem de conteúdo para mensagens externas

Por padrão, a funcionalidade de filtragem de conteúdo está habilitada para mensagens externas.

Para desabilitar a filtragem de conteúdo para mensagens externas, execute o seguinte comando:

    Set-ContentFilterConfig -ExternalMailEnabled $false

Para habilitar a filtragem de conteúdo para mensagens externas, execute o seguinte comando:

    Set-ContentFilterConfig -ExternalMailEnabled $true

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a filtragem de conteúdo para mensagens externas, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List ExternalMailEnabled

2.  Verifique o valor da propriedade *ExternalMailEnabled* que é mostrado.

## Usar o Shell para habilitar ou desabilitar a filtragem de conteúdo para mensagens internas

Como prática recomendada, você não deve filtrar mensagens de parceiros confiáveis ou de dentro da sua organização. Quando você executa filtros antispam, sempre há chance de que os filtros detectem falsos positivos. Para reduzir a chance de que os filtros tratem incorretamente emails legítimos, habilite agentes antispam para que sejam executados somente em mensagens de origens potencialmente não confiáveis ou desconhecidas.

Para habilitar a filtragem de conteúdo para mensagens internas, execute o seguinte comando:

    Set-ContentFilterConfig -InternalMailEnabled $true

Para desabilitar a filtragem de conteúdo para mensagens internas, execute o seguinte comando:

    Set-ContentFilterConfig -InternalMailEnabled $false

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a filtragem de conteúdo para mensagens internas, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List InternalMailEnabled

2.  Verifique o valor da propriedade *InternalMailEnabled* que é mostrado.

## Usar o Shell para configurar exceções de remetente e destinatário

Para substituir os valores existentes, execute o seguinte comando:

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

Este exemplo configura as seguintes exceções na filtragem de conteúdo:

  - As destinatárias laura@contoso.com e julia@contoso.com não são verificadas pela filtragem de conteúdo.

  - Os remetentes steve@fabrikam.com e cindy@fabrikam.com não são verificados pela filtragem de conteúdo.

  - Todos os remetentes no domínio nwtraders.com e todos os subdomínios não são verificados pela filtragem de conteúdo.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

Para adicionar ou remover entradas sem modificar quaisquer valores existentes, execute este comando:

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Este exemplo configura as seguintes exceções na filtragem de conteúdo:

  - Adicionar tiffany@contoso.com e chris@contoso.com à lista de destinatários existentes que não são verificados pela filtragem de conteúdo.

  - Adicionar joe@fabrikam.com e michelle@fabrikam.com à lista de remetentes existentes que não são verificados pela filtragem de conteúdo.

  - Adicionar blueyonderairlines.com à lista de domínios existentes cujos remetentes não são verificados pela filtragem de conteúdo.

  - Remover o domínio woodgrovebank.com e todos os subdomínios da lista de domínios existentes cujos remetentes não são verificados pela filtragem de conteúdo.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## Como saber se funcionou?

Para verificar se você configurou com êxito as exceções de destinatário e remetente, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  Verifique se os valores exibidos correspondem às configurações que você especificou.

## Usar o Shell para configurar frases permitidas e bloqueadas

Para adicionar frases e palavras permitidas e bloqueadas, execute o seguinte comando:

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

Este exemplo permite todas as mensagens que contenham a frase "comentário do cliente".

    Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"

Este exemplo bloqueia todas as mensagens que contenham a frase "dica de ações".

    Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"

Para remover frases permitidas ou bloqueadas, execute o seguinte comando:

    Remove-ContentFilterPhrase -Phrase <Phrase>

Este exemplo remove a frase "dica de ações":

    Remove-ContentFilterPhrase -Phrase "stock tip"

## Como saber se funcionou?

Para verificar se você configurou com êxito as frases permitidas e bloqueadas, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterPhrase | Format-List Influence,Phrase

2.  Verifique se os valores exibidos correspondem às configurações que você especificou.

## Usar o Shell para configurar limites de SCL

Para configurar os limites e as ações do nível de confiança de spam (SCL), execute este comando:

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>


> [!NOTE]
> A ação Excluir tem precedência sobre a ação Rejeitar, e a ação Rejeitar tem precedência sobre a ação Colocar em Quarentena. Assim, o limite do SCL para a ação Excluir deve ser maior do que o limite do SCL para a ação Rejeitar, que, por sua vez, deve ser maior do que o limite do SCL para a ação Colocar em Quarentena. Somente a ação Rejeitar é habilitada por padrão, e ela tem o valor limite de SCL de 7.



Este exemplo configura os seguintes valores para os limites de SCL:

  - A ação Excluir é habilitada, e o limite de SCL correspondente é definido para 9.

  - A ação Rejeitar é habilitada, e o limite de SCL correspondente é definido para 8.

  - A ação Colocar em Quarentena é habilitada, e o limite de SCL correspondente é definido para 7.

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## Como saber se funcionou?

Para verificar se você configurou com êxito os limites do SCL, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List SCL*

2.  Verifique se os valores exibidos correspondem às configurações que você especificou.

## Usar o Shell para configurar a resposta de rejeição

Quando a ação Rejeitar estiver habilitada, você poderá personalizar a resposta de rejeição que é enviada para o remetente da mensagem. A resposta à rejeição não pode exceder 240 caracteres.

Para configurar uma resposta de rejeição personalizada, execute o seguinte comando:

    Set-ContentFilterConfig -RejectionResponse "<Custom Text>"

Este exemplo configura o agente de Filtro de Conteúdo para enviar uma resposta de rejeição personalizada.

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## Como saber se funcionou?

Para verificar se você configurou com êxito a resposta de rejeição, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  Verifique se os valores exibidos correspondem às configurações que você especificou.

## Usar o Shell para habilitar ou desabilitar o Carimbo Postal do Outlook

A validação de *Carimbo Postal do Outlook* é uma prova computacional de que o Microsoft Outlook aplica às mensagens de saída para auxiliar os sistemas de mensagens a distinguir emails legítimos de lixo eletrônico. O Carimbo Postal está disponível no Outlook 2007 ou posterior. O Carimbo Postal ajuda a reduzir falsos positivos. O Carimbo Postal do Outlook está habilitado por padrão.

Para desabilitar o Carimbo Postal do Outlook, execute o seguinte comando:

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false

Para habilitar o Carimbo Postal do Outlook, execute o seguinte comando:

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true

## Como saber se funcionou?

Para verificar se você configurou com êxito o Carimbo Postal do Outlook, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled

2.  Verifique se o valor exibido corresponde às configurações que você especificou.

