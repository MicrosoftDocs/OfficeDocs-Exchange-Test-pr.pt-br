---
title: 'Aplicar ou remover uma diretiva de caixa de correio do Outlook Web App em uma caixa de correio: Exchange 2013 Help'
TOCTitle: Aplicar ou remover uma diretiva de caixa de correio do Outlook Web App em uma caixa de correio
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 50485584
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicar ou remover uma diretiva de caixa de correio do Outlook Web App em uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-12_

Você pode aplicar uma política de caixa de correio de Outlook Web App a uma ou mais caixas de correio ou remover um usando o EAC ou o Shell.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio do outlook Web App" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Aplicar uma política de caixa de correio do Outlook Web App

## Usar o EAC para aplicar uma política de caixa de correio do Outlook Web App

1.  Na EAC, clique em **Destinatários** \> **Caixas de correio**.

2.  No painel de trabalho, clique para selecionar a caixa de correio que você deseja aplicar uma política de caixa de correio Outlook Web App para. Você também pode selecionar várias caixas de correio.

3.  **Se você tiver selecionado uma caixa de correio:** 
    
    1.  Role para baixo, no painel de detalhes para **Conectividade de Email** e clique em **Exibir detalhes**.
    
    2.  Clique em **Procurar** para exibir e selecione as políticas de caixa de correio disponíveis.
    
    3.  Clique em **Salvar** para atribuir a política selecionada na caixa de correio selecionadas.
    
    **Se você tiver selecionado mais de uma caixa de correio:** 
    
    1.  Role para baixo, no painel de detalhes para o **Outlook Web App** e clique em **atribuir uma política**.
    
    2.  Clique em **Procurar** para exibir e selecione as políticas de caixa de correio disponíveis.
    
    3.  Clique em **Salvar** para atribuir a política selecionada para as caixas de correio selecionadas.

## Usar o Shell para aplicar uma política de caixa de correio do Outlook Web App para uma caixa de correio existente

Este exemplo aplica a diretiva de caixa de correio de Outlook Web App denominada "Calendário" à caixa de correio do usuário tony@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Remover uma política de caixa de correio do Outlook Web App

## Usar o EAC para remover uma política de caixa de correio do Outlook Web App

1.  Na EAC, clique em **Destinatários** \> **Caixas de correio**.

2.  No painel de trabalho, clique para selecionar a caixa de correio que você deseja remover uma política de caixa de correio Outlook Web App de.

3.  Role para baixo, no painel de detalhes para **Conectividade de Email** e clique em **Exibir detalhes**.
    
    Se tiver sido atribuída uma política de caixa de correio, clique em **Limpar** para removê-lo da caixa de correio.

4.  Clique em **Salvar** para salvar suas alterações.

## Use o Shell para remover uma política de caixa de correio do Outlook Web App de uma caixa de correio existente.

Este exemplo remove a diretiva de caixa de correio Outlook Web App da caixa de correio do usuário tony@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

