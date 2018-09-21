---
title: 'Remover uma pesquisa de descoberta eletrônica In-loco: Exchange 2013 Help'
TOCTitle: Remover uma pesquisa de descoberta eletrônica In-loco
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 50485960
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma pesquisa de descoberta eletrônica In-loco

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-07-14_

No Microsoft Exchange Server 2013, você pode usar In-Place eDiscovery para pesquisar o conteúdo de caixa de correio. Você pode remover uma pesquisa de descoberta eletrônica In-loco a qualquer momento. Quando você remove uma pesquisa de descoberta eletrônica In-loco, os resultados da pesquisa serão removidos da caixa de correio de descoberta.


> [!CAUTION]
> A exclusão de uma pesquisa de descoberta eletrônica In-loco removerá quaisquer resultados de pesquisa copiados para uma caixa de correio de descoberta.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2-5 minutos.

  - Para remover uma pesquisa de descoberta eletrônica In-loco que tenha habilitado de bloqueio In-loco, você deve primeiro remover o bloqueio In-loco da pesquisa. Para obter detalhes, consulte [Criar ou remover um bloqueio In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/create-or-remove-in-place-holds).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para remover uma pesquisa de descoberta eletrônica In-loco

1.  Navegue até **Gerenciamento de conformidade** \> **Retenção e Descoberta Eletrônica Locais**.

2.  Na exibição de lista, selecione a pesquisa de descoberta eletrônica In-loco que deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Use o Shell para remover uma pesquisa de descoberta eletrônica In-loco

Para obter um exemplo de como remover uma pesquisa de descoberta eletrônica In-loco, consulte a seção "Exemplos" em [Remove-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd298130\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito uma pesquisa de descoberta eletrônica In-loco, siga um destes procedimentos:

  - Use o EAC para verificar se a pesquisa não é mais exibida no modo de exibição de lista da guia **bloqueio e descoberta eletrônica In-loco**.

  - Use o cmdlet **Get-MailboxSearch** para recuperar pesquisas de descoberta eletrônica In-loco. Para obter um exemplo de como recuperar pesquisas de descoberta eletrônica In-loco, consulte a seção "Exemplos" em [Get-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd351021\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


