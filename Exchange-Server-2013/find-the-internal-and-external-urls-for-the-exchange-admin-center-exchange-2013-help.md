---
title: 'Encontre URLs internas e externas para o Centro de administração do Exchange'
TOCTitle: Encontre as URLs internas e externas para o Centro de administração do Exchange
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 50485389
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Encontre as URLs internas e externas para o Centro de administração do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-04_

Como o Centro de Administração do Exchange (EAC) é um console de gerenciamento baseado na Web do Exchange Server 2013, você pode acessá-lo usando a URL do diretório virtual do ECP em um navegador da Web. Este tópico mostra como encontrar a URL do diretório virtual do ECP.


> [!NOTE]
> O ECP é a interface de usuário baseada na web desenvolvido para o Exchange Server 2010. Os cmdlets do EAC para diretórios virtuais ainda usam "ECP" no nome, e esses cmdlets podem ser usados para gerenciar diretórios virtuais do ECP no Exchange 2010 e no Exchange 2013.



Para saber mais sobre o EAC, consulte [Centro de administração do Exchange no Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - O EAC não pode ser usado para esse procedimento. É necessário usar o Shell.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectividade do Centro de Administração do Exchange" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para encontrar as URLs interna e externa do diretório virtual do ECP

Este exemplo retorna o nome do diretório virtual do ECP, a URL interna e a URL externa, em uma lista formatada.

```powershell
Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL
```

Quando o comando for concluído, use os valores *InternalURL* ou *ExternalURL*, no seu navegador da web, para abrir o EAC.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd351058\(v=exchg.150\)).

