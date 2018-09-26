---
title: 'Habilitar ou desabilitar email para um usuário de email: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar email para um usuário de email
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50556155
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar ou desabilitar email para um usuário de email

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-11-14_

Você pode desabilitar o email para um usuário de email existente na sua organização do Exchange. Ao desabilitar o email para um usuário de email, ele é removido do Exchange e do catálogo de endereços de sua organização. Se o usuário de email for um membro de um grupo de distribuição, o usuário não receberá mais emails enviados ao grupo. Além disso, os atributos do Exchange são removidos do objeto do usuário no Active Directory, mas o objeto de usuário e seus atributos que não pertencem ao Exchange (como informações de contato e da organização) permanecerão no Active Directory.

Após desabilitar o email para um usuário de email, você pode habilitar o usuário para email novamente usando o cmdlet **Enable-MailUser** no Shell. Você também pode usar esse cmdlet para habilitar qualquer usuário do Active Directory.


> [!NOTE]
> Usuários de email (também chamados de <EM>usuários habilitados para email</EM>) são diferentes de usuários na sua organização que possuem uma caixa de correio. A principal diferença é que usuários de email representam usuários fora da sua organização do Exchange que possuem endereços de email externos. Eles não têm uma caixa de correio em sua organização. Para obter mais informações sobre as diferenças entre usuários que possuem caixas de correio em sua organização e usuários de email, consulte <A href="recipients-exchange-2013-help.md">Destinatários</A>.



Para outras tarefas de gerenciamento adicionais relacionadas a usuários de email, consulte [Gerenciar usuários de email](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-mail-users).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos.

  - Entrada "Usuários da caixa de correio" Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Desabilitar email para um usuário de email

Como especificado anteriormente, quando você desabilita o email para um usuário de email, os atributos do Exchange são removidos do objeto de usuário de email do Active Directory correspondente, mas o usuário é mantido. O usuário de email é removido da lista de usuários de email no EAC, mas você pode visualizar e gerenciar o objeto de contato do Active Directory correspondente usando Usuários e Computadores do Active Directory ou usando os cmdlets **Get-MailUser** e **Set-Set-MailUser** no Shell.

## Usar o EAC para desabilitar o email para um usuário de email

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Na lista de contatos, clique no usuário de email para qual deseja desabilitar o email.

3.  Clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e, em seguida, clique em **Desabilitar**.

4.  Uma mensagem será exibida perguntando se você tem certeza de que deseja desabilitar o usuário de email selecionado. Clique em **Sim** para desabilitá-lo.

O usuário de email será removido da lista de contatos.

## Usar o Shell para desabilitar o email para um usuário de email

Este exemplo desabilita o email para o usuário de email Yan Li.

```powershell
Disable-MailUser -Identity "Yan Li"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Disable-MailUser](https://technet.microsoft.com/pt-br/library/aa998578\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você desabilitou com êxito o email para um usuário de email, siga uma destas opções:

1.  No EAC, vá para **Destinatários** \> **Contatos** e verifique se o usuário de email não está mais listado.

2.  Em Usuários e Computadores do Active Directory, clique com o botão direito no usuário e depois clique em **Propriedades**. Na guia **Geral**, observe que a caixa **Email** está em branco. Isso confirma que o usuário de email não está habilitado para email.

3.  No Shell, execute o comando a seguir.
    
    ```powershell
    Get-MailUser
    ```
    
    O usuário de email para o qual você desabilitou o email não será listado nos resultados porque esse cmdlet retorna apenas usuários habilitados para email.

4.  No Shell, execute o comando a seguir.
    
    ```powershell
    Get-User
    ```
    
    O usuário de email para o qual você desabilitou o email será listado nos resultados porque esse cmdlet retorna todos os objetos de usuário do Active Directory.

## Usar o Shell para habilitar usuários para email

Você pode usar o cmdlet **Enable-MailUser** para habilitar usuários existentes do Active Directory para email. É possível habilitar para email um único usuário ou usar um arquivo CSV para habilitar diversos usuários para email.

## Usar o Shell para habilitar um único usuário para email

Este exemplo habilita para email o usuário Sanjay Shah. Você deve fornecer um endereço de email externo.

```powershell
Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com
```

## Usar o Shell e um arquivo CSV para habilitar vários usuários para email

Ao habilitar usuários para email em lote, primeiro, você exporta a lista de usuários que não estão habilitados para email para um arquivo CSV (valores separados por vírgula) e depois adiciona os endereços de email externos ao arquivo CSV usando um editor de texto como o Bloco de Notas ou um aplicativo de planilha como o Microsoft Excel. Depois, você usa o arquivo CSV atualizado no comando do Shell para habilitar para email os usuários listados no arquivo CSV.

1.  Execute o seguinte comando para exportar uma lista de usuários existentes que não estejam habilitados para email ou que não possuem uma caixa de correio na sua organização para um arquivo na área de trabalho do administrador chamado UsersToMailEnable.csv.
   
    ```powershell
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    ```

    O arquivo resultante será similar ao seguinte arquivo.
    
    ```powershell
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...
    ```

2.  Faça as seguintes alterações no arquivo CSV:
    
      - Exclua todos os usuários do arquivo CSV que não deseja habilitar para email. Por exemplo, você excluiria as três primeiras entradas no exemplo anterior porque elas são as contas padrão do sistema.
    
      - Exclua a coluna **RecipientType** e todas as instâncias de `User`.
    
      - Adicione um cabeçalho de coluna chamado **EmailAddress** e depois adicione um endereço de email para cada usuário no arquivo. O nome e o endereço de email externo para cada usuário devem ser separados por vírgula.
    
    O arquivo CSV atualizado deve ser similar ao seguinte:
    
    ```powershell
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...
    ```

3.  Execute o seguinte comando para usar os dados no arquivo CSV para habilitar para email usuários listados no arquivo.
    
    ```powershell
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    ```

    Os resultados do comando exibem informações sobre os novos usuários habilitados para email.

## Como saber se funcionou?

Para verificar se você habilitou para email com êxito usuários do Active Directory, siga uma destas opções:

  - No EAC, navegue até **Destinatários** \> **Contatos**. Novos usuários de email são exibidos na lista de contatos. Em **Tipo de contato**, o tipo é **Usuário de email**.
    

    > [!NOTE]
    > Pode ser necessário clicar em <STRONG>Atualizar</STRONG><IMG title="Ícone Atualizar" alt="Ícone Atualizar" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif"> para exibir novos usuários de email.



  - No Shell, execute o comando abaixo para exibir informações sobre novos usuários de email.
    
    ```powershell
    Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress
    ```

