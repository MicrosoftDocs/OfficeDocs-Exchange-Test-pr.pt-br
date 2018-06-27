---
title: 'Habilitar ou desabilitar o Outlook Voice Access para usuários: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar o Outlook Voice Access para usuários
ms:assetid: c0c244a0-ad2f-4adf-bc1f-1d55fd7ea2d5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351106(v=EXCHG.150)
ms:contentKeyID: 52058519
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o Outlook Voice Access para usuários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-12-12_

É possível habilitar ou desabilitar o acesso aos Outlook Voice Access para usuários habilitados para Unificação de mensagens que estão associados uma diretiva de caixa de correio de Unificação de mensagens (UM). Outlook Acesso de voz é um recurso usado pelos usuários habilitados para acessar suas caixas de correio através de um telefone. Por padrão, essa configuração estiver habilitada.

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar o Outlook Voice Access

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM**, marque ou desmarque a caixa de seleção ao lado de **Permitir que o Outlook Voice Access**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar o Outlook Voice Access

Este exemplo permite que os usuários que estão associados a UM política de caixa de correio `MyUMMailboxPolicy` usar Outlook Voice Access.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $true

Este exemplo impede que os usuários que estão associados a Unificação de mensagens da caixa de correio diretiva `MyUMMailboxPolicy` utilizem Outlook Voice Access.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $false

