---
title: 'Adicionar um número de ramal: Exchange 2013 Help'
TOCTitle: Adicionar um número de ramal
ms:assetid: 1a73c9c8-cb50-4bd7-a101-dadd20e28031
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335124(v=EXCHG.150)
ms:contentKeyID: 50556152
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar um número de ramal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem de ramal telefônico, um endereço proxy EUM é criado para o usuário que possui o número de ramal de usuário. Você deve definir pelo menos um número de ramal para a UM usar para que as mensagens de caixa postal sejam enviadas à caixa de correio do usuário. O número do ramal também é usado quando o usuário faz uma chamada telefônica para um número do Outlook Voice Access.

O número do ramal principal adicionado quando o usuário foi habilitado para a UM será listado como o endereço proxy EUM principal. Se o número de ramal principal tiver sido removido, o primeiro endereço proxy EUM adicionado que contém o número de ramal do usuário se tornará o endereço proxy EUM principal. Todos os outros números de ramal adicionados serão listados como endereços proxy EUM secundários. Quando outros números de ramal são adicionados, os chamadores podem deixar uma mensagem de caixa postal para o usuário em todos os números de ramal que foram definidos. Todas as mensagens de voz serão entregues à mesma caixa de correio do usuário.

Você pode usar o EAC ou o Shell para adicionar um número de ramal principal ou secundário para um usuário. Você pode usar a página **Endereço de Email** na caixa de correio do usuário no EAC para adicionar um número de ramal principal ou secundário. Não é possível usar a página **Caixa de Correio de UM** no EAC para adicionar um número de ramal principal, mas você pode usar essa página para adicionar números de ramal secundários.

Você pode visualizar os números de ramal principais e secundários para um usuário usando o cmdlet **Get-UMMailbox** ou o cmdlet **Get-Mailbox** no Shell.

Para mais tarefas de gerenciamento relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM de ramal telefônico foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se a caixa de correio do usuário foi habilitada para a UM e vinculada a um plano de discagem de ramal telefônico. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se o número de ramal que será atribuído ao usuário contém o número de dígitos correto definido no plano de discagem de UM.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para adicionar um número de ramal secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  No modo de exibição de lista, selecione a caixa de correio em que você deseja adicionar um número de ramal.

3.  No painel de detalhes, **Recursos de Telefone e Voz**, em **Unificação de Mensagens**, clique em **Exibir detalhes**.

4.  Na página **Caixa de Correio de UM**, clique em **Outros Ramais** e, em seguida, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Na página **Outros ramais**, ao lado da caixa **Plano de discagem de UM**, clique em **Navegar** e localize o plano de discagem para o usuário.

6.  Na página **Outros ramais**, na caixa **Número de ramal**, digite o número do ramal e depois clique em **OK**.

7.  Clique em **Salvar**.

## Usar o EAC para adicionar um número de ramal principal ou secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  No modo de exibição de lista, selecione a caixa de correio à qual você deseja adicionar um número de ramal e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de Correio de Usuário**, em **Endereço de email**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **Novo endereço de email**, selecione **EUM** e, na caixa **Endereço/Ramal**, digite o número de ramal do usuário.

5.  Na página **Novo endereço de email**, em **Plano de discagem**, clique em **Navegar** para selecionar o plano de discagem do ramal telefônico e depois clique em **OK**.

6.  Clique em **Salvar**.

## Usar o Shell para adicionar um número de ramal

Este exemplo adiciona um número de ramal 22222 para Tony Smith, um usuário habilitado para UM.


> [!TIP]
> Antes de adicionar um número de ramal usando o Shell, é preciso determinar a posição do endereço proxy EUM que deseja adicionar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG>. O primeiro endereço proxy na lista será 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

