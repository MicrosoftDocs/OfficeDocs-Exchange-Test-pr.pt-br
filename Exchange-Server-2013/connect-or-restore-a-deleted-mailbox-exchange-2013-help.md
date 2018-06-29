---
title: 'Conectar-se ou restaurar uma caixa de correio excluída: Exchange 2013 Help'
TOCTitle: Conectar-se ou restaurar uma caixa de correio excluída
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50556249
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar-se ou restaurar uma caixa de correio excluída

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-05-04_

É possível utilizar o EAC ou o Shell para conectar uma caixa de correio excluída a uma conta de usuário do Active Directory. Ao excluir uma caixa de correio, o Exchange mantém a caixa de correio no banco de dados de caixa de correio e alterna a caixa de correio para um estado desabilitado. A conta de usuário do Active Directory associada também é excluída. A caixa de correio fica retida até o período de retenção da caixa de correio excluída expirar, que é de 30 dias por padrão. Depois disso, ela será excluída (ou *eliminada*) permanentemente do banco de dados de caixa de correio.

Até uma caixa de correio excluída de forma reversível ser excluída permanentemente do banco de dados de caixa de correio do Exchange, é possível utilizar o EAC ou o Shell para conectá-la a uma conta de usuário do Active Directory. Também é possível utilizar o Shell para restaurar o conteúdo da caixa de correio excluída para uma caixa de correio existente.

Para saber mais sobre caixas de correio desconectadas e executar outras tarefas de gerenciamento relacionadas, confira estes tópicos:

  - [Caixas de correio desconectadas](disconnected-mailboxes-exchange-2013-help.md)

  - [Desabilitar ou excluir uma caixa de correio](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Conectar uma caixa de correio desabilitada](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Excluir permanentemente uma caixa de correio](permanently-delete-a-mailbox-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Crie uma nova conta de usuário no Active Directory para conectar a caixa de correio excluída. Ou utilize o cmdlet **Get-User** no Shell para verificar se a conta de usuário do Active Directory à qual deseja conectar a caixa de correio excluída existe e se ela já não está associada a outra caixa de correio. Para conectar uma caixa de correio excluída a uma conta de usuário, a conta deverá existir, e o valor da propriedade *RecipientType* precisará ser `User`, o que indica que a conta ainda não está habilitada para caixa de correio.
    
    Para organizações locais do Exchange, você também pode verificar essas informações em Usuários e Computadores do Active Directory.
    

    > [!IMPORTANT]
    > Ao conectar as caixas de correio vinculadas excluídas, caixas de correio de recursos ou caixas de correio compartilhadas, a conta de usuário do Active Directory à qual você está conectando a caixa de correio deverá ser desabilitada.



  - Para verificar se a caixa de correio excluída à qual deseja conectar uma conta de usuário existe no banco de dados de caixa de correio e não é uma caixa de correio excluída de forma reversível, execute o seguinte comando.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    A caixa de correio excluída precisa existir no banco de dados de caixa de correio, e o valor da propriedade *DisconnectReason* precisa ser `Disabled`. Se a caixa de correio tiver sido limpa a partir do banco de dados, o comando não retornará nenhum resultado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## O que você deseja fazer?

## Conectar uma caixa de correio excluída

Ao conectar uma caixa de correio excluída, você associa a caixa de correio a uma conta de usuário que não está habilitada para email, o que significa que ela não tem uma caixa de correio existente. Para conectar uma caixa de correio excluída a uma conta de usuário que tenha uma caixa de correio, é preciso restaurar a caixa de correio excluída. Para saber mais, confira Restaurar uma caixa de correio excluída mais adiante neste tópico.

## Utilizar o EAC para conectar uma caixa de correio excluída

O procedimento seguinte mostra como conectar uma caixa de correio de usuário excluída a uma conta de usuário. Você pode também usar esse procedimento para conectar caixas de correio vinculadas, caixas de correio de recursos e caixas de correio compartilhadas que tenham sido excluídas para uma conta de usuário.

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e depois em **Conectar uma caixa de correio**.
    
    Uma lista de caixas de correio desconectadas no servidor do Exchange selecionado em sua organização do Exchange será exibida.
    

    > [!TIP]
    > Essa lista de caixas de correio desconectadas inclui caixas de correio desabilitadas, caixas de correio excluídas e caixas de correio excluídas de forma reversível.



3.  Clique na caixa de correio excluída à qual deseja conectar um usuário e clique em **Conectar**.

4.  Na janela que pergunta se você tem certeza de que deseja conectar a caixa de correio, clique em **Sim**.
    
    É exibida uma lista de contas de usuário que não estão habilitados para email.

5.  Clique no usuário ao qual você deseja conectar a caixa de correio excluída e clique em **OK**.
    
    O Exchange conectará a caixa de correio excluída à conta de usuário selecionada.

## Utilize o Shell para conectar uma caixa de correio excluída

Use o cmdlet **Connect-Mailbox** no Shell para conectar uma caixa de correio excluída a uma conta de usuário que não está habilitada para email. Você precisa especificar o tipo de caixa de correio que está conectando. Os exemplos a seguir mostram a sintaxe de reconexão de caixas de correio de usuário, vinculadas, de ambiente, de equipamento e compartilhadas. Em todos os exemplos, o parâmetro *Alias* é usado para especificar o alias de email, que é a porção do endereço de email no lado esquerdo do símbolo de arroba (@). Se você não incluir o parâmetro *Alias*, o valor especificado no parâmetro *User* ou *LinkedMasterAccount* será usado para criar o alias do endereço de email da caixa de correio reconectada.


> [!TIP]
> Conforme mencionado anteriormente, quando você conectar caixas de correio vinculadas, de recurso ou compartilhadas, a conta de usuário do Active Directory à qual está vinculando a caixa de correio deverá ser desabilitada.



Este exemplo conecta-se a uma caixa de correio de usuário. O parâmetro *Identity* especifica o nome para exibição da caixa de correio excluída mantida no banco de dados de caixa de correio denominado MBXDB01. O parâmetro *User* especifica a conta de usuário do Active Directory para conectar a caixa de correio.

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw


> [!TIP]
> Você pode também usar os valores das propriedades <CODE>LegacyDN</CODE> ou <CODE>MailboxGuid</CODE> para identificar a caixa de correio excluída.



Este exemplo conecta uma caixa de correio vinculada. O parâmetro *Identity* especifica a caixa de correio excluída no banco de dados de caixa de correio denominado MBXDB02. O parâmetro *LinkedMasterAccount* especifica a contas de usuário do Active Directory na floresta de conta à qual deseja conectar a caixa de correio. O parâmetro *LinkedDomainController* especifica um controlador de domínio na floresta de contas.

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

Este exemplo conecta uma caixa de correio de sala.

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

Este exemplo conecta uma caixa de correio de equipamento.

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

Este exemplo conecta uma caixa de correio compartilhada.

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared


> [!TIP]
> Você pode também usar os valores <CODE>LegacyDN</CODE> ou <CODE>MailboxGuid</CODE> para identificar a caixa de correio excluída.



Para informações detalhadas sobre sintaxes e parâmetros, confira [Connect-Mailbox](https://technet.microsoft.com/pt-br/library/aa997878\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você conectou com êxito uma caixa de correio excluída a uma conta de usuário, siga um destes procedimentos:

  - No EAC, clique em **Destinatários**, navegue até a página apropriada do tipo de caixa de correio conectado, clique em **Atualizar**![Ícone Atualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Ícone Atualizar") e verifique se a caixa de correio está listada.

  - Em Usuários e Computadores do Active Directory, clique com o botão direito do mouse na conta de usuário que conectou à caixa de correio e clique em **Propriedades**. Na guia **Geral**, a caixa **Email** está preenchida com o endereço de email da caixa de correio conectada.

  - No Shell, execute o comando a seguir.
    
        Get-User <identity>
    
    O valor de **UserMailbox** da propriedade *RecipientType* indica que a conta de usuário e a caixa de correio estão conectadas. Você pode também executar o comando **Get-Mailbox \<identity\>** para verificar se a caixa de correio estava conectada.

## Restaurar uma caixa de correio excluída

É possível usar o Shell para restaurar uma caixa de correio excluída para uma caixa de correio existente usando o cmdlet **New-MailboxRestoreRequest**. Ao restaurar uma caixa de correio excluída, seu conteúdo será copiado para uma caixa de correio existente, chamada de *caixa de correio de destino*. Após a restauração de uma caixa de correio excluída, ela ainda fica mantida no banco de dados de caixa de correio até ser excluída permanentemente por um administrador ou eliminada quando o período de retenção da caixa de correio excluída expirar.

Após uma solicitação de restauração de caixa de correio ser concluída com êxito, ela ficará retida por 30 dias, por padrão, antes de ser removida. Você pode removê-la mais cedo, usando o cmdlet **Remove-StoreMailbox**.


> [!TIP]
> O EAC não pode ser usado para restaurar uma caixa de correio excluída.



## Utilize o Shell para restaurar uma caixa de correio excluída

Para criar uma solicitação de restauração de caixa de correio, é preciso usar o nome para exibição, a GUID da caixa de correio ou o nome diferenciado (DN) herdado da caixa de correio excluída. Use o **Get-MailboxStatistics** cmdlet para exibir os valores das propriedades `DisplayName`, `MailboxGuid` e `LegacyDN` da caixa de correio excluída que você deseja restaurar. Por exemplo, execute o seguinte comando para retornar essas informações de todas as caixas de correio excluídas na sua organização.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

Este exemplo restaura uma caixa de correio excluída, que é identificada pelo parâmetro *SourceStoreMailbox* e está localizada no banco de dados de caixa de correio MBXDB01, para a caixa de correio de destino Lara Cardoso. O parâmetro *AllowLegacyDNMismatch* é usado para que a caixa de correio de origem possa ser restaurada para uma caixa de correio diferente que não tenha o mesmo valor de DN herdado.

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

Este exemplo restaura a caixa de correio de arquivo morto excluída de Brenda Fernandes para sua caixa de correio de arquivo morto atual. O parâmetro *AllowLegacyDNMismatch* não é necessário porque uma caixa de correio principal e sua caixa de correio de arquivo morto correspondente têm o mesmo DN herdado.

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)).

## Utilize o Shell para restaurar uma caixa de correio de pasta pública excluída

Se você excluiu uma caixa de correio de pasta pública de forma irreversível, e agora deseja restaurá-la, e a caixa de correio está dentro do limite de Retenção de Itens Excluídos (confira [Configurar cotas de itens recuperáveis e retenção de Item excluído](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)), você pode usar o cmdlet `Connect-Mailbox`, seguido pelo cmdlet `Update-StoreMailboxState`. Para obter informações detalhadas de sintaxes e de parâmetros, confira [Connect-Mailbox](https://technet.microsoft.com/pt-br/library/aa997878\(v=exchg.150\)) e [Update-StoreMailboxState](https://technet.microsoft.com/pt-br/library/jj860462\(v=exchg.150\)).

Será necessário o GUID da caixa de correio de pasta pública excluída, além do GUID ou o nome do banco de dados da caixa de correio que continha a caixa de correio de pasta pública. Se você não tiver essas informações, siga as seguintes etapas:

1.  Obtenha o nome de domínio totalmente qualificado (FQDN) do controlador e a floresta do Active Directory executando o seguinte cmdlet:
    
        Get-OrganizationConfig | fl OriginatingServer

2.  Com as informações retornadas pela Etapa 1, pesquise o contêiner Objetos Excluídos no Active Directory pelo GUID da caixa de correio de pasta pública e pelo GUID ou nome do banco de dados da caixa de correio na qual a caixa de correio de pasta pública excluída estava.
    

    > [!TIP]
    > Você pode pesquisar o contêiner Objetos Excluídos usando um script personalizado ou usando o utilitário Ldp, que pode ser aberto ao digitar <STRONG>ldp.exe</STRONG> em um prompt do Powershell.



Ao descobrir o GUID da caixa de correio de pasta pública excluída e o nome ou GUID da caixa de correio do banco de dados que continha a caixa de correio de pasta pública, execute os seguintes comandos para restaurar a caixa de correio de pasta pública.

1.  Crie um novo objeto do Active Directory executando os seguintes comandos (você pode ser solicitado a fornecer credenciais apropriadas):
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    Onde `<mailUserName>`, `<emailAddress>` e `<mailUserName>` são valores que você escolher. Você precisará usar o mesmo valor de `<mailUserName>` na próxima etapa.

2.  Conecte a caixa de correio de pasta pública excluída ao objeto do Active Directory que você acabou de criar executando o comando a seguir:
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    

    > [!TIP]
    > O parâmetro <CODE>Identity</CODE> especifica o objeto de caixa de correio no banco de dados do Exchange para conectar a um objeto de usuário do Active Directory. O exemplo acima especifica o GUID da caixa de correio de pasta pública, mas você também pode usar o valor do Nome de Exibição ou o valor LegacyExchangeDN.



3.  Execute `Update-StoreMailboxState` na caixa de correio de pasta pública usando o exemplo a seguir como base:
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    Como na Etapa 2, o parâmetro `Identity` aceitará valores do GUID, Nome para Exibição ou LegacyExchangeDN para a caixa de correio de pasta pública.

## Como saber se funcionou?

Para verificar se uma caixa de correio de pasta pública excluída já foi restaurada, execute o cmdlet **Get-PublicFolder -GetChildren -\<public folder mailbox GUID\>**. Este cmdlet funcionará se a restauração tiver sido bem-sucedida.

Para obter mais informações, consulte:

  - [Connect-Mailbox](https://technet.microsoft.com/pt-br/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/pt-br/library/jj860462\(v=exchg.150\))

