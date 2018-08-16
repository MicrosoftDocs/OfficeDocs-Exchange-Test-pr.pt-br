---
title: 'Remover um endereço SIP: Exchange 2013 Help'
TOCTitle: Remover um endereço SIP
ms:assetid: eaaff0b0-7d85-4845-a7b8-ac22b42bc415
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ662761(v=EXCHG.150)
ms:contentKeyID: 50556305
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um endereço SIP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem URI SIP, dois endereços proxy EUM são criados. Um dos endereços contém o número do ramal do usuário e o outro contém um endereço SIP para o usuário. O número do ramal é usado quando o usuário chama para um número do Outlook Voice Access.

Os planos de discagem URI SIP e endereços SIP são usados quando você integra a UM e o Microsoft Office Communications Server 2007 R2 ou o Microsoft Lync Server. O endereço SIP é usado pelo Communications Server ou o Lync Server para rotear chamadas de entrada e enviar mensagens de caixa postal para o usuário. Por padrão, o endereço SIP que é usado pela UM será o endereço SIP que é usado pelo Communications Server ou o Lync Server.

Você pode remover o endereço SIP principal que foi adicionado quando o usuário foi habilitado para Unificação de mensagens ou um endereço SIP secundário que foi adicionado mais tarde, juntamente com o endereço de proxy EUM para o usuário. O endereço SIP principal que você adicionou quando o usuário foi habilitado para Unificação de mensagens será listado como o endereço de proxy EUM principal. Nenhum endereço SIP adicional que você adicionou será listado como endereços de proxy EUM secundários. Quando um endereço SIP é removido, os chamadores podem deixar uma caixa postal para o usuário não é mais no endereço SIP que foi removido, mesmo se o usuário tiver entrado com o endereço SIP atribuído ao usuário no Communications Server ou do Lync Server.

Se você remover o endereço SIP principal, Unificação de mensagens não será capaz de enviar a caixa postal para a caixa de correio do usuário e não serão processadas regras de atendimento de chamada. Depois que o endereço SIP principal foi removido, o endereço de proxy EUM para o usuário será listado como **Nulo** na caixa de correio do usuário no EAC e quando você executa o cmdlet **Get-Mailbox** no Shell. Além disso, quando você executar o cmdlet **Get-UMMailbox** , os parâmetros *Extensions*, *PhoneNumber*e *CallAnsweringRulesExtensions* poderão ser em branco ou nulo.

Você pode usar o EAC ou o Shell para remover um primário ou um endereço SIP secundário. Você pode usar a página de **Endereço de Email** na caixa de correio do usuário no EAC para remover um primário ou um endereço SIP secundário. Você não pode usar a página de **Correio de UM** no EAC para remover um endereço SIP primário ou secundário.

Você pode visualizar os endereços SIP principais e secundários para um usuário que esteja usando o cmdlet **Get-UMMailbox** ou o cmdlet **Get-Mailbox** no Shell.

Para mais tarefas de gerenciamento relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que caixa de correio do usuário foi habilitada para Unificação de mensagens e vinculada a um plano de discagem URI do SIP. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se os endereços SIP do primários e secundários estão configurados para o usuário.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover o principal ou um endereço SIP secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione a caixa de correio a partir do qual você deseja remover um endereço SIP e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de correio do usuário**, em **endereço de Email**, selecione o endereço SIP que você deseja remover da lista e, em seguida, clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone"). O endereço de proxy EUM principal ou o endereço SIP está listado na números e letras em negrito.

4.  Clique em **Salvar**.

## Use o Shell para remover o principal ou um endereço SIP secundário

Este exemplo remove o SIP endereço tsmith@contoso.com da caixa de correio de Tony Smith, um usuário habilitado para UM.


> [!NOTE]  
> Antes de remover um endereço SIP usando o Shell, você precisará determinar a posição do endereço do proxy EUM que você deseja modificar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG> . O endereço de proxy EUM primeiro na lista será 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:tsmith@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

