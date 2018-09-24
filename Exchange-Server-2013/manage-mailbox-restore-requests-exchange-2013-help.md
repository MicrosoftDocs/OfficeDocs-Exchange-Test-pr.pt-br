---
title: 'Gerenciar solicitações de restauração de caixa de correio: Exchange 2013 Help'
TOCTitle: Gerenciar solicitações de restauração de caixa de correio
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50556228
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar solicitações de restauração de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Solicitações de restauração de caixa de correio são usadas para restaurar as caixas de correio desconectadas. Uma caixa de correio desconectada é uma caixa de correio em um banco de dados de caixa de correio do Exchange que não esteja associado uma conta de usuário do Active Directory. Caixas de correio se tornam desconectadas quando estiver desabilitadas, excluídos ou movidos para outro banco de dados. Para obter mais informações, consulte [Caixas de correio desconectadas](disconnected-mailboxes-exchange-2013-help.md).

Caixas de correio desconectadas permanecem no banco de dados de caixa de correio por um período especificado nas configurações de retenção de caixa de correio excluída do banco de dados de caixa de correio. Por padrão, as caixas de correio desconectadas são mantidas por 30 dias. Durante esse período de retenção, o conteúdo de uma caixa de correio excluída pode ser restaurado (copiados) para uma caixa de correio existente. Este tópico descreve como usar o Shell para gerenciar solicitações de restauração de caixa de correio.

Para conhecer tarefas de gerenciamento adicionais relacionadas a caixas de correio desconectadas, confira os seguintes tópicos:

[Desabilitar ou excluir uma caixa de correio](disable-or-delete-a-mailbox-exchange-2013-help.md)

[Conectar uma caixa de correio desabilitada](connect-a-disabled-mailbox-exchange-2013-help.md)

[Conectar-se ou restaurar uma caixa de correio excluída](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[Restaurar uma caixa de correio excluída](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Solicitação de restauração de caixa de correio", no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Os procedimentos neste tópico só podem ser executados no Shell. Você não pode usar o EAC para gerenciar solicitações de restauração de caixa de correio.

  - Para exibir o valor da propriedade *Identity* para todas as solicitações de restauração de caixa de correio, execute o seguinte comando.
    
    ```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```
    
    Você pode usar esse valor de identity para especificar uma solicitação de restauração de caixa de correio específica quando você estiver executando os procedimentos neste tópico.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o Shell para exibir propriedades de solicitação de restauração

Você pode exibir as propriedades de uma solicitação de restauração de caixa de correio, que fornecem informações básicas sobre o status de uma solicitação de restauração de caixa de correio.

Para exibir uma lista e o valor da propriedade *Identity* para todas as solicitações de restauração de caixa de correio, execute o seguinte comando.

```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```

Você pode usar a identidade para obter mais informações sobre solicitações de restauração de caixa de correio específica.

Este exemplo retorna o status da solicitação de restauração "Pilar Pinilla \\MailboxRestore" usando o parâmetro *Identity* .

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"
```

Este exemplo retorna todas as informações para a segunda solicitação de restauração para a caixa de correio de destino Pilar Pinilla.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List
```

Este exemplo retorna o status de solicitações de restauração sendo restauradas do banco de dados de origem MBD01.

```powershell
Get-MailboxRestoreRequest -SourceDatabase MBD01
```

Este exemplo retorna que todas as solicitações de restauração que estão atualmente em andamento.

```powershell
Get-MailboxRestoreRequest -Status InProgress
```

Outros estados de status úteis incluem `Queued`, `Completed`, `Suspended`e `Failed`.

Este exemplo retorna que todas as solicitações de restauração que foram suspensas.

```powershell
Get-MailboxRestoreRequest -Suspend $true
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829907\(v=exchg.150\)).

## Saída de Get-MailboxRestoreRequest

Por padrão, o cmdlet **Get-MailboxRestoreRequest** retorna o nome da solicitação, a caixa de correio de destino aos quais dados está sendo restaurados e o status da solicitação. A tabela a seguir lista as informações úteis retornadas se você canalizar o cmdlet para o cmdlet **Format-List** .


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Especifica o banco de dados que contém a caixa de correio desconectada que está sendo restaurada.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>Especifica a caixa de correio para a qual os dados estão sendo restaurados.</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Especifica o nome da solicitação.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Especifica o banco de dados no qual o serviço de Replicação de Caixa de Correio do Microsoft Exchange (MRS) armazena o status detalhado da solicitação.</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>Especifica o status da solicitação.</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>Especifica se a solicitação é suspenso. Uma restauração de caixa de correio pode ser suspenso quando ele foi criado usando o cmdlet de <strong>New-MailboxRestoreRequest</strong> com o parâmetro <em>Suspend</em> . Ele também pode ser suspenso se a caixa de correio restaurar a operação falhar ou por um administrador usando o cmdlet <strong>Suspend-MailboxRestoreRequest</strong> .</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Especifica a identidade da solicitação. Essa identidade é uma combinação do nome da caixa de correio de destino e do nome da solicitação.</p></td>
</tr>
</tbody>
</table>


## Como saber se funcionou?

Execute o cmdlet **Get-MailboxRestoreRequest** para verificar que você pode visualizar as propriedades para solicitações de restauração de caixa de correio. Se o cmdlet retorna um erro, verifique se você estiver usando a sintaxe correta e identidade. Em alguns casos, o cmdlet pode ser bem-sucedida e não retornou resultados. Por exemplo, se você enviou a solicitação de restauração de uma caixa de correio e execute o comando `Get-MailboxRestoreRequest -Status InProgress` e nenhum resultado for retornado, então nenhuma das solicitações de restauração em execução no momento.

## Use o Shell para exibir estatísticas de solicitação de restauração

Você pode exibir as estatísticas de uma solicitação de restauração de caixa de correio, que fornecem informações detalhadas que podem ser usadas para fins de solução de problemas.

Este exemplo retorna as estatísticas padrão para o danp\\MailboxRestore1 de solicitação de restauração. Por padrão, as informações retornadas incluem nome, caixa de correio, status e porcentagem concluída.

```powershell
Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1
```

Este exemplo retorna as estatísticas de caixa de correio de Dan Park e exporta o relatório para um arquivo. csv.

    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv

Este exemplo retorna informações adicionais sobre a solicitação de restauração de caixa de correio do Pilar Pinilla usando o parâmetro *IncludeReport* e Canalizando os resultados para o cmdlet **Format-List** .

    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 

Este exemplo retorna informações adicionais de todas as solicitações de restauração com um status de `Failed`, utilizando o parâmetro *IncludeReport* e em seguida salvando as informações no arquivo AllRestoreReports.txt no local no qual o comando está sendo executado.

    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/pt-br/library/ff829912\(v=exchg.150\)) e [Get-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829907\(v=exchg.150\)).

## Saída de Get-MailboxRestoreRequestStatistics.

Por padrão, o cmdlet [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/pt-br/library/ff829912\(v=exchg.150\)) retorna o nome da solicitação, o status da solicitação, o alias da caixa de correio de destino, e a porcentagem concluída. A tabela a seguir lista outras informações úteis retornadas se você canalizar o cmdlet para o cmdlet **Format-List** .


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Especifica o nome da solicitação.</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>Especifica o status da solicitação.</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>Especifica mais detalhes sobre o status da solicitação. Por exemplo, se o valor de <code>Status</code>retornar <code>InProgress</code>, o valor <code>StatusDetail</code> retornaria os estágios específicos para o status <code>InProgress</code>, como <code>CreatingFolderHierarchy</code> e <code>CopyingMessages</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>Especifica o quanto a solicitação já avançou no processo de restauração.</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>Especifica se a solicitação de restauração foi suspensa. Este valor será <code>true</code> nos seguintes cenários:</p>
<ul>
<li><p>O MRS interrompeu ou está interrompendo a solicitação devido a uma falha.</p></li>
<li><p>Um administrador suspendeu a solicitação.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>Especifica o GUID da caixa de correio de origem a partir da qual os dados estão sendo restaurados.</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>Especifica o nome da pasta raiz na hierarquia da caixa de correio de origem do qual os dados está sendo restaurados. Se este valor estiver em branco, os dados são restaurados da pasta superior do armazenamento de informações.</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Especifica o nome do banco de dados no qual a caixa de correio de origem está localizada.</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>Especifica se a caixa de correio que está sendo restaurada está <code>Disabled</code> ou <code>Soft-Deleted</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>Especifica o alias da caixa de correio de destino.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>Especifica se a caixa de correio está sendo restaurada para um arquivo morto.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>Especifica o GUID da caixa de correio de destino.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>Especifica o nome da pasta raiz na hierarquia de caixa de correio de destino aos quais dados está sendo restaurados. Se este valor estiver em branco, os dados são restaurados para a pasta superior do armazenamento de informações.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>Especifica o nome do banco de dados no qual a caixa de correio de destino está localizada.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>Especifica a identidade da caixa de correio de destino.</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>Especifica a lista de pastas a serem incluídas durante a restauração. Se este valor estiver em branco, não há pastas foram especificadas quando a solicitação foi criada e todas as pastas serão restauradas na caixa de correio (a menos que o parâmetro <em>ExcludeFolders</em> é usado para excluir pastas específicas).</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>Especifica a lista de pastas a serem excluídas durante a restauração. Se este valor estiver em branco, não há pastas foram especificadas quando a solicitação foi criada e todas as pastas serão restauradas na caixa de correio (a menos que o parâmetro <em>IncludeFolders</em> é usado para incluir pastas específicas).</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>Especifica se a pasta Itens Recuperáveis foi excluída quando a solicitação foi criada.</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>Especifica a ação a ser desempenhada pelo MRS caso haja mensagens correspondentes nas pastas de origem e destino.</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>Especifica se as mensagens associadas são copiadas quando a solicitação é processada. As mensagens associadas são mensagens especiais contendo dados ocultos com informações sobre regras, exibições e formulários.</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>Especifica o número de itens incorretos que o MRS ignorará caso a solicitação encontre mensagens corrompidas.</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>Específica o número de mensagens corrompidas que foram encontradas pelo comando. Se o valor <em>BadItemsEncountered</em> for maior que o valor <em>BadItemLimit</em>, ocorrerá falha da solicitação.</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>Especifica a data e a hora nas quais que a solicitação foi iniciada para o MRS.</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>Especifica a data e hora em que MRS iniciados processando a solicitação de restauração.</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>Especifica a data e a hora nas quais a última alteração foi feita na solicitação. A alteração pode ter sido feita por um administrador ou pelo MRS.</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>Especifica a data e a hora nas quais a solicitação foi suspendida.</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>Especifica em quanto tempo a solicitação foi concluída. Se a solicitação estiver no status <code>Failed</code>, este valor especificará o intervalo de tempo entre o início da solicitação e o momento da falha. Se a solicitação não estiver concluída, este valor especificará o intervalo de tempo entre o início da solicitação e o momento em que o cmdlet <strong>Get-MailboxRestoreRequestStatistics</strong> passou a ser executado.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>Especifica por quanto tempo a solicitação ficou no estado <code>Suspended</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>Especifica por quanto tempo a solicitação ficou no estado <code>Failed</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>Especifica por quanto tempo a solicitação ficou no estado <code>Queued</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>Especifica por quanto tempo a solicitação ficou no estado <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>Especifica por quanto tempo a solicitação ficou paralisada por causa da alta disponibilidade.</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>Especifica o nome do servidor de Acesso para Cliente que processou a solicitação.</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>Especifica o tamanho total do arquivo que foi restaurado ou o tamanho do arquivo que MRS espera restaurar se a solicitação está no estado <code>In Progress</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>Especifica o número de itens que foram restaurados ou que o MRS espera restaurar caso a solicitação esteja no estado <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>Especifica a média de bytes transferidos por minuto.</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>Especifica o número de itens transferidos.</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>Especifica a porcentagem já concluída da solicitação.</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>Especifica quanto tempo uma solicitação de restauração concluídas serão mantidos antes de serem excluído. O padrão é 30 dias.</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>Caso a solicitação ainda não tenha iniciado, este valor especificará a posição Em fila da solicitação.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>Se houver falha, este valor especificará o código da falha.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>Se houver falha, este valor especificará o tipo da falha.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>Se houver falha, este valor especificará se a falha ocorreu na caixa de correio de destino ou na caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>Se houver falha, este valor especificará a mensagem da falha. Este valor pode especificar também o comentário de suspensão.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>Se a solicitação falhar, este valor especificará a data e hora em que a solicitação falhou.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>Se a solicitação falhar, este valor especificará informações sobre a ação que estava sendo realizada no momento da falha.</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>Se a solicitação não for válida, este valor especificará a razão.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Especifica o banco de dados no qual o MRS armazena o status detalhado da solicitação.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Especifica a identidade da solicitação.</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p>Se você usou o parâmetro <em>IncludeReport</em>, este valor especificará informações que podem ser utilizadas para solucionar problemas na solicitação.</p></td>
</tr>
</tbody>
</table>


## Como saber se funcionou?

Execute o cmdlet **Get-MailboxRestoreRequestStatistics** para verificar se você pode exibir as estatísticas de solicitações de restauração de caixa de correio. Se o cmdlet retorna um erro, verifique se que você está usando a identidade correta para a solicitação de restauração.

## Use o Shell para alterar propriedades de solicitação de restauração

Se uma restauração de caixa de correio solicitar falhar, você pode usar o cmdlet **Set-MailboxRestoreRequest** para alterar as propriedades da solicitação para tentar recuperar da falha.

Este exemplo especifica que a solicitação de restauração de caixa de correio de Debra Garcia MailboxRestore1 pula 10 itens de caixa de correio corrompidos.

```powershell
Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10
```

Este exemplo especifica que a solicitação de restauração de caixa de correio do Florence Flipo MailboxRestore1 pula 100 itens corrompidos. Porque o valor de *BadItemLimit* é maior que 50, o parâmetro *AcceptLargeDataLoss* deve ser especificado.

    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829909\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você alterou com êxito as propriedades de uma solicitação de restauração, execute o cmdlet de **Get-MailboxRestoreRequestStatistics** para exibir as propriedades revisadas para a solicitação de restauração. Se a solicitação de restauração foi criada com êxito, a propriedade *Status* terá um valor de `Queued`, `InProgress`ou `Completed`. Quando a solicitação de restauração for concluída, o conteúdo da caixa de correio excluída aparecerá na caixa de correio de destino.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/pt-br/library/ff829912\(v=exchg.150\)).

## Use o Shell para suspender uma solicitação de restauração

É possível suspender uma solicitação de restauração sempre depois que a solicitação foi criada, mas antes que a solicitação atinja o status de `Completed`. Consulte Use o Shell para retomar uma solicitação de restauração mais adiante neste tópico para a sintaxe de comando retomar a solicitação de restauração usando o cmdlet [Resume-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829908\(v=exchg.150\)) .

Este exemplo suspende a solicitação de restauração de caixa de correio do Pilar Pinilla MailboxRestore1.

```powershell
Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

Este exemplo suspende todas as solicitações em andamento de restauração por recuperar primeiramente todas as solicitações que têm um status de `InProgress`e, em seguida, canalizar a saída para o cmdlet **Suspend-MailboxRestoreRequest** e incluindo o comentário suspenso "Resume após a manutenção de FY13Q2".

    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829906\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você tiver suspendido com êxito uma solicitação de restauração de caixa de correio, execute o seguinte comando.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

Se o valor da propriedade *Suspend* for igual a `True`, a solicitação de restauração com êxito foi suspensa. Além disso, o valor `Suspended` para a propriedade *Status* indica que a solicitação de restauração foi suspensa.

## Usar o Shell para retomar uma solicitação de restauração

Use o cmdlet **Resume-MailboxRestoreRequest** para retomar uma solicitação de restauração que falhou ou foi suspensa.

Este exemplo retoma a solicitação de restauração Pinilla\\MailboxRestore1 Pilar.

```powershell
Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

Este exemplo retoma todas as solicitações de restauração que têm um status de Failed.

```powershell
Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Resume-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829908\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se uma solicitação de restauração foi retomada, execute o seguinte comando.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

Se o valor da propriedade *Suspend* for igual a `False`, a solicitação de restauração foi reiniciado com êxito. Além disso, o valor `InProgress` para a propriedade *Status* indica que a solicitação de restauração foi reiniciado.

## Usar o Shell para remover uma solicitação de restauração

Você pode usar o cmdlet **Remove-MailboxRestoreRequest** para remover solicitações de restauração de caixa de correio. Se você remover uma solicitação de restauração que iniciam os dados de caixa de correio que está sendo copiada para a caixa de correio de destino, os dados de caixa de correio são copiados permanecem na caixa de correio de destino.


> [!TIP]
> Como indicada anteriormente, concluída restauração solicitações são mantidas por 30 dias por padrão antes automaticamente excluídos.



Este exemplo remove a solicitação de restauração Pinilla\\MailboxRestore1 Pilar.

```powershell
Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

Este exemplo remove todas as solicitações de restauração com status Concluído.

```powershell
Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
```

Este exemplo cancela a solicitação de restauração, utilizando o parâmetro *RequestGuid* para uma solicitação armazenada em MBXDB01. O conjunto de parâmetros que exige os parâmetros *RequestGuid* e *RequestQueue* é usado apenas para fins de depuração do Serviço de Replicação do Microsoft. Use este parâmetro apenas se for instruído pelo Atendimento Microsoft.

```powershell
Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829910\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito uma solicitação de restauração de caixa de correio, execute o seguinte comando.

```powershell
Get-MailboxRestoreRequest -Identity <identity of removed restore request>
```

O comando retornará um erro informando que a solicitação de restauração não existe.

Também é possível executar o cmdlet **Get-MailboxRestoreRequest** . Se uma solicitação de restauração foi removida com êxito, ele não será incluído nos resultados.

