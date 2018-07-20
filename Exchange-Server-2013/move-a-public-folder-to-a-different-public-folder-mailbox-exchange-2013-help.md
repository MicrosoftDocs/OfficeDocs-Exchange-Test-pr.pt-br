---
title: 'Mover uma pasta pública para uma caixa de correio de pasta pública diferentes: Exchange 2013 Help'
TOCTitle: Mover uma pasta pública para uma caixa de correio de pasta pública diferentes
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51407900
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover uma pasta pública para uma caixa de correio de pasta pública diferentes

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-11-16_

Se o conteúdo de um correio de pasta pública começa excederá suas cotas de caixa de correio, você pode precisar mover pastas públicas para um correio de pasta pública diferentes. Há duas maneiras de fazer isso. Para mover um ou mais pastas públicas que não contêm subpastas, você pode usar os cmdlets **PublicFolderMoveRequest** . Se você precisar mover uma ramificação de toda a pasta pública (que inclui a pasta pública pai e todas as subpastas), você pode usar o script `Move-PublicFolderBranch.ps1` que está disponível quando você instala o Exchange 2013.

Para gerenciamento adicional tarefas relacionadas a pastas públicas consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão dessa tarefa depende do tamanho da pasta pública.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md) .

  - É possível usar o EAC para executar estes procedimentos. Use o Shell.

  - Se a pasta que você está movendo tem subpastas, as subpastas não serão movidas por padrão. Se quiser mover uma pasta pública e todas as suas subpastas, use o script **Move-PublicFolderBranch.ps1** .

  - Somente a movimentação de pastas públicas move conteúdo físico da pasta pública; ele não altera a hierarquia lógica.

  - Dependendo do tamanho de pasta pública e a quantidade de conteúdo que ele contém, a movimentação pode levar várias horas para ser concluída. Durante esse tempo, os usuários poderão acessar as pastas públicas. No entanto, os usuários não poderão acessar as pastas públicas por um breve período, enquanto a pasta está no estado "Conclusão em andamento".

  - Você pode executar apenas uma solicitação de movimentação de pasta pública por vez. Você deve usar o cmdlet **Remove-PublicFolderMoveRequest** para remover a solicitação após a conclusão.

  - Para verificar se o status de uma solicitação de movimentação de pasta pública em andamento, execute o cmdlet de [Get-PublicFolderMoveRequest](https://technet.microsoft.com/pt-br/library/jj878076\(v=exchg.150\)) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Mover uma única pasta pública

Este exemplo inicia a solicitação de movimentação de \\CustomerEnagagements a pasta pública da caixa de correio de pasta pública DeveloperReports para DeveloperReports01

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01


> [!TIP]
> O correio de pasta pública de destino será bloqueado enquanto a solicitação de movimentação está ativa.



Para detalhadas informações sintaxe e parâmetros, consulte [New-PublicFolderMoveRequest](https://technet.microsoft.com/pt-br/library/jj878081\(v=exchg.150\)).

## Mover várias pastas públicas

Este exemplo inicia a solicitação de movimentação de pastas públicas na ramificação de pastas públicas \\Dev na caixa de correio de pasta pública de destino DeveloperReports01. Este exemplo não moverá \\Dev de pasta pública.

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01


> [!TIP]
> A caixa de correio de pasta pública de destino será bloqueada enquanto a solicitação de movimentação está ativa.



Para detalhadas informações sintaxe e parâmetros, consulte [New-PublicFolderMoveRequest](https://technet.microsoft.com/pt-br/library/jj878081\(v=exchg.150\)).

## Mover uma ramificação de pastas públicas

Este exemplo usa o script `Move-PublicFolderBranch.ps1` para mover uma ramificação de pastas públicas. Isso inicia a solicitação de movimentação para \\Dev a pasta pública e todas as suas subpastas na caixa de correio de pasta pública DeveloperReports01. O script está localizado na pasta scripts e deve ser executado a partir desta localização.

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## Como saber se funcionou?

Para verificar se a solicitação de movimentação de pasta pública foi bem-sucedida, execute o comando a seguir:

    Get-PublicFolderMoveRequest | Format-List Status

Um status de `Completed` indica que a solicitação de movimentação foi realizada com êxito.

Se tiver sido bem sucedida a solicitação de movimentação, você pode precisar restaurar a pasta pública ou seus conteúdos. Para obter mais informações, consulte [Restaurar pastas públicas e caixas de correio de pasta pública de movimentações com falha](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

