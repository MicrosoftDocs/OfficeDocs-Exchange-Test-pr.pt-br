---
title: 'Gerenciar reputação do remetente: Exchange 2013 Help'
TOCTitle: Gerenciar reputação do remetente
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 50486987
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar reputação do remetente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Reputação do remetente é fornecida pelo agente de análise de protocolo. Reputação do remetente bloqueia as mensagens de acordo com a várias características do remetente. Reputação do remetente depende de dados persistentes sobre o remetente para determinar qual ação, se houver, para receber uma mensagem de entrada.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos de antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - O agente de análise de protocolo é o subjacentes para a funcionalidade de reputação do remetente. Quando você desabilita reputação do remetente, o agente de análise de protocolo ainda está habilitado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar a reputação do remetente

Este exemplo desabilita a reputação do remetente.

```powershell
Set-SenderReputationConfig -Enabled $false
```

Este exemplo habilita a reputação do remetente.

```powershell
Set-SenderReputationConfig -Enabled $true
```

## Como saber se funcionou?

Para verificar que você tenha habilitado ou desabilitado reputação do remetente com êxito, faça o seguinte:

1.  Verifique se o agente de análise de protocolo está instalado e habilitado executando o seguinte comando:
    
    ```powershell
Get-TransportAgent
```

2.  Verifique se os valores de reputação do remetente que você configurou executando o seguinte comando:
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

## Usar o Shell para habilitar ou desabilitar a reputação do remetente para mensagens internas ou externas

Por padrão, reputação do remetente está habilitada para mensagens externas e desabilitada para mensagens internas. Uma mensagem é considerada externa se ela for proveniente de uma conexão não-autenticado externo à sua organização do Exchange. Uma mensagem é considerada interna se ele vem de conexão autenticado e o domínio do remetente está configurado como um domínio autoritativo em sua organização do Exchange.

Para desabilitar a reputação do remetente para mensagens externas, execute o seguinte comando:

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $false
```

Para habilitar a reputação do remetente para mensagens externas, execute o seguinte comando:

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $true
```

Para desabilitar a reputação do remetente para mensagens internas, execute o seguinte comando:

```powershell
Set-SenderReputationConfig -InternalMailEnabled $false
```

Para habilitar a reputação do remetente para mensagens internas, execute o seguinte comando:

```powershell
Set-SenderReputationConfig -InternalMailEnabled $true
```

## Como saber se funcionou?

Para verificar que você tenha habilitado ou desabilitado reputação do remetente para mensagens internas e externas com êxito, faça o seguinte:

1.  Execute o comando a seguir:
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

2.  Verifique se os valores exibidos correspondem aos valores que você configurou.

## Use o Shell para configurar as propriedades de reputação do remetente

Para configurar as propriedades de reputação do remetente, execute o seguinte comando:

```powershell
Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>
```

Este exemplo define o limite de bloqueio (SRL) nível do remetente reputação 6 e configura a reputação do remetente para adicionar ofensivos remetentes à lista de bloqueios de IP para 36 horas:

```powershell
Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36
```

## Como saber se funcionou?

Para verificar se você configurou com êxito as propriedades de reputação do remetente, faça o seguinte:

1.  Execute o comando a seguir:
    
    ```powershell
Get-SenderReputationConfig
```

2.  Verifique se os valores exibidos correspondem aos valores que você configurou.

## Usar o Shell para configurar o acesso de saída para a detecção de servidores de proxy aberto

Você pode precisar executar etapas adicionais para permitir a reputação do remetente atravessar firewalls que estão entre a Internet e o servidor do Exchange que esteja executando o agente de análise de protocolo. A tabela a seguir lista as portas de saída que são necessárias para a reputação do remetente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolos</th>
<th>Portas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4, SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate, Telnet, Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT, HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


Para configurar o acesso de saída para a detecção de servidores de proxy aberto, execute o seguinte comando:

    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>

Este exemplo configura a reputação do remetente para usar o servidor de proxy aberto chamado SERVER01 que usa o protocolo HTTP se conectar na porta 80.

    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect

## Como saber se funcionou?

Para verificar se você configurou com êxito o acesso de saída para detecção de servidores de proxy aberto, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-SenderReputationConfig | Format-List ProxyServer*

2.  Verifique se os valores exibidos são os valores que você configurou.

