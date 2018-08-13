---
title: 'Acompanhar mensagens com notificações de entrega: Exchange 2013 Help'
TOCTitle: Acompanhar mensagens com notificações de entrega
ms:assetid: a14e4e62-08ca-4a7b-92e1-d39fe3e0a9e5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150554(v=EXCHG.150)
ms:contentKeyID: 50484761
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Acompanhar mensagens com notificações de entrega

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-13_

Notificações de Entrega é uma ferramenta de acompanhamento de mensagens no Centro de Administração do Exchange (EAC) que pode ser usada para pesquisar o status de entrega de emails enviados ou recebidos dos usuários do catálogo de endereços compartilhado da organização, com um determinado assunto. É possível acompanhar informações de entrega sobre mensagens enviadas ou recebidas em qualquer caixa de correio específica da organização. O conteúdo do corpo da mensagem não é retornado em uma notificação de entrega, mas a linha de assunto é exibida nos resultados. Você pode acompanhar mensagens por até 14 dias após elas serem enviadas ou recebidas.


> [!TIP]
> O recurso Notificações de Entrega acompanha mensagens enviadas por pessoas que usam os clientes de email Microsoft Outlook ou Outlook Web App. Ele não acompanha mensagens enviadas de clientes de email POP ou IMAP como o Windows Mail Outlook Express ou Mozilla Thunderbird.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: O tempo de conclusão variará com base no escopo de sua pesquisa.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Rastreamento de mensagens" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## O que você deseja fazer?

Use the EAC to track messages

Use the EAC to review a delivery report

## Usar o EAC para acompanhar mensagens

1.  Na EAC, navegue até **Fluxo de Emails** \> **Notificações de Entrega**.

2.  Insira as seguintes informações:
    
      - **\*Caixa de correio a ser pesquisada:**  Clique em **Procurar** para selecionar a caixa de correio no catálogo de endereços e clique em **OK**. É necessário selecionar a caixa de correio a ser pesquisada.
    
      - Selecione uma destas opções:
        
          - **Procurar mensagens enviadas para** Selecione esta opção para procurar mensagens enviadas a usuários específicos. Clique em **Selecionar usuários** e escolha os usuários no catálogo de endereços selecionando um usuário na lista e clicando em **Adicionar**. Você pode selecionar mais de um usuário. Quando terminar de selecionar os usuários, clique em **OK** para voltar à página de **Notificações de Entrega**. Ao selecionar esta opção, você também pode deixar o campo em branco para localizar mensagens enviadas a qualquer pessoa.
        
          - **Procurar mensagens recebidas de**  Use esta opção para procurar mensagens recebidas de um usuário específico. Novamente, basta selecionar um usuário no catálogo de endereços e clicar em **OK** para voltar à página **Notificações de Entrega**. Se você selecionar esta opção, será preciso especificar um remetente.
    
      - **Procurar por estas palavras na linha de assunto** Insira aqui as informações da linha de assunto ou deixe em branco para expandir a pesquisa.

3.  Ao concluir, clique em **Pesquisar**. Se desejar recomeçar, clique em **Limpar**.

## Use o EAC para analisar um relatório de entrega

Para exibir informações da entrega, selecione uma mensagem no painel **Resultados da pesquisa** e clique em **Detalhes**.

A notificação de entrega mostra o status de entrega e informações de entrega detalhadas da mensagem que você selecionou no painel **Resultados da Pesquisa**. Na parte superior da notificação, você verá os seguintes campos:

  - **Assunto** A linha de assunto da mensagem é exibida como cabeçalho da notificação.

  - **De** Alias, nome para exibição ou endereço de email da pessoa que enviou a mensagem.

  - **Para**   Alias, nome para exibição ou endereço de email de cada destinatário da mensagem.

  - **Enviada** Data e hora em que a mensagem foi enviada.

## Seção Resumo até

Esta seção aparecerá na notificação de entrega se uma mensagem for enviada a mais de uma pessoa ou destinatário. A parte superior da seção informa o número total de destinatários para os quais a mensagem foi enviada e fornece informações de entrega resumidas para cada destinatário.

  - **Resumo até** Exibe o total de destinatários e se há mensagens Pendentes, Entregues ou com Falha. Clique nos hiperlinks para classificar por status.

  - **Caixa de pesquisa**   A caixa de pesquisa será útil se você enviar a mensagem para um grupo com mais de 30 destinatários. Na caixa de pesquisa, digite um endereço de email sobre o qual você deseja obter informações de entrega e clique na lupa.

  - **Para** mostra o endereço de email do destinatário.

  - **Status** Esta coluna mostra o status da mensagem para cada destinatário.

## Informações detalhadas da notificação

Esta seção contém informações de entrega detalhadas de uma mensagem enviada ao destinatário selecionado a seção Resumo até.

  - **Notificação de Entrega de**   O endereço de email do destinatário selecionado é mostrado aqui.

  - **Enviada**   Data e hora em que a mensagem foi enviada para entrega pelo sistema.

Dependendo do estado de entrega da mensagem, você poderá ver diversos estados de status, incluindo:

  - **Entregue** Indica uma entrega bem-sucedida.

  - **Adiada** Indica que a mensagem foi adiada.

  - **Pendente** Se a entrega da mensagem estiver pendente porque a mensagem atende aos critérios de uma regra ou diretiva de toda a organização ou porque ela está sujeita a aprovação, a mensagem de status explicará a ação em execução por uma regra ou que a mensagem deve ser aprovada por um moderador antes da entrega.

  - **Moderador**   O status indica se a mensagem foi aprovada ou rejeitada pelo moderador.

  - **Grupo Expandido** Se uma mensagem foi enviada a um grupo, os usuários individuais são mostrados na seção **Resumo até**, de forma que você possa ver o status de entrega de cada destinatário. Se for necessário remover ou adicionar um usuário a um grupo durante uma investigação de notificação de entrega, você poderá modificar um grupo clicando em **Editar Grupos**.

  - **Falha**   Mostra a data, a hora e o motivo de falha na entrega de uma mensagem. Por exemplo, uma regra de toda a organização pode estar bloqueando a entrega da mensagem ou não foi possível entregar a mensagem.

Ao concluir a revisão da notificação, clique em **Fechar**. As notificações de entrega não são salvas, mas você pode executar uma notificação novamente a qualquer momento. Lembre-se de que há um intervalo de pesquisa de duas semanas.

## Como saber se funcionou?

Se a sua pesquisa tiver sido realizada com êxito, as mensagens que se enquadrarem nos critérios de pesquisa serão listadas no painel **Resultados da pesquisa**. Para exibir as informações de entrega de uma mensagem específica, selecione-a e clique em **Detalhes**. Se nenhuma mensagem for exibida no painel **Resultados da pesquisa**, altere os critérios de pesquisa e execute novamente a pesquisa.

