---
title: 'Configurar cotas de arquivo morto para um sistema de arquivamento In-loco no Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurar cotas de arquivo morto para um sistema de arquivamento In-loco no Exchange 2013
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50556315
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar cotas de arquivo morto para um sistema de arquivamento In-loco no Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-12-04_

Em implantações de local, arquivos mortos In-loco são criados com as cotas de armazenamento ilimitado por padrão. Como resultado, você precisará editar propriedades de caixa de correio para definir cotas de armazenamento para o arquivo morto. Você pode definir as cotas de seguintes para um arquivo morto:

  - **Cota de aviso de arquivo morto**   Quando um sistema de arquivamento In-loco excede a cota de aviso de arquivo morto especificado, um evento é registrado para o administrador Exchange e uma mensagem de aviso é enviada para o usuário de caixa de correio.

  - **Cota de arquivo morto**   Quando um sistema de arquivamento In-loco excede a cota de arquivo morto especificado, as mensagens não são mais são movidas para o arquivo morto e uma mensagem de aviso é enviada para o usuário de caixa de correio.

Para saber mais sobre arquivos mortos In-loco, consulte [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - No Exchange Administration Center (EAC), você pode usar uma lista suspensa com valores fixos para configurar a cota de arquivo morto e arquivar cota de aviso. Se você deseja definir a cota para um valor que não está listado no EAC, use o Shell.

  - Configure a cota de aviso de arquivo morto para um valor menor que a cota de arquivo morto. Dependendo da taxa de crescimento de arquivo morto para um usuário, a diferença entre a cota de aviso de arquivo morto e a cota de arquivo morto deve permitir tempo suficiente para o usuário executar as ações apropriadas, como excluir itens do arquivo morto ou solicitar que um administrador ou assistência técnica de TI para aumentar a cota de arquivo morto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para configurar a cota de arquivo morto e a cota de aviso para uma caixa de correio de arquivamento

1.  Navegue até **destinatários** \> **caixas de correio**

2.  Na exibição de lista, selecione uma caixa de correio

3.  No painel de detalhes, em **Arquivo In-loco**, clique em **Exibir detalhes**.

4.  Na **Caixa de correio de arquivo morto**, use as listas de **valor de cota (GB)** e o **Aviso de problema em (GB)** para selecionar os valores desejados.

5.  Clique em **OK**.

## Usar o Shell para configurar a cota de arquivo morto e a cota de aviso para uma caixa de correio de arquivamento

Este exemplo define a cota de arquivo morto de caixa de correio de Chris Ashton como 10 gigabytes (GB), no qual tempo que o usuário receberá uma mensagem de aviso que o arquivo morto In-loco está cheio e ele não mais poderão mover itens para o arquivo morto. Este exemplo também define a cota de aviso de arquivo morto para 9,5 GB, o momento em que o usuário receberá uma mensagem de aviso que o arquivo morto In-loco está quase cheio.

    Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você habilitou com êxito em um arquivo morto local para uma caixa de correio existente, siga um destes procedimentos:

  - No EAC, navegue até **destinatários** \> **caixas de correio** e marque a caixa de correio que você deseja. No painel de detalhes, em **Arquivo In-loco**, clique em **Exibir detalhes** e verificar as configurações de cota do arquivamento.

  - No Shell, execute o seguinte comando para exibir informações sobre o arquivo de cota.
    
        Get-Mailbox <Name> | FL Name,Archive*Quota

