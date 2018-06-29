---
title: 'Remover um número e. 164: Exchange 2013 Help'
TOCTitle: Remover um número e. 164
ms:assetid: 17941918-7dc5-41a0-b540-09f2f907362b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ662759(v=EXCHG.150)
ms:contentKeyID: 50556149
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um número e. 164

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem E.164, dois endereços proxy EUM são criados. Um contém o número do ramal do usuário e o outro contém o número E.164 para o usuário. O número do ramal é usado quando o usuário chama para um número do Outlook Voice Access.

Você pode remover o número e. 164 principal que foi adicionado quando o usuário foi habilitado para Unificação de mensagens ou um número e. 164 secundário que foi adicionado mais tarde, juntamente com os endereços de proxy EUM para o usuário. O número e. 164 principal que você adicionou quando o usuário foi habilitado para Unificação de mensagens será listado como o endereço de proxy EUM principal. Qualquer números e. 164 adicionais que você adicionou serão listados como endereços de proxy EUM secundários. Quando um número e. 164 é removido, os chamadores não são mais podem deixar caixa postal para o usuário no número e. 164 que foi removido.

Se você remover o número e. 164 primário, Unificação de mensagens não será capaz de enviar a caixa postal para a caixa de correio do usuário e não serão processadas regras de atendimento de chamada. Depois de remover o número e. 164 principal, o endereço de proxy EUM para o usuário será listado como **Nulo** na caixa de correio do usuário no EAC e quando você executa o cmdlet **Get-Mailbox** no Shell. Além disso, quando você executar o cmdlet **Get-UMMailbox** , os parâmetros *Extensions*, *PhoneNumber*e *CallAnsweringRulesExtensions* poderão ser em branco ou nulo.

Você pode usar o EAC ou o Shell para remover um primário ou um número e. 164 secundário para um usuário. Você pode usar a página de **Endereço de Email** na caixa de correio do usuário no EAC para remover um primário ou secundário número e. 164. Você não pode usar a página de **Correio de UM** no EAC para remover um número e. 164 de primário ou secundário.

Você pode visualizar os números E.164 principais e secundários para um usuário usando o cmdlet **Get-UMMailbox** ou o cmdlet **Get-Mailbox** no Shell.

Para mais tarefas de gerenciamento relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme que um plano de discagem e. 164 UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se a caixa de correio do usuário foi habilitada para UM e vinculada a um plano de discagem E.164. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se os números e. 164 primários e secundários estão configurados para o usuário.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover o principal ou um número e. 164 secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione a caixa de correio a partir do qual você deseja remover um número e. 164 e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de correio do usuário**, em **endereço de Email**, selecione o número e. 164 que você deseja remover da lista e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone"). O endereço de proxy EUM principal ou o número e. 164 estará listado na números e letras em negrito.

4.  Clique em **Salvar**.

## Use o Shell para remover o principal ou um número e. 164 secundário

Este exemplo remove o número e. 164 +14255551010 da caixa de correio de Tony Smith, um usuário habilitado para UM.


> [!TIP]
> Antes de remover um número e. 164 usando o Shell, você precisará determinar a posição do endereço do proxy EUM que você deseja modificar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG> . O endereço de proxy EUM primeiro na lista será 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:+14255551010;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

