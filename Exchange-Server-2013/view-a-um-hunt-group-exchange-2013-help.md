---
title: 'Exibir um grupo de busca de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Exibir um grupo de busca de Unificação de mensagens
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50556314
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir um grupo de busca de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-05_

Quando você exibe as propriedades de um grupo de busca de Unificação de mensagens (UM), você pode exibir as propriedades associadas com um único grupo de busca UM ou todos os grupos de busca UM associado a um único gateway IP de UM. Se nenhum dos parâmetros for especificado, todos os grupos de busca de Unificação de mensagens serão retornados. Você não pode usar o EAC para exibir UM propriedades do grupo de busca; Você deve usar o Shell.

Após ter sido criado um grupo de busca de Unificação de mensagens, as configurações definidas não podem ser alteradas. Se você quiser alterar uma configuração, como o identificador piloto de um UM grupo de busca, você deve excluir o grupo de busca existente e criar um novo grupo de busca de Unificação de mensagens que possui as configurações corretas.

Para tarefas adicionais relacionadas a grupos de busca de UM, consulte [Procedimentos de grupo de busca de Unificação de mensagens](um-hunt-group-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: menos de 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de busca da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme se um gateway UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme que um grupo de busca de UM foi criado. Para obter etapas detalhadas, consulte [Criar um grupo de busca de UM](create-a-um-hunt-group-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para exibir as propriedades de um grupo de busca de Unificação de mensagens

Este exemplo exibe todos os grupos de busca da UM da floresta do Active Directory.

    Get-UMHuntGroup

Este exemplo exibe os detalhes de um grupo de busca de UM chamado `MyUMHuntGroup` em uma lista formatada.

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List


> [!TIP]
> Quando você estiver usando o cmdlet <STRONG>Get-UMHuntGroup</STRONG> , você não pode inserir apenas o nome do grupo de busca de Unificação de mensagens. Você também deverá incluir o nome do gateway IP de UM que está associado ao grupo de busca de Unificação de mensagens.


