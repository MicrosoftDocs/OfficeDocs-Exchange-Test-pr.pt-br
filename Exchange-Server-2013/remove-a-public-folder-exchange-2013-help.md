---
title: 'Remover uma pasta pública: Exchange 2013 Help'
TOCTitle: Remover uma pasta pública
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 50485297
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma pasta pública

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-11-16_

Você pode ter que remover pastas públicas que não estão mais sendo usadas em sua organização. Para ajudar a determinar quais pastas públicas devem ser removidas, consulte [Exibir estatísticas de pastas públicas e itens de pasta pública](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas ao gerenciamento de pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Não é possível excluir uma pasta pública habilitada para email. Antes de excluí-la, é necessário primeiro desabilitar o email para a pasta pública. Para obter mais informações, consulte [Email habilitar ou desabilitar email uma pasta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para remover uma pasta pública

1.  Navegue até **Pastas públicas** \> **Pastas públicas**.

2.  Na exibição de lista, selecione a pasta pública que você deseja excluir. Observe que clicar no nome da pasta exibirá subpastas dentro dessa pasta, caso haja alguma. Nesse momento, você pode clicar para selecionar uma subpasta específica para remover.
    
    Ao excluir uma pasta ou subpasta, clique em qualquer lugar na linha da pasta, exceto o nome sublinhado da pasta e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone"). Se você clicar no nome sublinhado da pasta, a opção **Excluir** não estará disponível para selecionar.
    
    ![Selecionando uma pasta pública para remover](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "Selecionando uma pasta pública para remover")  

3.  Aparecerá um aviso, perguntando se você tem certeza de que deseja excluir a pasta pública. Clique em **Sim** para continuar.

## Use o Shell para excluir uma pasta pública

Este exemplo exclui a pasta pública Help Desk\\Resolved. Este comando assume que a pasta pública Resolved não possui subpastas.

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

Este exemplo testa o comando anterior sem efetuar nenhuma modificação.

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

Este exemplo remove a pasta pública Marketing e todas as suas subpastas porque o comando é executado recursivamente.

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-PublicFolder](https://technet.microsoft.com/pt-br/library/bb124894\(v=exchg.150\)).

