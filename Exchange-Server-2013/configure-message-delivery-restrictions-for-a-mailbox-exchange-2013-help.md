---
title: 'Configurar restrições de entrega de mensagens para uma caixa de correio'
TOCTitle: Configurar restrições de entrega de mensagens para uma caixa de correio
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50556279
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar restrições de entrega de mensagens para uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-11-29_

Você pode usar o EAC ou o Shell para colocar restrições em se as mensagens são entregues aos destinatários individuais. Restrições de entrega de mensagem são úteis para controlar quem pode enviar mensagens para usuários em sua organização. Por exemplo, você pode configurar uma caixa de correio para aceitar ou rejeitar mensagens enviadas por usuários específicos ou para aceitar mensagens apenas de usuários em sua organização do Exchange.

As restrições de entrega de mensagem abordadas neste tópico se aplicam a todos os tipos de destinatário. Para saber mais sobre os diferentes tipos de destinatário, consulte [Destinatários](recipients-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas aos destinatários, consulte os tópicos a seguir:

  - [Gerenciar caixas de correio do usuário](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)

  - [Criar e gerenciar grupos de distribuição](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups)

  - [Gerenciar grupos dinâmicos de distribuição](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [Gerenciar usuários de email](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-mail-users)

  - [Gerenciar contatos de email](manage-mail-contacts-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar restrições de entrega de mensagem

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio do usuário, clique em caixa de correio que você deseja configurar restrições de entrega de mensagens para e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Restrições de entrega de mensagem**, clique em **Exibir detalhes** para exibir e alterar as seguintes restrições de entrega:
    
      - **Aceitar mensagens de**   Use essa seção para especificar quem pode enviar mensagens para esse usuário.
        
          - **Todos os remetentes**    Essa opção especifica que o usuário pode aceitar mensagens de todos os remetentes. Isso inclui ambos os remetentes em sua organização do Exchange, mas os remetentes externos. Esta é a opção padrão. Ela inclui usuários externos somente se você desmarcar a caixa de seleção **exigir que todos os remetentes sejam autenticados**. Se você selecionar essa caixa de seleção, serão rejeitadas as mensagens de usuários externos.
        
          - **Apenas os remetentes na lista a seguir**    Essa opção especifica que o usuário pode aceitar mensagens somente de um conjunto especificado de remetentes em sua organização do Exchange. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para exibir uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que você deseja, adicioná-los à lista e clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa Pesquisar e clicando em **pesquisa**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
        
          - **Exigir que todos os remetentes sejam autenticados**    Essa opção impede que usuários anônimos enviem mensagens para o usuário. Isso inclui usuários externos que estão fora da sua organização do Exchange.
    
      - **Rejeitar mensagens de**   Use essa seção para evitar que pessoas enviem enviar mensagens para esse usuário.
        
          - **Não há remetentes**    Essa opção especifica que a caixa de correio não rejeitar mensagens de qualquer remetente na organização do Exchange. Esta é a opção padrão.
        
          - **Remetentes na lista a seguir**    Essa opção especifica que a caixa de correio irá rejeitar mensagens de um conjunto especificado de remetentes em sua organização do Exchange. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para exibir uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que você deseja, adicioná-los à lista e clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa Pesquisar e clicando em **pesquisa**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").

5.  Clique em **OK** para fechar a página de **Restrições de entrega de mensagem** e clique em **Salvar** para salvar suas alterações.

## Use o Shell para configurar restrições de entrega de mensagem

Os exemplos a seguir mostram como usar o Shell para configurar restrições de entrega de mensagens para uma caixa de correio. Para outros tipos de destinatário, use o cmdlet **Set-** correspondente com os mesmos parâmetros.

Este exemplo configura a caixa de correio de Robin Wood para aceitar mensagens apenas dos usuários Lori Penor, Jeff Phillips, e a equipe 1 legais de grupo de membros da distribuição.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"


> [!TIP]
> Se você estiver configurando uma caixa de correio para aceitar mensagens somente de remetentes individuais, você precisa usar o parâmetro <EM>AcceptMessagesOnlyFrom</EM> . Se você estiver configurando uma caixa de correio para aceitar mensagens somente de remetentes que são membros de um grupo de distribuição específica, use o parâmetro <EM>AcceptMessagesOnlyFromDLMembers</EM> .



Este exemplo adiciona o usuário chamado David Pelton à lista de usuários cujas mensagens serão aceitas por caixa de correio de Robin Wood.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

Este exemplo configura a caixa de correio de Robin Wood para exigir que todos os remetentes sejam autenticados. Isso significa que a caixa de correio aceitará somente as mensagens enviadas por outros usuários em sua organização do Exchange.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

Este exemplo configura a caixa de correio de Robin Wood para rejeitar mensagens de Joe Healy, Terry Adams, usuários e membros da distribuição grupo 2 legais de equipe.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

Este exemplo configura a caixa de correio de Robin Wood também rejeitar mensagens enviadas pelos membros do grupo 3 legais de equipe.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}


> [!TIP]
> Se você estiver configurando uma caixa de correio para rejeitar mensagens de remetentes individuais, você precisa usar o parâmetro <EM>RejectMessagesFrom</EM> . Se você estiver configurando uma caixa de correio para rejeitar mensagens de remetentes que são membros de um grupo de distribuição específica, use o parâmetro <EM>RejectMessagesFromDLMembers</EM> .



Para detalhadas sobre sintaxe e informações de parâmetro relacionados à configuração de restrições de entrega para diferentes tipos de destinatários, consulte os tópicos a seguir:

  - [Set-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/pt-br/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/pt-br/library/aa995971\(v=exchg.150\))

## Como saber se funcionou?

Para verificar se você configurou com êxito as restrições de entrega de mensagem para uma caixa de correio do usuário, siga um o seguinte:

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio do usuário, clique em caixa de correio que você deseja verificar as restrições de entrega de mensagem para e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Restrições de entrega de mensagem**, clique em **Exibir detalhes** para verificar as restrições de entrega da caixa de correio.

Ou

Execute o seguinte comando no Shell.

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

