---
title: 'Gerenciar permissões para destinatários: Exchange 2013 Help'
TOCTitle: Gerenciar permissões para destinatários
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51407809
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gerenciar permissões para destinatários

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2018-04-20_

Você pode usar o EAC ou o Shell para atribuir permissões aos usuários ou grupos (chamados *representantes*) que permitem que eles abram ou enviem mensagens a partir de outras caixas de correio. As permissões podem ser atribuídas às caixas de correio do usuário, caixas de correio vinculadas, caixas de correio de recurso e caixas de correio compartilhadas. Você também pode atribuir permissões a grupos de distribuição, grupos de distribuição dinâmica e grupos de segurança habilitados para email para permitir que os representantes enviem mensagens em nome do grupo. Você pode atribuir aos representantes as seguintes permissões para acessar caixas de correio ou enviar mensagens em nome das caixas de correio ou grupos:

  -    Esta permissão permite que um representante abra uma caixa de correio do usuário e acesse o conteúdo da caixa de correio. Entretanto, atribuir permissão de Acesso Completo não permite que o representante envie email a partir de caixa de correio. Você precisa atribuir ao representante a permissão de Enviar Como ou Enviar Em Nome De para enviar email.
    
    A permissão de Acesso Completo não está disponível ao configurar permissões para grupos.

  - **Enviar Como**   Esta permissão permite aos representantes usar a caixa de correio para enviar mensagens. Após essa permissão ter sido atribuída a um representante, qualquer mensagem que o representante envie a partir da caixa de correio parecerá que foi enviada pelo proprietário da caixa de correio. Entretanto, esta permissão não permite que um representante entre na caixa de correio do usuário. Ela permite apenas que os usuários abram a caixa de correio. Se esta permissão for atribuída para o grupo, uma mensagen enviada pelo representante parecerá ter sido enviada pelo grupo.

  - **Enviar Em Nome De**   Esta permissão também permite que um representante use a caixa de correio para enviar mensagens. Após esta permissão ter sido atribuída para um representante, o endereço **De** em qualquer mensagem enviada pelo representante indica que a mensagem foi enviada pelo representante em nome do proprietário da caixa de correio.


> [!TIP]
> Se você atribuir permissão de Acesso Completo, Enviar como ou Enviar em nome de para acessar uma caixa de correio que está oculta das listas de endereços, o representante não será capaz de abrir a caixa de correio ou enviar mensagens.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Atribuir permissões para uma caixa de correio

Conforme citado anteriormente, você pode atribuir permissões aos representantes para caixas de correio do usuário, caixas de correio de recurso e caixas de correio compartilhadas. Você pode usar também o Shell para atribuir permissões aos representantes para acessar uma caixa de correio de descoberta.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada de "Permissões e delegação" na seção "Permissões de Provisionamento do Destinatário" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

## Use o EAC para atribuir permissões

O procedimento a seguir mostra como atribuir permissões para uma caixa de correio do usuário. Você segue um procedimento semelhante para atribuir permissões para caixas de correio compartilhadas ou de recurso indo na página **Recursos** ou **Compartilhada** e selecionando a caixa de correio para a qual as permissões serão atribuídas.

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio, clique na caixa de correio para a qual você deseja atribuir permissões e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em **Delegação da Caixa de Correio**.

4.  Para atribuir permissões aos representantes, clique em **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") na permissão apropriada para exibir uma página que lista todos os destinatários na sua organização do Exchange que pode ser atribuída com a permissão. Escolha os destinatários desejados, adicione-os à lista e depois clique em **OK**. Você também pode procurar um destinatário específico digitando o nome do destinatário na caixa de pesquisa e depois clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
    
    Para remover uma permissão para um destinatário, na permissão apropriada, selecione o destinatário e depois clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

5.  Clique em **Salvar** para salvar as suas alterações.

## Use o EAC para atribuir permissões em massa

Use as seguintes etapas para atribuir permissões em massa.

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Marque as caixas de correio às quais você deseja atribuir permissões.

3.  Clique ou toque em **Mais opções** no painel direito e, em **Delegação da Caixa de Correio** escolha, **Adicionar**.

4.  Na página **Adicionar delegação em massa**, clique ou toque em **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") na permissão apropriada para exibir uma página que lista todos os destinatários da sua organização do Exchange aos quais se pode atribuir a permissão. Selecione os destinatários desejados, adicione-os à lista e, em seguida, clique em **OK**.
    
    Para remover uma permissão para destinatários, na permissão apropriada, selecione os destinatários e depois clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

## Use o EAC para atribuir uma permissão para o usuário enviar email a partir da caixa de correio de outro usuário

O procedimento a seguir mostra como atribuir uma permissão para o usuário enviar email da caixa de correio de outro usuário.

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio, clique na caixa de correio para a qual você deseja atribuir permissões de enviar como e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em **Delegação da Caixa de Correio**.

4.  Para atribuir permissões a representantes, clique em **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em **Enviar como** ou em **Enviar em Nome de** para exibir uma página listando todos os destinatários da sua organização Exchange, os quais podem receber a permissão. Selecione os destinatários que você deseja, adicione-os à lista e depois clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa de pesquisa e depois clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
    
    A permissão **Enviar Como** permite ao delegado enviar email a partir desta caixa de correio.
    
    A permissão **Enviar em Nome de** permite ao delegado enviar email em nome desta caixa de correio. A linha **De** em qualquer mensagem enviada por um delegado indica que a mensagem foi enviada pelo delegado em nome do proprietário da caixa de correio.
    

    > [!TIP]
    > Se o usuário precisar ter que abrir e exibir o conteúdo daquela caixa de correio, você deve atribuir ao usuário a permissão .



5.  Clique em **Salvar** para salvar as suas alterações.

## Use o EAC para atribuir a um usuário permissão para enviar email para um grupo.

O procedimento a seguir mostra como atribuir permissão a um usuário para enviar email a partir de um grupo.

1.  No EAC, navegue até **Destinatários** \> **Grupos**.

2.  Na lista de grupos, clique no grupo para o qual você deseja atribuir permissões de enviar como e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do grupo, clique em **Delegação de Grupo**.

4.  Para atribuir permissões a representantes, clique em **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em **Enviar como** ou em **Enviar em Nome de** para exibir uma página listando todos os destinatários da sua organização Exchange, os quais podem receber a permissão. Selecione os destinatários que você deseja, adicione-os à lista e depois clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa de pesquisa e depois clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
    
    A permissão **Enviar Como** permite ao delegado enviar email a partir deste grupo.
    
    A permissão **Enviar em Nome de** permite ao delegado enviar email em nome deste grupo. A linha **De** em qualquer mensagem enviada por um delegado indica que a mensagem foi enviada pelo delegado em nome do grupo.

5.  Clique em **Salvar** para salvar as suas alterações.

## Use o EAC para atribuir permissões de acesso completo

O procedimento a seguir mostra como atribuir permissões de acesso completo para uma caixa de correio do usuário.

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio, clique na caixa de correio para a qual você deseja atribuir permissão de acesso completo e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em **Delegação da Caixa de Correio**.

4.  Para atribuir permissões aos delegados, clique em **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em para exibir uma página que lista todos os destinatários na sua organização do Exchange que podem ter a permissão. Selecione os destinatários que você deseja, adicione-os à lista e depois clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa de pesquisa e depois clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
    
    A permissão de permite que um delgado abra a caixa de correio de um usuário e acesse o conteúdo da mesma.
    

    > [!TIP]
    > Atribuir a permissão de não permite que o delegado envie email a partir da caixa de correio. Você deve atribuir ao delegado a permissão de <STRONG>Enviar Como</STRONG> ou de <STRONG>Enivar em Nome de</STRONG> para o envio de email.



5.  Clique em **Salvar** para salvar as suas alterações.

## Use o Shell para atribuir permissões

As seções a seguir mostram como usar o Shell para gerenciar as permissões de Acesso Completo, Enviar Como e Enviar Em Nome De para as caixas de correio.

## Gerenciar a permissão de Acesso Completo

Os seguintes exemplos mostram como usar os cmdlets **Add-MailboxPermission** e **Remove-MailboxPermission** par gerenciar as permissões de Acesso Completo.

Este exemplo atribui ao representante Raymond Sam a permissão de Acesso Completo para a caixa de correio de Terry Adams.

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

Este exemplo atribui à Esther Valle a permissão de Acesso Completo à caixa de correio de pesquisa de descoberta padrão da organização.

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

Este exemplo atribui aos membros do grupo de distribuição de Assistência Técnica a permissão de Acesso Completo para a caixa de correio compartilhada dos Tíquetes de Assistência Técnica.

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

Este exemplo remove a permissão de Acesso Completo de Jim Hance para a caixa de correio de Ayla Kol.

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

Para obter informações detalhadas sobre sintaxes e parâmetros, confira os seguintes tópicos:

  - [Add-MailboxPermission](https://technet.microsoft.com/pt-br/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/pt-br/library/bb125153\(v=exchg.150\))

## Gerenciar a permissão Enviar Como

Os exemplos a seguir monstram como gerenciar as permissões Enviar Como no Exchange Server 2013 e no Exchange Online. No Exchange 2013, você deve usar os cmdlets **Add-ADPermission** e **Remove-ADPermission** ; no Exchange Online, você deve usar os cmdlets **Add-RecipientPermissionRemove-RecipientPermission** . Em ambos os casos, você usa o parâmetro *Identity* para especificar o nome da caixa de correio na qual a permissão Enviar Como deve ser adicionada ou removida e o parâmetro *User* ou *Trustee* para especificar o representante (por exemplo, um usuário ou grupo) que terá a permissão de Enviar Como atribuída ou não.


> [!TIP]
> Use o cmdlet <STRONG>Get-Recipient</STRONG> para obter a propriedade <EM>Name</EM> para a caixa de correio e do representante. Use estes valores para atribuir a permissão Enviar Como.



## Exchange Server 2013

Este exemplo atribui a permissão de Enviar Como ao grupo de Assistência Técnica na caixa de correio compartilhada Equipe de Suporte de Assistência Técnica.

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

Este exemplo remove a permissão de Enviar Como para o usuário Pilar Pinilla na caixa de correio de James Alvord.

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

Para obter informações detalhadas sobre sintaxes e parâmetros, confira:

  - [Add-ADPermission](https://technet.microsoft.com/pt-br/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/pt-br/library/aa996048\(v=exchg.150\))

## Exchange Online

Este exemplo atribui a permissão de Enviar Como ao grupo de Suporte da Impressora na caixa de correio compartilhada de nome Suporte da Impressora Contoso.

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

Este exemplo remove a permissão de Enviar Como para o usuário Karen Toh na caixa de correio para Yan Li.

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

Para obter informações detalhadas sobre sintaxes e parâmetros, confira:

  - [Add-RecipientPermission](https://technet.microsoft.com/pt-br/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/pt-br/library/ff945794\(v=exchg.150\))

## Gerenciar a permissão de Enviar Em Nome De

O exemplo a seguir usa o cmdlet **Set-Mailbox** para gerenciar as permissões de Enviar Em Nome De.

Este exemplo atribui ao representante Holly Holt a permissão de Enviar Em Nome De para a caixa de correio de Sean Chai.

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

Este exemplo remove a permissão de Enviar Em Nome De na caixa de correio compartilhada Contoso Executives que foi atribuída ao grupo de Assistentes Executivos Temporários.

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você atribuiu as permissões com sucesso para uma caixa de correio ou uma caixa de correio compartilhada, realize um dos procedimentos a seguir:

  - No EAC:
    
    1.  Vá em **Destinatários** \> **Caixa de Correio** ou **Compartilhada**, clique na caixa de correio e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    2.  Na página de propriedades da caixa de correio, clique em **Delegação da Caixa de Correio**.
    
    3.  Se você tiver atribuído permissões para um destinatário, verifique se este usuário ou grupo está listado na permissão apropriada. Se você removeu as permissões, verifique se o destinatário não está listado na permissão apropriada.

Ou

  - No Shell, execute um dos seguintes comandos, dependendo da permissão que você gerenciou.
    
      - **Acesso Completo**
        
            Get-MailboxPermission -Identity <mailbox>
        
        Para verificar se um representante específico é atribuído com a permissão de Acesso Completo para uma caixa de correio, execute o seguinte comando.
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **Enviar como**
        
        No Exchange Server 2013, execute o seguinte comando.
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        No Exchange Online, execute o seguinte comando.
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **Enviar em Nome de**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## Atribuir permissões para um gruo

Como citado anteriormente, você pode atribuir as permissões de Enviar Como e Enviar Em Nome De para grupos de distribuição, grupos de distribuição dinâmica e grupos de segurança habilitados para email para permitir que os representantes enviem mensagens como o grupo em nome do grupo.

As entradas de "Grupos de distribuição" e "Grupos de distribuição dinâmica" na seção "Permissões de Provisionamento do Destinatário" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

## Use o EAC para atribuir permissões

1.  No EAC, navegue até **Destinatários** \> **Grupos**.

2.  Na lista de grupos, clique no grupo para o qual você deseja atribuir permissões e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do grupo, clique em **Delegação de Grupo**.

4.  Para atribuir permissões aos representantes, clique em **Adicionar** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") na permissão apropriada para exibir uma página que mostra uma lista de todos os destinatários na sua organização do Exchange que podem ser atribuídos com essa permissão. Escolha os destinatários desejados, adicione-os à lista e depois clique em **OK**. Você também pode procurar um destinatário específico digitando o nome do destinatário na caixa de pesquisa e depois clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
    
    Para remover a permissão para um destinatário, na permissão apropriada, escolha o destinatário e então clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

5.  Clique em **Salvar** para salvar as suas alterações.

## Use o Shell para atribuir permissões

As seções a seguir mostram como usar o Shell para gerencir as permissões de Enviar Como e Enviar Em Nome De para grupos.

## Gerenciar a permissão Enviar Como

Os exemplos a seguir mostram como gerenciar as permissões de Enviar Como para grupos no Exchange Server 2013 e no Exchange Online. No Exchange 2013, você pode usar os cmdlets **Add-ADPermission** e **Remove-ADPermission** . No Exchange Online, você deve usar os cmdlets **Add-RecipientPermission** e **Remove-RecipientPermission** . Em ambos os casos, você usa o parâmetro *Identity* para especificar o nome do grupo para o qual a permissão de Enviar Como devem ser adicionadas ou removidas e o parâmetro *User* ou o *Trustee* para especificar o representante (por exemplo, um usuário ou grupo) para o qual será atribuída ou não a permissão de Enviar Como.


> [!TIP]
> Use o cmdlet <STRONG>Get-Recipient</STRONG> para obter a propriedade do <EM>Name</EM> para o grupo e para o representante. Use estes valores para atribuir a permissão Enviar Como.



## Exchange Server 2013

Este exemplo atribui a permissão de Enviar Como do grupo Sales Admins para o grupo de nome Contoso Sales Info. Isto permite que os membros do grupo sales admin enviem mensagens como o grupo Contoso Sales Information.

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

Este exemplo remove a permissão de Enviar Como para o usuário Alan Shen no grupo Corporate IT Admins.

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

Para obter informações detalhadas sobre sintaxes e parâmetros, confira:

  - [Add-ADPermission](https://technet.microsoft.com/pt-br/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/pt-br/library/aa996048\(v=exchg.150\))

## Exchange Online

Este exemplo atribui a permissão de Enviar Como para o grupo Contoso Admins no grupo de distribuição dinâmica de nome Transmissão de Mensagens de Emergência.

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

Este exemplo remove a ermissão de Enviar Como para o usuário Walter Harp no grupo de segurança Recursos de Impressora.

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

Para obter informações detalhadas sobre sintaxes e parâmetros, confira:

  - [Add-RecipientPermission](https://technet.microsoft.com/pt-br/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/pt-br/library/ff945794\(v=exchg.150\))

## Gerenciar a permissão de Enviar Em Nome De

Os exemplos a seguir mostram como usar os cmdlets **Set-DistributionGroup** e **Set-DynamicDistributionGroup** para gerenciar as permissões de Enviar Em Nome De para grupos.

Este exemplo atribui ao representante Sara Davis a permissão de Enviar Em Nome De para o grupo de distribuição Suporte da Impressora.

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

Esse exemplo atribui ao representante Administrador a permissão de Enviar Em Nome De para Todos os Funcionários do grupo de distribuição dinâmica.

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

Esse exemplo remove a permissão Enviar Em Nome De no grupo de distribuição dinâmica Todos os Funcionários que foi atribuída ao administrador.

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

Para obter informações detalhadas sobre sintaxes e parâmetros, confira:

  - [Set-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb123796\(v=exchg.150\))

## Como saber se funcionou?

Para verificar se você atribui as permissões para um grupo com sucesso, realize um dos procedimentos a seguir;

  - No EAC:
    
    1.  Vá em **Destinatários** \> **Grupos**, clique em grupo e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    2.  Na página de propriedades do grupo, clique em **Delegação de Grupo**.
    
    3.  Se você tiver atribuído permissões para um destinatário, verifique se este usuário ou grupo está listado na permissão apropriada. Se você removeu as permissões, verifique se o destinatário não está listado na permissão apropriada.

Ou

  - No Shell, execute um dos seguintes comandos dependendo da permissão que você gerenciou.
    
      - **Enviar como**
        
        No Exchange Server 2013, execute o seguinte comando.
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        No Exchange Online, execute o seguinte comando.
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **Enviar em Nome de**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        Ou
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

