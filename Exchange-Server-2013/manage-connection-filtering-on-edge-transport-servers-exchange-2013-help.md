---
title: 'Gerenciar filtragem de conexão em servidores de transporte de borda'
TOCTitle: Gerenciar nos servidores de transporte de borda de filtragem de Conexão
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60829939
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar nos servidores de transporte de borda de filtragem de Conexão

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

A filtragem de conexão é um recurso antispam fornecido pelo agente Filtragem de Conexão, que só é disponibilizado em servidores de Transporte de Borda no Microsoft Exchange 2013. A filtragem de conexão habilita os seguintes recursos:

  - Lista de Bloqueios de IP

  - Provedores de Lista de Bloqueios de IP

  - Lista de Permissões de IP

  - Provedores de Lista de Permissões de IP

Cada um desses recursos pode ser habilitado ou desabilitado separadamente.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para habilitar ou desabilitar a filtragem de conexão

Para habilitar ou desabilitar completamente a filtragem de conexão, habilite ou desabilite o agente Filtragem de Conexão. A alteração é efetivada depois de reiniciado o serviço de Transporte do Microsoft Exchange. Quando você reinicia o serviço de Transporte do Microsoft Exchange em um servidor de Transporte de Borda, o fluxo de mensagens no servidor é temporariamente interrompido.

Para desabilitar a filtragem de conexão, execute o seguinte comando:

```powershell
Disable-TransportAgent "Connection Filtering Agent"
```

Para habilitar a filtragem de conexão, execute o seguinte comando:

```powershell
Enable-TransportAgent "Connection Filtering Agent"
```

Para aplicar a alteração, reinicie o serviço de Transporte do Microsoft Exchange executando este comando:

```powershell
Restart-Service MSExchangeTransport
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito a filtragem de conexão, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled
```

## Procedimentos da lista de IPs Bloqueados

Esses procedimentos aplicam-se à lista de IPs Bloqueados que você configura manualmente. Eles não se aplicam aos provedores de lista de IPs Bloqueados.

Use os cmdlets **IPBlockListConfig** para exibir e configurar como a filtragem de conexão usa a lista de IPs Bloqueados. Use os cmdlets **IPBlockListEntry** para exibir e configurar os endereços IP da lista de IPs Bloqueados.

## Usar o Shell para exibir a configuração da lista de IPs Bloqueados

Para exibir a configuração da lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Get-IPBlockListConfig | Format-List *Enabled,*Response
```

## Usar o Shell para habilitar ou desabilitar a lista de IPs Bloqueados

Para desabilitar a lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Set-IPBlockListConfig -Enabled $false
```

Para habilitar a lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Set-IPBlockListConfig -Enabled $true
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito a lista de IPs Bloqueados, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-IPBlockListConfig | Format-List Enabled
```

## Usar o Shell para configurar a lista de IPs Bloqueados

Para configurar a lista de IPs Bloqueados, use esta sintaxe:

```powershell
Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]
```

Este exemplo configura a lista de IPs Bloqueados com as seguintes configurações:

  - A lista de IPs Bloqueados filtra as conexões de entrada de servidores de email internos e externos. Por padrão, as conexões são filtradas apenas em servidores de email externos (*ExternalMailEnabled* é definido como `$true` e *InternalMailEnabled* é definido como `$false`). As conexões não autenticadas e as autenticadas de parceiros externos são consideradas externas.

  - O texto de resposta personalizado para conexões filtradas por endereços IP, que foram automaticamente adicionados à lista de IPs Bloqueados pelo recurso de reputação de remetente do agente Análise de Protocolo, é definido com o valor "A conexão do endereço IP {0} foi rejeitada pela reputação do remetente".

  - O texto de resposta personalizado para conexões filtradas por endereços IP adicionados manualmente à lista de IPs Bloqueados é definido com o valor "A conexão do endereço IP {0} foi rejeitada pela filtragem de conexão".

<!-- end list -->

```powershell
Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."
```

## Como saber se funcionou?

Para verificar se configurou com êxito a lista de IPs Bloqueados, execute o seguinte comando e verifique se os valores exibidos são os que você configurou.

```powershell
Get-IPBlockListConfig | Format-List *MailEnabled,*Response
```

## Usar o Shell para exibir as entradas da lista de IPs Bloqueados

Para exibir todas as entradas da lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Get-IPBlockListEntry
```

Observe que cada entrada da lista de IPs Bloqueados é identificada por um número inteiro. O inteiro de identidade é atribuído em ordem crescente quando você adiciona entradas à lista de IPs Bloqueados e à lista de IPs Permitidos.

Para exibir uma entrada específica da lista de IPs Bloqueados, use a sintaxe a seguir:

```powershell
Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

Por exemplo, para exibir a entrada da lista de IPs Bloqueados que contém o endereço IP 192.168.1.13, execute este comando:

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.13
```

> [!NOTE]  
> Quando o parâmetro <EM>IPAddress</EM> é usado, a entrada da lista de IPs Bloqueados resultante pode ser um endereço IP individual, um intervalo de endereços IP ou um IP CIDR (Roteamento entre Domínios sem Classificação). Para usar o parâmetro <EM>Identity</EM>, é preciso especificar o valor inteiro atribuído à entrada da lista de IPs Bloqueados.



## Usar o Shell para adicionar entradas da lista de IPs Bloqueados

Para adicionar entradas da lista de IPs Bloqueados, use esta sintaxe:

```powershell
Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]
```

O exemplo a seguir adiciona a entrada da lista de IPs Bloqueados ao intervalo de endereços IP 192.168.1.10 a 192.168.1.15 e configura a entrada da lista de IPs Bloqueados para expirar em 4 de julho de 2014 às 15:00.

```powershell
Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## Como saber se funcionou?

Para verificar se adicionou com êxito uma entrada da lista de IPs Bloqueados, execute o seguinte comando e confirme se a nova entrada da lista de IPs Bloqueados é exibida.

```powershell
Get-IPBlockListEntry
```

## Usar o Shell para remover entradas da lista de IPs Bloqueados

Para remover entradas da lista de IPs Bloqueados, use esta sintaxe:

```powershell
Remove-IPBlockListEntry <IdentityInteger>
```

O exemplo a seguir remove a entrada da lista de IPs Bloqueados que tem o valor 3 para *Identity*.

```powershell
Remove-IPBlockListEntry 3
```

O seguinte exemplo remove a entrada da lista de IPs Bloqueados que contém o endereço IP 192.168.1.12 sem usar o número de *Identity*. Observe que a entrada da lista de IPs Bloqueados pode ser um endereço IP individual ou um intervalo de endereços IP.

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry
```

## Como saber se funcionou?

Para verificar se removeu com êxito uma entrada da lista de IPs Bloqueados, execute o seguinte comando e confirme se a entrada removida da lista de IPs Bloqueados desapareceu.

```powershell
Get-IPBlockListEntry
```

## Procedimentos do provedor de lista de IPs Bloqueados

Esses procedimentos aplicam-se aos provedores de lista de IPs Bloqueados. Eles não se aplicam à lista de IPs Bloqueados.

Use o cmdlet **IPBlockListProvidersConfig** para exibir e configurar como a filtragem de conexão usa todos os provedores de lista de IPs Bloqueados. Use os cmdlets **IPBlockListProvider** para exibir, configurar e testar provedores de lista de IPs Bloqueados.

## Usar o Shell para exibir a configuração de todos os provedores de lista de IPs Bloqueados

Para exibir como a filtragem de conexão usa todos os provedores de lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*
```

## Usar o Shell para habilitar ou desabilitar todos os provedores de lista de IPs Bloqueados

Para desabilitar todos os provedores de lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Set-IPBlockListProvidersConfig -Enabled $false
```

Para habilitar todos os provedores de lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Set-IPBlockListProvidersConfig -Enabled $true
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito todos os provedores de lista de IPs Bloqueados, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-IPBlockListProvidersConfig | Format-List Enabled
```

## Usar o Shell para configurar todos os provedores de lista de IPs Bloqueados

Para configurar como a filtragem de conexão usa todos os provedores de lista de IPs Bloqueados, use esta sintaxe:

```powershell
Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]
```

O seguinte exemplo configura todos os provedores de lista de IPs Bloqueados com as seguintes configurações:

  - Os provedores de lista de IPs Bloqueados filtra as conexões de entrada de servidores de email internos e externos. Por padrão, as conexões são filtradas apenas em servidores de email externos (*ExternalMailEnabled* é definido como `$true` e *InternalMailEnabled* é definido como `$false`). As conexões não autenticadas e as autenticadas de parceiros externos são consideradas externas.

  - As mensagens enviadas para os destinatários internos chris@fabrikam.com e michelle@fabrikam.com são excluídas da filtragem pelos provedores de lista de IPs Bloqueados. Observe que, se quiser adicionar destinatários à lista sem afetar os destinatários existentes, é possível usar a sintaxe `@{Add="<recipient1>","<recipient2>"...}`.

<!-- end list -->

```powershell
Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true
```

Para obter mais informações, consulte [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/pt-br/library/aa998543\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se configurou com êxito todos os provedores de lista de IPs Bloqueados, execute o seguinte comando e confirme se os valores exibidos são os que você configurou.

```powershell
Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*
```

## Usar o Shell para exibir provedores de lista de IPs Bloqueados

Para exibir uma lista resumida de todos os provedores de lista de IPs Bloqueados, execute o seguinte comando:

```powershell
Get-IPBlockListProvider
```

Para exibir detalhes de um provedor específico, use a sintaxe a seguir:

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity>
```

O seguinte exemplo mostra os detalhes do provedor de lista de IPs Bloqueados da Contoso.

```powershell
Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response
```

## Usar o Shell para adicionar um provedor de lista de IPs Bloqueados

Para adicionar um provedor de lista de IPs Bloqueados, use esta sintaxe:

    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

Este exemplo cria um provedor chamado "Contoso IP Block List Provider" (Provedor de lista de IPs Bloqueados da Contoso) com as seguintes opções:

  - **FQDN para usar o provedor**   rbl.contoso.com

  - **Código bitmask para uso do provedor**   127.0.0.1

<!-- end list -->

```powershell
Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1
```

> [!NOTE]  
> Ao adicionar um novo provedor de lista de IPs Bloqueados, ele é habilitado por padrão (o valor <EM>Enabled</EM> é <CODE>$true</CODE>) e o valor de prioridade é incrementado (a primeira entrada de <EM>Priority</EM> tem valor 1).

Para obter mais informações, consulte [Add-IPBlockListProvider](https://technet.microsoft.com/pt-br/library/bb124358\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se adicionou com êxito um provedor de lista de IPs Bloqueados, execute o seguinte comando e confirme se o novo provedor de lista de IPs Bloqueados é exibido.

```powershell
Get-IPBlockListProvider
```

## Usar o Shell para habilitar ou desabilitar um provedor de lista de IPs Bloqueados

Para habilitar ou desabilitar um provedor específico de lista de IPs Bloqueados, use a sintaxe a seguir:

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>
```

O exemplo abaixo desabilita o provedor chamado Provedor de lista de IPs Bloqueados da Contoso.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false
```

O exemplo abaixo habilita o provedor chamado Provedor de lista de IPs Bloqueados da Contoso.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito um provedor de lista de IPs Bloqueados, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled
```

## Usar o Shell para configurar um provedor de lista de IPs Bloqueados

As opções de configuração disponíveis no cmdlet **Set-IPBlockListProvider** são idênticas às do cmdlet **New-IPBlockListProvider**.

Para configurar um provedor de lista de IPs Bloqueados existente, use esta sintaxe:

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]
```

Por exemplo, para adicionar o código de status de endereço IP 127.0.0.1 à lista de códigos de status existentes do provedor chamado Provedor de lista de IPs Bloqueados da Contoso, execute o seguinte comando:

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

Para obter mais informações, consulte [Set-IPBlockListProvider](https://technet.microsoft.com/pt-br/library/bb124979\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se configurou com êxito um provedor de lista de IPs Bloqueados, execute o seguinte comando e confirme se os valores exibidos são os que você configurou.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List
```

## Usar o Shell para testar um provedor de lista de IPs Bloqueados

Para testar um provedor de lista de IPs Bloqueados, use esta sintaxe.

```powershell
Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>
```

O exemplo a seguir testa o provedor chamado Provedor de lista de IPs Bloqueados da Contoso pesquisando o endereço IP 192.168.1.1.

```powershell
Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1
```

## Usar o Shell para remover um provedor de lista de IPs Bloqueados

Para remover um provedor de lista de IPs Bloqueados, use esta sintaxe:

```powershell
Remove-IPBlockListProvider <IPBlockListProviderIdentity>
```

O exemplo a seguir remove o provedor chamado Provedor de lista de IPs Bloqueados da Contoso.

```powershell
Remove-IPBlockListProvider "Contoso IP Block list Provider"
```

## Como saber se funcionou?

Para verificar se removeu com êxito um provedor de lista de IPs Bloqueados, execute o seguinte comando e confirme se o provedor de lista de IPs Bloqueados removido desapareceu.

```powershell
Get-IPBlockListProvider
```

## Procedimentos da lista de IPs Permitidos

Esses procedimentos aplicam-se à lista de IPs Permitidos que você configura manualmente. Eles não se aplicam aos provedores de lista de IPs Permitidos.

Use os cmdlets **IPAllowListConfig** para exibir e configurar como a filtragem de conexão usa a lista de IPs Permitidos. Use os cmdlets **IPAllowListEntry** para exibir e configurar como os endereços IP da lista de IPs Permitidos.

## Usar o Shell para exibir a configuração da lista de IPs Permitidos

Para exibir a configuração da lista de IPs Permitidos, execute o seguinte comando.

```powershell
Get-IPAllowListConfig | Format-List *Enabled
```

## Usar o Shell para habilitar ou desabilitar a lista de IP Permitidos

Para desabilitar a lista de IPs Permitidos, execute o seguinte comando:

```powershell
Set-IPAllowListConfig -Enabled $false
```

Para habilitar a lista de IPs Permitidos, execute o seguinte comando:

```powershell
Set-IPAllowListConfig -Enabled $true
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito a lista de IPs Permitidos, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-IPAllowListConfig | Format-List *Enabled
```

## Usar o Shell para configurar a lista de IPs Permitidos

Para configurar a lista de IPs Permitidos, use esta sintaxe:

```powershell
Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>
```

Esse exemplo configura a lista de IPs Permitidos para filtrar conexões de entrada de servidores internos e externos. Por padrão, as conexões são filtradas apenas em servidores de email externos (*ExternalMailEnabled* é definido como `$true` e *InternalMailEnabled* é definido como `$false`). As conexões não autenticadas e as autenticadas de parceiros externos são consideradas externas.

```powershell
Set-IPAllowListConfig -InternalMailEnabled $true
```

## Como saber se funcionou?

Para verificar se configurou com êxito a lista de IPs Permitidos, execute o seguinte comando e verifique se os valores exibidos são os que você configurou.

```powershell
Get-IPAllowListConfig | Format-List *MailEnabled
```

## Usar o Shell para exibir as entradas da lista de IPs Permitidos

Para exibir todas as entradas da lista de IPs Permitidos, execute o seguinte comando:

```powershell
Get-IPAllowListEntry
```

Observe que cada entrada da lista de IPs Permitidos é identificada por um valor inteiro. O inteiro de identidade é atribuído em ordem crescente quando você adiciona entradas à lista de IPs Bloqueados e à lista de IPs Permitidos.

Para exibir uma entrada específica da lista de IPs Permitidos, use a sintaxe a seguir:

```powershell
Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

Por exemplo, para exibir a entrada da lista de IPs Permitidos que contém o endereço IP 192.168.1.13, execute este comando:

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.13
```

> [!NOTE]  
> Quando o parâmetro <EM>IPAddress</EM> é usado, a entrada da lista de IPs Permitidos resultante pode ser um endereço IP individual, um intervalo de endereços IP ou um IP CIDR (Roteamento entre Domínios sem Classificação). Para usar o parâmetro <EM>Identity</EM>, é preciso especificar o valor inteiro atribuído à entrada da lista de IPs Permitidos.

## Usar o Shell para adicionar entradas da lista de IPs Permitidos

Para adicionar entradas da lista de IPs Permitidos, use esta sintaxe:

```powershell
Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]
```

O exemplo a seguir adiciona a entrada da lista de IPs Permitidos ao intervalo de endereços IP 192.168.1.10 a 192.168.1.15 e configura a entrada da lista de IPs Permitidos para expirar em 4 de julho de 2014 às 15:00.

```powershell
Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## Como saber se funcionou?

Para verificar se adicionou com êxito uma entrada da lista de IPs Permitidos, execute o seguinte comando e confirme se a nova entrada da lista de IPs Permitidos é exibida.

```powershell
Get-IPAllowListEntry
```

## Usar o Shell para remover as entradas da lista de IPs Permitidos

Para remover entradas da lista de IPs Permitidos, use esta sintaxe:

```powershell
Remove-IPAllowListEntry <IdentityInteger>
```

O exemplo a seguir remove a entrada da lista de IPs Permitidos que tem o valor 3 para *Identity*.

```powershell
Remove-IPAllowListEntry 3
```

O seguinte exemplo remove a entrada da lista de IPs Permitidos que contém o endereço IP 192.168.1.12 sem usar o número de *Identity*. Observe que a entrada da lista de IPs Permitidos pode ser um endereço IP individual ou um intervalo de endereços IP.

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry
```

## Como saber se funcionou?

Para verificar se removeu com êxito uma entrada da lista de IPs Permitidos, execute o seguinte comando e confirme se a entrada removida da lista de IPs Permitidos desapareceu.

```powershell
Get-IPAllowListEntry
```

## Procedimentos do provedor de lista de IPs Permitidos

Esses procedimentos aplicam-se aos provedores de lista de IPs Permitidos. Eles não se aplicam à lista de IPs Permitidos.

Use os cmdlets **IPAllowListProvidersConfig** para exibir e configurar como a filtragem de conexão usa todos os provedores de lista de IPs Permitidos. Use os cmdlets **IPAllowListProvider** para exibir, configurar e testar provedores de lista de IPs Permitidos.

## Usar o Shell para exibir a configuração de todos os provedores de lista de IPs Permitidos

Para exibir como a filtragem de conexão usa todos os provedores de lista de IPs Permitidos, execute o seguinte comando:

```powershell
Get-IPAllowListProvidersConfig | Format-List *Enabled
```

## Usar o Shell para habilitar ou desabilitar todos os provedores de lista de IPs Permitidos

Para desabilitar todos os provedores de lista de IPs Permitidos, execute o seguinte comando:

```powershell
Set-IPAllowListProvidersConfig -Enabled $false
```

Para habilitar todos os provedores de lista de IPs Permitidos, execute o seguinte comando:

```powershell
Set-IPAllowListProvidersConfig -Enabled $true
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito todos os provedores de lista de IPs Permitidos, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-IPAllowListProvidersConfig | Format-List *Enabled
```

## Usar o Shell para configurar todos os provedores de lista de IPs Permitidos

Para configurar como a filtragem de conexão usa todos os provedores de lista de IPs Permitidos, use esta sintaxe:

```powershell
Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]
```

Esse exemplo configura todos os provedores de lista de IPs Permitidos para filtrar conexões de entrada de servidores internos e externos. Por padrão, as conexões são filtradas apenas em servidores de email externos (*ExternalMailEnabled* é definido como `$true` e *InternalMailEnabled* é definido como `$false`). As conexões não autenticadas e as autenticadas de parceiros externos são consideradas externas.

```powershell
Set-IPAllowListProvidersConfig -InternalMailEnabled $true
```

Para obter mais informações, consulte [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/pt-br/library/aa998543\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se configurou com êxito todos os provedores de lista de IPs Permitidos, execute o seguinte comando e confirme se os valores exibidos são os que você configurou.

```powershell
Get-IPAllowListProvidersConfig | Format-List *MailEnabled
```

## Usar o Shell para exibir provedores de lista de IPs Permitidos

Para exibir uma lista resumida de todos os provedores de lista de IPs Permitidos, execute o seguinte comando.

```powershell
Get-IPAllowListProvider
```

Para exibir detalhes de um provedor específico, use a sintaxe a seguir.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity>
```

O seguinte exemplo mostra os detalhes do provedor de lista de IPs Permitidos da Contoso.

```powershell
Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match
```

## Usar o Shell para adicionar um provedor de lista de IPs Permitidos

Para adicionar um provedor de lista de IPs Permitidos, use esta sintaxe:

```powershell
Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]
```

Este exemplo cria um provedor chamado "Contoso IP Allow List Provider" (Provedor de lista de IPs Permitidos da Contoso) com as seguintes opções:

  - **FQDN para usar o provedor**   allow.contoso.com

  - **Código bitmask para uso do provedor**   127.0.0.1

<!-- end list -->

```powershell
Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1
```

> [!NOTE]  
> Quando você adiciona um novo provedor de lista de IPs Permitidos, ele é habilitado por padrão (o valor <EM>Enabled</EM> é <CODE>$true</CODE>) e o valor de prioridade é incrementado (a primeira entrada de <EM>Priority</EM> tem valor 1).


Para obter mais informações, consulte [Add-IPBlockListProvider](https://technet.microsoft.com/pt-br/library/bb124358\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se adicionou com êxito um provedor de lista de IPs Permitidos, execute o seguinte comando e confirme se o novo provedor de lista de IPs Permitidos é exibido.

```powershell
Get-IPAllowListProvider
```

## Usar o Shell para habilitar ou desabilitar um provedor de lista de IPs Permitidos

Para habilitar ou desabilitar um provedor específico de lista de IPs Permitidos, use a sintaxe a seguir:

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>
```

Este exemplo desabilita o provedor chamado Provedor de lista de IPs Permitidos da Contoso.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false
```

Este exemplo habilita o provedor chamado Provedor de lista de IPs Permitidos da Contoso.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true
```

## Como saber se funcionou?

Para verificar se habilitou ou desabilitou com êxito um provedor de lista de IPs Permitidos, execute o seguinte comando e confirme se o valor exibido é o que você configurou.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled
```

## Usar o Shell para configurar um provedor de lista de IPs Permitidos

As opções de configuração disponíveis no cmdlet **Set-IPAllowListProvider** são idênticas às do cmdlet **New-IPAllowListProvider**.

Para configurar um provedor de lista de IPs Permitidos existente, use esta sintaxe:

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]
```

Por exemplo, para adicionar o código de status de endereço IP 127.0.0.1 à lista de códigos de status existentes do provedor chamado Provedor de lista de IPs Permitidos da Contoso, execute o seguinte comando:

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

Para obter mais informações, consulte [Set-IPBlockListProvider](https://technet.microsoft.com/pt-br/library/bb124979\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se configurou com êxito um provedor de lista de IPs Permitidos, execute o seguinte comando e confirme se os valores exibidos são os que você configurou.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List
```

## Usar o Shell para testar um provedor de lista de IPs Permitidos

Para testar um provedor de lista de IPs Permitidos, use esta sintaxe:

```powershell
Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>
```

O exemplo a seguir testa o provedor chamado Provedor de lista de IPs Permitidos da Contoso pesquisando o endereço IP 192.168.1.1.

```powershell
Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1
```

## Usar o Shell para remover um provedor de lista de IPs Permitidos

Para remover um provedor de lista de IPs Permitidos, use esta sintaxe:

```powershell
Remove-IPAllowListProvider <IPAllowListProviderIdentity>
```

Este exemplo remove o provedor chamado Provedor de lista de IPs Permitidos da Contoso.

```powershell
Remove-IPAllowListProvider "Contoso IP Allow List Provider"
```

## Como saber se funcionou?

Para verificar se removeu com êxito um provedor de lista de IPs Permitidos, execute o seguinte comando e confirme se o provedor de lista de IPs Permitidos removido desapareceu.

```powershell
Get-IPAllowListProvider
```