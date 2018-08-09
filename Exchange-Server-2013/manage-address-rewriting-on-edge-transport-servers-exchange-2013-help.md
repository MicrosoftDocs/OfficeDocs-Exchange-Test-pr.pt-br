---
title: 'Reconfigurar endereço em servidores de transporte de borda: Exchange 2013 Help'
TOCTitle: Gerenciar a reconfiguração de endereço em servidores de transporte de borda
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060557
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar a reconfiguração de endereço em servidores de transporte de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Você usa o Shell de Gerenciamento do Exchange em um servidor Transporte de Borda para todas as tarefas de gerenciamento relacionadas à reconfiguração de endereço e dos agentes de reconfiguração de endereço. Para obter mais informações sobre a reconfiguração de endereço, consulte [Reconfiguração nos servidores de transporte de borda de endereço](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

Você pode criar entradas de reconfiguração de endereço que se apliquem a um único destinatário, a todos os destinatários em um domínio ou subdomínio específico ou a todos os recipientes em vários subdomínios. A reconfiguração de endereço pode ser somente de saída ou de entrada e saída (bidirecional). Quando você criar entradas de reconfiguração de endereço, lembre-se do seguinte:

  - Verifique se os endereços de email resultantes são exclusivos em sua organização.

  - Somente cadeias de caracteres literais têm suporte nos valores de endereço de email.

  - O caractere curinga (\*) só tem suporte nos endereços internos (os endereços que você deseja alterar). A sintaxe válida para o uso do caractere curinga é **\*.contoso.com**. Os valores **\*contoso.com** ou **sales.\*.com** não são permitidos.

  - Quando você usa o caractere curinga, precisa definir a reconfiguração de endereço como somente de saída (é preciso definir o parâmetro *OutboundOnly* com o valor `$true`).

  - Quando você define a reconfiguração de endereço somente de saída (configurando o parâmetro *OutboundOnly* com o valor `$true`), precisa configurar endereços de proxy nos destinatários afetados. Isso permite que o email enviado para o endereço de reconfiguração seja entregue corretamente.

  - Por padrão, a reconfiguração de endereço é bidirecional para destinatários únicos ou para todos os destinatários em um domínio ou subdomínio específico (o valor padrão para o parâmetro *OutboundOnly* é `$false`).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidores de Transporte de Borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Tenha cuidado ao definir a reconfiguração de endereço. Qualquer alteração será imediatamente aplicada quando o comando for executado. Considere a execução do comando com o parâmetro *WhatIf*. Para mais informações sobre o parâmetro *WhatIf*, consulte [Comutadores WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar a reconfiguração de endereço

Para habilitar ou desabilitar completamente a reconfiguração de endereço, habilite ou desabilite os agentes de reconfiguração de endereço. Por padrão, os agentes de reconfiguração de endereço em um servidor de Transporte de Borda estão habilitados.

Para desabilitar a reconfiguração de endereço, execute os seguintes comandos:

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

Para habilitar a reconfiguração de endereço, execute os seguintes comandos:

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a reconfiguração de endereço, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-TransportAgent

2.  Verifique se os valores da propriedade **Enabled** para Agente de Entrada de Reconfiguração de Endereço e para Agente de Saída de Reconfiguração de Endereço são os valores que você definiu.

## Usar o Shell para exibir entradas de reconfiguração de endereço

Para exibir uma lista de resumo de todas as entradas de reconfiguração de endereço, execute o comando a seguir.

    Get-AddressRewriteEntry

Para exibir detalhes de uma entrada de reconfiguração de endereço, use a sintaxe a seguir.

    Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List

O exemplo a seguir exibe os detalhes da entrada de reconfiguração de endereço chamada Rewrite Contoso.com to Northwindtraders.com (Reconfigurar Contoso.com como Northwindtraders.com):

    Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List

## Usar o Shell para criar entradas de reconfiguração de endereço

## Reconfigurar os endereços de email de recipientes únicos

Para reconfigurar o endereço de email para um único destinatário, use a seguinte sintaxe:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

O exemplo a seguir reconfigura o endereço de email de todas as mensagens que entram ou sarem da organização do Exchange para o destinatário joe@contoso.com. As mensagens de saída são reconfiguradas de forma que apareçam como vindas de support@nortwindtraders.com. As mensagens de entrada enviadas para support@northwindtraders.com são reconfiguradas para joe@contoso.com para entrega para o destinatário (o parâmetro *OutboundOnly* é `$false` por padrão).

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## Reconfigurar endereços de email para destinatários em um único domínio ou subdomínio

Para reconfigurar os endereços de email em um único domínio ou subdomínio, use a sintaxe a seguir:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

O exemplo a seguir reconfigura os endereços de email de todas as mensagens que entram e saem da organização do Exchange para destinatários no domínio contoso.com. As mensagens de saída são reconfiguradas de forma que parecem ter vindo do domínio fabrikam.com. Mensagens de entrada enviadas para endereços de email com fabrikam.com são reconfiguradas para contoso.com para entrega para os destinatários (o parâmetro *OutboundOnly* é `$false` por padrão).

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

O exemplo a seguir reconfigura os endereços de email de todas as mensagens que saem da organização do Exchange e são enviadas por destinatários no subdomínio sales.contoso.com. As mensagens de saída são reconfiguradas de forma que parecem ter vindo do domínio contoso.com. As mensagens de entrada enviadas para endereços de email da contoso.com não são reconfiguradas.

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## Reconfigurar todos os endereços de email para destinatários em vários subdomínios

Para reconfigurar os endereços de email para destinatários em um domínio e todos os subdomínios, use a sintaxe a seguir.

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

O exemplo a seguir reconfigura os endereços de email de todas as mensagens que saem da organização do Exchange e são enviadas por destinatários no domínio contoso.com e todos os subdomínios. As mensagens de saída são reconfiguradas de forma que parecem ter vindo do domínio contoso.com. Mensagens de entrada enviadas para destinatários de contoso.com não podem ser reconfiguradas porque um caractere curinga é usado no parâmetro *InternalAddress*.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

O exemplo a seguir é igual ao exemplo anterior, exceto que agora as mensagens enviadas por destinatários nos subdomínios legal.contoso.com e corp.contoso.com nunca são reconfiguradas:

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## Como saber se funcionou?

Para verificar se você criou entradas de reconfiguração de endereço com êxito, faça o seguinte:

1.  Execute o comando `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` e verifique se as configurações exibidas são as que você definiu.

2.  De uma caixa de correio afetada por uma entrada de reconfiguração de endereço, envie uma mensagem de teste para uma caixa de correio externa. Verifique se a mensagem de teste aparentemente se origina do endereço de email reconfigurado.

3.  Responda à mensagem de teste da caixa de correio externa. Verifique se que a caixa de correio original recebe a resposta.

## Usar o Shell para modificar entradas de reconfiguração de endereço

As opções de configuração disponíveis quando você modifica uma entrada de reconfiguração de endereço existente são idênticas às opções de configuração quando você cria uma nova entrada de reconfiguração de endereço.

## Modificar entradas de reconfiguração de endereço para destinatários únicos

Para modificar uma entrada de reconfiguração de endereço que reconfigure o endereço de email de um único destinatário, use a seguinte sintaxe:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

O exemplo a seguir modifica as seguintes propriedades da entrada de reconfiguração de endereço de destinatário único chamada "joe@contoso.com to support@nortwindtraders.com" (joe@contoso.com para support@nortwindtraders.com:

  - Altera o endereço externo para support@northwindtraders.net.

  - Altera o nome da entrada de reconfiguração de endereço para "joe@contoso.com to support@northwindtraders.net".

  - Altera o valor de *OutboundOnly* para `$true`. Observe que esta alteração exige que você configure support@northwindtraders.net como um endereço de proxy na caixa de correio de Joe.

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## Modificar entradas de reconfiguração de endereço para destinatários para domínios ou subdomínios únicos

Para modificar uma entrada de reconfiguração de endereço que reconfigure os endereços de email de destinatários para um único domínio ou subdomínio, use a sintaxe a seguir.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

O exemplo a seguir altera o valor de endereço interno da entrada de reconfiguração de endereço de domínio único chamada "Northwind Traders to Contoso" (Northwind Traders para Contoso).

    Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net

## Modificar entradas de reconfiguração de endereço para destinatários em vários subdomínios

Para modificar uma entrada de reconfiguração de endereço que reconfigure o endereço de email de destinatários em um domínio ou em todos os subdomínios, use a sintaxe a seguir.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

Para substituir os valores de lista de exceções existentes de uma entrada de reconfiguração de endereço de subdomínio, use a sintaxe a seguir:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

O exemplo a seguir substitui a lista de exceções existente para a entrada de reconfiguração de endereço de vários subdomínios chamada Contoso para Northwind Traders com os valores marketing.contoso.com e legal.contoso.com:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

Para adicionar ou remover seletivamente valores da lista de exceções de uma entrada de reconfiguração de endereço de vários subdomínios sem modificar qualquer valor de lista de exceções existente, use a seguinte sintaxe:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

O exemplo a seguir adiciona finance.contoso.com e remove marketing.contoso.com da lista de exceções da entrada de reconfiguração de endereço de vários subdomínios chamada Contoso para Northwind Traders:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## Como saber se funcionou?

Para verificar se você modificou com êxito uma entrada de reconfiguração de endereço, faça o seguinte:

1.  Execute o comando `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` e verifique se as configurações exibidas são as que você definiu.

2.  De uma caixa de correio afetada por uma entrada de reconfiguração de endereço, envie uma mensagem de teste para uma caixa de correio externa. Verifique se a mensagem de teste aparentemente se origina do endereço de email reconfigurado.

3.  Da caixa de correio externa, responda à mensagem de teste. Verifique se que a caixa de correio original recebe a resposta.

## Usar o Shell para remover entradas de reconfiguração de endereço

Para remover uma entrada de reconfiguração de endereço, use a sintaxe a seguir.

    Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>

O exemplo a seguir remove a entrada de reconfiguração de endereço chamada "Contoso.com to Northwindtraders.com" (Contoso.com para Northwindtraders.com):

    Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"

Para remover várias entradas de reconfiguração de endereço, use esta sintaxe:

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

O exemplo a seguir remove todas as entradas de reconfiguração de endereço:

    Get-AddressRewriteEntry | Remove-AddressRewriteEntry

O exemplo a seguir simula a remoção de entradas de reconfiguração de endereço que contenham o texto "to contoso.com" (para contoso.com) no nome. A opção *WhatIf* permite que você visualize o resultado sem confirmar nenhuma alteração.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

Se estiver satisfeito com a lista, execute o comando novamente sem a opção *WhatIf* para remover as entradas de reconfiguração de endereço.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## Como saber se funcionou?

Para verificar se você removeu com êxito uma entrada de reconfiguração de endereço, faça o seguinte:

1.  Execute o comando `Get-AddressRewriteEntry` e verifique se as entradas de reconfiguração de endereço que você removeu estão listadas.

2.  De uma caixa de correio afetada por uma entrada de reconfiguração de endereço, envie uma mensagem de teste para uma caixa de correio externa. Verifique se a mensagem de teste ainda é afetada pela entrada de reconfiguração de endereço removida.

3.  Da caixa de correio externa, responda à mensagem de teste. Verifique se a caixa de correio original recebe a resposta e se a mensagem que foi afetada pela entrada de reconfiguração de endereço removida.

