---
title: 'Excluir uma política de caixa de correio de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Excluir uma política de caixa de correio de Unificação de mensagens
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50556284
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Excluir uma política de caixa de correio de Unificação de mensagens

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-05_

Quando você exclui uma diretiva de caixa de correio de Unificação de mensagens (UM), a diretiva de caixa de correio de Unificação de mensagens ficarão mais disponível a ser associado a destinatários que estão sendo habilitados para Unificação de mensagens. Você não pode excluir uma política de caixa de correio UM se é referenciado por qualquer caixa de correio habilitado e você não pode excluir um plano de discagem de UM, se uma diretiva de caixa de correio de UM estiver associada ele.

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para excluir uma política de caixa de correio de Unificação de mensagens

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, na barra de ferramentas, clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Use o Shell para excluir uma política de caixa de correio de Unificação de mensagens

Este exemplo exclui uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

