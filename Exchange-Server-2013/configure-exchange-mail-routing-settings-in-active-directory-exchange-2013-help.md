---
title: 'Configurar definições de roteamento de email do Exchange no Active Directory'
TOCTitle: Configurar definições de roteamento de email do Exchange no Active Directory
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 50486693
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar definições de roteamento de email do Exchange no Active Directory

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Por padrão o Microsoft Exchange Server 2013 faz referência os objetos de link de site IP no Active Directory para ajudar a determinar o caminho de roteamento de menor custo. No entanto, se você determinar os custos do link de site IP do Active Directory e padrões do fluxo de tráfego não ideais para email de roteamento no Exchange, você poderá definir configurações no Active Directory que são usados pelo Exchange somente para ajudar a otimizar o fluxo de emails.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "gerenciamento de link de site e site do active Directory" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para configurar um custo específicas do Exchange em um link de site IP do Active Directory

Determine o nome do link de site IP do Active Directory para o qual deseja definir um custo do Exchange. Um valor de custo mais baixo indica uma rota mais preferencial. Você pode examinar o conteúdo dos logs de tabela de roteamento e exibir os dados na seção **ADTopologyPath ID** para exibir detalhes sobre o caminho de roteamento de custo mínimo calculados entre dois sites do Active Directory.

Para definir um custo específicas do Exchange em um link de site do Active Directory, execute o seguinte comando:

```powershell 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

Este exemplo define um custo específicas do Exchange de 10 de link de site IP chamado IPSiteLinkAB.

```powershell
Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10
```

Este exemplo limpa o custo do Exchange do link de site IP chamado IPSiteLinkAB.

```powershell
Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null
```

## Como saber se funcionou?

Para verificar que você definiu com êxito um custo do Exchange em um link de site do Active Directory, faça o seguinte:

1.  Execute o seguinte comando:
    
    ```powershell
    Get-AdSiteLink | Format-List Name,ExchangeCost
    ```

2.  Verificar que o custo do Exchange está configurado no link de site do Active Directory.

## Use o Shell para configurar um site do Active Directory como um local de concentrador

Quando um site de hub existe ao longo do caminho de roteamento de custo mínimo para uma mensagem, a mensagem deve ser roteada através do site de hub. Examinar o conteúdo dos logs de tabela de roteamento e exibir os dados na seção **ADTopologyPath ID** para verificar a existência de site selecionado ao longo do caminho de roteamento de custo mínimo entre dois sites do Active Directory. Se isso não for o caso, você precisa atribuir os custos de específicas do Exchange para os links de site IP para tornar o caminho de roteamento de custo mínimo passem por sites selecionados.

Para configurar um site do Active Directory como um site de hub, execute o seguinte comando:

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

Este exemplo configura o site do Active Directory chamado Site A como um site de hub.

```powershell
Set-AdSite "Site A" -HubSiteEnabled $true
```

Este exemplo remove o atributo do site de hub do site do Active Directory denominado local B.

```powershell
Set-AdSite "Site B" -HubSiteEnabled $false
```

## Como saber se funcionou?

Para verificar se você configurou com êxito um site do Active Directory como um site de hub, faça o seguinte:

1.  Execute o seguinte comando:
    
    ```powershell
    Get-AdSite | Format-List Name,HubSiteEnabled
    ```

2.  Verifique se que o valor de *HubSiteEnabled* é `True` para o site do Active Directory.

