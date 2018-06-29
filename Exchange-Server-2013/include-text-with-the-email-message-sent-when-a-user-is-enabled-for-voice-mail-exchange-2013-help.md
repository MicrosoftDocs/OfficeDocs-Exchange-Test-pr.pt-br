---
title: 'Incluir texto com a mensagem de email enviada quando um usuário está habilitado para caixa postal: Exchange 2013 Help'
TOCTitle: Incluir texto com a mensagem de email enviada quando um usuário está habilitado para caixa postal
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51407853
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir texto com a mensagem de email enviada quando um usuário está habilitado para caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-12-16_

Quando a caixa de correio de um usuário for habilitada para Unificação de Mensagens (UM), uma mensagem de email de boas-vindas à Unificação de Mensagens será enviada ao usuário. Essa mensagem contém as informações de PIN que o usuário utilizará para acessar o sistema de Unificação de Mensagens pela primeira vez.

Você pode personalizar o texto enviado na mensagem de email de boas-vindas adicionando o texto à caixa **Quando um usuário está habilitado para Unificação de Mensagens** em uma política de caixa de correio da UM. É possível incluir informações como os números de telefone de suporte técnico da UM ou números adicionais do Outlook Voice Access. Depois de adicionar o texto, ele será incluído na mensagem de email enviada quando os usuários associados à política de caixa de correio da UM estiverem habilitados para Unificação de Mensagens.


> [!TIP]
> O texto personalizado adicionado à mensagem de boas-vindas é limitado a 512 caracteres e pode incluir texto HTML simples.



Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para personalizar o texto enviado quando uma caixa de correio for habilitada para Unificação de Mensagens

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Política de Caixa de Correio da UM** \> **Texto da mensagem**, na caixa de texto para **Quando um usuário está habilitado para Unificação de Mensagens**, insira o texto que deseja incluir na mensagem de email enviada quando usuários estão habilitados para caixa postal da Unificação de Mensagens.

4.  Clique em **Salvar**.

## Usar o Shell para personalizar o texto enviado quando uma caixa de correio for habilitada para Unificação de Mensagens

Este exemplo habilita usuários habilitados para a UM que estejam associados a uma diretiva de caixa de correio da UM a receber instruções adicionais sobre a UM e o número do Outlook Voice Access que podem usar para acessar sua caixa de correio pelo telefone.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

