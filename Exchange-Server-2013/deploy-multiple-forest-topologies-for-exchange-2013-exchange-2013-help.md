---
title: 'Implantar várias topologias de floresta do Exchange 2013: Exchange 2013 Help'
TOCTitle: Implantar várias topologias de floresta do Exchange 2013
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51407922
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantar várias topologias de floresta do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico fornece uma visão geral da implantação do Microsoft Exchange Server 2013 em várias topologias de floresta. Você encontrará informações sobre os seguintes assuntos:

  - **Suporte a várias topologias de floresta** Exchange 2013 suporta dois tipos de várias topologias de floresta: floresta de recursos e entre florestas.   

  - **Sincronização da GAL**   Se você tiver um ambiente entre florestas, você precisará garantir que GAL em qualquer floresta determinado contém destinatários de email de outras florestas.

  - **Mover caixas de correio entre florestas**    Os cmdlets **New-MoveRequest** e **New-MigrationBatch** em Exchange Management Shell pode ajudar a mover caixas de correio de uma floresta para outro.

  - **Noções básicas sobre a administração de várias florestas**   Saiba mais sobre o modelo de permissões para configurar e gerenciar as permissões entre seus florestas.

## Suporte a várias topologias de floresta

Exchange 2013 suporta os seguintes tipos de várias topologias de floresta:

  - **Entre florestas**   Uma topologia entre florestas é aquele com várias florestas Exchange. Aqui está uma visão geral do que você precisa fazer para implantar Exchange 2013 em uma topologia com uma floresta de várias:
    
    1.  Você deve primeiro instalar Exchange 2013 em cada floresta. Para obter mais informações, consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md).
    
    2.  Em seguida, você deve sincronizar os destinatários em cada uma das florestas, para que a lista de endereços Global (GAL) em cada floresta contém os usuários de todas as florestas sincronizados. Consulte a seção "Sincronização da GAL" abaixo para obter mais detalhes.
    
    3.  Finalmente, você deve configurar o serviço de disponibilidade para que usuários em uma floresta podem exibir os dados de disponibilidade para usuários em outra floresta. Para obter mais informações, consulte [Configurar o serviço de disponibilidade para topologias entre florestas](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md).
    
    Para obter detalhes sobre como implantar o Exchange 2013 em uma topologia entre florestas, consulte [Implantar o Exchange 2013 em uma topologia entre florestas](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md).

  - **Floresta de recursos**   Uma topologia de floresta de recursos é um com uma floresta de Exchange e uma ou mais florestas de contas de usuário. Aqui está uma visão geral do que você precisa fazer para implantar Exchange 2013 em uma topologia com uma floresta de recursos:
    
    1.  Você deve ter uma floresta com Exchange instalado. Na floresta Exchange, você deve desabilitou as contas de usuário que têm Exchange caixas de correio.
    
    2.  Você deve ter pelo menos uma floresta que contém as contas de usuário. Floresta deve *não* ter Exchange instalado.
    
    3.  Em seguida, você deve associar as contas de usuário desabilitadas na floresta Exchange com as contas de usuário na floresta de contas.
    
    Para obter detalhes sobre como implantar o Exchange 2013, em uma topologia de floresta de recursos, consulte [Implantar o Exchange 2013 em uma topologia de floresta de recursos do Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## Sincronização da GAL

Por padrão, um GAL contém destinatários de email de uma única floresta. Se você tiver um ambiente entre florestas, é recomendável usando o Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) para garantir que a GAL em qualquer determinados floresta contém destinatários de email de outras florestas. ILM 2007 FP1 cria usuários de email que representam os destinatários de outras florestas, permitindo que os usuários para exibi-los na GAL e enviar emails. Por exemplo, usuários em exibido com uma floresta como um usuário de email na floresta B e vice-versa. Os usuários da floresta de destino, em seguida, podem selecionar o objeto de usuário de email que representa um destinatário em outra floresta para enviar email.

Para habilitar a sincronização da GAL, crie agentes de gerenciamento que importam usuários, contatos e grupos habilitados para email de serviços designados do Active Directory em um metadiretório centralizado. No metadiretório, os objetos habilitados para email são representados como usuários de email. Os grupos são representados como contatos sem nenhum membro associado. Em seguida, os agentes de gerenciamento exportam esses usuários de email para uma unidade organizacional na floresta de destino especificada.

Para obter mais informações sobre o Forefront Identity Manager (FIM), consulte [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864).

## Mover caixas de correio entre florestas

Em uma topologia entre florestas, convém mover caixas de correio de uma floresta para outro. Para fazer isso, você deve usar o cmdlet **New-MoveRequest** ou **New-MigrationBatch** em Exchange Management Shell. Para obter mais informações sobre como mover caixas de correio entre florestas, consulte os tópicos a seguir:

  - [Preparar a caixas de correio para solicitações de movimentação entre florestas](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Prepare a caixas de correio para movimentações entre florestas usando o script de preparação-MoveRequest.ps1 no Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [Preparar a caixas de correio para movimentações entre florestas usando código de exemplo](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## Noções básicas sobre a administração de várias florestas

Exchange 2013 usa a nova funcionalidade de permissões para gerenciar seus ambientes de várias florestas.

Exchange 2013 usa um modelo de permissões de controle de acesso com base da função (RBAC). Os grupos de função de gerenciamento que os administradores são membros e as diretivas de atribuição de função de gerenciamento que os usuários finais são atribuídos, determinam o que cada administrador e usuário final podem fazer. Para entender as várias permissões de floresta, você precisa estar familiarizado com o RBAC. Para obter mais informações sobre a atribuição de função e grupos de função e RBAC políticas em particular, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

Você pode usar o modelo de permissões de RBAC para configurar e gerenciar as permissões entre seus florestas. Para obter mais informações sobre permissões de várias florestas, consulte os tópicos a seguir:

  - [Compreendendo as permissões de várias florestas](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [Gerenciar grupos de função vinculado](manage-linked-role-groups-exchange-2013-help.md)

  - [Criar grupos de função vinculado que espelham grupos de função internos](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

