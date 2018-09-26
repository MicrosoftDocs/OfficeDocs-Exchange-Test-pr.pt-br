---
title: 'Habilitar ou desabilitar o email para um contato de email: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar o email para um contato de email
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50556287
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o email para um contato de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-12-05_

Você pode desabilitar o email para um contato de email existente na sua organização do Exchange. Quando você desabilita o email para um contato de email, ele é removido do Exchange e do catálogo de endereços da sua organização. Se o contato de email for um membro de um grupo de distribuição, o contato não recebe emails enviados para o grupo. Além disso, os atributos do Exchange foram removidos do objeto de contato habilitado para email no Active Directory, mas o contato e seus atributos não são do Exchange (por exemplo, informações de contato e organização) são mantidos no Active Directory.

Depois que você desabilitar o email para um contato de email, você pode habilitar email do contato novamente usando o cmdlet **Enable-MailContact** no Shell. Você também pode usar este cmdlet para ativar o email de qualquer contato do Active Directory.

Para tarefas de gerenciamento adicionais relacionadas a contatos de email, consulte [Gerenciar contatos de email](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-mail-contacts).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Contatos de email" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Desabilitar email para um contato de email

Conforme anteriormente mencionado, quando você desabilitar o email para um contato de email, os atributos do Exchange foram removidos do objeto de contato do Active Directory correspondente, mas o contato é mantido. O contato de email é removido da lista de contatos de email no EAC, mas você pode exibir e gerenciar o objeto de contato do Active Directory correspondente usando a computadores e usuários do Active Directory ou usando os cmdlets **Get-Contact** e **Set-Contact** no Shell.

## Usar o EAC para desabilitar o email para um contato de email

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Na lista de contatos, clique no contato de email para o qual você deseja desabilitar o email.

3.  Clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e, em seguida, clique em **Desabilitar**.

4.  Um aviso será exibido perguntando se você tiver certeza de que deseja desabilitar o contato de email selecionado. Clique em **Sim** para desativá-la.

O contato de email será removido da lista Contatos.

## Use o Shell para desabilitar o email para um contato de email

Este exemplo desabilita o email para o contato de email Neil Black.

```powershell
    Disable-MailContact -Identity "Neil Black"
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Disable-MailContact](https://technet.microsoft.com/pt-br/library/aa997465\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você desabilitou com êxito email para um contato de email, siga um destes procedimentos:

1.  No EAC, navegue até **destinatários** \> **Contatos** e verificar que o contato de email não está mais listado.

2.  Em e computadores do Active Directory Users, clique com botão direito no contato e clique em **Propriedades**. Na guia **Geral**, observe que a caixa de **email** está em branco. Isso verifica se o contato não está habilitado para email.

3.  No Shell, execute o comando a seguir.
    
    ```powershell
    Get-MailContact
    ```
    
    O que você desabilitou o email para contato não será retornado nos resultados da porque este cmdlet retorna apenas os contatos habilitados para email.

4.  No Shell, execute o comando a seguir.
    
    ```powershell
    Get-Contact
    ```
    
    O que você desabilitou o email para contato é retornado nos resultados da porque este cmdlet retorna todos os objetos de contato do Active Directory.

## Usar o Shell para ativar o email de contatos

Você pode usar o cmdlet **Enable-MailContact** para ativar o email de contatos existentes do Active Directory. Você pode ativar o email de um único contato ou use um arquivo CSV para habilitar email vários contatos.

## Use o Shell para ativar o email de um único contato

Este exemplo habilita para email do contato Rene Valdes. Você deve fornecer um endereço de email externo.

```powershell
Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com
```

## Use o Shell e um arquivo CSV para habilitar email vários contatos

Quando você está mail-habilitando contatos em massa, você primeiro exporta a lista de contatos que não estão habilitados para email para um arquivo CSV (valores separados por vírgula) e, em seguida, adicione os endereços de email externo ao arquivo CSV, usando um editor de texto como o bloco de notas ou um aplicativo de planilha, como o Microsoft Excel. Em seguida, você usa o arquivo CSV atualizado no comando Shell para habilitar email de contatos listados no arquivo CSV.

1.  Execute o seguinte comando para exportar uma lista de contatos existentes que não estão habilitados para email para um arquivo na área de trabalho do administrador chamado Contacts.csv.
    
    ```powershell
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    ```

    O arquivo resultante será similar ao seguinte arquivo.
    
    ```powershell
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...
    ```

2.  Adicione um título de coluna chamado **EmailAddress** e, em seguida, adicione um endereço de email para cada contato no arquivo. O nome e o endereço de email externo para cada contato devem ser separados por uma vírgula. O arquivo CSV atualizado deve ser semelhante ao arquivo a seguir.
    
    ```powershell
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...
    ```

3.  Execute o seguinte comando para usar os dados no arquivo CSV para habilitar os contatos listados no arquivo de email.
    
    ```powershell
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    ```

    Os resultados do comando exibem informações sobre os novos contatos habilitados para email.

## Como saber se funcionou?

Para verificar se você tiver contatos habilitados para email com êxito do Active Directory, siga um destes procedimentos:

  - No EAC, navegue até **destinatários** \> **Contatos**. Novos contatos de email são exibidos na lista de contatos. Em **Tipo de contato**, o tipo é o **contato de email**.
    

    > [!NOTE]
    > Talvez você precise clique em <STRONG>Atualizar</STRONG><IMG title="Ícone Atualizar" alt="Ícone Atualizar" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif"> para exibir contatos de email novo.



  - No Shell, execute o seguinte comando para exibir informações sobre novos contatos de email.
    
    ```powershell
    Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress
    ```

