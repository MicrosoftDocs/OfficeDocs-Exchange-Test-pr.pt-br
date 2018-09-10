---
title: 'Configurar limites de tamanho de mensagem para uma caixa de correio'
TOCTitle: Configurar os limites de tamanho de mensagens de uma caixa de correio
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50556288
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar os limites de tamanho de mensagens de uma caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-12_

Você pode usar o EAC e o Shell para configurar os limites de tamanho de mensagens da caixa de correio de um usuário. Esses limites controlam o tamanho das mensagens que um usuário pode enviar e receber. Por padrão, quando uma caixa de correio é criada, não há um limite de tamanho para as mensagens enviadas e recebidas.

Há outras configurações em uma organização do Exchange que determinam o tamanho máximo de mensagens que uma caixa de correio pode enviar e receber (por exemplo, o tamanho máximo de mensagens configurado em um servidor de caixa de correio). Saiba mais sobre as restrições de tamanho de mensagens no Exchange, inclusive os tipos de limite de tamanho de mensagens, o escopo e a ordem de precedência delas em [Limites de tamanhos de mensagens](message-size-limits-exchange-2013-help.md).

Confira outras tarefas de gerenciamento relacionadas às caixas de correio de usuário em [Gerenciar caixas de correio do usuário](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).


> [!NOTE]
> Também é possível controlar o tamanho das mensagens enviadas e recebidas por usuários de correio e de caixas de correio compartilhadas.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar os limites de tamanho de mensagens

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique naquela cujos limites de tamanho das mensagens você quer alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Restrições de tamanho das mensagens**, clique em **Exibir detalhes** para exibir e alterar estes limites de tamanho das mensagens:
    
      - **Mensagens enviadas**   Para especificar um tamanho máximo para as mensagens enviadas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário enviar uma mensagem maior do que o tamanho especificado, ela retornará ao remetente com uma mensagem de erro descritiva.
    
      - **Mensagens recebidas**   Para especificar um tamanho máximo para as mensagens recebidas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário receber uma mensagem maior do que o tamanho especificado, ela será devolvida ao remetente com uma mensagem de erro descritiva.

5.  Clique em **OK** e em **Salvar** para salvar as alterações.

## Usar o Shell para configurar limites de tamanho de mensagens

Este exemplo define o tamanho máximo de mensagens enviadas como 25 MB e o tamanho máximo de mensagens recebidas como 35 MB para a caixa de correio de Sara Melo.

    Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você conseguiu configurar os limites de tamanho de mensagens, siga um destes procedimentos:

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio dos usuários, clique na caixa de correio cujos limites de tamanho das mensagens você quer verificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Restrições de tamanho de mensagens**, clique em **Exibir detalhes** para verificar os limites de tamanho das mensagens da caixa de correio.

Ou

Execute o seguinte comando no Shell.

    Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize

