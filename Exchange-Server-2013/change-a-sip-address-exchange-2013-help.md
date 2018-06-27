---
title: 'Alterar um endereço SIP: Exchange 2013 Help'
TOCTitle: Alterar um endereço SIP
ms:assetid: 33f4f464-9baa-48af-bf5e-a0d55bb45f60
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335189(v=EXCHG.150)
ms:contentKeyID: 50556161
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar um endereço SIP

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-14_

Quando você habilita um usuário para UM e o vincula a um plano de discagem URI SIP, dois endereços proxy EUM são criados. Um dos endereços contém o número do ramal do usuário e o outro contém um endereço SIP para o usuário. O número do ramal é usado quando o usuário chama para um número do Outlook Voice Access.

Os planos de discagem URI SIP e endereços SIP são usados quando você integra a UM e o Microsoft Office Communications Server 2007 R2 ou o Microsoft Lync Server. O endereço SIP é usado pelo Communications Server ou o Lync Server para rotear chamadas de entrada e enviar mensagens de caixa postal para o usuário. Por padrão, o endereço SIP que é usado pela UM será o endereço SIP que é usado pelo Communications Server ou o Lync Server.

Você pode alterar o endereço SIP principal que foi adicionado quando o usuário foi habilitado para UM ou um endereço SIP secundário que foi adicionado posteriormente, junto com os endereços proxy EUM para o usuário. O endereço SIP principal adicionado quando o usuário foi habilitado para UM será listado como o endereço proxy EUM principal. Todos os outros endereços SIP secundários adicionados serão listados como endereços proxy EUM secundários. Quando endereços SIP secundários são alterados, os chamadores poderão deixar uma mensagem de caixa postal para o usuário em todos os pontos de extremidade de SIP em que o usuário está inscrito para usar os novos endereços SIP. Todas as mensagens de voz serão entregues à mesma caixa de correio do usuário.

Você pode usar o EAC ou o Shell para alterar um endereço SIP principal ou secundário. Você pode usar a página **Endereço de Email** na caixa de correio do usuário no EAC para alterar um endereço SIP principal ou secundário. Não é possível usar a página **Caixa de Correio de UM** no EAC para alterar um endereço SIP principal ou secundário.

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

## Usar o EAC para alterar o endereço SIP principal ou secundário

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  No modo de exibição de lista, selecione a caixa de correio para qual você deseja alterar um endereço SIP e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Caixa de Correio de Usuário**, em **Endereço de email**, selecione o endereço SIP que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). O endereço SIP principal é listado em números e em negrito.

4.  Na página **Endereço de email**, na caixa **Endereço/Ramal**, insira o novo endereço SIP para o usuário e depois clique em **OK**. Se precisar selecionar um novo plano de discagem de UM, você pode clicar em **Navegar**.

5.  Clique em **Salvar**.

## Usar o Shell para alterar o endereço SIP principal ou secundário

Este exemplo altera um endereço SIP para Tony Smith.


> [!TIP]
> Antes de alterar um endereço SIP usando o Shell, é preciso determinar a posição do endereço proxy EUM que deseja modificar. Para determinar a posição, use o comando <STRONG>$mbx.EmailAddresses</STRONG>. O primeiro endereço proxy EUM é o endereço SIP padrão (principal) e será 0 na lista.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:tsmith@contoso.com;phone-context=MySIPDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

