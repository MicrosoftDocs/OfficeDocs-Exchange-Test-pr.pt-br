---
title: 'Configurar caixa postal protegida de chamadores autenticados: Exchange 2013 Help'
TOCTitle: Configurar caixa postal protegida de chamadores autenticados
ms:assetid: f69e94a7-9768-4445-9ded-e78d732bd623
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423560(v=EXCHG.150)
ms:contentKeyID: 52058554
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar caixa postal protegida de chamadores autenticados

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode configurar a Unificação de mensagens para atender uma chamada de entrada e, em seguida, determine se ele se aplica proteção mensagens de caixa postal usando criptografia. Quando uma mensagem de voz estiver protegida:

  - A mensagem é marcada como particular no Microsoft Outlook e Outlook Web App.

  - A mensagem de voz pode ser aberta apenas pelo destinatário pretendido.

  - O destinatário pode responder a mensagem de voz, mas não pode encaminhá-la a uma pessoa que não estava incluída na mensagem de voz original.

Essa configuração se aplica às mensagens de voz enviadas aos usuários habilitados para Unificação de mensagens quando eles não atender o telefone dela. Essa configuração também se aplica quando os chamadores entrar com suas caixas de correio usando Outlook Voice Access e, em seguida, criar e enviar uma mensagem de voz.

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

## Usar o EAC para configurar a caixa postal protegida de chamadores autenticados

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **protegidos caixa postal**, em **mensagem de voz Protect dos chamadores autenticados**, selecione uma das seguintes opções:
    
      - **Nenhum**   Use essa configuração se não quiser a proteção aplicada para as mensagens de voz enviadas para usuários habilitados para UM.
    
      - **Particular**   Use essa configuração quando você quiser que a Unificação de Mensagens aplique proteção somente para as mensagens de voz que tenham sido marcadas como particulares pelo chamador.
    
      - **Todas**   Use essa configuração se quiser que a Unificação de Mensagens aplique proteção a todas as mensagens de voz, incluindo aquelas não marcadas como privadas.

4.  Clique em **Salvar**.

## Use o Shell para configurar a caixa postal protegida de chamadores autenticados

Este exemplo protege mensagens de voz de todos os chamadores autenticados no de política de caixa de correio de Unificação de mensagens `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy ProtectAuthenticatedVoiceMail -All

