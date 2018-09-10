---
title: 'Gerenciar grupos de segurança habilitados para email: Exchange 2013 Help'
TOCTitle: Gerenciar grupos de segurança habilitados para email
ms:assetid: 80b3b537-4786-4d02-9202-44e373811a25
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123521(v=EXCHG.150)
ms:contentKeyID: 50484742
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar grupos de segurança habilitados para email

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-10-04_

Um grupo de segurança habilitados para email pode ser usado para distribuir mensagens, bem como para conceder permissões de acesso a recursos em Active Directory. Para obter mais informações, consulte [Destinatários](recipients-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 a 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar um grupo de segurança habilitados para email

## Usar o EAC para criar um grupo de segurança

1.  Na EAC, navegue até **Destinatários** \> **Grupos**.

2.  Clique em **New**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") \> **grupo de segurança**.

3.  Na página **novo grupo de segurança**, preencha os seguintes campos:
    
      - **\* Nome para exibição**   Use essa caixa para digitar o nome para exibição. Esse nome é exibido no catálogo de endereços compartilhado, na linha Para: quando um email é enviado a esse grupo e na lista Grupos do EAC. O nome para exibição é necessário e deve ser amigável para que as pessoas o reconheçam. Ele também deve ser exclusivo na floresta.
        

        > [!TIP]
        > Se for aplicado a um diretiva de nomeação de grupo, você deve seguir as restrições de nomenclatura impostas para sua organização. Para obter mais informações, consulte <A href="https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy">Criar um diretiva de nomeação de grupo de distribuição</A>. Se você deseja substituir a diretiva de nomenclatura de grupo da sua organização, consulte <A href="https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/override-group-naming-policy">Substituir o diretiva de nomenclatura de grupo de distribuição</A>.

    
      - \* **Alias**    Use esta caixa para digitar o alias do grupo de segurança. O alias não pode exceder 64 caracteres e deve ser exclusivo na floresta. Quando um usuário digita o alias para: linha de uma mensagem de email, que é resolvida para o nome para exibição do grupo.
    
      - **Descrição**    Use esta caixa para descrever o grupo de segurança para que pessoas saibam o que é a finalidade do grupo.
    
      - **Unidade organizacional**   É possível selecionar uma OU (unidade organizacional) que não seja a padrão (que é o escopo do destinatário). Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio do Active Directory que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido como um domínio específico, por padrão, o contêiner Usuários desse domínio será selecionado. Se o escopo do destinatário estiver definido como uma unidade organizacional específica, essa unidade será selecionada por padrão.
        
        Para selecionar uma unidade organizacional diferente, clique em **Procurar**. A caixa de diálogo exibe todas as unidades organizacionais da floresta que estão no escopo especificado. Selecione a OU desejada e clique em **OK**.
    
      - \* **Proprietários**    Por padrão, a pessoa que cria um grupo é o proprietário. Todos os grupos devem ter pelo menos um proprietário. Você pode adicionar proprietários clicando em **Adicionar**.
    
      - **Membros**   Use esta seção para adicionar membros e para especificar se é necessário obter aprovação para que as pessoas ingressem ou saiam do grupo.
        
        Os proprietários do grupo não precisam ser membros do grupo. Use a opção **Adicionar proprietários do grupo como membros** para adicionar ou remover os proprietários como membros.
        
        Para adicionar membros ao grupo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Quando você terminar de adicionar membros, clique em **Okey** para retornar à página do **novo grupo de segurança**.
        
        Marque a caixa de seleção **a aprovação do proprietário é necessária** se você quiser que os proprietários do grupo para receber solicitações de usuário para ingressar no grupo. Se você selecionar essa opção, os membros somente podem ser removidos dos proprietários do grupo.

4.  Quando tiver terminado, clique em **Salvar** para criar o grupo de segurança.


> [!TIP]
> Por padrão, todos os novos grupos de segurança habilitados para email exigem que todos os remetentes sejam autenticados. Isso impede que os remetentes externos enviem mensagens para grupos de segurança habilitados para email. Para configurar um grupo de segurança habilitados para email para aceitar mensagens de todos os remetentes, você deve modificar as configurações de restrição de entrega de mensagem para esse grupo.



## Use o Shell para criar um grupo de segurança

Este exemplo cria um grupo de segurança com um fsadmin alias e os gerentes de servidor de arquivo de nome. O grupo de segurança é criado na unidade Organizacional padrão e qualquer pessoa pode participar desse grupo com a aprovação dos proprietários do grupo.

    New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security

Para obter mais informações sobre como usar o Shell para criar grupos de segurança habilitados para email, consulte [New-DistributionGroup](https://technet.microsoft.com/pt-br/library/aa998856\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito um grupo de segurança habilitados para email, siga um destes procedimentos:

  - No EAC, navegue até **destinatários** \> **grupos**. O novo grupo de segurança habilitados para email é exibido na lista de grupos. Em **Tipo de grupo**, o tipo é o **grupo de segurança**.

  - No Shell, execute o seguinte comando para exibir informações sobre o novo grupo de segurança habilitados para email.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Alterar propriedades do grupo de segurança habilitados para email

## Usar o EAC para alterar propriedades do grupo de segurança habilitados para email

1.  No EAC, navegue até **Destinatários** \> **Grupos**.

2.  Na lista de grupos, clique no grupo de segurança que você deseja exibir ou alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do grupo, clique em uma destas seções, para exibir ou alterar propriedades.
    
      - Geral
    
      - Propriedade
    
      - Associação
    
      - Membership approval
    
      - Delivery management
    
      - Message approval
    
      - Email options
    
      - MailTip
    
      - Group delegation

## Geral

Use essa seção para visualizar ou alterar informações básicas sobre o grupo.

  - **\* Nome para exibição**   Este nome será exibido no catálogo de endereços, na linha Para: quando um email é enviado a esse grupo e na lista Grupos. O nome para exibição é necessário e deve ser amigável para que as pessoas o reconheçam. Ele também deve ser exclusivo em seu domínio.

  - **\* Alias**   É a parte do endereço de email que aparece à esquerda do símbolo de arroba (@). Se você alterar o alias, o endereço SMTP principal do grupo também será alterado e conterá o novo alias. Além disso, o endereço de email com o alias anterior será mantido como um endereço proxy para o grupo.

  - **Descrição**   Use essa caixa para descrever o grupo, para que as pessoas saibam qual é o objetivo do grupo. Essa descrição é exibida no catálogo de endereços e no painel Detalhes do EAC.

  - **Ocultar este grupo das listas de endereços**    Marque esta caixa de seleção se não quiser que os usuários vejam a este grupo no catálogo de endereços. Se essa caixa de seleção estiver marcada, um remetente tem que digitar o endereço de email ou o alias do grupo para: ou Cc: linhas para enviar emails ao grupo.
    

    > [!TIP]
    > Considere ocultar grupos de segurança porque eles são tipicamente usados para atribuir permissões a membros do grupo e não para enviar emails.



  - **Unidade organizacional**    Esta caixa somente leitura exibe a unidade organizacional (UO) que contém o grupo de segurança. Você precisa usar computadores e usuários do Active Directory para mover grupo para uma UO diferente.

## Propriedade

Use esta seção para atribuir o grupo proprietários. O proprietário do grupo pode adicionar membros ao grupo e aprovar ou rejeitar solicitações para ingressar no grupo. Por padrão, a pessoa que cria um grupo é o proprietário. Todos os grupos devem ter pelo menos um proprietário.

Você pode adicionar proprietários, clicando em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). É possível remover um proprietário, selecionando-o e clicando em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

## Associação

Use esta seção para adicionar ou remover membros. Os proprietários do grupo não precisam ser membros do grupo. Em **Membros**, você pode adicionar membros, clicando em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Você pode remover um membro, selecionando um usuário na lista de membros e clicando em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

## Aprovação de associação

Use esta seção para especificar se a aprovação do proprietário é necessária para os usuários ingressar no grupo. Se você selecionar a caixa de seleção **é necessária a aprovação do proprietário**, o proprietário do grupo ou proprietários recebem um email solicitando aprovação para ingressar no grupo. Conforme mencionado anteriormente, somente os proprietários podem remover membros do grupo.


> [!TIP]
> Essa opção não funcionará com grupos de segurança habilitados para email devido a limitações relacionadas à segurança.



## Gerenciamento de entregas

Use essa seção para gerenciar quem pode enviar emails a esse grupo.

  - **Apenas os remetentes da minha organização**   Selecione esta opção para permitir que apenas os remetentes da sua organização enviem mensagens ao grupo. Isso significa que, se alguém fora da sua organização enviar uma mensagem de email a esse grupo, ela será rejeitada. Essa é a configuração padrão.

  - **Remetentes de dentro e de fora da minha organização**   Selecione esta opção para permitir que qualquer pessoa envie mensagens ao grupo.
    
    É possível limitar ainda mais as pessoas que podem enviar mensagens ao grupo permitindo que apenas remetentes específicos enviem mensagens a esse grupo. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione um ou mais destinatários. Se você adicionar remetentes a essa lista, eles serão os únicos que poderão enviar email ao grupo. Os emails enviados por qualquer pessoa que não estiver na lista serão rejeitados.
    
    Para remover uma pessoa ou grupo da lista, selecione-o na lista e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").
    

    > [!IMPORTANT]
    > Se você configurou o grupo para permitir que somente os remetentes dentro da organização enviar mensagens ao grupo, emails enviados a partir de um contato de email serão rejeitada, mesmo se eles estiver adicionados a essa lista.



## Aprovação de mensagem

Use esta seção para configurar opções para moderar o grupo. Os moderadores aprovam ou rejeitam as mensagens enviadas ao grupo antes que elas cheguem aos membros do grupo.

  - **As mensagens enviadas a esse grupo precisam ser aprovados pelo moderador**    Essa caixa de seleção não é selecionada por padrão. Se você selecionar essa caixa de seleção, as mensagens recebidas serão revisadas pelos Moderadores do grupo antes da entrega. Os moderadores do grupo podem aprovar ou rejeitar mensagens de entrada.

  - **Moderadores do grupo**    Para adicionar os moderadores do grupo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover um moderador, selecione moderador e, em seguida, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"). Se você tiver selecionado "Têm as mensagens enviadas a esse grupo a ser aprovado por um moderador" e você não marcar um moderador, mensagens ao grupo serão enviadas para os proprietários do grupo de aprovação.

  - **Remetentes que não exigem aprovação de mensagens**    Para adicionar pessoas ou grupos que poderá ignorar a moderação para esse grupo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover uma pessoa ou um grupo, selecione o item e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

  - **Selecionar notificações de moderação   **Use esta seção para definir como os usuários serão notificados sobre a aprovação de mensagens.
    
      - **Notificar todos os remetentes quando suas mensagens não são aprovadas**    Esta é a configuração padrão. Remetentes de dentro e fora da sua organização serão notificados quando suas mensagens não são aprovadas.
    
      - • **Notificar remetentes da organização apenas quando as mensagens não forem aprovadas**   Se esta opção for selecionada, somente pessoas ou grupos da sua organização serão notificados quando uma mensagem enviada por eles ao grupo não for aprovada por um moderador.
    
      - **Não notificar ninguém quando uma mensagem não for aprovada**   Quando você seleciona esta opção, nenhuma notificação é enviada para os remetentes cujas mensagens não são aprovadas pelos moderadores do grupo.

## Opções de email

Use essa seção para visualizar ou alterar os endereços de email associados ao grupo. Isso inclui endereços SMTP principais do grupo e todos os endereços de proxy associados. O endereço SMTP principal (também conhecido como *endereço de resposta*) será exibido em negrito, na lista de endereços, com o valor em maiúsculas **SMTP** na coluna **Tipo**.

  - **Adicionar**  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço de email para essa caixa de correio. Selecione um dos seguintes tipos de endereço:
    
      - **SMTP**   Esse é o tipo de endereço padrão. Clique nesse botão e digite o novo endereço SMTP na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Para tornar o novo endereço o endereço SMTP principal para o grupo, marque a caixa de seleção <STRONG>tornar este o endereço de resposta</STRONG>. Essa caixa de seleção é exibida somente quando a caixa de seleção <STRONG>Atualizar automaticamente os endereços de email com base na diretiva de endereço de email aplicada para o destinatário</STRONG> não está selecionada.

    
      - **Tipo de endereço personalizado**   Clique nesse botão e digite um dos tipos de endereço de email não SMTP compatíveis na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Com a exceção de endereços X.400, o Exchange não valida endereços personalizados para a formatação adequada. Certifique-se de que o endereço personalizado que você especificar esteja de acordo com os requisitos de formato para esse tipo de endereço.



  - **Editar**   Para alterar um endereço de email associado ao grupo, selecione-o na lista e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    

    > [!TIP]
    > Para tornar um endereço existente o endereço SMTP principal para o grupo, marque a caixa de seleção <STRONG>tornar este o endereço de resposta</STRONG>. Como mencionado anteriormente, essa caixa de seleção é exibida somente quando a caixa de seleção <STRONG>Atualizar automaticamente os endereços de email com base na diretiva de endereço de email aplicada para o destinatário</STRONG> não está selecionada.



  - **Remover**   Para excluir um endereço de email associado ao grupo, selecione-o na lista e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

  - **Atualizar automaticamente os endereços de email com base na diretiva de endereço de email aplicada para o destinatário** Marque essa caixa de seleção para que os endereços de email do destinatário atualizados automaticamente com base em alterações feitas por políticas de endereço em sua organização de email. Por padrão, essa caixa está marcada.

## MailTip

Use esta seção para adicionar uma Dica de Email a fim de alertar os usuários sobre possíveis problemas antes de eles enviarem uma mensagem a esse grupo. Uma Dica de Email é o texto exibido na barra de informações quando esse grupo é adicionado às linhas Para, Cc ou Cco de uma nova mensagem de email. Por exemplo, você poderia acrescentar uma dica de email a grupos grandes para advertir remetentes potenciais de que a sua mensagem será enviada a muitas pessoas.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. As marcas HTML não são contadas no limite.



## Delegação de grupo

Use essa seção para atribuir permissões a um usuário (chamado de *delegar*) para permitir que eles enviem mensagens como o grupo ou enviar mensagens em nome do grupo. É possível atribuir as seguintes permissões:

  - **Enviar como**   Essa permissão permite que o representante envie mensagens como o grupo. Depois que essa permissão for atribuída, o representante tem a opção de adicionar o grupo na linha **De** para indicar que a mensagem foi enviada pelo grupo.

  - **Enviar em Nome de**   Essa permissão também permite que um representante envie mensagens em nome do grupo. Depois que essa permissão for atribuída, o representante tem a opção de adicionar o grupo na linha **De**. Parecerá que a mensagem foi enviada pelo grupo e será indicado que ela foi enviada pelo representante em nome do grupo.

Para atribuir permissões para representantes, clique em **Adicionar** na permissão apropriada para exibir a página **Selecionar o destinatário**, que exibe uma lista de todos os destinatários na sua organização do Exchange que pode ser atribuída a permissão. Selecione os destinatários que você deseja, adicioná-los à lista e, em seguida, clique em **Okey**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa Pesquisar e clicando em **pesquisa**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").

## Use o Shell para alterar propriedades do grupo de segurança

Use os cmdlets **Get-DistributionGroup** e **Set-DistributionGroup** para exibir e alterar propriedades dos grupos de segurança. Vantagens de usar o Shell são a capacidade de alterar as propriedades que não estão disponíveis no EAC e alterar as propriedades de vários grupos de segurança. Para obter informações sobre quais parâmetros correspondem às quais propriedades do grupo de distribuição, consulte os seguintes tópicos:

  - [Get-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124955\(v=exchg.150\))

Aqui estão alguns exemplos de como usar o Shell para alterar propriedades do grupo de segurança.

Este exemplo exibe uma lista de todos os grupos de segurança na organização.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')}

Este exemplo altera o endereço SMTP principal (também chamado de endereço de resposta) para o grupo de segurança Administradores de Seattle de admins@contoso.com para seattle.admins@contoso.com. O endereço de resposta anterior será mantido como um endereço de proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com

Este exemplo oculta todos os grupos de segurança na organização do catálogo de endereços.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} | Set-DistributionGroup -HiddenFromAddressListsEnabled $true

## Como saber se funcionou?

Para verificar se você alterou com êxito as propriedades de um grupo de segurança, faça o seguinte:

  - No EAC, selecione o grupo e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade ou recurso que você alterou. Dependendo da propriedade que você tiver alterado, ela poderá ser exibida no painel Detalhes do grupo selecionado.

  - No Shell, use o cmdlet **Get-DistributionGroup** para verificar as alterações. Uma vantagem de usar o Shell é que você pode visualizar várias propriedades de vários grupos. No exemplo acima onde todos os grupos de segurança estavam ocultas do catálogo de endereços, execute o seguinte comando para verificar o novo valor.
    
        Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} |
         fl Name,HiddenFromAddressListsEnabled


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="O ícone pequeno do LinkedIn Learning" alt="O ícone pequeno do LinkedIn Learning" /> <strong>Começando a usar o Office 365?</strong><br />
Descubra cursos em vídeo gratuitos para <a href="https://support.office.com/pt-br/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, oferecidos pelo LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

