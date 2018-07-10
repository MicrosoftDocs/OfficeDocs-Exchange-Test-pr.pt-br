---
title: 'Adicionar um número e. 164: Exchange 2013 Help'
TOCTitle: Adicionar um número e. 164
ms:assetid: fab86207-be03-40ef-9fea-045a50f3d122
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ662762(v=EXCHG.150)
ms:contentKeyID: 50556317
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar um número e. 164

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem E.164, dois endereços proxy EUM são criados. Um contém o número do ramal do usuário e o outro contém o número E.164 para o usuário. O número do ramal é usado quando o usuário chama para um número do Outlook Voice Access.

O número e. 164 principal que você adicionou quando o usuário foi habilitado para Unificação de mensagens será listado como o endereço de proxy EUM principal. Se o número e. 164 principal foi removido, o primeiro endereço de proxy EUM que você adicionar que contém o número do usuário e. 164 será listado como o endereço de proxy EUM principal. Qualquer números e. 164 adicionais que você adicionar serão listados como endereços de proxy EUM secundários. Quando os números de e. 164 adicionais são adicionados, os chamadores podem deixar a caixa postal para o usuário em todos os números e. 164 que foram definidos. Todas as mensagens de voz serão entregue à caixa de correio do usuário mesmo.

Você pode usar o EAC ou o Shell para adicionar um primário ou um número e. 164 secundário para um usuário. Você pode usar a página de **Endereço de Email** na caixa de correio do usuário no EAC para adicionar um número e. 164 de primário ou secundário. Você não pode usar a página de **Correio de UM** no EAC para adicionar um número e. 164 de primário ou secundário.

Você pode visualizar os números E.164 principais e secundários para um usuário usando o cmdlet **Get-UMMailbox** ou o cmdlet **Get-Mailbox** no Shell.

Para mais tarefas de gerenciamento relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM E.164 foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que caixa de correio do usuário foi habilitada para Unificação de mensagens e vinculada a um plano de discagem e. 164. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que o número e. 164 que será atribuído ao usuário é válido e está formatada corretamente.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para adicionar um número e. 164 de primário ou secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na exibição de lista, selecione a caixa de correio para o qual você deseja adicionar um número e. 164 e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de Correio de Usuário**, em **Endereço de email**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **novo endereço de email**, selecione **EUM** e, na caixa **Extensão do endereço**, digite o novo número e. 164 para o usuário.

5.  Na página **novo endereço de email**, em **plano de discagem**, clique em **Procurar** para selecionar o plano de discagem e. 164 e clique em **OK**.

6.  Clique em **Salvar**.

## Use o Shell para adicionar um número e. 164

Este exemplo adiciona um número e. 164 de Tony Smith, um usuário habilitado para UM.


> [!TIP]
> Antes de adicionar um número e. 164 usando o Shell, você precisará determinar a posição do endereço do proxy EUM que você deseja adicionar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG> . O primeiro endereço de proxy na lista será 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(2)="eum:+14255550123;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

