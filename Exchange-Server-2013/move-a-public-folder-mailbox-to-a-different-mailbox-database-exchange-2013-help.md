---
title: 'Mover cx. corr. de pasta pública para outro banco de dados de caixa de correio'
TOCTitle: Mover uma caixa de correio de pasta pública para um banco de dados de caixa de correio diferente
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51407879
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover uma caixa de correio de pasta pública para um banco de dados de caixa de correio diferente

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-07-21_

Você pode precisar mover uma caixa de correio de pasta pública para um banco de dados de uma caixa de correio diferente para balanceamento de carga ou para mover os recursos para mais perto de sua localização geográfica. Semelhante a mover uma caixa de correio normal, você usa os cmdlets **MoveRequest** para mover uma caixa de correio de pasta pública. Para mais informações sobre como mover caixas de correio, veja [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar depende do tamanho da caixa de correio de pasta públic.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Mover caixa de correio e migrar permissões" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Não é possível realizar esse procedimento no EAC. Você pode realizar este procedimento somente no Shell.

  - Dependendo do tamanho da caixa de correio de pasta pública, a ação pode demorar várias horas para ser concluída. Durante essse tempo, os usuários não poderão acessar as pastas públicas. Os usuários também não terão acesso às pastas públicas por um breve período de tempo enquanto a pasta estiver no estado "Conclusão em Andamento".

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma solicitação para mover

O cmdlet **New-MoveRequest** coloca na fila a caixa de correio de pasta pública no serviço de Replicação de Caixa de Correio do Microsoft Exchange. Quando o serviço de Replicação de Caixa de Correio do Microsoft Exchange estiver disponível, ele atenderá à solicitação para mover e começará a mover a caixa de correio de pasta pública. Ele completará a solicitação do começo ao fim.

Este exemplo inicial a solicitação para mover para a caixa de correio de pasta pública PF\_SanFrancisco para o banco de dados de caixa de correio MBX\_DB01.

```powershell
New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01
```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Crie uma solicitação de movimentação para finalizar mais tarde

Durante o estágio final da solicitação de movimentação, quando ele está na fase de `CompletionInProgress` , usuários podem ser temporariamente bloqueados a caixa de correio de pasta pública. Se necessário, você pode suspender a solicitação de movimentação antes de alcançar fase e retomá-lo cada vez quando os usuários não afetados.

Este exemplo começa solicitação para mover para a caixa de correio de pasta pública PF\_SanFrancisco para o banco de dados de caixa de correio MBX\_DB01, e suspende-a quando a solicitação para mover estiver pronta para ser finalizada.

```powershell
New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete
```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

Este exemplo recupera o status da movimentação que está ocorrendo na caixa de correio para a caixa de correio de pasta pública PF\_SanFrancisco.

```powershell
Get-MoveRequest -Identity "PF_SanFrancisco"
```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Get-MoveRequest](https://technet.microsoft.com/pt-br/library/dd335227\(v=exchg.150\)).

Quando a solicitação para mover atingir o status de Suspensa, você pode continuar a solicitação. Este exemplo continua a solicitação para mover para a caixa de correio de pasta pública PF\_SanFrancisco.

```powershell
Resume-MoveRequest -Identity "PF_SanFrancisco"
```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Resume-MoveRequest](https://technet.microsoft.com/pt-br/library/ee332320\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que a solicitação para mover foi criada com sucesso, execute o seguinte comando:

```powershell
Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status
```

Um status de `Completed` indica que a solicitação de movimentação foi realizada com êxito.

Caso contrário, você pode precisar restaurar a pasta pública. Para obter mais informações, consulte [Restaurar pastas públicas e caixas de correio de pasta pública de movimentações com falha](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

