---
title: 'Incluir texto com a mensagem de email enviada quando uma redefinição de PIN é: Exchange 2013 Help'
TOCTitle: Incluir texto com a mensagem de email enviada quando uma redefinição de PIN é
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51407939
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir texto com a mensagem de email enviada quando uma redefinição de PIN é

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode incluir texto adicional na mensagem de email enviada aos usuários quando seus Unificação de mensagens (UM) ou o PIN da caixa postal é redefinida. Você pode fazer isso inserindo texto personalizado na caixa de ferramentas **ao Outlook Voice Access PIN de um usuário é redefinido** em uma diretiva de caixa de correio de UM. O texto personalizado pode incluir, por exemplo, as informações relacionadas a segurança para usuários habilitados para UM.

Por padrão, um PIN usado para o Outlook Voice Access é redefinido pelo sistema de correio de Unificação de mensagens ou voz se o número de tentativas fracassadas de entrar excede 5. Os usuários também podem redefinir seus pinos usando os recursos de Unificação de mensagens incluídos com o Outlook Web App ou o Outlook 2010 ou posteriores ou usando Outlook Voice Access de um telefone.


> [!TIP]
> O texto inserido nesta caixa está limitado a 512 caracteres e pode incluir texto HTML simples.



Para tarefas adicionais relacionadas à segurança do PIN do Outlook Voice Access, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para acrescentar texto a mensagem de email enviada aos usuários quando o PIN é redefinido

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **texto da mensagem**, na caixa de texto para **quando o Outlook Voice Access PIN de um usuário é redefinido**, insira o texto que você deseja incluir na mensagem de email enviada quando o PIN de um usuário é redefinido.

4.  Clique em **Salvar**.

## Usar o Shell para adicionar texto a mensagem de email enviada aos usuários quando o PIN é redefinido

Este exemplo inclui o texto adicional, "não compartilhar seu PIN com outros usuários. Isso pode resultar em ação disciplinar", na mensagem de email enviada aos usuários que estão associados com o de diretiva de caixa de correio de Unificação de mensagens `MyUMMailboxPolicy` quando o PIN é redefinido.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

