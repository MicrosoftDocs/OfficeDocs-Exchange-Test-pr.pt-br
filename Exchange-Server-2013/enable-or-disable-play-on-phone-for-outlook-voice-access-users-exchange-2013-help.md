---
title: 'Habilitar ou desabilitar tocar no telefone para usuários do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar tocar no telefone para usuários do Outlook Voice Access
ms:assetid: d3281a97-6fc6-42a3-855f-1af1184a644a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351161(v=EXCHG.150)
ms:contentKeyID: 52058500
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar tocar no telefone para usuários do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-12_

Você pode habilitar ou desabilitar tocar no recurso de telefone para os usuários associados a uma diretiva de caixa de correio de Unificação de mensagens (UM). Essa opção é habilitada por padrão e permite que os usuários participar sua voz mensagens de email de qualquer telefone. Essa opção não está disponível para usuários habilitados para Unificação de mensagens que têm uma caixa de correio em um servidor deExchange Server 2007Microsoft.

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

## Usar o EAC para habilitar ou desabilitar tocar no telefone

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM**, marque ou desmarque a caixa de seleção ao lado de **Permitir tocar no telefone para caixa postal**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar tocar no telefone

Este exemplo habilita a tocar no recurso de telefone para usuários que estão associados a de diretiva de caixa de correio de Unificação de mensagens `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowPlayOnPhone $true

Este exemplo desabilita a tocar no recurso de telefone para usuários que estão associados a de diretiva de caixa de correio de Unificação de mensagens `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowPlayOnPhone $false

