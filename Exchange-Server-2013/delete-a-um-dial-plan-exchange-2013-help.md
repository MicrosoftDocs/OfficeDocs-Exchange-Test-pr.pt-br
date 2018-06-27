---
title: 'Excluir um plano de discagem de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Excluir um plano de discagem de Unificação de mensagens
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 50486619
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Excluir um plano de discagem de Unificação de mensagens

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-11_

Você pode excluir um plano de discagem de Unificação de mensagens (UM) existente. Quando você exclui UM plano de discagem, ela não ficarão mais disponível para gateways IP de UM, diretivas de caixa de correio de Unificação de mensagens, e grupos de busca de UM. Você não pode excluir um plano de discagem UM se ela tem referenciado pelo associados a políticas de caixa de correio de UM, atendentes automáticos, gateways IP de UM ou grupos de busca de UM.

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para excluir um plano de discagem existente

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de Unificação de mensagens que você deseja excluir e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  Na página aviso, clique em **Sim**.

## Use o Shell para excluir um plano de discagem existente

Este exemplo exclui um plano de discagem de UM chamado `MyUMDialPlan`.

    RemoveUMDialplan -identity MyUMDialPlan

