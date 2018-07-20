---
title: 'Adicionar um endereço SIP: Exchange 2013 Help'
TOCTitle: Adicionar um endereço SIP
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50556187
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar um endereço SIP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem URI SIP, dois endereços proxy EUM são criados. Um dos endereços contém o número do ramal do usuário e o outro contém um endereço SIP para o usuário. O número do ramal é usado quando o usuário chama para um número do Outlook Voice Access.

Os planos de discagem URI SIP e endereços SIP são usados quando você integra a UM e o Microsoft Office Communications Server 2007 R2 ou o Microsoft Lync Server. O endereço SIP é usado pelo Communications Server ou o Lync Server para rotear chamadas de entrada e enviar mensagens de caixa postal para o usuário. Por padrão, o endereço SIP que é usado pela UM será o endereço SIP que é usado pelo Communications Server ou o Lync Server.

O endereço SIP principal que você adicionou quando o usuário foi habilitado para Unificação de mensagens será listado como o endereço de proxy EUM principal. Se o endereço SIP principal foi removido, o primeiro endereço de proxy EUM que você adicionar que contém o endereço SIP do usuário será listado como o endereço de proxy EUM principal. Nenhum endereço SIP adicional que você adicionar será listado como endereços de proxy EUM secundários. Quando forem adicionados endereços SIP do secundários, os chamadores podem deixar a caixa postal para o usuário nos pontos de extremidade SIP que o usuário está conectado ao usando os endereços SIP. Todas as mensagens de voz serão entregue à caixa de correio do usuário mesmo.

Você pode usar o EAC ou o Shell para adicionar um primário ou um endereço SIP secundário para um usuário. Você pode usar a página de **Endereço de Email** na caixa de correio do usuário no EAC para adicionar um endereço SIP de primário ou secundário. Você não pode usar a página de **Correio de UM** no EAC para adicionar um endereço SIP de primário ou secundário.

Você pode visualizar os endereços SIP principais e secundários para um usuário que esteja usando o cmdlet **Get-UMMailbox** ou o cmdlet **Get-Mailbox** no Shell.

Para mais tarefas de gerenciamento relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM de URI SIP foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se o usuário existente foi habilitado para UM e vinculado a um plano de discagem URI SIP. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de realizar esses procedimentos, verifique se o endereço SIP que será atribuído ao usuário é válido e se está formatado corretamente.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para adicionar um endereço SIP de primário ou secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na exibição de lista, selecione a caixa de correio para o qual você deseja adicionar um endereço SIP e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de Correio de Usuário**, em **Endereço de email**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **novo endereço de email**, selecione **EUM** e, na caixa **Extensão do endereço**, digite o novo endereço SIP do usuário.

5.  Na página **novo endereço de email**, em **plano de discagem**, clique em **Procurar** para selecionar o plano de discagem URI do SIP e, em seguida, clique em **OK**.

6.  Clique em **Salvar**.

## Use o Shell para adicionar um endereço SIP

Este exemplo adiciona um endereço SIP de Tony Smith, um usuário habilitado para UM.


> [!TIP]
> Antes de adicionar um endereço SIP usando o Shell, você precisará determinar a posição do endereço do proxy EUM que você deseja adicionar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG> . O primeiro endereço de proxy na lista será 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

