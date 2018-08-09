---
title: 'Texto para clientes de email sem o gerenciamento de direitos do Windows'
TOCTitle: Especificar o texto a ser exibido para os clientes de email que não há suporte para gerenciamento de direitos do Windows
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52058481
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Especificar o texto a ser exibido para os clientes de email que não há suporte para gerenciamento de direitos do Windows

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode especificar o texto que será enviado a um usuário quando recebem uma mensagem de voz protegida, mas seu cliente de email não tem suporte para gerenciamento de direitos de informação (IRM) ou o Windows Rights Management.

Caixa postal protegida pode ser acessada apenas por clientes de email que oferecem suporte ao gerenciamento de direitos do Windows ou quando um usuário habilitado para Unificação de mensagens usa Outlook Voice Access para acessar uma mensagem de voz protegido.

Caixa postal protegida é criptografada. Quando uma mensagem de voz estiver protegida:

  - A mensagem é marcada como particular no Microsoft Outlook e Outlook Web App.

  - A mensagem de voz pode ser aberta apenas pelo destinatário pretendido.

  - O destinatário pode responder a mensagem de voz, mas não pode encaminhá-la a uma pessoa que não estava incluída na mensagem de voz original.

Se uma mensagem de voz protegida é enviada a alguém cujo cliente de email não é compatível com Windows Rights Management e não está acessando a mensagem usando Outlook Voice Access, uma mensagem de email será enviada a eles que inclui o texto especificado. Esse texto deve incluir instruções sobre o que deve fazer parte chamada possam receber a mensagem de voz protegida.

Para conhecer tarefas de gerenciamento adicionais relacionadas a procedimentos de Caixa Postal Protegida, consulte [Procedimentos de caixa postal protegidos](protected-voice-mail-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAT para especificar o texto a ser exibido para os clientes de email que não há suporte para gerenciamento de direitos do Windows

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **protegidos caixa postal**, sob a **mensagem para enviar aos usuários que não têm suporte do Windows Rights Management**, digite o texto da mensagem na caixa de texto.

4.  Clique em **Salvar**.

## Use o Shell para especificar o texto a ser exibido para os clientes de email que não há suporte para gerenciamento de direitos do Windows

Este exemplo especifica o texto a ser exibido aos usuários associados com a diretiva de caixa de correio de Unificação de mensagens denominada `MyUMMailboxPolicy` com clientes de email que não há suporte para gerenciamento de direitos do Windows.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

