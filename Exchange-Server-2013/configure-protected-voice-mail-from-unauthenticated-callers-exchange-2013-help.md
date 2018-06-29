---
title: 'Configurar caixa postal protegida de chamadores de não-autenticados: Exchange 2013 Help'
TOCTitle: Configurar caixa postal protegida de chamadores de não-autenticados
ms:assetid: 106bfa0a-a0fa-4a1b-bd59-4b6df1d0d61d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335098(v=EXCHG.150)
ms:contentKeyID: 52058368
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar caixa postal protegida de chamadores de não-autenticados

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode configurar a Unificação de Mensagens para responder a uma chamada de entrada e determinar se você deve aplicar proteção a mensagens de caixa postal usando criptografia. Quando uma mensagem de caixa postal está protegida:

  - A mensagem está marcada como Particular no Microsoft Outlook e no Outlook Web App.

  - A mensagem de voz pode ser aberta apenas pelo destinatário pretendido.

  - O destinatário pode responder a mensagem de voz, mas não pode encaminhá-la a uma pessoa que não estava incluída na mensagem de voz original.

Essa configuração se aplica a mensagens de voz enviadas para usuários habilitados para UM quando eles não atendem ao telefone. Essa configuração também se aplica a mensagens de voz enviadas diretamente para usuários habilitados para UM, quando o chamador usa um atendedor automático de UM.

Para conhecer tarefas de gerenciamento adicionais relacionadas a procedimentos de Caixa Postal Protegida, consulte [Procedimentos de caixa postal protegidos](protected-voice-mail-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar a Caixa Postal Protegida de chamadores não autenticados

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de Caixa de Correio do UM** \> **Caixa postal protegida**, em **Proteger mensagem de voz de chamadores não autenticados**, selecione uma das seguintes opções:
    
      - **Nenhum**   Use essa configuração se não quiser a proteção aplicada para as mensagens de voz enviadas para usuários habilitados para UM.
    
      - **Particular**   Use essa configuração quando você quiser que a Unificação de Mensagens aplique proteção somente para as mensagens de voz que tenham sido marcadas como particulares pelo chamador.
    
      - **Todas**   Use essa configuração se quiser que a Unificação de Mensagens aplique proteção a todas as mensagens de voz, incluindo aquelas não marcadas como privadas.

4.  Clique em **Salvar**.

## Usar o EAC para configurar a caixa postal protegida de chamadores não autenticados

Este exemplo protege todas as mensagens de voz de todos os chamadores não autenticados na diretiva de caixa de correio da UM `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectUnauthenticatedVoiceMail -All

