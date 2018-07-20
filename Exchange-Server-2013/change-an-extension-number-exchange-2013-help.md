---
title: 'Alterar um número de ramal: Exchange 2013 Help'
TOCTitle: Alterar um número de ramal
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50556318
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar um número de ramal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem de ramal telefônico, um endereço proxy EUM é criado para o usuário que possui o número de ramal de usuário. Você deve definir pelo menos um número de ramal para a UM usar para que as mensagens de caixa postal sejam enviadas à caixa de correio do usuário. O número do ramal também é usado quando o usuário faz uma chamada telefônica para um número do Outlook Voice Access.

Você pode alterar o número do ramal principal que foi adicionado quando o usuário foi habilitado para Unificação de mensagens ou um número de ramal secundário que foi adicionado mais tarde, juntamente com os endereços de proxy EUM relacionados para o usuário. O número do ramal principal que você adicionou quando o usuário foi habilitado para Unificação de mensagens será listado como o endereço de proxy EUM principal. Qualquer números de ramal de secundário adicionais que você adicionou serão listados como endereços de proxy EUM secundários. Quando os números de ramal foram alterados, os chamadores podem deixar caixa postal para o usuário em todos os novos números de ramal que foram definidos. Todas as mensagens de voz serão entregue à caixa de correio do usuário mesmo.

Você pode usar o EAC ou o Shell para alterar um primário ou um número de ramal secundário para um usuário. Você pode usar a página de **Endereço de Email** na caixa de correio do usuário no EAC para alterar um número de ramal primário ou secundário. Você não pode usar a página de **Correio de UM** no EAC para alterar um número de ramal primário, mas você pode usá-lo para alterar um número de ramal secundário. Se você quiser alterar um número de ramal secundário, você deve remover primeiro o número de ramal de secundário existente e, em seguida, adicione o número de extensão secundário correta para o usuário.

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

## Usar o EAC para alterar o número do ramal primário ou secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione a caixa de correio para o qual você deseja alterar um número de ramal e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de correio do usuário**, em **endereço de Email**, selecione o número do ramal que você deseja alterar e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). O número do ramal primário está listado na números e letras em negrito.

4.  Na página **endereço de Email**, na caixa **Extensão do endereço**, digite o novo número de ramal para o usuário. Se você precisa selecionar um novo plano de discagem de Unificação de mensagens, clique em **Procurar**.

5.  Clique em **Salvar**.

## Use o Shell para alterar o número do ramal primário ou secundário

Este exemplo altera o número de ramal para 22222 de Tony Smith, um usuário habilitado para UM.


> [!TIP]
> Antes de alterar um número de ramal usando o Shell, você precisará determinar a posição do endereço do proxy EUM que você deseja alterar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG> . O primeiro endereço proxy EUM é o número de ramal (principal) do padrão e será 0 na lista.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

