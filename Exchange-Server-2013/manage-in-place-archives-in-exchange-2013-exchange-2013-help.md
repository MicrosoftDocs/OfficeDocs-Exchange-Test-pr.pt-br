---
title: 'Gerenciar arquivos mortos de In-loco no Exchange 2013: Exchange 2013 Help'
TOCTitle: Gerenciar arquivos mortos de In-loco no Exchange 2013
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 50485510
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar arquivos mortos de In-loco no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-02-01_

Arquivamento in-loco ajuda você a recuperar o controle de dados de mensagens da sua organização, eliminando a necessidade de arquivos de armazenamento pessoal (. pst) e permitindo que você atenda aos requisitos de retenção e descoberta eletrônica de mensagem da sua organização. Com o arquivamento habilitado, os usuários podem armazenar mensagens em uma caixa de correio de arquivo morto, que pode ser acessada por meio de MicrosoftOutlook e Outlook Web App.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Arquivamento In-loco" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Não há suporte para que a caixa de correio principal do usuário residem em uma versão mais antiga do Exchange que o arquivo do usuário. Se a caixa de correio principal do usuário for ainda no Exchange 2010, você deve movê-la para o Exchange 2013 ao mesmo tempo em que você mova o arquivo morto para o Exchange 2013.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma caixa de correio e habilitar um arquivo morto no local

## Usar o EAC

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  Clique em **Nova** \> **Caixa de correio de usuário**.

3.  Na página **Nova caixa de correio de usuário**, na caixa **Alias**, digite o alias do usuário.
    

    > [!TIP]
    > Se você deixar essa caixa em branco, o valor digitado em <STRONG>Nome de logon do usuário</STRONG> será usado como o alias.



4.  Selecione uma das seguintes opções:
    
      - **Usuário existente**   Clique nesse botão e então clique em **Procurar** para abrir a caixa de diálogo **Selecionar Usuário – Floresta Inteira** dialog box. Essa caixa de diálogo exibe uma lista de contas de usuário do Active Directory existentes na floresta que não são habilitadas para email nem possuem caixas de correio do Exchange. Selecione a conta de usuário que você deseja habilitar para email e clique em **OK** para retornar ao assistente. Se você selecionar essa opção, não terá que fornecer informações de conta de usuário, porque essas informações já existirão no Active Directory.
    
      - **Novo usuário**   Clique nesse botão para criar uma nova conta de usuário no Active Directory e criar uma caixa de correio para ele. Se você selecionar essa opção, terá que fornecer as informações de conta de usuário necessárias.
    

    > [!TIP]
    > A conta Active Directory&nbsp;associada a caixas de correio de usuários deve residir na mesma floresta que o servidor Exchange. Para criar uma caixa de correio para uma conta de usuário que esteja em uma floresta confiável, você terá que criar uma caixa de correio vinculada. Para obter detalhes, consulte <A href="manage-linked-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio vinculadas</A>.



5.  Clique em **Mais opções**, para definir as configurações a seguir.
    
      - **Banco de dados de caixa de correio**   Clique em **Procurar** para selecionar um banco de dados de caixa de correio para armazenar a caixa de correio. Se você não selecionar um banco de dados, o Exchange atribuirá um automaticamente.
    
      - **Arquivo morto**   Marque essa caixa de seleção para criar uma caixa de correio de arquivamento para a caixa de correio. Se você criar uma caixa de correio de arquivo morto, os itens da caixa de correio serão movidos automaticamente da caixa de correio principal para o arquivo morto, com base nas configurações da política de retenção padrão ou naquelas que você definiu.
        
        Clique em **Procurar** para selecionar um banco de dados que esteja na floresta local, para armazenar a caixa de correio de arquivo morto.
        
        Para saber mais, consulte [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Política do catálogo de endereços**   Use essa lista para selecionar uma política de catálogo de endereços (ABP) para a caixa de correio. As ABPs contêm um catálogo de endereços global (GAL), um catálogo de endereços offline (OAB), uma lista de salas e um conjunto de listas de endereços. Quando atribuída aos usuários da caixa de correio, uma ABP fornece a eles acesso a uma GAL personalizada no Outlook e no Outlook Web App. Para saber mais, consulte [Políticas de catálogo de endereços](address-book-policies-exchange-2013-help.md).

6.  Após concluir, clique em **Salvar** para criar a caixa de correio.

## Usar o Shell

Este exemplo cria o usuário Chris Ashton no Active Directory, cria a caixa de correio no banco de dados de caixa de correio DB01 e habilita um arquivo morto. A senha deve ser redefinida no próximo logon. Para definir o valor inicial da senha, este exemplo cria uma variável ($password), solicita que você insira uma senha e atribui a senha à variável como um objeto SecureString.

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito uma caixa de correio de usuário, com um arquivo morto local, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio** e selecione a nova caixa de correio do usuário na lista. No painel de detalhes, em **Arquivo In-loco**, confirme se ele está definido como **Habilitado**. Clique em **Exibir detalhes** para exibir propriedades do arquivo morto, incluindo o status do arquivo morto e o banco de dados de caixa de correio em que ele é criado.

  - No Shell, execute o comando a seguir, para exibir informações sobre a nova caixa de correio de usuário e o arquivo morto.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - No Shell, use o cmdlet **Test-ArchiveConnectivity**, para testar a conectividade ao arquivo morto. Para obter um exemplo de como testar a conectividade do arquivo morto, consulte a seção Exemplos em [Test-ArchiveConnectivity](https://technet.microsoft.com/pt-br/library/hh529914\(v=exchg.150\)).

## Habilitar um arquivo morto local para a caixa de correio existente

Você também pode criar arquivos mortos para usuário existentes que tenham uma caixa de correio, mas não estejam habilitados para arquivo morto. Isso é conhecido como *habilitar um arquivo morto* para uma caixa de correio existente.

## Usar o EAC

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  Selecione uma caixa de correio.

3.  No painel de detalhes, em **Arquivo In-loco**, clique em **Habilitar**.
    

    > [!TIP]
    > Também é possível habilitar arquivos em massa selecionando várias caixas de correio (use as teclas Shift ou Ctrl). Depois de selecionar várias caixas de correio, no painel de detalhes, clique em <STRONG>Mais opções</STRONG>. Em seguida, em <STRONG>Arquivo Morto</STRONG>, clique em <STRONG>Habilitar</STRONG>.



4.  Na página **Criar arquivo morto in-loco**, clique em **OK**, para o Exchange selecionar automaticamente um banco de dados de caixa de correio para o arquivo morto ou clique em **Procurar** para especificar um.

## Usar o Shell

Este exemplo habilita o arquivo morto da caixa de correio de Tony Smith.

    Enable-Mailbox "Tony Smith" -Archive

Este exemplo recupera caixas de correio no banco de dados DB01 que não têm um arquivo morto local ou baseado em nuvem habilitado, além de não terem um nome começando com DiscoverySearchMailbox. Ele canaliza o resultado do cmdlet **Enable-Mailbox**, para habilitar o arquivo morto para todas as caixas de correio no banco de dados de caixa de correio DB01.

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Enable-Mailbox](https://technet.microsoft.com/pt-br/library/aa998251\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você habilitou com êxito em um arquivo morto local para uma caixa de correio existente, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio** e selecione a caixa de correio na lista. No painel de detalhes, em **Arquivo In-loco**, confirme se ele está definido como **Habilitado**. Clique em **Exibir detalhes** para exibir propriedades do arquivo morto, incluindo o status do arquivo morto e o banco de dados de caixa de correio em que ele é criado.

  - No Shell, execute o comando a seguir para exibir informações sobre o novo arquivo morto.
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - No Shell, use o cmdlet **Test-ArchiveConnectivity**, para testar a conectividade ao arquivo morto. Para um exemplo de como testar a conectividade do arquivo morto, veja os Exemplos em [Test-ArchiveConnectivity](https://technet.microsoft.com/pt-br/library/hh529914\(v=exchg.150\)).

## Desabilitar um arquivo morto local

Você pode desabilitar o arquivo morto de um usuário para fins de solução de problemas ou se estiver movendo a caixa de correio para uma versão do Exchange que não suporte Arquivamento In-loco. Se você desabilitar um arquivo morto local, todas as informações dele serão mantidas no banco de dados de caixa de correio até o tempo de retenção de caixa de correio passar e o arquivo morto ser excluído permanentemente. (Por padrão, o Exchange mantém as caixas de correio desconectadas, incluindo caixas de correio de arquivo morto, por 30 dias.)


> [!IMPORTANT]
> Desabilitar o arquivo morto o removerá da caixa de correio e o marcará no banco de dados de caixa de correio para exclusão.



Se você quiser reconectar o arquivo morto local a essa caixa de correio, poderá usar o cmdlet [Connect-Mailbox](https://technet.microsoft.com/pt-br/library/aa997878\(v=exchg.150\)) com o parâmetro *Archive*.

## Usar o EAC

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  Selecione uma caixa de correio.

3.  No painel de detalhes, em **Arquivo In-loco**, clique em **Desabilitar**.
    

    > [!TIP]
    > Também é possível desabilitar arquivos mortos em massa selecionando várias caixas de correio (use as teclas Shift ou Ctrl). Depois de selecionar várias caixas de correio, no painel de detalhes, clique em <STRONG>Mais opções</STRONG>. Em seguida, em <STRONG>Arquivo Morto</STRONG>, clique em <STRONG>Desabilitar</STRONG>.



## Usar o Shell

Este exemplo desabilita o arquivo morto da caixa de correio de Chris Ashton. Ele não desabilita a caixa de correio.

    Disable-Mailbox -Identity "Chris Ashton" -Archive

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Disable-Mailbox](https://technet.microsoft.com/pt-br/library/aa997210\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você desabilitou com êxito um arquivo morto, faça o seguinte:

  - No EAC, selecione a caixa de correio. Em seguida, no painel de detalhes, verifique o status de arquivamento em **Arquivo Morto In-loco**.

  - No Shell, execute o comando a seguir para verificar as propriedades do arquivo morto para o usuário de caixa de correio.
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    Se o arquivo morto estiver desabilitado, os seguintes valores serão retornados, para propriedades relativas a arquivo morto.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Propriedade</th>
    <th>Valor</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase (para arquivos mortos locais)</p></td>
    <td><p>&lt;em branco&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase (para arquivos mortos locais)</p></td>
    <td><p>&lt;nome do banco de dados de caixa de correio&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;guid do arquivo morto desabilitado&gt;</p></td>
    </tr>
    </tbody>
    </table>


## Conectar um arquivo morto local

Quando você desabilitar uma caixa de correio de arquivo morto, ele se tornará desconectado. Uma caixa de correio de arquivo morto desconectado é mantida no banco de dados de caixa de correio por um tempo determinado. Por padrão, o Exchange retém os arquivos mortos desconectados por 30 dias. Durante esse tempo, você pode recuperar o arquivo morto, associando-o a uma caixa de correio existente. Você pode modificar o período de retenção de caixa de correio excluída, para reter uma caixa de correio ou arquivo morto excluído por um período maior ou menor.


> [!WARNING]
> Se você desabilitar um arquivo morto para um usuário e depois habilitar o arquivo morto para o mesmo usuário, ele irá receber um novo arquivo morto. O novo arquivo morto não irá conter os dados que estavam no arquivo morto desconectado do usuário. Se você quiser reconectar um usuário ao seu arquivo morto desconectado, deverá usar este procedimento.




> [!TIP]
> Você não pode usar o EAC para conectar um arquivo morto desconectado a um usuário de caixa de correio.



## Usar o Shell

1.  Se você não souber o nome do arquivo morto, você poderá exibi-lo no Shell, executando o seguinte comando. Este exemplo recupera o banco de dados de caixa de correio DB01, envia-o em pipe para o cmdlet **Get-MailboxStatistics** para recuperar estatísticas de caixa de correio para todas as caixas de correio no banco de dados e então usa o cmdlet **Where-Object** para filtrar os resultados e recuperar uma lista de arquivos mortos desconectados. O comando mostra informações adicionais sobre cada arquivo morto, como a GUID e a contagem de itens.
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  Conecte o arquivo morto à caixa de correio principal. Este exemplo conecta o arquivo de Chris Ashton à caixa de correio principal de Chris Ashton e usa o GUID como a identidade do arquivo morto.
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/pt-br/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/pt-br/library/aa998251\(v=exchg.150\))

## Como saber se funcionou?

Para verificar se você conectou com êxito um arquivo morto desconectado a um usuário de caixa de correio, execute este comando do Shell, para recuperar as propriedades do arquivo morto do usuário de caixa de correio e verificar os valores retornados para as propriedades *ArchiveGuid* e *ArchiveDatabase*:

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

