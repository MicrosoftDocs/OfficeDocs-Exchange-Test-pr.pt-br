---
title: 'Exibir carimbos de antispam no Outlook: Exchange 2013 Help'
TOCTitle: Exibir carimbos de antispam no Outlook
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 50486668
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir carimbos de antispam no Outlook

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-03_

Você pode usar o Microsoft Outlook para exibir os carimbos antispam que o Microsoft Exchange aplicada a uma mensagem de email. Carimbos antispam ajudarão-lo a diagnosticar problemas relacionados a spam aplicando metadados diagnóstico ou carimbos, como informações específicas do remetente, resultados da validação de quebra-cabeça e conteúdo filtrando os resultados às mensagens conforme as mensagens que passam pelos agentes antispam que filtrar mensagens de entrada da Internet.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Acesso à caixa de correio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Outlook 2010 ou Outlook 2013 para exibir carimbos antispam

1.  Em Outlook 2010 ou Outlook 2013, em um computador cliente, no modo de exibição de **email** , clique duas vezes em uma mensagem para abri-lo.

2.  Na seção de **marcas** da faixa de opções, clique no ícone de **Opções** para exibir a caixa de diálogo de **Propriedades** da mensagem.

3.  Na caixa de diálogo **Propriedades**, na seção **cabeçalhos da Internet**, use a barra de rolagem para exibir os carimbos antispam, conforme mostrado no exemplo a seguir.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## Usar o Outlook 2007 para exibir os carimbos antispam

1.  Em Outlook 2007, em um computador cliente, no modo de exibição de **email** , clique duas vezes em uma mensagem para abri-lo.

2.  Na guia **mensagem**, no grupo de **Opções**, clique em **Opções de mensagem**.

3.  Na caixa de diálogo **Opções de mensagem**, na seção **cabeçalhos da Internet**, use a barra de rolagem para exibir os carimbos antispam, conforme mostrado no exemplo a seguir.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

