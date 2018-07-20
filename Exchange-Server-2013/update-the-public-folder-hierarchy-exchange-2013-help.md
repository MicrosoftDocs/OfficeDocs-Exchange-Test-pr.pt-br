---
title: 'Atualizar a hierarquia de pastas públicas: Exchange 2013 Help'
TOCTitle: Atualizar a hierarquia de pastas públicas
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52058477
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualizar a hierarquia de pastas públicas

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2014-04-03_

Você só precisa atualizar a hierarquia de pasta pública, se quiser invocar manualmente o sincronizador de hierarquia e o assistente de caixa de correio. Ambos são invocados pelo menos uma vez a cada 24 horas para cada caixa de correio de pasta pública na organização. O sincronizador de hierarquia é invocado a cada 15 minutos, se os usuários estiverem conectados a uma caixa de correio secundária através dos clientes do Microsoft Outlook ou de Conectividade dos Serviços Web do Microsoft Exchange.

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas no Exchange Online, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas no Exchange Server 2013, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Não é possível realizar esse procedimento no EAC. É necessário usar o Shell.

  - Recomendamos que ao executar este comando com o parâmetro *InvokeSynchronizer* , utilize o parâmetro *SuppressStatus* . Se você não utilizar este parâmetro no comando, a saída exibirá mensagens de status a cada 3 segundos por até um minuto. Até passar um minuto, não é possível utilizar esta instância do Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Atualizar a hierarquia de pastas públicas

Este exemplo atualiza a hierarquia de pastas públicas na caixa de correio da pasta pública PF\_marketing e suprime a saída do comando.

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

Este exemplo atualiza todas as caixas de correio de pasta pública e suprime a saída do comando.

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

