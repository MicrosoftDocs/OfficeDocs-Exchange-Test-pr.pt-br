---
title: 'Iniciar ou parar uma pesquisa de descoberta eletrônica In-loco: Exchange 2013 Help'
TOCTitle: Iniciar ou parar uma pesquisa de descoberta eletrônica In-loco
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 50484936
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Iniciar ou parar uma pesquisa de descoberta eletrônica In-loco

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-07-14_

Você pode parar ou reiniciar uma pesquisa de descoberta eletrônica In-loco a qualquer momento. Por exemplo, se você deseja modificar as propriedades de pesquisa como palavras-chave ou caixas de correio pesquisadas, você deve primeiro parar uma pesquisa. Em seguida, você pode reiniciar a pesquisa depois de fazer as alterações necessárias.


> [!WARNING]
> Se você reiniciar uma pesquisa de descoberta eletrônica In-loco, copiados para a caixa de correio de descoberta especificada em uma pesquisa de resultados da pesquisa serão removidos.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "In-Place eDiscovery" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para iniciar ou parar uma pesquisa de descoberta eletrônica In-loco

1.  Navegue até **gerenciamento de conformidade** \> **bloqueio e descoberta eletrônica In-loco**.

2.  Para interromper uma pesquisa em andamento, selecione a pesquisa e, em seguida, clique em **Parar a pesquisa**.

3.  Para iniciar uma pesquisa que foi interrompida, selecione a pesquisa e clique em **Pesquisar continuar**.

## Usar o Shell para iniciar ou parar uma pesquisa de descoberta eletrônica In-loco

Para obter um exemplo de como iniciar uma pesquisa de descoberta eletrônica In-loco, consulte "exemplo 1" em [Start-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd351245\(v=exchg.150\)).

Para obter um exemplo de como interromper uma pesquisa de descoberta eletrônica In-loco, consulte "exemplo 1" em [Stop-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd351075\(v=exchg.150\)).

