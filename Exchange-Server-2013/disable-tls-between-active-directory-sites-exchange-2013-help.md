---
title: 'Desabilitar o TLS entre sites do Active Directory: Exchange 2013 Help'
TOCTitle: Desabilitar o TLS entre sites do Active Directory
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52058803
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar o TLS entre sites do Active Directory

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-19_

O Microsoft Exchange Server 2013 suporta a desabilitação de TLS para comunicação SMTP entre servidores de Caixa de Correio em determinadas topologias nas quais os dispositivos WOC (WAN Optimization Controller) que compactam o tráfego SMTP são usados.

Este tópico fornece instruções detalhadas sobre como configurar o serviço Transporte em seus servidores de Caixa de Correio afetados a fim de desabilitar o TLS e assegurar que sua topologia de roteamento do Active Directory esteja configurada para encaminhar corretamente as mensagens. Para saber mais sobre esse cenário, consulte [Cenário: Configurar o Exchange para oferecer suporte a controladores de otimização de WAN](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 60 minutos.

  - Embora as etapas de configuração individuais neste cenário possam ser realizadas com menos direitos, para completar todas as tarefas do cenário sua conta precisa ser membro do grupo de funções Gerenciamento de Organização.

  - Desabilite o TLS apenas em conexões que passem por dispositivos WOC.

  - Este procedimento exige que o Exchange 2013 seja implantado em vários sites do Active Directory, com pelo menos um site conectado aos outros sites em um link WAN.

  - Esse procedimento exige que os dispositivos WOC sejam implantados para compactar o tráfego SMTP sobre o link WAN.

  - Esse procedimento exige um caminho de fluxo de mensagens lógico para o Exchange chegando até o link WAN com os dispositivos WOC implantados.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Etapa 1: Use o Shell para configurar o serviço Transporte no servidor de Caixa de Correio a fim de usar a autenticação do Exchange Server desatualizado

Para configurar o serviço Transporte em um servidor de Caixa de Correio a fim de usar a autenticação do Exchange server desatualizado, execute o seguinte comando:

```powershell
Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true
```

Esse exemplo faz essa alteração de configuração no servidor chamado Mailbox01.

```powershell
Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true
```

## Etapa 2: Crie um Conector de recebimento dedicado no servidor de Caixa de Correio para o site de destino do Active Directory

## Use o EAC para criar o Conector de recebimento

1.  No Centro de administração do Exchange (EAC), clique em **Fluxo de emails** \> **Conectores de recebimento** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na primeira página do assistente **Novo Conector de recebimento**, insira os seguintes valores
    
      - **Nome**   Insira um valor descritivo.
    
      - **Tipo**   Interno
    
    Quando você tiver concluído, clique em **Avançar**.

3.  Na segunda página do assistente **Novo Conector de recebimento**, na seção **Configurações remotas**, insira os endereços IP ou intervalos de endereço IP para o site de destino do Active Directory. Ao concluir, clique em **Concluir**.

## Usar o Shell para criar o Conector de recebimento

Para criar todos os Conectores de recebimento no servidor de Caixa de Correio, execute o seguinte comando:

  ```powershell
  New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal
  ```

Esse exemplo cria o Conector de recebimento chamado WAN no servidor chamado Mailbox01 com as seguintes configurações:

  - O parâmetro *RemoteIPRanges* é definido como 10.0.2.0/24. Esse intervalo de endereços IP deve corresponder ao site remoto do Active Directory de onde este Conector de recebimento receberá as conexões não criptografadas. Se houver mais de uma sub-rede IP no site remoto, você poderá digitar todas elas separadas por vírgulas.

  - O tipo de uso é definido como Interno.

<!-- end list -->

```powershell
New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal
```

## Etapa 3: Use o Shell para desabilitar o TLS no Conector de recebimento dedicado

Para desabilitar o TLS no Conector de recebimento, execute o seguinte comando:

```powershell
Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true
```

Esse exemplo desabilita o TLS no Conector de recebimento chamado WAN no servidor de Caixa de Correio chamado Mailbox01.

```powershell
Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true
```

## Etapa 4: Use o Shell para designar os sites do Active Directory como sites de hub

Para designar um site do Active Directory como um site de hub, execute o seguinte comando:

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

Você precisa executar esse procedimento uma vez em cada site do Active Directory com servidores de Caixa de Correio que participam do tráfego não criptografado.

Esse exemplo configura o site do Active Directory chamado Central Office Site 1 como o site de hub.

```powershell
Set-AdSite "Central Office Site 1" -HubSiteEnabled $true
```

## Etapa 5: Use o Shell para configurar o caminho de roteamento de menor custo por meio da conexão WAN

Dependendo de como os custos de link de site IP estão configurados no Active Directory, talvez esta etapa não seja necessária. Você precisa verificar se o link de rede com os dispositivos WOC implantados está no caminho de roteamento de menor custo. Para exibir os custos de link de site do Active Directory e os custos de link de site específicos ao Exchange, execute o seguinte comando:

```powershell
Get-AdSiteLink
```

Se o link de rede com os dispositivos WOC implantados não estiver no caminho de roteamento de menor custo, será necessário atribuir um custo específico ao Exchange para o link de site IP específico a fim de assegurar que as mensagens sejam encaminhadas corretamente. Para saber mais sobre esse problema específico, consulte a seção "Configurar custos de link de site do Active Directory específicos do Exchange" em [Cenário: Configurar o Exchange para oferecer suporte a controladores de otimização de WAN](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

Este exemplo configura um custo específico do Exchange de 15 no link de site IP chamado Branch Office 2-Branch Office 1.

```powershell
Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15
```

