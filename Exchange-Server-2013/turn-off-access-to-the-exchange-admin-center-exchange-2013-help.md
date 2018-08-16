---
title: 'Desativar o acesso ao centro de administração do Exchange: Exchange 2013 Help'
TOCTitle: Desativar o acesso ao centro de administração do Exchange
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 50485528
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desativar o acesso ao centro de administração do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-05-20_

Para fins de segurança, algumas organizações podem querer restringir o acesso ao Centro de Administração do Exchange (EAC), para usuários vindos da Internet. Este procedimento mostra como desativar o acesso ao EAC. Este procedimento não evita que os usuários acessem as Opções no Outlook Web App.


> [!NOTE]
> Este procedimento desabilita completamente o acesso do administrador do EAC no servidor CAS onde as etapas são aplicadas. Se você habilitar o administrador do EAC para usuários internos, deverá instalar um servidor CAS separado e configurá-lo para lidar somente com solicitações internas usando este comando:<BR><CODE>Set-ECPVirtualDirectory -Identity "InternalCAS\ecp (default web site)" -AdminEnabled $True</CODE>




> [!CAUTION]
> O procedimento se aplica somente a implantações no local do Exchange Server 2013.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectividade do Centro de Administração do Exchange" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - O EAC não pode ser usado para esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para desativar o acesso de Internet ao EAC

Este exemplo desabilita o acesso ao EAC no servidor CAS01.

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Set-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd297991\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você desativou com êxito o acesso ao EAC, faça o seguinte:

1.  Usando seu navegador de Internet, digite a URL externa da sua organização para acessar o Outlook Web App, mas substitua o identificador **/owa** por **/ecp**. Por exemplo, se a URL externa para acessar o Outlook Web App for https://primary.tailspintoys.com/owa, use https://primary.tailspintoys.com/ecp.

2.  Se o acesso à Internet estiver desativado, você receberá um erro **404 – site da web não encontrado**.

