---
title: 'Criar caixas de correio do usuário: Exchange 2013 Help'
TOCTitle: Criar caixas de correio do usuário
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52058841
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar caixas de correio do usuário

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2013-04-12_

As caixas de correio são o tipo de destinatário mais comum usado por trabalha com informações em uma organização do Exchange. Cada caixa de correio é associada a uma conta de usuário do Active Directory. O usuário pode usar a caixa de correio para enviar e receber mensagens, bem como para armazenar mensagens, compromissos, tarefas, anotações e documentos. Use o EAC ou o Shell para criar caixas de correio de usuário.

Também é possível criar caixas de correio para usuários existentes que possuem uma conta no Active Directory, mas não possuem uma caixa de correio correspondente. Isso é conhecido como *habilitar para caixa de correio* os usuários existentes.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada tarefa de caixa de correio do usuário: 2 a 5 minutos.

  - Quando criar uma nova caixa de correio do usuário, você não pode usar um apóstrofo (') ou aspas (") no alias ou no nome de logon do usuário porque esses caracteres não são compatíveis. Embora você não possa receber um erro se criar uma nova caixa de correio usando caracteres sem suporte, esses caracteres podem causar problemas mais tarde. Por exemplo, os usuários que foram atribuídos permissões de acesso a uma caixa de correio que foi criada usando um caractere sem suporte podem experimentar problemas ou um comportamento inesperado.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário", no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar uma caixa de correio de usuário

## Usar o EAC para criar uma caixa de correio de usuário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Clique em **Nova** \> **Caixa de correio de usuário**.

3.  Na página **Nova caixa de correio de usuário**, na caixa **Alias**, digite o alias do usuário, que especifica o alias do email do usuário. O alias do usuário é a parte do endereço de email à esquerda do símbolo @. Ele deve ser exclusivo na floresta.
    

    > [!NOTE]
    > Se você deixar essa caixa em branco, o valor da parte do nome de usuário do <STRONG>Nome de logon do usuário</STRONG> é usado para o alias de email.



4.  Selecione uma das seguintes opções:
    
      - **Usuário existente**   Selecione para habilitar para email e criar uma caixa de correio para um usuário existente.
        
        Clique em **Procurar** para abrir a caixa de diálogo **Selecionar Usuário — Floresta Inteira**. Essa caixa de diálogo exibe uma lista de contas de usuário do Active Directory existentes na floresta que não estão habilitadas para email nem possuem caixas de correio do Exchange. Selecione a conta de usuário que você deseja habilitar para email e clique em **OK** para retornar ao assistente. Se você selecionar essa opção, não terá que fornecer informações de conta de usuário, porque essas informações já existirão no Active Directory.
    
      - **Novo usuário**   Selecione para criar uma nova conta de usuário no Active Directory e criar uma caixa de correio para esse usuário. Se você selecionar essa opção, terá que fornecer as informações de conta de usuário necessárias.
    

    > [!NOTE]
    > A conta Active Directory&nbsp;associada a caixas de correio de usuários deve residir na mesma floresta que o servidor Exchange. Para criar uma caixa de correio para uma conta de usuário que esteja em uma floresta confiável, você terá que criar uma caixa de correio vinculada. Consulte <A href="manage-linked-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio vinculadas</A>.



5.  Se você tiver selecionado **Novo usuário**, na Etapa 4, preencha as seguintes caixas na página **Nova caixa de correio de usuário**. Caso contrário, pule para a Etapa 7.
    
      - **Nome**   Use essa caixa para digitar o nome do usuário.
    
      - **Iniciais**   Use esta caixa para digitar as iniciais do usuário.
    
      - **Sobrenome**   Use essa caixa para digitar o sobrenome do usuário.
    
      - **\*Nome para exibição**   Use essa caixa para digitar um nome de exibição para o usuário. Esse é o nome que fica na lista de caixa de correio no EAC e no catálogo de endereços compartilhado. Por padrão, essa caixa é preenchida com os nomes que você insere nas caixas **Nome**, **Iniciais** e **Sobrenome**. Se você não tiver usado essas caixas, ainda deverá digitar um nome nessa caixa, pois isso é obrigatório. O nome não pode exceder 64 caracteres.
    
      - **\*Nome**   Use esta caixa para digitar um nome para o usuário. Esse é o nome que está listado em Active Directory. Essa caixa também é populada com os nomes que você insere nas caixas **Nome**, **Iniciais** e **Sobrenome**. Se você não tiver usado essas caixas, ainda deverá digitar um nome, pois essa caixa é obrigatória. Esse nome também não pode exceder 64 caracteres.
    
      - **Unidade organizacional**   É possível selecionar uma OU (unidade organizacional) que não seja a padrão (que é o escopo do destinatário). Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio do Active Directory que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido como um domínio específico, por padrão, o contêiner Usuários desse domínio será selecionado. Se o escopo do destinatário estiver definido como uma unidade organizacional específica, essa unidade será selecionada por padrão.
        
        Para selecionar uma unidade organizacional diferente, clique em **Procurar**. A caixa de diálogo exibe todas as unidades organizacionais da floresta que estão no escopo especificado. Selecione a OU desejada e clique em **OK**.
    
      - **\* Nome de logon do usuário**   Use esta caixa para digitar o nome que o usuário irá usar para fazer o logon na caixa de correio e fazer o logon no domínio. O nome de logon do usuário consiste no nome do usuário à esquerda do símbolo (@) e um sufixo à direita. Geralmente, o sufixo é o nome de domínio no qual a conta de usuário reside. Observe que você não pode usar um apóstrofo (') ou aspas (') no nome de logon do usuário porque esses caracteres não são compatíveis.
        

        > [!NOTE]
        > Se o valor do nome de usuário for diferente do valor usado na caixa <STRONG>Alias</STRONG> , o endereço de email do usuário e o nome de logon do usuário serão diferentes.

    
      - **\* Nova senha**   Use esta caixa para digitar a senha que o usuário deve usar para fazer logon em sua caixa de correio.
        

        > [!NOTE]
        > Verifique se a senha fornecida é compatível com os requisitos de tamanho, complexidade e histórico do domínio no qual você está criando a conta do usuário.

    
      - **\*Confirmar senha**   Use essa caixa para confirmar a senha que você digitou na caixa **Senha**.
    
      - **O usuário deve alterar a senha no próximo logon**   Marque essa caixa de seleção se quiser que o usuário redefina a senha quando fizer o primeiro logon na caixa de correio.
        
        Se você marcar essa caixa de seleção, no primeiro logon, o novo usuário verá uma caixa de diálogo pedindo para ele alterar a senha. O usuário não terá permissão para executar nenhuma tarefa até que a senha tenha sido alterada com êxito.

6.  Clique em **Mais opções**, para configurar as caixas a seguir. Caso contrário, pule para a etapa 7, para salvar a nova caixa de correio do usuário.
    
      - **Especificar o banco de dados da caixa de correio**   Use essa opção para especificar um banco de dados de caixa de correio, em vez de permitir que o Exchange selecione um banco de dados para você. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar Banco de Dados de Caixa de Correio**. Essa caixa de diálogo lista todos os bancos de dados de caixa de correio de sua organização do Exchange. Por padrão, os bancos de dados de caixa de correio são classificados por nome. Você também pode clicar no título da coluna correspondente para classificar os bancos de dados por nome ou versão do servidor. Selecione o banco de dados de caixa de correio que você deseja usar e clique em **OK**.
    
      - **Criar armazenamento de arquivo morto local para esse usuário**   Marque essa caixa de seleção, para criar uma caixa de correio de arquivo morto para a caixa de correio. Se você criar uma caixa de correio de arquivo morto, os itens da caixa de correio serão movidos automaticamente da caixa de correio principal para o arquivo morto, com base nas configurações da política de retenção padrão ou naquelas que você definiu.
        
        Clique em **Procurar** para selecionar um banco de dados que esteja na floresta local, para armazenar a caixa de correio de arquivo morto.
        
        Para saber mais, consulte [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Política de catálogo de endereços**   Use essa opção para especificar uma ABP (política de catálogo de endereços) para a caixa de correio. As ABPs contêm um GAL (lista de endereços global), um OAB (catálogo de endereços offline), uma lista de salas e um conjunto de listas de endereços. Quando atribuída aos usuários da caixa de correio, uma ABP fornece a eles acesso a uma GAL personalizada no Outlook e no Outlook Web App. Para saber mais, consulte [Políticas de catálogo de endereços](https://docs.microsoft.com/pt-br/exchange/address-books/address-book-policies/address-book-policies).
        
        Na lista suspense, selecione a política que você deseja associar a esta caixa de correio.

7.  Após concluir, clique em **Salvar** para criar a caixa de correio.

## Usar o Shell para criar uma caixa de correio de usuário

Este exemplo cria uma nova conta de usuário e caixa de correio para Pilar Pinilla com os seguintes detalhes:

  - O alias é pilarp

  - O primeiro nome é Pilar e o último nome é Pinilla

  - O nome e o nome de exibição é Pilar Pinilla

  - O nome de logon do usuário é pilarp@contoso.com

  - A senha é Pa$$word1

  - A caixa de correio será criada na unidade organizacional padrão. Para especificar uma unidade organizacional diferente, você pode usar o parâmetro *OrganizationalUnit*.

<!-- end list -->

```powershell
    New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)
```

Para obter informações sobre sintaxes e parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou uma caixa de correio de usuário com êxito, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de correio**. A nova caixa de correio do usuário é exibida na lista de caixas de correio. Em **Tipo de Caixa de Correio**, o tipo é **Usuário**.

  - No Shell, execute o comando a seguir para exibir informações sobre a nova caixa de correio de usuário:
    
    ```powershell
    Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    ```

## Criar uma caixa de correio para um usuário existente

Também é possível criar caixas de correio para usuários existentes que possuem uma conta no Active Directory, mas não possuem uma caixa de correio correspondente. Isso é conhecido como *habilitar para caixa de correio* os usuários existentes. Depois que você habilitar uma caixa de correio para um usuário existente, o usuário poderá enviar e receber mensagens de email.

## Usar o EAC para criar uma caixa de correio para um usuário existente

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Clique em **Nova** \> **Caixa de correio de usuário**.

3.  Na página **Nova caixa de correio de usuário**, na caixa **Alias**, digite o alias do usuário, que especifica o alias do email do usuário. O alias do usuário é a parte do endereço de email à esquerda do símbolo @. Ele deve ser exclusivo na floresta.
    

    > [!NOTE]
    > Se você deixar essa caixa em branco, o valor da parte do nome de usuário do <STRONG>Nome de logon do usuário</STRONG> é usado para o alias de email.



4.  Clique em **Usuário existente**.

5.  Clique em **Procurar** para abrir a caixa de diálogo **Selecionar Usuário — Floresta Inteira**. Essa caixa de diálogo exibe uma lista de contas de usuário do Active Directory existentes na floresta que não estão habilitadas para email nem possuem caixas de correio do Exchange. Selecione a conta de usuário que você deseja habilitar para email e clique em **OK** para retornar ao assistente.
    
    Ao criar uma caixa de correio para um usuário existente, você não terá que fornecer informações de conta de usuário, porque essas informações já existirão no Active Directory.
    

    > [!NOTE]
    > A conta Active Directory&nbsp;associada a caixas de correio de usuários deve residir na mesma floresta que o servidor Exchange. Para criar uma caixa de correio para uma conta de usuário que esteja em uma floresta confiável, você terá que criar uma caixa de correio vinculada. Consulte <A href="manage-linked-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio vinculadas</A>.



6.  Clique em **Mais opções**, para configurar as caixas a seguir. Caso contrário, pule para a etapa 7, para salvar a nova caixa de correio do usuário.
    
      - **Especificar o banco de dados da caixa de correio**   Use essa opção para especificar um banco de dados de caixa de correio, em vez de permitir que o Exchange selecione um banco de dados para você. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar Banco de Dados de Caixa de Correio**. Essa caixa de diálogo lista todos os bancos de dados de caixa de correio de sua organização do Exchange. Por padrão, os bancos de dados de caixa de correio são classificados por nome. Você também pode clicar no título da coluna correspondente para classificar os bancos de dados por nome ou versão do servidor. Selecione o banco de dados de caixa de correio que você deseja usar e clique em **OK**.
    
      - **Criar armazenamento de arquivo morto local para esse usuário**   Marque essa caixa de seleção, para criar uma caixa de correio de arquivo morto para a caixa de correio. Se você criar uma caixa de correio de arquivo morto, os itens da caixa de correio serão movidos automaticamente da caixa de correio principal para o arquivo morto, com base nas configurações da política de retenção padrão ou naquelas que você definiu.
        
        Clique em **Procurar** para selecionar um banco de dados que esteja na floresta local, para armazenar a caixa de correio de arquivo morto.
        
        Para saber mais, consulte [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Política de catálogo de endereços**   Use essa opção para especificar uma ABP (política de catálogo de endereços) para a caixa de correio. As ABPs contêm um GAL (lista de endereços global), um OAB (catálogo de endereços offline), uma lista de salas e um conjunto de listas de endereços. Quando atribuída aos usuários da caixa de correio, uma ABP fornece a eles acesso a uma GAL personalizada no Outlook e no Outlook Web App. Para saber mais, consulte [Políticas de catálogo de endereços](https://docs.microsoft.com/pt-br/exchange/address-books/address-book-policies/address-book-policies).
        
        Na lista suspense, selecione a política que você deseja associar a esta caixa de correio.

7.  Após concluir, clique em **Salvar** para criar a caixa de correio.

## Usar o Shell para criar uma caixa de correio para um usuário existente

Este exemplo cria uma caixa de correio para o usuário existente estherv@contoso.com no banco de dados do Exchange chamado UsersMailboxDatabase.

```powershell
Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase
```

É possível usar o cmdlet **Enable-Mailbox** para habilitar para email múltiplos usuários. Isso pode ser feito pela canalização dos resultados do cmdlet **Get-User** para o cmdlet **Enable-Mailbox**. Ao executar o cmdlet **Get-User**, você deve retornar apenas usuários que não estão habilitados para email. Para isso, você precisa especificar o valor Usuário com o parâmetro *RecipientTypeDetails*. Também é possível limitar os resultados retornados usando o parâmetro *Filter* para solicitar somente usuários que atendem aos critérios que você definiu. Depois, canalize os resultados para o cmdlet **Enable-Mailbox**.

Por exemplo, o comando a seguir habilita a caixa de correio de usuários que não tenham sido habilitados para caixa de correio ainda e que tenham um valor na propriedade **UserPrincipalName**, o que ajuda a assegurar que você não converta inadvertidamente uma conta de sistema em uma caixa de correio.

```powershell
Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox
```

Para informações sobre sintaxe e parâmetros, consulte [Enable-Mailbox](https://technet.microsoft.com/pt-br/library/aa998251\(v=exchg.150\)) e [Get-User](https://technet.microsoft.com/pt-br/library/aa996896\(v=exchg.150\)).

Para mais informações sobre canalização, consulte [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou uma caixa de correio para um usuário existente com êxito, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de correio**. O novo usuário habilitado para caixa de correio é exibido na lista de caixas de correio. Em **Tipo de Caixa de Correio**, o tipo é **Usuário**.

  - No Shell, execute o comando a seguir para exibir informações sobre o novo usuário habilitado para caixa de correio:
    
    ```powershell
    Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    ```
    
    Observe que o valor para a propriedade *RecipientTypeDetails* é `UserMailbox`.

