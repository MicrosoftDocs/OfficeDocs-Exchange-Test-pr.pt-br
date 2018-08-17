---
title: 'Remover um número de ramal: Exchange 2013 Help'
TOCTitle: Remover um número de ramal
ms:assetid: c2b896cf-21f7-4453-a4e6-b23d236a6dd3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351124(v=EXCHG.150)
ms:contentKeyID: 50556273
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um número de ramal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-07-21_

Quando você habilita um usuário para UM e o vincula a um plano de discagem de ramal telefônico, um endereço proxy EUM é criado para o usuário que possui o número de ramal de usuário. Você deve definir pelo menos um número de ramal para a UM usar para que as mensagens de caixa postal sejam enviadas à caixa de correio do usuário. O número do ramal também é usado quando o usuário faz uma chamada telefônica para um número do Outlook Voice Access.

Você pode remover o número do ramal primário que foi adicionado quando o usuário foi habilitado para Unificação de mensagens ou um número de ramal secundário que foi adicionado mais tarde, juntamente com os endereços de proxy EUM relacionados para o usuário. O número do ramal principal que você adicionou quando o usuário foi habilitado para Unificação de mensagens será listado como o endereço de proxy EUM principal. Qualquer números de ramal adicionais que você adicionou serão listados como endereços de proxy EUM secundários. Quando um número de ramal for removido, os chamadores não são mais podem deixar caixa postal para o usuário no número do ramal que foi removido.

Se você remover o número do ramal principal, Unificação de mensagens não será capaz de enviar a caixa postal para a caixa de correio do usuário e não serão processadas regras de atendimento de chamada. Depois que o número do ramal principal foi removido, o endereço de proxy para o usuário EUM será listado como **Nulo** na caixa de correio do usuário no EAC e quando você executa o cmdlet **Get-Mailbox** no Shell. Além disso, quando você executar o cmdlet **Get-UMMailbox** , os parâmetros *Extensions*, *PhoneNumber*e *CallAnsweringRulesExtensions* será em branco ou nulo.

Você pode usar o EAC ou o Shell para remover um primário ou um número de ramal secundário. Você pode usar a página de **Endereço de Email** na caixa de correio do usuário no EAC para remover um primário ou um número de ramal secundário. Você não pode usar a página de **Correio de UM** no EAC para remover um número de ramal principal, mas você pode usá-lo para remover um número de ramal secundário.

Você pode visualizar os números de ramal principais e secundários para um usuário usando o cmdlet **Get-UMMailbox** ou o cmdlet **Get-Mailbox** no Shell.

Para mais tarefas de gerenciamento relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se a caixa de correio do usuário foi habilitada para a UM e vinculada a um plano de discagem de ramal telefônico. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se os números de ramal primários e secundários estão configurados para o usuário.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover o número do ramal primário ou secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione a caixa de correio a partir do qual você deseja remover um número de ramal e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de correio do usuário**, em **endereço de Email**, selecione o número do ramal que você deseja remover da lista e, em seguida, clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone"). O principal EUM endereço ou extensão número proxy está listado na números e letras em negrito.

4.  Clique em **Salvar**.

## Usar o EAC para remover um número de ramal secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione o usuário cuja caixa de correio que você deseja remover um número de ramal de.

3.  No painel de detalhes, em **Telefone e Características de Voz** \> **Unificação de Mensagens**, clique em **Ver detalhes**.

4.  Na página **outras extensões**, na caixa **número de ramal**, selecione o número do ramal que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

5.  Clique em **Salvar**.

## Use o Shell para remover um número de ramal

Este exemplo remove o número do ramal 12345 da caixa de correio de Tony Smith, um usuário habilitado para UM.


> [!NOTE]
> Antes de remover um número de ramal usando o Shell, você precisará determinar a posição do endereço do proxy EUM que você deseja modificar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG> . O endereço de proxy EUM primeiro na lista será 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.remove("eum:22222;phone-context=MyDialPlan.contoso.com") 
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

