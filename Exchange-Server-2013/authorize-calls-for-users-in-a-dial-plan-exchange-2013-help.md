---
title: 'Autorizar chamadas para usuários em um plano de discagem: Exchange 2013 Help'
TOCTitle: Autorizar chamadas para usuários em um plano de discagem
ms:assetid: 7c7fd0c4-4001-408e-b352-c49bac9f78cc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691175(v=EXCHG.150)
ms:contentKeyID: 51407887
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizar chamadas para usuários em um plano de discagem

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Você pode habilitar autorizações de discagem em um plano de discagem de Unificação de mensagens (UM). Autorizações de discagem em um plano de discagem são usadas para fazer chamadas telefônicas de país/região ou internacionais ou *discagem externa para*proibir que usuários não-autenticados do Outlook Voice Access. Discagem externa acontece quando Unified Messaging faz uma chamada de saída para um usuário depois que eles tenham chamado para um número de telefone do Outlook Voice Access que está configurado em um plano de discagem de UM. Quando você configura uma configuração de um UM plano de discagem da, que configuração se aplica a todos os usuários não-autenticados que ligam para um número do Outlook Voice Access.

Para conhecer tarefas de gerenciamento adicionais relacionadas à discagem externa, consulte [Permitindo que usuários façam chamadas de procedimentos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme que as regras de discagem do país/região e internacionais foram criadas em um plano de discagem de UM. Para obter etapas detalhadas, consulte [Criar regras de discagem para usuários](create-dialing-rules-for-users-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar autorizações de discagem em um plano de discagem de UM para grupos de regras de discagem do país/região

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, clique em **Configurar**.

3.  Na página de **Plano de discagem de UM** \> **autorização de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") sob **autorizados grupos de regras de discagem do país/região**.

4.  Na página **Selecionar grupos de regras de discagem para permitir**, selecione o grupo de regras de discagem, clique em **OK** e, em seguida, clique em **Salvar**.

## Usar o EAC para habilitar autorizações de discagem em um plano de discagem de UM para grupos de regras de discagem internacional

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, clique em **Configurar**.

3.  Na página de **Plano de discagem de UM** \> **autorização de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em **grupos de regras de discagem internacional de autorizados**.

4.  Na página **Selecionar grupos de regras de discagem para permitir**, selecione o grupo de regras de discagem, clique em **OK** e, em seguida, clique em **Salvar**.

## Use o Shell para habilitar autorizações de discagem do país/região e internacionais em um plano de discagem de UM

Este exemplo habilita o InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 e denominado `MyUMDialPlan`de plano de discagem de InternationalGroup2 autorizações de discagem em uma Unificação de mensagens.

    Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

