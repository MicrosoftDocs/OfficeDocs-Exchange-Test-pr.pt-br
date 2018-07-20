---
title: 'Caixas de correio desconectadas: Exchange 2013 Help'
TOCTitle: Caixas de correio desconectadas
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50556200
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Caixas de correio desconectadas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Cada caixa de correio do Microsoft Exchange é constituída de uma conta de usuário do Active Directory e dos dados da caixa de correio armazenados no banco de dados de caixa de correio do Exchange. Todos os dados de configuração da caixa de correio são armazenados nos atributos do Exchange do objeto de usuário do Active Directory. O banco de dados de caixa de correio contém os dados de email que estão na caixa de correio associada à conta de usuário. A figura a seguir mostra os componentes de uma caixa de correio.

**Componentes da caixa de correio**

![Partes que compõem uma caixa de correio](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Partes que compõem uma caixa de correio")

Uma *caixa de correio desconectada* é um objeto de caixa de correio no banco de dados de caixa de correio que não está associado a uma conta de usuário do Active Directory. Há dois tipos de caixas de correio desconectadas:

  - **Caixas de correio desabilitadas**   Quando uma caixa de correio é desabilitada ou excluída no Centro de Administração do Exchange (EAC) ou está usando o cmdlet **Disable-Mailbox** ou **Remove-Mailbox** no Shell de Gerenciamento do Exchange, o Exchange mantém a caixa de correio excluída no banco de dados de caixa de correio e alterna a caixa de correio para um estado desabilitado. É por isso que as caixas de correio desabilitadas ou excluídas são conhecidas como *caixas de correio desabilitadas*. A diferença é que quando você desabilita uma caixa de correio, os atributos do Exchange são removidos da conta de usuário do Active Directory correspondente, mas a conta do usuário é mantida. Quando você exclui uma caixa de correio, os atributos do Exchange e a conta de usuário do Active Directory são excluídos.
    
    As caixas de correio desabilitadas e excluídas são retidas no banco de dados de caixa de correio até que o período de retenção da caixa de correio excluída expire, que é de 30 dias por padrão. Após o período de retenção especificado expirar, a caixa de correio é permanentemente excluída (o que também é chamado de *eliminação*). Se uma caixa de correio for excluída com o uso do cmdlet **Remove-Mailbox**, ela será retida também pelo tempo que durar o período de retenção.
    

    > [!IMPORTANT]
    > Se uma caixa de correio for excluída usando o cmdlet <STRONG>Remove-Mailbox</STRONG> ou o parâmetro <EM>Permanent</EM> ou <EM>StoreMailboxIdentity</EM>, ela será imediatamente excluída do banco de dados de caixa de correio.

    
    Para identificar as caixas de correio desabilitadas em sua organização, execute o seguinte comando no Shell.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **Caixas de correio excluídas por software**   Quando uma caixa de correio é movida para um banco de dados de caixa de correio diferente, o Exchange não exclui totalmente a caixa de correio do banco de dados de caixa de correio de origem quando a mudança estiver concluída. Em vez disso, a caixa de correio do banco de dados de caixa de correio de origem é alternada para um estado *excluído por software*. Como caixas de correio desabilitadas, as caixas de correio excluídas por software são mantidas no banco de dados de origem até que o período de retenção de caixa de correio excluída expire ou até que o cmdlet **Remove-StoreMailbox** seja usado para limpar a caixa de correio.
    
    Execute o seguinte comando para identificar caixas de correio excluídas de forma reversível em sua organização.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**Sumário**

Trabalhando com caixas de correio desabilitadas

Trabalhando com caixas de correio de arquivo morto desabilitadas

Trabalhando com caixas de correio excluídas por software

Resumo do trabalho com caixas de correio desconectadas

Documentação de caixa de correio desconectada

## Trabalhando com caixas de correio desabilitadas

Você pode executar várias operações em uma caixa de correio desabilitada antes de ela ser eliminada do banco de dados de caixa de correio:

  - Reconectá-la à mesma conta de usuário.

  - Conectá-la a uma conta de usuário diferente que não está habilitada para email, o que significa que a conta de usuário não tem uma caixa de correio.

  - Restaurá-la para uma conta de usuário que tenha uma caixa de correio existente. Por exemplo, se um usuário cuja caixa de correio foi excluída tiver uma nova caixa de correio, você poderá restaurar a caixa de correio desabilitada do usuário para a nova caixa de correio dele.

  - Excluí-la permanentemente do banco de dados de caixa de correio do Exchange.

## Conectando ou restaurando uma caixa de correio desabilitada

Eis os cenários nos quais você pode querer conectar ou restaurar uma caixa de correio desabilitada antes de o período de retenção de caixa de correio expirar ou antes de ele ser excluído permanentemente:

  - Você desabilitou uma caixa de correio e agora deseja reconectá-la à mesma conta de usuário do Active Directory.

  - Você excluiu uma caixa de correio usando o EAC ou o cmdlet [Remove-Mailbox](https://technet.microsoft.com/pt-br/library/aa995948\(v=exchg.150\)) e agora deseja reconectar a caixa de correio a uma conta de usuário diferente do Active Directory.

  - Você excluiu uma caixa de correio e agora deseja restaurá-la para uma caixa de correio existente. Por exemplo, se um usuário cuja caixa de correio foi excluída tiver uma nova caixa de correio, você poderá restaurar a caixa de correio desabilitada do usuário para a nova caixa de correio dele.

  - Você deseja converter uma caixa de correio de usuário em uma caixa de correio vinculada que está associada a uma conta de usuário externa à floresta na qual sua organização do Exchange existe. O cenário de floresta de recursos é um exemplo de quando você deseja associar uma caixa de correio a uma conta externa. Nesse cenário, os objetos de usuário na floresta do Exchange têm caixas de correio, mas os objetos de usuário estão desabilitados para logon. Você deve associar uma caixa de correio na floresta do Exchange a uma conta de usuário na floresta de conta externa.

Há duas maneiras de reconectar ou restaurar uma caixa de correio desabilitada. O primeiro método é usar o EAC ou o cmdlet **Connect-Mailbox** para conectar uma caixa de correio desabilitada a uma conta de usuário. Para procedimentos de como reconectar caixas de correio desabilitadas, consulte [Conectar uma caixa de correio desabilitada](connect-a-disabled-mailbox-exchange-2013-help.md).

O segundo método usa o cmdlet **New-MailboxRestoreRequest** para mesclar o conteúdo da caixa de correio desabilitada com uma caixa de correio existente. Esse cmdlet usa o MRS (Serviço de Replicação de Caixa de Correio) para restaurar a caixa de correio. Para procedimentos sobre como restaurar caixas de correio desabilitadas, consulte [Conectar-se ou restaurar uma caixa de correio excluída](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md).

## Excluindo permanentemente uma caixa de correio desabilitada

Como já foi mencionado, o Exchange retém as caixas de correio desabilitadas no banco de dados de caixa de correio com base nas configurações de retenção de caixa de correio excluída definidas para esse banco de dados de caixa de correio. Após o período de retenção especificado, uma caixa de correio desabilitada é eliminada do banco de dados de caixa de correio do Exchange. Você pode também excluir permanentemente uma caixa de correio desabilitada e todo o seu conteúdo de mensagem do banco de dados de caixa de correio usando o cmdlet **Remove-StoreMailbox**. Após uma caixa de correio desabilitada ser automaticamente eliminada ou excluída permanentemente por um administrador, a perda de dados será permanente, e a caixa de correio não poderá ser recuperada.

Para saber mais, consulte [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md).

Configuração

## Trabalhando com caixas de correio de arquivo morto desabilitadas

As caixas de correio de arquivo morto ficam desconectadas quando são desabilitadas. Igual a uma caixa de correio principal desabilitada, uma caixa de correio de arquivo morto desconectada pode ser conectada usando o cmdlet **Connect-Mailbox** com o parâmetro *Archive*.

A caixa de correio principal e a caixa de correio de arquivo morto compartilham o mesmo DN (nome distinto) herdado, portanto, você deve conectar a caixa de correio de arquivo morto à mesma caixa de correio de usuário à qual ela estava conectado antes. A caixa de correio de arquivo morto não pode ser conectada a uma caixa de correio de usuário diferente.

Você pode executar duas operações em uma caixa de correio de arquivo morto desconectada:

  - **Conectá-la a uma caixa de correio principal existente**   Como uma caixa de correio principal desconectada, uma caixa de correio de arquivo morto desconectada fica retida no banco de dados de caixa de correio até o período de retenção da caixa de correio excluída expirar, que é de 30 dias por padrão. Durante esse tempo, você pode recuperar a caixa de correio de arquivo morto reconectando-a à mesma conta de usuário à qual estava conectada antes de ser desabilitada.
    

    > [!TIP]
    > Se você desabilitar uma caixa de correio de arquivo morto de uma caixa de correio de usuário e depois habilitar uma caixa de correio de arquivo morto para o mesmo usuário, a caixa de correio desse usuário receberá uma nova caixa de correio de arquivo morto. Embora seja possível usar o cmdlet <STRONG>Connect-Mailbox</STRONG> para se conectar a uma caixa de correio principal a um usuário, você deve usar o cmdlet <STRONG>Enable-Mailbox</STRONG> para conectar uma caixa de correio de arquivo morto desabilitada a uma caixa de correio existente.

    
    Para saber mais, consulte [Gerenciar arquivos mortos de In-loco no Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Excluí-la permanentemente do banco de dados de caixa de correio do Exchange**    O Exchange mantém caixas de correio de arquivo morto desconectadas com base nas configurações de retenção da caixa de correio excluída definidas para o banco de dados de caixa de correio. O período de retenção padrão é de 30 dias. Após o período de retenção de caixa de correio especificado, uma caixa de correio de arquivo morto desabilitada é eliminada do banco de dados de caixa de correio do Exchange.
    
    Como uma caixa de correio principal desabilitada, você pode permanentemente excluir uma caixa de correio de arquivo morto a qualquer momento usando o cmdlet **Remove-StoreMailbox**. Para saber mais, consulte [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md).

Configuração

## Trabalhando com caixas de correio excluídas de forma reversível

Uma caixa de correio de exclusão reversível é criada quando uma caixa de correio é movida de um banco de dados de caixa de correio do Exchange para outro banco de dados de caixa de correio. O Exchange não exclui completamente a caixa de correio do banco de dados de origem após uma movimentação em caso de erros durante a movimentação que façam a caixa de correio do banco de dados de destino falhar. Sempre é possível restaurar a caixa de correio de origem e tentar novamente. O Exchange manterá a caixa de correio excluída de forma reversível pelo período de retenção da caixa de correio.

Você pode executar duas operações em uma caixa de correio excluída de forma reversível:

  - Restaurá-la para uma caixa de correio existente.

  - Excluí-la permanentemente do banco de dados de caixa de correio do Exchange.

Os procedimentos para restaurar e excluir permanentemente uma caixa de correio excluída de forma reversível são similares aos de uma caixa de correio desabilitada. Para saber mais, consulte os seguintes tópicos:

  - [Restaurar uma caixa de correio excluída](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md)

Configuração

## Resumo do trabalho com caixas de correio desconectadas

A tabela a seguir resume as informações sobre as caixas de correio desconectadas, incluindo como a caixa de correio foi desconectada, o que acontece com a conta de usuário do Active Directory correspondente quando uma caixa de correio é desconectada e as opções e as ferramentas que você tem para conectar ou restaurar caixas de correio desconectadas.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Como a caixa de correio foi desabilitada</th>
<th>Valor da propriedade <em>DisconnectReason</em></th>
<th>A conta de usuário do Active Directory é mantida?</th>
<th>Opções de conexão ou restauração</th>
<th>Ferramentas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>O EAC: <strong>Destinatários</strong> &gt; <strong>Caixas de correio</strong> &gt; <strong>Desabilitar</strong></p></li>
<li><p>O Shell: cmdlet <strong>Disable-Mailbox</strong></p></li>
</ul></td>
<td><p>Desabilitado</p></td>
<td><p>Sim</p></td>
<td><p>Conectar-se à mesma conta de usuário</p></td>
<td><ul>
<li><p>O EAC: <strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong> &gt; <strong>Conectar uma Caixa de Correio</strong></p></li>
<li><p>O Shell: cmdlet <strong>Connect-Mailbox</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>O EAC: <strong>Destinatários</strong> &gt; <strong>Caixas de correio</strong> &gt; <strong>Excluir</strong></p></li>
<li><p>O Shell: cmdlet <strong>Remove-Mailbox</strong></p></li>
</ul></td>
<td><p>Desabilitado</p></td>
<td><p>Não</p></td>
<td><ul>
<li><p>Conectar-se a uma conta de usuário diferente</p></li>
<li><p>Restaurar para uma caixa de correio diferente</p></li>
</ul></td>
<td><ul>
<li><p>O EAC: <strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong> &gt; <strong>Conectar uma Caixa de Correio</strong></p></li>
<li><p>O Shell: cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>O Shell: cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Movido para um banco de dados de caixa de correio diferente</p></td>
<td><p>SoftDeleted</p></td>
<td><p>Sim</p></td>
<td><ul>
<li><p>Conectar-se a uma conta de usuário diferente</p></li>
<li><p>Restaurar para uma caixa de correio diferente</p></li>
</ul></td>
<td><ul>
<li><p>O EAC: <strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong> &gt; <strong>Conectar uma Caixa de Correio</strong></p></li>
<li><p>O Shell: cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>O Shell: cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
</tbody>
</table>


Configuração

## Documentação de caixa de correio desconectada

A tabela a seguir contém links para tópicos que o ajudarão a gerenciar caixas de correio desconectadas. Isso inclui o gerenciamento de caixas de correio de usuário desconectadas, caixas de correio vinculadas, caixas de correio de recursos e caixas de correio compartilhadas.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">Desabilitar ou excluir uma caixa de correio</a></p></td>
<td><p>Saiba como desabilitar ou excluir caixas de correio.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">Conectar uma caixa de correio desabilitada</a></p></td>
<td><p>Saiba como conectar uma caixa de correio desabilitada a uma conta de usuário existente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">Conectar-se ou restaurar uma caixa de correio excluída</a></p></td>
<td><p>Saiba como conectar uma caixa de correio excluída a uma conta de usuário ou restaurar o conteúdo de uma caixa de correio excluída para uma caixa de correio existente.</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">Restaurar uma caixa de correio excluída</a></p></td>
<td><p>Saiba como conectar uma caixa de correio excluída de forma reversível a uma conta de usuário ou restaurar uma caixa de correio excluída de forma reversível para uma caixa de correio existente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">Gerenciar solicitações de restauração de caixa de correio</a></p></td>
<td><p>Saiba como gerenciar solicitações de restauração de caixa de correio usando o Shell.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">Excluir permanentemente uma caixa de correio</a></p></td>
<td><p>Saiba como excluir permanentemente uma caixa de correio.</p></td>
</tr>
</tbody>
</table>


Trabalhando com caixas de correio desabilitadas

