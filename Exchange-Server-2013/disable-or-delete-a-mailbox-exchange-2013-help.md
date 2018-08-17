---
title: 'Desabilitar ou excluir uma caixa de correio: Exchange 2013 Help'
TOCTitle: Desabilitar ou excluir uma caixa de correio
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50556180
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Desabilitar ou excluir uma caixa de correio

 

_**Aplica-se a:** Exchange Server 2013 SP1_

_**Tópico modificado em:** 2015-03-09_

Você pode usar o EAC ou o Shell para desabilitar ou excluir uma caixa de correio no Exchange 2013. Quando uma caixa de correio é desabilitada ou excluída, o Exchange mantém o banco de dados da caixa de correio e alterna a caixa de correio para um estado de desabilitada. As caixas de correio desabilitadas e excluídas são retidas no banco de dados de caixa de correio até que o período de retenção da caixa de correio excluída expire, que é de 30 dias por padrão. Depois que o período de retenção expirar, a caixa de correio será permanentemente excluída ou *limpa*.

Se você precisar excluir uma caixa de correio no Exchange Online, confira [Excluir ou restaurar caixas de correio do usuário no Exchange Online](https://technet.microsoft.com/pt-br/library/dn186233\(v=exchg.150\)).


> [!NOTE]
> As caixas de correio desabilitadas ou excluídas são referidas como <EM>caixas de correio desconectadas</EM>.



A principal diferença entre excluir e desabilitar uma caixa de correio é que quando você desabilita uma caixa de correio, os atributos do Exchange são removidos da conta de usuário do Active Directory correspondente, mas a conta de usuário é mantida. Quando você exclui uma caixa de correio, os atributos do Exchange e a conta de usuário do Active Directory são excluídos. Essa diferença também determina suas opções para reconectar ou restaurar caixas de correio desabilitadas ou excluídas.

A tabela a seguir mostra quais tipos de caixas de correio do Exchange você pode desabilitar ou excluir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de caixa de correio</th>
<th>Desabilitar?</th>
<th>Excluir?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Caixa de correio do arquivamento</p></td>
<td><p>Sim</p></td>
<td><p>Não *</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio vinculada</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio de recurso (Sala ou Equipamento)</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio compartilhada</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio do usuário</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


\* Se uma caixa de correio de arquivo morto for habilitada, ela será excluída quando a caixa de correio principal é excluída. Para saber mais sobre como desabilitar caixas de correio de arquivo morto, confira [Gerenciar arquivos mortos de In-loco no Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

Se um administrador excluir uma conta de usuário que tem uma caixa de correio, o Armazenamento de Informações do Exchange eventualmente detectará que a caixa de correio não está mais conectada a uma conta de usuário e marcará essa caixa de correio para exclusão, mesmo se ela estiver em espera. Se você deseja manter a caixa de correio, deve fazer o seguinte:

1.  Em vez de excluir a conta de usuário, desabilite a conta de usuário.

2.  Altere as propriedades da caixa de correio para restringir o seu uso e acesso à caixa de correio. Por exemplo, defina as cotas de envio e de recebimento como 1, bloqueie quem pode enviar mensagens à caixa de correio e restrinja quem pode acessar a caixa de correio.

3.  Retenha a caixa de correio até que todos os dados sejam eliminados ou até que a retenção de dados não seja mais necessária.

Para conhecer tarefas de gerenciamento adicionais relacionadas a caixas de correio desconectadas, confira os seguintes tópicos:

  - [Caixas de correio desconectadas](disconnected-mailboxes-exchange-2013-help.md)

  - [Conectar uma caixa de correio desabilitada](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Conectar-se ou restaurar uma caixa de correio excluída](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Desabilitar uma caixa de correio

Como especificado anteriormente, quando você desabilita uma caixa de correio, os atributos do Exchange são removidos da conta de usuário do Active Directory correspondente, mas a conta de usuário é mantida.

## Usar o EAC para desabilitar uma caixa de correio

O procedimento a seguir mostra como desabilitar uma caixa de correio do usuário. Use o mesmo procedimento para desabilitar outros tipos de caixa de correio após ir para a página apropriada no EAC.

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuário, clique na caixa de correio que deseja desabilitar.

3.  Clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e, em seguida, clique em **Desabilitar**.

4.  Uma mensagem será exibida perguntando se você tem certeza de que deseja desabilitar a caixa de correio. Clique em **Sim** para desabilitar a caixa de correio.

A caixa de correio é removida da lista de caixas de correio.

## Usar o Shell para desabilitar uma caixa de correio

Use o seguinte comando para desabilitar caixas de correio de usuário, caixas de correio vinculadas, caixas de correio de recurso e caixas de correio compartilhadas.

    Disable-Mailbox <identity>

Quando você executa esse comando, uma mensagem é exibida que pede para você confirmar se deseja desabilitar a caixa de correio.

Aqui estão alguns exemplos de comandos para desabilitar as caixas de correio.

```
    Disable-Mailbox danj
```
```
    Disable-Mailbox "Conf Room 31/1234 (12)"
```
```
    Disable-Mailbox sharedmbx@contoso.com
```

## Como saber se funcionou?

Para confirmar se você desabilitou uma caixa de correio com êxito, siga um destes procedimentos:

  - No EAC, clique em **Destinatários**, vá para a página adequada para o tipo de caixa de correio que desabilitou e depois verifique se a caixa de correio não está mais listada.

  - Em Usuários e Computadores do Active Directory, clique com o botão direito do mouse na conta de usuário cuja caixa de correio foi desabilitada e, em seguida, clique em **Propriedades**. Na guia **Geral**, o campo **Email** está em branco. Isso confirma que a caixa de correio está desabilitada, mas a conta de usuário ainda existe.

  - No Shell, execute o comando a seguir.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    O valor de `Disabled` na propriedade *DisconnectReason* indica que a caixa de correio está desabilitada.
    

    > [!NOTE]
    > Quando você exclui uma caixa de correio, o valor na propriedade <EM>DisconnectReason</EM> também é <CODE>Disabled</CODE>. No entanto, a conta de usuário do Active Directory correspondente é excluída.



  - No Shell, execute o comando a seguir.
    
        Get-User <identity>
    
    O valor para a propriedade *RecipientType* é `User`, em vez de `UserMailbox`, que é o valor para usuários com caixas de correio habilitadas. Isso também confirma que a caixa de correio está desabilitada, mas a conta de usuário é mantida.

## Excluir uma caixa de correio

Como especificado anteriormente, quando você exclui uma caixa de correio, os atributos do Exchange e a conta de usuário do Active Directory são excluídos. A caixa de correio (e a caixa de correio de arquivo morto, se estiver habilitada) será excluída permanentemente do banco de dados de caixa de correio depois que o período de retenção da caixa de correio expirar.

## Usar o EAC para excluir uma caixa de correio

O procedimento a seguir mostra como excluir uma caixa de correio do usuário. Use o mesmo procedimento para excluir outros tipos de caixa de correio após ir para a página apropriada no EAC.

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio que deseja excluir e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  Uma mensagem será exibida perguntando se você tem certeza de que deseja excluir a caixa de correio. Clique em **Sim** para excluir a caixa de correio.

A caixa de correio é removida da lista de caixas de correio.

## Usar o Shell para excluir uma caixa de correio

Use o seguinte comando para excluir caixas de correio de usuário, caixas de correio vinculadas, caixas de correio de recurso e caixas de correio compartilhadas.

    Remove-Mailbox <identity>

Quando você executa esse comando, uma mensagem é exibida que pede para você confirmar se deseja remover a caixa de correio e a conta de usuário do Active Directory correspondente.

Aqui estão alguns exemplos de comandos para excluir caixas de correio.

```
    Remove-Mailbox pilarp@contoso.com
```
```
    Remove-Mailbox "Fleet Van (16)"
```

```
    Remove-Mailbox corpprint
```

## Como saber se funcionou?

Para confirmar se você excluiu uma caixa de correio com êxito, siga um destes procedimentos de verificação.

1.  No EAC, clique em **Destinatários** e vá para a página adequada para o tipo de caixa de correio que excluiu e verifique se a caixa de correio não está mais listada.

2.  Em Usuários e Computadores do Active Directory, verifique se a conta de usuário correspondente não está mais listada.

Ou

1.  Execute o seguinte comando para verificar se a caixa de correio foi excluída.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    O valor `Disabled` na propriedade *DisconnectReason* indica que a caixa de correio foi excluída.
    

    > [!NOTE]
    > Quando você desabilita uma caixa de correio, o valor na propriedade <EM>DisconnectReason</EM> também é <CODE>Disabled</CODE>. No entanto, a conta de usuário do Active Directory correspondente é mantida.



2.  Execute o seguinte comando para verificar se a conta de usuário do Active Directory foi excluída.
    
        Get-User <identity>
    
    O comando retornará um erro que diz que o usuário não foi encontrado, confirmando que a conta foi excluída.

