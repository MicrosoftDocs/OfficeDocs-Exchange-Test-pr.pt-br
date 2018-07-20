---
title: 'Adicionar ou remover endereços de email para uma caixa de correio: Exchange Online Help'
TOCTitle: Adicionar ou remover endereços de email para uma caixa de correio
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50556244
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Adicionar ou remover endereços de email para uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

É possível configurar mais de um endereço de email para a mesma caixa de correio. Os endereços adicionais são chamados de *endereços proxy*. Um endereço proxy permite que um usuário receba email enviado a um endereço de email diferente. Qualquer mensagem de email enviada ao endereço proxy do usuário é fornecida ao seu endereço de email principal, que é também conhecido como *endereço SMTP principal* ou *endereço de resposta padrão*.


> [!IMPORTANT]
> Se você estiver usando o Office 365 para empresas, adicione ou remova endereços de email em caixas de correio do usuário no <A href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Centro de administração do Office 365: Adicione outros aliases de email para um usuário no Office 365</A>



Para tarefas de gerenciamento adicionais relacionadas ao gerenciamento de destinatários, confira a tabela "Documentação de destinatários" em [Destinatários](recipients-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Os procedimentos neste tópico mostram como adicionar ou remover endereços de email para uma caixa de correio de usuário. Você pode usar procedimentos similares para adicionar ou remover endereços de email de outros tipos de destinatário.

## O que você deseja fazer?

## Adicionar um endereço de email a uma caixa de correio do usuário

## Usar o EAC para adicionar uma política de endereço de email

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio à qual quer adicionar um endereço de email e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Endereço de Email**.
    

    > [!TIP]
    > Na página <STRONG>Endereço de Email</STRONG>, o endereço SMTP principal será exibido em negrito, na lista de endereços, com o valor em maiúsculas <STRONG>SMTP</STRONG> na coluna <STRONG>Tipo</STRONG>.



4.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), depois clique em **SMTP** para adicionar um endereço de email SMTP a essa caixa de correio.
    

    > [!TIP]
    > SMTP é o tipo de endereço de email padrão. Você pode também adicionar endereços de Unificação de Mensagens do Exchange (EUM) ou endereços personalizados a uma caixa de correio. Para saber mais, confira "Alterar propriedades de caixa de correio" no tópico <A href="manage-user-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio do usuário</A>.



5.  Digite o novo endereço SMTP na caixa **Endereço de email** e clique em **OK**.
    
    O novo endereço é exibido na lista de endereços de email da caixa de correio selecionada.

6.  Clique em **Salvar** para salvar a alteração.

## Usar o Shell para adicionar uma política de endereço de email

Os endereços de email associados a uma caixa de correio estão contidos na propriedade *EmailAddresses* da caixa de correio. Como ela pode conter mais de um endereço de email, a propriedade *EmailAddresses* é conhecida como uma propriedade *de múltiplos valores*. Os exemplos a seguir mostram diferentes maneiras de modificar uma propriedade de múltiplos valores.

Este exemplo mostra como adicionar um endereço SMTP para a caixa de correio de Dan Jump.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

Este exemplo mostra como adicionar vários endereços SMTP a uma caixa de correio.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

Para mais informações sobre como usar esse método de adicionar e remover valores de propriedades de múltiplos valores, confira [Modificando as propriedades com valores múltiplos](modifying-multivalued-properties-exchange-2013-help.md).

Este exemplo mostra outra forma de adicionar endereços de email a uma caixa de correio especificando todos os endereços associados à caixa de correio. Neste exemplo, danj@tailspintoys.com é o novo endereço de email que você deseja adicionar. Os outros dois endereços de email são endereços existentes. O endereço com o `SMTP` qualificador com diferenciação entre maiúsculas e minúsculas é o endereço SMTP principal. Você precisa incluir todos os endereços de email da caixa de correio ao usar essa sintaxe de comando. Caso contrário, os endereços especificados no comando substituirão os endereços existentes.

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você adicionou com êxito um endereço de email a uma caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio**, clique na caixa de correio e em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

  - Na página de propriedades de caixa de correio, clique em **Endereço de Email**.

  - Na lista de endereços de email da caixa de correio, verifique se o novo endereço de email está incluído.

Ou

  - Execute o seguinte comando no Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verifique se o novo endereço de email está incluído nos resultados.

## Remover um endereço de email de uma caixa de correio do usuário

## Usar o EAC para remover uma política de endereço de email

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio da qual você deseja remover um endereço de email e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Endereço de Email**.

4.  Na lista de endereços de email, selecione o endereço que você deseja remover e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

5.  Clique em **Salvar** para salvar a alteração.

## Usar o Shell para remover uma política de endereço de email

Este exemplo mostra como remover um endereço de email da caixa de correio de Janet Schorr.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

Este exemplo mostra como remover vários endereços de uma caixa de correio.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

Para mais informações sobre como usar esse método de adicionar e remover valores de propriedades de múltiplos valores, confira [Modificando as propriedades com valores múltiplos](modifying-multivalued-properties-exchange-2013-help.md).

Você pode também remover um endereço de email omitindo-o do comando para definir endereços de email de uma caixa de correio. Por exemplo, digamos que a caixa de correio de Janet Schorr tem três endereços de email: janets@contoso.com (o endereço SMTP principal), janets@corp.contoso.com e janets@tailspintoys.com. Para remover o endereço janets@corp.contoso.com, você executaria o comando a seguir.

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

Como janets@corp.contoso.com foi omitido no comando anterior, ele é removido da caixa de correio.

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você removeu com êxito um endereço de email de uma caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio**, clique na caixa de correio e em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

  - Na página de propriedades de caixa de correio, clique em **Endereço de Email**.

  - Na lista de endereços de email da caixa de correio, verifique se o endereço de email não está incluído.

Ou

  - Execute o seguinte comando no Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verificar se o endereço de email não está incluído nos resultados.

## Usar o Shell para adicionar endereços de email a várias caixas de correio

Você pode adicionar um novo endereço de email a várias caixas de correio de uma vez usando o Shell e um arquivo CSV.

Este exemplo importa dados de C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv, que tem o seguinte formato.

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

Execute o comando a seguir para usar os dados no arquivo CSV para adicionar o endereço de email a cada caixa de correio especificada no arquivo CSV.

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}


> [!TIP]
> Os nomes das colunas na primeira linha deste arquivo CSV (<CODE>Mailbox,NewEmailAddress</CODE>) são arbitrários. Sejam quais forem os nomes de colunas usados, os mesmos nomes deverão ser usados no comando do Shell.



## Como saber se funcionou?

Para confirmar se você adicionou com êxito um endereço de email a várias caixas de correio, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio**, clique na caixa de correio à qual você adicionou o endereço, depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

  - Na página de propriedades de caixa de correio, clique em **Endereço de Email**.

  - Na lista de endereços de email da caixa de correio, verifique se o novo endereço de email está incluído.

Ou

  - Execute o seguinte comando no Shell, usando o mesmo arquivo CSV que usava para adicionar o novo endereço de email.
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - Verifique se o novo endereço de email está incluído nos resultados de cada caixa de correio.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..


