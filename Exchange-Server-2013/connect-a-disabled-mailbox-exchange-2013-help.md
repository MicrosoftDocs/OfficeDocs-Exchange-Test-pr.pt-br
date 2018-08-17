---
title: 'Conectar uma caixa de correio desabilitada: Exchange 2013 Help'
TOCTitle: Conectar uma caixa de correio desabilitada
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50556266
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar uma caixa de correio desabilitada

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-13_

Use o EAC ou o Shell para conectar uma caixa de correio desabilitada a uma conta de usuário do Active Directory. Ao desabilitar uma caixa de correio, o Exchange a mantém no banco de dados de caixa de correio e altera seu estado para desabilitado. Os atributos do Exchange também são removidos da conta de usuário do Active Directory correspondente, mas a conta é mantida. A caixa de correio é mantida até que o período de retenção da caixa de correio excluída expire, que é de 30 dias por padrão e, então, ela é permanentemente excluída (ou *eliminada*) do banco de dados de caixa de correio.

Até que uma caixa de correio desabilitada seja excluída permanentemente do banco de dados de caixa de correio do Exchange, você poder usar o EAC ou o Shell para reconectá-la à conta de usuário do Active Directory original.

Para saber mais sobre caixas de correio desconectadas e executar outras tarefas de gerenciamento relacionadas, confira estes tópicos:

  - [Caixas de correio desconectadas](disconnected-mailboxes-exchange-2013-help.md)

  - [Desabilitar ou excluir uma caixa de correio](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Conectar-se ou restaurar uma caixa de correio excluída](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Execute o cmdlet **Get-User** no Shell para verificar se a conta de usuário do Active Directory à qual você deseja conectar a caixa de correio desabilitada existe, e se já não está associada a outra caixa de correio. Para conectar uma caixa de correio desabilitada a uma conta de usuário, a conta deve existir e o valor da propriedade *RecipientType* deve ser `User`, que indica que a conta não está habilitada para uma caixa de correio.
    
    Para organizações locais do Exchange, você também pode verificar essas informações em Usuários e Computadores do Active Directory.

  - Execute o seguinte comando para verificar se a caixa de correio desabilitada à qual você deseja conectar uma conta de usuário existe no banco de dados de caixa de correio e se não se trata de uma caixa de correio excluída por software.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    Para poder conectar uma caixa de correio desabilitada, ela deve existir no banco de dados de caixas de correio e o valor da propriedade *DisconnectReason* deve ser `Disabled`. Se a caixa de correio tiver sido eliminada do banco de dados, o comando não retornará resultados.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para conectar uma caixa de correio desabilitada

O procedimento a seguir mostra como conectar uma caixa de correio do usuário desabilitada. Você pode também reconectar caixas de correio vinculadas desabilitadas e caixas de correio compartilhadas desabilitadas à conta de usuário correspondente.

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e depois em **Conectar uma caixa de correio**.
    
    Uma lista de caixas de correio desconectadas no servidor do Exchange selecionado em sua organização do Exchange será exibida.
    

    > [!NOTE]
    > Essa lista de caixas de correio desconectadas inclui caixas de correio desabilitadas, caixas de correio excluídas e caixas de correio excluídas de forma reversível.



3.  Clique na caixa de correio desabilitada que deseja reconectar e, em seguida, clique em **Conectar**.

4.  Na janela que pergunta se você tem certeza de que deseja reconectar a caixa de correio, clique em **Sim**.
    
    O Exchange reconectará a caixa de correio desabilitada para a conta de usuário correspondente.

## Usar o Shell para conectar uma caixa de correio desabilitada

Use o cmdlet **Connect-Mailbox** no Shell para conectar uma conta de usuário a uma caixa de correio desabilitada. Você precisa especificar o tipo de caixa de correio que está conectando. Os exemplos a seguir mostram a sintaxe para reconectar caixas de correio compartilhadas, vinculadas e de usuário.

Este exemplo conecta uma caixa de correio de usuário. O parâmetro *Identity* especifica a caixa de correio desconectada no banco de dados do Exchange. O parâmetro *User* especifica a conta de usuário do Active Directory à qual a caixa de correio será reconectada.

    Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"

Este exemplo conecta uma caixa de correio vinculada. O parâmetro *Identity* especifica a caixa de correio desconectada do banco de dados do Exchange. O parâmetro *LinkedMasterAccount* especifica a conta de usuário do Active Directory na floresta de conta à qual deseja reconectar a caixa de correio. O parâmetro *Alias* especifica o alias, que é a parte do endereço de email à esquerda do símbolo arroba (@), para a caixa de correio reconectada.

    Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia

Este exemplo conecta uma caixa de correio compartilhada.

    Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared


> [!NOTE]
> Se você não incluir o parâmetro <EM>Alias</EM> ao executar o cmdlet <STRONG>Connect-Mailbox</STRONG>, o valor especificado nos parâmetros <EM>User</EM> ou <EM>LinkedMasterAccount</EM> será usado para criar o alias do endereço de email para a caixa de correio reconectada.



Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Connect-Mailbox](https://technet.microsoft.com/pt-br/library/aa997878\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você conectou com êxito a caixa de correio desabilitada a uma conta de usuário, siga um destes procedimentos:

  - No EAC, clique em **Destinatários**, navegue até a página apropriada para o tipo de caixa de correio que você reconectou, clique em **Atualizar**![Ícone Atualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Ícone Atualizar") e verifique se a caixa de correio está listada.

  - Em Usuários e Computadores do Active Directory, clique com o botão direito do mouse na conta de usuário cuja caixa de correio foi desabilitada e clique em **Propriedades**. Na guia **Geral**, observe que a caixa **Email** está preenchida com o endereço de email da caixa de correio reconectada.

  - No Shell, execute o comando a seguir.
    
        Get-User <identity>
    
    O valor de **UserMailbox** para a propriedade *RecipientType* indica que a conta de usuário e a caixa de correio estão conectadas. Você também pode executar o cmdlet **Get-Mailbox** para verificar se a caixa de correio existe.

